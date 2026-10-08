---
title: BRCPLEO 28.0.36269.0
categories: [BRCPLEO, ReleaseNotes]
description: Adds a once-a-day usage signal to BrightCom and hardens how the PLEO connection token is handled.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36090.0 on 2026-10-07.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | BRC PLEO sends a once-a-day usage signal to BrightCom, so BrightCom can see which features are used and spot problems early. | 31562 |
| Security hardening | The PLEO access token can no longer be inspected in the debugger. | 31545 |

## Detailed Feature Information

---

### Daily usage telemetry (#31562)

BRC PLEO now sends a small usage signal once a day, per company, to BrightCom's Application Insights. It contains configuration and activity counts: which features are set up and how many expenses were processed. BrightCom uses it to see which features are in use and to spot problems early.

The signal contains no personal data and no document contents. It holds only counts, yes/no values and a number of days. Nothing a user typed, and no names, numbers, URLs or tokens, is included.

It is sent as three events:

- **BRCPLO-0101, Configuration.** Which parts of the app a company has switched on and set up, such as automatic posting, receipt download, journal batch and default accounts. It also holds how many account, department and payment mappings exist, and how many are approved.
- **BRCPLO-0102, Volume.** How many expenses, expense lines and attachments the app holds.
- **BRCPLO-0103, Health.** Whether the sync jobs are present, failing or on hold, how many mappings still wait for approval, and how many days have passed since the last import.

To read the job queue for the health signal, the **BRC PLEO** permission set now includes read access to Job Queue Entry. No action is needed if your users already get this permission set.

#### Related PR

- PR 15915 (BRCPLEO): #31562 Add daily usage telemetry

---

### Security hardening (#31545)

This release is part of a security hardening effort across BrightCom's apps.

- The code that adds the PLEO access token to requests can no longer be inspected in the debugger.

#### Related PR

- PR 15993 (BRCPLEO): #31545 Sensitive-data hardening

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No separate bugfixes in this release.
