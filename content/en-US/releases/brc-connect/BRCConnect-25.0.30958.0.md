---
title: BRC Connect 25.0.30958.0
categories: [BRC Connect, ReleaseNotes]
description: BOM inventory calculation improvements and price date handling bugfix
date: 2026-04-22
---

## Release Summary

| Feature                                      | Description                                                                     |   ID |
| -------------------------------------------- | ------------------------------------------------------------------------------- | ---: |
| Send Calculated Inventory for BOM Items     | Extend inventory adjustment triggers for BOM products beyond sales transactions | 22825 |

## Detailed Feature Information

---

### Send Calculated Inventory for BOM Items (#22825)

Extended inventory adjustment triggers to support more transaction types beyond just sales, specifically for Bill of Materials (BOM) products. Currently only sales transactions trigger calculated inventory updates, but this enhancement enables adjustments for receipts and inventory differences as well.

**Business Value:** Provides more accurate inventory tracking for BOM items throughout their lifecycle, not just at the point of sale. Customers using BOM products can now maintain accurate calculated inventory across all transaction types including receipts and inventory adjustments.

**Technical Details:**
- Inventory adjustment triggers now support receipts
- Added support for inventory difference transactions
- Extends beyond sales-only calculated inventory updates
- Applies specifically to BOM product types

---

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Fixed start date and end date handling for price synchronization
