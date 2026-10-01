---
title: BRCRisk 28.0.35617.0
categories: [BRCRisk, ReleaseNotes]
description: Objects moved into the AppSource ID range with BRC-prefixed Customer and Vendor card actions, plus Business Central 2026 release wave 1 (BC28) and a raised minimum version.
date: 2026-10-01
---

## About this release

This is the first published release note for BRC Risk Management. The app brings credit scores, risk ratings and criteria-based watchlists from third-party risk data providers (TIC or compatible) into Business Central, linked directly from Customer and Vendor cards. It also covers scheduled updates through the Job Queue, webhook updates from the provider, a Risk Manager role center, and API call logging. This release follows 1.0.27121.0. It moves the app into BrightCom's AppSource object range and onto Business Central 2026 release wave 1.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| AppSource object range and BRC prefixes | All objects and table-extension fields renumbered into BrightCom's AppSource ID range, and the actions and FactBoxes added to the Customer and Vendor cards now carry the BRC prefix. | 18454 |
| Business Central 2026 release wave 1 (BC28) | The app now targets Business Central 28.0 and AL runtime 17.0. The version moves from 1.0 to 28.0 because the major version now follows the Business Central platform. | 31339 |

## Detailed Feature Information

---

### AppSource object range and BRC prefixes (#18454)

AppSource requires every app to use the object ID range assigned to its publisher. Version 1.0.27121.0 still used a per-tenant development range (70000-70099).

All of the app's objects are now numbered in BrightCom's assigned AppSource range, 12073394-12073468. This covers tables, pages, codeunits, enums, permission sets, and the fields that the app adds to the Customer and Vendor tables. Object names, field names and permission set names are unchanged.

The actions and FactBoxes that the app adds to the Customer and Vendor cards were renamed to carry the `BRC` prefix that AppSource validation requires:

- Actions: `FetchRiskData` → `BRCFetchRiskData`, `ViewRiskAssessment` → `BRCViewRiskAssessment`, `AddToWatchlist` → `BRCAddToWatchlist`
- FactBoxes: `RiskFactBox` → `BRCRiskFactBox`, `WatchlistInfoFactBox` → `BRCWatchlistInfoFactBox`

Captions and behaviour are unchanged, so users see the same actions and FactBoxes as before.

---

### Business Central 2026 release wave 1 (BC28) (#31339)

The app now targets Business Central 2026 release wave 1:

- `platform` and `application` move from `26.0.0.0` to `28.0.0.0`
- `runtime` moves from `15.0` to `17.0`
- the app version moves from `1.0.0.0` to `28.0.0.0`

From this release, the app's major version follows the Business Central platform it targets. That is why the version jumps from 1.0 to 28.0. The app still targets Business Central online only (`target: Cloud`). It compiled against BC28 without any code changes, so no functionality was added or removed.

## Breaking Changes

**Minimum Business Central version raised to 28.0.**

This release requires Business Central 28.0 (2026 release wave 1) or later, on AL runtime 17.0. Before this release the minimum was 26.0. Environments still on Business Central 26 or 27 cannot install this version and must upgrade first.

**Object IDs changed since 1.0.27121.0.**

Every object and table-extension field has a new ID, so an environment that has 1.0.27121.0 installed cannot be upgraded to this release in place. In that environment, uninstall 1.0.27121.0 and remove its data. Then install this release and repeat the setup: provider API key, risk levels, watchlists and links to business entities. Page personalizations that referenced the renamed Customer and Vendor card actions or FactBoxes must also be redone.

The app still has no dependencies on other BrightCom apps.

## Bugfixes

- None in this release.
