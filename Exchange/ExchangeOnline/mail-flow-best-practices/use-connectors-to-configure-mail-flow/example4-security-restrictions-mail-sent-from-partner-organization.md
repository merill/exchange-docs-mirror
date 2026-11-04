---
layout: Conceptual
title: Example 4 - Require that all email sent to your organization from the internet is sent from a specific IP address (third-party email service scenario) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example4-security-restrictions-mail-sent-from-partner-organization
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
description: Example 4 - Security restrictions to mails sent from your partner organization to Microsoft 365 or Office 365.
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
document_id: 4d310aaf-b49d-bc87-b3ee-0617debf71b6
document_version_independent_id: e11a447a-152d-137a-3312-8455f31e933a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example4-security-restrictions-mail-sent-from-partner-organization.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/example4-security-restrictions-mail-sent-from-partner-organization
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example4-security-restrictions-mail-sent-from-partner-organization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 1af1606e-945c-b372-a98f-97dc6dc80900
---

# Example 4 - Require that all email sent to your organization from the internet is sent from a specific IP address (third-party email service scenario) | Microsoft Learn

Mail flow from a third-party email service to Microsoft 365 or Office 365 works without a connector. However, in this scenario, you can optionally use a connector to restrict all mail delivery to your organization. If you use the settings described in this example, they'll apply to *all email sent to your organization*. When all emails sent to your organization come from a single third-party email service, you can optionally use a connector to restrict all mail delivery; only mails sent from a single IP address or address range will be delivered.

Note

Ensure you identify the full range of IP addresses that your third-party email service sends mails from. If you miss an IP address, or if one gets added without your knowledge, some mails won't be delivered to your organization.

You can apply this restriction in the New EAC and Classic EAC.

## New EAC

In the New EAC, to restrict all mails sent to your organization from a specific IP address or address range, use the options during setup as shown in the following screenshots:

![Screenshot that shows the screen on which there's a configuration to apply the settings globally.](../../exchangeonline/media/specific-internet-ip-address.png)

![Screenshot that shows the screen on which the your partner organization's IP address range is defined](../../exchangeonline/media/configuring-receipt-from-specific-ip-address.png)

## Classic EAC

In the Classic EAC, to restrict all mails sent to your organization from a specific IP address or address range, use the options during setup as shown in the following screenshots:

![Screenshot that shows to choose to use the sender's domain name.](../../exchangeonline/media/3b3b0cc6-3928-4cab-a022-436821f9d559.png)

![Screenshot that shows to enter &quot;*&quot; to apply settings to all sender domains.](../../exchangeonline/media/1be173e2-1c57-4d5d-9bb7-f353c1c29e1f.png)

![Screenshot that shows to enter your partner organization's IP address range.](../../exchangeonline/media/3a6896f0-3a60-4ef7-91e1-7cf7f24a8bc4.png)

When you set these restrictions, all mails sent to your organization will be from a specific IP address range. Any internet email that doesn't originate from this IP address range will be rejected.