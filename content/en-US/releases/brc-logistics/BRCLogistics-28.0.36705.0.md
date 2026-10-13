---
title: BRCLogistics 28.0.36705.0
categories: [BRCLogistics, ReleaseNotes]
description: Fixes Ongoing, VeraCore and Logiwa requests being sent without the real password, adds Test Connection to the setup card, recovers EasyCom exchange orders that were never created, and fixes Ongoing status updates missed when pagination is enabled.
date: 2026-10-13
---

This release fixes an issue introduced in 28.0.36303.0. Customers using the Ongoing, VeraCore or Logiwa integration should install it as soon as possible.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| WMS password sent correctly again | Ongoing, VeraCore and Logiwa requests created with 28.0.36303.0 were sent with a masked placeholder instead of the password, so the warehouse system rejected them. They are now sent with the real password. | 31545 |
| Test Connection | A new action on the BRC Logi Setup card checks that the warehouse system accepts the configured credentials, without creating or changing anything there. | 32017 |
| Recovery of missing exchange orders | A new job queue routine creates exchange orders that were never created for closed returns. Excluded exchange lines in EasyCom no longer close the return. | 30325 |
| Ongoing status updates with pagination | With Ongoing pagination enabled, Shipment and Receival Status Requests no longer miss status changes on orders below the page cursor. | 32025 |

## Detailed Feature Information

---

### WMS password sent correctly again (#31545)

28.0.36303.0 stopped storing the warehouse system password in the saved request data. The password was replaced by a placeholder, and the real password was meant to be added back when the request is sent. For Ongoing, VeraCore and Logiwa this did not happen, so these requests reached the warehouse system with the placeholder and were rejected.

This version adds the real password when the request is sent, for every request type. The saved request data still does not hold the password. A setup with a blank password sends an empty password, as before 28.0.36303.0.

**After installing:**

- Requests that failed are still marked **Document Not Sent** and are sent again by the normal job queue. No data needs to be corrected.
- Warehouse transactions that reached the maximum error count while the issue was present need their error count reset before they are retried.
- Run **Test Connection** on the setup to confirm the connection (see below).

#### Related PR

- PR 16134 (BRCLogistics): #31545 BRC Logistics hotfix: send the real WMS password, not the placeholder

---

### Test Connection (#32017)

A new **Test Connection** action on the BRC Logi Setup card checks that the warehouse system accepts the credentials on the setup and shows the result. Nothing is created or changed in the warehouse system.

The test uses the same code as the integration's real requests, so it fails whenever real requests would fail.

Supported in this version:

- **Ongoing:** sends a read-only inventory query for an article that does not exist.
- **Integrations that log in for an access token:** 3PL Central, Bitlog (including the separate WMS login when a WMS API URL is set), Deposco, Logiwa, Nyce WS, Posti, PrimePenguin, ReclaimIt, Schipt, ShipHero, Speedgroup and VeraCore. The test requests a token with the setup's credentials.

For other integrations, the action shows that Test Connection is not supported yet. More integrations will follow.

The result is also sent to BrightCom's Application Insights as event **BRCLGS-0005**. It holds only the logistics code, the integration and whether the test succeeded, failed or is not supported. No error text and no credentials are sent.

#### Related PR

- PR 16136 (BRCLogistics): #32017 BRC Logistics: Test Connection for WMS credentials

---

### Recovery of missing exchange orders (#30325)

When the return flow failed partway, a closed return with exchange lines could end up without its exchange order, and no error was shown. The customer's replacement was then never sent.

#### Exchange order recovery job (#30744)

A new job queue routine finds closed returns that have exchange lines but no exchange order, and creates the missing exchange order.

- Run it with the job queue parameter **`<Logistics Code>,EXCHRECOVERY`** on **BRC Logi Whse. Job Scheduler**.
- **Exchange Order Recovery Period** (BRC Logi Setup) sets how far back it looks, for example `-30D`. Blank means 30 days. It never looks further back than **Delete Old Transactions after**.
- **Exchange Order Recovery Max. per Run** (BRC Logi Setup) limits how many returns are recovered per run. 0 means 1000.
- **Skip Exchange Order Recovery** on a warehouse transaction excludes that return, for example when the exchange was handled manually.
- A return is skipped when an exchange order transaction or an open exchange sales order already exists, so no duplicates are created.
- The job never reopens a return or changes an existing exchange transaction. Failures are written once to the error log.

#### Other changes in the return flow

- **EasyCom:** an excluded exchange line no longer closes the return. The line is marked as not returned and the return stays open, so the exchange order is still created.
- **Original order not yet invoiced:** creating an exchange order now waits, with a readable error description and without raising the error count. When the original order only has prepayment invoices or no posted shipment, the error names the order.
- A new exchange transaction now always starts without errors.

#### Related PR

- PR 16130 (BRCLogistics): #30325 Recover missing exchange orders and keep exchange lines open in EasyCom

---

### Ongoing status updates with pagination (#32025)

With Ongoing pagination enabled (**Ong Order Page Size** or **Ong InOrder Page Size** above 0), Shipment and Receival Status Requests could permanently miss status updates:

- A completed run moved the "changed since" time forward to the time of its last page. An order whose status changed while the run was paging, on a page already read, was then never picked up.
- A page whose processing failed, even weeks earlier, made every later run start at that page's order ID, so orders with a lower ID were skipped.

Now a completed paginated run moves the "changed since" time forward to when the run started, and a run only resumes from the most recent run's last page. Requests without pagination are unchanged.

**After installing:** the first Shipment and Receival Status Request run starts over from the first page once and reads the current window again. Some orders are processed again; nothing is lost.

#### Related PR

- PR 16153 (BRCLogistics): #32025 Ongoing pagination: advance the watermark to the run start, resume only the latest run

## Breaking Changes

No breaking changes in this release.

Behaviour changes to be aware of:

- **EasyCom excluded exchange lines.** An excluded exchange line now keeps the return open, where before it closed it.
- **Exchange orders for orders not yet invoiced** wait for the invoice instead of failing.

## Bugfixes

- Ongoing, VeraCore and Logiwa requests are rejected by the warehouse system because the password placeholder is sent instead of the password (#31545)
- Exchange orders are silently not created when the return flow fails (#30325)
- Ongoing Shipment and Receival Status Requests miss status changes when pagination is enabled (#32025)
