---
title: BRC Core 27.1.30864.0
categories: [BRC Core, ReleaseNotes]
description: Customs JSON mapping correction for PostNord integration
date: 2026-04-20
---

## Release Summary

| Feature                                      | Description                                                                     |   ID |
| -------------------------------------------- | ------------------------------------------------------------------------------- | ---: |
| Customs JSON Mapping Correction              | Fixed incorrect field mapping in PostNord customs JSON                          | 26447 |

## Detailed Feature Information

---

### Customs JSON Mapping Correction (#26447)

Corrected an error in the Customs JSON mapping for PostNord integration where one field was mapped to the wrong data source. The contact/customer field key was incorrectly mapped to seller ID instead of the correct contact or customer number field.

**Business Value:** Ensures accurate customs documentation for international shipments using PostNord. Correct mapping prevents customs delays and potential compliance issues by providing accurate shipper and recipient information in customs declarations.

**Technical Details:**
- Fixed mapping of contact and Customer No. fields in PostNord customs JSON
- Corrected field that was previously mapped to seller ID
- Ensures proper shipper/recipient information in customs declarations
- Applies to international PostNord shipments requiring customs documentation

---

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Fixed incorrect field mapping in PostNord customs JSON (#26447)
