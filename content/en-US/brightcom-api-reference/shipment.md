---
title: "Shipment"
linkTitle: "Shipment"
weight: 50
description: >
  Posted sales shipment headers and lines, plus BRC Connect's read-only shipping extension fields.
---

This resource is Business Central's **posted** Sales Shipment — it represents shipments that have already happened, not open/pending ones. Treat it as read-mostly: posted documents aren't meant to change after the fact.

## Posted sales shipment

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/postedSalesShipments" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `number` | `No.` | |
| `shipmentDate` | `Shipment Date` | |
| `customerNumber` | `Sell-to Customer No.` | |
| `customerName` | `Sell-to Customer Name` | |
| `currencyCode` | `Currency Code` | |
| `salespersonCode` | `Salesperson Code` | |
| `externalDocumentNumber` | `External Document No.` | |
| `orderId` | — | derived by looking up the source order via `orderNumber`; blank if that order no longer exists as an open order |
| `orderNumber` | `Order No.` | |
| `locationCode` | `Location Code` | |
| `shipmentMethodCode` | `Shipment Method Code` | |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Response

```json
{
  "id": "1a4c8e6f-2b9d-4e33-a0f1-7c5d9e2b4a88",
  "number": "SHP-088310",
  "shipmentDate": "2026-08-26",
  "customerNumber": "20000",
  "customerName": "Anna Karlsson",
  "currencyCode": "SEK",
  "salespersonCode": "WEB",
  "externalDocumentNumber": "SHOP-100245",
  "orderId": "9d3a7e2c-4b5f-4a10-8c2e-1f6a3b9d5e77",
  "orderNumber": "SO-104502",
  "locationCode": "MAIN",
  "shipmentMethodCode": "POSTNORD",
  "lastModifiedDateTime": "2026-08-26T08:47:12Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

## Posted sales shipment line

Nested under `postedSalesShipments` as `postedSalesShipmentLines`, and also reachable as its own top-level endpoint.

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/postedSalesShipmentLines" >}}

| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `documentId` | — | derived by looking up the parent shipment; not stored |
| `documentNumber` | `Document No.` | |
| `lineNumber` | `Line No.` | |
| `lineType` | `Type` | option |
| `itemNumber` | `No.` | |
| `itemVariantCode` | `Variant Code` | |
| `description` | `Description` | |
| `unitOfMeasureCode` | `Unit of Measure Code` | |
| `quantity` | `Quantity` | |
| `unitPrice` | `Unit Price` | |
| `discountPercent` | `Line Discount %` | |
| `locationCode` | `Location Code` | |

{{% alert title="No description2 or lastModifiedDateTime on this endpoint" color="info" %}}
Unlike the sales order line resource, shipment lines don't carry a `description2` or a `lastModifiedDateTime` field.
{{% /alert %}}

## BRC Connect extension fields

Separate endpoint, joined to `postedSalesShipments` above by `id`. There is no Connect extension endpoint for shipment lines.

{{< apimethod method="GET" path="/api/brightcom/brcconnect/v1.0/companies({id})/postedSalesShipments" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only, same value as the Core shipment's `id` |
| `brcConExternalDocumentNumber` | `BRC External Document No.` | **read-only** |
| `brcConSource` | `BRC Source` | **read-only** |
| `brcConShippingExtra1` | `BRC Shipping Extra 1` | **read-only** |
| `brcConShippingExtra2` | `BRC Shipping Extra 2` | **read-only** |
| `brcConShippingExtra3` | `BRC Shipping Extra 3` | **read-only** |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Response

```json
{
  "id": "1a4c8e6f-2b9d-4e33-a0f1-7c5d9e2b4a88",
  "brcConExternalDocumentNumber": "SHOP-100245",
  "brcConSource": "SHOPIFY",
  "brcConShippingExtra1": "Leave at door",
  "brcConShippingExtra2": "",
  "brcConShippingExtra3": "",
  "lastModifiedDateTime": "2026-08-26T08:47:12Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

{{% alert title="Read-only, unlike Order" color="warning" %}}
Every `brcCon*` field on this endpoint is explicitly read-only — a genuine asymmetry compared to the Order resource, where the equivalent fields are writable. This matches the shipment being a posted, immutable document; don't build a PATCH against these fields.
{{% /alert %}}

## Extended Info

Shipment messages also carry `extendedInfo`, at both header and line level, same as Order. See the dedicated [Extended Info](extended-info/) page for the full explanation, field reference, and supported data types.
