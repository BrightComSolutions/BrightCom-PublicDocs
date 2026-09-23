---
title: BRC Logistics 25.0.34805.0
categories: [BRCLogistics, ReleaseNotes]
description: Full error history per warehouse document, faster inventory balance loads, duplicate-safe line identification, and optional automatic recovery from insufficient stock on item movements.
date: 2026-09-22
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Error history per warehouse document | Every failed processing attempt is now kept as its own entry with message, callstack and timestamp, instead of only the most recent error text. | 18451 |
| Skip old items in the inventory balance load | An optional date formula leaves long-dormant items out of the inventory-per-warehouse load, cutting the runtime of the full balance job. | 18451 |
| Duplicate-safe line identification | A warehouse line can no longer be matched to a document line another line on the same document has already claimed. | 29059 |
| Automatic recovery from insufficient stock | Opt-in: item movement lines that fail on insufficient stock get a merged positive adjustment posted and are retried on the next run. | 30312 |

## Detailed Feature Information

---

### Error history per warehouse document (#18451)

Until now a failing warehouse document kept only its **last** error text on the header, so an intermittent failure overwrote whatever came before it and there was nothing to look back at.

A new **BRC Logistics Error Entry** table records each failed processing attempt separately, with:

- the error message and the error callstack
- the date and time of the attempt
- the document and, where relevant, the line it belongs to

The entries are reachable from the **Error Try Count** field on a warehouse transaction, which now opens the new **BRC Logistics Error Entries** page filtered to that document. Entries are removed together with the warehouse document, so no orphaned history is left behind.

This makes a recurring failure diagnosable from inside Business Central rather than from the previous run's error text alone.

> **Note:** a defect in this version means only the first error per document line is recorded; a repeat failure on the same line reports a duplicate-key error instead of being added to the history. Fixed in 25.0.34865.0.

---

### Skip old items in the inventory balance load (#18451)

Some customers ran full inventory balance loads that took several hours, because the job walked every item in the database even when most of them had never moved.

A new **Skip Item Balance on Old Items** date formula on BRC Logistics Setup sets a cut-off. An item is left out of the load when **both** of the following hold:

- it was created before the cut-off date, and
- it has no item ledger entries at all

Items with any transaction history are always included, whatever their age. Leaving the field blank keeps the previous behaviour and loads every item.

---

### Duplicate-safe line identification (#29059)

When warehouse lines were matched against purchase, sales and transfer lines, each warehouse line searched independently. Two warehouse lines for the same item, variant and quantity could therefore both latch onto the *same* document line — which showed up downstream as a shipment notice reporting Finished and then a further line arriving afterwards, leaving the order awkward to invoice.

Identification now checks whether a candidate document line has already been claimed by another identified warehouse line on the same document, and moves on to the next candidate if it has. Purchase line identification was additionally moved into its own routine and now skips warehouse lines that are already identified, so re-running identification does not reshuffle earlier matches.

---

### Automatic recovery from insufficient stock on item movements (#30312)

Customer-driven development adds an **opt-in** recovery path for item movement lines that fail because the stock is not there.

When enabled, after the per-line movement run BRC Logistics will:

1. collect the lines that failed with an insufficient-stock error (Swedish and English messages are both recognised)
2. group them by item, variant and location, summing the quantity each group is short
3. post **one merged positive adjustment** per group, topping the balance up to exactly cover the pending demand
4. re-open those lines so they are retried on the next run

Configuration is on the BRC Logistics Setup card:

- **Autofix Insufficient Stock for Item Movement** — the on/off switch; recovery only runs when this is on *and* a journal template and batch are set
- **Insufficient Stock Adj. Journal Template** / **Batch** — where the adjustments are created
- **Insufficient Stock Reason Code** — optional reason code stamped on the adjustment
- **Insufficient Stock Max Auto-Fixes** — how many times one document may be auto-fixed before it is left to fail normally (0 uses the default of 3)

Safeguards worth knowing about:

- **Items with item tracking are never auto-adjusted**, since the lot or serial information is not available at this point; those lines fail normally
- a group whose inventory turns out to be sufficient, whose item cannot be found, or whose source location cannot be resolved is skipped, and the reason is written to the affected line's error message rather than passing silently
- the adjustment batch is cleared of leftover unposted lines before and after a failed posting, so nothing is double-counted on the next run
- the per-document recovery counter caps the retries, so an unresolvable shortage escalates into a normal error instead of looping

The feature is off by default, so existing installations see no change until it is configured.

#### Related PRs

- PR 15405 (BRCLogistics): Identify line for BRC Connect — error entries, old-item skip, duplicate-safe identification
- PR 15417 (BRCLogistics): Automatic item movement recovery on insufficient stock

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Daylight saving time is now taken into account when the Unix timestamp for the SMD shared access signature is generated. During DST the token was built from an offset that was one hour out.
