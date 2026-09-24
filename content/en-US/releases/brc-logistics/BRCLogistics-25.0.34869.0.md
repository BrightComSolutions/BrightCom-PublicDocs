---
title: BRC Logistics 25.0.34869.0
categories: [BRCLogistics, ReleaseNotes]
description: Picking-started events are detected again on Bitlog's new WMS API, so Shipment Notices are created for customers who have migrated.
date: 2026-09-24
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Picking-started events on the new Bitlog WMS API | Shipment Notices are created again for connections switched to Bitlog's new WMS API, whose order status feed has a different shape from the old one. | 27685 |

## Detailed Feature Information

---

### Picking-started events on the new Bitlog WMS API (#27685)

Bitlog's previous WMS API stops working at the end of September 2026. BRC Logistics supports the old and the new API side by side so each connection can be migrated on its own schedule, controlled by **Use API For Report** on the Bitlog connection.

On the new API the order status feed was still being read as though it were the old one. The connector looked for the events inside a `result` wrapper, and for fields named `type` and `time` carrying the value `started`. The new feed returns the event array **at the root**, and names those fields `eventType` and `eventTimeUtc`, with the value `PickingStarted`.

Nothing ever matched. For any connection already moved to the new API, **picking was never registered and no Shipment Notice was created** — the shipment order simply stayed open and was polled again on the next run.

This release corrects the reading of that feed:

- the event array is accepted whether it sits at the root or inside a `result` wrapper
- the event field names and the "picking started" value are chosen to match whichever API the connection is set to use
- the configured **Site** and **Tenant** are now sent with the order status feed request on the new API, as that API requires

#### How Shipment Notices are numbered

The old implementation used Bitlog's numeric event id, zero-padded, as the Shipment Notice number, and relied on that number to avoid creating the same notice twice.

The new API's status feed carries no event id, so this no longer works. A Shipment Notice is instead created **at most once per shipment order** — re-checked immediately before creation, so a notice raised in the meantime through another channel is also respected — and its number is taken from the warehouse document number series.

> **Before migrating a connection to the new API:** the Shipment Notice number is now taken from **No. Series Whse. Document** on BRC Logistics Setup. This flow previously supplied its own number and never consulted that field. If it is blank, creating the notice will fail on a missing-field error.

Shipment Notices raised by this flow will therefore carry document numbers from your own number series rather than Bitlog event ids. Existing notices are untouched.

#### Item adjustments

Where an item adjustment payload omits the `Warehouse` field altogether, the connection's own **Identifier** is now used instead of leaving the warehouse blank.

#### Related PRs

- PR 15452 (BRCLogistics): Feature/27685 CheckForPickingStarted

## Breaking Changes

No breaking changes to configuration or data. Note the numbering change described above: Shipment Notices created from Bitlog picking-started events are now numbered from **No. Series Whse. Document** rather than from the Bitlog event id, and that field must be populated on connections using this flow.

## Bugfixes

No separate bugfixes in this release.
