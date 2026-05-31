---
title: BRC Logistics 25.0.32298.0
categories: [BRCLogistics, ReleaseNotes]
description: New Ongoing shipment mapping for Department/Store IDs plus two Ongoing integration bugfixes.
date: 2026-05-31
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Sync Department and Store IDs to Ongoing via Shipment Order | Adds new Store ID (Customer Card) and Department ID (Sales Order Header) fields and maps them into the Ongoing Shipment Order document via BRC extra fields, supporting EDI flows for key accounts. | 27002 |

## Detailed Feature Information

---

### Sync Department and Store IDs to Ongoing via Shipment Order (#27002)

Two new free-text fields (20 characters) have been added to support EDI flows where the receiving party expects a department and store identifier on the outbound shipment:

- **Store ID** on the Customer Card, under the Shipping menu group.
- **Department ID** on the Sales Order Header, placed alongside the External Document No. field.

Both values flow through to the Ongoing Shipment Order document using BRC's extra-fields mapping mechanism, so no integration configuration changes are required.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Ongoing Correction for Inventory Picks when using Transfer Orders — restored the previous design that relies on the `SalesLine.Get` return value, fixing a regression in the sales line lookup during Ongoing pick processing. (#27675)
- Check Receival Status now works for Purchase Orders — the action previously appeared to do nothing on Purchase Orders; the Receival Notice was being created in Ongoing but was not correctly linked back to the PO (missing `Applies-to Document Type` and `Applies-to Doc. No.`). Linking has been corrected. (#27415)
