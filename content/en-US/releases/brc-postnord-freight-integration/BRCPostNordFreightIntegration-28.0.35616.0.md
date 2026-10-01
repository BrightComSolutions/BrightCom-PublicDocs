---
title: BRCPostNordFreightIntegration 28.0.35616.0
categories: [BRCPostNordFreightIntegration, ReleaseNotes]
description: PostNord Freight Integration now targets Business Central 2026 release wave 1 (BC28), with a raised minimum version.
date: 2026-10-01
---

## About this release

This is the first release note published for PostNord Freight Integration, the add-on that books shipments directly with PostNord's APIs and prints labels from Business Central. It covers the changes made to the app during 2026.

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Business Central 2026 release wave 1 (BC28) | The app is rebuilt for Business Central 28.0, and its version number now follows the Business Central platform. | 31339 |

## Detailed Feature Information

---

### Business Central 2026 release wave 1 (BC28) (#31339)

PostNord Freight Integration now targets Business Central 2026 release wave 1. The app's required platform and application versions move from `19.0.0.0` to `28.0.0.0`, and the AL runtime moves from `8.0` to `17.0`.

Earlier in 2026 the app's code was brought up to date for newer Business Central versions, including the removal of its dependency on the retired `NoSeriesManagement` codeunit, which no longer exists in BC28. In this version a PostNord sending gets its number through the Business Central `No. Series` codeunit, which replaces it.

The version jumps from 20.0 to 28.0 because the app's major version now follows the Business Central platform it is built for.

#### Related PR

- PR 15715 (BRCPostNordFreightIntegration): BC28 — platform/application 28, runtime 17.0, version 28.0.0.0
- PR 13260 (BRCPostNordFreightIntegration): Code quality cleanup for newer Business Central versions
- PR 15799 (BRCPostNordFreightIntegration): Assign the sending number from its number series again

## Breaking Changes

**Minimum Business Central version raised to 28.0 (2026 release wave 1).**

The app's required application and platform versions move from `19.0.0.0` to `28.0.0.0`. Environments still on Business Central 27 or earlier cannot install this version; they stay on the previous release of the app until the environment is updated.

## Bugfixes

- Creating a PostNord sending works again: a new sending gets its number from the **PostNord Sending Nos.** number series. Build 28.0.35455.0, published earlier on 2026-10-01, stopped with the error *"Number series assignment not yet updated for BC compatibility"* instead; this release replaces it.
