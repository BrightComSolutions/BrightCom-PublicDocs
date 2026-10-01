---
title: BRCnShiftConnect 28.0.35366.0
categories: [nShift Connect, ReleaseNotes]
description: nShift Connect now targets Business Central 2026 release wave 1 (BC28), with a raised minimum version.
date: 2026-10-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Business Central 2026 release wave 1 (BC28) | The app is rebuilt for Business Central 28.0, and its version number now follows the Business Central platform. | 31339 |

## Detailed Feature Information

---

### Business Central 2026 release wave 1 (BC28) (#31339)

nShift Connect now targets Business Central 2026 release wave 1. The app's required platform and application versions move from `24.0.0.0` to `28.0.0.0`, and the AL runtime moves from `8.0` to `17.0`. The app remains a cloud (`Cloud` target) extension.

The app did not use any of the APIs Microsoft removed in BC28, so no code changes were needed: shipment booking, label printing and the customs settings introduced in earlier releases work exactly as before.

The version jumps from 19.1 to 28.0 because the app's major version now follows the Business Central platform it is built for.

#### Related PR

- PR 15713 (BRCnShiftConnect): BC28 — platform/application 28, runtime 17.0, version 28.0.0.0

## Breaking Changes

**Minimum Business Central version raised to 28.0 (2026 release wave 1).**

The app's required application and platform versions move from `24.0.0.0` to `28.0.0.0`. Environments still on Business Central 27 or earlier cannot install this version; they stay on the previous release, 19.1.34081.0, until the environment is updated.

## Bugfixes

- None in this release.
