---
layout: Conceptual
title: Microsoft 365 Exchange data deletion | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/data-deletion
Manager: robertoyms
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how soft and hard data deletions for mailboxes and items within mailboxes are handled in Exchange Online.
author: brenle
ms.author: brenle
ms.reviewer: 
audience: ITPro
ms.topic: reference
ms.service: exchange-online
search.appverid:
- MET150
ms.collection:
- MS-Compliance
- MS-Compliance-Assurance
- MCAT
f1.keywords:
- NOCSH
ms.date: 2026-05-28T00:00:00.0000000Z
locale: en-us
document_id: eb62f01c-58b7-e5b2-4f06-d08be0c92cd6
document_version_independent_id: 8636e3e2-3106-1446-8d82-17be4f790b6a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/data-deletion.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/data-deletion
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/data-deletion.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 45fe5ac3-4b11-49aa-af30-3414a4240bac
---

# Microsoft 365 Exchange data deletion | Microsoft Learn

Within Exchange, two kinds of deletion exist: soft deletion and hard deletion. This distinction applies to both mailboxes and items within a mailbox.

## Soft-deleted and hard-deleted mailboxes

A soft-deleted user mailbox is one that you delete by using the Microsoft 365 admin center or the Remove-Mailbox cmdlet. The mailbox is still in the Microsoft Entra ID recycle bin and has been there for less than 30 days. A mailbox can become soft-deleted in any of the following ways:

- You soft-delete the user mailbox's associated Microsoft Entra user account (the user object is out of scope or in the recycle bin container).
- You hard-delete the user mailbox's associated Microsoft Entra user account but the Exchange mailbox is under a litigation hold or eDiscovery hold.
- You purge the user mailbox's associated Microsoft Entra user account within the last 30 days; which is the maximum retention length Exchange keeps the mailbox in a soft-deleted state before it's permanently purged and unrecoverable.

A hard-deleted user mailbox is a mailbox that you delete in one of the following ways:

- You soft-delete the user mailbox for more than 30 days, and you hard-delete the associated Microsoft Entra user. All mailbox content such as emails, contacts, and files are permanently deleted.
- You hard-delete the user account associated with the user mailbox from the Microsoft Entra ID. The user mailbox is now soft-deleted in Exchange Online and stays in a soft-deleted state for 30 days. If in the 30-day period a new Microsoft Entra user is synchronized from the original recipient account with the same **ExchangeGuid** or **ArchiveGuid**, and that new account is licensed for Exchange, this action results in a hard deletion of the original user mailbox. All mailbox content such as emails, contacts, and files are permanently deleted.
- You delete a soft-deleted mailbox by using **Remove-Mailbox -PermanentlyDelete**.

The preceding deletion scenarios assume that the user mailbox isn't in any of the hold states, like Litigation or eDiscovery hold. If there's any type of hold on the mailbox, then you can't delete the mailbox. For all mail-user recipient types, any [Hold](https://support.office.com/article/manage-legal-investigations-in-office-365-2e5fbe9f-ee4d-4178-8ff8-4356bc1b168e?ui=en-US&amp;rs=en-US&amp;ad=US) settings are ignored and have no effect on hard-deletions or soft-deletions.

## Soft-deleted and hard-deleted items

When a user deletes a mailbox item (such as an email message, a contact, a calendar appointment, or a task), the item moves to the Recoverable Items folder, and into a subfolder named "Deletions". This action is a soft deletion. How long deleted items stay in the Deletions folder depends on the deleted item retention period that is set for the mailbox. An Exchange mailbox keeps deleted items for 14 days by default, but Exchange administrators can change this setting to increase the period up to a maximum of 30 days. (For detailed steps to increase the deleted item retention period for an Exchange mailbox, see [Change how long permanently deleted items are kept for an Exchange mailbox](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/change-deleted-item-retention).) Users can recover or purge deleted items before the retention time for a deleted item expires. To do so, they use the Recover Deleted Items feature in Microsoft Outlook or Outlook on the web.

If a user purges a deleted item by using the Recover Deleted Items feature in Outlook or Outlook on the web, this action is a hard deletion. In Exchange, single item recovery is enabled by default when you create a new mailbox, so an administrator can still [recover](/en-us/Exchange/recipients/user-mailboxes/recover-deleted-messages) hard-deleted items before the deleted item retention period expires. Also, if a message is changed by a user or a process, copies of the original item are also retained when single item recovery is enabled.

