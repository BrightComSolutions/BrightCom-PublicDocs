---
title: BRCCore 28.0.37747.0
categories: [BRCCore, ReleaseNotes]
description: Fixes two defects in the retention policy setup - locale-dependent date formulas and minimum retention periods given in the wrong unit.
date: 2026-10-28
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Retention policy setup fixes | Retention setup works in every language, and the mandatory minimum retention periods are now the intended number of days. | 32097 |

## Detailed Feature Information

---

### Retention policy setup fixes (#32097)

BRC Core sets up retention policies for its log and archive tables on install and upgrade. Two defects are fixed:

- **Install and upgrade could fail in some languages.** The retention period date formulas were parsed in the session language, so where the day letter is not "D" (for example German or French) setting up retention failed for that company. The formulas are now locale-independent.
- **Mandatory minimum retention was far too short.** The minimum periods were meant in months but were read as days, so the real floors were 1 to 12 days. They now match each table's default retention period (for example 365 days for the credential audit log).

The minimum only gets longer, so no data is lost. A shorter policy set by an administrator is raised to the minimum when retention runs. Existing tenants get the fix through the upgrade.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Retention setup date defects | Locale-dependent date formulas could fail install/upgrade, and minimum retention periods were given in months but read as days. | 32097 |
