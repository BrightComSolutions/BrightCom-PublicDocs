---
title: BRC Connect 25.0.31515.0
categories: [BRCConnect, ReleaseNotes]
description: Three new features including location code validation, automatic inventory updates, and configurable JSON price handling.
date: 2026-05-08
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Location Code Validation | Purchase orders created via BRC Connect and Incoming Data now correctly populate location codes from the JSON payload, resolving BC validation errors in recent versions. | 20455 |
| Automatic Inventory Updates | Inventory updates are now sent automatically when promised receipt dates change, with improved duplicate detection based on full payload changes. | 24034 |
| JSON Price Toggle | Control whether BRC Connect uses JSON prices or Business Central price lists when creating sales and purchase orders. | 26003 |

## Detailed Feature Information

---

### Location Code Validation (#20455)

Purchase orders created via BRC Connect and Incoming Data now correctly populate location codes from the JSON payload, resolving BC validation errors in recent versions. The enhancement adds proper location code handling to both purchase line and header creation, ensuring that location codes specified in the JSON message are properly validated and applied to the resulting purchase documents.

---

### Automatic Inventory Updates (#24034)

Inventory updates are now sent automatically when promised receipt dates change, with improved duplicate detection based on full payload changes. The system now monitors for changes in promised receipt dates and automatically triggers inventory updates to connected web platforms, while the duplicate detection logic has been enhanced to compare full payload content rather than just basic identifiers, reducing false duplicate blocks.

---

### JSON Price Toggle (#26003)

Control whether BRC Connect uses JSON prices or Business Central price lists when creating sales and purchase orders. A new setup option allows installations to configure whether prices from incoming JSON messages should override Business Central's standard price lists, or whether BC price lists should take precedence, providing flexibility for different customer pricing workflows.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

None in this release.
