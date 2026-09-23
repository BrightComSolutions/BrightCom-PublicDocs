---
title: BRC Logistics 25.0.34843.0
categories: [BRCLogistics, ReleaseNotes]
description: Inbound Ongoing WMS shipment and receival status requests can now retrieve large result sets in sequential pages instead of one oversized response.
date: 2026-09-23
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Paginated retrieval from Ongoing WMS | Opt-in: Shipment Status and Receival Status requests fetch large result sets in sequential pages, so a high-volume run no longer depends on a single oversized response. | 30025 |

## Detailed Feature Information

---

### Paginated retrieval from Ongoing WMS (#30025)

Customers running Ongoing WMS at high volume have been hitting HTTP timeouts on the Ongoing side and processing failures in Business Central when an inbound response grows past what the job queue can handle comfortably. A captured production Shipment Status Request covering a two-day window returned **87 MB across 2,811 orders** — roughly 31 KB per order — in a single response.

BRC Logistics now supports Ongoing's own keyset pagination on the two inbound requests that grow without bound:

| Request | Retrieved in pages of |
| --- | --- |
| Shipment Status Request | **Ongoing Order Page Size** orders per call |
| Receival Status Request | **Ongoing Inbound Order Page Size** inbound orders per call |

Instead of asking for the whole window at once, the connector walks the result set a page at a time and processes each page independently, which keeps memory and execution pressure in the job queue flat regardless of how much the window contains.

#### Configuration

Two new fields on the BRC Logistics Setup card, both **0 by default, which means pagination is off**:

- **Ongoing Order Page Size** — how many orders each Shipment Status Request asks for
- **Ongoing Inbound Order Page Size** — how many inbound orders each Receival Status Request asks for

At 0 the request sent to Ongoing is byte-for-byte what the previous build sent, so no existing integration changes behaviour until a page size is deliberately set. **250 is a reasonable starting point** for a high-volume warehouse.

#### Behaviour worth knowing about

- **A partial run will not skip data.** The change-tracking watermark is only advanced once a run has read its window to the end. If a run stops part-way, the window is retried on the next run rather than being passed over.
- **Long backlogs drain across runs.** A single run stops after 20 pages and records where it got to; the next scheduled run picks the cursor up from there. A large catch-up therefore spreads over several runs instead of monopolising the Logistics job queue.
- **Response handling is unchanged.** The existing response parsers were deliberately left alone — page bookkeeping reads the record count and the highest order id straight off the stored response. Transaction visibility, retry handling and error logging on the WMS transaction pages work exactly as before.
- **Non-Ongoing engines are untouched.** Only the Ongoing inbound path is affected; outbound requests and outbound synchronisation are out of scope.

#### Not included in this phase

**Balance Request is deliberately excluded.** Depending on setup and correction mode it resolves to four different API calls, two of which return orders rather than inventory, so it needs its own handling and is planned separately.

#### Rolling this out on a customer

1. Enable the order side first — set **Ongoing Order Page Size** and leave **Ongoing Inbound Order Page Size** at 0 until it has run cleanly for several cycles.
2. Confirm that no two job queue entries run CHECK concurrently for the same connection and document type.

#### Related PRs

- PR 15433 (BRCLogistics): #30025 Paginate responses from Ongoing WMS (Phase 1)

## Breaking Changes

No breaking changes in this release. Pagination is off by default and the emitted request is unchanged until a page size is configured.

## Bugfixes

No bugfixes in this release.
