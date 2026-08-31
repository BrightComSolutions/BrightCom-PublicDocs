---
title: BRC Logistics 25.0.34046.0
categories: [BRCLogistics, ReleaseNotes]
description: Return reason codes can now be excluded from the InRetrn return order flow.
date: 2026-08-25
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Excluded return reason codes for InRetrn | A new setup field lists return reason codes that should not be brought into Business Central, so repair and spare part returns no longer create documents. | 29536 |

## Detailed Feature Information

---

### Excluded return reason codes for InRetrn (#29536)

Where InRetrn is running with webhooks *and* BRC Logistics is also issuing a return order request, the request returns every closed return — including operational returns such as **repair** and **spare part** cases that should never reach Business Central. These were being imported as customer returns, creating manual cleanup and the risk of incorrect warehouse and financial processing.

Because all incoming returns carry the status *Closed*, status cannot be used to distinguish them. The filter is therefore applied on the **return reason**.

A new field, **Excluded Return Reason Codes**, has been added to the BRC Logistics Setup card under a new **EasyCom/Inretrn** group. It accepts a comma-separated list of return reason codes. Returns whose reason matches an entry in that list are closed out during the return order request instead of being created in Business Central.

The field is empty by default, so existing behavior is unchanged until reason codes are configured.

#### Related PR

- PR 15146 (BRCLogistics): #29536 CR-138 InRetrn spare part

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- None in this release.
