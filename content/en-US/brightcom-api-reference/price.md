---
title: "Price"
linkTitle: "Price"
weight: 20
description: >
  Price list entries per item/variant, with currency, VAT, and validity dates.
---

Each entry targets an item (optionally a specific variant) on a given price list, with price, VAT, and currency.

## Add price entries to the queue

{{< apimethod method="POST" path="/price" >}}

Accepts a JSON array of price entries.

{{< apicols >}}
{{< apicol side="left" >}}
| Field | Type | Notes |
|---|---|---|
| `id` | string (GUID) | |
| `externalId` | string | |
| `partNo` | string | |
| `source` | string | |
| `variantCode` | string | |
| `priceListCode` | string | |
| `priceListName` | string | |
| `appliesToType` | string | |
| `appliesToCode` | string | |
| `campaign` | boolean | Flags this entry as campaign pricing — not a campaign code/name |
| `price` | number | |
| `vat` | number | |
| `previousPrice` | number | |
| `previousVat` | number | |
| `currencyCode` | string | |
| `validFrom` | datetime | |
| `validUntil` | datetime | |
| `created` | datetime | |
| `checksum` | string | |
| `extendedInfo` | array | See [Extended Info](../extended-info/) |
| `minimumQuantity` | number | |
| `unitOfMeasure` | string | |
| `productRanges` | array | Channel/assortment flags — see [Extended Info](../extended-info/#important-characteristics) for how this differs from `extendedInfo` |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
[
  {
    "externalId": "10023-050-ONE-SUMMER26",
    "partNo": "10023",
    "source": "example-pim",
    "variantCode": "050-ONE",
    "priceListCode": "SUMMER26",
    "priceListName": "Summer Campaign 2026",
    "appliesToType": "Item",
    "appliesToCode": "10023",
    "campaign": true,
    "price": 249.00,
    "vat": 25,
    "currencyCode": "SEK",
    "validFrom": "2026-06-01T00:00:00Z",
    "validUntil": "2026-08-31T23:59:59Z",
    "unitOfMeasure": "PCS",
    "extendedInfo": []
  }
]
```

#### Response

```
201 Created
"1 price(s) queued"
```
{{< /apicol >}}
{{< /apicols >}}

## Retrieve price entries from the queue

{{< apimethod method="GET" path="/price" >}}

| Query parameter | Notes |
|---|---|
| `count` | Number of entries to retrieve. The API docs describe a default of 100 if omitted, though unlike the other resources this parameter has no code-level default value — pass it explicitly to be safe. |
| `acknowledge` | The `acknowledgeToken` from your previous batch — pass it to close that batch and advance the queue. |

```json
{
  "count": 1,
  "acknowledgeToken": "3b6a1f0e-9c2d-4e11-8a77-1e2f9b6d4c10",
  "nextLink": "/price?acknowledge=3b6a1f0e-9c2d-4e11-8a77-1e2f9b6d4c10",
  "data": [
    {
      "externalId": "10023-050-ONE-SUMMER26",
      "partNo": "10023",
      "variantCode": "050-ONE",
      "priceListCode": "SUMMER26",
      "price": 249.00,
      "currencyCode": "SEK",
      "extendedInfo": []
    }
  ]
}
```
