---
title: BRC Extended IC 23.0.31823.0
categories: [BRCExtendedIC, ReleaseNotes]
description: New unit conversion support in IC master data synchronization, plus a bugfix for IC transaction number sequencing.
date: 2026-05-17
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Unit Conversion in IC Master Data Synchronization | Introduces a Conversion Factor field for intercompany master data imports to handle unit and currency conversions across different company localizations. | 25108 |

## Detailed Feature Information

---

### Unit Conversion in IC Master Data Synchronization (#25108)

Introduces a Conversion Factor field for intercompany master data imports to handle unit and currency conversions across different company localizations. When companies in an IC setup use different units of measure or currencies, the incoming decimal values (such as prices or quantities) can now be multiplied by a configured conversion factor before being stored in Business Central. A factor of 1 means no conversion is applied. The factor is validated on setup (must be greater than 0, defaulting to 1), and rounding is applied per field precision. Import failures due to constraint violations are logged as errors.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- IC Transaction Number Sequencing (#20447) — Implemented a centralized `GetNextICTransactionNo` procedure and refactored transaction number retrieval across multiple codeunits. This ensures consistent and correct IC transaction number assignment throughout the intercompany flow, addressing scenarios where numbers could be retrieved inconsistently.
