---
title: BRCExtendedIC 28.0.35612.0
categories: [BRCExtendedIC, ReleaseNotes]
description: Concurrent Ext. IC releases no longer block each other, plus a broad set of fixes for intercompany between separate environments (API and Azure Blob partners).
date: 2026-10-01
---

## Release Summary

| Feature | Description | ID |
| --- | --- | ---: |
| Concurrent Ext. IC releases no longer block each other | Releasing several Ext. IC orders at the same time no longer makes some of them fail or get stuck in the selling company. IC transaction numbers are taken without locking General Ledger Setup, and one release no longer waits on another's IC outbox transaction. | 30457 |
| Cross-environment IC fixes | Orders, relations, field updates, post requests, partner settings and master data now flow correctly between companies in separate Business Central environments (API and Azure Blob partners). Found and verified with a new end-to-end cross-tenant test rig. | 30457 |

## Detailed Feature Information

---

### Concurrent Ext. IC releases no longer block each other (#30457)

Some customers saw sales orders that should have been passed on to their warehouse company get stuck in the selling company, with an error in the incoming log saying changes could not be saved because of an update to General Ledger Setup. It happened sporadically and more often under load; the workaround was to reopen and release the stuck orders by hand.

The cause was that every Ext. IC release locked shared records until the release finished:

- **IC transaction numbers.** When Business Central's own IC transaction number sequence did not yet exist, Extended IC took each number by locking and updating **Last IC Transaction No.** in General Ledger Setup. Extended IC now always uses the shared, lock-free IC transaction number sequence. The sequence is created once, on install or upgrade, seeded from the highest number already used in General Ledger Setup and all IC inbox and outbox tables, so numbering carries on without gaps or clashes.
- **The IC outbox.** Business Central's "already sent, send again?" check scanned the whole IC Outbox Transaction table and waited on other sessions' unfinished releases. Extended IC's automatic send is non-interactive and already guards against sending a document twice, so that check is now skipped for it.

Releases of different orders now run independently of each other.

---

### Cross-environment IC fixes

This release fixes the faults found by a new **cross-tenant test rig**: one Business Central container with two tenants that talk to each other only through the real Extended IC inbox API, as two separate customer environments would. Its scenarios cover orders, relations, field updates, post requests, returns, price markup, item references, partner outages, master data sync/rename/delete, a restricted delegated (GDAP) consultant user and concurrent releases.

The fixes below mostly affect partners with Inbox Type **BRC ExtIC API** or **BRC ExtIC Azure Blob**. Partners in the same database are affected only where noted.

#### Orders and post requests

