---
title: BRCConnect 28.0.37755.0
categories: [BRCConnect, ReleaseNotes]
description: Changing the expected receipt date on a purchase line now triggers an inventory update to the web side.
date: 2026-10-28
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Expected receipt date triggers inventory sync | Changing Expected Receipt Date on a purchase line queues the item for an inventory update to the web side. | 27432 |

## Detailed Feature Information

---

### Expected receipt date triggers inventory sync (#27432)

Until now, changing the expected receipt date on a purchase order was not enough to send the item to the web side. The new date only went out the next time the item was sent for another reason, or with a manual **Send to Web**.

Now, when **Expected Receipt Date** is changed on a purchase line for an item, BRC Connect queues that item for an inventory update. This happens when:

- **Integration Active** and **Auto Send Inventory Update** are on in BRC Connect Setup, and
- a BRC Connect Type that sends item inventory to the web has **Sync to Web on Modify** on.

The item goes through the normal outgoing queue, so the updated next-delivery information reaches the web side on the next queue run.

#### Expected receipt date change triggers item sync (#30209)

## Breaking Changes

No breaking changes in this release.
