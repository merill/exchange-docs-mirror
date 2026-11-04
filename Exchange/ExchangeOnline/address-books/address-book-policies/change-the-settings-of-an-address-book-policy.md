---
layout: Conceptual
title: Change the settings of an address book policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-book-policies/change-the-settings-of-an-address-book-policy
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
description: Admins can learn how to modify address book policies (ABPs) in Exchange Online
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: ba1ca350-71c2-4c60-a612-33bfa9320b5e
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2024-03-15T00:00:00.0000000Z
locale: en-us
document_id: 96185fb5-b5a0-4da4-a459-bc66ebb56176
document_version_independent_id: 4515c3bc-e3a1-67f4-4099-0cfd46db777a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-book-policies/change-the-settings-of-an-address-book-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-book-policies/change-the-settings-of-an-address-book-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-book-policies/change-the-settings-of-an-address-book-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 65bf4578-21a4-af66-25a1-65261801a304
---

# Change the settings of an address book policy in Exchange Online | Microsoft Learn

Address book policies (ABPs) allow you to segment users into specific groups to give them customized global address lists (GALs) in Outlook and Outlook on the web (formerly known as Outlook Web App). For more information about ABPs, see [Address book policies in Exchange Online](address-book-policies).

After you create an ABP, you can view or modify the name and the assigned address lists: the global address list (GAL), offline address book (OAB), room list, and other address lists.

In Exchange Online, you can only modify ABPs in Exchange Online PowerShell.

For additional management tasks related to ABPs, see [Address book policy procedures in Exchange Online](address-book-policy-procedures).

## What do you need to know before you begin?

- Estimated time to complete: Less than 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets or features that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

## Use Exchange Online PowerShell to modify address book policies

To modify an ABP, use this syntax:

```PowerShell
Set-AddressBookPolicy -Identity "<ABPName>" [-Name "<Unique Name>"] [-GlobalAddressList "<GAL>"] [-OfflineAddressBook "<OAB>"] [-RoomList "<RoomList>"] [-AddressLists <AddressLists>]
```

- The *Name*, *GlobalAddressList*, *OfflineAddressBook*, and *RoomList* parameters all take single values, so the value you specify replaces the existing value.

    This example modifies the ABP named "All Fabrikam ABP" by replacing the OAB with the specified OAB.

    ```PowerShell
    Set-AddressBookPolicy -Identity "All Fabrikam ABP" -OfflineAddressBook \Fabrikam-OAB-2
    ```
- The *AddressLists* parameter takes multiple values, so you need to decide whether you want to *replace* the existing address lists in the ABP, or *add and remove* address lists without affecting the other address lists in the ABP.

    This example replaces the existing address lists in the ABP named Government Agency A with the specified address lists.

    ```PowerShell
    Set-AddressBookPolicy -Identity "Government Agency A" -AddressLists "GovernmentAgencyA-Atlanta","GovernmentAgencyA-Moscow"
    ```

    To add address lists to an ABP, you need to specify the new address lists *and* any existing address lists that you want to keep.

    This example adds the address list named Contoso-Chicago to the ABP named ABP Contoso, which is already configured to use the address list named Contoso-Seattle.

    ```PowerShell
    Set-AddressBookPolicy -Identity "ABP Contoso" -AddressLists "Contoso-Chicago","Contoso-Seattle"
    ```

    To remove address lists from an ABP, you need to specify the existing address lists that you want to keep, and omit the address lists that you want to remove.

    For example, the ABP named ABP Fabrikam uses the address lists named Fabrikam-HR and Fabrikam-Finance. To remove the Fabrikam-HR address list, specify only the Fabrikam-Finance address list.

    ```PowerShell
    Set-AddressBookPolicy -Identity "ABP Fabrikam" -AddressLists Fabrikam-Finance
    ```

For detailed syntax and parameter information, see [Set-AddressBookPolicy](/en-us/powershell/module/exchangepowershell/set-addressbookpolicy).

### How do you know this worked?

To verify that you've successfully modify an ABP, replace *&lt;ABPName&gt;* with the name of the ABP, and run the following command in Exchange Online PowerShell to verify the property values:

```PowerShell
Get-AddressBookPolicy -Identity "<ABPName>" | Format-List
```