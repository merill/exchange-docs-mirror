---
layout: Conceptual
title: Remove an offline address book from Exchange in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/offline-address-books/remove-offline-address-book
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
description: Admins can learn how to remove offline address book (OAB) from Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
ms.reviewer: 
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 9a2d4039-81e6-8134-97db-cb3f1878c1d1
document_version_independent_id: b09aea1b-0895-cf5f-17f9-29c26c891784
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/offline-address-books/remove-offline-address-book.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/offline-address-books/remove-offline-address-book
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/offline-address-books/remove-offline-address-book.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 74ce8724-f0aa-9e6e-5b1b-83255a138c53
---

# Remove an offline address book from Exchange in Exchange Online | Microsoft Learn

This topic explains how to remove an offline address book (OAB) from Exchange Online. If you remove the default OAB, you must assign a different OAB as the default OAB. For instructions about how to change the default OAB, see [Change the default offline address book](change-default-offline-address-book).

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- You can only use Exchange Online PowerShell to perform the procedures in this topic. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to remove an OAB

This example removes an OAB named My OAB.

```PowerShell
Remove-OfflineAddressBook -Identity "My OAB"
```

For detailed syntax and parameter information, see [Remove-OfflineAddressBook](/en-us/powershell/module/exchangepowershell/remove-offlineaddressbook).

## How do you know this worked?

To verify that you've successfully removed the OAB, run the following command to verify that the OAB is gone.

```PowerShell
Get-OfflineAddressBook
```