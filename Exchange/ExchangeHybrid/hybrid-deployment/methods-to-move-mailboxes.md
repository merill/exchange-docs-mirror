---
layout: Conceptual
title: Methods to move mailboxes between on-premises and Exchange Online organizations | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/methods-to-move-mailboxes
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
audience: ITPro
ms.topic: upgrade-and-migration-article
f1.keywords:
- CSH
ms.custom:
- O365E_HRCMoveRequest_FL312271
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
- M365-email-calendar
ms.assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms.reviewer: 
description: With an Exchange-based hybrid deployment, you can choose either Exchange Admin Center (EAC) or PowerShell to move on-premises Exchange mailboxes to the Exchange Online organization or to move Exchange Online mailboxes to the Exchange organization.
ms.date: 2024-10-03T00:00:00.0000000Z
locale: en-us
document_id: 6956f09a-6f8f-af09-cb93-a9430211679c
document_version_independent_id: c5a8a75c-cb65-009a-e863-89e67064224e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/methods-to-move-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/methods-to-move-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/methods-to-move-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 9eb1379e-3709-1150-2379-8cbed9def1aa
---

# Methods to move mailboxes between on-premises and Exchange Online organizations | Microsoft Learn

This article specifies the different methods by which you can move mailboxes between on-premises and Exchange Online organizations.

- **EAC**: Using Exchange Admin Center (EAC), you can move mailboxes from an on-premises organization to an Exchange Online organization, or from an Exchange Online organization to an on-premises organization. For more information, see [Use the EAC to move mailboxes](move-mailboxes-using-eac#use-the-eac-to-move-mailboxes).
- **PowerShell**: Using PowerShell, you can move mailboxes from an on-premises organization to an Exchange Online organization, or from an Exchange Online organization to an on-premises organization. For more information, see [Use PowerShell to move mailboxes](move-mailboxes-using-powershell#use-powershell-to-move-mailboxes).