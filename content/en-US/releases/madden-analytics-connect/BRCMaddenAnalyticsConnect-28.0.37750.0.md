---
title: BRCMaddenAnalyticsConnect 28.0.37750.0
categories: [BRCMaddenAnalyticsConnect, ReleaseNotes]
description: Statements sent to Madden now always carry invoicedDate, so statement-only transactions get the right date.
date: 2026-10-28
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| invoicedDate on statements | Statements on transactions and transactionsReturn now always include invoicedDate, taken from the posting date. | 31488 |

## Detailed Feature Information

---

### invoicedDate on statements (#31488)

When a transaction or transactionsReturn sent to Madden contained only a statement, it had no invoicedDate, and Madden used a fallback date. This could put the transaction on the wrong date in Madden's reporting.

Statements now always include **invoicedDate**: the posting date of the sales invoice (transactions) or the sales credit memo (transactionsReturn). Nothing else in the payload changes.

## Breaking Changes

No breaking changes in this release.
