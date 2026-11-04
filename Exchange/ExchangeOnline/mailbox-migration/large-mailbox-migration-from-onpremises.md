---
layout: Conceptual
title: Migrate large mailboxes from on-premises Exchange to Microsoft 365 Exchange with retention policies | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/large-mailbox-migration-from-onpremises
Manager: michh
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: wesmills
author: wesmills
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Guidance and best practices for migrating large mailboxes from on-premises to Microsoft 365 Exchange with retention policies.
ms.custom: seo-marvel-jun2021
ms.date: 2024-04-15T00:00:00.0000000Z
locale: en-us
document_id: 067ed0d8-3d86-8c6c-bd02-59e92188f0ca
document_version_independent_id: cfdf11d7-d948-1b50-83ec-afd4620664f4
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/large-mailbox-migration-from-onpremises.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/large-mailbox-migration-from-onpremises
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/large-mailbox-migration-from-onpremises.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 2ee95018-dc41-eaa5-4d1f-afcd8cf36d46
---

# Migrate large mailboxes from on-premises Exchange to Microsoft 365 Exchange with retention policies | Microsoft Learn

## Introduction

This document provides comprehensive guidance for tenant administrators on migrating mailboxes from on-premises Exchange servers, to Microsoft 365 Primary and [Archive mailboxes](/en-us/purview/archive-mailboxes). Administrators will use a combination of retention policies and the autoexpanding archive feature to move mailboxes smoothly to Microsoft 365.

## What do you need to know before you begin?

Tenant admins moving large amounts of Exchange user data (such as email, calendar, and contacts), defined as more than 100 GB per user, from an on-premises Exchange Server environment into Microsoft 365 comes with the following important notes:

### Limitations

- The maximum size of a Microsoft 365 user's stored mailbox data is 1.5 TB. This size includes the primary mailbox, the main archive mailbox, and extra archive storage space from the autoexpanding archive feature. Storing more than 1.5 TB of data for a single Microsoft 365 user isn't supported. If the on-premises user has more than 1.5 TB of data, then this data has to be split across multiple Microsoft 365 mailboxes to be onboarded to Microsoft 365.
- Onboarding an on-premises archive of more than 240 GB to Microsoft 365 is not supported by this retention policy approach.
- [Deleted-item retention](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/change-deleted-item-retention) (also known as "single-item recovery") time in Microsoft 365 is 14 days, with a maximum of 30 days. When a mailbox is migrated to the cloud, items exceeding this time limit in mailboxes that aren't on hold are removed.

### Requirements

- Cloud archives must be provisioned for users in Microsoft 365 before migration.
- [Autoexpanding archive](/en-us/purview/enable-autoexpanding-archiving) must be enabled at the organization level, which enables the feature for all users who are migrated. Review the "considerations and limitations" and "Outlook requirements" sections in this article and "before you enable autoexpanding archiving" in the [Enable autoexpanding Archive](/en-us/purview/enable-autoexpanding-archiving) article.
- When a mailbox is on legal hold on-premises, administrators need to ensure that on-premises holds are synced to Microsoft 365 and that the target MailUser objects of users who are being migrated have the required hold state.

### Performance

Before beginning a migration of any mailbox, but particularly for large mailboxes, be familiar with the concepts and recommendations in the [Microsoft 365 email migration performance and best practices guide](/en-us/exchange/mailbox-migration/office-365-migration-best-practices).

Retention policies are used to relocate data when needed to reduce the size of primary mailboxes. Administrators need to include time required to plan retention policies and for those policies to relocate data to the cloud.

The following advice can be used to tune the quantity and interval of items processed by the Exchange Lifecycle service:

- To increase the number of items moved to the cloud archive during each run of the Exchange Lifecycle, or "ELC", process, set this registry value on every on-premises back-end Exchange server: SYSTEM\CurrentControlSet\Services\MSExchange MRM\Parameters\MoveToArchiveTotalCountLimit to 10000 and restart the MSExchangeAssistants service. (The default is 2000.)
- For priority or VIP mailboxes, tenant admins can choose to run the Start-ManagedFolderAssistant command no more often than once every hour. This action creates more ELC work runs that move up to 10,000 more items. Admins may also [change the ELC work cycle](/en-us/exchange/policy-and-compliance/mrm/configure-managed-folder-assistant) to process mailboxes every 8 hours. (This setting affects all mailboxes on the specified servers, which may have a performance impact, and the default is once per day.)

## Beginning the migration

Once an archive is provisioned in the cloud for a user who is being migrated, tenant admins use [retention policies to move content](/en-us/purview/retention-settings) into that cloud archive to reduce the size of the primary mailbox under 100 GB. Tenant admins must consult with their compliance or legal teams to determine company policies on length of time for retention of items in the primary mailbox.

