---
layout: Conceptual
title: Troubleshoot mail flow in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/troubleshoot-mail-flow
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
ms.author: serdars
ms.topic: troubleshooting-general
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: ccb62ce1-a822-4859-a0db-3d546c5c1f50
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
description: Admins can learn about the mail flow troubleshooting options in Microsoft 365 or Office 365.
audience: ITPro
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: f9108de4-e74c-0d0f-a380-0a9a8a2f0b22
document_version_independent_id: 51dc0b18-03e3-e9e2-d427-e559e56e10a1
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/troubleshoot-mail-flow.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/troubleshoot-mail-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/troubleshoot-mail-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 5dab61e1-031e-0ff7-b88b-c0ef3261523d
---

# Troubleshoot mail flow in Exchange Online | Microsoft Learn

Can't send or receive email? Microsoft 365 and Office 365 for business offer admins several ways to troubleshoot. We recommend using the automated solutions because they're typically easier and faster than manual troubleshooting.

For instructions about troubleshooting options, see [Find and fix email delivery issues as a Microsoft 365 or Office 365 for business admin](/en-us/exchange/troubleshoot/mail-delivery/email-delivery-issues).

## Troubleshoot mail flow caused by connectors

To validate and troubleshoot mail flow from Microsoft 365 or Office 365 to the email servers in your on-premises organization (also called the on-premises server), validate your connectors. You can set up and validate connectors on the **Connectors** page in the Exchange admin center (EAC). The built-in validation tests that your mail flow from Microsoft 365 or Office 365 reaches:

- Your organization's email server
- A partner organization.

For more information, see [Validate connectors](use-connectors-to-configure-mail-flow/validate-connectors).

## Troubleshoot mail flow issues caused by incorrect SPF records or MX records

[How Microsoft 365 uses Sender Policy Framework (SPF) to prevent spoofing](/en-us/defender-office-365/email-authentication-spf-configure#troubleshooting-spf-txt-records) gives tips on how to fix several SPF record errors. The beginning of that article also provides an explanation of what SPF records are and how Microsoft 365 and Office 365 use them to prevent spoofing.

Mail flow issues can also happen when your MX record isn't set up correctly. To verify your MX record, see [Find and fix issues after adding your domain or DNS records](/en-us/microsoft-365/admin/get-help-with-domains/find-and-fix-issues).

## Troubleshoot mail flow with thirty-party service

If you're a service provider for Office 365 customers and also an Office 365 customer, then ensure that you don't create an inbound connector of on-premises type using a certificate domain that's same as any of your customers use to send email to Office 365.

For example, if you're Contoso service provider that offers a filtering service for some Office 365 customers, you route emails to Office 365 after you processed them. For this route, you use a TLS certificate with domain name (or SAN) *ContosoService.com*. However, Contoso service is also an Office 365 customer, your firm needs to relay emails to Office 365. In this route, don't use certificate domain *ContosoService.com*, and don't create an inbound connector using this certificate domain *ContosoService.com*. This misconfiguration could cause mail loop for your customers. You must relay your firm's email using a different certificate and configure that certificate domain in the connector.

## For more information

[Mail flow best practices for Exchange Online and Microsoft 365 or Office 365 (overview)](mail-flow-best-practices)

[Mail flow in cloud organizations](/en-us/defender-office-365/mail-flow-about)