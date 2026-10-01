---
title: BRCConnect 28.0.35584.0
categories: [BRCConnect, ReleaseNotes]
description: App updates no longer switch Add Rounding Adjustment Line back on, plus Business Central 2026 release wave 1 (BC28) as the new minimum version.
date: 2026-10-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Add Rounding Adjustment Line is kept on app update | Updating or reinstalling BRC Connect no longer sets **Add Rounding Adjustment Line** back to on, so a setting you have turned off stays off. | 30438 |
| Business Central 2026 release wave 1 (BC28) | BRC Connect now targets Business Central 28.0 (platform and application 28.0, runtime 17.0). | 31339 |

## Detailed Feature Information

---

### Add Rounding Adjustment Line is kept on app update (#30438)

**Add Rounding Adjustment Line**, on BRC Connect Setup and on each BRC Connect Source, controls whether a rounding line is added to an imported document so its total matches the amount from the web. Customers who had turned the setting off found it turned back on every time BRC Connect was updated. After an update, orders could then pick up unexpected rounding adjustment lines until someone noticed and turned the setting off again.

Two pieces of code caused this:

- an upgrade step, meant to run only once long ago, ran on every app update and set the field to on in BRC Connect Setup and in every BRC Connect Source
- the install routine set the field to on in BRC Connect Setup on every install or reinstall

Both have been removed. App updates and reinstalls now leave the value you have chosen in place, whether it is on or off.

New setups still start with **Add Rounding Adjustment Line** turned on. That is now the field's default value on BRC Connect Setup, and a new BRC Connect Source still takes its value from the setup. Nothing changes for existing setups.

#### "Add Rounding Adjustment Line" is no longer set to TRUE on app update (#30750)

Customer-driven. Removes the repeating upgrade step and the install-time override, and makes "on" the default value on the Setup field instead.

#### Related PR

- PR 15736 (BRCConnect): #30750 Stop upgrade/install from resetting Add Rounding Adjustment Line

---

### Business Central 2026 release wave 1 (BC28) (#31339)

BRC Connect is now built for Business Central 2026 release wave 1:

- `platform` and `application` in app.json raised from 25.0.0.0 to 28.0.0.0
- `runtime` raised from 12.0 to 17.0
- app version base set to 28.0.0.0

The app already targeted `Cloud` and did not use any of the APIs Microsoft removed in BC28, so no code changes were needed. This is what raises the minimum supported version (see Breaking Changes).

#### Related PR

- PR 15697 (BRCConnect): #31339 BC28: platform/application 28, runtime 17.0, version 28.0.0.0

## Breaking Changes

**Minimum Business Central version raised to 28.0 (2026 release wave 1).**

The app's required platform and application versions move from `25.0.0.0` to `28.0.0.0`, and the runtime moves from `12.0` to `17.0`. Environments on Business Central 27 or earlier cannot install this version. They stay on the previous release, 25.0.34265.0, until the environment is updated.

## Bugfixes

No separate bugfixes in this release.