When a recoverable item is moved to an archive, a user can't restore it using the "recover deleted item" feature in Outlook/OWA on the primary mailbox. Tenant admins need to set their retention policies for recoverable items to move only items older than [the deleted item retention setting](/en-us/exchange/recipients/user-mailboxes/deleted-item-retention-and-recoverable-items-quotas) on-premises so users keep using this feature as expected.

## Migrating users without an on-premises archive

### More than 100 GB but less than 240 GB of mailbox content

For users whose mailboxes don't have an on-premises archive and the mailbox is over 100 GB but less than 240 GB, follow these steps:

1. Create a retention policy that moves recoverable items from the user's on-premises mailbox to a **new** cloud archive where the autoexpanding feature is enabled.
2. If this action reduces the on-premises mailbox under 100 GB, perform a regular migration of the user's on-premises mailbox to the cloud. (If it doesn't, use retention policies to move items from the user's primary mailbox to the cloud archive to reduce the primary mailbox under 100 GB, then perform a regular migration.)

![A diagram reflecting the two steps. The left column is labeled on-premises primary mailbox. Under are two filled blue boxes, both surrounded by a blue outline. The top box reads regular items; the bottom box reads Recoverable Items Dumpster. On the right column, labeled Cloud, is a filled green box on top and a filled green cylinder on bottom, each with a New yellow star. The top reads primary mailbox. The bottom reads archive with autoexpanding. An orange left-to-right arrow labeled 1, connects the bottom-left blue box with the bottom-right green cylinder. A blue left-to-right arrow labeled 2, connects the top-left blue box with the top-right green box.](../exchangeonline/mailbox-migration/media/large-mailbox-steps-100-240.png)

### More than 240 GB of mailbox content

For users whose mailboxes don't have an on-premises archive and are over 240 GB, follow these steps:

1. Create a retention policy that moves recoverable items from the user's on-premises mailbox to a new cloud archive where the autoexpanding feature is enabled.
2. Use retention policies to move items from the user's primary mailbox to the cloud archive to reduce the primary mailbox under 100 GB.
3. Once the on-premises primary mailbox total size is under 100 GB, perform a regular migration of the user's primary mailbox to the cloud.

![A diagram reflecting the three steps. The left column is labeled on-premises primary mailbox. Under are two filled blue boxes, both surrounded by a blue outline. The top box reads regular items; the bottom box reads Recoverable Items Dumpster. On the right column, labeled Cloud, is a filled green box on top and a filled green cylinder on bottom, each with a New yellow star. The top reads primary mailbox. The bottom reads archive with autoexpanding. An orange left-to-right arrow labeled 1, connects the bottom-left blue box with the bottom-right green cylinder. A blue left-to-right arrow labeled 2, connects the top-left blue box with the bottom-right green cylinder. A purple left-to-right arrow labeled 3, connects the blue line surrounding both blue boxes to the top-right green box.](../exchangeonline/mailbox-migration/media/large-mailbox-steps-over-240.png)

## Users with an on-premises archive

### Primary mailbox more than 100 GB of content and archive less than 240 GB

**Reminder**: On-premises archive mailboxes larger than 240 GB **cannot** be migrated to Microsoft 365 using the retention policy approach.

For users whose mailboxes do have an on-premises archive and the primary mailbox is over 100 GB and the on-premises archive is under 240 GB, follow these steps:

1. Migrate the user's on-premises archive to the cloud, ensuring that autoexpanding is enabled.
2. Use retention policies to move all recoverable items from the primary mailbox to the user's cloud archive, along with enough regular items from the primary mailbox to reduce the primary mailbox size under 100 GB. Do this step once the archive migration is complete.
3. Once sufficient items are moved to the cloud archive, perform a regular migration of the user's primary mailbox to the cloud.

![A diagram reflecting the three steps. Three columns, left-to-right, read On-Premises Primary Mailbox, On-Premises Archive Mailbox, and Cloud. Under the farthest left column, two filled blue boxes are surrounded by a blue outline. The top blue box reads regular items. The bottom blue box reads recoverable items dumpster. Under the middle column, a filled blue cylinder reads archive. Under the farthest right column, a filled green box reads primary mailbox and a filled green cylinder reads archive with autoexpanding. Both are tagged with a star labeled New. A blue left-to-right arrow labeled 1, connects the middle Archive cylinder with the bottom-right Archive cylinder. Two orange left-to-right arrows, both labeled 2, connect both the regular items and recoverable items blue boxes from the furthest left column to the furthest right green cylinder. A purple left-to-right arrow labeled 3, connects the blue outline from the furthest left column to the filled green box in the furthest right column.](../exchangeonline/mailbox-migration/media/large-mailbox-steps-archive-over-100-and-240.png)