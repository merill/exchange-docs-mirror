---
layout: Conceptual
title: Create a global address list in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-lists/create-global-address-list
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
description: Admins can learn how to create of global address lists (GALs) in Exchange Online.
ms.topic: how-to
author: Srividyavaranasi
ms.author: srvar
ms.assetid: 59e4955a-8999-4d17-be9f-23a41a23b929
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2026-10-26T00:00:00.0000000Z
locale: en-us
document_id: ab0ed59f-71c5-de9b-2b26-bbe12848514d
document_version_independent_id: 39c67675-d3b8-9a3a-a2cc-87eb372b8d59
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-lists/create-global-address-list.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-lists/create-global-address-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-lists/create-global-address-list.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: fade6448-bf38-4350-808f-712c5daefea7
---

# Create a global address list in Exchange Online | Microsoft Learn

The built-in global address list (GAL) that's automatically created by Exchange Online includes every mail-enabled object in the organization. You can create additional GALs to separate users by organization or location, but a user can only see and use one GAL. For more information about address lists, see [Address lists in Exchange Online](address-lists).

If your organization uses address book policies (ABPs), you'll need to create additional GALs. To learn more, see [Address book policies in Exchange Online](../address-book-policies/address-book-policies).

For additional GAL management tasks, see [Manage address lists in Exchange Online](manage-address-lists).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- By default, the Address Lists role isn't assigned to any role groups in Exchange Online. To use cmdlets that require the Address Lists role, add the role to a role group. For more information, see [Modify role groups](/en-us/exchange/permissions-exo/role-groups#use-the-eac-to-modify-role-groups). .
- You can only use Exchange Online PowerShell to perform the procedures in this topic. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For details about recipient filters in the Exchange Online PowerShell, see [Recipient filters for address lists in Exchange Online PowerShell](use-recipient-filters-to-create-an-address-list).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to create global address lists

To create a GAL, use the following syntax:

```PowerShell
New-GlobalAddressList -Name "<GAL Name>" [<Precanned recipient filter | Custom recipient filter>]
```

This example creates a GAL with a precanned recipient filter:

- **Name**: Contoso GAL
- **Precanned recipient filter**: All recipient types where the **Company** value is Contoso.

```PowerShell
New-GlobalAddressList -Name "Contoso GAL" -IncludedRecipients AllRecipients -ConditionalCompany Contoso
```

This example creates a GAL with a custom recipient filter:

- **Name**: Agency A GAL
- **Custom recipient filter**: All recipient types where the CustomAttribute15 property contains the value AgencyA.

```PowerShell
New-GlobalAddressList -Name "Agency A GAL" -RecipientFilter "CustomAttribute15 -like '*AgencyA*'"
```

For detailed syntax and parameter information, see [New-GlobalAddressList](/en-us/powershell/module/exchangepowershell/new-globaladdresslist).

#### How do you know this worked?

To verify that you've successfully created a GAL, replace *&lt;GAL Name&gt;* with the name of the GAL and run the following command in Exchange Online PowerShell to verify the property values:

```PowerShell
Get-GlobalAddressList -Identity "<GAL Name>" | Format-List Name,RecipientFilterType,RecipientFilter,IncludedRecipients,Conditional*
```