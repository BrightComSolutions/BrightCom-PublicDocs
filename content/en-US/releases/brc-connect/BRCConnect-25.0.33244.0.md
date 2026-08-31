---
title: BRC Connect 25.0.33244.0
categories: [BRCConnect, ReleaseNotes]
description: New setup option to automatically reopen content records whose target document no longer exists.
date: 2026-07-15
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Auto reopen content when record not found | New setup toggle that resets content marked OK back to Validated when the document it points at no longer exists, so it can be reprocessed. | 29547 |

## Detailed Feature Information

---

### Auto reopen content when record not found (#29547)

Incoming content could be marked with status **OK** even though the document it was supposed to create no longer existed in Business Central — leaving no record and no obvious error, so the data was silently lost.

A new field, **Auto Reopen Content if Record Not Found**, has been added to the BRC Connect Setup card. When enabled, content processing verifies that the stored **Record ID** still resolves to a live record. If it does not, the content entry is reset from **OK** back to **Validated** and its stale Record ID is cleared, so the entry is picked up again on the next processing run instead of remaining a false success.

The check runs in both the single-content and process-all-contents paths. The setting is off by default, so existing behavior is unchanged unless it is enabled.

#### Related PR

- PR 15004 (BRCConnect): #29547 Added setup field to allow auto reopen content

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Incoming data marked OK but never created is now detected and reopened for retry (#29547)
