---
title: BRCExtendedIC 28.0.35385.0
categories: [BRCExtendedIC, ReleaseNotes]
description: Master data import and export actions available for every IC Direction, plus Business Central 2026 release wave 1 (BC28) compatibility.
date: 2026-10-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Master Data actions no longer hidden by Direction | The Master Data import and export actions on the IC Partner card are now available whatever the partner's BRC Ext. IC Direction is, so a receiving (Incoming) company can still export master data. | 30249 |
| Business Central 2026 release wave 1 (BC28) | The app now targets Business Central 28.0 (2026 release wave 1) and AL runtime 17.0. | 31339 |

## Detailed Feature Information

---

### Master Data actions no longer hidden by Direction (#30249)

Since cross-environment support was added, the **BRC Ext. IC Direction** field on the IC Partner card also decided which Master Data actions were shown: export actions only for **Outgoing** partners, import actions only for **Incoming** partners.

That did not match how Extended IC is used. The receiving company (for example a warehouse company) is typically set up with Direction **Incoming**, yet it is often the company that exports master data to its partners. With the old behaviour it could not reach **Data Export Configuration** at all.

The Master Data actions are now shown for every Direction:

- Data Export Configuration and Data Import Configuration
- Send Table Definition and Deliver Outbox Now
- Execute Master Data Export and Execute Master Data Import
- Export Company Information

Where an action depends on the partner's inbox type, it is still enabled or disabled exactly as before. Import and export processing itself is unchanged.

#### Related PR

- PR 15321 (BRCExtendedIC): #30249 Remove visibility conditions for data export and import actions

---

### Business Central 2026 release wave 1 (BC28) (#31339)

BRC Extended IC is now built for Business Central 2026 release wave 1.

- The app's `platform` and `application` versions move from 27.0.0.0 to 28.0.0.0, and the AL runtime from 16.0 to 17.0.
- The app version is now 28.0.0.0, in line with the platform it targets.
- The app already targeted `Cloud`, and none of the APIs Microsoft removed in BC28 were in use, so no code changes were needed.

#### Related PR

- PR 15708 (BRCExtendedIC): #31339 BC28: platform/application 28, runtime 17.0, version 28.0.0.0

## Breaking Changes

**Minimum Business Central version raised to 28.0 (2026 release wave 1).**

The app's required application and platform versions move from `27.0.0.0` to `28.0.0.0`. Environments on Business Central 27 or earlier cannot install this version and stay on the previous release, 27.0.34466.0, until they are updated.

The minimum BRC Core version is unchanged (25.0.25005.0).

## Bugfixes

- None in this release.
