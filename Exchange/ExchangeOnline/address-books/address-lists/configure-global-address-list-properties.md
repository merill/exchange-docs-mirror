---
layout: Conceptual
title: Configure global address list properties in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-lists/configure-global-address-list-properties
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
description: Admins can learn how to modify the settings of a global address list (GAL) in Exchange Online.
ms.topic: how-to
author: Srividyavaranasi
ms.author: srvar
ms.assetid: 5fd2c96f-fe93-4b5a-8495-70c450511a37
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2026-10-27T00:00:00.0000000Z
locale: en-us
document_id: fc2985bc-3016-dc63-efe6-56f221b2eb04
document_version_independent_id: e2af137a-79ed-63c7-2d13-6f9ced8d71d7
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-lists/configure-global-address-list-properties.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-lists/configure-global-address-list-properties
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-lists/configure-global-address-list-properties.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 9ee5e460-411d-62e7-9efb-5124816287dc
---

# Configure global address list properties in Exchange Online | Microsoft Learn

The built-in global address list (GAL) that's automatically created by Exchange Online includes every mail-enabled object in the organization. You can create additional GALs to separate users by organization or location, but a user can only see and use one GAL. For more information about address lists, see [Address lists in Exchange Online](address-lists).

The same settings to configure a GAL are available as when you created the GAL. For more information, see [Create a global address list in Exchange Online](create-global-address-list). For additional GAL management tasks, see [Manage address lists in Exchange Online](manage-address-lists).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- You can't modify the GAL named Default Global Address List, the built-in GAL that's available in Exchange Online, and the only GAL that has the **IsDefaultGlobalAddressList** property value `True`.
- You can't replace a custom recipient filter with a precanned recipient filter or vice-versa in an existing GAL.
- You can only use Exchange Online PowerShell to perform the procedures in this topic. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For details about recipient filters in the Exchange Online PowerShell, see [Recipient filters for address lists in Exchange Online PowerShell](use-recipient-filters-to-create-an-address-list).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use the Exchange Online PowerShell to modify global address lists

To modify a GAL, use the following syntax:

```PowerShell
Set-GlobalAddressList -Identity <GALIdentity> [-Name <Name>] [<Precanned recipient filter | Custom recipient filter>]
```

When you modify the precanned *Conditional* parameter values, you can use the following syntax to add or remove values without affecting other existing values: `@{Add="<Value1>","<Value2>"...; Remove="<Value1>","<Value2>"...}`.

This example modifies the existing GAL named Contoso GAL by adding the **Company** value Fabrikam to the precanned recipient filter.

```PowerShell
Set-GlobalAddressList -Identity "Contoso GAL" -ConditionalCompany @{Add="Fabrikam"}
```

For detailed syntax and parameter information, see [Set-GlobalAddressList](/en-us/powershell/module/exchangepowershell/set-globaladdresslist).

#### How do you know this worked?

To verify that you've successfully modified a GAL, replace *&lt;GAL Name&gt;* with the name of the GAL and run the following command in Exchange Online PowerShell to verify the property values:

```PowerShell
Get-GlobalAddressList -Identity "<GAL Name>" | Format-List Name,RecipientFilterType,RecipientFilter,IncludedRecipients,Conditional*
```