---
title: "Shipment"
linkTitle: "Shipment"
weight: 50
description: >
  Full or partial shipment notifications, with tracking and line-level handled/closed quantities.
---

Reports a fully or partially shipped order.

## Add a shipment to the queue

{{< apimethod method="POST" path="/shipment" >}}

Accepts **either** a single shipment object or a JSON array — the request body is sniffed for a leading `[`. An explicit batch route also exists at `POST /shipment/shipments` (identical `List` body) if you'd rather always send arrays.

{{< apicols >}}
{{< apicol side="left" >}}
| Field | Type | Notes |
|---|---|---|
| `id` | string (GUID) | |
| `externalId` | string | |
| `source` | string | |
| `created` | datetime | |
| `closed` | datetime | |
| `expectedDeliveryDate` | datetime | |
| `sourceWarehouseId` | string | |
| `targetWarehouseId` | string | |
| `status` | string | |
| `completelyShipped` | boolean | |
| `completleyReceived` | boolean | Spelled exactly like this on the wire ("Completley") — a typo in the underlying model, not yours to fix |
| `lines` | array of object | See [Shipment line](#shipment-line) below |
| `extendedInfo` | array | See [Extended Info](../extended-info/) |
| `checksum` | string | |
| `sourceName` | string | |
| `targetName` | string | |
| `reasonCode` | string | |
| `documentType` | string | |
| `trackingUrl` | string | |
| `trackingNo` | string | |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
{
  "externalId": "SHP-088310",
  "source": "example-erp",
  "created": "2026-08-26T08:47:12Z",
  "sourceWarehouseId": "MAIN",
  "completelyShipped": true,
  "trackingNo": "1234567890",
  "lines": [
    {
      "partNo": "10023",
      "variantCode": "050-ONE",
      "name": "Outdoor Scarf",
      "quantity": 1,
      "handledQuantity": 1,
      "closedQuantity": 1
    }
  ],
  "extendedInfo": []
}
```

#### Response

```
201 Created
"1 shipment(s) queued"
```
{{< /apicol >}}
{{< /apicols >}}

### Shipment line

| Field | Type | Notes |
|---|---|---|
| `id` | string (GUID) | |
| `externalId` | string | |
| `partNo` | string | |
| `variantCode` | string | |
| `name` | string | |
| `quantity` | number | |
| `handledQuantity` | number | |
| `closedQuantity` | number | |
| `extendedInfo` | array | See [Extended Info](../extended-info/) — Shipment is one of the resources where it appears at both header and line level |
| `status` | string | |
| `checksum` | string | |
| `price` | number | |
| `cost` | number | |
| `reasonCode` | string | |

## Retrieve shipments from the queue

{{< apimethod method="GET" path="/shipment" >}}

| Query parameter | Notes |
|---|---|
| `count` | Number of entries to retrieve. Default 100 if omitted. |
| `acknowledge` | The `acknowledgeToken` from your previous batch — pass it to close that batch and advance the queue. |

```json
{
  "count": 1,
  "acknowledgeToken": "1a4c8e6f-2b9d-4e33-a0f1-7c5d9e2b4a88",
  "nextLink": "/shipment?acknowledge=1a4c8e6f-2b9d-4e33-a0f1-7c5d9e2b4a88",
  "data": [
    {
      "externalId": "SHP-088310",
      "sourceWarehouseId": "MAIN",
      "completelyShipped": true,
      "trackingNo": "1234567890",
      "extendedInfo": []
    }
  ]
}
```

{{% alert title="A GET /shipment/shipments also exists — don't use it" color="warning" %}}
There's also a `GET /shipment/shipments` route that just redirects to the same result as `GET /shipment` above. It's hidden from the published API spec and marked in the Gateway's own source as unexplained leftover ("Todo: why do we have this redirect?"). Use `GET /shipment`.
{{% /alert %}}
