---
title: BRC Extended Finance Management 26.0.30957.0
categories: [BRC Extended Finance Management, ReleaseNotes]
description: Customer contract access improvements and API enhancements
date: 2026-04-22
---

## Release Summary

| Feature                                      | Description                                                                     |   ID |
| -------------------------------------------- | ------------------------------------------------------------------------------- | ---: |
| Customer Card Contract Navigation            | Add direct link from customer card to view related contracts                    | 22273 |

## Detailed Feature Information

---

### Customer Card Contract Navigation (#22273)

Added new "BRC EFM Contracts" action to the Customer Card and Customer List pages, enabling users to quickly navigate from a customer record to view all related contracts.

**Business Value:** Streamlines the workflow for sales and customer service teams who need to review customer contracts. Instead of navigating through multiple menus, users can now access contract information directly from the customer record with a single click.

**Implementation Details:**

This feature includes several related enhancements:

#### Contract Category Field (#14220, #20785, #20810)

Added new Contract Category field to contracts functionality:
- New field available on contract records
- Displayed in contract list views
- Enables categorization and filtering of contracts by type

#### API Timestamp Tracking (#21659)

Added SystemModifyAt field to Contracts and Contract Lines API endpoints (pages 12099481 & 12099479):
- Enables external systems to track when contract records were last updated
- Supports incremental data synchronization scenarios
- Provides audit trail for contract modifications

---

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Fixed missing BRCCore dependency reference in repository (#14222)
