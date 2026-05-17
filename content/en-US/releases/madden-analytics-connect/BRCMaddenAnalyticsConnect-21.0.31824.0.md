---
title: Madden Analytics Connect 21.0.31824.0
categories: [BRCMaddenAnalyticsConnect, ReleaseNotes]
description: Bugfix for integration failure when item lines contain empty item numbers.
date: 2026-05-17
---

## Release Summary

This release contains a bugfix for integration stability when processing lines with empty item numbers.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Empty Item No Stops Integration (#27425) — Fixed an issue where the integration would fail when processing item lines with an empty item number. The integration now skips lines where item number is empty, preventing the failure and allowing the remainder of the document to be processed correctly.
