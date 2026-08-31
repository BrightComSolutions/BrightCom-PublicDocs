---
title: BRCConnect 25.0.32986.0
categories: [BRCConnect, ReleaseNotes]
description: Parent BOM inventory recalculation, fewer false-positive errors, and purchase order dimension handling.
date: 2026-07-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Parent BOM inventory recalculation on component sales | When inventory calculation is set to Inventory-SalesorderInvoice, changes to a component sales line now recalculate the parent BOM item's availability immediately, reducing overselling. | 27585 |
| Reduced false-positive error messages | Documents retried during high-speed operation no longer leave stale "false positive" entries in the Errors list, making real issues easier to find. | 27566 |
| Purchase order dimension handling | Dimensions (cost center) can now be set on purchase orders in Business Central from inbound Connect messages, with added JSON content validation on the BRC Connect Content page. | 22125 |

## Detailed Feature Information

---

### Parent BOM inventory recalculation on component sales (#27585)

When the inventory calculation feature is set to **Inventory-SalesorderInvoice**, creating, modifying, or deleting a sales line for a **component** item now triggers an immediate recalculation of the **parent** (mother) BOM item. Previously recalculation only happened after a posted change (shipment or invoice), which could sync incorrect parent availability to connected e-commerce channels and lead to overselling of bundle/kit items.

#### Related PR

- PR 14933 (BRCConnect): Recalculate Mother Item when BOM item gets sold so the inventory is correct

---

### Reduced false-positive error messages (#27566)

During normal operations, a document may be retried multiple times when working at high speed. This update improves status validation so those retries no longer leave "false positive" entries in the Errors list, making it easier to locate the real issues that need attention.

#### Related PR

- PR 14928 (BRCConnect): Proper validation of Status to clear errors on Status changes

---

### Purchase order dimension handling (#22125)

BRC Connect can now read dimension information (such as cost center) from inbound purchase document messages and apply it to the resulting purchase orders in Business Central — previously there was no support for reading dimensions on the inbound purchase document. This release also adds JSON content validation on the BRC Connect Content page to catch malformed payloads earlier.

#### Related PR

- PR 14850 (BRCConnect): Enhance dimension handling in purchase line and header processing; add JSON content validation in BRC Connect Content page

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- None in this release.
