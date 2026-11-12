---
title: BRCConnect 28.0.38802.0
categories: [BRCConnect, ReleaseNotes]
description: More reliable queue processing, controlled batch posting, scheduled cost adjustments and daily telemetry for BRC Connect operations.
date: 2026-11-12
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| More reliable outgoing queue processing | Outgoing integration data is processed more reliably between the queue and the connected back office. | 32160 |
| Scheduled small-batch cost adjustment | Standard cost adjustment item batches can be processed in smaller scheduled batches. | 33766 |
| Capped batch posting from the job queue | Sales orders, invoices and credit memos can be posted in capped batches from the job queue. | 33762 |
| Daily queue and operator telemetry | Daily telemetry records Connect job queue entries and Process Operator configuration. | 33761 |

## Detailed Feature Information

---

### More reliable outgoing queue processing (#32160)

Outgoing data processing between the BRC Logistics Outgoing Sync Queue and the connected back office has been corrected to improve reliability.

### Scheduled small-batch cost adjustment (#33766)

Cost adjustment item batches can be scheduled in smaller groups to make processing more predictable and manageable.

### Capped batch posting from the job queue (#33762)

Posting of sales orders, invoices and credit memos from the job queue can be capped into controlled batches.

### Daily queue and operator telemetry (#33761)

Daily telemetry now provides an inventory of Connect job queue entries and Process Operator configuration.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Unreliable outgoing queue processing | Corrected processing of outgoing integration data. | 32160 |