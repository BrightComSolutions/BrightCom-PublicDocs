---
title: BRCExtendedIC 28.0.37756.0
categories: [BRCExtendedIC, ReleaseNotes]
description: Hotfix - turns Auto Release Sales Orders back on for every IC partner on upgrade, so incoming IC sales orders are released again.
date: 2026-10-28
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Auto Release Sales Orders restored on upgrade | Every IC partner gets Auto Release Sales Orders turned on once on upgrade, so incoming IC sales orders are released automatically again. | 31960 |

## Detailed Feature Information

---

### Auto Release Sales Orders restored on upgrade (#31960)

The IC Partner field **Auto Release Sales Orders** is meant to be on by default, but it was only set for existing partners on a new install. After an upgrade from a version without the field, existing IC partners had it off, so incoming IC sales orders (B2B and B2C) were created but no longer released.

This version turns **Auto Release Sales Orders** on for every IC partner in every company, once, on upgrade. If you want it off for a partner, switch it off again afterwards. Later upgrades will not turn it back on.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| IC sales orders no longer auto-released after upgrade | Existing IC partners had Auto Release Sales Orders off after an upgrade. | 31960 |
