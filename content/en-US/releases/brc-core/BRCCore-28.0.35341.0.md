---
title: BRCCore 28.0.35341.0
categories: [BRCCore, ReleaseNotes]
description: Business Central 2026 release wave 1 (BC28) compatibility, with Business Central 28.0 and Intrastat Core 28.0 as the new minimum versions.
date: 2026-10-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Business Central 2026 release wave 1 (BC28) | BRC Core now targets Business Central 28.0 (platform and application 28.0, runtime 17.0) and requires Intrastat Core 28.0. | 31339 |

## Detailed Feature Information

---

### Business Central 2026 release wave 1 (BC28) (#31339)

BRC Core is now built for Business Central 2026 release wave 1:

- `platform` in app.json raised from 27.0.0.0 to 28.0.0.0, and `application` from 27.1.0.0 to 28.0.0.0
- `runtime` raised from 15.0 to 17.0
- the dependency on Microsoft's **Intrastat Core** app raised from 27.1.0.0 to 28.0.0.0
- app version base set to 28.0.0.0

The app already targeted `Cloud` and did not use any of the APIs Microsoft removed in BC28, so no code changes were needed. Functionality is the same as in 27.1.34039.0. This is what raises the minimum supported version (see Breaking Changes).

#### Related PR

- PR 15696 (BRCCore): #31339 BC28: platform/application 28, runtime 17.0, version 28.0.0.0

## Breaking Changes

**Minimum Business Central version raised to 28.0 (2026 release wave 1).**

The app's required platform and application versions move to `28.0.0.0` (from 27.0.0.0 and 27.1.0.0), and the runtime moves from `15.0` to `17.0`. The minimum version of the **Intrastat Core** dependency moves from `27.1.0.0` to `28.0.0.0`. Microsoft ships that version with Business Central 28.0.

Environments on Business Central 27 or earlier cannot install this version. They stay on the previous release, 27.1.34039.0, until the environment is updated.

## Bugfixes

No separate bugfixes in this release.
