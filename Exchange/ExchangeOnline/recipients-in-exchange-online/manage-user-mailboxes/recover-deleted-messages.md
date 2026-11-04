---
layout: Conceptual
title: Recover deleted messages in a user's mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/recover-deleted-messages
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
description: Administrators can search for and recover deleted email messages in a user's mailbox.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 9e0e34ce-efc5-454e-8d15-57b4da867f12
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
document_id: 496c2124-3973-e6d1-385e-4ec25228dc49
document_version_independent_id: cd70012a-5cdf-bac5-3a29-df38b19df1cb
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/recover-deleted-messages.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-user-mailboxes/recover-deleted-messages
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/recover-deleted-messages.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: daca8870-8d43-73be-077c-cd61f42cc30d
---

# Recover deleted messages in a user's mailbox in Exchange Online | Microsoft Learn

Administrators can search for and recover deleted email messages in a user's mailbox. This includes items that are permanently deleted (purged) by a person (by using the Recover Deleted Items feature in Outlook or Outlook on the web (formerly known as Outlook Web App)), or items deleted by an automated process, such as the retention policy assigned to user mailboxes. In these situations, the purged items can't be recovered by a user. But administrators can recover purged messages if the deleted item retention period for the item hasn't expired.

Note

In addition to using this procedure to search for and recover deleted items (which are moved to the Recoverable Items\Purges folder if either single item recovery or litigation hold is enabled), you can also use this procedure to search for items residing in other folders in the mailbox and to delete items from the source mailbox.

## What you need to know before you begin?

- Estimated time to complete: 15-30 minutes.
- Procedures in this article require specific permissions. See each procedure for its permissions information.
- Single item recovery must be enabled for a mailbox before the item you want to recover is deleted. In Exchange Online, single item recovery is enabled by default when a new mailbox is created. In Exchange Server, single item recovery is disabled when a mailbox is created. For more information, see [Enable or disable single item recovery for a mailbox](enable-or-disable-single-item-recovery).
- To search for and recover items, you must have the following information:

    - **Source mailbox**: This is the mailbox being searched.
    - **Search criteria**: Criteria include sender or recipient, or keywords (words or phrases) in the message.
- You need the *Mailbox Import Export* RBAC role before you can do this procedure or procedures.

## Use EAC for recovering deleted messages

1. In the EAC, navigate to **Recipients &gt; Mailboxes**.
2. Select the mailbox for which you want to recover deleted messages.
3. Under **Others** &gt; **Recover deleted items**, select the link **Recover deleted items**.
4. Use the filters available to locate the messages you want to recover, and then select **Apply filter**.
5. Select the messages you want to recover, and then click **Recover deleted items**.

## Using PowerShell to manage deleted items

### Step 1: Connect to Exchange Online PowerShell

For instructions, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

### Step 2: Search for and recover missing items

This example returns all of the available recoverable deleted messages with the specified subject in the mailbox laura@contoso.com for the specified date/time range.

```PowerShell
Get-RecoverableItems -Identity laura@contoso.com -SubjectContains "FY17 Accounting" -FilterItemType IPM.Note -FilterStartTime "2/1/2018 12:00:00 AM" -FilterEndTime "2/5/2018 11:59:59 PM"
```

For detailed syntax and parameter information, see [Get-RecoverableItems](/en-us/powershell/module/exchangepowershell/get-recoverableitems?).

### Step 3: Restore recovered items

Once you have finalized the filters for the messages you want to recover, you can restore them to the user's mailbox by using the **Restore-RecoverableItems** cmdlet.

```PowerShell
Restore-RecoverableItems -Identity "malik@contoso.com","lillian@contoso.com" -FilterItemType IPM.Note -SubjectContains "Fiscal Year Review" -FilterStartTime "3/15/2019 12:00:00 AM" -FilterEndTime "3/25/2019 11:59:59 PM" -MaxParallelSize 2
```

After using the Get-RecoverableItems cmdlet to verify the existence of the item, this example restores the specified deleted items in the specified mailboxes:

Mailboxes: malik@contoso.com, lillian@contoso.com

Item type: Email message

Message subject: Fiscal Year Review

Location: Recoverable Items\Deletions

Date range: 3/15/2019 to 3/25/2019

Number of mailboxes processed simultaneously: 2

For detailed syntax and parameter information, see [Restore-RecoverableItems](/en-us/powershell/module/exchangepowershell/restore-recoverableitems?).

## More information

Users can recover a deleted item if it hasn't been purged and if the deleted item retention period for that item hasn't expired. If users need to recover deleted items from the Recoverable Items folder, point them to the following articles:

- [Recover deleted items in Outlook for Windows](https://support.microsoft.com/office/49e81f3c-c8f4-4426-a0b9-c0fd751d48ce)
- [Recover deleted email messages in Outlook on the web](https://support.microsoft.com/office/a8ca78ac-4721-4066-95dd-571842e9fb11)