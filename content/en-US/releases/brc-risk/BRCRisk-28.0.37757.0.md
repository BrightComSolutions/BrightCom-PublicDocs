---
title: BRCRisk 28.0.37757.0
categories: [BRCRisk, ReleaseNotes]
description: Credit score thresholds are evaluated the right way round, so a good credit score no longer gives CRITICAL, and the links on the risk fact boxes and Business Entity Card now open the right pages.
date: 2026-10-28
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Working links from risk fact boxes and Business Entity Card | Fields and actions that look like links now open the right page. | 32005 |
| Credit score risk level fixed | Credit score thresholds count as met at or below the threshold value. | 32004 |

## Detailed Feature Information

---

### Working links from risk fact boxes and Business Entity Card (#32005)

Several fields looked like links but did not take you anywhere useful. Now:

- **Risk Assessment fact box** (Customer and Vendor Card): Credit Score opens the Business Entity Card, like Company Name and View Details.
- **Watchlist Information fact box**: Member of Watchlists and Watchlist Codes open Risk Watchlists. If the company is not on any enabled watchlist, all watchlists open instead of the "not a member" message.
- **Business Entity Card** and **Linked Entity fact box**: Customer Name and Vendor Name open the customer or vendor card, like the No. fields next to them.
- **Customer and Vendor Card**: View Risk Assessment opens the Business Entity Card instead of a placeholder message.

The permission set BRC RISK - VIEW gets execute permission on the codeunit that opens linked customers and vendors. It cannot change any data with it.

### Credit score risk level fixed (#32004)

A higher credit score means lower risk, but every threshold was evaluated as "at or above". With the default setup, every company with a credit score of 40 or more qualified for CRITICAL, which is set to Block. A company with a score of 100, no debt and no payment marks could be blocked.

- **Risk Level Threshold** has a new **Comparison** field (At or Above / At or Below). Credit score thresholds default to At or Below. The MINIMAL threshold (86 or higher) stays At or Above.
- A credit score of 0 is treated as "no score" and shown with the Ambiguous style.
- On upgrade, existing credit score thresholds are converted (except the default MINIMAL 86) and risk levels on all business entities are recalculated.

## Breaking Changes

- **Risk levels change after the upgrade.** Business entities are recalculated with the corrected credit score logic. Customers and vendors with Risk Action Block or Warn may get a different result than before. The recalculation does not raise **OnRiskLevelChanged**.
- **GetCreditScoreStyle()** (public) now returns Ambiguous for a credit score of 0.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Risk level wrong for credit score | A good credit score gave CRITICAL because credit score thresholds were evaluated as "at or above". | 32004 |
