---
title: BRCnShiftConnect 28.0.36298.0
categories: [BRCnShiftConnect, ReleaseNotes]
description: Customs information and Trade Type for return shipments, a once-a-day usage signal, and security hardening of credential handling.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36089.0 on 2026-10-07.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Customs information and Trade Type on return shipments | A new setting on the combination setup adds customs information to return shipments. A new Trade Type (B2B or B2C) is sent to nShift. | 31513 |
| Daily usage telemetry | The app sends a once-a-day usage signal to BrightCom with configuration and activity counts. It contains no personal data and no document contents. | 31561 |
| Security hardening | Credential fields are masked, secrets are removed from logs, messages and telemetry, and credential-handling procedures can no longer be inspected in the debugger. | 31545 |

## Detailed Feature Information

---

### Customs information and Trade Type on return shipments (#31513)

Some carriers, UPS for example, use the same service for outbound and return shipments. A return shipment can therefore need customs information too. Before, customs information was only sent for outbound shipments.

Customer-driven. What changed:

- **Add Customs Info on Return Shipment.** A new setting on each combination setup line. When it is on, a return shipment gets the same customs information as an outbound one: customs invoice type and print set, customs declaration, sender local VAT number and import/export type.
- **Trade Type.** A new field on the combination setup with the values B2B and B2C. It is copied to the consignment and sent to nShift as `tradeType` together with the customs information. Leave it empty to send nothing.
- **Consignment page.** Trade Type, Customs ImportExportType and the new return setting are shown on the consignment (Send-to) page.

Existing setups behave as before. The new setting is off by default, so return shipments carry no customs information until you turn it on.

#### Related PR

- PR 15887 (BRCnShiftConnect): Added customs info to return

---

### Daily usage telemetry (#31561)

The app now sends a small usage signal once a day, per company, to BrightCom's Application Insights. It shows which features are set up and how many documents are processed, so BrightCom can see which features are used and spot problems early.

The signal contains counts, yes/no settings and fixed option names only. It contains no personal data and no document contents: no names, numbers, addresses, URLs or credentials.

Three events are sent:

- **BRCNSH-0101, configuration.** Whether the integration is active, how many carrier partners, combination rules, senders, service codes, add-on templates, dangerous goods items, pickup mappings and PrintNode printers are set up, and which API flow is used.
- **BRCNSH-0102, workflow options.** Which workflow options are switched on (batch processing, dropshipment, invoice posting, JSON response parsing and similar), and how many rules use add-ons, return services, customs declaration or automatic consignment creation.
- **BRCNSH-0103, documents by source type.** How many consignment documents exist in total and per source document type, such as sales order, transfer order or return order.

The signal is sent to BrightCom only. It is not sent to the environment's own telemetry. The permission set was extended to cover the new codeunit.

#### Related PR

- PR 15914 (BRCnShiftConnect): #31561 nShift Connect: meaningful daily usage telemetry

---

### Security hardening (#31545)

This release strengthens how the app handles credentials.

- **Masked credential fields.** Credential fields on the setup page, the partner page and the printer selection page are now masked.
- **Secrets removed from logs and messages.** Passwords, keys and tokens are removed from stored request files, from error and debug messages shown to users, and from telemetry.
- **Not visible in the debugger.** The procedures that handle credentials can no longer be inspected in the debugger.

Entries written before this version are not changed.

#### Related PR

- PR 15992 (BRCnShiftConnect): #31545 Sensitive-data hardening: mask credentials, redact logs, remove client data

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No separate bugfixes in this release.
