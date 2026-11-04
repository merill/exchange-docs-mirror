---
layout: Conceptual
title: Remove a global address list in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-lists/remove-a-global-address-list
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
description: Admins can learn how to remove custom global address lists (GALs) from Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 65d75b69-641b-4a37-a63c-47cf018f5f22
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
document_id: f5a24db2-8374-37ea-dfe2-6cdd5f7a72ff
document_version_independent_id: b21e002a-d1ef-dd28-9bc7-e635a301cf6f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-lists/remove-a-global-address-list.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-lists/remove-a-global-address-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-lists/remove-a-global-address-list.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: ddff2e4f-36fe-cda6-17e1-a54b132b384c
---

# Remove a global address list in Exchange Online | Microsoft Learn

The built-in global address list (GAL) that's automatically created by Exchange Online includes every mail-enabled object in the organization. You can create additional GALs to separate users by organization or location, but a user can only see and use one GAL. For more information about address lists, see [Address lists in Exchange Online](address-lists).

You can use the procedures in this topic to remove any custom GALs that you've created. You can't remove:

- The GAL named Default Offline Address Book, which is the built-in GAL that's available in Exchange Online, and the only GAL that has the **IsDefaultGlobalAddressList** property value `True`.
- A GAL that's defined in an offline address book (OAB). For OAB procedures, see [Offline address book procedures](../offline-address-books/offline-address-book-procedures).

For additional GAL management tasks, see [Address list procedures in Exchange Online](address-list-procedures).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- You can only use Exchange Online PowerShell to perform the procedures in this topic. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to remove a GAL

To remove a GAL, use the following syntax:

```PowerShell
Remove-GlobalAddressList -Identity <GALIdentity>
```

This example removes the address list named Agency A GAL.

```PowerShell
Remove-GlobalAddressList -Identity "Agency A GAL"
```

For detailed syntax and parameter information, see [Remove-GlobalAddressList](/en-us/powershell/module/exchangepowershell/remove-globaladdresslist).

#### How do you know this worked?

To verify that you've successfully removed a GAL, run the following command in Exchange Online PowerShell to verify that the GAL isn't listed:

```PowerShell
Get-GlobalAddressList
```