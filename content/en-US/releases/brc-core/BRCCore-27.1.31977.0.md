---
title: BRC Core 27.1.31977.0
categories: [BRCCore, ReleaseNotes]
description: Customs invoice integration now includes shipment numbers from every pallet line.
date: 2026-05-22
---

## Release Summary

| Feature | Description | ID |
| ------- | ----------- | ---: |
| Add all Shipment Numbers from pallet lines | Outbound customs-invoice integration now collects the Shipment No. from every pallet line and sends them as separate entries in the shipment array, preventing incomplete or incorrect downstream processing. | 27490 |

## Detailed Feature Information

---

### Add all Shipment Numbers from pallet lines (#27490)

Ensures accurate and complete integration data by including all pallet-specific Shipment Numbers in the outbound message, preventing downstream processing errors.

Previously, only a single Shipment No. (or not all of them) from the pallet lines on a customs invoice was included in the integration payload. Each pallet line can carry its own manually entered Shipment No., and the external system depends on receiving the full list — so omitting values resulted in incomplete or incorrect processing in the receiving system.

**Functionality.** A customs invoice can contain multiple pallet lines, and each pallet line has its own manually entered Shipment No. When the integration message is triggered, the system now:

- Loops through all pallet lines related to the customs invoice
- Collects the Shipment No. from each pallet line
- Includes every Shipment No. as a separate entry in the existing Shipment No. array in the outbound payload

The integration message structure already supports an array of Shipment Numbers — this change ensures all pallet lines are represented in that array, not just the first or a single value.

**Validation.** The customs invoice has a "Number of Pallets" field. Before sending the integration message, the system validates that the number of pallet lines with a populated Shipment No. matches the value in "Number of Pallets". If the counts do not match, the integration is blocked with a clear error message.

**Scope.**

- Applies to the outbound integration triggered from the customs invoice
- Supports multiple Shipment Numbers per customs invoice (one per pallet)
- Does not change how Shipment Numbers are entered (still manually entered per pallet line)
- Does not require changes to the external message schema (the array structure already exists)

This change is a customer-driven enhancement to ensure complete and reliable shipment data transmission.

#### Add all shipments (#27495)

Add the shipments to the message.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No bugfixes in this release.
