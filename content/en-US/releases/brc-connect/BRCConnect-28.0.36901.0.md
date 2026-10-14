---
title: BRCConnect 28.0.36901.0
categories: [BRCConnect, ReleaseNotes]
description: Posted transfer shipments reach the web side again, and the outgoing queue no longer marks documents as synced before their posting has finished.
date: 2026-10-14
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Transfer shipments reach the web side | Posted transfer shipments are sent reliably when Auto Send Transfer Shipment is on. | 32062 |

## Detailed Feature Information

---

### Transfer shipments reach the web side (#32062)

Posted transfer shipments could show as synced in BRC Connect without ever arriving on the web side. This was seen with transfer shipments posted through BRC Logistics.

Two things caused it, and both are fixed:

- **Auto Send Transfer Shipment was not honoured at the end of posting.** BRC Connect queues a posted transfer shipment again once posting has finished, but that step checked **Auto Send Sales Shipment** instead of **Auto Send Transfer Shipment**. With only the transfer setting on, the shipment was queued only once, in the middle of posting, before its lines existed. The step now runs when either setting is on. If you turned on Auto Send Sales Shipment to get transfer shipments sent, that keeps working.
- **The outgoing queue could pick up a document before its posting had finished.** **BRC Process Outgoing Queue** now only reads queue entries whose posting has completed. Entries from a posting that is still running are picked up on the next run, with the complete document.

A queue entry whose record changes while the job is processing it is no longer marked as synced. The next run sends the newer version.

No setup changes are needed.

Related PR:

- PR 16273: Stop marking transfer shipments synced before their posting has committed

## Breaking Changes

No breaking changes in this release.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Transfer shipments not sent | Posted transfer shipments were marked as synced but never reached the web side. | 32062 |
