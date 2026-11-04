---
layout: Conceptual
title: Choose a large mailbox migration approach to Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/choose-large-migration-approach
Manager: aleeming
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: rahu
author: rahu-microsoft
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Learn how to choose a large mailbox migration approach before migrating to Exchange Online.
ms.date: 2026-08-26T00:00:00.0000000Z
locale: en-us
document_id: 6720bdd0-2bd1-a119-d128-5209e3977d38
document_version_independent_id: 0cb0406f-9f12-8a59-8f33-12f5d550b2a6
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/choose-large-migration-approach.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/choose-large-migration-approach
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/choose-large-migration-approach.md
platformId: 220d353b-002c-9e76-7d75-1b121568b367
---

# Choose a large mailbox migration approach to Microsoft 365 | Microsoft Learn

Large mailbox migrations require additional planning because mailbox data might exceed the storage capacity of a single Exchange Online mailbox or require specialized migration procedures. This article helps you choose the appropriate migration approach based on the source system, mailbox characteristics, and migration requirements.

## What is a large mailbox?

For the purposes of migration to Microsoft 365, a large mailbox is a mailbox whose content can't be accommodated within a single Exchange Online mailbox and therefore requires archive storage, mailbox-content redistribution, or specialized migration procedures.

## Choose a migration approach by source system

The below source systems are supported.

- Google Workspace.
- Mail server that supports Internet Message Access Protocol (IMAP), that is, IMAP server.
- Exchange Server.

Use the following guidance to determine the appropriate migration approach.

![A diagram reflecting the decision tree to choose a large mailbox migration approach.](../exchangeonline/mailbox-migration/media/choose-migration-approach-decision-tree.png)

| Source system | Migration method | Description |
| --- | --- | --- |
| Google Workspace or IMAP server | [XML mapping](automated-large-mailbox-migration-from-imap-sources) | Migrate mailbox directly to Exchange Online and control how mailbox content is distributed across the primary mailbox, archive mailbox, and auxiliary archive mailboxes. |
| Exchange Server | [Retention policy](large-mailbox-migration-from-onpremises) | Use retention policies and auto-expanding archiving feature to reduce primary mailbox size before migration. |
| Exchange Server | [XML mapping](large-mailbox-migration-from-onpremises-xml-mapping) | Migrate mailbox directly to Exchange Online and control how mailbox content is distributed across the primary mailbox, archive mailbox, and auxiliary archive mailboxes. |

## Choose a migration approach for Exchange Server

### Retention policy

This method uses Exchange retention policies and auto-expanding archiving to move content into Exchange Online archive mailboxes before a standard mailbox migration.

Use this migration method when:

- Existing retention policies meet your business and compliance requirements.
- Mailbox content can be reorganized before migration.
- You don't need to control the destination mailbox location for specific content.

For more information, see [Migrate large mailboxes from Exchange on-premises with retention policies](large-mailbox-migration-from-onpremises).

### XML Mapping

This method uses Large Mailbox Onboarding (LMO) to migrate mailbox content directly to Exchange Online primary, archive, and auxiliary archive mailboxes during migration. Administrators define mailbox-content mappings by using an XML mapping file. For more information about automated XML file generation, see [Analyze source mailboxes before migrating from Google Workspace or IMAP](source-mailbox-analysis-google-imap) or [Analyze source mailboxes before migrating from Exchange On-Premises](source-mailbox-analysis-onpremises).

Use this migration method when:

- Mailbox data can't be easily reduced by using retention policies.
- You need explicit control over mailbox-content placement during migration.
- Mailboxes contain large amounts of data that must be distributed across multiple Exchange Online storage locations.

For more information, see [Migrate large mailboxes from Exchange on-premises with XML mappings](large-mailbox-migration-from-onpremises-xml-mapping).