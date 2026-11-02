---
title: BRCExtendedFinanceManagement 28.0.38059.0
categories: [BRCExtendedFinanceManagement, ReleaseNotes]
description: Salesperson changes on the customer card can update the customer's sales contracts, and contract comments can be updated through the API.
date: 2026-11-02
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Salesperson follows the customer card on sales contracts | A new setting updates the Salesperson Code on a customer's BRC sales contracts when the salesperson is changed on the customer card. | 31367 |
| Contract comments through the API | Contract Comments on BRC sales contracts can be created, changed and cleared with PATCH requests. | 31585 |

## Detailed Feature Information

---

### Salesperson follows the customer card on sales contracts (#31367)

A new setting, **Auto Update Sales Person**, on **BRC Sales Contract Setup** keeps contracts in line with the customer card. When it's on and you change **Salesperson Code** on a customer, the new salesperson is set on every BRC sales contract with that customer as Sell-to Customer.

The update happens at the moment of the change on the customer card. You can still change the salesperson on a single contract afterwards. Off by default.

### Contract comments through the API (#31585)

**Contract Comments** on BRC sales contracts can now be updated through the web service as well as on the page: integrations can create, change and clear a contract's comments with a PATCH request.

## Breaking Changes

For extensions that build on BRC Extended Finance Management: the table procedure `SetContractComments(var BigText)` on **BRC EFM Sales Contract Header** is obsolete and now raises an error. Use `SetSalesContractComments(Text)` instead. The field itself is unchanged.

## Bugfixes

| Bug | Description | ID |
| --- | --- | ---: |
| Contract comments repeated across contracts | When several contracts were read in one request, a contract without comments could show the comments of the contract read before it. Each contract now shows its own comments. | 31585 |
