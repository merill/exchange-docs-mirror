---
layout: Conceptual
title: Single sign-on with hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/single-sign-on
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: install-set-up-deploy
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
ms.assetid: 050606f9-718d-4a1f-b7a6-50b08c6e9e07
ms.reviewer: 
description: "Single sign-on enables users to access both the on-premises and Microsoft 365 or Office 365 organizations with a single username and password. It provides users with a familiar sign-on experience and can allow administrators to easily control account policies for Exchange Online organization mailboxes by using on-premises Active Directory management tools. While you don't have to configure a hybrid deployment with single sign-on enabled, we strongly recommend that you do. Without single sign-on, users will need to remember two different sets of credentials, one for your on-premises organization, and one for Microsoft 365 or Office 365. Here are a few other advantages to single sign-on:"
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 50117f9a-45dd-90fb-a592-6a12c6104875
document_version_independent_id: d07fe199-59af-86bf-fe79-c7e2d342a463
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/single-sign-on.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: single-sign-on
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/single-sign-on.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: e9953669-cf22-fd99-aa06-7c9b6b6b0a17
---

# Single sign-on with hybrid deployments | Microsoft Learn

Single sign-on enables users to access both the on-premises and Microsoft 365 or Office 365 organizations with a single username and password. It provides users with a familiar sign-on experience and can allow administrators to easily control account policies for Exchange Online organization mailboxes by using on-premises Active Directory management tools. While you don't have to configure a hybrid deployment with single sign-on enabled, we strongly recommend that you do. Without single sign-on, users will need to remember two different sets of credentials, one for your on-premises organization, and one for Microsoft 365 or Office 365. Here are a few other advantages to single sign-on:

- **Exchange Online Archiving**: When single sign-on is deployed, on-premises Outlook users are prompted for their credentials when accessing archived content in the Exchange Online organization for the first time. However, users can then temporarily avoid future credential prompting by choosing "save password" and then will only be prompted for credentials again when their on-premises account password is changed. If single sign-on isn't deployed in Exchange organizations and Exchange Online Archiving is enabled, the on-premises user principal name (UPN) must match their Exchange Online account and users will always be prompted for their on-premises credentials when accessing their archive.
- **Policy control**: You can control account policies through Active Directory, which gives you the ability to manage password policies, workstation restrictions, lock-out controls, and more, without having to perform additional tasks in your Microsoft 365 or Office 365 organization.
- **Reduced support calls**: Forgotten passwords are a common source of support calls in all companies. If users have fewer passwords to remember, they are less likely to forget them.

You have three options when deploying single sign-on: password hash synchronization, pass-through authentication and federation, for example, Active Directory Federation Services (AD FS). All options are implemented by Microsoft Entra Connect. We strongly recommend using the password hash synchronization method unless you have a specific need that requires federation. Password hash synchronization provides many of the same benefits of federation without the complexity of its deployment.

To learn more about each option, see [Choose the right authentication method for your Microsoft Entra hybrid identity solution](/en-us/entra/identity/hybrid/connect/choose-ad-authn).

Important

We strongly recommend using MFA for all logins of users or admins in case of Hybrid Deployments.