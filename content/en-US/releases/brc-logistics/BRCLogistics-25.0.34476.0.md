---
title: BRC Logistics 25.0.34476.0
categories: [BRCLogistics, ReleaseNotes]
description: DSV CargoWrite warehouse integration for the EU region, plus additional integration events for partner extensions.
date: 2026-09-11
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| DSV CargoWrite warehouse integration (EU) | New connector for the DSV CargoWrite public API covering product data, purchase and sales orders, inbound deliveries and order status retrieval. | 14983 |
| Additional integration events for partner extensions | New integration events across the Connect readers, EasyCom posted sales requests and warehouse order routines, giving partner extensions supported hook points. | 29986 |

## Detailed Feature Information

---

### DSV CargoWrite warehouse integration (EU) (#14983)

Customer-driven development adds support for the **DSV CargoWrite** warehouse platform in the EU region, built against DSV's public Solutions Warehouse API.

The connector covers the full exchange in both directions:

- **Outbound** — creates product data, purchase orders and sales orders in CargoWrite, and sends shipment and receival requests
- **Inbound** — reads inbound delivery confirmations, incoming messages and sales order status back into Business Central

Configuration is surfaced on the BRC Logistics Setup card, and the Warehouse Shipment card and warehouse shipment header are extended with the fields the integration needs.

#### Related PR

- PR 14949 (BRCLogistics): DSV Cargowrite

---

### Additional integration events for partner extensions (#29986)

Several logistics routines previously offered no supported extension point, which left per-tenant extensions with no clean way to participate in those flows.

Integration events have been added to:

- Connect item balance, receival request and return request readers
- EasyCom posted sales requests
- Exchange order and return order creation
- The warehouse line table

Partner extensions can now subscribe to these events rather than relying on unsupported workarounds.

#### Related PR

- PR 15274 (BRCLogistics): Added events for per-tenant extension use

## Breaking Changes

No breaking changes in this release.

**Deprecation notice for extension developers.** Four integration events in the DSV area are published under names that predate the DSV rename and are now marked obsolete:

- `OnBeforeCallMintsoftAndGetResponse` / `OnAfterCallMintsoftAndGetResponse` (codeunit BRC DSV Send Request)
- `OnBeforeReadSalesOrderDsvStatus` / `OnAfterReadSalesOrderDsvStatus` (codeunit BRC DSV Read SalesOrder Mth)

They continue to fire in this release, so existing subscribers keep working. They will be removed in a future version — extensions subscribing to them should plan to move to the current event names.

## Bugfixes

- None in this release.
