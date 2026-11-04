---
layout: Conceptual
title: Example 3 - Require that all emails are sent from a specific IP address range | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example3-security-restrictions-mail-sent-from-partner-organization
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
description: Example 3 - Security restrictions to mails sent from your partner organization to Microsoft 365 or Office 365.
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
document_id: 7c4e8ecb-7b3a-7c34-1727-fba08d272d3d
document_version_independent_id: 9639c2ef-177d-bdb7-4a6d-cdc3c0f38085
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example3-security-restrictions-mail-sent-from-partner-organization.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/example3-security-restrictions-mail-sent-from-partner-organization
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/example3-security-restrictions-mail-sent-from-partner-organization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 7de64f78-b8c9-af08-5950-130aae9c38f2
---

# Example 3 - Require that all emails are sent from a specific IP address range | Microsoft Learn

This email could be from a partner organization, such as ContosoBank.com, or from your on-premises environment. For instance, the MX record for your domain, contoso.com, points to on-premises, and you want all emails being sent to contoso.com to come from your on-premises IP addresses only. This condition helps prevent spoofing and ensures your compliance policies can be enforced for all messages.

To do this configuration, specify your partner organization domain name to identify mails from that partner, and then restrict the IP addresses that you accept mails from. Using an IP address makes the connector more specific because it identifies a single address or an address range that your partner organization sends mails from.

You can do this configuration in the New EAC and Classic EAC.

## New EAC

To do this configuration in the New EAC, perform the following procedure:

1. Enter your partner domain as described in [Example 1 - Require that email sent from your partner organization domain contosobank.com is encrypted using transport layer security (TLS)](example1-security-restrictions-mail-sent-from-partner-organization#example-1-require-that-email-sent-from-your-partner-organization-domain-contosobankcom-is-encrypted-using-transport-layer-security-tls).
2. Use the options as shown in the following screenshot:

![Screenshot that shows the screen on which email source IP address is set.](../../exchangeonline/media/receive-email-from-specific-ip-address.png)

## Classic EAC

To do this configuration in the Classic EAC, perform the following procedure:

1. Enter your partner domain as described in [Example 1 - Require that email sent from your partner organization domain contosobank.com is encrypted using transport layer security (TLS)](example1-security-restrictions-mail-sent-from-partner-organization#example-1-require-that-email-sent-from-your-partner-organization-domain-contosobankcom-is-encrypted-using-transport-layer-security-tls).
2. Use the options as shown in the following screenshot:

![Screenshot that shows to enter your partner organization's IP address range.](../../exchangeonline/media/3a6896f0-3a60-4ef7-91e1-7cf7f24a8bc4.png)

When you set these restrictions, all emails that are sent from your partner organization domain, ContosoBank.com, or from your on-premises environment will be from the IP address or an address range you specify. Any mail that doesn't meet these conditions will be rejected.