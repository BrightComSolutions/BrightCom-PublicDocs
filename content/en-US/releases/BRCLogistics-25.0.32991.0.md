---
title: BRCLogistics 25.0.32991.0
categories: [BRCLogistics, ReleaseNotes]
description: QSSI carton quantity fix, Ongoing free-text mapping, Bitlog picking-started status, Assembly resource lines, and InReturn invoice totals fix.
date: 2026-07-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| QSSI per-carton quantity fix | The QSSI Shipment Notice import now uses PIECES_TO_MOVE (per-carton quantity) instead of PIECES_SHIPPED (line total) when creating carton/package records. | 29062 |
| Ongoing receival line free-text mapping | Receival Order Line Field 1003 can now be mapped to InOrderLineFreeText2 in the Ongoing WMS connector. | 29178 |
| Bitlog "Picking Started" status | The Bitlog connector can now detect when picking has started and reflect that status in Business Central. | 28178 |
| Assembly BOM resource line support | Assembly BOMs containing Resource lines can now be sent to external WMS by ignoring resources in WMS payloads while keeping correct costing in BC. | 24289 |
| InReturn invoice quantity/amount fix | Corrected quantity and amount totals sent to InReturn for Posted Sales Invoices that have no originating order reference. | 28602 |

## Detailed Feature Information

---

### QSSI per-carton quantity fix (#29062)

The QSSI connector previously used **PIECES_SHIPPED** from the Shipment Notice message to determine carton/package quantities. That field represents the total quantity shipped for a line, not the quantity per individual carton, which could produce incorrect carton quantities in Business Central. The logic now uses **PIECES_TO_MOVE** so each carton/package record reflects its own per-line value.

#### Related PR

- PR 14946 (BRCLogistics): Fetch and store PIECES_TO_MOVE instead of PIECES_SHIPPED

---

### Ongoing receival line free-text mapping (#29178)

**Receival Order – Line – Field 1003** is now exposed in the BRC Logistics mapping setup so it can be mapped to **InOrderLineFreeText2** in the Ongoing WMS connector. When receival orders are exported to Ongoing, the value from Field 1003 on each line is transferred to the corresponding InOrderLineFreeText2 field in the outbound message.

#### Related PR

- PR 14932 (BRCLogistics): Ongoing InOrderLine FreeText2

---

### Bitlog "Picking Started" status (#28178)

The Bitlog connector now supports a new intermediate lifecycle status: **Picking Started**. A recurring Job Queue entry calls the Bitlog endpoint `api/order/feed/{orderNo}` for outbound sales orders that have been sent to Bitlog and are not yet shipped, giving near real-time visibility into when warehouse work begins for improved planning and customer communication.

#### Related PR

- PR 14910 (BRCLogistics): Picking Started

---

### Assembly BOM resource line support (#24289)

BRC Logistics now aligns with standard Business Central behavior by allowing Assembly BOMs that include lines of type **Resource**. Resources — which exist for correct costing and posting rather than physical picking — are ignored in the WMS payload instead of being validated as SKUs, so assemblies containing resource lines no longer error when sent to an external WMS such as Bitlog.

#### Related PR

- PR 14900 (BRCLogistics): Filter assembly lines by item type in CreateBRCLogiWarehouseLineFromAssemblyLine

---

### InReturn invoice quantity/amount fix (#28602)

When sending a Posted Sales Invoice to InReturn (EasyCom), the connector accumulates quantities and amounts across related invoice lines to support partial invoices. When an invoice line had no originating **Order No.** / **Order Line No.**, this summation incorrectly aggregated all invoice lines sharing the same item and variant. A safeguard now excludes lines without a valid order reference, producing correct quantities and amounts.

#### Related PR

- PR 14864 (BRCLogistics): Inreturn Sales Invoices Qty and Amounts not calculated correctly

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- InReturn invoice quantity/amount summation fix (#28602)
