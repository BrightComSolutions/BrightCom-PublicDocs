---
title: BRCExtendedFinanceManagement 28.0.36085.0
categories: [BRCExtendedFinanceManagement, ReleaseNotes]
description: Adds a once-a-day usage signal so BrightCom can see which Contract Billing features are in use and spot problems early.
date: 2026-10-08
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | The app sends a once-a-day usage signal with configuration and activity counts to BrightCom's Application Insights. It contains no personal data and no document contents. | 31556 |

## Detailed Feature Information

---

### Daily usage telemetry (#31556)

BRC Extended Finance Management now sends one small usage signal per company per day to BrightCom's Application Insights. It helps BrightCom see which features are used and spot problems early.

The signal contains only counts, yes/no values and the names of setup options. It contains no personal data, no names, numbers or codes typed by users, and no document contents. It is sent to BrightCom only, and does not appear in your own telemetry. The app only reads data to build it, and nothing changes in your data.

The signal is sent on Business Central's own daily schedule. There is no job queue entry to set up.

Three events are sent:

- **BRCEFM-0101, Contract Billing configuration.** Which billing modes and switches are set up in the Sales Contract Setup, such as invoicing level, default invoice periodicity and whether deferral or phase-in pricing is on.
- **BRCEFM-0102, Module footprint.** How much each part of the app holds in the company: the number of contracts per status (quote, active, closed), and the number of contract types, contract categories, commission rules, chemical tax groups, bank account types and bank accounts that use a type.
- **BRCEFM-0103, Contract invoicing health.** How many active contracts are overdue for invoicing, how many have been overdue for more than 30 days, and how many have no next invoice date.

If a user does not have permission to read a table, that part is left out. The signal never causes an error.

The new codeunit is added to the **BRC EFM All** permission set.

#### Daily usage telemetry (#31556)

Adds the three daily events above for BRC Extended Finance Management.

#### Related PR

- PR 15909 (BRCExtendedFinanceManagement): #31556 Daily usage telemetry (BRCEFM-0101/0102/0103)

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No bugfixes in this release.
