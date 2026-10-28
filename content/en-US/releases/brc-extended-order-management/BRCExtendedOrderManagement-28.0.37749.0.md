---
title: BRCExtendedOrderManagement 28.0.37749.0
categories: [BRCExtendedOrderManagement, ReleaseNotes]
description: Price list import shows one summary message instead of one confirmation per price list.
date: 2026-10-28
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| One summary message for price list imports | Import Prices shows a single summary when it finishes instead of one confirmation per updated price list. | 30375 |

## Detailed Feature Information

---

### One summary message for price list imports (#30375)

**Import Prices** on Sales and Purchase Price Lists used to show Business Central's confirmation once for every price list it updated, which meant many clicks for a large import.

The import now verifies the draft lines itself and shows one message at the end with the number of price lists that were processed, verified, failed and skipped. Validations and blocking errors behave as before.

Swedish translations are included for the new message and for the purchase import's result message and verification question.

## Breaking Changes

No breaking changes in this release.
