---
title: BRC Logistics 25.0.34050.0
categories: [BRCLogistics, ReleaseNotes]
description: Extra field mappings now support DateTime target fields.
date: 2026-08-25
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| DateTime support in extra field mappings | The generic extra fields mapping now handles DateTime target fields, so values such as the Ongoing dock arrival time can be mapped through the standard mechanism. | 28202 |

## Detailed Feature Information

---

### DateTime support in extra field mappings (#28202)

The dock arrival date/time delivered in an earlier release was specific to the Ongoing connector. To make the same kind of value usable generally, the main app's **extra fields** mapping mechanism now understands **DateTime** destination fields.

When a mapping targets a DateTime field, the value is transferred as a DateTime rather than being pushed through text validation:

- If the source field is itself a DateTime, its value is assigned directly.
- Otherwise the incoming text is evaluated into a DateTime before being validated onto the target.

Mappings targeting any other field type are unaffected and continue to validate as before.

This means arrival timestamps and similar values from a WMS can be mapped into Business Central fields through the standard extra field configuration, without connector-specific handling.

#### Related PR

- PR 15107 (BRCLogistics): #28202 — addition to the previous Ongoing-specific change; the main app must be able to handle DateTime as extra fields

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- None in this release.
