---
title: BRC Extended IC 26.0.31281.0
categories: [BRCExtendedIC, ReleaseNotes]
description: Cross-database intercompany support and a new reversed IC order flow direction.
date: 2026-04-30
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Cross-Database Extended IC Support | Adds support for using BRC Extended Intercompany alongside standard Business Central Intercompany when companies reside in different databases, expanding compatibility for multi-database intercompany setups. | 23388 |
| Reversed IC Order Flow | Implements support for a reversed intercompany order flow direction, enabling scenarios where the warehouse company initiates the intercompany transaction rather than the sales company, extending the flexibility of the Extended IC module. | 23368 |

## Detailed Feature Information

---

### Cross-Database Extended IC Support (#23388)

Adds support for using BRC Extended Intercompany alongside standard Business Central Intercompany when companies reside in different databases, expanding compatibility for multi-database intercompany setups. Previously, BRC Extended IC required all intercompany partners to exist within the same database. This release introduces credential configuration on the IC partner card to enable cross-database communication, with export and import groups defined for controlled data exchange.

---

### Reversed IC Order Flow (#23368)

Implements support for a reversed intercompany order flow direction, enabling scenarios where the warehouse company initiates the intercompany transaction rather than the sales company, extending the flexibility of the Extended IC module. New item card extensions, updated transaction management, and revised inbox/outbox handling together enable this alternative flow across the full IC transaction lifecycle.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No bugfixes in this release.
