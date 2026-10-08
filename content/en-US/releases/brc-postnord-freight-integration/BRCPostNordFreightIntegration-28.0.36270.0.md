---
title: BRCPostNordFreightIntegration 28.0.36270.0
categories: [BRCPostNordFreightIntegration, ReleaseNotes]
description: A daily usage signal helps BrightCom spot problems early, and the API key and PrintNode key are now masked and kept out of the debugger and messages.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36071.0 on 2026-10-06.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | The app sends a once-a-day usage signal to BrightCom's Application Insights with configuration and activity counts. It contains no personal data and no document contents. | 31563 |
| Security hardening | Credential fields on the setup pages are masked, and credentials are kept out of the debugger and out of messages. | 31545 |

## Detailed Feature Information

---

### Daily usage telemetry (#31563)

The app now sends a once-a-day usage signal to BrightCom's Application Insights. It holds configuration and activity counts, such as which features are set up and how many documents were processed. BrightCom uses it to see which features are used and to spot problems early.

The signal contains no personal data and no document contents. It is sent once per company, with the platform's own daily telemetry. Nothing is scheduled and nothing needs to be set up.

Three events are sent:

- **BRCPN-0101, configuration.** Whether the setup exists and is active, whether the environment is Test or Production, and which options are switched on (label printing, shipment and invoice posting, dropshipment, batch processing, several services per document). It also counts partners and combination rules.
- **BRCPN-0102, volume.** The number of PostNord documents, in total and per source document type (sales orders, transfer orders, purchase orders, inventory picks, sales shipments), and the number of parcels.
- **BRCPN-0103, health.** The number of PostNord job queue entries, and how many are Ready, On Hold or in Error.

If a company has no setup, or the app cannot read a table, the event is skipped without any error for the user. The app's permission set was extended so the daily event can run.

#### Related PR

- PR 15916 (BRCPostNordFreightIntegration): #31563 Daily usage telemetry

---

### Security hardening (#31545)

This release is part of a security review of all BrightCom apps.

- **Masked credential fields.** The API key (**Secret ID**) on the PostNord Setup page and the **PrintNode Auth. Key** on the Printer Selections page are now masked. They are no longer readable over your shoulder or during a screen share.
- **Credentials kept out of the debugger.** The procedures that handle the API key and the PrintNode key can no longer be inspected in the debugger.
- **Cleaner PrintNode message.** After a print job, the status message from PrintNode now shows only the status code and reason, not the full response.

Values you have already entered keep working. You do not need to enter them again. Entries written before this version are not changed.

#### Related PR

- PR 15994 (BRCPostNordFreightIntegration): #31545 Sensitive-data hardening

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- No bug fixes in this release.
