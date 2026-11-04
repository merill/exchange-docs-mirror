---
layout: Conceptual
title: Apply a sharing policy to mailboxes in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/sharing-policies/apply-a-sharing-policy
Manager: dansimp
ms.subservice: sharing
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
description: Sharing policies control how your users share their calendars with people outside your organization. The sharing policy that an admin applies to the user's mailbox determines what level of access a user can share and with whom. If you don't change anything, then all users can invite anyone with an email address to view their calendar. If you create a new sharing policy, you have to apply that policy to mailboxes before it takes effect. Sharing policies are applied to individual user's mailboxes. An admin can also disable a user's sharing policy to prevent external access to calendars.
ms.topic: how-to
author: navanethan-msft
ms.author: nagangat
ms.assetid: a075b1ec-5a96-4d0e-a609-ab64e50cdb9e
ms.reviewer: AkshayaPrakash-PM
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2025-09-25T00:00:00.0000000Z
locale: en-us
document_id: fee1853a-0d58-a418-048e-0bc3eb271ff7
document_version_independent_id: 45cc3da3-602f-2ea9-ee3a-38043b48ddf8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/sharing-policies/apply-a-sharing-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/sharing-policies/apply-a-sharing-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/sharing-policies/apply-a-sharing-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: b7008a15-0e8c-fabd-3b1f-c18548e37485
---

# Apply a sharing policy to mailboxes in Exchange Online | Microsoft Learn

Sharing policies control how your users share their calendars with people outside your organization. The sharing policy that an admin applies to the user's mailbox determines what level of access a user can share and with whom. If you don't change anything, then all users can invite anyone with an email address to view their calendar. If you create a new sharing policy, you have to apply that policy to mailboxes before it takes effect. Sharing policies are applied to individual user's mailboxes. An admin can also disable a user's sharing policy to prevent external access to calendars.

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the [Permissions in Exchange Online](../../permissions-exo/permissions-exo) article.
- A sharing policy must exist. For details, see [Create a sharing policy in Exchange Online](create-a-sharing-policy).

## Use the Exchange admin center to apply a sharing policy to one mailbox

1. In the Exchange admin center at https://admin.exchange.microsoft.com, go to **Recipients** &gt; **Mailboxes**. Or, to go directly to the **Manage mailboxes** page, use https://admin.exchange.microsoft.com/#/mailboxes.
2. On the **Manage mailboxes** page, select a mailbox by clicking anywhere in the row other than the round check box that appears next to the **Display name** column.
3. In the details flyout that opens, select the **Mailbox** tab.
4. On the **Mailbox** tab, select **Manage mailbox policies** in the **Mailbox policies** section.
5. On the **Mailbox policies** flyout that opens, select the **Sharing policy** you want to apply.
6. Select **Save** to apply the sharing policy.

## Use the Exchange admin center to apply a sharing policy to multiple mailboxes

1. In the Exchange admin center at https://admin.exchange.microsoft.com, go to **Recipients** &gt; **Mailboxes**. Or, to go directly to the **Manage mailboxes** page, use https://admin.exchange.microsoft.com/#/mailboxes.
2. On the **Manage mailboxes** page, hover over an entry in the list so the round check box that appears next to the **Display name** column, and then select the round check box.

    - To select a continuous range of mailboxes, press the Shift key and select the round check box of another mailbox farther down the list.
    - To select separated mailboxes, press and hold the CTRL key as you select the round check box of each mailbox.
3. Select the **Mailbox policies** action that appears.
4. On the **Mailbox policies** flyout that opens, select the **Sharing policy** you want to apply.
5. Select **Save** to apply the sharing policy.

## Use Exchange Online PowerShell to apply a sharing policy to one or more mailboxes

This example applies the sharing policy Contoso to Barbara's mailbox.

```powershell
Set-Mailbox -Identity Barbara -SharingPolicy "Contoso"
```

This example finds all user mailboxes in the Marketing department and then applies the sharing policy named Contoso Marketing.

```powershell
$Marketing = Get-Mailbox -ResultSize unlimited -Filter "Department -eq 'Marketing'"

$Marketing | foreach {Set-Mailbox -Identity $_.Identity -SharingPolicy "Contoso Marketing"}
```

For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox) and [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox).

## How do you know these procedures worked?

To verify you successfully applied the sharing policy to a user mailbox, do one of the following procedures:

- **Exchange admin center**:

    1. On the **Manage mailboxes** page at https://admin.exchange.microsoft.com/#/mailboxes, select the mailbox by clicking anywhere in the row other than the round check box that appears next to the **Display name** column.
    2. In the details flyout that opens, select the **Mailbox** tab.
    3. On the **Mailbox** tab, verify the **Sharing policy** value in the **Mailbox policies** section.
- **Exchange Online PowerShell**:

    - **Individual mailbox**: Replace &lt;MailboxIdentity&gt; with the name, alias, email address or account of the mailbox, and then run the following command and verify the *SharingPolicy* property value:

        ```powershell
        Get-Mailbox -Identity "<MailboxIdentity>" | Format-List Name,SharingPolicy
        ```
    - **Specific mailboxes**:

        ```powershell
        Get-Mailbox -ResultSize unlimited -Filter "Department -eq 'Marketing'" | Format-Table Name,SharingPolicy
        ```
    - **All user mailboxes**:

        ```powershell
        Get-Mailbox -ResultSize Unlimited -RecipientTypeDetails UserMailbox | Format-Table Name,SharingPolicy
        ```
    - **Show all mailboxes with a specific sharing policy applied**: Replace &lt;SharingPolicy&gt; with the name of the sharing policy, and then run the following command:

        ```powershell
        Get-Mailbox -ResultSize unlimited | where {$_.SharingPolicy -eq "<SharingPolicy>"} | Format-Table Alias,EmailAddresses
        ```