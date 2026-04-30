---
title: BRC Extended Order Management 25.0.31277.0
categories: [BRCExtendedOrderManagement, ReleaseNotes]
description: E-commerce order quarantine period and return order receive functionality.
date: 2026-04-30
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| E-Commerce Order Release Delay (Quarantine) | Adds a configurable quarantine period for e-commerce orders, holding them in Open status before releasing to the warehouse for picking, with a new report for managing and releasing delayed orders. | 19961 |
| Return Order Receive Functionality | Extends the Extended Order Management auto-posting setup to support receiving and posting return orders, enabling automated return order processing within the existing posting job framework. | 27102 |

## Detailed Feature Information

---

### E-Commerce Order Release Delay (Quarantine) (#19961)

Adds a configurable quarantine period for e-commerce orders, holding them in Open status before releasing to the warehouse for picking, with a new report for managing and releasing delayed orders. This allows cancellation requests to be processed before an order is committed to the warehouse, reducing unnecessary pick-and-cancel cycles. The quarantine duration is configurable, with optional exclusion of transport service lines and support for scheduled release windows.

---

### Return Order Receive Functionality (#27102)

Extends the Extended Order Management auto-posting setup to support receiving and posting return orders, enabling automated return order processing within the existing posting job framework. A new setup option and supporting codeunit allow return orders to be received automatically, with the posting date set to today, without triggering a full financial posting at receipt time.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No bugfixes in this release.
