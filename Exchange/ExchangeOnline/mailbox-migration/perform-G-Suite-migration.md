---
layout: Conceptual
title: Perform a Google Workspace migration to Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/perform-g-suite-migration
Manager: jtremper
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: heidip
author: MicrosoftHeidi
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Migration instructions from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches.
ms.custom: seo-marvel-apr2020
ms.date: 2024-03-12T00:00:00.0000000Z
locale: en-us
document_id: 963b7331-1f6d-0400-d004-59797a4e87d1
document_version_independent_id: 71f2a5dd-0581-d33a-c41a-bef0ed1f208c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/perform-G-Suite-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/perform-g-suite-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/perform-G-Suite-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: 0901851f-825c-e828-e941-ebb8d0fbe9e6
---

# Perform a Google Workspace migration to Microsoft 365 or Office 365 | Microsoft Learn

You can migrate the following functionalities from Google Workspace to Microsoft 365 or Office 365:

- Mail & Rules
- Calendar
- Contacts

You can migrate batches of users from Google Workspace to Microsoft 365 or Office 365, allowing a migration project to be done in stages. This migration requires that you provision all of your users who will be migrated as mail-enabled users outside of the migration process. You must specify a list of users to migrate for each batch.

All procedures in this article assume that your Microsoft 365 or Office 365 domain is verified and that your TXT records have been set up. For more information, see [Set up your domain (host-specific instructions)](/en-us/microsoft-365/admin/get-help-with-domains/set-up-your-domain-host-specific-instructions).

Note

Google Workspace migration is not currently available for Office 365 US Government GCC High or DoD.

## Select your method of migration

You can migrate from Google Workspace using any of the following methods:

- [Automated - through the Exchange admin center](automated-migration-neweac)
- [Manual - through the Exchange admin center](manual-gspace-migration-overview)
- [PowerShell](perform-gspace-migration-powershell)

## Migration limitations

Important

Microsoft's data migration tool is currently unaware of tools enforcing messaging records management (MRM) or archival policies. Because of this, any messages that are deleted or moved to archive by these policies will result in the migration process flagging these items as "missing". The result is perceived data loss rather than actual data loss, which makes it much harder to identify actual data loss during any content verification checks.

Therefore, Microsoft strongly recommends disabling all MRM and archival policies before attempting any data migration to mailboxes.

Note

The largest single email message that can be migrated is based on the transport configuration for your tenant. The default limit is 35 MB. To increase this limit, see [Office 365 now supports larger email messages](https://www.microsoft.com/en-us/microsoft-365/blog/2015/04/15/office-365-now-supports-larger-email-messages-up-to-150-mb/).

Tip

To migrate Google Workspace mailboxes larger than 100 GB to Exchange Online primary and archive mailboxes, see [Migrate large mailboxes from Google or other IMAP sources to Microsoft 365 Exchange](automated-large-mailbox-migration-from-imap-sources).

Throughput limitations for contacts and calendars completely depend on the quota restrictions for your tenant's service account on the Google Workspace side.

Other migration limitations are described in the following table:

| Data type | Limitations |
| --- | --- |
| Mail | Vacation settings, Automatic reply settings |
| Meeting rooms | Room bookings won't be migrated |
| Calendar | Shared calendars and event colors won't be migrated |
| Contacts | A maximum of three email addresses per contact are migrated over |
| Contacts | Gmail tags, contact URLs, and custom tags won't be migrated |

Tip

Rules will be migrated and remain turned off by default. We advise users to verify the rules on Outlook before enabling them.

If you will be [starting your migration batch with Exchange Online Powershell](perform-gspace-migration-powershell), as described later in this article, use the `-ExcludeFolder` parameter to prevent certain folders from being migrated. This reduces the amount of data in your migration, and the size of a user's new Exchange Online mailbox. You can identify folders you don't want to migrate by name, and you can also identify Gmail labels that apply to multiple messages in order to exclude those messages from the migration. For more information on using `-ExcludeFolder`, see [New-MigrationBatch](/en-us/powershell/module/exchangepowershell/new-migrationbatch).

To skip the migration of Gmail filters, use the `-SkipRules` parameter to prevent the migration of Outlook rules. For more information on using `-SkipRules`, see [New-MigrationBatch](/en-us/powershell/module/exchangepowershell/new-migrationbatch).

## Prerequisites

Ensure you complete the following prerequisites before initiating either manual or automated Google Workspace migration:

1. Ensure you have been assigned a project creator role and you're signed into Google Workspace with the project creator credentials.
2. Ensure you complete the following procedures before initiating the migration process:
    1. Create a subdomain for mail routing to Microsoft 365 or Office 365
    2. Create a subdomain for mail routing to your Google Workspace domain
    3. Provision users in Microsoft 365 or Office 365

For detailed information on these steps, see [Google Workspace migration prerequisites](google-workspace-migration-prerequisites).