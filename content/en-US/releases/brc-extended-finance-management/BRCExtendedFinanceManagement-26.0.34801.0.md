---
title: BRC Extended Finance Management 26.0.34801.0
categories: [BRC Extended Finance Management, ReleaseNotes]
description: Location Code on contract lines, controlled by a new contract setup option.
date: 2026-09-22
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Location Code on contract lines | A Location Code can now be set per contract line and is carried to the sales line when the contract is invoiced, so the items can be picked from inventory. Where it is allowed is controlled from BRC EFM Sales Contract Setup. | 27059 |

## Detailed Feature Information

---

### Location Code on contract lines (#27059)

Customer-driven development adds a **Location Code** to BRC contract lines, so a contract can specify where the items on a line are to be picked from.

**New setup option.** BRC EFM Sales Contract Setup gets an **Allow Location Code On** field with four options:

- **Do Not Allow** (default) — no Location Code on any line level
- **One-time Lines Only**
- **Recurring Lines Only**
- **Both One-time and Recurring Lines**

The Location Code column is shown on the One Time Lines and Recurring Lines subpages only where the setup allows it, so environments that do not want line-level locations see no change.

**Carried to the sales line.** When a contract line with a Location Code is invoiced, the location is transferred to the created sales line. A blank Location Code on the contract line leaves the sales line's own location logic untouched, so existing contracts keep behaving exactly as before.

#### Related PR

- PR 15371 (BRCExtendedFinanceManagement): Add WMS Location Code to BRC contract lines

## Breaking Changes

No breaking changes in this release. The new setup option defaults to **Do Not Allow**, which reproduces the previous behaviour.

## Bugfixes

- None in this release.
