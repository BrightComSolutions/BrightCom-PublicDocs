---
title: "Customer"
linkTitle: "Customer"
weight: 15
description: >
  Customer master data and ship-to addresses, plus BRC Connect's web number, price list, and credit limit fields.
---

## Customer

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/customers" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brccore/v1.0/companies({id})/customers({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `number` | `No.` | |
| `displayName` | `Name` | |
| `searchName` | `Search Name` | |
| `name2` | `Name 2` | |
| `addressLine1` | `Address` | |
| `addressLine2` | `Address 2` | |
| `city` | `City` | |
| `state` | `County` | JSON name is `state`, BC field is `County` |
| `postalCode` | `Post Code` | |
| `countryRegionCode` | `Country/Region Code` | |
| `contact` | `Contact` | |
| `phoneNumber` | `Phone No.` | |
| `mobilePhoneNumber` | `Mobile Phone No.` | |
| `email` | `E-Mail` | |
| `website` | `Home Page` | |
| `vatRegistrationNumber` | `VAT Registration No.` | |
| `registrationNumber` | `Registration Number` | |
| `currencyCode` | `Currency Code` | |
| `languageCode` | `Language Code` | |
| `customerPostingGroup` | `Customer Posting Group` | |
| `generalBusinessPostingGroup` | `Gen. Bus. Posting Group` | |
| `vatBusinessPostingGroup` | `VAT Bus. Posting Group` | |
| `paymentTermsCode` | `Payment Terms Code` | |
| `paymentMethodCode` | `Payment Method Code` | |
| `shipmentMethodCode` | `Shipment Method Code` | |
| `locationCode` | `Location Code` | |
| `salespersonCode` | `Salesperson Code` | |
| `creditLimitLCY` | `Credit Limit (LCY)` | |
| `balance` | `Balance` | **read-only** |
| `balanceLCY` | `Balance (LCY)` | **read-only** |
| `blocked` | `Blocked` | option |
| `taxLiable` | `Tax Liable` | boolean |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
{
  "email": "anna.karlsson@example.com",
  "creditLimitLCY": 50000.00
}
```

#### Response

```json
{
  "id": "5b2f7c1a-8d4e-4b9a-9f31-2c6a8e1d4b90",
  "number": "20000",
  "displayName": "Anna Karlsson",
  "searchName": "ANNA KARLSSON",
  "name2": "",
  "addressLine1": "Storgatan 4",
  "addressLine2": "",
  "city": "Göteborg",
  "state": "",
  "postalCode": "411 03",
  "countryRegionCode": "SE",
  "contact": "Anna Karlsson",
  "phoneNumber": "+46 31 555 0123",
  "mobilePhoneNumber": "",
  "email": "anna.karlsson@example.com",
  "website": "",
  "vatRegistrationNumber": "",
  "registrationNumber": "",
  "currencyCode": "SEK",
  "languageCode": "SWE",
  "customerPostingGroup": "RETAIL",
  "generalBusinessPostingGroup": "RETAIL",
  "vatBusinessPostingGroup": "SWEDEN",
  "paymentTermsCode": "14 DAGAR",
  "paymentMethodCode": "CARD",
  "shipmentMethodCode": "POSTNORD",
  "locationCode": "MAIN",
  "salespersonCode": "WEB",
  "creditLimitLCY": 50000.00,
  "balance": 0,
  "balanceLCY": 0,
  "blocked": " ",
  "taxLiable": true,
  "lastModifiedDateTime": "2026-08-20T09:00:00Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

### Customer ship-to addresses

Nested under `customers` as `customerShipToAddresses`, and also reachable as its own top-level endpoint (`customerShipToAddress` / `customerShipToAddresses`) — a customer's named delivery addresses, distinct from the customer's own `addressLine1`/`addressLine2` above.

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/customerShipToAddresses" >}}

| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `customerId` | — | derived at read time by looking up the parent customer; not stored |
| `customerNumber` | `Customer No.` | |
| `code` | `Code` | |
| `name` | `Name` | |
| `addressLine1` | `Address` | |
| `addressLine2` | `Address 2` | |
| `city` | `City` | |
| `state` | `County` | |
| `postalCode` | `Post Code` | |
| `countryRegionCode` | `Country/Region Code` | |
| `contact` | `Contact` | |
| `phoneNumber` | `Phone No.` | |
| `shipmentMethodCode` | `Shipment Method Code` | |
| `locationCode` | `Location Code` | |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |

## BRC Connect extension fields

Separate endpoint, joined to `customers` above by `id`. All fields here are writable.

{{< apimethod method="GET" path="/api/brightcom/brcconnect/v1.0/companies({id})/customers" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brcconnect/v1.0/companies({id})/customers({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only, same value as the Core customer's `id` |
| `brcConWebNumber` | `BRC Web No.` | |
| `brcConPriceListCode` | `BRC Price List Code` | |
| `brcConCreditLimitLCY` | `BRC Credit Limit (Local Currency)` | a **separate** field from Core's `creditLimitLCY` |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Response

```json
{
  "id": "5b2f7c1a-8d4e-4b9a-9f31-2c6a8e1d4b90",
  "brcConWebNumber": "WEB-20000",
  "brcConPriceListCode": "SUMMER26",
  "brcConCreditLimitLCY": 50000.00,
  "lastModifiedDateTime": "2026-08-20T09:00:00Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

{{% alert title="Two similarly-named fields" color="warning" %}}
`creditLimitLCY` (Core) and `brcConCreditLimitLCY` (Connect) are two different underlying BC fields on the same customer — don't assume they're kept in sync automatically.
{{% /alert %}}

## Extended Info

The outbound customer message also carries `extendedInfo` — independently on the customer itself **and** on each entry in its `contacts` array. It also carries a separate `shipToAddresses` array (address details inline in the message, not the same thing as the `customerShipToAddresses` REST sub-resource above). See the dedicated [Extended Info](extended-info/) page for the full explanation, field reference, and supported data types.

## Permissions

Customer access is granted through `BRC API Cust READ` / `WRITE` — a dedicated permission set, unlike Warehouse which shares the broader Reference one.
