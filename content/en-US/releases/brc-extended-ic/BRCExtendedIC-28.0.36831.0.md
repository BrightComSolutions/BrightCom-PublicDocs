---
title: BRCExtendedIC 28.0.36831.0
categories: [BRCExtendedIC, ReleaseNotes]
description: Users and apps without Extended IC permissions can delete records again when the global delete trigger is on.
date: 2026-10-14
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Deletes without Extended IC permissions | Users and apps that have no Extended IC permissions no longer get a permission error when they delete records in a company that uses Extended IC. | 31975 |

## Detailed Feature Information

---

### Deletes without Extended IC permissions (#31975)

When Extended IC's global delete trigger is on, every delete in the company runs Extended IC's relation clean-up. That clean-up read the **BRC ExtIC Relation** table with the permissions of the user doing the delete. A user or an app without Extended IC permissions got the error *"TableData 12097468 BRC ExtIC Relation Read"* and the delete stopped. This hit integration users and deployment apps that only have permission sets such as D365 AUTOMATION.

Extended IC now checks whether the user can read its tables first. If not, it steps aside and the delete goes ahead. No permissions are added or raised. Users keep exactly the access they had.

- **Relation clean-up.** A user who cannot read BRC ExtIC Relation can delete the record. Any IC relation to that record is left in place, and the partner is not told about the delete. Users with Extended IC permissions work exactly as before.
- **Master data rename log.** The same check applies when the rename log is on. Renames and deletes by a user who cannot read the Extended IC data export setup are not logged.

Related PR:

- PR 16218: Skip Extended IC global trigger logic for users without read permission

## Breaking Changes

No breaking changes in this release.

**Behaviour change when the master data rename log is on.** Before this version, Extended IC could switch off Business Central's global delete and rename triggers for tables that are not in the data export setup. It now only switches them on. Other features that rely on those triggers run as configured again, for example the change log, Dataverse sync, API webhooks and data archive. IC partners may start receiving "Delete Record" updates that were skipped before.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Permission error on delete | Deleting records failed with a BRC ExtIC Relation permission error for users and apps without Extended IC permissions. | 31975 |
