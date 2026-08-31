---
title: BRC Core 27.1.34039.0
categories: [BRCCore, ReleaseNotes]
description: Price Book fields restored to the mainline, unblocking the AppSource upgrade, plus a bulk price API and batch engine rework.
date: 2026-08-25
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Stabilized and verified Price Book functionality | Restores Price Book work that had shipped only as a development deployment, correcting an upgrade failure and adding a bulk price API, a reworked batch engine, and price counters. | 25918 |
| Price Book produced no results without explanation | Price Book calculation could complete but return an empty result set with no indication of why. Addressed as part of the Price Book stabilization work. | 27555 |

## Detailed Feature Information

---

### Stabilized and verified Price Book functionality (#25918, #27555)

Price Book improvements that had previously been delivered to a customer as a development deployment were never merged back to the mainline. As a result, two fields existed in the deployed build but not in the released app, and the AppSource upgrade failed outright when it could not find them:

- `BRC Core Price Book` — field **Only Emit Explicit Prices** (Boolean)
- `BRC Core PB Miss` — field **Generation No.** (Integer)

Both fields are now restored on the mainline and the upgrade path is unblocked.

The same restoration brings across the rest of that work:

- **Bulk Price API** with an accompanying Swagger definition, for retrieving calculated prices in volume.
- **Batch engine rework** for price generation.
- **Price counters** via `GetPriceCount`, with separate Card and List counts, so it is visible how many prices a calculation actually produced.
- **Scope columns** on the Asset and Source subparts.
- An **upgrade-time purge** of stale `BRC Core PB Miss` rows (roughly 500,000 accumulated records), tagged `BRCCORE-27555-PURGE-PBMISS-20260526`.

Together these address the reported case where calculating a price book appeared to run successfully but produced an empty **Price Book Results** page with no reason given, and where prices could still appear for a unit of measure that had no price defined.

#### Related PR

- PR 15141 (BRCCore): Merge bugfix/27555-noprices into main — restore Price Book fields blocking the AppSource upgrade

## Breaking Changes

No breaking changes in this release.

**Upgrade note:** this release restores two table fields whose absence caused the AppSource upgrade to fail on tenants that had received the earlier development deployment. Upgrading to this version or later resolves that failure. The upgrade also purges stale `BRC Core PB Miss` rows, which may extend upgrade time on tenants with a large accumulated backlog.

## Bugfixes

- Price Book calculation returned no prices and gave no reason (#27555)
- AppSource upgrade failed on the missing Price Book fields "Only Emit Explicit Prices" and "Generation No." (#25918)
