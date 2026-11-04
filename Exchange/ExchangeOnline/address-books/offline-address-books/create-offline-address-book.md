---
layout: Conceptual
title: Create an offline address book in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/offline-address-books/create-offline-address-book
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
description: Admins can learn how to create offline address books (OABs) in Exchange Online.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms.reviewer: 
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
f1.keywords:
- CSH
ms.custom:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
- has-azure-ad-ps-ref
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: db5c9d81-c5be-473c-fc4e-1f9ffef67044
document_version_independent_id: 31dae735-15ca-38f7-9657-25e270b69eed
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/offline-address-books/create-offline-address-book.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/offline-address-books/create-offline-address-book
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/offline-address-books/create-offline-address-book.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: bf82e3d9-aae2-a175-02e2-477a168fde99
---

# Create an offline address book in Exchange Online | Microsoft Learn

An offline address book (OAB) is a downloadable address list collection that Outlook users can access while disconnected from Exchange Online. An OAB allows Outlook users to access the information within the specified address lists while disconnected from Exchange Online. Admins can decide which address lists are made available to users who work offline.

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- You can only use Exchange Online PowerShell to perform the procedures in this topic. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to create an OAB with web-based distribution

This example creates an OAB named OAB\_Contoso that contains the default global address list.

```PowerShell
New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List"
```

For detailed syntax and parameter information, see [New-OfflineAddressBook](/en-us/powershell/module/exchangepowershell/new-offlineaddressbook).