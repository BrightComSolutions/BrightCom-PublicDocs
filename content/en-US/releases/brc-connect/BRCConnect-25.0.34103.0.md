---
title: BRC Connect 25.0.34103.0
categories: [BRCConnect, ReleaseNotes]
description: New extension points allowing a PTE to substitute an alternate item identifier for partNo across all inbound and outbound integration flows.
date: 2026-08-28
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Item number resolution events for PTE extensibility | New events let a customer extension resolve `partNo` against an alternate item identifier (for example Item "No. 2") on every inbound lookup and outbound line, without modifying BRC Connect. | 30003 |

## Detailed Feature Information

---

### Item number resolution events for PTE extensibility (#30003)

Some customers identify items to their web platform by something other than the Business Central Item **No.** — typically **No. 2** or another alternate identifier. Previously this required either aligning the item numbering with the platform or maintaining a customization inside BRC Connect itself.

This release adds a set of subscriber-inert extension points so a per-tenant extension (PTE) can own that translation:

**Inbound resolution.** A new codeunit **12073586 "BRC Item No. Resolution"** publishes `OnResolveItemNo`, raised before every `partNo` to Item resolution in the app — the sales line ladder, the purchase line ladder and its existing-line match, line validation, both price models, the warehouse journal, and all four 3PL shipment-line procedures.

**Item creation.** `OnBeforeInsertNewItem` and `OnAfterInsertNewItem` in **BRC Create/Update Item Mth** allow a subscriber to assign the Item **No.** from a number series while keeping the incoming `partNo` in a different field.

**Outbound serialization.** `OnAfterCreateJsonLine` has been added to all ten document line serializers, so `partNo` can be rewritten per line on the way out. Item, inventory, and price master data already exposed usable `OnAfterSet*Json` events.

Both permission sets have been updated to include the new codeunit. A PTE author guide is included in the repository at `.aidocs/itemno-resolution-pte-guide.md`.

**There is no behavior change without subscribers** — with no PTE attached, resolution works exactly as it did before.

**Known gap:** the legacy "BRC Sales Price to Web Mth" codeunit exposes only entry-level events and is not covered by the new resolution hook. This is not relevant on the current price model.

#### Related PR

- PR 15185 (BRCConnect): #30003 Add item-no resolution and line-JSON events for PTE extensibility

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- None in this release.
