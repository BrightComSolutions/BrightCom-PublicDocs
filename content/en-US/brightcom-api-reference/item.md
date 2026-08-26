---
title: "Item"
linkTitle: "Item"
weight: 10
description: >
  Item master data, variants, units of measure, and cross-references (EAN/GTIN), plus BRC Connect's brand and web-enablement fields.
---

The Item resource covers standard item master data from BRC Core, plus three nested sub-resources (variants, units of measure, and cross-references) and BRC Connect's own extension fields on a separate endpoint.

## Item

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/items" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brccore/v1.0/companies({id})/items({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `number` | `No.` | |
| `displayName` | `Description` | |
| `displayName2` | `Description 2` | |
| `type` | `Type` | option |
| `blocked` | `Blocked` | boolean |
| `itemCategoryCode` | `Item Category Code` | |
| `baseUnitOfMeasure` | `Base Unit of Measure` | |
| `salesUnitOfMeasure` | `Sales Unit of Measure` | |
| `purchUnitOfMeasure` | `Purch. Unit of Measure` | |
| `unitCost` | `Unit Cost` | |
| `unitPrice` | `Unit Price` | |
| `lastDirectCost` | `Last Direct Cost` | |
| `standardCost` | `Standard Cost` | |
| `priceProfitCalculation` | `Price/Profit Calculation` | option |
| `grossWeight` | `Gross Weight` | |
| `netWeight` | `Net Weight` | |
| `unitsPerParcel` | `Units per Parcel` | |
| `unitVolume` | `Unit Volume` | |
| `inventoryPostingGroup` | `Inventory Posting Group` | |
| `genProdPostingGroup` | `Gen. Prod. Posting Group` | |
| `vatProdPostingGroup` | `VAT Prod. Posting Group` | |
| `countryRegionOfOriginCode` | `Country/Region of Origin Code` | |
| `tariffNo` | `Tariff No.` | |
| `statisticGroup` | `Statistics Group` | |
| `itemTrackingCode` | `Item Tracking Code` | |
| `serialNos` | `Serial Nos.` | |
| `lotNos` | `Lot Nos.` | |
| `vendorNo` | `Vendor No.` | |
| `vendorItemNo` | `Vendor Item No.` | |
| `leadTimeCalculation` | `Lead Time Calculation` | returned as formatted text; write support unconfirmed |
| `reorderingPolicy` | `Reordering Policy` | option |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
{
  "displayName": "Mountain Bike, Alpine 27\"",
  "unitPrice": 2495.00,
  "blocked": false
}
```

#### Response

```json
{
  "id": "8f14e45f-ceea-467e-b3b3-6b1e2e6e4a0a",
  "number": "1000",
  "displayName": "Mountain Bike, Alpine 27\"",
  "displayName2": "",
  "type": "Inventory",
  "blocked": false,
  "itemCategoryCode": "BIKES",
  "baseUnitOfMeasure": "PCS",
  "salesUnitOfMeasure": "PCS",
  "purchUnitOfMeasure": "PCS",
  "unitCost": 1450.00,
  "unitPrice": 2495.00,
  "lastDirectCost": 1450.00,
  "standardCost": 1450.00,
  "priceProfitCalculation": "Profit=Price-Cost",
  "grossWeight": 14.2,
  "netWeight": 13.5,
  "unitsPerParcel": 1,
  "unitVolume": 0.18,
  "inventoryPostingGroup": "RETAIL",
  "genProdPostingGroup": "RETAIL",
  "vatProdPostingGroup": "VAT25",
  "countryRegionOfOriginCode": "SE",
  "tariffNo": "",
  "statisticGroup": "1",
  "itemTrackingCode": "",
  "serialNos": "",
  "lotNos": "",
  "vendorNo": "40000",
  "vendorItemNo": "ALP-27-BLK",
  "leadTimeCalculation": "2W",
  "reorderingPolicy": "Fixed Reorder Qty.",
  "lastModifiedDateTime": "2026-08-20T09:12:31Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

### Item variants

Nested under `items` as `itemVariants`, and also reachable as its own top-level endpoint.

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/itemVariants" >}}

| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `itemId` | — | derived at read time by looking up the parent item; not stored |
| `itemNumber` | `Item No.` | |
| `code` | `Code` | |
| `description` | `Description` | |
| `description2` | `Description 2` | |
| `blocked` | `Blocked` | boolean |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |

### Item units of measure

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/itemUnitsOfMeasure" >}}

| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `itemId` | — | derived, not stored |
| `itemNumber` | `Item No.` | |
| `code` | `Code` | |
| `quantity` | `Qty. per Unit of Measure` | |
| `length` | `Length` | |
| `width` | `Width` | |
| `height` | `Height` | |
| `cubage` | `Cubage` | |
| `weight` | `Weight` | |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |

### Item references (EAN / GTIN cross-references)

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/itemReferences" >}}

| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `itemNumber` | `Item No.` | |
| `variantCode` | `Variant Code` | |
| `unitOfMeasure` | `Unit of Measure` | |
| `referenceType` | `Reference Type` | option — e.g. Bar Code, Vendor |
| `referenceTypeNo` | `Reference Type No.` | |
| `referenceNo` | `Reference No.` | the actual EAN/GTIN/vendor code value |
| `description` | `Description` | |
| `description2` | `Description 2` | |

{{% alert title="No lastModifiedDateTime on this endpoint" color="info" %}}
Unlike the other Item sub-resources, `itemReferences` doesn't expose a `lastModifiedDateTime` field.
{{% /alert %}}

## BRC Connect extension fields

Separate endpoint, joined to `items` above by `id`. All fields here are writable.

{{< apimethod method="GET" path="/api/brightcom/brcconnect/v1.0/companies({id})/items" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brcconnect/v1.0/companies({id})/items({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only, same value as the Core `items` `id` |
| `brcConEnabledWeb` | `BRC Enabled Web` | boolean |
| `brcConBrand` | `BRC Brand` | |
| `brcConItemParentNo` | `BRC Item Parent No.` | |
| `brcConDangerousGoods` | `BRC Dangerous Goods` | boolean |
| `brcConItemParentSorting` | `BRC Item Parent Sorting` | |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Response

```json
{
  "id": "8f14e45f-ceea-467e-b3b3-6b1e2e6e4a0a",
  "brcConEnabledWeb": true,
  "brcConBrand": "ALPINE",
  "brcConItemParentNo": "",
  "brcConDangerousGoods": false,
  "brcConItemParentSorting": 10,
  "lastModifiedDateTime": "2026-08-20T09:12:31Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

## Extended Info

Item and Item Variant messages also carry `extendedInfo` — BRC Connect's mechanism for flexible, source-specific attributes, independently at both the item and variant level. See the dedicated [Extended Info](extended-info/) page for the full explanation, field reference, and supported data types.