- **Releasing an order while the IC partner is unreachable no longer fails** (#31441). The release completes, the IC transaction stays in the IC outbox and the document gets IC Status **Pending**. The Outbox Delivery Task (Outgoing partners) or the Inbox Maintenance Task (Incoming partners) sends it automatically once the partner is reachable, and the failure is written to the Activity Log.
- **Accepted orders wait for their Ext. IC data** (#31426). With **Auto. Accept Transactions** on, the IC transaction could arrive before the order's header and line data and fail with "could not be retrieved from IC partner's inbox". The transaction is now left for the Auto. Accept job until the data has arrived (for up to 30 minutes, after which the normal error is shown).
- **A failed accept no longer leaves an order behind** (#31351). Creating the sales order from an IC inbox transaction is now all-or-nothing, so a retry no longer creates another, empty order. Before anything is created, Extended IC also checks that the partner's **Sales Order Line Fields** send the item No. and Quantity, and if not, explains exactly what to add in the partner's company.
- **Ship and Invoice for a fully received order works** (#31428). When posting completed an order, the warehouse failed with "The Sales Line does not exist" while building the post request for the seller. The partner's line references are now kept through the posting.
- **Reopening a sent order works** (#31427). Reopen no longer fails with "Value change for field 120 'Status' is not allowed for Sales Header". Status fields are no longer checked against the Sales Document Fields setup.
- **A skipped send is now logged** (#31342). When a released order is not sent because the item's IC vendor has the wrong IC Partner Code, or a location that doesn't match, an Activity Log error names the cause and the fix, where before the order was silently not sent.
- **One release can no longer send another release's IC transaction** (#31365). The IC outbox export no longer widens the filter it is given.

#### Relations and field updates

- **The seller now processes the warehouse's relations** (#31423). These were only processed when the partner had Auto. Accept Transactions, or by the Relation Task, which exists only for Incoming partners. The Inbox Maintenance Task now processes them on both sides.
- **The Relation Task now finds its work** (#31424). It looked for pending entries under the wrong IC partner code and never ran.
- **Relations are processed one entry at a time** (#31425). Overlapping runs no longer fail with "The BRC Ext. IC JSON Inbox does not exist". A failing entry is logged and retried without holding back the others, and entries are applied in the order they were received.
- **Field updates reach API/Blob partners** (#31443). Field update rows were sent without a record ID, and the partner's inbox rejected them.
- **Received field updates are applied** (#31445). Updates arrived but were never applied, and in some cases blank values were applied instead of the partner's values. The partner's values are now applied, and an error is raised if the source data is missing, instead of fields being cleared.

#### Partner settings and setup data

- **Price markup and other partner settings now apply across environments** (#31429). Each company now sends its IC Partner settings (price method, markup, post requests, service items) to the partner, without connection details or secrets.
- **Order release no longer fails with "LCY Code must have a value"** (#31340), and **inbox accept no longer fails with "IC Partner Code must have a value in IC Setup"** (#31350). The partner's General Ledger Setup and IC Setup received through the inbox are now read correctly.
- **Missing partner data is reported as missing** (#31341). The inbox lookup reported success when nothing had arrived, so callers went on with empty data.

#### Master data

- **Rename and delete propagate to API/Blob partners** (#31432). The old key now travels with each rename or delete entry (new **Old Primary Key** field on the BRC Ext IC Rename Log Entry). Each entry is applied on its own, so one failure is logged and no longer stops the whole Data Import Task.
- **A rename no longer creates a duplicate record** (#31431). Renames are now applied before the partner's data is imported.
- **Imported records no longer inherit values from the previous row** (#31430). Each imported row starts from an empty record.

#### Delivery and the inbox API

- **IC transactions can be delivered over the API** (#31349). The receiver decoded the UTF-16 XML as UTF-8 and failed with "Data at the root level is invalid".
- **Retried deliveries are not duplicated** (#31345). An entry that is already in the JSON inbox is accepted again without being inserted twice.
- **The inbox API no longer returns the partner API key** (#31346). The response no longer echoes the shared secret or the payload.
- **Outbox delivery no longer blocks other work** (#31366). Entries are delivered one by one in short transactions, and background delivery is bound to the IC partner, so concurrent accepts and releases no longer time out and delivery tasks no longer fail because another task already sent an entry.

#### Delegated (GDAP) users and background tasks

- **Release no longer fails with "no permission to create scheduled tasks"** (#30779). A reversed check tried to create a scheduled task exactly when that was not allowed. Users who cannot schedule tasks, such as delegated (GDAP) administrators, now fall back to a background session.

#### Activity Log

- **The verbosity setting works as described** (#31352). The filter was reversed: **Warning** dropped errors, and the default (**None** for IC Setup records created before Extended IC was installed) logged nothing at all. The default is now **Error**, and existing setups set to None are moved to Error on upgrade.
- **Repeated entries are no longer swallowed** (#31353). The duplicate check compared against an empty record and could stop all logging. Only identical entries within the same minute are skipped.
- **Logging can no longer break the operation it logs** (#31354). If the logging session cannot start, the entry goes to telemetry instead.
- **Release in Swedish no longer fails** (#30778). Translated Activity Log context texts were longer than the field and broke the release; those texts are now fixed, untranslated labels.

#### Other fixes

- **Sales Order Fields opens for the right partner** (#30777). It could pick up an IC Partner with a blank Code instead of the partner being configured.
- **Deleting an IC Partner with a blank Code explains why it fails** (#30780). Business Central blocks the delete while **Allow G/L Acc. Deletion Before** is set; the message now says so, explains the workaround and offers to open General Ledger Setup.
- **Swedish and Danish texts** (#30781). Swedish and Danish texts that were cut off after "BRC Ext." are complete again; in the Sales Document Field configuration error, the cut hid the part that tells you to set the partner's Direction. All previously untranslated texts now have Swedish and Danish translations.

#### Related PR

- PR 15797 (BRCExtendedIC): #30457 Cross-environment IC fixes found with the cross-tenant rig

## Breaking Changes

No breaking changes in this release.

Behaviour changes to be aware of:

- **Activity Log verbosity.** Because the verbosity filter now works as described, environments set to **Warning** or **Error** will log entries they previously dropped, and IC Setup records set to **None** are moved to **Error** on upgrade. Set the verbosity again after upgrading if you want a different level.
- **Received orders are validated first.** An incoming IC order whose partner does not send the item No. and Quantity in its Sales Order Line Fields is now refused with an explanation. Previously an order with empty lines was created.

## Bugfixes

- Concurrent Ext. IC releases no longer block each other on General Ledger Setup and the IC outbox (#30457)
- Sales Order Fields page resolves a blank-code IC Partner instead of the filtered partner (#30777)
- Release of an IC sales order fails in Swedish: Activity Log context too long for translated labels (#30778)
- Release of an IC sales order fails with "no permission to create scheduled tasks" (#30779)
- IC Partner with a blank Code cannot be deleted: now explained with a workaround (#30780)
- sv-SE and da-DK translations truncated after "BRC Ext." (#30781)
- Cross-environment order release fails with "LCY Code must have a value" (#31340)
- Inbox lookup reports success when no partner data has arrived (#31341)
- Order send silently skipped when the IC vendor's IC Partner Code or location doesn't match (#31342)
- Retried deliveries create duplicate JSON Inbox entries (#31345)
- Inbox API returns the partner API key in its response (#31346)
- IC transactions cannot be delivered over API: "Data at the root level is invalid" (#31349)
- Cross-environment inbox accept fails with "IC Partner Code must have a value in IC Setup" (#31350)
- Failed IC inbox accept leaves the created sales order behind (#31351)
- Activity Log verbosity filter reversed; default logged nothing (#31352)
- Activity Log duplicate check could silently stop all logging (#31353)
- Activity Log failure could break the operation being logged (#31354)
- IC outbox export could send another release's IC transaction (#31365)
- JSON outbox delivery locked the partner's whole outbox, so concurrent accepts and releases timed out (#31366)
- Seller never processed the warehouse's relations without Auto. Accept Transactions (#31423)
- Relation Task never ran: wrong IC partner code in its pending-entry check (#31424)
- Concurrent relation processing fails with "The BRC Ext. IC JSON Inbox does not exist" (#31425)
- With Auto. Accept Transactions on, the IC order was accepted before its Ext. IC order data arrived (#31426)
- Reopening a sent sales order fails on the Status field check (#31427)
- Warehouse can't post Ship and Invoice for a received order: "The Sales Line does not exist" (#31428)
- Price markup not applied across environments (#31429)
- Master data import copies field values from the previous record into new records (#31430)
- Cross-environment master data rename creates a duplicate record (#31431)
- Master data rename and delete never propagate to API/Blob partners (#31432)
- Releasing an Ext. IC order fails while the IC partner is unreachable (#31441)
- Field updates never reach an API/Blob partner (#31443)
- Field updates from an API/Blob partner arrive but are never applied (#31445)
