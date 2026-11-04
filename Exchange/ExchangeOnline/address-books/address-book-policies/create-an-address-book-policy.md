---
layout: Conceptual
title: Create an address book policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-book-policies/create-an-address-book-policy
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
description: Learn how to create address book policies (ABPs) in Exchange Online.
ms.topic: how-to
author: Srividyavaranasi
ms.author: srvar
ms.assetid: 6359abaf-e6f6-4667-8c2b-3860728b39a9
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2026-10-28T00:00:00.0000000Z
locale: en-us
document_id: 898cf967-a7a6-b71a-193d-ae1f2718e42f
document_version_independent_id: 67cb1b4e-849d-8f97-c2fe-2996fa44e34f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-book-policies/create-an-address-book-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-book-policies/create-an-address-book-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-book-policies/create-an-address-book-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: e1be88f6-792b-032b-29a9-8b7bea868bbe
---

# Create an address book policy in Exchange Online | Microsoft Learn

Address book policies (ABPs) allow you to segment users into specific groups to give them customized global address lists (GALs). Users assigned an ABP can find only recipients included in the GAL associated with that policy in people-search experiences across Microsoft 365 products. For more information about ABPs, see [Address book policies in Exchange Online](address-book-policies).

In Exchange Online, you can only create ABPs in Exchange Online PowerShell.

An ABP requires one global address list (GAL), one offline address book (OAB), one room list, and one or more address lists. To view the available objects, use the **Get-GlobalAddressList**, **Get-OfflineAddressBook**, and **Get-AddressList** cmdlets.

Note

- In Exchange Online, these cmdlets are available only in the Address Lists role, and by default, the role isn't assigned to any role groups. To use these cmdlets, add the Address Lists role to a role group (for example, to the Organization Management role group). For more information, see [Modify role groups in Exchange Online](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- The room list that's required for an ABP is an address list that specifies rooms (contains the filter `RecipientDisplayType -eq 'ConferenceRoomMailbox'`). It's not a room finder distribution group that you create with the *RoomList* switch on the **New-DistributionGroup** or **Set-DistributionGroup** cmdlets.

## What do you need to know before you begin?

- Estimated time to complete: Less than 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets or features that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- Creating an ABP for an organization is a multi-step process that requires planning. For more information, see [Address book policies in Exchange Online](address-book-policies).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to create an ABP

To create an ABP, use this syntax:

```PowerShell
New-AddressBookPolicy -Name "<Unique Name>" -GlobalAddressList "<GAL>" -OfflineAddressBook "<OAB>" -RoomList "<RoomList>" -AddressLists "<AddressList1>","<AddressList2>"...
```

This example creates an ABP with the following settings:

- **Name**: All Fabrikam ABP
- **GAL**: All Fabrikam
- **OAB**: Fabrikam-All-OAB
- **Room list**: All Fabrikam Rooms
- **Address lists**: All Fabrikam, All Fabrikam Mailboxes, All Fabrikam DLs, and All Fabrikam Contacts

```PowerShell
New-AddressBookPolicy -Name "All Fabrikam ABP" -AddressLists "\All Fabrikam","\All Fabrikam Mailboxes","\All Fabrikam DLs","\All Fabrikam Contacts" -OfflineAddressBook \Fabrikam-All-OAB -GlobalAddressList "\All Fabrikam" -RoomList "\All Fabrikam Rooms"
```

For detailed syntax and parameter information, see [New-AddressBookPolicy](/en-us/powershell/module/exchangepowershell/new-addressbookpolicy).

### How do you know this worked?

To verify that you've successfully created an ABP, use either of these procedures in Exchange Online PowerShell:

- Run the following command to verify that the ABP is listed:

    ```PowerShell
    Get-AddressBookPolicy
    ```
- Replace *&lt;ABPName&gt;* with the name of the ABP, and run the following command to verify the property values:

    ```PowerShell
    Get-AddressBookPolicy -Identity "<ABPName>" | Format-List
    ```

## For more information

After you create an ABP, you need to assign the ABP to users. For instructions, see [Assign an address book policy to users in Exchange Online](assign-an-address-book-policy-to-mail-users).