---
title: BRCExtendedFinanceManagement 28.0.35382.0
categories: [BRC Extended Finance Management, ReleaseNotes]
description: Business Central 2026 release wave 1 (BC28) compatibility, with the minimum supported version raised to 28.0.
date: 2026-10-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Business Central 2026 release wave 1 (BC28) | The app now targets Business Central 28.0 (2026 release wave 1) and AL runtime 17.0. | 31339 |

## Detailed Feature Information

---

### Business Central 2026 release wave 1 (BC28) (#31339)

BRC Extended Finance Management is now built for Business Central 2026 release wave 1.

- The app's `platform` and `application` versions move from 26.0.0.0 to 28.0.0.0, and the AL runtime from 14.0 to 17.0.
- The app version is now 28.0.0.0, in line with the platform it targets.
- The app already targeted `Cloud`, and none of the APIs Microsoft removed in BC28 were in use, so no code changes were needed. Functionality is unchanged.

#### Related PR

- PR 15707 (BRCExtendedFinanceManagement): #31339 BC28: platform/application 28, runtime 17.0, version 28.0.0.0

## Breaking Changes

**Minimum Business Central version raised to 28.0 (2026 release wave 1).**

The app's required application and platform versions move from `26.0.0.0` to `28.0.0.0`. Environments on Business Central 27 or earlier cannot install this version and stay on the previous release, 26.0.34801.0, until they are updated.

The minimum BRC Core version is unchanged.

## Bugfixes

- None in this release.
