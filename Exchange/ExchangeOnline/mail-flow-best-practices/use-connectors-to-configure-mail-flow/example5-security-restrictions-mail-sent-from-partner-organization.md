---
layout: Conceptual
title: Example 5 - Require that all mail sent from your partner organization IP address or address range is encrypted using TLS | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example5-security-restrictions-mail-sent-from-partner-organization
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
description: Example 5 - Security restrictions to mails sent from your partner organization to Microsoft 365 or Office 365.
ms.topic: article
author: v-smandalika
ms.author: v-smandalika
ms.assetid: 1ce4d6a4-41ba-4d1e-9ca9-e826252c1041
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2023-10-20T00:00:00.0000000Z
locale: en-us
document_id: 80c7234a-1370-16e2-0fd4-b12ac053c14d
document_version_independent_id: 4edb8e75-e022-7136-130c-dd3878565fe2
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example5-security-restrictions-mail-sent-from-partner-organization.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/example5-security-restrictions-mail-sent-from-partner-organization
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example5-security-restrictions-mail-sent-from-partner-organization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 4f5ce836-60f6-3632-eba5-c01f0075c402
---

# Example 5 - Require that all mail sent from your partner organization IP address or address range is encrypted using TLS | Microsoft Learn

To identify your partner organization by IP address in the New EAC, use the options during setup as shown in the following screenshot:

![Screenshot that shows the screen on which the mails by partner organization are identified by IP address of the sender.](../../exchangeonline/media/identify-partner-by-ip-address.png)

Add the requirement for TLS encryption by using the following setting:

![Screenshot that shows the screen on which IP addresses by which Partner organization will be identified is set.](../../exchangeonline/media/configuring-receipt-from-specific-ip-address.png)

To identify your partner organization by IP address in the Classic EAC, use the options during setup as shown in the following screenshots:

![Screenshot that shows to choose the IP address to identify your partner organization.](../../exchangeonline/media/d5d54819-2e69-4f76-be37-ba701876beb6.png)

![Screenshot that shows to enter your partner organization's IP address.](../../exchangeonline/media/4ad3f410-e49b-4c92-82f5-8a8a6ab9535c.png)

Add the requirement for TLS encryption by using the following setting:

![Screenshot that shows to choose TLS to encrypt email from partner organization.](../../exchangeonline/media/0de0e09c-8420-419f-87fc-cf66f10098ec.png)

When you set these restrictions, all mails from your partner organization sent from the IP address or address range you specify must be sent using TLS. Any mail that doesn't meet this restriction will be rejected.