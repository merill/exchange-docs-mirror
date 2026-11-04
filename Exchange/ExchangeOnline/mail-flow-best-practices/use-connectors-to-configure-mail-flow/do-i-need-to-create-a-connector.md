---
layout: Conceptual
title: Do I need to create a connector in Exchange Online? in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/do-i-need-to-create-a-connector
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Find your mail flow scenario to see if you need to create a connector for your cloud-based organization.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 16731ae9-c909-49dd-bffc-a46e6151fc29
ms.reviewer: 
f1.keywords:
- CSH
ms.custom:
- ms.exch.eac.ConnectorIsConnectorNeeded
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: b285591c-809d-16f4-bf04-f0eed48a508c
document_version_independent_id: 86ad8ac9-3bf6-0e6c-64f3-db5b5d51af96
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/do-i-need-to-create-a-connector.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/do-i-need-to-create-a-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/do-i-need-to-create-a-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: d0cd16be-04ed-6b0c-c581-6326dfc9ff38
---

# Do I need to create a connector in Exchange Online? in Exchange Online | Microsoft Learn

Find your mail flow scenario to see if you need to create a connector for your cloud-based organization.

| Scenario | Description | Connector required? | Connector settings |
| --- | --- | --- | --- |
| You have licenses for the Built-in security add-on for on-premises mailboxes. | You have your own on-premises email servers, and you built-in security features in the cloud for your on-premises mailboxes (and you have no cloud mailboxes).  For more information, see [Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/standalone-eop) and [How connectors work with my on-premises email servers](use-connectors-to-configure-mail-flow#how-connectors-work-with-my-on-premises-email-servers). | Yes | **Connector for incoming email:**<br>- **From**: Your on-premises email server<br>- **To**: Office 365<br><br>**Connector for outgoing email**: <br>- **From**: Office 365<br>- **To**: Your on-premises mail server |
| Some of your mailboxes are on your on-premises email servers, and some are in Exchange Online. | Before you manually configure connectors, check whether an Exchange hybrid deployment better meets your business needs.  For details, see [I have my own email servers](use-connectors-to-configure-mail-flow#i-have-my-own-email-servers) and [Exchange Server Hybrid Deployments](../../exchange-hybrid). | Yes | **Connector for incoming email:**<br>- **From**: Your on-premises email server<br>- **To**: Office 365<br><br>**Connector for outgoing email:**<br>- **From**: Office 365<br>- **To**: Your on-premises email server |
| All of your mailboxes are in Exchange Online, but you need to send email from sources in your on-premises organization. | You don't have your own email servers, but you need to send email from non-mailboxes: printers, fax machines, apps, or other devices.  For details, see [SMTP relay: Configure a connector to relay email from your device or application through Microsoft 365 or Office 365](../how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365#smtp-relay-configure-a-connector-to-relay-email-from-your-device-or-application-through-microsoft-365-or-office-365) | Optional | **Only one connector for incoming email:**<br>- **From**: Your organization's email server<br>- **To**: Office 365 |
| You frequently exchange sensitive information with business partners, and you want to apply security restrictions. | You want to use Transport Layer Security (TLS) to encrypt sensitive information or you want to limit the source (IP addresses) for email from the partner domain.  For details, see [Set up connectors for secure mail flow with a partner organization](set-up-connectors-for-secure-mail-flow-with-a-partner). | Optional | **Connector for incoming email:**<br>- **From**: Partner organization<br>- **To**: Office 365<br><br>**Connector for outgoing email:**<br>- **From**: Office 365<br>- **To**: Partner organization |

Note

For more information about these scenarios, see [Configure mail flow using connectors in Office 365](use-connectors-to-configure-mail-flow).