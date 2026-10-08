---
title: BRCExtendedIC 28.0.36261.0
categories: [BRCExtendedIC, ReleaseNotes]
description: A once-a-day usage signal that helps BrightCom spot problems early, and security hardening that keeps credentials out of setup pages, logs, messages and telemetry.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36073.0 on 2026-10-06.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | Extended IC sends a once-a-day usage signal to BrightCom with configuration and activity counts. It contains no personal data and no document contents. | 31557 |
| Security hardening | Credential fields are masked, and passwords, keys and tokens are kept out of logs, error messages, debug messages and telemetry. | 31545 |

## Detailed Feature Information

---

### Daily usage telemetry (#31557)

Extended IC now sends a small usage signal once a day to BrightCom's Application Insights. It shows which features are set up and how many documents were processed. BrightCom uses it to see which features customers use and to spot problems early.

The signal contains counts and settings only. It contains no personal data and no document contents. It does not name partners, companies or endpoints. Nothing needs to be set up or scheduled. It is sent together with Business Central's own daily telemetry, once per company per day.

There are two events:

- **BRCEIC-0101, configuration.** How many IC partners exist and how many are enabled. How many partners send and how many receive. How many partners use each transport (API, Azure Blob, Database, File Location, E-mail, other). Which features are switched on: sales documents, master data, master data rename, automatic purchase sending, reverse order flow and WMS-initiated returns.
- **BRCEIC-0103, health.** How many entries wait in the JSON inbox and outbox and how old the oldest one is. The Activity Log verbosity setting. How many errors were written to the Activity Log yesterday.

#### Transport breakdown (#31599)

The configuration event counts partners for every transport, not only API and Azure Blob. The transport counts always add up to the number of enabled partners. The warnings count was removed from the health event because the app almost never writes warnings, so it carried no information.

Related PRs:

- PR 15910: Daily usage telemetry
- PR 15958: Daily usage telemetry v2

---

### Security hardening (#31545)

This release makes Extended IC safer to use and support.

- **Credential fields are masked.** The Access Key, Password and API key fields on the IC Partner card and the inbox API are now masked. Values are hidden on screen, for example during screen sharing. Stored values are unchanged and keep working. You do not need to enter them again.
- **Credentials are removed from logs and messages.** Passwords, keys and tokens no longer appear in error messages, in the Activity Log or in telemetry. This includes keys in web addresses and in request data.
- **Credential handling is protected from the debugger.** Procedures that handle credentials can no longer be inspected in the debugger.

Entries written before this version are not changed.

Related PR:

- PR 15984: Sensitive-data hardening

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No bug fixes in this release.
