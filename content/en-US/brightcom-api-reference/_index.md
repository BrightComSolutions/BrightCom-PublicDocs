---
title: "BrightCom API Reference"
linkTitle: "BrightCom API Reference"
menu: {main: {weight: 36}}
description: >
  REST API reference for the BrightCom Gateway — the queue-based integration hub between Business Central and connected e-commerce, PIM, and marketplace systems.
---

## Overview

The BrightCom Gateway is a queue-based store-and-forward integration hub, not a direct CRUD API. Business Central pushes messages **into** a resource's queue with `POST`; your system pulls the next batch **out** with `GET`, using FIFO ordering and an acknowledge-token handshake.

**Base URLs**

```
QA:         https://qa.onbrightcom.com/gateway/v1
Production: https://onbrightcom.com/gateway/v1
```

**How the queue works**

1. `GET` a batch (default 100 entries unless you pass `count`). The response is wrapped in an envelope: `{ "count": ..., "acknowledgeToken": "...", "nextLink": "...", "data": [...] }`. `nextLink` is only present when more entries remain beyond this batch — treat it as your pagination signal, not a field to expect on every response.
2. Process the batch.
3. Pass `acknowledgeToken` back as the `acknowledge` query parameter on your next `GET`. This closes out the batch you just processed and advances the queue — if you don't acknowledge, the same entries stay open and you'll receive them again.

Queues are configured per target: which source's updates go to which queue is set up in the Gateway configuration, and multiple sources may share a common queue.

{{% alert title="Consumers must be idempotent" color="warning" %}}
When an already-delivered entry needs correcting, the Gateway doesn't edit it in place — it appends a new copy to the end of the queue instead, to avoid disturbing the acknowledge watermark. That means the same logical record can arrive more than once. Match incoming entries on your own key (e.g. `externalId`) and treat a repeat as an update, not a new record — don't assume delivery is exactly-once.
{{% /alert %}}

This reference covers six resources:

{{< cardpane >}}
{{< card header="**Item**" title="Products & variants" url="/brightcom-api-reference/item/" >}}
Item, variant, and parent-grouping messages — non-variant items, BC-level variants, and virtual parent groupings.
{{< /card >}}

{{< card header="**Customer**" title="Customers & contacts" url="/brightcom-api-reference/customer/" >}}
Customer master data, addresses, and contacts.
{{< /card >}}

{{< card header="**Price**" title="Price entries" url="/brightcom-api-reference/price/" >}}
Price list entries per item/variant, with currency, VAT, and validity dates.
{{< /card >}}

{{< card header="**Warehouse**" title="Stock & inventory" url="/brightcom-api-reference/warehouse/" >}}
Stock levels and movements per warehouse — absolute quantities, deltas, and planning/history data.
{{< /card >}}

{{< card header="**Order**" title="Orders, invoices & credit memos" url="/brightcom-api-reference/order/" >}}
Sales orders, closed invoices, and credit memos, with lines, buyer/payer/ship-to, payments, and delivery.
{{< /card >}}

{{< card header="**Shipment**" title="Shipment notifications" url="/brightcom-api-reference/shipment/" >}}
Full or partial shipment notifications, with tracking and line-level handled/closed quantities.
{{< /card >}}

{{< card header="**Extended Info**" title="Flexible attributes" url="/brightcom-api-reference/extended-info/" >}}
The typed, config-driven mechanism used to extend every message beyond its base fields.
{{< /card >}}
{{< /cardpane >}}

## What's not covered yet

- **Authentication** — request gating happens in tenant-resolution middleware backed by an external package outside this reference's source access. Don't guess at a header name; ask BrightCom Solutions for the current mechanism before building against it.
- **Item cross-references, structure (BOM), suppliers, and units of measure** — these exist on the Item message but are only listed by name here, not expanded field-by-field yet.
- **Operational endpoints** (dead-letter queue, configuration, mapping, admin/stats/tooling) — internal to BrightCom Solutions, not part of the integrator-facing surface documented here.
- **Interactive try-it-out reference** — this version is documentation to read, not a live console.

{{% alert title="Two other integration paths exist and are out of scope here" color="info" %}}
Business Central also exposes its own direct REST/OData API pages (`/api/brightcom/brccore/...`, `/api/brightcom/brcconnect/...`) for automation directly against BC. Those are a different integration path from the Gateway documented here and aren't covered on this page.
{{% /alert %}}

## Other product API references

These aren't the Gateway — they're the separate integration/extension references for other BrightCom Business Central apps, kept here for a single API-docs entry point.

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
