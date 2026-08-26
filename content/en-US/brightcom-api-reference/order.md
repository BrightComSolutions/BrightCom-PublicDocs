---
title: "Order"
linkTitle: "Order"
weight: 40
description: >
  Sales orders, closed invoices, and credit memos, with lines, buyer/payer/ship-to, payments, and delivery.
---

An order message serves three purposes, distinguished by `documentType`:

- **`order`** (default) — a sales order. Normally generates a sales order in the ERP; also used by the ERP to send order status back to the source system.
- **`invoice`** — an order that's already closed and shipped, such as a receipt from a point-of-sale system.
- **`credit memo`** — a credit memo that's already closed.

### Required fields for a successful order

`source` (origin — use your tenant code unless told otherwise), `orderDate`, `externalId`, `primaryWarehouseId` (optional), `buyer` (with at least an invoicing address including a country code), `shipTo` (optional; set `shipToAddresses` to one element on it), `payments` (at least a code and amount, multiple allowed), `currency` (optional), `totalAmount`, `totalExclVat`, `totalVat`, `totalFreight` (required if there's no line for shipping), `totalFreightVat`.

Line requirements: `partNo`, `variantCode` (optional), `quantity` (positive for an order, negative for a credit memo), `pricePerItem`, `vatPerItem`, `discountAmount`, `discountAmountVat`, `name` (recommended), `id` (a globally unique identifier for the line), `lineNumber` (optional — recommend 10000/20000/30000 to match BC's own numbering).

## Add an order to the queue

{{< apimethod method="POST" path="/order" >}}

Accepts **either** a single order object or a JSON array — the request body is sniffed for a leading `[`. An explicit batch route also exists at `POST /order/orders` (identical `List` body) if you'd rather always send arrays.

{{< apicols >}}
{{< apicol side="left" >}}
| Field | Type | Notes |
|---|---|---|
| `id` | string (GUID) | |
| `externalId` | string | |
| `documentNumber` | string | |
| `documentStatus` | string | |
| `customerReference` | string | |
| `documentType` | string | `order` (default) / `invoice` / `credit memo` |
| `relatedExternalId` | string | |
| `orderDate` | datetime | |
| `deliveryDate` | datetime | |
| `externalReference` | string | |
| `source` | string | |
| `created` | datetime | |
| `primaryWarehouseId` | string | |
| `buyer` | object | [Customer](../customer/) shape |
| `payer` | object | [Customer](../customer/) shape |
| `shipTo` | object | [Customer](../customer/) shape |
| `seller` | object | [Customer](../customer/) shape |
| `deliveryMethod` | object | See [Delivery method](#delivery-method) below |
| `payments` | array of object | See [Payment](#payment) below |
| `items` | array | Full [Item](../item/) objects, when included |
| `lines` | array of object | See [Order line](#order-line) below |
| `currency` | string | |
| `comment` | string | |
| `totalAmount` | number | |
| `totalExclVat` | number | |
| `totalVat` | number | |
| `totalFreight` | number | |
| `totalFreightVat` | number | |
| `freightDiscount` | number | |
| `freightDiscountVat` | number | |
| `discountPct` | number | |
| `discountAmount` | number | |
| `centRounding` | number | |
| `discountCode` | string | |
| `extendedInfo` | array | See [Extended Info](../extended-info/) |
| `checksum` | string | |
| `freight` | number | |
| `freightVat` | number | |
| `deductedTax` | number | |
| `hasDeductedTax` | boolean | |
| `duties` | number | |
| `dutiesVat` | number | |
| `fees` | number | |
| `feesVat` | number | |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
{
  "externalId": "SHOP-100245",
  "documentType": "order",
  "source": "example-shop",
  "orderDate": "2026-08-25T00:00:00Z",
  "primaryWarehouseId": "MAIN",
  "buyer": {
    "firstName": "Anna",
    "lastName": "Karlsson",
    "email": "anna.karlsson@example.com",
    "invoicingAddress": {
      "address1": "Storgatan 4",
      "city": "Göteborg",
      "zip": "411 03",
      "country": "SE"
    }
  },
  "payments": [
    { "code": "CARD", "amount": 2495.00 }
  ],
  "currency": "SEK",
  "totalAmount": 2495.00,
  "totalExclVat": 1996.00,
  "totalVat": 499.00,
  "totalFreight": 0,
  "totalFreightVat": 0,
  "lines": [
    {
      "id": "d3a7e2c4-b5f4-4a10-8c2e-1f6a3b9d5e77",
      "lineNumber": 10000,
      "partNo": "10023",
      "variantCode": "050-ONE",
      "name": "Outdoor Scarf",
      "quantity": 1,
      "pricePerItem": 1996.00,
      "vatPerItem": 499.00
    }
  ],
  "extendedInfo": []
}
```

#### Response

```
201 Created
"1 order(s) queued"
```
{{< /apicol >}}
{{< /apicols >}}

### Order line

| Field | Type | Notes |
|---|---|---|
| `id` | string (GUID) | Globally unique identifier for the line |
| `externalId` | string | |
| `lineNumber` | number | Recommend 10000/20000/30000 to match BC |
| `parentLineNumber` | number | |
| `partNo` | string | |
| `name` | string | |
| `warehouseCode` | string | |
| `quantity` | number | Positive for an order, negative for a credit memo |
| `pricePerItem` | number | Before discount, excl. VAT |
| `vatPerItem` | number | |
| `discountPct` | number | |
| `discountAmount` | number | Excl. VAT, for the whole line |
| `discountAmountVat` | number | VAT portion of the line discount |
| `checksum` | string | |
| `variantCode` | string | |
| `unitOfMeasure` | string | |
| `totalLineAmount` | number | |
| `dropShipment` | boolean | |
| `extendedInfo` | array | See [Extended Info](../extended-info/) — Order is one of the resources where it appears at both header and line level |
| `shippedQuantity` | number | |
| `invoicedQuantity` | number | |

### Delivery method

| Field | Type |
|---|---|
| `id` | string (GUID) |
| `externalId` | string |
| `code` | string |
| `agentId` | string |
| `extendedInfo` | array |
| `checksum` | string |
| `price` | number |
| `vat` | number |

Use `code` and `externalId`, and build a transformation table in BC unless you have both the shipping agent and service code.

### Payment

| Field | Type |
|---|---|
| `id` | string (GUID) |
| `externalId` | string |
| `code` | string |
| `paymentReference` | string |
| `amount` | number |
| `extendedInfo` | array |
| `checksum` | string |

You may specify multiple payments — e.g. to distinguish a payment from a discount. BC places one payment method on the order header but represents multiple payments as order lines. Use `code` and `externalId` for routing, and `paymentReference` if you need it to surface as the external document number.

## Retrieve orders from the queue

{{< apimethod method="GET" path="/order" >}}

| Query parameter | Notes |
|---|---|
| `count` | Number of entries to retrieve. Default 100 if omitted. |
| `acknowledge` | The `acknowledgeToken` from your previous batch — pass it to close that batch and advance the queue. |

```json
{
  "count": 1,
  "acknowledgeToken": "9d3a7e2c-4b5f-4a10-8c2e-1f6a3b9d5e77",
  "nextLink": "/order?acknowledge=9d3a7e2c-4b5f-4a10-8c2e-1f6a3b9d5e77",
  "data": [
    {
      "externalId": "SHOP-100245",
      "documentNumber": "SO-104502",
      "documentType": "order",
      "documentStatus": "Open",
      "extendedInfo": []
    }
  ]
}
```

{{% alert title="A GET /order/orders also exists — don't use it" color="warning" %}}
There's also a `GET /order/orders` route that just redirects to the same result as `GET /order` above. It's hidden from the published API spec and marked in the Gateway's own source as unexplained leftover ("Todo: why do we have this redirect?"). Use `GET /order`.
{{% /alert %}}
