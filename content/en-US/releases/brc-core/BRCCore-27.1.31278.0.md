---
title: BRC Core 27.1.31278.0
categories: [BRCCore, ReleaseNotes]
description: Bugfix for configurable receiver party ID in Customs Document mapping.
date: 2026-04-30
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Customs Document Party ID Configuration | Adds a configurable setting for the receiver party ID in Customs Document mapping, correcting an issue where the buyer and ship-to party IDs were incorrectly derived from the customer number. | 27070 |

## Detailed Feature Information

---

### Customs Document Party ID Configuration (#27070)

Adds a configurable setting for the receiver party ID in Customs Document mapping, correcting an issue where the buyer and ship-to party IDs were incorrectly derived from the customer number. The Customs Document Setup page and table have been updated to expose a dedicated receiver party ID field, allowing the correct identifier to be specified per setup rather than falling back to the customer number. Translation strings for the new field are included.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Customs Document Party ID Configuration (#27070)
