---
title: BRCLogistics 25.0.32697.0
categories: [BRCLogistics, ReleaseNotes]
description: Expiration date fix and WMS Transaction Card layout updates.
date: 2026-06-18
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Warehouse reference field length fix | Increased the field length used for storing source warehouse document numbers to prevent overflow/runtime issues. | 27772 (via 27669) |
| Expiration date handling fix | Corrected expiration date handling in the related logistics flow. | 27828 |
| WMS Transaction Card line layout update | Reworked the WMS Transaction Card so line content is moved out of its previous group for clearer structure and better maintainability. | 18315 |

## Detailed Feature Information

---

### Warehouse reference field length fix (#27772 via #27669)

This change increases the Sales Header field length for the warehouse reference (BRC Logi Created From Wh. No.) to align with source warehouse document number length and avoid runtime failures when longer values are received.

#### Related PR

- PR 14711 (BRCLogistics): Increase length of "BRC Logi Created From Wh. No." to 30

---

### Expiration date handling fix (#27828)

This update resolves expiration date behavior in the affected logistics process to ensure the expected values are handled correctly.

#### Related PR

- PR 14829 (BRCLogistics): ExpirationDateOnPurchase

---

### WMS Transaction Card line layout update (#18315)

Line content on the WMS Transaction Card was moved outside its previous group. The previous placement is marked toward deprecation and line update propagation was aligned for consistent updates.

#### Related PR

- PR 14777 (BRCLogistics): WMS Trans Card: moving Lines out of the Group

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- None in this release.
