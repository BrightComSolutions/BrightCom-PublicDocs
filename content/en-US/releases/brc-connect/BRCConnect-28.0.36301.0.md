---
title: BRCConnect 28.0.36301.0
categories: [BRCConnect, ReleaseNotes]
description: Security hardening, daily usage signal, auto-release of transfer orders, safer parallel Operators, better diagnostics for failed sends and a location fix for next expected delivery.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36084.0 on 2026-10-06.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Security hardening | Credential fields are masked, and secrets are kept out of logs, messages and telemetry. | 31545 |
| Daily usage telemetry | A once-a-day usage signal helps BrightCom see which features are used and spot problems early. | 31554 |
| Auto-release transfer orders | Transfer orders created by BRC Connect can be released automatically. | 31525 |
| Next expected delivery respects location | The next expected delivery in stock messages only uses purchase lines for the same location. | 30368 |

## Detailed Feature Information

---

### Security hardening (#31545)

BRC Connect now handles credentials more carefully:

- Credential fields on setup pages, such as the Bearer Token on BRC Connect Setup, are masked.
- Passwords, keys and tokens are removed from logs, error messages, debug messages and telemetry.
- Procedures that handle credentials can no longer be inspected in the debugger.

Entries written before this version are not changed.

#### Related PR

- PR 15977 (BRCConnect): #31545 Sensitive-data hardening: mask credentials, redact logs, remove client data

---

### Daily usage telemetry (#31554)

Once a day, the app sends a usage signal to BrightCom's Application Insights. It holds configuration and activity counts, for example which features are set up and how many documents were processed. BrightCom uses it to see which features are used and to spot problems early.

The signal contains no personal data and no document contents.

The signal is sent as five events, with IDs BRCCON-0101 to BRCCON-0105:

- BRCCON-0101: how Connect is set up
- BRCCON-0102: how much work Connect did the day before
- BRCCON-0103: backlogs and error counts
- BRCCON-0104: traffic per target table
- BRCCON-0105: integration landscape and mapping shape

#### BRC Connect: daily usage telemetry v2 (#31595)

Corrects and extends the signal after the first days of data. Several counts now measure what their names say, and failed or exhausted work is reported separately from work that is still being retried.

#### Related PR

- PR 15907 (BRCConnect): #31554 BRC Connect: meaningful daily usage telemetry
- PR 15961 (BRCConnect): #31595 BRC Connect: daily usage telemetry v2

---

### Auto-release transfer orders (#31525)

Transfer orders created by BRC Connect can now be released automatically as soon as they are created. This saves a manual step and lets warehouse processing start sooner.

- The new setting **Auto-Release Created Transfer Documents** is on BRC Connect Setup and on each BRC Connect Source. A new source takes its value from the setup.
- It is off by default. Nothing changes until you turn it on.
- Standard Business Central release checks still apply. If a document cannot be released, it stays open.

#### Related PR

- PR 16008 (BRCConnect): #31525 Add support for auto-releasing transfer orders in BRC Connect

---

### Next expected delivery respects location (#30368)

When **Add Next Exp Delivery** is on, stock messages include the incoming quantity from purchase lines. The quantity now only comes from purchase lines with the same location code as the stock message. Lines for other locations no longer count. Message structure and API payloads are unchanged.

#### Related PR

- PR 15620 (BRCConnect): Add a filter on location when fetching next available date.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- **Parallel Operators could link Incoming Data to the wrong document (#31607).** Two Operators working at the same time could end up linking two Incoming Data entries to the same document. This was seen on transfer orders, and sales documents were affected too. Operators now claim work one at a time. Overlapping claims are dropped, and a document is only linked to the Incoming Data it came from. Conflicts are retried without using up the retries for the entry, and are counted in the new **Conflict Count** field on Incoming Data. (PR 16001)
- **Outgoing entries marked as sent could not be diagnosed when the send failed (#31608).** Connect Entries now store the real **HTTP Status Code** of the last request. Before this, every error showed "HTTP 0". When no response arrives at all, the reason is stored instead. The new **Response Warning** field flags a successful response whose body reports an error. Both fields are shown on the BRC Connect Entries page. Entries are processed as before. Entries with a response warning are kept for 7 days during cleanup. (PR 16002)
