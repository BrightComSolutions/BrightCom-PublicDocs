---
title: BRCLogistics 28.0.38056.0
categories: [BRCLogistics, ReleaseNotes]
description: Item sync to WMS sends only the items that changed, from one item selection per setup, and can skip payloads WMS already has. Transfer-order shipments from WMS can top up inventory automatically.
date: 2026-11-02
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Item sync to WMS: changed items only, one item selection | Auto-send Changed Items sends only items that changed since the previous run, including changes to variants, units of measure, references and translations. A single Item Selection View replaces the old item selection settings. Unchanged item payloads can be skipped. | 30185 |
| Automatic inventory adjustment for transfer-order shipments | When a transfer shipment reported by WMS can't post because Business Central has too little inventory at the transfer-from location, BRC Logistics can post a positive adjustment for the missing quantity and retry. | 27881 |

## Detailed Feature Information

---

### Item sync to WMS: changed items only, one item selection (#30185)

Until now, a change to one item could resend every item to WMS, and items changed while a run was processing could be missed. Item sync has been reworked around three settings on the BRC Logistics setup.

**Item Selection View.** One filter on the Item table, set with the lookup, decides which items go to WMS. Empty means all items. The same selection is used everywhere: auto-send, the item card and list, the new **Send All Items to WMS** action, item balances, and the check that decides whether order lines for an item go to WMS. It replaces **All Items Enabled**, **Item Field No. for Enable** and **Item Available Filter View**, which are now obsolete and hidden. The upgrade moves the old settings into the view (see Breaking Changes).

**Which changes send an item.** With **Auto-send Changed Items** on, each run sends the items changed since the previous run:

- changes to the item itself, and
- inserts, changes, renames and deletes of its variants, units of measure, item references and translations. A reference moved to another item sends both items.

The window runs from the previous run, minus **Changed Items Overlap (Seconds)** (default 60, maximum 3600), to the start of the current run, so a change made during a run is picked up by the next one.

**Skip Unchanged Item Payloads** (off by default). When it's on, an item payload identical to the last one WMS received for that setup and SKU isn't sent again. The warehouse transaction gets the status **Unchanged - Not Sent**. It applies to the integrations that send one payload per SKU: Ongoing, Bitlog, Extend, ILG, Logiwa, Snap, Deposco, mintsoft, DSV, PrimePenguin, Nyce, Nowaste, 3PL, Alyson, ShipHero, VeraCore, Zenventory, Aditro, JD and Speedgroup. An item request from the item card or list, **Send All Items to WMS**, **Send Request** on a transaction, and a change of the item selection always send.

After you change the item selection, the setup card offers **Send all items to WMS** in a notification. Run it as well after you point a setup at another WMS environment, for example from test to production.

### Automatic inventory adjustment for transfer-order shipments (#27881)

When WMS reports stock that Business Central hasn't registered yet, a transfer shipment from WMS can fail to post because of Prevent Negative Inventory. A new group, **Qty. Adjustment For Shipment Orders**, on the BRC Logistics setup card handles this:

- **Auto Adjust Qty. On Shipment Orders** turns it on.
- **Item Journal** and **Journal Batch** name a dedicated item journal batch. It must be empty when an adjustment starts, because the whole batch is posted.
- **Reason Code** is a BRC Logistics reason code. Its posting groups and dimensions are applied to the journal lines.

After the first failed posting of an identified transfer-order shipment, BRC Logistics compares the shipped quantity with the inventory at the transfer-from location. It posts a positive adjustment for the difference only, then retries the shipment. Items with item tracking aren't adjusted: the shipment keeps its error, because the adjustment would need lot or serial numbers.

Off by default. Nothing changes until it's turned on and the journal, batch and reason code are set.

## Breaking Changes

**Item selection on upgrade (#30185).** The upgrade converts each setup's old item selection into **Item Selection View**:

- **All Items Enabled**, or nothing set: an empty view (all items).
- **Item Field No. for Enable** on a Boolean or Integer field, or an Option/Enum field with a value of ordinal 1: a view with the same filter.
- **Item Available Filter View**: copied as it is.
- **Item Field No. for Enable** on any other field: **not converted**. Item flows for that setup stop with an error until someone sets **Item Selection View**. This is logged in telemetry as BRCLGS-0008.

The fields **All Items Enabled**, **Item Field No. for Enable** and **Item Available Filter View** on the BRC Logistics setup are obsolete. Extensions or integrations that read or set them should use **Item Selection View** instead.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Items changed during an auto-send run were missed | A change saved while Auto-send Changed Items was running is now sent by the next run. | 30185 |
