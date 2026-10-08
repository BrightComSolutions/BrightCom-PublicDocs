---
title: BRCMaddenAnalyticsConnect 28.0.36266.0
categories: [BRCMaddenAnalyticsConnect, ReleaseNotes]
description: A once-a-day usage signal so BrightCom can see which features are used, plus security hardening that masks credentials and keeps them out of logs and messages.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36088.0 on 2026-10-07.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | The app sends a once-a-day usage signal to BrightCom's Application Insights, with configuration and activity counts. It contains no personal data and no document contents. | 31560 |
| Security hardening | Credential fields on the setup page are masked. Passwords, keys and tokens are removed from messages, error texts and logs. | 31545 |

## Detailed Feature Information

---

### Daily usage telemetry (#31560)

Madden Analytics Connect now sends a usage signal once a day, per company, to BrightCom's Application Insights. It shows BrightCom which features are set up and used, and helps us spot problems early.

The signal holds configuration and activity counts only. For example: which features are switched on, how many templates and endpoints exist, and how many records were queued for sync the day before. It contains no personal data and no document contents. No names, codes, IDs, URLs or free text are sent.

The signal is sent as three events:

- **BRCMAD-0101** - the shape of the setup: which switches are on and how many extra purchase and transfer fields are in use.
- **BRCMAD-0102** - the size of the template layer: how many templates, endpoints and mappings there are.
- **BRCMAD-0103** - activity and health: records queued the previous day, how many are still unsynced, and how many SKU locations exist.

You do not need to set anything up. The signal is sent by the standard Business Central daily telemetry run, so nothing is scheduled in your environment.

#### Related PR

- PR 15913 (BRCMaddenAnalyticsConnect): #31560 Add daily usage telemetry

---

### Security hardening (#31545)

Credentials are now better protected in Madden Analytics Connect.

- **Masked credential fields.** **API Key**, **Bearer Token** and **Access Token** on the Madden Setup page are now masked. They no longer show as plain text.
- **Credentials removed from messages and logs.** Passwords, keys and tokens are removed from the messages and errors shown on the setup, endpoint and template pages. They are also removed from the error text saved on web entries.
- **No inspection in the debugger.** Procedures that handle credentials can no longer be inspected in the debugger.

Entries written before this version are not changed.

#### Related PR

- PR 15991 (BRCMaddenAnalyticsConnect): #31545 Sensitive-data hardening: mask credentials, redact logs, remove client data

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No separate bugfixes in this release.
