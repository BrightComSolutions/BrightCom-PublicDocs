---
title: BRC PS Inkasso Connect 22.0.31279.0
categories: [BRCPSInkassoConnect, ReleaseNotes]
description: Bugfix ensuring Document No. is correctly populated when creating Cash Receipt Journal lines via the API.
date: 2026-04-30
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Cash Receipt Journal API Document Number Fix | Fixes an issue where the Document No. field was not populated when creating Cash Receipt Journal lines via the API, ensuring correct document numbering for all API-created journal entries. | 27032 |

## Detailed Feature Information

---

### Cash Receipt Journal API Document Number Fix (#27032)

Fixes an issue where the Document No. field was not populated when creating Cash Receipt Journal lines via the API, ensuring correct document numbering for all API-created journal entries. The Cash Receipt Journal API page has been updated to set the document number on insert via a trigger, so that lines created through the API carry a consistent and traceable document number from the point of creation.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Cash Receipt Journal API Document Number Fix (#27032)
