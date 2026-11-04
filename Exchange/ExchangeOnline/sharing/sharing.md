---
layout: Conceptual
title: Sharing in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/sharing
Manager: dansimp
ms.subservice: sharing
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: You may need to coordinate schedules with people in different organizations or with friends and family members so that you can work together on projects or plan social events. With Microsoft 365 and Office 365, administrators can set up different levels of calendar access in Exchange Online to allow businesses to collaborate with other businesses and to let users share their schedules with others. Business-to-business calendar sharing is set up by creating organization relationships. User-to-user calendar sharing is set up by applying sharing policies.
ms.topic: concept-article
author: navanethan-msft
ms.author: nagangat
ms.assetid: 7a7bc6fe-3ab8-4d39-a655-ec3390a1437e
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
- essentials-manage
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-26T00:00:00.0000000Z
locale: en-us
document_id: 39cc4696-4255-cf58-5f79-830a1d544623
document_version_independent_id: fa1c6a8d-b156-4132-dd0a-70b31ec199ac
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/sharing.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/sharing
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/sharing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: c3428f98-9fa9-81e9-3e08-1adbc29f0dec
---

# Sharing in Exchange Online | Microsoft Learn

You may need to coordinate schedules with people in different organizations or with friends and family members so that you can work together on projects or plan social events. With Microsoft 365 and Office 365, administrators can set up different levels of calendar access in Exchange Online to allow businesses to collaborate with other businesses and to let users share their schedules with others. Business-to-business calendar sharing is set up by creating organization relationships. User-to-user calendar sharing is set up by applying sharing policies.

Note

Organization Sharing functionality of the Classic Exchange admin center experience is available in the new Exchange admin center as we continue to work on updated versions. If you're using **Edge** incognito and this page isn't working, enable the [third-party cookies](https://support.microsoft.com/microsoft-edge/temporarily-allow-cookies-and-site-data-in-microsoft-edge-597f04f2-c0ce-f08c-7c2b-541086362bd2).

## Sharing Scenarios in Exchange Online

The following sharing scenarios are supported in Exchange Online:

| Sharing goal | Setting to use | Requirements |
| --- | --- | --- |
| Share calendars with another Microsoft 365 or Office 365 organization | Organization relationships | None, ready to configure |
| Share calendars with an on-premises Exchange organization | Organization relationships | The on-premises Exchange administrator has to set up an authentication relationship with the cloud (also known as "federation") and must meet minimum software requirements |
| Share a Microsoft 365 or Office 365 user's calendar with another internet user | Sharing policies | None, ready to configure |
| Share a Microsoft 365 or Office 365 user's calendar with an Exchange on-premises user | Sharing policies | The on-premises Exchange administrator has to set up an authentication relationship with the cloud (also known as "federation") and must meet minimum software requirements |

## Sharing documentation

The following table contains links to articles that will help you learn about and manage sharing in Exchange Online.

| Topic | Description |
| --- | --- |
| [Organization relationships in Exchange Online](organization-relationships/organization-relationships) | Learn more about the one-to-one relationships between organizations that enable calendar free/busy sharing. |
| [Sharing policies in Exchange Online](sharing-policies/sharing-policies) | Learn more about the person-to-person policies that enable calendar sharing. |