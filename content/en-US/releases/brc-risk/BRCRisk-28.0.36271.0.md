---
title: BRCRisk 28.0.36271.0
categories: [BRCRisk, ReleaseNotes]
description: Adds a once-a-day usage signal to BrightCom's Application Insights and removes credentials from the API log, error messages and telemetry.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36077.0 on 2026-10-06.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | The app sends a once-a-day usage signal to BrightCom's Application Insights, so BrightCom can see which features are used and spot problems early. It contains no personal data and no document contents. | 31566 |
| Security hardening | Passwords, keys and tokens are removed from the API log, error messages and telemetry. Credential-handling procedures can no longer be inspected in the debugger. | 31545 |

## Detailed Feature Information

---

### Daily usage telemetry (#31566)

Once a day, for each company, BRC Risk Management sends a small usage signal to BrightCom's Application Insights. BrightCom uses it to see which features are in use and to spot problems early.

The signal contains configuration and activity counts. It contains no personal data and no document contents. Nothing is scheduled by the app. It runs with Business Central's own daily telemetry hook, and it only reads data.

Three events are sent:

- **BRCRSK-0201, configuration.** Which features are set up: number of providers configured and enabled, the primary provider, whether the webhook is enabled, whether setup is completed, the logging level, the number of risk levels (and how many of them block), enabled risk thresholds, and the number of watch lists (and how many are enabled).
- **BRCRSK-0202, volume.** What the app did the previous day: API calls (and month to date), webhooks received and failed, and entities refreshed.
- **BRCRSK-0203, portfolio.** The size and health of the monitored portfolio: number of business entities, how many update automatically, how many are overdue for an update, how many have never been fetched, and the number of linked customers and vendors.

Provider URLs and API keys are never read for this signal.

The permission sets BRC RISK - ADMIN and BRC RISK - EDIT now include the new telemetry codeunit.

#### Related PR

- PR 15919 (BRCRisk): #31566 Meaningful daily usage telemetry

---

### Security hardening (#31545)

Part of a security review across all BrightCom apps. For BRC Risk Management:

- **Credentials are removed from the API log.** Passwords, keys, tokens and similar values are masked in logged request addresses, request and response bodies, and error messages.
- **Error messages show less.** Network error messages no longer include part of the response body.
- **Telemetry carries no query strings.** Endpoint addresses and error texts sent to telemetry no longer include query strings.
- **Credential-handling procedures can no longer be inspected in the debugger.**

Entries written to the API log before this version are not changed.

#### Related PR

- PR 15996 (BRCRisk): #31545 Sensitive-data hardening

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- No separate bug fixes in this release.
