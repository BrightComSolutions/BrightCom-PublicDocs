---
title: BRCRetailExtension 28.0.36072.0
categories: [BRCRetailExtension, ReleaseNotes]
description: BRC Retail Extension now sends a once-a-day usage signal with configuration and catalog-size counts to BrightCom's Application Insights.
date: 2026-10-08
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Daily usage telemetry | The app sends a once-a-day usage signal with setup and master data counts, so BrightCom can see which features are used and spot problems early. | 31565 |

## Detailed Feature Information

---

### Daily usage telemetry (#31565)

BRC Retail Extension now sends a small usage signal to BrightCom's Application Insights once a day for each company. It runs together with the standard Business Central daily telemetry.

BrightCom uses the signal to see which retail features are in use and how large the retail master data is, and to spot problems early. It helps us decide which options to keep, improve or retire.

The signal contains counts, yes/no values and the names of the app's own option values only. It contains no personal data, no codes, names or free text, and no document contents. It does not change or block anything in Business Central. If the setup is missing or cannot be read, nothing is sent.

Two events are sent:

- **BRCRET-0101, Retail daily: configuration.** Which setup options are in use:
  - how many document types (sales, purchase, transfer) prompt for variants
  - how many document types use variant descriptions on lines
  - how many matrix location slots are filled for sales, purchase and transfer documents (the count only, never the location codes)
  - the EAN check digit method
  - whether variant values are inserted automatically
  - whether sorting is updated on modify
  - whether delivery season is calculated automatically, which date basis is used, and how many targets it is copied to
- **BRCRET-0102, Retail daily: catalog size.** How many records the app's own master data tables hold: variant templates, variants, variant values, item variant assignments, brands, seasons, delivery seasons, order types and ordering terms. Document tables are not counted.

The new codeunit is included in the **BRC Retail All** permission set.

#### Related PR

- PR 15918 (BRCRetailExtension): #31565 Add daily usage telemetry (BRCRET-0101 configuration, BRCRET-0102 catalog size)

## Breaking Changes

No breaking changes in this release.

## Bugfixes

No separate bugfixes in this release.
