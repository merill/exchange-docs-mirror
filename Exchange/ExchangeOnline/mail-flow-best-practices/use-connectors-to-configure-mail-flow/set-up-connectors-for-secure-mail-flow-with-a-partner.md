---
layout: Conceptual
title: Set up connectors for secure mail flow with a partner organization in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-for-secure-mail-flow-with-a-partner
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
description: You can create connectors to apply security restrictions to mail exchanges with a partner organization. A partner can be an organization you do business with, such as a bank. It can also be a third-party cloud service that provides services such as archiving, anti-spam, and filtering.
ms.topic: install-set-up-deploy
author: AshaIyengar21
ms.author: serdars
ms.assetid: 1ce4d6a4-41ba-4d1e-9ca9-e826252c1041
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 2bfe7d75-e6b7-1e78-7978-5c84dcced8b1
document_version_independent_id: f41c0a31-2ae9-1ed6-5eea-40722f3bae6c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-for-secure-mail-flow-with-a-partner.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-for-secure-mail-flow-with-a-partner
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-for-secure-mail-flow-with-a-partner.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/486161dc-fa28-4625-9b1c-1a21d690bc8d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/5dd28c86-729c-4723-ab5a-57e26fcec2a8
platformId: b96a36ef-4684-ef88-5770-ece3bfd75bcd
---

# Set up connectors for secure mail flow with a partner organization in Exchange Online | Microsoft Learn

You can create connectors to apply security restrictions to mail exchanges with a partner organization. A partner can be an organization you do business with, such as a bank. It can also be a third-party cloud service that provides services such as archiving, anti-spam, and filtering.

You can create a connector to enforce encryption via transport layer security (TLS). You can also apply other security restrictions such as specifying domain names or IP address ranges that your partner organization sends mail from.

Note

Setting up a connector to exchange mail with a partner organization is optional; mail flows to and from your partner organization occur without connectors.

If email messages don't meet the security restrictions that you specify, the messages will be rejected.

For more information on setting up, using, and managing connectors for mails exchange, see:

- [Set up a connector to apply security restrictions to mail sent from Microsoft 365 or Office 365 to your partner organization](set-up-connectors-to-secure-mail-sent-to-partner-organization#set-up-a-connector-to-apply-security-restrictions-to-mail-sent-from-microsoft-365-or-office-365-to-your-partner-organization)
- [Set up a connector to apply security restrictions to mail sent from your partner organization to Microsoft 365 or Office 365](set-up-connectors-to-secure-mail-sent-from-partner-organization#set-up-a-connector-to-apply-security-restrictions-to-mail-sent-from-your-partner-organization-to-microsoft-365-or-office-365)
- [Change a connector that Microsoft 365 or Office 365 is using for mail flow](change-connector-used-by-m365-o365-for-mail-flow#change-a-connector-that-microsoft-365-or-office-365-is-using-for-mail-flow)
- [Examples of connector configurations for securing email exchange between Microsoft 365 or Office 365 and your partner organization](security-restrictions-examples-to-apply-mail-sent-from-partner-organization#examples-of-connector-configurations-for-securing-email-exchange-between-microsoft-365-or-office-365-and-your-partner-organization)

If you use a third-party cloud service for email filtering and need instructions for making this work with Microsoft 365 or Office 365, see [Mail flow best practices for Exchange Online and Microsoft 365 or Office 365 (overview)](../mail-flow-best-practices).