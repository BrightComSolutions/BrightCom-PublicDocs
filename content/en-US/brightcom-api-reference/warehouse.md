---
title: "Warehouse"
linkTitle: "Warehouse"
weight: 30
description: >
  Stock levels and movements per warehouse — absolute quantities, deltas, and planning/history data.
---

Inventory levels and stock movements per warehouse, item, and variant — as absolute quantities and/or delta adjustments, optionally with incoming quantity, next delivery date, and forward planning / historical consumption data.

## Add warehouse entries to the queue

{{< apimethod method="POST" path="/warehouse" >}}

Accepts a JSON array of warehouse entries.

{{< apicols >}}
{{< apicol side="left" >}}
| Field | Type | Notes |
|---|---|---|
| `id` | string (GUID) | |
| `externalId` | string | |
| `checksum` | string | |
| `warehouseExternalId` | string | |
| `sourceWarehouseExternalId` | string | For transfer-type movements |
| `destinationWarehouseExternalId` | string | For transfer-type movements |
| `messageType` | string | |
| `comment` | string | |
| `source` | string | |
| `partNo` | string | |
| `variantCode` | string | |
| `quantity` | number | Absolute quantity |
| `deltaQuantity` | number | Adjustment relative to the last known quantity |
| `created` | datetime | |
| `incomingQuantity` | number | |
| `nextDelivery` | datetime | |
| `reasonCode` | string | |
| `transactionId` | string | |
| `name` | string | |
| `extendedInfo` | array | See [Extended Info](../extended-info/) |
| `type` | string | |
| `period` | string | |
| `planning` | array of object | See [Planning](#planning) below |
| `history` | array of object | See [History](#history) below |
| `productRanges` | array | Channel/assortment flags |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
[
  {
    "externalId": "MAIN-10023-050-ONE",
    "warehouseExternalId": "MAIN",
    "source": "example-erp",
    "partNo": "10023",
    "variantCode": "050-ONE",
    "quantity": 42,
    "deltaQuantity": -3,
    "created": "2026-08-26T08:00:00Z",
    "incomingQuantity": 100,
    "nextDelivery": "2026-09-05T00:00:00Z",
    "extendedInfo": []
  }
]
```

#### Response

```
201 Created
"1 warehouse entr(y/ies) queued"
```
{{< /apicol >}}
{{< /apicols >}}

### Planning

| Field | Type |
|---|---|
| `startPeriod` | datetime |
| `endPeriod` | datetime |
| `quantityPhysical` | number |
| `scheduledReceipt` | number |
| `grossRequirement` | number |
| `quantity` | number |

### History

| Field | Type |
|---|---|
| `periodStart` | datetime |
| `periodEnd` | datetime |
| `periodStartInventory` | number |
| `purchases` | number |
| `sales` | number |
| `other` | number |
| `periodEndInventory` | number |

## Retrieve warehouse entries from the queue

{{< apimethod method="GET" path="/warehouse" >}}

| Query parameter | Notes |
|---|---|
| `count` | Number of entries to retrieve. Default 100 if omitted. |
| `acknowledge` | The `acknowledgeToken` from your previous batch — pass it to close that batch and advance the queue. |

```json
{
  "count": 1,
  "acknowledgeToken": "6c2e9a4d-1a3b-4f60-9e0c-2d7a5f8b3c11",
  "nextLink": "/warehouse?acknowledge=6c2e9a4d-1a3b-4f60-9e0c-2d7a5f8b3c11",
  "data": [
    {
      "externalId": "MAIN-10023-050-ONE",
      "warehouseExternalId": "MAIN",
      "partNo": "10023",
      "variantCode": "050-ONE",
      "quantity": 42,
      "extendedInfo": []
    }
  ]
}
```
