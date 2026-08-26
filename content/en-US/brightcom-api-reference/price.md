---
title: "Price"
linkTitle: "Price"
weight: 20
description: >
  Price list headers and lines, plus BRC Connect's campaign and web-enablement fields.
---

BRC Core's modern Price List (not the legacy Sales Price table) backs this resource. A price list line is nested under its header as `priceListLines`, and is also reachable as its own top-level endpoint.

## Price list header

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/priceListHeaders" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brccore/v1.0/companies({id})/priceListHeaders({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `code` | `Code` | |
| `description` | `Description` | |
| `priceType` | `Price Type` | option — Sale / Purchase |
| `sourceType` | `Source Type` | option |
| `sourceNumber` | `Source No.` | |
| `startingDate` | `Starting Date` | |
| `endingDate` | `Ending Date` | |
| `currencyCode` | `Currency Code` | |
| `status` | `Status` | option — Draft / Active / Inactive |
| `allowLineDisc` | `Allow Line Disc.` | boolean |
| `allowInvoiceDisc` | `Allow Invoice Disc.` | boolean |
| `priceIncludesVAT` | `Price Includes VAT` | boolean |
| `vatBusinessPostingGroup` | `VAT Bus. Posting Gr. (Price)` | |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
{
  "description": "Summer Campaign 2026",
  "startingDate": "2026-06-01",
  "endingDate": "2026-08-31",
  "status": "Active"
}
```

#### Response

```json
{
  "id": "3b6a1f0e-9c2d-4e11-8a77-1e2f9b6d4c10",
  "code": "SUMMER26",
  "description": "Summer Campaign 2026",
  "priceType": "Sale",
  "sourceType": "All Customers",
  "sourceNumber": "",
  "startingDate": "2026-06-01",
  "endingDate": "2026-08-31",
  "currencyCode": "SEK",
  "status": "Active",
  "allowLineDisc": true,
  "allowInvoiceDisc": true,
  "priceIncludesVAT": false,
  "vatBusinessPostingGroup": "",
  "lastModifiedDateTime": "2026-08-15T07:40:02Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

## Price list line

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/priceListLines" >}}

| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `priceListCode` | `Price List Code` | join key back to the header's `code` |
| `lineNo` | `Line No.` | |
| `priceType` | `Price Type` | option |
| `sourceType` | `Source Type` | option |
| `sourceNumber` | `Source No.` | |
| `assetType` | `Asset Type` | option — Item / Resource / etc. |
| `assetNumber` | `Asset No.` | |
| `variantCode` | `Variant Code` | |
| `unitOfMeasureCode` | `Unit of Measure Code` | |
| `startingDate` | `Starting Date` | |
| `endingDate` | `Ending Date` | |
| `currencyCode` | `Currency Code` | |
| `minimumQuantity` | `Minimum Quantity` | |
| `unitPrice` | `Unit Price` | |
| `lineDiscountPercent` | `Line Discount %` | |
| `allowLineDisc` | `Allow Line Disc.` | boolean |
| `allowInvoiceDisc` | `Allow Invoice Disc.` | boolean |
| `status` | `Status` | option |

{{% alert title="No lastModifiedDateTime on this endpoint" color="info" %}}
Unlike the header, `priceListLines` doesn't expose a `lastModifiedDateTime` field.
{{% /alert %}}

## BRC Connect extension fields

Separate endpoint, joined to `priceListHeaders` above by `id`. All fields here are writable. There is no Connect extension endpoint for price list lines.

{{< apimethod method="GET" path="/api/brightcom/brcconnect/v1.0/companies({id})/priceListHeaders" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brcconnect/v1.0/companies({id})/priceListHeaders({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only, same value as the Core header's `id` |
| `brcConEnabledWeb` | `BRC Enabled Web` | boolean |
| `brcConCampaign` | `BRC Campaign` | |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Response

```json
{
  "id": "3b6a1f0e-9c2d-4e11-8a77-1e2f9b6d4c10",
  "brcConEnabledWeb": true,
  "brcConCampaign": "SUMMER26",
  "lastModifiedDateTime": "2026-08-15T07:40:02Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

## Extended Info

Price messages also carry `extendedInfo`, at a single flat level (one array per price row). See the dedicated [Extended Info](extended-info/) page for the full explanation, field reference, and supported data types.
