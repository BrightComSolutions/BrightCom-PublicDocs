---
title: BRC Core 27.1.33932.0
categories: [BRCCore, ReleaseNotes]
description: Permission corrections for the Atlas foundation so users without SUPER are unaffected.
date: 2026-08-20
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Atlas permission corrections | Permission set and global-trigger corrections in the Atlas foundation, ensuring users without SUPER — including those who never use Atlas — are not affected. | 24812 |

## Detailed Feature Information

---

### Atlas permission corrections (#24812)

Three permission-related defects in the newly shipped Atlas foundation have been corrected. All of them post-date the initial Atlas release and were found before any tenant began using the functionality.

**Usage statistics on the processing path.** The Atlas usage statistics table was granted only through the licence-management role, which no processing role includes. Because message handling writes to it on the caller's session, a user without SUPER could not process a message at all — the operation failed on insert rather than simply going uncounted. The table is now granted on the processing roles that need it.

**Global triggers must not affect non-Atlas users.** Two subscribers hang off `GlobalTriggerManagement` and therefore run for every user in the tenant: the Cargo Bay cleanup answers `OnDatabaseDelete` for every table, and the trigger watch list answers trigger setup for every table. Both performed a lazy read of an Atlas table, which could fail for a user who had never touched Atlas. Both reads are now guarded, so users who do not use Atlas are unaffected regardless of their permission set.

**Usage metering permissions.** The metering path has been aligned with the roles that actually invoke it.

Because Atlas is not yet in use on any tenant, no live scenario was affected. These are corrections made ahead of adoption rather than a hotfix.

#### Related PR

- PR 15124 (BRCCore): Atlas permission fixes for non-SUPER users (pages, triggers, usage metering)

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Users without SUPER could not process an Atlas message due to a missing table permission (#24812)
- Two Atlas global-trigger subscribers could fail for users who never use Atlas (#24812)
