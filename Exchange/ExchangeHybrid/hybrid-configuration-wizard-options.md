---
layout: Conceptual
title: Hybrid Configuration wizard options | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-configuration-wizard-options
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
ms.topic: article
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
ms.assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms.reviewer: 
description: Overview of Exchange hybrid configuration wizard options
ms.date: 2026-10-13T00:00:00.0000000Z
locale: en-us
document_id: 733b2020-e22b-05ca-5d43-a4a216177477
document_version_independent_id: 920a7ac4-5f25-f59c-51cf-a7776b2c5420
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-configuration-wizard-options.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-configuration-wizard-options
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-configuration-wizard-options.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: bafbee46-c314-07de-b9e2-50f7b6910d43
---

# Hybrid Configuration wizard options | Microsoft Learn

The Hybrid Configuration wizard (HCW) changed a lot since it was released as part of Exchange 2010 Service Pack 2. Currently, it supports a Classic Topology (Minimal, Express, and Full), and a Modern Topology (Minimal and Full). The following table shows the differences between the available options.

Note

This table is an expanded version of table originally published in Chapter 13 in the book, "Microsoft Office 365 Administration Inside Out, 2nd Edition." Reference- Fisher, Ed; Guilmette, Aaron; Kegg, Darryl; Mandich, Lou. Microsoft Office 365 Administration Inside Out (Includes Current Book Service), 2nd ed. Pearson Education, Inc., 2017. Print.

| Exchange Hybrid Configuration options | ClassicMinimal | ClassicExpress | ClassicFull | ModernMinimal | ModernFull |
| --- | --- | --- | --- | --- | --- |
| Email Address Policy and Domain configuration | Yes | Yes | Yes | Yes | Yes |
| Send and Receive Connector Configuration | No | No | Yes | No | Yes |
| OAuth Configuration | No | No | Yes¹ | No | Yes¹ |
| Dedicated Exchange Server Application in Entra ID | No | No | Yes | No | Yes |
| Organization Relationship Configuration | No | No | Yes | No | Yes |
| Federation Trust Configuration for Exchange 2010 or earlier | No | No | No | No | No |
| MRS Endpoint Configuration | Yes | Yes | Yes | Yes | Yes |
| Microsoft Entra Connect in Express Configuration | No | Yes | No; set up separately | No; set up separately | No; set up separately |
| Organization Configuration Transfer | Yes | Yes | Yes | Yes | Yes |
| Hybrid Modern Authentication | No | No | No² | No | No |
| Cross-premises multi mailbox search | No | No | Yes | No | No |
| Cross-premises Mail Tips | No | No | Yes | No | Yes |
| Autodiscover external DNS and public certificate required | Yes | Yes | Yes | Yes³ | Yes³ |
| Transport external DNS and public certificate required | No | No | Yes | No | Yes |
| EWS external DNS and public certificate required | Yes | Yes | Yes | No | No |
| TCP Port 443 Inbound to Exchange On-premises | Yes | Yes | Yes | - Yes for Autodiscover (if needed)<br>- No for Hybrid Agent | - Yes for Autodiscover (if needed)<br>- No for Hybrid Agent |
| TCP Port 443 Outbound to Exchange Online | Yes | Yes | Yes | Yes | Yes |
| TCP Port 25 Inbound to Exchange on-premises | No | No | Yes | No | Yes |
| TCP Port 25 Outbound to Microsoft 365 | No | No | Yes | No | Yes |
| TCP Port 80 Outbound for Certificate Revocation Check | Yes | Yes | Yes | Yes | Yes |
| Third-Party Certificate Required- Autodiscover/Transport/EWS for Exchange on-premises, Exchange Server 2013/2016/2019 | Yes | Yes | Yes | - Yes for Autodiscover (if needed)<br>- No for Hybrid Agent | - Yes for Autodiscover (if needed)<br>- Yes for Transport (if needed)<br>- No for Hybrid Agent |
| Exchange Server Edge 2013/2016/2019 with Edge Sync and Edge Third-Party Certificate for Transport Option, TCP Port 25 in/out at network egress | No | No | Yes | No | Yes |
| Exchange Server Edge 2013/2016/2019 without Edge Sync and Edge Third-Party Certificate for Transport Option, TCP Port 25 in/out at network egress | No | No | No | No | No |

Note

Federation Trust configuration is no longer available in HCW.

- ¹ Requires Exchange 2013 or later with current Cumulative Updates (CUs), Security Updates (SUs), and Hotfix Updates (HUs).
- ² The Hybrid Configuration wizard provides the foundational components to prepare the environment for Hybrid Modern Authentication. The extra steps to complete the process for Hybrid Modern Authentication are described in [How to configure Exchange Server on-premises to use Hybrid Modern Authentication](/en-us/microsoft-365/enterprise/configure-exchange-server-for-hybrid-modern-authentication).
- ³ Depending on the topology and configuration, you might still need to publish Autodiscover records in external DNS or open TCP Port 25 inbound and outbound to your Exchange environment. For example:

    - Exchange ActiveSync Clients using the legacy mail client in Android or iOS (although we highly recommend Microsoft Outlook for iOS and Android as the mobile messaging application).
    - Using a feature like Exchange Server Hybrid Modern Authentication.

    Be sure to review the limitations of the hybrid agent and modern hybrid topology covered in the article [Microsoft Hybrid Agent](hybrid-deployment/hybrid-agent).