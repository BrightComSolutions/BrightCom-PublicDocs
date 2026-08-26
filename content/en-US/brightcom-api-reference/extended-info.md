---
title: "Extended Info"
linkTitle: "Extended Info"
weight: 60
description: >
  The typed, config-driven mechanism used to extend every Gateway message beyond its base fields, confirmed by BrightCom's own integration docs.
---

From the Gateway's own documentation: *"All messages can be extended beyond their base models, using our Extended Info format."* It's a first-party, cross-cutting mechanism — not specific to one resource — used to carry source-specific attributes (HS codes, season identifiers, supplier information, and similar) that don't have a dedicated field on the base message.

It's flexible in two ways: the **set of codes is configurable**, not fixed, and it can appear at **more than one level** on a message — e.g. independently on an item and on each of its variants, or on an order and on each of its lines.

## Shape

Each entry is a typed key/value object:

```json
{
  "id": "4e9c9374-83b0-4d7b-bd13-7ee076c9361f",
  "externalId": "",
  "code": "HSCode",
  "valueType": "string",
  "stringValue": "6214900019",
  "decimalValue": null,
  "boolValue": null,
  "json": null,
  "value": "6214900019",
  "checksum": ""
}
```

## Field reference

| Field | Type | Description |
|---|---|---|
| `id` | string (GUID) | Identifier for this attribute instance. |
| `externalId` | string | Your system's identifier for this entry, if you set one. |
| `code` | string | The attribute identifier — configurable per integration setup, e.g. `HSCode`, `SeasonId`, `ItemGroup`, `CompanyName`. Case-sensitive, may contain spaces (`"Duty AB"`, `"Family name"`). |
| `valueType` | string | `string`, `boolean`, or `decimal` in practice today (see note below). Determines which typed field is populated. |
| `stringValue` | string | Populated when `valueType` is `string`. |
| `decimalValue` | number | Populated when `valueType` is `decimal`. |
| `boolValue` | boolean | Populated when `valueType` is `boolean`. |
| `json` | object | Reserved for structured/complex values. Not currently populated by Business Central's outbound messages — the underlying data model supports it, but you shouldn't expect it in practice today. |
| `value` | string | Always populated — a string representation of the value, for display/logging. Don't parse it for typed processing; formatting isn't guaranteed. |
| `checksum` | string | Present on the model but not something to build logic around — confirm current behavior with BrightCom Solutions before relying on it for change detection. |

{{% alert title="Three types in practice, four reserved" color="info" %}}
Business Central's message-building code only ever produces `string`, `boolean`, or `decimal` — confirmed via a three-branch type switch in the BC integration code, with a text/string fallback for anything else (dates, codes, option fields all come through as `string`). The Gateway's data model additionally reserves a `json` field for structured values, for future or non-BC sources — don't build integration logic assuming you'll never see it, but don't expect it from BC today either.
{{% /alert %}}

**How to read values:** branch on `valueType` and read the matching typed field — `decimal` → `decimalValue`, `boolean` → `boolValue`, `string` → `stringValue`. Use `value` only as a display fallback, never for typed logic.

## Where it appears

Every message DTO documented in this reference carries an `extendedInfo` array — see each resource's own page for the specific level(s) it appears at (e.g. [Item](../item/) has it on the item and independently on the source data behind each variant; [Order](../order/) has it on the order and on each line).

## Important characteristics

- **The set of codes isn't fixed.** Different sources can send different codes — don't assume a specific code is always present.
- **This is separate from Product Ranges.** Item, Price, and Warehouse messages also carry a `productRanges` array (channel/assortment flags — see each resource's page) — a different, narrower mechanism for tagging which sales channels a record applies to. Don't conflate the two: Extended Info is a generic attribute bag, Product Ranges is specifically about channel membership.
- **Mapping to Business Central** is configured per integration, not part of the public REST contract — there's no API to read or change that mapping from outside BC today.
