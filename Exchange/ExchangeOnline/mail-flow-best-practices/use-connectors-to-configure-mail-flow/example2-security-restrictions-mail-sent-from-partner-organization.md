---
layout: Conceptual
title: Example 2 - Require that email sent from your partner organization domain ContosoBank.com is encrypted and uses their domain certificate | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example2-security-restrictions-mail-sent-from-partner-organization
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
description: Example 2 - Security restrictions to mails sent from your partner organization to Microsoft 365 or Office 365.
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
document_id: 0ba2e1c2-9160-6be6-f4f8-fcfce1f73e26
document_version_independent_id: bed8dbd9-0bdb-a768-b2b7-b1dd7109ede6
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example2-security-restrictions-mail-sent-from-partner-organization.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/example2-security-restrictions-mail-sent-from-partner-organization
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example2-security-restrictions-mail-sent-from-partner-organization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: bec05ee1-1e67-0bd2-cd6d-464ea53475b5
---

# Example 2 - Require that email sent from your partner organization domain ContosoBank.com is encrypted and uses their domain certificate | Microsoft Learn

This configuration can be done in the New EAC and in the Classic EAC.

## New EAC

To do this configuration in the New EAC, perform the following steps:

1. Use all the settings shown in [Example 1 - Require that email sent from your partner organization domain contosobank.com is encrypted using transport layer security (TLS)](example1-security-restrictions-mail-sent-from-partner-organization#example-1-require-that-email-sent-from-your-partner-organization-domain-contosobankcom-is-encrypted-using-transport-layer-security-tls).
2. Add the certificate domain name that your partner organization uses to connect with Microsoft 365 or Office 365.

![Screenshot that shows the screen on which encryption is done using the domain certificate name.](../../exchangeonline/media/encryption-using-certificate-new-eac.png)

## Classic EAC

To do this configuration in the Classic EAC, perform the following steps:

1. Use all the settings shown in [Example 1 - Require that email sent from your partner organization domain contosobank.com is encrypted using transport layer security (TLS)](example1-security-restrictions-mail-sent-from-partner-organization#example-1-require-that-email-sent-from-your-partner-organization-domain-contosobankcom-is-encrypted-using-transport-layer-security-tls).
2. Add the certificate domain name that your partner organization uses to connect with Microsoft 365 or Office 365.

![Screenshot that shows to enter your partner organization certificate name.](../../exchangeonline/media/46229d66-dcfd-4e3d-bc12-9f53a5572f81.png)

When you set these restrictions, all mails from your partner organization domain must be encrypted using TLS, and sent from a server with the certificate name you specify. Any email that doesn't meet these conditions will be rejected.