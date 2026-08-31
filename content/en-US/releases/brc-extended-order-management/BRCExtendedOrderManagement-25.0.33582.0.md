---
title: BRC Extended Order Management 25.0.33582.0
categories: [BRCExtendedOrderManagement, ReleaseNotes]
description: The Excel price matrix for sales price lists is now available for purchase price lists.
date: 2026-08-03
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Price matrix for purchase price lists | Export, add/update, and import actions on Purchase Price Lists, matching the spreadsheet-based price matrix already available for sales price lists. | 27545 |

## Detailed Feature Information

---

### Price matrix for purchase price lists (#27545)

The spreadsheet-driven price matrix that already existed for sales price lists is now available for **purchase** price lists as well, so buying prices can be maintained in the same way as selling prices.

Three actions have been added to the **Purchase Price Lists** page:

- **Export Prices** — writes the current purchase price list to a spreadsheet, one row per item and variant, with item number, variant code, unit of measure, and description columns, and the price list currency applied.
- **Add / Update Prices** — opens the item list so a selection of items can be added to the price list, producing a matrix pre-filled with each item's existing purchase price where one is defined.
- **Import Prices** — reads an edited spreadsheet back in and updates the purchase price list lines accordingly.

Variants are handled alongside their parent item, and the unit of measure is resolved from the existing purchase price list lines, falling back to the item's base unit of measure.

This mirrors the sales-side behavior, so the same working method applies to both directions.

#### Related PR

- PR 15029 (BRCExtendedOrderManagement): Added the same functionality for purchase price lists as for sales price lists (price matrix)

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- None in this release.
