---
title: BRCExtendedIC 26.0.32982.0
categories: [BRCExtendedIC, ReleaseNotes]
description: Extended Intercompany now works reliably across separate Business Central environments.
date: 2026-07-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Cross-environment Intercompany support | Extended IC order flow now propagates correctly between separate Business Central environments instead of assuming a single shared environment. | 27421 |

## Detailed Feature Information

---

### Cross-environment Intercompany support (#27421)

Extended Intercompany was reworked so the order flow operates correctly when the participating companies live in **separate Business Central environments**. Previously, cross-environment scenarios did not behave as intended; this update ensures intercompany order updates are exchanged and applied reliably across environment boundaries.

#### Related PR

- PR 14943 (BRCExtendedIC): Cross-Environment Updates

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- None in this release.
