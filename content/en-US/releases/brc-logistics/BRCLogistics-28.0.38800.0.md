---
title: BRCLogistics 28.0.38800.0
categories: [BRCLogistics, ReleaseNotes]
description: Improved receipt matching with variants, support for multiple unit-of-measure message values and corrected return-shipment handling.
date: 2026-11-12
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Receipt matching with variants | Receival Notices are matched correctly to Receival Orders when variants are involved. | 32365 |
| Multiple unit-of-measure message values | Logistics messages support several unit-of-measure values for the same integration scenario. | 33578 |
| Correct return-shipment handling | Returned service items are marked as return shipments. | 33566 |

## Detailed Feature Information

---

### Receipt matching with variants (#32365)

Matching between Receival Notices and Receival Orders now handles item variants correctly.

### Multiple unit-of-measure message values (#33578)

Logistics messages can support several unit-of-measure values, improving integration scenarios where a single item uses more than one unit representation.

### Correct return-shipment handling (#33566)

When a service item is returned, BRC Logistics now marks it as a return shipment.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Receival matching with variants | Corrected matching of Receival Notices to Receival Orders. | 32365 |
| Returned service item classification | Returned service items are classified as return shipments. | 33566 |