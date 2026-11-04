---
layout: Conceptual
title: Example 1 - Require that email sent from your partner organization domain contosobank.com is encrypted using transport layer security (TLS) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example1-security-restrictions-mail-sent-from-partner-organization
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
description: Example 1 - Security restrictions to mails sent from your partner organization to Microsoft 365 or Office 365.
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
document_id: 6e9dcabf-6448-1120-cac1-66a2c32606d0
document_version_independent_id: 6b5ec032-0aab-6497-bf0c-6c465f59c6d7
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example1-security-restrictions-mail-sent-from-partner-organization.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/example1-security-restrictions-mail-sent-from-partner-organization
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example1-security-restrictions-mail-sent-from-partner-organization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 77dcdb55-7ad6-7a34-2b13-b2c021880257
---

# Example 1 - Require that email sent from your partner organization domain contosobank.com is encrypted using transport layer security (TLS) | Microsoft Learn

To do this configuration, specify your partner organization domain name to identify mails from that partner, and then choose transport layer security (TLS) encryption when you create the connector for mail flow from your partner to Microsoft 365 or Office 365.

During setup of the connector in the New EAC, use the options as shown in the following screenshots:

![Screenshot that shows the screen on which TLS encryption is done.](../../exchangeonline/media/connector-partner-to-365-encryption-tls.png)

Use the screen shown in the following screenshot to enter your partner organization's domain name(s) so that the connector can identify mails sent by your partner:

![Screenshot that shows the screen on which the domain name is set.](../../exchangeonline/media/domain-name-partner-to-365-encryption-tls.png)

Choose the setting shown in the following screenshot to require encryption for all emails from ContosoBank.com using TLS:

![Screenshot that shows the screen on which the mandatory TLS encryption is configured.](../../exchangeonline/media/requiring-tls-encryption.png)

During setup of the connector in the Classic EAC, use the options as shown in the following screenshots:

![Screenshot that shows to choose to use the sender's domain name.](../../exchangeonline/media/3b3b0cc6-3928-4cab-a022-436821f9d559.png)

Use the screen shown in the following screenshot to enter your partner organization's domain name(s) so that the connector can identify mails sent by your partner:

![Screenshot that shows to add partner organization domain name.](../../exchangeonline/media/6ea7db5c-71ff-41cb-bfcd-89be4106f7e1.png)

Choose the setting shown in the following screenshot to require encryption for all emails from ContosoBank.com using TLS:

![Screenshot that shows choose TLS to encrypt email from partner organization.](../../exchangeonline/media/0de0e09c-8420-419f-87fc-cf66f10098ec.png)

When you choose these settings, all emails from your partner organization's domain, ContosoBank.com, must be encrypted using TLS. Any mail that's not encrypted will be rejected.