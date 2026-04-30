---
title: BRC Extended IC 26.0.30959.0
categories: [BRC Extended IC, ReleaseNotes]
description: Cross-database intercompany support with OAuth2 authentication
date: 2026-04-22
---

## Release Summary

| Feature                                              | Description                                                                                    |   ID |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---: |
| Extended IC & Standard IC Cross-Database Support     | Enable intercompany transactions across different databases using OAuth2 authentication        | 23388 |

## Detailed Feature Information

---

### Extended IC & Standard IC Cross-Database Support (#23388)

Built support for Extended Intercompany and standard Intercompany functionality across different databases using OAuth2 authentication. Previously, Extended IC only supported companies within the same database, limiting its use for organizations with multi-database architectures.

**Business Value:** Enables intercompany transactions between Business Central companies hosted in separate databases, supporting more complex organizational structures. Multiple customers require IC functionality across database boundaries, and this enhancement removes that limitation while maintaining security through OAuth2 authentication.

**Technical Details:**
- Implements OAuth2 authentication for cross-database IC communication
- Supports both Extended Intercompany and standard Intercompany scenarios
- Master Data can now reside in different databases
- Maintains compatibility with existing single-database IC configurations
- Enables secure, authenticated communication between database instances

**Use Cases:**
- Organizations with separate databases per legal entity
- Multi-tenant scenarios requiring intercompany transactions
- Hybrid cloud/on-premises IC scenarios
- Compliance-driven database separation

---

## Breaking Changes

No breaking changes in this release. Existing single-database IC configurations continue to work as before.
