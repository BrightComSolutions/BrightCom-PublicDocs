---
title: BRCExtendedIC 27.0.34466.0
categories: [BRCExtendedIC, ReleaseNotes]
description: Unit conversion for intercompany master data synchronization, plus Business Central 29 compatibility and a raised minimum version.
date: 2026-09-11
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Unit Conversion in IC Master Data Sync | Automatically convert weight, dimensions, volume and costs during intercompany master data import using configurable conversion factors. | 25108 |
| Business Central 29 compatibility | Intercompany outbox writes now use the enum-typed IC Source Type field that replaces the retired Source Type field. | 18310 |

## Detailed Feature Information

---

### Unit Conversion in IC Master Data Sync (#25108)

Intercompany partners operating in different localizations may record weight, length, width, depth and volume in different units of measure, and hold costs in different local currencies. Importing master data from a partner company therefore risked carrying values across unchanged, leaving them wrong for the receiving company.

The Extended IC Data Import Field table now carries a **Conversion Factor** decimal field. When master data is imported from another company, the configured factor is applied so weights, dimensions, volumes and costs arrive already expressed in the receiving company's units and currency.

Conversion is configured per field, so companies that share units for some values and not others only convert what actually differs.

#### Related PR

- PR 14958 (BRCExtendedIC): Unit conversion in IC master data synchronization

---

### Business Central 29 compatibility (#18310)

Microsoft has retired the `Source Type` field on the IC Outbox Transaction and IC Inbox Transaction tables, replacing it with the enum-typed `IC Source Type`. Extended IC previously wrote to both fields while the old one was still available.

All intercompany outbox writers now set only `IC Source Type`, and the record-reference workarounds that existed purely to tolerate the old field have been retired in favour of direct field access.

This is what raises the app's minimum supported platform — see Breaking Changes below.

#### Related PR

- PR 15313 (BRCExtendedIC): BC 29 compatibility — migrate to "IC Source Type", raise minimum to BC 27

## Breaking Changes

**Minimum Business Central version raised to 27.0.**

The app's required application and platform versions move from `26.0.0.0` to `27.0.0.0`, and the runtime moves from `12.0` to `16.0`. Environments still on Business Central 26 or earlier cannot install this version and must upgrade first.

Customers who do not yet need the unit conversion feature can remain on 26.0.23827.9 until their environment is upgraded.

## Bugfixes

- None in this release.
