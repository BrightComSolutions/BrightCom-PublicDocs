---
title: BRC Retail Extension 24.4.32290.0
categories: [BRCRetailExtension, ReleaseNotes]
description: Variant selection prompt now appears on Sales Return Order lines, matching existing Sales Order behavior.
date: 2026-05-31
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Variant Selection Prompt on Sales Returns | Ensures the same variant selection popup used on Sales Orders is also shown on Sales Return Orders for consistent and error-free return handling. | 24182 |

## Detailed Feature Information

---

### Variant Selection Prompt on Sales Returns (#24182)

Retail users already rely on the automatic variant selection prompt when entering items on Sales Orders. That behavior has now been extended to Sales Return Orders, eliminating an inconsistency that previously led to slower processing and a higher risk of selecting the wrong item variant during returns.

**Behavior**

- When a user enters or validates an `Item No.` on a Sales Return Order line, the system triggers the same variant selection popup that already exists on Sales Orders.
- If the item has variants, the user must select one before continuing; the selected variant is then populated on the Sales Return Order line.
- The prompt only fires when the **Sales Line Variant Prompt** setting is enabled in Retail Setup — no new setup field is introduced.

**Scope**

The feature applies only to the Sales Return Order subform. It does not extend to Sales Credit Memos, posted return documents, or other sales-related lines. The existing variant selection logic and UI are reused, so behavior is identical across document types.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No bugfixes in this release.
