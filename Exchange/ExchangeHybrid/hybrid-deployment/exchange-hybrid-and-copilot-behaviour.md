---
layout: Conceptual
title: 'Exchange Hybrid: Microsoft Copilot and on-premises mailboxes | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/exchange-hybrid-and-copilot-behaviour
Manager: dansimp
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: tracyp
author: MSFTTracyP
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: article
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
- magic-ai-copilot
ms.assetid: ecc0a687-6c05-47bd-a079-a43d83cba9ea
ms.reviewer: 
description: This article provides Microsoft's support statement for Microsoft Copilot and on-premises mailboxes and summarizes the expected behavior of Copilot in an Exchange Hybrid environment by Outlook type, license assignment, and mailbox location.
ms.date: 2025-11-20T00:00:00.0000000Z
locale: en-us
document_id: 05490ff6-981c-82b3-0180-40465010779f
document_version_independent_id: 1e5edcde-96fc-e4e7-b4ae-c85317f887df
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/exchange-hybrid-and-copilot-behaviour.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/exchange-hybrid-and-copilot-behaviour
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/exchange-hybrid-and-copilot-behaviour.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: e672d4ad-c20b-d3a8-3456-99c23e39d8dd
---

# Exchange Hybrid: Microsoft Copilot and on-premises mailboxes | Microsoft Learn

Microsoft Copilot is cloud-based and has no access to on-premises mailboxes. There are hybrid deployment scenarios where a user with a primary mailbox on-premises also has access to Microsoft 365 services and Microsoft Copilot, but in those scenarios, because the primary mailbox is located on-premises and not in the cloud, grounding Copilot with mailbox content, including calendar information, is not supported.

The table that follows details the *Copilot in Outlook* user experience based on Outlook version, license assignment, and location of user mailbox.

