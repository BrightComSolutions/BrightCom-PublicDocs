---
title: BRCRisk 28.0.38799.0
categories: [BRCRisk, ReleaseNotes]
description: Expanded risk mapping and credit-score guidance, migrated the provider integration to the LENS API and added direct company navigation.
date: 2026-11-12
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Risk Entity Mappings | Finished the placeholder actions and Risk Entity Mappings page. | 32008 |
| LENS API integration | Moved the provider integration to the LENS API ahead of the legacy API closure. | 32064 |
| Credit-score explanation | Added clearer explanations of credit scores for users. | 32007 |
| Correct zero-score risk level | Corrected the meaning of a credit score of zero when calculating risk level. | 32004 |
| Open provider company page | Added direct navigation to the company's page at the risk-data provider. | 32006 |

## Detailed Feature Information

---

### Risk Entity Mappings (#32008)

The Risk Entity Mappings page and its remaining placeholder actions are now complete.

### LENS API integration (#32064)

The provider integration now uses the LENS API, preparing the app for the closure of the legacy API.

### Credit-score explanation (#32007)

Users can see a clearer explanation of how a credit score contributes to the risk assessment.

### Correct zero-score risk level (#32004)

Risk-level calculation now interprets a credit score of zero correctly.

### Open provider company page (#32006)

The risk fact box now provides direct access to the company's page at the provider.

## Breaking Changes

No breaking changes in this release.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Incorrect risk level for a zero credit score | Corrected risk-level calculation for credit score zero. | 32004 |