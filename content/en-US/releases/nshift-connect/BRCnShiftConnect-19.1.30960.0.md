---
title: nShift Connect 19.1.30960.0
categories: [nShift Connect, ReleaseNotes]
description: Improved multi-document PDF handling from nShift responses
date: 2026-04-22
---

## Release Summary

| Feature                                      | Description                                                                     |   ID |
| -------------------------------------------- | ------------------------------------------------------------------------------- | ---: |
| Improved Multi-Document Response Handling    | Download all PDF documents from nShift responses                                | 26433 |

## Detailed Feature Information

---

### Improved Multi-Document Response Handling (#26433)

Enhanced the nShift response handler to properly process and download all PDF documents returned in API responses. Previously, when nShift returned multiple documents (e.g., shipping label and customs declaration), only the first document was being downloaded.

**Business Value:** Ensures all shipping documents are captured and available in Business Central, preventing missing customs declarations, delivery notes, or other critical shipping documentation. This is particularly important for international shipments requiring multiple document types.

**Technical Details:**
- New improved response handler processes all documents in nShift API response
- Downloads all PDF documents, not just the first one
- Handles multiple document types (labels, customs forms, delivery notes)
- Maintains document association with shipment records

---

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Fixed issue where second and subsequent documents in nShift responses were not being downloaded (#26433)
