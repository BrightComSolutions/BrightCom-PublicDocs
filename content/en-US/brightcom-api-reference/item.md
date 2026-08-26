---
title: "Item"
linkTitle: "Item"
weight: 10
description: >
  Item, variant, and parent-grouping messages — non-variant items, BC-level variants, and virtual parent groupings.
---

An item message can represent one of three shapes, distinguished by `class`:

- **Non-Variant Item (`nonVariantItem`)** — has no variations, sold as-is.
- **Item with Variants (`itemWithVariants`)** — has variants in BC, sold at the variant level.
- **Item with Parent (`itemWithParent`)** — structurally an item in BC (like a non-variant item), but has a virtual parent that doesn't exist as an item in BC. Used to let external systems group these as if they were variants of a common parent.

### Queue semantics

If an item with the same identifier already exists in the queue, the new entry is added at the back as a copy, not merged in place. If the queue holds two or more copies of the same identifier with byte-wise identical content, they're deduplicated on retrieval; copies that differ are delivered in FIFO order. Posted items are filtered and transformed against the configured targets before delivery — an item can be culled entirely if it doesn't match a target's filters.

## Add items to the queue

{{< apimethod method="POST" path="/item" >}}

Accepts a JSON array of item entries.

{{< apicols >}}
{{< apicol side="left" >}}
| Field | Type | Notes |
|---|---|---|
| `id` | string (GUID) | |
| `externalId` | string | Your system's identifier for this item |
| `class` | string | `unclassified` / `nonVariantItem` / `itemWithVariants` / `itemWithParent` / `hasBom` |
| `parentPartNo` | string | For `itemWithParent` |
| `parentName` | string | |
| `partNo` | string | The item number |
| `source` | string | Origin of the message |
| `name` | string | |
| `description` | string | |
| `unitOfMeasure` | string | |
| `categoryCode` | string | |
| `itemType` | string | |
| `vatType` | string | |
| `unspscCode` | string | |
| `countryOfOrigin` | string | |
| `structure` | array | Bill-of-materials structure lines — not yet expanded field-by-field in this reference |
| `variants` | array | Variant entries — not yet expanded field-by-field in this reference |
| `crossReferences` | array | EAN/GTIN and other cross-references — not yet expanded field-by-field in this reference |
| `extendedInfo` | array | See [Extended Info](../extended-info/) |
| `productRanges` | array | Channel/assortment flags — code, channel, status, start/end date |
| `grossWeight` | number | |
| `netWeight` | number | |
| `dangerousGoods` | boolean | |
| `dropShipment` | boolean | |
| `checksum` | string | |
| `commodityCode` | string | |
| `status` | string | |
| `nameLocale` | object | Language code → localized name |
| `descriptionLocale` | object | Language code → localized description |
| `variantAttributes` | array of string | e.g. which attributes distinguish variants (`["Color", "Size"]`) |
| `brand` | string | |
| `mpn` | string | Manufacturer part number |
| `imageUrl` | string | |
| `suppliers` | array | Not yet expanded field-by-field in this reference |
| `units` | array | Not yet expanded field-by-field in this reference |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
[
  {
    "externalId": "10023",
    "class": "itemWithVariants",
    "partNo": "10023",
    "source": "example-pim",
    "name": "Outdoor Scarf",
    "brand": "EXAMPLE",
    "status": "Published",
    "variantAttributes": ["Color", "Size"],
    "imageUrl": "https://assets.example.com/10023/main.png",
    "extendedInfo": [
      { "code": "SeasonId", "valueType": "string", "stringValue": "2608", "value": "2608", "checksum": "", "id": "f55f8c70-26a3-4e72-abda-f5fc54241752" }
    ]
  }
]
```

#### Response

```
201 Created
"1 item(s) queued"
```
{{< /apicol >}}
{{< /apicols >}}

## Retrieve items from the queue

{{< apimethod method="GET" path="/item" >}}

| Query parameter | Notes |
|---|---|
| `count` | Number of entries to retrieve. Default 100 if omitted. |
| `acknowledge` | The `acknowledgeToken` from your previous batch — pass it to close that batch and advance the queue. |
| `groupByParentPartNo` | Group entries by their parent part number. Only relevant if you're using BC's item parent list feature. |

```json
{
  "count": 1,
  "acknowledgeToken": "8f14e45f-ceea-467e-b3b3-6b1e2e6e4a0a",
  "nextLink": "/item?acknowledge=8f14e45f-ceea-467e-b3b3-6b1e2e6e4a0a",
  "data": [
    {
      "externalId": "10023",
      "class": "itemWithVariants",
      "partNo": "10023",
      "source": "example-pim",
      "name": "Outdoor Scarf",
      "brand": "EXAMPLE",
      "status": "Published",
      "extendedInfo": []
    }
  ]
}
```