| Outlook type | Microsoft 365 license assigned | Microsoft Copilot license assigned | Location of User Mailbox | Copilot Experience in Outlook | Copilot Experience outside Outlook |
| --- | --- | --- | --- | --- | --- |
| Outlook (on-premises version) | N | N | On-premises | Copilot nonexistent | Copilot nonexistent |
| Outlook (on-premises version) | Y | N | On-premises | Copilot nonexistent | Copilot not available |
| Outlook (on-premises version) | Y | Y | On-premises | Copilot nonexistent | Copilot available outside Outlook for cloud content; mailbox grounding not supported |
| Outlook (on-premises version) | Y | N | Cloud | Copilot nonexistent | Copilot not available |
| Outlook (on-premises version) | Y | Y | Cloud | Copilot nonexistent | Copilot available outside Outlook for cloud content; mailbox grounding supported |
| Outlook (Microsoft 365 Apps) | N | N | On-premises | Copilot icon exists but is grayed out and no user experience (UX) can be called | Copilot not available |
| Outlook (Microsoft 365 Apps) | Y | N | On-premises | Copilot icon exists but is dimmed / grayed-out and no UX can be called | Copilot not available |
| Outlook (Microsoft 365 Apps) | Y | Y | On-premises | Copilot icon exists but is dimmed / grayed-out and no UX can be called | Copilot available outside Outlook for cloud content; mailbox grounding not supported |
| Outlook (Microsoft 365 Apps) | Y | N | Cloud | Copilot icon exists and [Copilot Chat](/en-us/copilot/manage#microsoft-365--chat-eligibility) is available in Outlook - see: [Copilot Chat comes to the Microsoft 365 apps](https://techcommunity.microsoft.com/blog/microsoft365copilotblog/copilot-chat-comes-to-the-microsoft-365-apps/4453349) | Copilot Chat available |
| Outlook (Microsoft 365 Apps) | Y | Y | Cloud | Copilot icon exists and Copilot is available in Outlook | Copilot available across all surfaces; mailbox grounding supported |

The text that follows describes Copilot user experience based on Outlook version, license assignment, and location of user mailbox, line-by-line.

1. **Outlook (on-premises version) without Microsoft 365 license or Copilot license assigned, with on-premises mailbox**:
    - **Expected Copilot Behavior in Outlook**: Copilot nonexistent (no icons, user experience (UX), or functions).
    - **Expected Copilot Behavior outside Outlook**: Copilot nonexistent (no icons, UX, or functions).
2. **Outlook (on-premises version) with Microsoft 365 license, but without Copilot license assigned, with on-premises mailbox**:
    - **Expected Copilot Behavior in Outlook**: Copilot nonexistent (no icons, UX, or functions).
    - **Expected Copilot Behavior outside Outlook**: Copilot not available.
3. **Outlook (on-premises version) with both Microsoft 365 and Copilot licenses assigned, with on-premises mailbox**:
    - **Expected Copilot Behavior in Outlook**: Copilot nonexistent (no icons, UX, or functions).
    - **Expected Copilot Behavior outside Outlook**: Copilot available outside Outlook for cloud content; mailbox grounding not supported.
4. **Outlook (on-premises version) with Microsoft 365 license but without Copilot license assigned, Cloud mailbox**:
    - **Expected Copilot Behavior in Outlook**: Copilot nonexistent (no icons, UX, or functions).
    - **Expected Copilot Behavior outside Outlook**: Copilot not available.
5. **Outlook (on-premises version) with both Microsoft 365 and Copilot licenses assigned, Cloud mailbox**:
    - **Expected Copilot Behavior in Outlook**: Copilot nonexistent (no icons, UX, or functions).
    - **Expected Copilot Behavior outside Outlook**: Copilot available outside Outlook for cloud content; mailbox grounding supported.
6. **Outlook (Microsoft 365 Apps) without Microsoft 365 license and without Copilot license assigned, with on-premises mailbox**:
    - **Expected Copilot Behavior in Outlook**: Copilot icon exists but is dimmed / grayed-out and no UX can be called.
    - **Expected Copilot Behavior outside Outlook**: Copilot not available.
7. **Outlook (Microsoft 365 Apps) with Microsoft 365 license but without Copilot license assigned, on-premises mailbox**:
    - **Expected Copilot Behavior in Outlook**: Copilot icon exists but is dimmed/grayed-out and no UX can be called.
    - **Expected Copilot Behavior outside Outlook**: Copilot not available.
8. **Outlook (Microsoft 365 Apps) with both Microsoft 365 and Copilot licenses assigned, on-premises mailbox**:
    - **Expected Copilot behavior in Outlook**: Copilot icon exists but is dimmed / grayed-out and no UX can be called.
    - **Expected Copilot behavior outside Outlook**: Copilot available outside outlook for cloud content; mailbox grounding not supported.
9. **Outlook (Microsoft 365 Apps) with Microsoft 365 license, without Copilot license assigned, Cloud mailbox**:
    - **Expected Copilot behavior in Outlook**: Copilot icon exists and [Copilot Chat](/en-us/copilot/manage#microsoft-365--chat-eligibility) is available in Outlook - see: [Copilot Chat comes to the Microsoft 365 apps](https://techcommunity.microsoft.com/blog/microsoft365copilotblog/copilot-chat-comes-to-the-microsoft-365-apps/4453349).
    - **Expected Copilot behavior outside Outlook**: Copilot Chat available.
10. **Outlook (Microsoft 365 Apps) with both Microsoft 365 and Copilot licenses assigned, Cloud mailbox**:
    - **Expected Copilot behavior in Outlook**: Copilot icon exists and Copilot is available in Outlook.
    - **Expected Copilot behavior outside Outlook**: Copilot available across all surfaces; mailbox grounding supported.

## What's next?

[How does Microsoft Copilot work?](/en-us/microsoft-365/copilot/microsoft-365-copilot-overview)

[Frequently asked questions about Outlook Copilot](https://support.microsoft.com/en-us/office/frequently-asked-questions-about-copilot-in-outlook-07420c70-099e-4552-8522-7d426712917b)

[Troubleshoot a hybrid deployment](troubleshoot-a-hybrid-deployment).