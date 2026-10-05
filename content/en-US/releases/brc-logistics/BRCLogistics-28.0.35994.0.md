---
title: BRCLogistics 28.0.35994.0
categories: [BRCLogistics, ReleaseNotes]
description: Application Insights telemetry for failing integrations, an option to stop sending Return Order Requests per logistics setup, and two fixes for Bitlog transaction import and insufficient-stock adjustments.
date: 2026-10-05
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Telemetry for failing integrations | BRC Logistics now emits Application Insights telemetry when a warehouse transaction fails, reaches its maximum error count, or is closed without producing a document in Business Central. | 30054 |
| Optional Return Order Requests per WMS integration | A new **Send Return Order Requests** setting on BRC Logistics Setup controls whether Return Order Requests are sent for each logistics setup, preventing duplicate return flows where returns already arrive through another channel. | 25607 |

## Detailed Feature Information

---

### Telemetry for failing integrations (#30054)

BRC Logistics processes warehouse transactions in protected calls: when one fails, the error is caught, written to the transaction, and its error count is raised, and the job moves on. That keeps processing running, but it also means these errors never reached any monitoring. Once a transaction reached its **Error Max Count** it was quietly left out of all later runs, and the only trace was a field on the transaction itself.

From this release, BRC Logistics emits custom telemetry for these events. Each event has a stable event ID, so alerts and dashboards built on them keep working across versions:

| Event ID | Severity | Raised when |
| --- | --- | --- |
| `BRCLGS-0001` | Warning | An error on a warehouse transaction is caught and suppressed. Raised once per failure: it is not repeated on every retry, and is raised again only after the transaction has succeeded or its errors have been reset. |
| `BRCLGS-0002` | Error | A transaction's error count reaches the **Error Max Count** on BRC Logistics Setup, so it will not be processed again without manual action. Not raised when Error Max Count is 0. |
| `BRCLGS-0003` | Error | A transaction is closed without an **Applies-to Document No.**, that is, the integration finished without producing anything in Business Central. Item Adjustment, Item Balance and Item Movement transactions, and the setup's **Doc Type for Check**, are excluded because they do not apply to a document. |
| `BRCLGS-0004` | Error | A Return Order transaction with one or more **Exchange Item** lines is closed without a matching Exchange Order, so the replacement item will not be sent. |

Every event carries these custom dimensions:

- `brcLogisticsCode` - the logistics setup the transaction belongs to
- `brcDocumentType` and `brcDocumentNo` - the warehouse transaction
- `brcProcessName` - `Connector Error Suppression` for events 0001 and 0002, `Warehouse Header Closed` for events 0003 and 0004
- `brcErrorCount` (events 0001 and 0002) and `brcErrorMaxCount` (event 0002)

The events are classified as system metadata. **The error text is deliberately not sent**, because it can contain names, addresses and item descriptions. To see the actual error, open the transaction in Business Central.

#### Where the telemetry goes

The events are emitted to both of these destinations:

- **Your own environment's Application Insights resource**, if one is configured for the environment in the Business Central admin center. Partners and customers can query and alert on the events there, in the same way as on Microsoft's own telemetry.
- **The BRC Logistics app's Application Insights resource**, set in the app manifest, which lets BrightCom spot a fault that affects several customers at once.

Nothing needs to be set up and there is no new setup field: telemetry is on by default and does not change how transactions are processed. If no Application Insights resource is configured for the environment, nothing is sent there.

#### Where it is emitted

The events are emitted from the central warehouse transaction job and from the error handling in every connector's check-for-updates, file import and file export processing. They are also emitted when updating shipments, receipts, assemblies and item balances back to documents. When a request is sent or processed successfully, or when errors are reset on **BRC Logi Whse. Transactions** or the transaction card, the transaction is marked as clear, so that its next failure is reported again.

A new system field, **Error Telemetry Reported**, on the warehouse transaction keeps track of whether the current failure has already been reported.

#### Related work items and PRs

- Requirement #30246: time tracking for this feature
- PR 15490 (BRCLogistics): Feature/30054EmitTelemetry

---

### Optional Return Order Requests per WMS integration (#25607)

Some return setups do not need Business Central to send Return Order Requests to the WMS. For example, returns may already be created in Business Central by a webhook from the return system. When both mechanisms are active, the same return can be processed twice, and someone has to correct it by hand.

#### Send Return Order Requests setting (#27791)

**BRC Logistics Setup** has a new field, **Send Return Order Requests**, on the **Document** tab next to the other return settings. It applies to each logistics setup (per WMS connection), not to the whole company.

- **On (default):** Return Order Requests are created and sent exactly as before.
- **Off:** any Return Order Request created for that logistics setup is **cancelled automatically**: its document status is set to **Document Cancelled** as it is created, so it is never sent. No error message or log entry is written, because the cancellation is intended.
- While the setting is off, a Return Order Request for that logistics setup **cannot be un-cancelled**. Any change to such a request sets its status back to **Document Cancelled**.

The setting only affects Return Order Requests. Inbound returns and other request types, such as Picking Status Requests, are not affected.

New logistics setups get the field switched on. When you upgrade, an upgrade step switches it on for all existing logistics setups, so nothing changes until you turn it off.

#### Related work items and PRs

- Requirements #30199 and #30200: time tracking for this feature
- PR 15793 (BRCLogistics): Requirement/27791 Send Return Order Requests setting

## Breaking Changes

No breaking changes in this release.

**Worth knowing:**

- **New telemetry:** BRC Logistics now emits Application Insights events `BRCLGS-0001` to `BRCLGS-0004` (see above). If your environment has Application Insights configured, these events will start appearing there. They do not contain the error text.
- **Turning off Send Return Order Requests cancels without a message:** Return Order Requests for that logistics setup are cancelled with no error or log entry. This also applies to Return Order Requests that are still open when you turn the setting off: they are set to **Document Cancelled** the next time they are changed. Turning the setting back on affects only new requests. Requests already cancelled stay cancelled.

## Bugfixes

- **Bitlog transaction import: logistics setup lookup for moves (PR 15744, #27687).** When importing Bitlog transactions whose warehouse does not match the **Identifier** of a logistics setup, BRC Logistics falls back to a default logistics setup. For **Move** transactions this fallback no longer requires a default setup (one with a blank Identifier), because a move can come from any warehouse. The first enabled Bitlog logistics setup is now used instead. In addition, the fallback now only considers logistics setups whose **Integration Engine** is Bitlog, so a transaction can no longer be assigned to a setup for a different WMS.
- **Insufficient-stock auto-fix: Gen. Bus. Posting Group from the reason code (PR 15825, #31509).** When the insufficient-stock auto-fix creates an item journal line, the **Gen. Bus. Posting Group** of the logistics reason set in **Insuff. Stock Reason Code** on BRC Logistics Setup is now applied to the line. This takes priority over the posting group from the journal batch. Previously the reason's posting group was not used, so in localizations without a batch-level posting group the adjustment could be posted with no Gen. Bus. Posting Group or with the wrong one.
