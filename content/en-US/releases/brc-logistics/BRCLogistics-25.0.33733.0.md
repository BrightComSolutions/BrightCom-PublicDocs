---
title: BRC Logistics 25.0.33733.0
categories: [BRCLogistics, ReleaseNotes]
description: Dock arrival date/time captured from Ongoing, plus a fix for transfer order lines in Ongoing shipment orders.
date: 2026-08-10
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Dock arrival date/time from Ongoing | The arrival date reported by Ongoing WMS when a delivery is received at the dock is now stored on the WMS transaction and shown on the transaction card. | 28202 |
| Transfer order lines in Ongoing shipment orders | Shipment orders sourced from a transfer order no longer attempt to read a sales line, correcting currency, VAT, and comment handling on those lines. | 29552 |

## Detailed Feature Information

---

### Dock arrival date/time from Ongoing (#28202)

Ongoing WMS reports when an inbound delivery was physically received at the warehouse dock, but that value was not retained in Business Central.

Inbound message processing now reads the arrival value from the Ongoing response and stores it in a new **Dock Arrival DateTime** field on the warehouse header. The field is shown on the **WMS Transaction Card**, making the actual receipt time available for reporting, KPI analysis, and traceability of inbound warehouse operations.

Behavior is unchanged when Ongoing does not supply the value. Implausible dates are ignored rather than stored, and an arrival time already recorded on a transaction is not overwritten by a later message.

#### Related PR

- PR 15067 (BRCLogistics): Store the arrival information from Ongoing for when a delivery was received

---

### Transfer order lines in Ongoing shipment orders (#29552)

When building an Ongoing shipment order, the connector read the originating sales line for every warehouse shipment line. For lines sourced from a **transfer order** there is no sales line to read, so the values taken from it were not meaningful.

The connector now checks the source document type first and only reads the sales line when the source is genuinely a sales order. For transfer order lines it skips the sales-line-derived content instead:

- **Order line comments** are omitted rather than read from a non-existent line.
- **Currency code** falls back to the LCY code from General Ledger Setup.
- **VAT percent** is sent as zero.
- **Assemble-to-order sub-lines** are not evaluated.

#### Related PR

- PR 15012 (BRCLogistics): Ongoing — skip sales lines for transfer orders

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Ongoing shipment orders read a sales line for transfer order lines, producing incorrect currency, VAT, and comment values (#29552)
