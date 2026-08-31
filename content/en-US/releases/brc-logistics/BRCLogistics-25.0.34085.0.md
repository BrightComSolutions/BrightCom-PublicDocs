---
title: BRC Logistics 25.0.34085.0
categories: [BRCLogistics, ReleaseNotes]
description: Item balance import now clears old journal lines per location instead of across all locations.
date: 2026-08-27
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Item balance import respects location | Cleanup of previous item journal lines during an inventory balance import is now scoped to the location being imported, so balances for other locations are left intact. | 22558 |

## Detailed Feature Information

---

### Item balance import respects location (#22558)

When an inventory balance was imported, the routine that removes previously created item journal lines matched only on document number, item, variant, unit of measure, batch, and series — but not on **location**.

For customers running inventory counts per location, importing a balance for one location therefore removed the pending journal lines belonging to other locations for the same item, so those counts were lost before they could be posted.

The cleanup now includes the **Location Code** in its filter, so only journal lines for the location actually being imported are removed. When no location is supplied the previous behavior is retained, keeping single-location setups unaffected.

#### Related PR

- PR 15173 (BRCLogistics): #22558 — enhance the DeleteOldItemJournalLine procedure to include a Location Code parameter

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Item balance import deleted pending item journal lines belonging to other locations (#22558)
