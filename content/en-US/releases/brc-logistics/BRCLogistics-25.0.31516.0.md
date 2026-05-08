---
title: BRC Logistics 25.0.31516.0
categories: [BRCLogistics, ReleaseNotes]
description: Four new features including improved return handling, multi-currency support, and NoWaste batch tracking, plus three bugfixes.
date: 2026-05-08
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Partial Returns from Sello | Ensures partial returns from Sello are processed correctly across multiple return messages without duplicate prevention blocking the flow. | 24125 |
| Multiple Tracking Numbers from Ongoing | Import and store multiple tracking numbers from Ongoing shipments in Business Central for improved shipment visibility and return handling. | 24364 |
| Currency Fix for Warehouse Shipments | Warehouse shipments now send the Sales Order currency and amounts to WMS, ensuring accurate pricing in multi-currency scenarios. | 25549 |
| NoWaste Batch Indicator | Item synchronization to NoWaste now includes batch tracking status, enabling proper handling of returns for batch-tracked items. | 25980 |

## Detailed Feature Information

---

### Partial Returns from Sello (#24125)

Ensures partial returns from Sello are processed correctly across multiple return messages without duplicate prevention blocking the flow. The system now increases the buffer time for record polling to 100 minutes to accommodate Sello's update delays, allowing partial return documents to be created without triggering duplicate detection when subsequent return messages arrive for the same order.

---

### Multiple Tracking Numbers from Ongoing (#24364)

Import and store multiple tracking numbers from Ongoing shipments in Business Central for improved shipment visibility and return handling. When a shipment carries more than one waybill tracking number, all values are now fetched from Ongoing and stored as a comma-separated field in Business Central, ensuring complete tracking data is available for return handling and shipment lookup scenarios.

---

### Currency Fix for Warehouse Shipments (#25549)

Warehouse shipments now send the Sales Order currency and amounts to WMS, ensuring accurate pricing in multi-currency scenarios. Previously, when using warehouse shipments, the currency information was not properly transferred to the WMS system, causing potential pricing and reporting issues for orders in foreign currencies.

---

### NoWaste Batch Indicator (#25980)

Item synchronization to NoWaste now includes batch tracking status, enabling proper handling of returns for batch-tracked items. A new BatchIndicator field is now populated during item synchronization to NoWaste, ensuring the return system can properly handle items that require batch/lot tracking.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Assembly Order Integration (#24376) — Integration support for assembly orders to Nyce/Bonver for NoWaste workflows.
- Return Order Zero-Price Handling (#26580) — Fixed an issue in the Create Return Order codeunit where items with zero prices were incorrectly ignored even when the return system should set the price.
- Sales Return Order Invoice Numbers (#27099) — Fixed incorrect invoice number assignment on copied partial invoices for sales return orders.
