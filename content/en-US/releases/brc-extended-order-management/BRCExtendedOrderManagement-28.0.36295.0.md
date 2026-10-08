---
title: BRCExtendedOrderManagement 28.0.36295.0
categories: [BRCExtendedOrderManagement, ReleaseNotes]
description: Daily usage signal so BrightCom can see which features are used and spot problems early, plus a fix for the Shipping Advice Code field on the purchase order.
date: 2026-10-08
---

This release also includes the changes first shipped in 28.0.36086.0 on 2026-10-07.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | The app sends a once-a-day usage signal to BrightCom's Application Insights, so BrightCom can see which features are used and spot problems early. No personal data and no document contents are sent. | 31558 |
| Shipping Advice Code on purchase orders | The field is now shown to users of the Back Order feature, which is where it belongs. | 31604 |

## Detailed Feature Information

---

### Daily usage telemetry (#31558)

Once a day, per company, Extended Order Management sends a small usage signal to BrightCom's Application Insights. It lets BrightCom see which features customers actually use, and notice problems, such as automatic posting that has stopped, before they turn into support cases.

The signal contains configuration and activity counts only: which features are set up and how many documents were processed. It contains no personal data, no document contents and nothing typed by a user. It uses the platform's own daily telemetry schedule, so no job queue entry is needed and nothing changes in how you work.

There are two events:

- **BRCEOM-0101, Configuration.** Which features are set up: automatic posting (and for how many document types), drop shipment, prepayment (sales and purchase), back orders, extended status codes, demand planning level and intercompany partners using extra fields.
- **BRCEOM-0103, Automatic posting health.** Whether the automatic posting job is ready, on hold or in error, how many documents it logged yesterday, how many failed, and how many documents are still failing.

#### Daily usage telemetry, first version (#31558)

Adds the configuration and automatic posting health events described above.

#### Daily usage telemetry, second version (#31598)

Based on the first day of real data:

- Failing documents are now counted per document, not per failed retry, so one stuck document no longer looks like many. Whether the posting log is ever cleaned up is also reported.
- Prepayment is reported separately for sales and for purchases.
- The "BRC EOM All" permission set now includes the Prepayment Setup page and table. Users with this permission set can open the Prepayment Setup. The telemetry itself no longer depends on the user's permissions.

#### Related PR

- PR 15911 (BRCExtendedOrderManagement): #31558 Add daily usage telemetry
- PR 15960 (BRCExtendedOrderManagement): #31598 Telemetry v2

---

### Shipping Advice Code on purchase orders (#31604)

The Shipping Advice Code field on the Purchase Order page was tied to the Drop Shipment feature. It now belongs to the Back Order feature. It is shown for users of the Back Order feature and no longer depends on Drop Shipment being enabled.

#### Related PR

- PR 15972 (BRCExtendedOrderManagement): #31604 Fix application area on a field

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Shipping Advice Code on the Purchase Order page used the wrong application area (#31604)
