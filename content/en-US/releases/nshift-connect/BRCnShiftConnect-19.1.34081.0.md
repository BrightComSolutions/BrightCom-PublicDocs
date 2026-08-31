---
title: nShift Connect 19.1.34081.0
categories: [nShift Connect, ReleaseNotes]
description: The VAT-exclusive customs setting now also applies to the line value field.
date: 2026-08-27
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| VAT-exclusive setting extended to the line value field | The Send Customs Value Excl. VAT setting now governs the `value` field as well as `linecustomsValue`, so both are consistent. | 29460 |

## Detailed Feature Information

---

### VAT-exclusive setting extended to the line value field (#29460)

The **Send Customs Value Excl. VAT** setting introduced in the previous release applied only to the `linecustomsValue` JSON field. The `value` field continued to be sent from the VAT-inclusive line amount, so a shipment could carry two different values for what is effectively the same figure.

With this release the setting governs both fields. When **Send Customs Value Excl. VAT** is enabled, `value` is calculated from the sales line **Amount** divided by quantity — the same VAT-exclusive basis as `linecustomsValue`. When the setting is disabled, both fields continue to use the previous VAT-inclusive calculation.

This completes the work started in 19.1.33771.0 and makes the customs figures sent to nShift internally consistent.

#### Related PR

- PR 15171 (BRCnShiftConnect): #29460 — update line amount calculation to conditionally include or exclude VAT based on setup

## Breaking Changes

No breaking changes in this release.

**Note:** on tenants that already enabled **Send Customs Value Excl. VAT**, the `value` field will change from a VAT-inclusive to a VAT-exclusive figure with this upgrade. This is the intended correction, but it is a change in transmitted data for those tenants.

## Bugfixes

- The `value` field ignored the VAT-exclusive customs setting, leaving it inconsistent with `linecustomsValue` (#29460)
