---
title: BRC Logistics 25.0.31820.0
categories: [BRCLogistics, ReleaseNotes]
description: Improved item adjustment message type handling for WMS integration.
date: 2026-05-17
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Item Adjustment Message Type Handling | Separates processing of item adjustment message types (inventory journal, item adjustment, item reclassification) to ensure each type creates the correct WMS transaction. | 22555 |

## Detailed Feature Information

---

### Item Adjustment Message Type Handling (#22555)

Separates processing of item adjustment message types (inventory journal, item adjustment, item reclassification) to ensure each type creates the correct WMS transaction. Previously, all incoming item adjustment messages were processed through a shared code path which did not differentiate between the different message types. The integration now routes each message type to the appropriate transaction creation logic, allowing inventory journals, item adjustments, and item reclassifications to be handled independently and correctly in Business Central.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No bugfixes in this release.
