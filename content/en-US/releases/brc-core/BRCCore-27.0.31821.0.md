---
title: BRC Core 27.0.31821.0
categories: [BRCCore, ReleaseNotes]
description: Bugfix for missing colli (package) information in EDI messages.
date: 2026-05-17
---

## Release Summary

This release contains a bugfix for colli information in EDI output.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Colli Info Missing from EDI (#27350) — Fixed an issue where colli (package/parcel) information was missing from outgoing EDI messages. The integration now correctly includes colli data in the EDI output, ensuring downstream systems receive complete shipment package information.
