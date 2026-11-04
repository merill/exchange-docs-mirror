---
layout: Conceptual
title: Manage recipients in the Built-in security add-on for on-premises mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/standalone-eop/manage-recipients-in-eop
Manager: deniseb
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: chrisda
author: chrisda
ms.date: 2024-05-22T00:00:00.0000000Z
audience: ITPro
ms.topic: overview
ms.localizationpriority: medium
ms.assetid: 2921f544-8257-4bae-8e3a-ce9250e9f162
ms.custom:
- seo-marvel-apr2020
description: Admins in on-premises organizations that use the Built-in security add-on for on-premises mailboxes can learn about the different types of recipient objects in the add-on.
ms.service: exchange-online
locale: en-us
document_id: 2382f9c5-6ada-023c-edf1-bc64df8c0799
document_version_independent_id: b205cd64-6406-f285-529d-fd0cfd7e7a26
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/standalone-eop/manage-recipients-in-eop.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standalone-eop/manage-recipients-in-eop
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/standalone-eop/manage-recipients-in-eop.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: c526b095-2f13-9c62-144b-9c1c16116932
---

# Manage recipients in the Built-in security add-on for on-premises mailboxes | Microsoft Learn

If you use the Built-in security add-on for on-premises mailboxes, the following types of recipients are available in the add-on:

- **Mail users**: Mail users are the fundamental type of user accounts in the Built-in security add-on for on-premises mailboxes. Mail users have sign in credentials in the cloud organization, but they have external email addresses (their mailboxes are located outside the cloud organization).

    For more information about managing mail users, see [Manage mail users in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-mail-users).
- **Mail contacts**: Contacts have external email addresses, but no sign in credentials in the cloud organization. The mail contact is visible in your organization's shared address book (also known as the global address list or GAL) and other address lists.

    For more information about managing mail contacts, see [Manage mail contacts in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-mail-contacts).
- **Groups**: You can create the following types of groups in the Built-in security add-on for on-premises mailboxes:

    - Microsoft 365 Groups
    - Distribution groups
    - Mail-enabled security groups
    - Dynamic distribution groups

For instructions, see [Manage groups in the Built-in security add-on for on-premises mailboxes](manage-groups-in-eop).