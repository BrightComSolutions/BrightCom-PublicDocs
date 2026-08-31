---
title: nShift Connect 19.1.33771.0
categories: [nShift Connect, ReleaseNotes]
description: New setup options to send the line customs value excluding VAT and to send quantity as copies.
date: 2026-08-12
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Send customs value excluding VAT | A new setup option sends the line customs value based on the VAT-exclusive amount, so customs declarations are no longer inflated by VAT. | 29460 |
| Send quantity as copies | A new setup option sends the sales line quantity in the nShift `copies` field. | 29460 |

## Detailed Feature Information

---

### Send customs value excluding VAT (#29460)

The JSON fields `value` and `linecustomsValue` were both derived from the sales line **Line Amount** divided by quantity. Because Line Amount includes VAT in the relevant scenarios, the customs value sent to nShift was overstated — creating a risk of incorrect customs reporting, extra handling costs, and delayed shipments.

A new Boolean field, **Send Customs Value Excl. VAT**, has been added to the nShift Setup card. When enabled, `linecustomsValue` is calculated from the sales line **Amount** (excluding VAT) divided by quantity instead.

In this release the `value` field is unchanged and continues to use the previous calculation. The setting is off by default, so existing behavior is preserved unless enabled.

---

### Send quantity as copies (#29460)

A second setup option, **Send Quantity as copies**, has been added. When enabled, the sales line **Quantity** is sent as an integer in the nShift `copies` field. The option is off by default.

#### Related PR

- PR 15082 (BRCnShiftConnect): Send Customs Value Incl. VAT (setting)

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Customs value was sent including VAT, overstating the declared value (#29460)
