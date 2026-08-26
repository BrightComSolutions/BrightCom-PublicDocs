---
title: "Extended Info"
linkTitle: "Extended Info"
weight: 60
description: >
  BRC Connect's mechanism for flexible, source-specific attributes that don't have a dedicated field — used across every message flow, supporting string, boolean, and decimal values.
---

{{% alert title="Different surface" color="warning" %}}
`extendedInfo` lives on BRC Connect's outbound and inbound integration **messages** — not on the direct BC REST API endpoints documented for [Item](item/), [Price](price/), [Warehouse](warehouse/), [Order](order/), and [Shipment](shipment/). Those pages link back here instead of repeating this explanation five times.
{{% /alert %}}

## What it is

`extendedInfo` carries source-specific attributes that don't have a dedicated field in the standard message shape — things like HS codes, season identifiers, or supplier information that vary by integration source. It's a single mechanism used the same way across every one of BRC Connect's message flows, and it's flexible in two independent ways:

- **It works at more than one level.** On some flows it's a single flat array per message; on others it appears independently at both a header and a line/variant level.
- **The set of codes is configurable, not fixed.** Which codes appear depends on how the sending integration is set up — different sources can send different codes, and it isn't a static list baked into this reference.

## Supported data types

Each entry is a typed key/value pair. `valueType` determines which of three typed fields is populated:

| `valueType` | Populated field | Example |
|---|---|---|
| `string` | `stringValue` | `SeasonName` = `"2026 Q3"` |
| `boolean` | `boolValue` | `IsPrimary` = `true` |
| `decimal` | `decimalValue` | `Duty AB` = `0.000` |

```json
{
  "code": "HSCode",
  "valueType": "string",
  "stringValue": "6214900019",
  "value": "6214900019",
  "checksum": "",
  "id": "4e9c9374-83b0-4d7b-bd13-7ee076c9361f"
}
```

## Field reference

| Field | Type | Description |
|---|---|---|
| `code` | string | The attribute identifier — configurable per integration setup, e.g. `HSCode`, `SeasonId`, `ItemGroup`, `CompanyName`. Case-sensitive, may contain spaces (`"Duty AB"`, `"Family name"`). |
| `valueType` | string | `string`, `boolean`, or `decimal`. Determines which typed field below is populated. |
| `stringValue` | string | Populated when `valueType` is `string`. |
| `boolValue` | boolean | Populated when `valueType` is `boolean`. |
| `decimalValue` | number | Populated when `valueType` is `decimal`. |
| `value` | string | Always populated — a string representation of the value, for display/logging. Don't parse it for typed processing; formatting isn't guaranteed. |
| `checksum` | string | **Confirmed unused** — always an empty string in the current implementation, not read or compared anywhere. Ignore it; it isn't a change-detection signal despite the name. |
| `id` | string (GUID) | Identifier for this attribute instance. |

**How to read values:** branch on `valueType` and read the matching typed field — `decimal` → `decimalValue`, `boolean` → `boolValue`, `string` → `stringValue`. Use `value` only as a display fallback, never for typed logic.

## Where it appears

| Flow | Level(s) | Notes |
|---|---|---|
| [Item](item/) | Item (style) **and** Item Variant, independently | Richest example — see below |
| [Customer](customer/) | Customer **and** each entry in its `contacts` array | Customer also carries a separate `shipToAddresses` array, unrelated to `extendedInfo` |
| [Price](price/) | Single, flat — one array per price row | Same shape whether the sending environment uses the legacy Sales Price table or the modern Price List Line |
| [Warehouse](warehouse/) | Single, flat — one array per stock message | This message is also where actual stock quantities travel; the REST Location endpoint never carries them |
| [Order](order/) | Header **and** each line | Also works inbound — your integration can send its own `extendedInfo` codes when creating an order |
| [Shipment](shipment/) | Header **and** each line | Outbound only, same shape as Order |

## Example: item-level and variant-level together

```json
{
  "partNo": "10023",
  "source": "example-pim",
  "name": "Outdoor Scarf",
  "brand": "EXAMPLE",
  "status": "Published",
  "extendedInfo": [
    { "code": "CompanyName", "valueType": "string", "stringValue": "Nordic Apparel AB", "value": "Nordic Apparel AB", "checksum": "", "id": "38edce62-d40f-4444-b5e0-a4214bd3ec75" },
    { "code": "SupplierName", "valueType": "string", "stringValue": "Example Textiles Ltd", "value": "Example Textiles Ltd", "checksum": "", "id": "b3089724-736a-4a43-9b15-9cb4678ed5a6" },
    { "code": "SeasonId", "valueType": "string", "stringValue": "2608", "value": "2608", "checksum": "", "id": "f55f8c70-26a3-4e72-abda-f5fc54241752" },
    { "code": "HSCode", "valueType": "string", "stringValue": "6214900019", "value": "6214900019", "checksum": "", "id": "4e9c9374-83b0-4d7b-bd13-7ee076c9361f" },
    { "code": "ReadyForExport", "valueType": "boolean", "boolValue": true, "value": "True", "checksum": "", "id": "5df1a579-7af1-46d6-96b3-f2f9449f4615" },
    { "code": "Duty AB", "valueType": "decimal", "decimalValue": 0, "value": "0.000", "checksum": "", "id": "a6a7d21d-fb78-41c3-8e70-0cdc15d1931c" }
  ],
  "variants": [
    {
      "variantCode": "050-ONE",
      "name": "Cream Outdoor Scarf ONE",
      "extendedInfo": [
        { "code": "SizeRangeName", "valueType": "string", "stringValue": "one", "value": "one", "checksum": "", "id": "b9af63f9-556b-4fca-9394-2c1a760d8652" }
      ]
    }
  ]
}
```

## Important characteristics

- **The set of codes isn't fixed.** Different sources can send different codes — don't assume a specific code is always present.
- **Unmatched codes are auto-registered, not rejected.** If an incoming message includes an `extendedInfo` code BRC Connect hasn't seen configured before, it gets registered automatically rather than causing an error. A typo in a code name won't surface as a failure — it'll silently create a new one.
- **Mapping to Business Central** is configured per integration, not part of the public REST contract — there's no API to read or change that mapping from outside BC today.
