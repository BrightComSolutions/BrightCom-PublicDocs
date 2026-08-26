---
title: "BrightCom API Reference"
linkTitle: "BrightCom API Reference"
menu: {main: {weight: 36}}
description: >
  REST API reference for BRC Connect — Item, Price, Warehouse, Order, and Shipment endpoints, built on the standard Business Central API stack.
---

## Overview

BRC Connect's REST API surface is built on two Business Central apps working together:

- **BRC Core** exposes the standard, "normal" fields for each resource — item number, description, price, quantity, and so on — via its own API pages.
- **BRC Connect** exposes only its own additional fields (all prefixed `brcCon*` — brand, web flags, shipping extras, and similar) on a **separate** set of endpoints under the same resource name, joined to BRC Core's records by `id`. There is no server-side merge of the two.

In practice, an integration reading "the Item API" queries **two** endpoints and joins the results on `id`:

```http
GET /api/brightcom/brccore/v1.0/companies({id})/items
GET /api/brightcom/brcconnect/v1.0/companies({id})/items
```

This reference covers five resources — the normal Business Central fields plus the BRC Connect extension fields for each:

{{< cardpane >}}
{{< card header="**Item**" title="Products & variants" url="/brightcom-api-reference/item/" >}}
Item master data, variants, units of measure, and cross-references (EAN/GTIN), plus BRC Connect's brand and web-enablement fields.
{{< /card >}}

{{< card header="**Price**" title="Price lists" url="/brightcom-api-reference/price/" >}}
Price list headers and lines, plus BRC Connect's campaign and web-enablement fields.
{{< /card >}}

{{< card header="**Warehouse**" title="Locations" url="/brightcom-api-reference/warehouse/" >}}
Location master data, plus BRC Connect's location-filter and web-enablement fields.
{{< /card >}}

{{< card header="**Order**" title="Sales orders" url="/brightcom-api-reference/order/" >}}
Sales order headers and lines, plus BRC Connect's shipping, cancellation, and status fields.
{{< /card >}}

{{< card header="**Shipment**" title="Posted shipments" url="/brightcom-api-reference/shipment/" >}}
Posted sales shipment headers and lines, plus BRC Connect's read-only shipping extension fields.
{{< /card >}}

{{< card header="**Extended Info**" title="Flexible attributes" url="/brightcom-api-reference/extended-info/" >}}
The typed, config-driven mechanism used across every message flow to carry source-specific attributes that don't have a dedicated field.
{{< /card >}}
{{< /cardpane >}}

## Other product API references

These aren't BRC Connect — they're the separate integration/extension references for other BrightCom Business Central apps, kept here for a single API-docs entry point.

{{< cardpane >}}
{{< card header="**BRC Core**" title="API Reference" url="/brc-core/reference/api-reference/" >}}
Integration points, events, and extension capabilities for BRC Core.
{{< /card >}}

{{< card header="**BRC Retail**" title="API Reference" url="/brc-retail/reference/api-reference/" >}}
Inventory, catalog, pricing, and sales integration endpoints for BRC Retail Extension.
{{< /card >}}

{{< card header="**BRC Risk**" title="API Reference" url="/brc-risk/reference/api-reference/" >}}
External provider and internal Business Central APIs for risk data.
{{< /card >}}
{{< /cardpane >}}

## What's not covered yet

- **Generic item attributes** (`itemAttribute`, `itemAttributeValue`, `itemAttributeValueMapping`) — a typed key/value attribute-bag pattern used for less common item data. Deliberately left out of this first version.
- **Authentication and message-delivery details** — how duplicate or retried messages are handled, and which auth methods are supported for which consumers. Left out of this page until confirmed internally, rather than publish a guess integrators would end up relying on.
- **Interactive try-it-out reference** — this version is documentation to read, not a live console. An interactive version generated from an OpenAPI spec is planned for a later iteration.

## Permissions

Access is granted through Business Central permission sets, grouped by functional area rather than one-to-one with these five resources:

| Permission set | Covers |
|---|---|
| `BRC API Item READ` / `WRITE` | Item, Item Variant, Item UoM, Item Reference |
| `BRC API Price READ` / `WRITE` | Price List Header, Price List Line |
| `BRC API Ref READ` / `WRITE` | Location (Warehouse), plus unrelated reference data (currencies, payment terms, posting groups, etc.) |
| `BRC API Sales READ` / `WRITE` | Sales Order, Sales Order Line |
| `BRC API PSale READ` / `WRITE` | Posted Sales Shipment, Posted Sales Shipment Line |

{{% alert title="No dedicated Warehouse permission set" color="info" %}}
Location access comes bundled with the broader Reference permission set — there isn't a Warehouse-specific one to grant on its own.
{{% /alert %}}
