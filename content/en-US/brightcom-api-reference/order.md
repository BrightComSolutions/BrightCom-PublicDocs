---
title: "Order"
linkTitle: "Order"
weight: 40
description: >
  Sales order headers and lines, plus BRC Connect's shipping, cancellation, and status fields.
---

This resource is Business Central's Sales Header/Sales Line, filtered to `Document Type = Order`. Creating a new order always forces the document type to Order — you can't use these endpoints to create a quote or invoice.

## Sales order

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/salesOrders" >}}
{{< apimethod method="POST" path="/api/brightcom/brccore/v1.0/companies({id})/salesOrders" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brccore/v1.0/companies({id})/salesOrders({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `number` | `No.` | |
| `orderDate` | `Order Date` | |
| `documentDate` | `Document Date` | |
| `customerNumber` | `Sell-to Customer No.` | |
| `customerName` | `Sell-to Customer Name` | |
| `billToCustomerNumber` | `Bill-to Customer No.` | |
| `sellToAddressLine1` | `Sell-to Address` | |
| `sellToAddressLine2` | `Sell-to Address 2` | |
| `city` | `Sell-to City` | |
| `postalCode` | `Sell-to Post Code` | |
| `countryRegionCode` | `Sell-to Country/Region Code` | |
| `shipToCode` | `Ship-to Code` | |
| `shipToName` | `Ship-to Name` | |
| `shipToAddressLine1` | `Ship-to Address` | |
| `shipToAddressLine2` | `Ship-to Address 2` | |
| `salespersonCode` | `Salesperson Code` | |
| `currencyCode` | `Currency Code` | |
| `paymentTermsCode` | `Payment Terms Code` | |
| `paymentMethodCode` | `Payment Method Code` | |
| `shipmentMethodCode` | `Shipment Method Code` | |
| `locationCode` | `Location Code` | |
| `externalDocumentNumber` | `External Document No.` | |
| `requestedDeliveryDate` | `Requested Delivery Date` | |
| `promisedDeliveryDate` | `Promised Delivery Date` | |
| `status` | `Status` | **read-only**, option |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
{
  "customerNumber": "20000",
  "externalDocumentNumber": "SHOP-100245",
  "shipToName": "Anna Karlsson",
  "shipToAddressLine1": "Storgatan 4",
  "requestedDeliveryDate": "2026-09-01"
}
```

#### Response

```json
{
  "id": "9d3a7e2c-4b5f-4a10-8c2e-1f6a3b9d5e77",
  "number": "SO-104502",
  "orderDate": "2026-08-25",
  "documentDate": "2026-08-25",
  "customerNumber": "20000",
  "customerName": "Anna Karlsson",
  "billToCustomerNumber": "20000",
  "sellToAddressLine1": "Storgatan 4",
  "sellToAddressLine2": "",
  "city": "Göteborg",
  "postalCode": "411 03",
  "countryRegionCode": "SE",
  "shipToCode": "",
  "shipToName": "Anna Karlsson",
  "shipToAddressLine1": "Storgatan 4",
  "shipToAddressLine2": "",
  "salespersonCode": "WEB",
  "currencyCode": "SEK",
  "paymentTermsCode": "14 DAGAR",
  "paymentMethodCode": "CARD",
  "shipmentMethodCode": "POSTNORD",
  "locationCode": "MAIN",
  "externalDocumentNumber": "SHOP-100245",
  "requestedDeliveryDate": "2026-09-01",
  "promisedDeliveryDate": "2026-09-01",
  "status": "Open",
  "lastModifiedDateTime": "2026-08-25T13:22:09Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

## Sales order line

Nested under `salesOrders` as `salesOrderLines`, and also reachable as its own top-level endpoint.

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/salesOrderLines" >}}

| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `documentId` | — | derived by looking up the parent order; not stored |
| `documentNumber` | `Document No.` | |
| `lineNumber` | `Line No.` | |
| `lineType` | `Type` | option — Item / Resource / G/L Account / etc. |
| `itemNumber` | `No.` | |
| `itemVariantCode` | `Variant Code` | |
| `description` | `Description` | |
| `description2` | `Description 2` | |
| `unitOfMeasureCode` | `Unit of Measure Code` | |
| `quantity` | `Quantity` | |
| `quantityShipped` | `Quantity Shipped` | **read-only** |
| `quantityInvoiced` | `Quantity Invoiced` | **read-only** |
| `quantityOutstanding` | `Outstanding Quantity` | **read-only** |
| `unitPrice` | `Unit Price` | |
| `lineDiscountPercent` | `Line Discount %` | |
| `lineDiscountAmount` | `Line Discount Amount` | |
| `lineAmount` | `Line Amount` | |
| `vatPercent` | `VAT %` | |
| `shipmentDate` | `Shipment Date` | |
| `locationCode` | `Location Code` | |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |

## BRC Connect extension fields

Separate endpoint, joined to `salesOrders` above by `id`. All fields here are writable. There is no Connect extension endpoint for order lines.

{{< apimethod method="GET" path="/api/brightcom/brcconnect/v1.0/companies({id})/salesOrders" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brcconnect/v1.0/companies({id})/salesOrders({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only, same value as the Core order's `id` |
| `brcConExternalDocumentNumber` | `BRC External Document No.` | a **separate** field from Core's `externalDocumentNumber` |
| `brcConSource` | `BRC Source` | |
| `brcConMarkForCancel` | `BRC Mark For Cancel` | boolean |
| `brcConShippingExtra1` | `BRC Shipping Extra 1` | |
| `brcConShippingExtra2` | `BRC Shipping Extra 2` | |
| `brcConShippingExtra3` | `BRC Shipping Extra 3` | |
| `brcConOrderComment` | `BRC Con Order Comment` | |
| `brcConStatus` | `BRC Con Status` | a Connect-specific status, distinct from Core's `status` |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Response

```json
{
  "id": "9d3a7e2c-4b5f-4a10-8c2e-1f6a3b9d5e77",
  "brcConExternalDocumentNumber": "SHOP-100245",
  "brcConSource": "SHOPIFY",
  "brcConMarkForCancel": false,
  "brcConShippingExtra1": "Leave at door",
  "brcConShippingExtra2": "",
  "brcConShippingExtra3": "",
  "brcConOrderComment": "Gift wrap requested",
  "brcConStatus": "SYNCED",
  "lastModifiedDateTime": "2026-08-25T13:22:09Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

{{% alert title="Two similarly-named fields" color="warning" %}}
`externalDocumentNumber` (Core) and `brcConExternalDocumentNumber` (Connect) are two different underlying BC fields on the same order — don't assume they're kept in sync automatically. Check with BrightCom Solutions which one your integration should read and write.
{{% /alert %}}

## Extended Info

Order messages also carry `extendedInfo`, at both header and line level — and it works inbound too: your integration can send its own `extendedInfo` codes when creating an order. See the dedicated [Extended Info](extended-info/) page for the full explanation, field reference, and supported data types.
