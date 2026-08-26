---
title: "Customer"
linkTitle: "Customer"
weight: 15
description: >
  Customer master data, addresses, and contacts.
---

Creates or updates customers in Business Central. If a customer already exists on the queue, the entry is replaced by the new one — matched by e-mail address if present, otherwise by customer code.

## Add customers to the queue

{{< apimethod method="POST" path="/customer" >}}

Accepts a JSON array of customer entries.

{{< apicols >}}
{{< apicol side="left" >}}
| Field | Type | Notes |
|---|---|---|
| `id` | string (GUID) | |
| `externalId` | string | |
| `customerNumber` | string | |
| `source` | string | |
| `firstName` | string | |
| `lastName` | string | |
| `companyName` | string | |
| `customerType` | string | |
| `email` | string | Used as the upsert key if present |
| `phone` | string | |
| `mobilePhone` | string | |
| `vatNumber` | string | |
| `orgNumber` | string | |
| `currency` | string | |
| `warehouseId` | string | |
| `invoiceToCountryCode` | string | |
| `shipToCountryCode` | string | |
| `invoicingAddress` | object | See [Address](#address) below |
| `shipToAddress` | object | See [Address](#address) below |
| `shipToAddresses` | array of object | Multiple named delivery addresses, each shaped like [Address](#address) |
| `extendedInfo` | array | See [Extended Info](../extended-info/) |
| `checksum` | string | |
| `hasVatNumber` | boolean | |
| `hasCustomerNumber` | boolean | |
| `contacts` | array of object | See [Contact](#contact) below |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
[
  {
    "externalId": "20000",
    "customerNumber": "20000",
    "source": "example-shop",
    "firstName": "Anna",
    "lastName": "Karlsson",
    "customerType": "Person",
    "email": "anna.karlsson@example.com",
    "phone": "+46 31 555 0123",
    "currency": "SEK",
    "invoicingAddress": {
      "address1": "Storgatan 4",
      "city": "Göteborg",
      "zip": "411 03",
      "country": "SE"
    },
    "extendedInfo": []
  }
]
```

#### Response

```
201 Created
"1 customer(s) queued"
```
{{< /apicol >}}
{{< /apicols >}}

### Address

| Field | Type | Notes |
|---|---|---|
| `id` | string (GUID) | |
| `externalId` | string | |
| `defaultAddress` | boolean | |
| `code` | string | |
| `contact` | string | |
| `address1` | string | |
| `address2` | string | |
| `zip` | string | |
| `city` | string | |
| `county` | string | |
| `country` | string | |
| `phone` | string | |
| `extendedInfo` | array | See [Extended Info](../extended-info/) |
| `checksum` | string | |

### Contact

| Field | Type | Notes |
|---|---|---|
| `code` | string | |
| `firstName` | string | |
| `lastName` | string | |
| `email` | string | |
| `phone` | string | |
| `mobilePhone` | string | |
| `jobTitle` | string | |
| `extendedInfo` | array | See [Extended Info](../extended-info/) — Customer is one of the resources where Extended Info appears at more than one level: on the customer itself, and independently on each contact. |

## Retrieve customers from the queue

{{< apimethod method="GET" path="/customer" >}}

| Query parameter | Notes |
|---|---|
| `count` | Number of entries to retrieve. Default 100 if omitted. |
| `acknowledge` | The `acknowledgeToken` from your previous batch — pass it to close that batch and advance the queue. |

```json
{
  "count": 1,
  "acknowledgeToken": "5b2f7c1a-8d4e-4b9a-9f31-2c6a8e1d4b90",
  "nextLink": "/customer?acknowledge=5b2f7c1a-8d4e-4b9a-9f31-2c6a8e1d4b90",
  "data": [
    {
      "externalId": "20000",
      "customerNumber": "20000",
      "firstName": "Anna",
      "lastName": "Karlsson",
      "email": "anna.karlsson@example.com",
      "extendedInfo": []
    }
  ]
}
```
