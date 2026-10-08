---
title: BRCCore 28.0.36257.0
categories: [BRCCore, ReleaseNotes]
description: A once-a-day usage signal that shows BrightCom which BRC Core features are in use, plus security hardening that masks credentials and keeps them out of logs, messages and telemetry.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36066.0 on 2026-10-06.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | BRC Core sends a once-a-day usage signal with configuration and activity counts, so BrightCom can see which features are used and spot problems early. No personal data and no document contents. | 31555 |
| Security hardening | Credential fields are masked on setup pages. Passwords, keys and tokens are removed from logs, error messages, debug messages and telemetry. Procedures that handle credentials can no longer be inspected in the debugger. | 31545 |

## Detailed Feature Information

---

### Daily usage telemetry (#31555)

Once a day, BRC Core sends a short usage signal to BrightCom's Application Insights. It tells BrightCom which BRC Core features are set up and how much they are used. BrightCom uses this to see which features matter to customers, to spot problems early, and to decide what to improve or retire.

The signal contains only counts, Yes/No values and the names of BRC Core's own setup options. It contains no personal data, no names, no URLs, no keys and no document contents.

Three events are sent. Their IDs are:

- **BRCCOR-0101**, enabled features: which BRC Core functions are switched on, such as currency exchange rates, PrintNode, customs documents, GDPR, IC variants and the background monitor. It also counts how features are enabled (for all users, or with user or company conditions). It is sent once per database per day, not once per company.
- **BRCCOR-0102**, configuration: how far each feature is set up, such as the number of price books, enabled rate services, background monitor receivers, customs customers and enabled PrintNode reports.
- **BRCCOR-0103**, activity and health: for example how many price books were generated yesterday, whether the background monitor ran yesterday, and counts of customs invoices, new customs shipments and anonymised customers.

Nothing changes in how BRC Core behaves. The signal needs no setup.

#### BRC Core: daily usage telemetry v2 (#31597)

Refines the signal after the first day of data:

- Currency rate setup is reported as configured only when an enabled rate service of BRC Core is actually set up. Opening the setup page once no longer counts.
- Feature conditions are counted by what is attached to features, not by the standard "all users" condition that is always present. Enablement for all users is reported separately.
- The features signal (BRCCOR-0101) is sent once per database per day.
- "Background monitor ran" now looks at yesterday only.
- The Price Books switch is no longer reported, because it does not control anything. Price book use is reported through the counts in BRCCOR-0102.

#### Related PR

- PR 15908 (BRCCore): #31555 Daily usage telemetry for BRC Core features
- PR 15962 (BRCCore): #31597 Daily usage telemetry v2

---

### Security hardening (#31545)

BRC Core now handles credentials more carefully, as part of a review of all BrightCom apps.

- **Masked fields.** Credential fields on setup and log pages are now masked, including the PrintNode authentication key and the carrier credentials used by customs documents.
- **Redaction.** Passwords, keys, tokens and secrets are removed from the HTTP call log, error messages, debug messages and telemetry. A masked value (***) is shown instead. The PrintNode report log now shows *** in the authentication key field.
- **Debugger protection.** Procedures that handle credentials or build authorisation headers are now marked as non-debuggable, so their values cannot be inspected in the debugger.

Entries written before this version are not changed.

#### Related PR

- PR 15980 (BRCCore): #31545 Sensitive-data hardening: mask credentials, redact logs

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No separate bugfixes in this release.
