---
title: BRC Extended IC 26.0.31486.0
categories: [BRCExtendedIC, ReleaseNotes]
description: Bugfix for reversed intercompany flow scenarios.
date: 2026-05-07
---

## Release Summary

This release contains a bugfix for reversed IC flow handling.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Reversed IC Flow (#21719) — Fixed issues with reversed intercompany flows where the warehouse company initiates the transaction rather than the sales company, enabling complex IC scenarios where the normal flow direction is inverted.
