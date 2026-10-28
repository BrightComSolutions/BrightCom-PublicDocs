---
title: BRCLogistics 28.0.37758.0
categories: [BRCLogistics, ReleaseNotes]
description: Lot numbers and expiration dates from Ongoing on production picks and put-aways, auto-send for production warehouse documents, separate invoice and delivery addresses for warehouse shipments, and a configurable order attribute for EasyCom/Inretrn.
date: 2026-10-28
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Lot No. and Expiration Date on production picks and put-aways (Ongoing) | Lot numbers and expiration dates reported by Ongoing are applied to inventory picks and put-aways created from production orders. | 31497 |
| Separate invoice and delivery address for warehouse shipments (Ongoing) | Warehouse shipments sent to Ongoing carry the sales order's invoice and delivery addresses separately. | 30072 |
| Order attribute for EasyCom/Inretrn | A new setting sends Extra Field 7 to Inretrn as an order attribute under a key you choose. | 31499 |

## Detailed Feature Information

---

### Lot No. and Expiration Date on production picks and put-aways (#31497)

When Ongoing reports a lot (batch) number or an expiration date on an item movement, BRC Logistics now stores it and applies it to the inventory pick or put-away in Business Central. This closes a gap in lot traceability for material consumed and output in production.

- It applies when **Batch No. - Receival** is on in BRC Logistics Setup and the item is lot tracked (Lot Specific Tracking or Lot Warehouse Tracking on its Item Tracking Code).
- The Lot No. and Expiration Date are set on the warehouse activity line using standard Business Central item tracking. No custom expiration logic is involved.
- If Ongoing reports several lots for one line, the line is split into one warehouse activity line per lot, each with its own quantity, so every lot posts correctly. Partial receivals of the same line are handled.

No setup changes are needed beyond the existing **Batch No. - Receival** setting.

### Separate invoice and delivery address for warehouse shipments (#30072)

For customers who release outbound deliveries to Ongoing as **Warehouse Shipments** rather than sales orders, BRC Logistics now looks up the sales order behind the shipment. The order's invoice (bill-to) and delivery (ship-to) information is then sent to Ongoing separately, the same way it is for sales orders, so Ongoing can tell which address to invoice and which to deliver to.

Shipments with the same bill-to and ship-to address are sent as before.

### Order attribute for EasyCom/Inretrn (#31499)

A new field, **EasyCom Extra Field 7 Attr Key**, in the EasyCom/Inretrn group on BRC Logistics Setup lets an EasyCom/Inretrn connection send one extra value at order level to Inretrn.

- When the key is set and **Extra Field 7** on the posted sales warehouse header has a value, it is sent as an order attribute (`IdentifierKey: "SalesOrder"`, `AttributeKey: <your key>`, `AttributeValue: <Extra Field 7>`). Inretrn picks up order attributes by key in its own rules.
- Extra Field 7 is filled through the existing Extra Fields mapping, so the value can be anything you map. For example, a Map Value Code can turn a posting group into true/false for a B2B flag.
- With the key blank, nothing changes: existing connections send exactly the same payload as before.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Production picks and put-aways not auto-sent | Inventory picks and put-aways created from production orders are now sent to the WMS automatically when **Auto-Send Non-Sent Inv. Pick** / **Auto-Send Non-Sent Inv. Put Away** is on, the same as manually created ones. | 32059 |
