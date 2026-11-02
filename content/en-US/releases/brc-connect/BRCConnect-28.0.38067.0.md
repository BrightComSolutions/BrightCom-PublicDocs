---
title: BRCConnect 28.0.38067.0
categories: [BRCConnect, ReleaseNotes]
description: Order dates from webshop timestamps are taken in local time, so orders placed late in the evening get the right date.
date: 2026-11-02
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Order dates from webshop timestamps in local time | When the order date or delivery date in a document from the webshop is a full timestamp, BRC Connect takes the date in local time instead of the UTC date. | 28107 |

## Detailed Feature Information

---

### Order dates from webshop timestamps in local time (#28107)

Webshops such as Shopify send timestamps in UTC. BRC Connect used to read the first ten characters, which is the UTC date. An order placed late in the evening, Swedish time, was therefore dated the next day.

When **orderDate** or **deliveryDate** in a sales or purchase document is a full ISO 8601 timestamp, BRC Connect now converts it to the time zone of the Business Central session that creates the document before taking the date. This sets **Order Date** and **Document Date**, and **Shipment Date** (sales) or **Requested Receipt Date** (purchases). Values sent as a plain date, for example `2026-11-05`, are read exactly as before.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Late-evening orders dated the next day | Orders whose UTC timestamp falls on the next day get the local date as Order Date. | 28107 |
