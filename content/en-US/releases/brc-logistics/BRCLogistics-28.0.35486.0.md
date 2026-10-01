---
title: BRCLogistics 28.0.35486.0
categories: [BRCLogistics, ReleaseNotes]
description: Business Central 2026 release wave 1 (BC28) compatibility, with Business Central 28.0 as the new minimum version.
date: 2026-10-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Business Central 2026 release wave 1 (BC28) | BRC Logistics now targets Business Central 28.0 (platform and application 28.0, runtime 17.0). | 31339 |

## Detailed Feature Information

---

### Business Central 2026 release wave 1 (BC28) (#31339)

BRC Logistics is now built for Business Central 2026 release wave 1:

- `platform` and `application` in app.json raised to 28.0.0.0 (previously `platform` 1.0.0.0 and `application` 25.0.0.0)
- `runtime` raised from 14.0 to 17.0
- app version base set to 28.0.0.0

The app already targeted `Cloud` and did not use any of the APIs Microsoft removed in BC28, so no code changes were needed. Functionality is the same as in 25.0.34869.0. This is what raises the minimum supported version (see Breaking Changes).

#### Related PR

- PR 15698 (BRCLogistics): #31339 BC28: platform/application 28, runtime 17.0, version 28.0.0.0

## Breaking Changes

**Minimum Business Central version raised to 28.0 (2026 release wave 1).**

The app's required platform and application versions move to `28.0.0.0`, and the runtime moves from `14.0` to `17.0`. Environments on Business Central 27 or earlier cannot install this version. They stay on the previous release, 25.0.34869.0, until the environment is updated.

## Bugfixes

No separate bugfixes in this release.
