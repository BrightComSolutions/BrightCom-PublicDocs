---
title: BRC Logistics 25.0.30970.0
categories: [BRC Logistics, ReleaseNotes]
description: Partial return handling, dangerous goods compliance, BOM quantity improvements, and warehouse integration enhancements
date: 2026-04-22
---

## Release Summary

| Feature                                              | Description                                                                                                      |   ID |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---: |
| Correct Handling of Partial Sello Returns           | Process partial returns from Sello without duplicate prevention blocking incrementally increasing quantities    | 24125 |
| Update Quantity Sent to WMS for Assembly BOM Items   | Send correct quantity to consume for assembly orders in WMS integration                                          | 23423 |
| Flash Point Export to Ongoing Integration            | Send item Flash Point values to Ongoing for improved dangerous goods classification and compliance               | 25616 |
| Compensation Linked to Sales Line Margin             | Link InReturn compensations to original sales lines and adjust item margin without affecting inventory           | 25848 |
| Ignore Scrapped Items from Ongoing Returns           | Add configuration to ignore scrapped item adjustments when handled in Ongoing                                    | 26471 |

## Detailed Feature Information

---

### Correct Handling of Partial Sello Returns (#24125)

Handle partial returns from Sello where multiple return messages arrive for the same sales order with incrementally increasing quantities. Similar to Ongoing shipment handling, each return message now creates a separate return document without being blocked by duplicate prevention logic.

**Business Value:** Critical for customers using monthly invoicing where copy document cannot be used. Ensures all partial returns from marketplace platforms are processed correctly across multiple return messages.

**Technical Details:**
- Ensures partial returns are processed sequentially without duplicate blocking
- Supports incremental quantity increases across multiple return messages
- Enables proper handling for monthly invoicing scenarios

Additionally, this release includes improvements to UTC time conversion handling throughout the logistics integrations to ensure consistent timestamp processing across time zones.

---

### Update Quantity Sent to WMS for Assembly BOM Items (#23423)

Fixed quantity handling for assembly orders sent to WMS. The system now sends "Quantity to Consume" instead of Quantity or Remaining Quantity to reflect the actual quantity to ship from the sales order line.

**Business Value:** Ensures partial shipments of assembly BOM items are correctly reflected in the WMS, improving inventory accuracy for customers selling assembly items using Assemble-to-Order.

**Technical Details:**
- Updated WMS integration to support sending qty. to consume for assembly orders (#20794)
- Applies to customers selling assembly BOM items using ATO
- Ensures correct quantity synchronization for partial shipments

---

### Flash Point Export to Ongoing Integration (#25616)

Extended Ongoing integration to send Flash Point (flammepunkt) values for dangerous goods items. The system already sends UNIsDangerousGoods boolean, but now includes Flash Point as a decimal value for improved dangerous goods classification.

**Business Value:** Required for proper dangerous goods classification and handling compliance. Provides Ongoing with complete dangerous goods information for regulatory and safety requirements.

**Technical Details:**
- Flash Point values sent in InventoryByQuery payload
- Ongoing supports additional dangerous goods fields including FlashPoint
- Complements existing UNIsDangerousGoods boolean field

---

### Compensation Linked to Sales Line Margin (#25848)

Changed InReturn compensation handling to link compensations to specific sales lines rather than standalone item charge lines. Uses salesOrderLineNumber from InReturn to match compensation to the original sales line.

**Business Value:** Critical for accurate product-level margin reporting. Creates financial-only Value Entry that affects margin calculations without impacting inventory levels.

**Technical Details:**
- Links compensations to original sales lines using salesOrderLineNumber
- Creates financial-only Value Entry affecting margin but not inventory
- InReturn replacement orders now create both return order and sales order with matching amounts (#25238)

---

### Ignore Scrapped Items from Ongoing Returns (#26471)

Added configuration option to Ongoing Logistics Card to ignore scrapped items from returns. When enabled, inventory changes where IsScrapped = true will not create item adjustments in Business Central.

**Business Value:** Prevents misleading double inventory adjustments when scrapping is already handled in Ongoing. Improves inventory accuracy by avoiding duplicate adjustments for the same scrapped items.

**Technical Details:**
- New option on Ongoing Logistics Card: "Ignore Scrapped Items from Returns" (#26009)
- Ongoing's GetInventoryChanges includes IsScrapped boolean
- When enabled, adjustments with IsScrapped = true are skipped
- Prevents duplicate adjustments when scrapping handled in Ongoing

---

## Additional Improvements

### Partial Shipment with Inventory Picks (#25902)

Added functionality to calculate line amounts based on quantity to ship for inventory picks, supporting partial shipment scenarios with improved accuracy.

### Sello Return Pagination (#26425)

Fixed pagination issue in Sello Return Fetching to ensure all return orders are retrieved when processing large volumes of marketplace returns.

### Ongoing Item Class Handling (#26636)

Fixed issue in Ongoing item integration where Extra Field 19 (mapped to enum) with space as first value caused problems. The system now sends blank instead of space when Extra Field 19 contains spaces, allowing Ongoing to interpret values correctly.

### InReturn Integration Improvements

- **Invoice Shipment Count** (#26519): Fixed issue where invoices sent to InReturn had incorrect number of shipments with partial invoicing
- **Zero Price Returns** (#26580): Fixed logic to accept returns with price 0 when InReturn explicitly sends zero (compensation already given)
- **Warehouse Receipt Bugfix** (#26377): Resolved issue in Warehouse Receipt Card functionality

---

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Fixed handling of Extra Field 19 in XML output to clear spaces properly (#26636)
- Fixed Sello pagination issue preventing retrieval of all return orders (#26425)
- Fixed InReturn invoice integration showing incorrect number of shipments (#26519)
- Fixed warehouse receipt card functionality issue (#26377)
- Fixed zero-price return handling from InReturn (#26580)