## Page zeroing

*Zeroing* is a security mechanism that writes either zeros or a binary pattern over deleted data so that the deleted data is more difficult to recover. In Exchange, mailbox databases use *pages* as their unit of storage, and implement an overwriting process called *page zeroing*. Page zeroing is enabled by default, and you can't disable it. The transaction log files record page zeroing operations so that all copies of a given database zero pages in a similar manner. Zeroing a page on an active database copy causes the page to get zeroed on passive copies of the database.

Page zeroing writes a binary pattern over hard-deleted records. The page-zeroing pattern is specific to Extensible Storage Engine (ESE) operations (the name of the internal database engine used by servers in Exchange), and it's different for run-time operations versus background database maintenance operations. (Background database maintenance is a process that continuously checksums and scans each database. Its primary function is to checksum database pages, but it also handles cleaning up space and zeroing out records and pages that weren't zeroed out because of a Store crash.)

The following table lists the fill patterns that correspond to specific run-time operations.

| ESE run-time operation | Fill pattern |
| --- | --- |
| Replace | R |
| Record/long value delete | D |
| Freed page space | H |

The following table lists the fill patterns that correspond to specific operations that occur during ESE background database maintenance.

| ESE background database maintenance operation | Fill pattern |
| --- | --- |
| Record delete | D |
| Long value delete | L |
| Freed page space of partially used page | Z |
| Freed page space of unused page | U |

### Page zeroing process

The process for page zeroing depends on the deletion scenario. The following table describes database delete scenarios and when page zeroing functions occur.

| Database delete scenario | ESE process and timeframe to zero database data |
| --- | --- |
| Item expires based on the deleted item retention period. | An asynchronous thread writes a binary pattern over the deleted data. This action occurs within milliseconds of the record deletion. If the Store process crashes while the asynchronous zeroing work is still outstanding (or version store cleanup is canceled due to version store growth), the zeroing process finishes when background database maintenance processes that section of the database. |
| View scenario: Expiration of items from Outlook/Outlook on the web folder view (for example, Conversation view) | Data zeroing occurs when background database maintenance processes that section of the database. |
| Move Mailbox/Delete Mailbox scenario: Source mailbox deleted (expiry of deleted mailbox) | Data zeroing occurs when background database maintenance processes that section of the database. |

### Mailbox data types without page zeroing

The following mailbox data types don't have provisions for page zeroing:

- **Mailbox database transaction logs** - When transaction logs are deleted as part of normal operations, there's no process to zero the blocks in the file system that stored the deleted log files. The file system likely quickly reuses that free space for newly created logs, but there's no guarantee that this happens.
- **Content index catalog files** - Exchange uses Search Foundation (also known as FAST) for search indexing functionality. The search index catalog is composed of several dozen files stored on the same volume as the mailbox database file. When a message is hard-deleted from the mailbox database, the associated content in the search catalog isn't immediately deleted. Content deletion occurs when Search Foundation does a shadow (or master merge) of many small catalog files into a single larger file. After the master merge completes, the smaller catalog files are deleted. There's no process to zero the blocks that stored the deleted catalog files.

## Continuous replication

Continuous replication (also known as log shipping and replay) is technology in Exchange that creates and maintains copies of every mailbox database to provide high availability, site resilience, and disaster recovery. Continuous replication uses the Exchange Server database crash recovery support to provide technology that performs asynchronous updating of one or more copies of a mailbox database. Each mailbox server records database updates made on an active database (for example, user email activity) as log records in a sequential set of 1-MB transaction log files. This set of files is referred to as the log stream. In continuous replication, the log stream is also used to asynchronously update one or more copies of a database. This process transmits the logs to a location containing a passive copy of the active database and then replays them into the passive database copy. If all logs from the active database are replayed against a passive copy of the database, then the two databases are equivalent. Through this process, any physical change made to an active database is replicated to all passive copies of that database.

Any deletion from a mailbox database, whether a mailbox item or an entire mailbox, and whether a soft-delete or a hard-delete, represents a physical change to the active database. Page zeroing also entails making physical changes to the active database. These changes are written to the log files through a process called continuous replication, and when those log files are replayed against passive copies of the database, the same physical changes are made to those passive databases.