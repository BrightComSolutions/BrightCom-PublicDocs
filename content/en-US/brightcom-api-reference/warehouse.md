---
title: "Warehouse"
linkTitle: "Warehouse"
weight: 30
description: >
  Location master data, plus BRC Connect's location-filter and web-enablement fields.
---

{{% alert title="Location master data, not stock levels" color="warning" %}}
The REST endpoint below is Business Central **Location** master data — code, name, address. It cannot answer "how much of item X is available at location Y." Stock quantities travel separately, in BRC Connect's outbound warehouse stock message — see [Extended Info](#extended-info) below. There is no REST GET endpoint for stock levels; if you need to query them on demand rather than receive them as messages, ask BrightCom Solutions first.
{{% /alert %}}

## Location

{{< apimethod method="GET" path="/api/brightcom/brccore/v1.0/companies({id})/locations" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brccore/v1.0/companies({id})/locations({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only |
| `code` | `Code` | |
| `displayName` | `Name` | |
| `addressLine1` | `Address` | |
| `addressLine2` | `Address 2` | |
| `city` | `City` | |
| `state` | `County` | JSON name is `state`, BC field is `County` |
| `postalCode` | `Post Code` | |
| `countryRegionCode` | `Country/Region Code` | |
| `phoneNumber` | `Phone No.` | |
| `contact` | `Contact` | |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Request

```json
{
  "displayName": "Main Warehouse Stockholm",
  "phoneNumber": "+46 8 555 0110"
}
```

#### Response

```json
{
  "id": "6c2e9a4d-1a3b-4f60-9e0c-2d7a5f8b3c11",
  "code": "MAIN",
  "displayName": "Main Warehouse Stockholm",
  "addressLine1": "Lagervägen 12",
  "addressLine2": "",
  "city": "Stockholm",
  "state": "",
  "postalCode": "121 34",
  "countryRegionCode": "SE",
  "phoneNumber": "+46 8 555 0110",
  "contact": "Warehouse Office",
  "lastModifiedDateTime": "2026-07-02T11:05:44Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

## BRC Connect extension fields

Separate endpoint, joined to `locations` above by `id`. All fields here are writable.

{{< apimethod method="GET" path="/api/brightcom/brcconnect/v1.0/companies({id})/locations" >}}
{{< apimethod method="PATCH" path="/api/brightcom/brcconnect/v1.0/companies({id})/locations({id})" >}}

{{< apicols >}}
{{< apicol side="left" >}}
| Field | BC field | Notes |
|---|---|---|
| `id` | `SystemId` | read-only, same value as the Core location's `id` |
| `brcConEnabledWeb` | `BRC Enabled Web` | boolean |
| `brcConLocationFilter` | `BRC Location Filter` | |
| `lastModifiedDateTime` | `SystemModifiedAt` | read-only |
{{< /apicol >}}
{{< apicol side="right" >}}
#### Response

```json
{
  "id": "6c2e9a4d-1a3b-4f60-9e0c-2d7a5f8b3c11",
  "brcConEnabledWeb": true,
  "brcConLocationFilter": "MAIN|WEB",
  "lastModifiedDateTime": "2026-07-02T11:05:44Z"
}
```
{{< /apicol >}}
{{< /apicols >}}

## Extended Info

The outbound warehouse stock message also carries `extendedInfo`, at a single flat level (one array per stock message) — this message is also where actual stock quantities travel, since the REST endpoint above never carries them. See the dedicated [Extended Info](extended-info/) page for the full explanation, field reference, and supported data types.

## Permissions

Location access is granted through the **Reference** permission sets (`BRC API Ref READ` / `WRITE`), bundled together with unrelated reference data such as currencies, payment terms, and posting groups — there is no Warehouse-specific permission set.
