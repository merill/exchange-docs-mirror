---
layout: Conceptual
title: Shared free/busy in Exchange hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/shared-free-busy
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
ms.assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms.reviewer: 
description: Sharing free/busy (calendar availability) information between users located on-premises and in the Exchange Online organization is one of the primary benefits of a hybrid deployment. Users in both organizations can view each other's calendars as if they were located in the same physical organization. This makes scheduling meetings and resources easy and efficient.
ms.date: 2026-10-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 59be6f6e-75b7-68cc-e158-c22a7e2508a6
document_version_independent_id: 4dfeded2-fdb7-3f34-fb81-79d50f71b776
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/shared-free-busy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: shared-free-busy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/shared-free-busy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 6d1e2c27-7bf5-d33c-d38e-47e3a003b109
---

# Shared free/busy in Exchange hybrid deployments | Microsoft Learn

Sharing free/busy (also known as *calendar availability*) information between users in on-premises Exchange and Exchange Online is one of the primary benefits of a hybrid deployment. Users in both organizations can view each other's calendars as if they were located in the same physical organization. This configuration makes scheduling meetings and resources easy and efficient.

Several components in a hybrid deployment are required to enable the shared free/busy feature between your on-premises Exchange organization and Exchange Online.

- **OAuth authentication**: In supported Exchange hybrid deployments, OAuth provides authentication for cross-premises features such as free/busy sharing. HCW configures OAuth when the corresponding hybrid configuration option is selected. For dedicated Exchange hybrid application requirements, see [Deploy dedicated Exchange hybrid app](hybrid-deployment/deploy-dedicated-hybrid-app).
- **Organization relationships**: Organization relationships are needed for both the on-premises Exchange and Exchange Online organization. These relationships are configured automatically by the Hybrid Configuration wizard. An organization relationship defines the level of free/busy information that's shared from the organization.

    By default, the free/busy data access sharing level is **Free/busy access with time, plus subject and location** for both the on-premises and Exchange Online organization relationships. You can manually configure the organization relationship access level after the Hybrid Configuration wizard has completed.

    Learn more at [Sharing](sharing-exchange-2013-help).

In a supported Full Hybrid deployment, HCW configures shared free/busy when the corresponding OAuth and organization relationship options are selected. Federation Trust/EWS will no longer be supported for hybrid free/busy.

Learn more at [Hybrid components](/en-us/exchange/exchange-hybrid#exchange-hybrid-deployment-components).

The following features use cross-premises authentication and organization relationships as applicable.

| Messaging area | Feature |
| --- | --- |
| Email client | Message tracking <br> MailTips <br><br> Multi-mailbox search |
| Compliance | Exchange Online Archiving <br> Exchange In-place eDiscovery |