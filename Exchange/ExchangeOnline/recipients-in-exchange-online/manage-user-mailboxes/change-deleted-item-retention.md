---
layout: Conceptual
title: Change how long permanently deleted items are kept for an Exchange Online mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/change-deleted-item-retention
Manager: serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn how to use Exchange Online PowerShell to change the deleted item retention period for Exchange Online mailboxes.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: ce17f1ec-b96c-4c9e-b20a-507fe0afc684
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-30T00:00:00.0000000Z
locale: en-us
document_id: 10a43744-eddc-762f-d3c7-6f8732141ad7
document_version_independent_id: c20377ab-03ae-62ed-96bd-04a9bc653286
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/change-deleted-item-retention.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-user-mailboxes/change-deleted-item-retention
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/change-deleted-item-retention.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 091b930e-ccde-54c5-06f9-7837fe04970c
---

# Change how long permanently deleted items are kept for an Exchange Online mailbox in Exchange Online | Microsoft Learn

If you've *permanently* deleted an item in Microsoft Outlook or Outlook on the web (formerly known as Outlook Web App), the item is moved to a folder (**Recoverable Items** &gt; **Deletions**) and kept there for 14 days, by default. You can change how long items are kept, up to a maximum of 30 days.

## What do you need to know before you begin?

- Estimated time to complete each procedure: 3 minutes.
- If you place a mailbox on litigation hold, the retention limit is ignored. For more information, see [In-Place Hold and Litigation Hold](../../security-and-compliance/in-place-and-litigation-holds).
- You need permissions before you can do this procedure or procedures. To see what permissions you need, see the "Recipients" section in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- You can use Exchange Online PowerShell to perform this procedure. To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Change how long permanently deleted items are kept

In these examples, we increase the retention period to 30 days, the maximum for Exchange Online mailboxes. But you can set the number to whatever you like, up to that limit.

**Example 1:** Set Emily Maier's mailbox to keep deleted items for 30 days. In Exchange Online PowerShell, run the following command.

```PowerShell
Set-Mailbox -Identity "Emily Maier" -RetainDeletedItemsFor 30
```

**Example 2:** Set all user mailboxes in the organization to keep deleted items for 30 days. In Exchange Online PowerShell, run the following command.

```PowerShell
Get-Mailbox -ResultSize unlimited -Filter "RecipientTypeDetails -eq 'UserMailbox'" | Set-Mailbox -RetainDeletedItemsFor 30
```

Need more details about using these commands? See Exchange Online PowerShell Help article [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).

Note

These commands only apply to existing mailboxes and will not affect new mailboxes that you create in the future. To change this setting on all new mailboxes, use a mailbox plan that has a new retention policy that applies to new mailboxes. See [Mailbox plans](mailbox-plans) and [Set-MailboxPlan](/en-us/powershell/module/exchangepowershell/set-mailboxplan) for more information.

## More about deleted items and retention time

When a user permanently deletes a mailbox item (such as an email message, a contact, a calendar appointment, or a task) in Microsoft Outlook and Outlook on the web, the item is moved to the **Recoverable Items** folder, and into a subfolder named **Deletions**.

A mailbox item is deleted and moved to the **Recoverable Items** folder when a user does one of the following:

- Deletes an item from the Deleted Items folder
- Empties the Deleted Items folder
- Permanently deletes an item by selecting it and pressing **Shift+Delete**

Users can recover, or purge, deleted items before the retention time for a deleted item expires. To do so, they use the **Recover Deleted Items** feature in Outlook or Outlook on the web. See the following articles for [Outlook for Windows](https://support.microsoft.com/office/49e81f3c-c8f4-4426-a0b9-c0fd751d48ce) or for [Outlook on the web](https://support.microsoft.com/office/a8ca78ac-4721-4066-95dd-571842e9fb11).

To learn more about deleted item retention, the Recoverable Items folder, In-Place Hold, and Litigation Hold, see [Recoverable Items folder in Exchange Online](../../security-and-compliance/recoverable-items-folder/recoverable-items-folder).