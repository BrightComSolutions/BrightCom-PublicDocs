---
title: BRC Logistics 25.0.33924.0
categories: [BRCLogistics, ReleaseNotes]
description: InRetrn integration moves to API v3, and return reference fields are widened to 30 characters.
date: 2026-08-19
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| InRetrn API v3 for return orders | The InRetrn return order integration now calls API v3 instead of v2, giving access to the current InRetrn feature set. | 27683 |
| Return reference fields widened to 30 characters | Return reference fields have been aligned at 30 characters so warehouse document numbers can be copied through the return flow without error. | 29768 |

## Detailed Feature Information

---

### InRetrn API v3 for return orders (#27683)

The InRetrn integration was hard-coded to API **v2** for all return order requests. That limited access to functionality available only in later API versions and was becoming a long-term support concern.

Return order requests now use **v3**. This is the version customers need in order to get the full feature set of the InRetrn integration.

#### Related PR

- PR 15121 (BRCLogistics): Change version to v3 for return order

---

### Return reference fields widened to 30 characters (#29768)

The warehouse header **No.** field is 30 characters, but the return reference fields it is copied into were only 20. When a warehouse document number exceeded 20 characters, the copy failed and interrupted the return and exchange workflow.

The following fields are now 30 characters, matching their source:

- **Sales Header** — "BRC Logi Return Reference No.", from 20 to 30
- **Return Exchange Entry** — "Reference No.", from 20 to 30

Values copied from warehouse return documents now carry through the full process flow without truncation or validation errors.

#### Related PR

- PR 15119 (BRCLogistics): Increase length of fields

## Breaking Changes

No breaking changes in this release.

**Note:** two fields have been widened from `Code[20]` to `Code[30]`. Any extension or integration that reads these fields into a 20-character variable should be reviewed.

## Bugfixes

- Mismatched field lengths caused errors when copying warehouse document numbers into return reference fields (#29768)
