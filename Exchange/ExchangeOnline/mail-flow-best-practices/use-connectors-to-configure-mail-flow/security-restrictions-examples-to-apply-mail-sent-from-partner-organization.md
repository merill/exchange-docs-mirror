---
layout: Conceptual
title: examples of connector configurations for securing email exchange between Microsoft 365 or Office 365 and your partner organization | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/security-restrictions-examples-to-apply-mail-sent-from-partner-organization
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
description: This topic describes a few examples of connector configuration for securing email exchange between Microsoft 365 or Office 365 and your partner organization.
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
document_id: 65292125-8420-d51d-6d57-e94fce889194
document_version_independent_id: c6f76c5d-b065-6c83-3993-8e81bdc1eb7d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/security-restrictions-examples-to-apply-mail-sent-from-partner-organization.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/security-restrictions-examples-to-apply-mail-sent-from-partner-organization
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/security-restrictions-examples-to-apply-mail-sent-from-partner-organization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 01375a97-ce87-5789-149b-424dc90e2b98
---

# examples of connector configurations for securing email exchange between Microsoft 365 or Office 365 and your partner organization | Microsoft Learn

Review these connector examples to help you decide whether you want to apply security restrictions to emails sent by a partner organization, and understand what settings will meet your business needs:

## Create a partner organization connector

**For New EAC**:

For information on this procedure, see the [For New EAC](set-up-connectors-to-secure-mail-sent-from-partner-organization#for-new-eac)

**For Classic EAC**:

From the new EAC portal, navigate to the Classic EAC portal by selecting **Classic Exchange admin center**. Then, choose **mail flow &gt; connectors**.

To start the wizard, click **+**. To create a connector for emails you receive from a partner organization, use the options depicted in the following screenshot:

![Screenshot that shows connector from partner organization to Microsoft 365 or Office 365.](../../exchangeonline/media/e6d15001-989b-48b3-a848-427b800c2a70.png)

Once you choose this mail flow scenario, you can set up a connector that will apply security restrictions to emails that your partner organization sends to you. For some security restrictions, you might need to talk to your partner organization to obtain information to complete some settings. Look for the examples that best meet your needs to help you set up your partner connector.

For information on the examples that you can analyze to determine the one that best meets your needs, see:

- [Example 1: Require that email sent from your partner organization domain contosobank.com is encrypted using transport layer security (TLS)](example1-security-restrictions-mail-sent-from-partner-organization#example-1-require-that-email-sent-from-your-partner-organization-domain-contosobankcom-is-encrypted-using-transport-layer-security-tls)
- [Example 2: Require that email sent from your partner organization domain ContosoBank.com is encrypted and uses their domain certificate](example2-security-restrictions-mail-sent-from-partner-organization#example-2-require-that-email-sent-from-your-partner-organization-domain-contosobankcom-is-encrypted-and-uses-their-domain-certificate)
- [Example 3: Require that all emails are sent from a specific IP address range](example3-security-restrictions-mail-sent-from-partner-organization#example-3-require-that-all-emails-are-sent-from-a-specific-ip-address-range)
- [Example 4: Require that all email sent to your organization from the internet is sent from a specific IP address (third-party email service scenario)](example4-security-restrictions-mail-sent-from-partner-organization#example-4-require-that-all-email-sent-to-your-organization-from-the-internet-is-sent-from-a-specific-ip-address-third-party-email-service-scenario)
- [Example 5: Require that all mail sent from your partner organization IP address or address range is encrypted using TLS](example5-security-restrictions-mail-sent-from-partner-organization#example-5-require-that-all-mail-sent-from-your-partner-organization-ip-address-or-address-range-is-encrypted-using-tls)

Note

Any email sent from your partner organization which doesn't meet security restrictions that you specify won't be delivered.