---
layout: Conceptual
title: Hierarchical address books in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/hierarchical-address-books/hierarchical-address-books
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
description: Admins can learn about hierarchical address books that reflect the organization hierarchy in the address book in Exchange Online.
ms.topic: overview
author: Srividyavaranasi
ms.author: srvar
ms.assetid: a1d277a0-5437-40af-aade-e4730a0d1308
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
document_id: 6f1c6ced-4d52-df69-b492-8a6a47e793ec
document_version_independent_id: acb719f5-1828-d101-bf8f-af6f7fc03758
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/hierarchical-address-books/hierarchical-address-books.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/hierarchical-address-books/hierarchical-address-books
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/hierarchical-address-books/hierarchical-address-books.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/e93f3d5f-c77d-4365-a7fb-c9f2234416c7
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/62e8d07a-cc62-4934-b30b-e168a571e51d
platformId: 1cf24575-6d23-06b3-5c17-296ce7f094f8
---

# Hierarchical address books in Exchange Online | Microsoft Learn

The hierarchical address book (HAB) allows users to look for recipients in their address book using an organizational hierarchy. Normally, users are limited to the default global address list (GAL) and its recipient properties and the structure of the GAL often doesn't reflect the management or seniority relationships of recipients in your organization. Being able to customize an HAB that maps to your organization's unique business structure provides your users with an efficient method for locating internal recipients.

## Using hierarchical address books

In an HAB, your root organization (for example, Contoso, Ltd) is used as the top-level tier. Under this top-level tier, you can add several child tiers to create a customized HAB that's segmented by division, department, or any other organizational tier you want to specify. The following figure illustrates an HAB for Contoso, Ltd with the following structure:

- The top-level tier represents the root organization Contoso, Ltd.
- The second-level child tiers represent the business divisions within Contoso, Ltd: Corporate Office, Product Support Organization, and Sales & Marketing Organization.
- The third-level child tiers represent departments within the Corporate Office division: Human Resources, Accounting Group, and Administration Group.

![Hierarchical Address Book dialog.](../../exchangeonline/media/itpro_mailbox_habdisplay.gif)

You can provide an additional level of hierarchical structure by using the *SeniorityIndex* parameter. When creating an HAB, use the *SeniorityIndex* parameter to rank individual recipients or organizational groups by seniority within these organizational tiers. This ranking specifies the order in which the recipients or groups are displayed in the HAB. For example, in the preceding example, the *SeniorityIndex* parameter for the recipients in the Corporate Office division is set to the following:

- `100` for David Hamilton
- `50` for Rajesh M. Patel
- `25` for Amy Alberts

Note

If the *SeniorityIndex* parameter isn't set or is equal for two or more users, the HAB sorting order uses the *PhoneticDisplayName* parameter value to list the users in ascending alphabetical order. If the *PhoneticDisplayName* parameter value isn't set, the HAB defaults to the *DisplayName* parameter value and lists the users in ascending alphabetical order.

## Configuring hierarchical address books

Detailed instructions for creating HABs are included in the topic [Enable or disable hierarchical address books](enable-or-disable-hierarchical-address-books). The general steps are as follows:

1. Create a distribution group that will be used for the root organization (top-level tier).
2. Create distribution groups for the child tiers and designate them as members of the HAB. Modify the *SeniorityIndex* parameter of these groups so they're listed in the proper hierarchical order within the root organization.
3. Add organization members. Modify the *SeniorityIndex* parameter of the members so they're listed in the proper hierarchical order within the child tiers.
4. For accessibility purposes, you can use the *PhoneticDisplayName* parameter, which specifies a phonetic pronunciation of the *DisplayName* parameter, and is also used for the sort order if the *SeniorityIndex* parameter value isn't set.