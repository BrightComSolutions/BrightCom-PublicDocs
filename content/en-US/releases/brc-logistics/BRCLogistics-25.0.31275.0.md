---
title: BRC Logistics 25.0.31275.0
categories: [BRCLogistics, ReleaseNotes]
description: Three new features for Ongoing WMS integration and Deposco, plus two bugfixes for InReturn and return order handling.
date: 2026-04-30
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Multiple Waybill Tracking Numbers from Ongoing | Import and store multiple tracking numbers from Ongoing shipments in Business Central for improved shipment visibility and return handling. | 24364 |
| Ignore Scrap Item Adjustments from Ongoing | Adds a configurable option on the Logistics Setup to ignore item adjustments flagged as scrapped returns when importing inventory changes from Ongoing, preventing unwanted stock movements in Business Central. | 26009 |
| Deposco WMS Integration Updates | Updates the Deposco WMS integration with improvements to order creation, shipment reading, and item data synchronization to support customer-specific warehouse configurations. | 18116 |

## Detailed Feature Information

---

### Multiple Waybill Tracking Numbers from Ongoing (#24364)

Import and store multiple tracking numbers from Ongoing shipments in Business Central for improved shipment visibility and return handling. When a shipment carries more than one waybill tracking number, all values are now fetched from Ongoing and stored as a comma-separated field in Business Central, ensuring complete tracking data is available for return handling and shipment lookup scenarios.

---

### Ignore Scrap Item Adjustments from Ongoing (#26009)

Adds a configurable option on the Logistics Setup to ignore item adjustments flagged as scrapped returns when importing inventory changes from Ongoing, preventing unwanted stock movements in Business Central. The Ongoing integration now supports the `IsScrapped` flag on inventory change records, and a new toggle on the Logistics Setup card allows this filter to be enabled or disabled per installation.

---

### Deposco WMS Integration Updates (#18116)

Updates the Deposco WMS integration with improvements to order creation, shipment reading, and item data synchronization to support customer-specific warehouse configurations. Changes span the order creation, shipment request reading, and item data codeunits to align with current Deposco API expectations.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- InReturn Shipment Count Fix for Partial Invoicing (#26519)
- Return Order Zero-Price Handling Fix (#26580)
