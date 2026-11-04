---
layout: Conceptual
title: Add an address list to or remove an address list from an offline address book in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/offline-address-books/add-or-remove-an-address-list
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
description: Admins can learn how to add or remove address lists in offline address books (OABs) in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms.reviewer: 
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: b904aaa3-52bb-1fee-df91-ae0e6592db4f
document_version_independent_id: a0d1a92c-f44c-2ebd-4834-63c70959f8e2
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/offline-address-books/add-or-remove-an-address-list.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/offline-address-books/add-or-remove-an-address-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/offline-address-books/add-or-remove-an-address-list.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: edf1c996-39dd-dc93-c8a6-7af56e1d849f
---

# Add an address list to or remove an address list from an offline address book in Exchange Online | Microsoft Learn

You can use Exchange Online PowerShell to add or remove an address list from an offline address book (OAB). By default, there is an OAB named the Default Offline Address Book that contains the global address list (GAL). OABs are generated based on the address lists that they contain. To create custom OABs that users can download, you can add or remove address lists from OABs.

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes
- Changes to the address list aren't available for client download until after the OAB in which the address list resides has been generated.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- You can only use Exchange Online PowerShell to perform the procedures in this topic. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to add and remove address lists from offline address books

When you modify the address lists that are configured in an OAB, the values that you specify will *replace* any address lists in the OAB. To add address lists to the OAB, specify the current address lists plus the ones you want to add. To remove address lists from the OAB, specify the current address lists minus the ones you want to remove.

In this example, the OAB named Marketing OAB is already configured with Address List 1 and Address List 2. To keeps those address lists and add Address List 3, run the following command:

```PowerShell
Set-OfflineAddressBook -Identity "Marketing OAB" -AddressLists "Address List1","Address List 2","Address List 3"
```

Similarly, to keep the OAB configured with Address List 1 and Address 2, but remove Address List 3, run the following command:

```PowerShell
Set-OfflineAddressBook -Identity "Marketing OAB" -AddressLists "Address List 1","Address List 2"
```

For detailed syntax and parameter information, see [Set-OfflineAddressBook](/en-us/powershell/module/exchangepowershell/set-offlineaddressbook).

## How do you know this worked?

To verify that you've successfully added or removed address lists from an OAB, run the following command to verify the property `AddressLists` property values:

```PowerShell
Get-OfflineAddressBook | Format-List Name,AddressLists
```