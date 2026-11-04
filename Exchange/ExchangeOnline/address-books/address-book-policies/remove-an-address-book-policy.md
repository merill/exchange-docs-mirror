---
layout: Conceptual
title: Remove an address book policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-book-policies/remove-an-address-book-policy
Manager: serdars
ms.subservice: exo-address-books
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
description: Learn how to remove address book policies (ABPs) from Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 2f17cba3-8570-52e6-c0c5-bd4c0766ba9b
document_version_independent_id: 7956828d-ed52-e5b1-fd37-73a4e551ba0d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-book-policies/remove-an-address-book-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-book-policies/remove-an-address-book-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-book-policies/remove-an-address-book-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 1d16aa11-f971-60d5-5b61-46f1be415ca9
---

# Remove an address book policy in Exchange Online | Microsoft Learn

Address book policies (ABPs) allow you to segment users into specific groups to give them customized global address lists (GALs) in Outlook and Outlook on the web (formerly known as Outlook Web App). For more information about ABPs, see [Address book policies in Exchange Online](address-book-policies).

You can only remove ABPs from your Exchange Online organization using Exchange Online PowerShell, and only if the ABP isn't assigned to a mailbox (active mailboxes or soft-deleted mailboxes that are still recoverable).

## What do you need to know before you begin?

- Estimated time to complete: Less than 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets or features that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to remove an ABP

### Step 1: Verify the ABP isn't assigned to a mailbox

1. Replace &lt;ABPName&gt; with the name of the ABP, and run the following command to get the **DistinguishedName** (DN) value of the ABP that you want to remove:

    ```PowerShell
    Get-AddressBookPolicy -Identity "<ABPName>" | Format-List DistinguishedName
    ```
2. To see if the ABP is assigned to an active mailbox, replace &lt;ABPDistinguishedName&gt; with the DN of the ABP and run the following command:

    ```PowerShell
    Get-Mailbox -ResultSize unlimited -Filter "AddressBookPolicy -eq '<ABPDistinguishedName>'"
    ```

    To remove the ABP assignment from any active mailboxes that you find, replace &lt;ABPDistinguishedName&gt; with the DN of the ABP and run the following commands:

    ```PowerShell
    $a = Get-Mailbox -ResultSize unlimited -Filter "AddressBookPolicy -eq '<ABPDistinguishedName>'"
    ```

    ```PowerShell
    $a | foreach {Set-Mailbox -Identity $_.MicrosoftOnlineServicesID -AddressBookPolicy $null}
    ```
3. To see if the ABP is assigned to a soft-deleted (recoverable) mailbox, replace &lt;ABPDistinguishedName&gt; with the DN of the ABP and run the following command:

    ```PowerShell
    Get-Mailbox -SoftDeletedMailbox -ResultSize unlimited -Filter "AddressBookPolicy -eq '<ABPDistinguishedName>'"
    ```

    To remove the ABP assignment from any soft-deleted mailboxes that you find, replace &lt;ABPDistinguishedName&gt; with the DN of the ABP and run the following commands:

    ```PowerShell
    $s = Get-Mailbox -SoftDeletedMailbox -ResultSize unlimited -Filter "AddressBookPolicy -eq '<ABPDistinguishedName>'"
    ```

    ```PowerShell
    $s | foreach {Set-Mailbox -Identity $_.MicrosoftOnlineServicesID -AddressBookPolicy $null}
    ```

**Note**: If you don't assign an ABP to a mailbox, the GAL for your entire organization will be visible to the user in Outlook and Outlook on the web. Instead of using the value `$null`, you can specify the name of a different ABP (enclosed in quotation marks if the name contains spaces).

### Step 2: Remove the ABP

To remove an ABP, use this syntax:

```PowerShell
Remove-AddressBookPolicy -Identity <ABPIdentity>
```

This example removes the ABP named ABP TailspinToys.

```PowerShell
Remove-AddressBookPolicy -Identity "ABP TailspinToys"
```

For detailed syntax and parameter information, see [Remove-AddressBookPolicy](/en-us/powershell/module/exchangepowershell/remove-addressbookpolicy).

## How do you know this worked?

To verify that you've successfully removed an ABP, use either of these procedures in Exchange Online PowerShell:

- Run the following command to verify that the ABP isn't listed:

    ```PowerShell
    Get-AddressBookPolicy
    ```
- Replace *&lt;ABPName&gt;* with the name of the ABP, and run the following command to confirm that an error is returned:

    ```PowerShell
    Get-AddressBookPolicy -Identity "<ABPName>"
    ```