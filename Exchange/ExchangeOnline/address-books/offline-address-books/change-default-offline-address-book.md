---
layout: Conceptual
title: Change the default offline address book in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/offline-address-books/change-default-offline-address-book
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
description: Admins can learn how to specify the default offline address book (OAB) in Exchange Online
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 61abf78e-2543-4431-acc8-839e3c7a4548
ms.reviewer: 
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: c8785a1b-2d72-5801-8dab-fcb0d377411b
document_version_independent_id: 6e61a23b-e6f5-1cf3-09a3-f4f23c2e71e7
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/offline-address-books/change-default-offline-address-book.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/offline-address-books/change-default-offline-address-book
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/offline-address-books/change-default-offline-address-book.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: f6c9ac5c-6ab1-0fc9-4945-6b9fb0765c96
---

# Change the default offline address book in Exchange Online | Microsoft Learn

By default, the automatically-created OAB named Default Offline Address Book is the default OAB. You can set any OAB in your Exchange Online organization as the default OAB. The default OAB is used by:

- Mailboxes without an address book policy (ABP) assigned, or where the assigned ABP policy has no OAB defined (by default, there are no ABPs).
- Mailboxes without an OAB assigned (by default, all mailboxes).

If you delete the default OAB, Exchange Online doesn't automatically assign another OAB as the default. You need to manually designate another OAB as the default.

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures).

## What do you need to know before you begin?

- Estimated time to complete this procedure: 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- You can only use Exchange Online PowerShell to perform the procedures in this topic. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to change the default OAB

This example sets the OAB named My OAB as the default OAB.

```PowerShell
Set-OfflineAddressBook -Identity "My OAB" -IsDefault $true
```

For detailed syntax and parameter information, see [Set-OfflineAddressBook](/en-us/powershell/module/exchangepowershell/set-offlineaddressbook).

## How do you know this worked?

To verify that you've successfully changed the default OAB, run the following command to verify the `IsDefault` property value:

```PowerShell
Get-OfflineAddressBook | Format-List Name,IsDefault
```