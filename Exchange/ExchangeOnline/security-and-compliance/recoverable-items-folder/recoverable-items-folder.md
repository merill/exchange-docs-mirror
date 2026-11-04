---
layout: Conceptual
title: Recoverable Items folder in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/recoverable-items-folder/recoverable-items-folder
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ai-usage: ai-assisted
description: 'Summary: Admins can learn how deleted items in mailboxes are protected in Exchange Online.'
ms.topic: article
author: AshaIyengar21
ms.author: srvar
ms.assetid: efc48fb4-2ed8-4d05-93af-f3505fbc389d
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-server-it-pro
ms.date: 2026-09-25T00:00:00.0000000Z
locale: en-us
document_id: 6fbbc82b-b1c8-f2b7-9f57-9fa9137305a3
document_version_independent_id: f1ce321a-ed5e-fe57-450d-35cc7b104350
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/recoverable-items-folder/recoverable-items-folder.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/recoverable-items-folder/recoverable-items-folder
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/recoverable-items-folder/recoverable-items-folder.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 94d235f6-f0a6-ca53-8527-563d4739ef46
---

# Recoverable Items folder in Exchange Online | Microsoft Learn

Important

Refer to the [Microsoft 365 security center](https://security.microsoft.com/homepage) and the [Microsoft Purview compliance portal](https://compliance.microsoft.com/homepage) for Exchange security and compliance features. They are no longer available in the new [Exchange admin center](https://admin.exchange.microsoft.com).

To protect from accidental or malicious deletion and to facilitate discovery efforts commonly undertaken before or during litigation or investigations, Exchange Online uses the Recoverable Items folder. The Recoverable Items folder replaces the feature that was known as *the dumpster* in earlier versions of Exchange. The following Exchange features use the Recoverable Items folder:

- Deleted item retention
- Single item recovery
- In-Place Hold
- Litigation Hold
- eDiscovery hold
- Microsoft 365 and Office 365 retention policies
- Mailbox audit logging
- Calendar logging

## Terminology

Knowledge of the following terms will help you understand the content in this article.

**Delete**: Describes when an item is deleted from any folder and placed in the Deleted Items default folder.

**Soft delete**: Describes when an item is deleted from the Deleted Items default folder and placed in the Recoverable Items folder. Also describes when an Outlook user deletes an item by pressing Shift+Delete, which bypasses the Deleted Items folder and places the item directly in the Recoverable Items folder.

**Hard delete**: Describes when an item is marked to be purged from the mailbox database. This is also known as a *store hard delete*.

## Recoverable Items folder

Each user mailbox is divided into two subtrees: the IPM (interpersonal messaging) subtree, which contains the normal, visible folders such as Inbox, Calendar, and Sent Items; and the non-IPM subtree, which contains internal data, preferences, and other operational data about the mailbox. The Recoverable Items folder resides in the non-IPM subtree of each mailbox. This subtree isn't visible to users using Outlook, Outlook on the web (formerly known as Outlook Web App), or other email clients.

This architectural change provides the following key benefits:

- When a mailbox is moved to another mailbox database, the Recoverable Items folder moves with it.
- The Recoverable Items folder is indexed by Exchange Search and can be discovered by using In-Place eDiscovery or Content Search in the Microsoft Purview compliance portals.
- The Recoverable Items folder has its own storage quota.
- Exchange can prevent data from being purged from the Recoverable Items folder.
- Exchange can track edits of certain content.

The Recoverable Items folder contains the following subfolders:

- **Deletions**: This subfolder contains all items deleted from the Deleted Items folder. (In Outlook, a user can soft delete an item by pressing Shift+Delete.) This subfolder is available to users through the Recover Deleted Items feature in Outlook and Outlook on the web.
- **Versions**: If In-Place Hold, Litigation Hold, or a Microsoft 365 or Office 365 retention policy is enabled, this subfolder contains the original copy of the item; and also, if the item is modified multiple times, a copy of the item before modification is saved. To understand what action is considered as modification, refer the Copy-on-Write section later in this article. This folder isn't visible to end users.
- **Purges**: If either Litigation Hold or single item recovery is enabled, this subfolder contains all items that are hard deleted. This folder isn't visible to end users.
- **Audits**: If mailbox audit logging is enabled for a mailbox, this subfolder contains the audit log entries. To learn more about mailbox audit logging, see [Export mailbox audit logs in Exchange Online](../exchange-auditing-reports/export-mailbox-audit-logs).
- **DiscoveryHolds**: If In-Place Hold is enabled or if a Microsoft 365 or Office 365 retention policy is assigned to the mailbox, this subfolder contains all items that meet the hold query parameters and are hard deleted.
- **Calendar Logging**: This subfolder contains calendar changes that occur within a mailbox. This folder isn't available to users.
- **SubstrateHolds**: If In-Place Hold, Litigation Hold, or a Microsoft 365 or Office 365 Teams Chat retention policy is enabled, this subfolder contains the original copy of the Teams message if the message has been modified or deleted. A copy of the item before modification is saved. This folder isn't visible to end users.

The following illustration shows the subfolders in the Recoverable Items folders. It also shows the deleted item retention, single item recovery, and hold workflow processes that are described in the following sections.

![Recoverable Items folder.](../../exchangeonline/media/itpro_recoverableitems.gif)

### Deleted item retention

An item is considered to be soft deleted in the following cases:

- A user deletes an item or empties all items from the Deleted Items folder.
- A user presses Shift+Delete to delete an item from any other mailbox folder.

Soft-deleted items are moved to the Deletions subfolder of the Recoverable Items folder. This provides an additional layer of protection so users can recover deleted items without requiring Help desk intervention. Users can use the Recover Deleted Items feature in Outlook or Outlook on the web to recover a deleted item. Users can also use this feature to permanently delete an item. For more information, see:

- [Recover deleted items in Outlook for Windows](https://support.microsoft.com/office/49e81f3c-c8f4-4426-a0b9-c0fd751d48ce)
- [Recover deleted items or email messages in Outlook on the web](https://support.microsoft.com/office/cf06ab1b-ae0b-418c-a4d9-4e895f83ed50)

Items remain in the Deletions subfolder until the deleted item retention period is reached. The default deleted item retention period for Exchange Online is 14 days. You can modify this period for mailboxes up to a maximum of 30 days. In addition to a deleted item retention period, the Recoverable Items folder is also subject to quotas. To learn more, see Recoverable Items mailbox quotas later in this article.

When the deleted item retention period expires, the item is removed from Exchange Online.

Note

If a user presses Shift-Delete on a folder inside their mailbox, or deletes a folder that is located inside Deleted Items, the folder will be hard deleted (the folder(s) can't be recovered even if the mailbox is placed on litigation hold or in-place hold), while its contents will move under Recoverable Items\Deletions where they can be recovered for up to 14 days by default. This applies only to user-created folders, not to the default folders which exist in the mailbox at the moment of its creation (Inbox, Sent Items, Drafts, Deleted Items, Junk Email, Archive, Outbox, and so on).

### Single item recovery

If an item is removed from the Deletions subfolder, either by a user purging the item by using the Recover Deleted Items feature or by an automated process such as the Managed Folder Assistant (retention tag set to permanently delete, for example), the item is moved to the Purges subfolder, and it can't be recovered by the user. When the Managed Folder Assistant processes the Recoverable Items folder for a mailbox that has single item recovery enabled, any item in the Purges subfolder isn't purged if the deleted item retention period hasn't expired for that item. This means that an admin can still recover the item by using an eDiscovery tool such as In-Place eDiscovery or Content Search.

The following table lists the contents of and actions that can be performed in the Recoverable Items folder if single item recovery is enabled.

| State of single item recovery | Recoverable Items folder contains soft-deleted items | Recoverable Items folder contains hard-deleted items | Users can purge items from the Recoverable Items folder | Managed Folder Assistant automatically purges items from the Recoverable Items folder |
| --- | --- | --- | --- | --- |
| Enabled | Yes | Yes | No | Yes. By default, all items are purged after 14 days, except for calendar items, which are purged after 120 days. If the Recoverable Items warning quota is reached before the deleted item retention period elapses, messages are deleted in first in, first out (FIFO) order. |
| Disabled | Yes | No | Yes | Yes. By default, all items are purged after 14 days, except for calendar items, which are purged after 120 days. If the Recoverable Items warning quota is reached before the deleted item retention period elapses, messages are deleted in first in, first out (FIFO) order. |

### In-Place Hold and Litigation Hold

In Exchange Online, discovery managers can use In-Place eDiscovery with delegated [Discovery Management](../../permissions-exo/permissions-exo#role-groups-in-exchange-online) role group permissions to perform eDiscovery searches of mailbox content. In Exchange Online, you can use In-Place Hold to preserve mailbox items that match query parameters and protect the items from deletion by users or automated processes. You can also use Litigation Hold to preserve all items in user mailboxes and protect the items from deletion by users or automated processes.

Putting a mailbox on In-Place Hold or Litigation Hold stops the Managed Folder Assistant from automatically purging messages from the DiscoveryHolds, Deletions, and Purges subfolders. Additionally, copy-on-write page protection is also enabled for the mailbox. Copy-on-write page protection creates a copy of the original item before any modifications are written to the Exchange store. After the mailbox is removed from hold, the Managed Folder Assistant resumes automated purging.

Note

If you put a mailbox on both In-Place Hold and Litigation Hold, Litigation Hold takes preference because this puts the entire mailbox on hold.

The following table lists the contents of and actions that can be performed in the Recoverable Items folder if Litigation Hold is enabled.

| State of hold | Recoverable Items folder contains soft-deleted items | Recoverable Items folder contains modified and hard-deleted items | Users can purge items from the Recoverable Items folder | Managed Folder Assistant automatically purges items from the Recoverable Items folder |
| --- | --- | --- | --- | --- |
| Enabled | Yes | Yes | No | No |
| Disabled | Yes | No | Yes | Yes |

To learn more about In-Place eDiscovery, In-Place Hold, and Litigation Hold, see the following articles:

- [In-Place eDiscovery in Exchange Online](../in-place-ediscovery/in-place-ediscovery)
- [In-Place Hold and Litigation Hold in Exchange Online](../in-place-and-litigation-holds)

### Copy-on-write page protection and modified items

If a user who is placed on In-Place Hold or Litigation Hold modifies specific properties of a mailbox item, a copy of the original mailbox item is created before the changed item is written. The original copy is saved in the Versions subfolder. This process is known as *copy-on-write page protection*. Copy-on-write page protection applies to items residing in any mailbox folder. The Versions subfolder isn't visible to users.

The following table lists the message properties that trigger copy-on-write page protection.

| Item type | Properties that trigger copy-on-write page protection |
| --- | --- |
| Messages (IPM.Note\*)  Posts (IPM.Post\*) | Subject  Body  Attachments  Senders and recipients  Sent and received dates |
| Items other than messages and posts | Any change to a visible property, except the following: <br>- Item location (when an item is moved between folders)<br>- Item status change (read or unread)<br>- Changes to a retention tag applied to an item |
| Items in the Drafts default folder | None. Items in the Drafts folder are exempt from copy-on-write page protection. |

Important

Copy-on-write page protection doesn't save a version of the meeting when a meeting organizer receives responses from attendees and the meeting's tracking information is updated. Also, changes to RSS feeds aren't captured by copy-on-write page protection.

When a mailbox is no longer on In-Place Hold or Litigation Hold, copies of modified items stored in the Versions folder are removed.

## Recoverable Items mailbox quotas

When an item is moved to the Recoverable Items folder, its size is deducted from the mailbox quota and added to the size of the Recoverable Items folder (quota available is reduced). In Exchange Online, the default limits for the Recoverable Items quota are: a soft limit of 20 GB and a hard limit of 30 GB. However, the quotas for the Recoverable Items folder are automatically increased to 90 GB and 100 GB, respectively, when you place a mailbox on Litigation Hold or In-Place Hold or if a Microsoft 365 or Office 365 retention policy is applied to the mailbox. For more information, see [Increase the Recoverable Items quota for mailboxes on hold](/en-us/purview/ediscovery-increase-the-recoverable-quota-for-mailboxes-on-hold).

Important

When you analyze the size of the Recoverable Items folder, be aware that the following folders under `DiscoveryHolds` are internal search-processing folders used by the Managed Folder Assistant:

- `DiscoveryHolds/SearchDiscoveryHoldsItemFolder`
- `DiscoveryHolds/SearchDiscoveryHoldsUnindexedItemFolder`

These folders don't store recoverable mailbox content and don't count toward mailbox or Recoverable Items quotas. You can verify this behavior by using `Get-MailboxFolderStatistics`, where these folders show `TargetQuota: None`.

The size reported for these folders represents the volume of data that the Managed Folder Assistant processed. It doesn't indicate that the corresponding data still exists in the mailbox. When you evaluate Recoverable Items folder consumption, use the `FolderSize` value for each Recoverable Items folder returned by `Get-MailboxFolderStatistics`. Don't rely on `FolderAndSubfolderSize`, because it can include internal search-processing folders that don't count toward mailbox quotas.

The Managed Folder Assistant recreates these search-processing folders as needed when Recoverable Items content matches processing criteria. As a result, a reported folder size can persist independently of the recoverable content currently in the mailbox.

If the Recoverable Items folder for a mailbox reaches the Recoverable Items quota, no more items can be stored in the folder. This impacts mailbox functionality in the following ways:

- Mailbox users can't delete items.
- The Managed Folder Assistant can't delete items based on retention tag or managed folder settings.
- For mailboxes that have single item recovery, In-Place Hold, or Litigation Hold enabled, the copy-on-write page protection process can't maintain versions of items edited by the user.
- For mailboxes that have mailbox audit logging enabled, no mailbox audit log entries can be saved in the Audits subfolder.

For mailboxes that aren't placed on In-Place Hold or Litigation Hold, the Managed Folder Assistant automatically purges items from the Recoverable Items folder when the deleted item retention period expires. If the folder reaches the Recoverable Items warning quota, the Managed Folder Assistant automatically purges items in FIFO order.

If the mailbox is placed on In-Place Hold or Litigation Hold or assigned to a Microsoft 365 or Office 365 retention policy, copy-on-write page protection can't maintain versions of modified items. To maintain versions of modified items, you need to reduce the size of the Recoverable Items folder. For more information, see [Delete items in the Recoverable Items folder of cloud-based mailboxes on hold](/en-us/purview/ediscovery-delete-items-in-the-recoverable-items-folder-of-mailboxes-on-hold).

Note

When archiving is enabled for a specific user whose mailbox is on hold or assigned to a retention policy, the storage quota for the user's primary mailbox's Recoverable Items folder is raised from 100 GB to 105 GB and Recoverable Items warning quota is raised from 90 GB to 95 GB. This additional space supports an efficient archiving experience for users, even if auto-expanding archive isn't enabled.

## More information

- Copy-on-write is only enabled when a mailbox is on In-Place Hold or Litigation Hold.
- If users need to recover deleted items from the Recoverable Items folder, point them to the following articles:

    - [Recover deleted items in Outlook for Windows](https://support.microsoft.com/office/49e81f3c-c8f4-4426-a0b9-c0fd751d48ce)
    - [Recover deleted items or email in Outlook on the web](https://support.microsoft.com/office/98b5a90d-4e38-415d-a030-f09a4cd28207)
- If you need to change the default deleted item retention period for Exchange Online, read the following article:

    - [Change how long permanently deleted items are kept for an Exchange Online mailbox](../../recipients-in-exchange-online/manage-user-mailboxes/change-deleted-item-retention)