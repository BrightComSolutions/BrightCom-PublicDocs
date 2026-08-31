---
title: BRC Core 27.1.33905.0
categories: [BRCCore, ReleaseNotes]
description: Feature Management no longer filters ApplicationArea on API calls, plus new Atlas foundation infrastructure.
date: 2026-08-18
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| ApplicationArea guard by object type | Feature Management no longer applies ApplicationArea filtering to API pages and web service calls, so integrations no longer receive unexpectedly blank fields. | 29512 |
| Atlas foundation infrastructure | Groundwork for the Atlas integration foundation — staging tables, message routing, HTTP client utilities, and extensibility interfaces — ships in Core. Not yet enabled for use. | 24812 |

## Detailed Feature Information

---

### ApplicationArea guard by object type (#29512)

When BRC Core was installed alongside another extension, that extension's API pages could return unexpectedly blank field values.

The cause was in BRC Feature Management: it applied **ApplicationArea** filtering in all cases, including API pages and web service calls. Pages that correctly do *not* declare `ApplicationArea = All` — which API pages have no reason to — were therefore having their fields filtered out of the response.

Feature Management now guards on the object type. ApplicationArea filtering is applied only where it is meaningful for the user interface, and is skipped for API and web service invocations. A matching guard was added to the Login event so the same filtering does not run in that path either.

Integrations that were receiving empty values from a co-installed extension's API pages will now receive the correct data.

#### Related PRs

- PR 14975 (BRCCore): #29512 New ApplicationArea guard by type
- PR 14978 (BRCCore): #29512 Add guard to Login event

---

### Atlas foundation infrastructure (#24812)

This build carries the first release of the **Atlas** foundation into BRC Core: staging tables, message routing, HTTP client utilities, usage metering, and the extensibility interfaces that later app migrations will build on.

The infrastructure ships inactive. It introduces no change to existing Core behavior and requires explicit configuration before any of it takes effect. Further guidance will accompany the individual app migrations as they are released.

#### Related PR

- PR 15113 (BRCCore): Launching Atlas into AppSource

## Breaking Changes

No breaking changes in this release.

## Bugfixes

- Feature Management applied ApplicationArea filtering to API calls, blanking fields for co-installed extensions (#29512)
