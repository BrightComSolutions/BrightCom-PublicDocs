---
title: BRC Logistics 25.0.34865.0
categories: [BRCLogistics, ReleaseNotes]
description: Inventory count lines always carry a description, plus fixes to the error history and the insufficient-stock recovery introduced in 25.0.34805.0.
date: 2026-09-23
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Description always filled on inventory count lines | Item journal lines created from an inbound inventory count fall back to the item's own description when nothing else supplies one. | 30064 |

## Detailed Feature Information

---

### Description always filled on inventory count lines (#30064)

Some customers feed inventory counts into Business Central from an external counting app. When the incoming data carried no description of its own, and no Extra Field mapping supplied one, the resulting item journal line was left with a **blank Description**.

Both the item balance and the item balance line routines now fall back to the **item's own Description** when the journal line would otherwise be left empty. Lines that already receive a description — from the source data or from an Extra Field mapping — are unaffected, so this only fills in what was previously blank.

#### Related PRs

- PR 15449 (BRCLogistics): Requirement/30064 Item Descr for Item Balance

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- **Only one error entry was kept per document line.** The BRC Logistics Error Entry table introduced in 25.0.34805.0 computed the next entry number but never wrote it to the record, so every entry was stored with an Entry No. of 0. Because Entry No. forms part of the table's primary key, a second failure on the same document line collided with the first instead of being recorded next to it — which is precisely the repeated-failure case the error history exists to capture. Entries are now numbered correctly and the full history per document line is kept.

- **Insufficient-stock recovery could stop early when the shortage had already resolved.** In the opt-in item movement recovery shipped in 25.0.34805.0, a group whose inventory had become sufficient by the time recovery ran — for example because another message posted a receipt in the meantime — was counted as "not recovered". Where that was the only group in the run, the run exited early and the affected lines were annotated as skipped instead of being re-opened for the next run. Such groups are now treated as ready to retry, and the adjustment journal is only posted when there is genuinely something to adjust.
