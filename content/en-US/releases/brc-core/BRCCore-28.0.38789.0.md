---
title: BRCCore 28.0.38789.0
categories: [BRCCore, ReleaseNotes]
description: Delivered outbound messages now retain their source record identifier for callbacks.
date: 2026-11-12
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Archive source records for delivered messages | Delivered outbound messages retain the Source Record ID so the sender receives the record it originally sent. | 33685 |

## Detailed Feature Information

---

### Archive source records for delivered messages (#33685)

When an outbound message is delivered, BRC Core now archives its Source Record ID. The scenario's sender can therefore identify the record that it sent when handling the delivery callback.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Delivered messages lost their source record | Delivery callbacks no longer receive a blank Source Record ID. | 33685 |