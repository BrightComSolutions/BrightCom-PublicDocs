---
title: BRC Madden Analytics Connect 21.0.31280.0
categories: [BRCMaddenAnalyticsConnect, ReleaseNotes]
description: New API endpoints exposing line-level data for Purchase Orders and Transfer Orders.
date: 2026-04-30
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Purchase and Transfer Order Line APIs | Adds new API endpoints exposing line-level data for Purchase Orders and Transfer Orders, giving the Madden Analytics integration access to complete document details including individual line items. | 27097 |

## Detailed Feature Information

---

### Purchase and Transfer Order Line APIs (#27097)

Adds new API endpoints exposing line-level data for Purchase Orders and Transfer Orders, giving the Madden Analytics integration access to complete document details including individual line items. Previously the Purchase Order and Transfer Order APIs only exposed header-level data. This release adds dedicated line API pages for both document types, as well as updated header pages that reference the line endpoints, enabling full document retrieval in a single integration flow.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No bugfixes in this release.
