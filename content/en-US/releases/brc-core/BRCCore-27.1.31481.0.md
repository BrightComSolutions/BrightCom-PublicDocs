---
title: BRC Core 27.1.31481.0
categories: [BRCCore, ReleaseNotes]
description: Bugfix for customs document EDI handling of weight and price values.
date: 2026-05-07
---

## Release Summary

This release contains a bugfix for customs document EDI output.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Customs Weight and Price Per Item (#27308) — Fixed EDI customs document to send per-item weight and price values instead of totals, correcting an issue where customs declarations were incorrectly reporting aggregate values rather than individual line item values.
