---
title: BRCLogistics 28.0.36303.0
categories: [BRCLogistics, ReleaseNotes]
description: Daily usage telemetry, hardened handling of credentials, a configurable Sello return lookback window, Ongoing expiration dates on purchase receipts, and a fix for sales and assembly lines that share an item and line number.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36087.0 on 2026-10-07.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | Once a day the app sends a usage signal with configuration and activity counts to BrightCom, so we can see which features are used and spot problems early. No personal data, no document contents. | 31559 |
| Security hardening | Credential fields on setup pages are masked, and passwords, keys and tokens are kept out of logs, messages and telemetry. | 31545 |
| Configurable lookback window for Sello return polling | A new setting controls how far back each Sello return poll looks, so returns that Sello registers late are no longer missed. | 30315 |
| Expiration date from Ongoing on purchase orders | The expiration date reported by Ongoing on a receipt is now stored on the warehouse line package. | 31494 |
| Sales and assembly lines with the same item and line number | Shipment notices now tell apart a sales order line and an assembly component line that share item and line number. | 27786 |

## Detailed Feature Information

---

### Daily usage telemetry (#31559)

The app now sends a usage signal to BrightCom's Application Insights once a day per company. It contains configuration and activity counts: which features are set up (for example which integration engines are enabled and whether automatic sending is on) and how many documents were processed. BrightCom uses it to see which features are used and to spot problems early.

The signal contains no personal data and no document contents. Only counts, yes/no values and integration engine numbers are sent.

Four events are sent, with these event IDs:

- **BRCLGS-0101** - configuration: enabled and configured integration engines, and which automation options are on.
- **BRCLGS-0102** - volume: how many shipment, receival, return and exchange orders, item requests and confirmation notices were handled the day before.
- **BRCLGS-0103** - health: how many recent documents are still open, how many of those have errors, and how many outbound orders are not yet sent or are waiting for the warehouse system.
- **BRCLGS-0104** - traffic: yesterday's warehouse transactions per integration engine.

#### Daily usage telemetry v2 (#31596)

Second version of the signal, based on the first days of real data.

- **Connector coverage.** The configuration event now also reports the integration engines of setups that are not enabled, so it shows what each company has set up, not only what is switched on.
- **More accurate open-document counts.** The "open documents" and "with errors" counts now cover only the document types the app itself closes when it processes them: shipment and receival notices, and item adjustments, balances and movements. A new value states this scope. The earlier count mostly measured outbound orders, which the app does not close, so it is now reported separately as a volume figure.
- The "not sent" and "awaiting warehouse" counts now apply to outbound orders, where those statuses belong.

#### Related PR

- PR 15912 (BRCLogistics): #31559 Meaningful daily usage telemetry
- PR 15959 (BRCLogistics): #31596 Daily usage telemetry v2

---

### Security hardening (#31545)

Part of a sweep across all BrightCom apps to protect sensitive data.

- **Masked credential fields.** Password, key and secret fields on the BRC Logi Setup card, including the Bitlog fields, are now masked.
- **Credentials kept out of logs and messages.** Passwords, keys and tokens are removed from logs, stored request data, error messages, debug messages, confirmations and telemetry.
- **No debugger inspection.** Procedures that handle credentials can no longer be inspected in the debugger.

Entries written before this version are not changed.

#### Related PR

- PR 15989 (BRCLogistics): #31545 Sensitive-data hardening

---

### Configurable lookback window for Sello return polling (#30315)

Sello makes a return available for polling some time after the marketplace reports it. If that delay was longer than the fixed 100-minute window the app used, the return was never fetched. Some customers saw returns missing at random because of this.

#### Configurable lookback window (#30742)

A new field, **Sello Return Lookback (Minutes)**, is available in a new Sello group on the BRC Logi Setup card. It is shown for the Sello Return integration engine.

- It sets how many minutes before the previous poll each new poll starts looking for updated returns. Raise it if returns are missed.
- Blank or 0 means 100 minutes, so existing connections behave exactly as before.
- The maximum is 1440 minutes (24 hours).
- The first poll still looks back 10 days.

#### Related PR

- PR 15899 (BRCLogistics): #30315 Configurable lookback window for Sello return polling

---

### Expiration date from Ongoing on purchase orders (#31494)

When Ongoing reports a received purchase order line with an expiration date, the app now reads it and stores it in the **Expiration Date** field of the warehouse line package. Before, the date was ignored.

#### Related PR

- PR 15923 (BRCLogistics): #31494 Use Expiration Date sent from Ongoing on PO

---

### Sales and assembly lines with the same item and line number (#27786)

When an item was sold on its own line and also used as a component of an assembly item, and both lines had the same item and line number, a shipment notice could mix them up. The line was then treated as already delivered, which caused wrong deliveries, items not picked and failing or stuck warehouse transactions.

Shipment notice processing now:

- prefers the request line that matches the document and table the warehouse reports;
- does not match a request line that another line has already claimed;
- skips closed assembly lines, avoids duplicate lines and clears errors once a line matches;
- flags unmatched assembly components that have a quantity as errors.

#### Related PR

- PR 15901 (BRCLogistics): #27786 Distinguish sales and assembly component lines with same item and line no.

## Breaking Changes

No breaking changes in this release.

Behaviour changes to be aware of:

- **Masked fields.** Credential fields on the setup pages now show masked values. Stored values are unchanged.
- **Assembly components in shipment notices.** Unmatched assembly components with a quantity are now reported as errors.

## Bugfixes

- Sales order lines and assembly component lines with the same item and line number are mixed up in shipment notices (#27786)
- Sello returns registered late by the marketplace are never fetched (#30315)
- Expiration date sent by Ongoing on purchase orders is ignored (#31494)
