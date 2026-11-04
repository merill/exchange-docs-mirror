---
layout: Conceptual
title: Google Workspace automated batch mail migration overview | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrate-google-mail-automated-overview
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
author: MachelleTranMSFT
ms.author: dansimp
audience: admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Overview of the automated solution for migrating a Google Workspace email to Microsoft 365 or Office 365
ms.date: 2023-08-06T00:00:00.0000000Z
locale: en-us
document_id: f54b0598-b7d9-88cc-4d30-e376a3a5f2f1
document_version_independent_id: 33253218-f43e-7c3c-6ca7-b99c58cf8516
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-automated-overview.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrate-google-mail-automated-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-automated-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: eada2347-4a92-4e10-fe0a-ed168561a5ab
---

# Google Workspace automated batch mail migration overview | Microsoft Learn

The [batch migration tool](manage-migration-batches) in the [Exchange Admin Center](https://admin.exchange.microsoft.com/) can transfer your organization's mail, rules, calendars, and contacts from Google Workspace to Microsoft 365. Microsoft recommends using the automated method because it completes several required tasks in your Google admin console for you.

Note

Google Workspace migration is not currently available for Office 365 US Government, GCC High, or DoD.

Important

We strongly recommend disabling all messaging records management (MRM) tools and archival policies before attempting any data migration. Tools that enforce MRM and archival policies cause perceived data loss when no actual data loss has occurred. Archiving or deleting messages also result in items flagged as "missing" during the verification checks.

## Prerequisites

Before attempting an automated migration, you must complete the following prerequisites:

- [Prerequisite Step 1 - Create a subdomain in Google Workspace to route mail to Microsoft 365](migrate-google-mail-prerequisite-create-mail-routing-subdomain-m365)
- [Prerequisite Step 2 - Create a subdomain to route mail to Google Workspace](migrate-google-mail-prerequisite-create-mail-routing-subdomain-google-domain)
- [Prerequisite Step 3 - Provision mail users to migrate from Google Workspace to Microsoft 365](migrate-google-mail-prerequisite-provision-m365-users)
- [Prerequisite Step 4 - Verify Google migration administrator role assignments](migrate-google-mail-prerequisites-admin-role-assignment)

## Batch migrations

As an Exchange administrator, you can migrate users all at once or in batches. Batch migration is recommended if your organization has many users, which require mail migration to occur in stages. You need to create a CSV file that lists the users you want to migrate for each migration batch. The CSV creation process is covered in later steps.

Tip

If you need to migrate a small number of users, you can migrate them all at once using a PST file.

For an overview of the automated migration process, check out this video:

## Migration limitations

The quota restrictions of your Google Workspace tenant service account can determine the throughput limitations for contacts and calendars.

| Data type | Limit |
| --- | --- |
| Contacts | A maximum of three email addresses per contact are migrated over |
| Email size | Default limit of 35 MB per single email. This size can be configured up to 150 MB. |

### What isn't migrated

| Data type | Not migrated |
| --- | --- |
| Mail | vacation settings, automatic reply settings |
| Meeting rooms | room bookings |
| Calendar | shared calendars, event colors |
| Contacts | Gmail tags, contact URLs, custom tags |