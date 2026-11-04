---
layout: Conceptual
title: Convert a mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/convert-a-mailbox
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
ms.custom:
- has-azure-ad-ps-ref
description: Converting a mailbox to a different type of mailbox is very similar to the experience in earlier versions of Exchange. You must still use the Set-Mailbox cmdlet in Exchange Online PowerShell to do the conversion.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: dfed045e-a740-4a90-aff9-c58d53592f79
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
document_id: 5b06ba52-118b-9ebd-a997-65b77f54b651
document_version_independent_id: b6fa9cac-7ae7-a99e-1100-e22552ad7596
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/convert-a-mailbox.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-user-mailboxes/convert-a-mailbox
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/convert-a-mailbox.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: cb5819ef-99bd-d6a1-4e35-d97738113520
---

# Convert a mailbox in Exchange Online | Microsoft Learn

You can use the Exchange admin center (EAC) for the following types of mailbox conversions:

- User mailbox to shared mailbox.
- Shared mailbox to user mailbox.

Other types of mailbox conversions require Exchange Online PowerShell:

- User mailbox to resource (room or equipment) mailbox
- Shared mailbox to resource mailbox
- Resource mailbox to user mailbox
- Resource mailbox to shared mailbox

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- If your organization uses a hybrid Exchange environment, you need to manage your mailboxes using on-premises Exchange management tools.

    - To convert a mailbox in a hybrid environment that was provisioned in Exchange Online but not migrated, you need to convert the remote mailbox object using the Exchange Management Shell in on-premises Exchange:

        ```powershell
        Set-RemoteMailbox <MailboxIdentity> -Type <Regular | Shared | Room | Equipment>
        ```
    - If the mailbox was previously migrated to Exchange Online, you also need to update the mailbox object in Exchange Online. For more information, see:

        - Use the Exchange admin center to convert a mailbox
        - Use Exchange Online PowerShell to convert a mailbox

## Use the Exchange admin center to convert a mailbox

1. In the EAC, go to **Recipients &gt; Mailboxes**.
2. Select the mailbox that you want to convert.
3. From the **More actions** pane, click **Convert to regular mailbox** or **Convert to shared mailbox**.
4. In the pane that opens up, select **Confirm**.

    The mailbox is converted from its present type to its other type, and the notification message **Mailbox converted successfully is displayed**.

## Use Exchange Online PowerShell to convert a mailbox

To convert a mailbox, use the following syntax:

```PowerShell
Set-Mailbox -Identity <MailboxIdentity> -Type <Regular | Room | Equipment | Shared>
```

This example converts the shared mailbox named MarketingDept1 to a user mailbox.

```PowerShell
Set-Mailbox -Identity MarketingDept1 -Type Regular
```

For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).