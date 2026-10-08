---
title: BRCPSInkassoConnect 28.0.36273.0
categories: [BRCPSInkassoConnect, ReleaseNotes]
description: Daily usage telemetry and security hardening for credentials on the PS Inkasso Connect setup page.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36074.0 on 2026-10-06.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | Once a day the app sends BrightCom a usage signal with configuration and activity counts. It contains no personal data and no document contents. | 31564 |
| Security hardening | Credential fields on the setup page are masked, and the app handles credentials more carefully. | 31545 |

## Detailed Feature Information

---

### Daily usage telemetry (#31564)

PS Inkasso Connect now sends a once-a-day usage signal to BrightCom's Application Insights. It holds configuration and activity counts, for example which features are set up and how many documents were processed. BrightCom uses it to see which features are used and to spot problems early.

The signal contains no personal data and no document contents. It does not include URLs, keys, account numbers, customer data or the names of mapped fields. It is sent once per company per day, using Business Central's own daily telemetry schedule, so nothing is scheduled or added to the job queue.

The signal is sent with these event IDs:

- `BRCPSI-0101` - configuration: whether the integration is turned on, which list and customer-info features are active, whether an endpoint is set up (not the address itself), the security protocol setting, and the number of currency account setups.
- `BRCPSI-0102` - how many of the extra field mappings are in use, per entity and in total (counts only).

#### Related PR

- PR 15917 (BRCPSInkassoConnect): #31564 PS Inkasso Connect: meaningful daily usage telemetry

---

### Security hardening (#31545)

This release hardens how the app handles credentials.

- Credential fields on the PS Inkasso Connect setup page (API key, secret and token) are now masked.
- The code that sends credentials to the Pay Solution service can no longer be inspected in the debugger.

Entries written before this version are not changed.

#### Related PR

- PR 15995 (BRCPSInkassoConnect): #31545 Sensitive-data hardening: mask credentials, redact logs, remove client data

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No separate bugfixes in this release.
