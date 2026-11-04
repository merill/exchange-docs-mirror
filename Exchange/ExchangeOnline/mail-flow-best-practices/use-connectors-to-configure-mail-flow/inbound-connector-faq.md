---
layout: Conceptual
title: Inbound connectors from on-premises organizations FAQ" | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/inbound-connector-faq
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.date: 2024-07-12T00:00:00.0000000Z
ms.localizationpriority: medium
ms.topic: faq
author: Benny-54
ms.author: serdars
ms.assetid: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords: 
description: The article covers the questions regarding inbound connectors.
locale: en-us
document_id: 6d5b90a7-8874-614b-7c2d-f9c0d6350f76
document_version_independent_id: eb65b260-ff18-e58c-77eb-f9fbdf2a400a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/inbound-connector-faq.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/inbound-connector-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/inbound-connector-faq.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 702a2536-b990-3f59-6176-72b1cce2df78
---

# Inbound connectors from on-premises organizations FAQ" | Microsoft Learn

**Summary**: This article covers the most common questions asked by the customers and administrators about using Inbound connectors from on-premises organizations in Exchange Online.

Inbound connectors from on-premises organizations are just one type of connector that's available in Office 365 or Microsoft 365 organizations with Exchange Online. For more information about connectors in Exchange Online, see [Configure mail flow using connectors in Exchange Online](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow).

Admins create Inbound connectors from on-premises organizations using any of the following methods:

- On the **Connectors** page in the Exchange admin center (EAC) at https://admin.exchange.microsoft.com/#/connectors with the following options:

    - **Connection from**: Select **Your organization's email server**
    - The unmodifiable **Connection to** value is **Office 365**.
- In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) using the [New-InboundConnector](/en-us/powershell/module/exchangepowershell/new-inboundconnector) cmdlet with the following settings:

    - **Parameter**: *ConnectorType*
    - **Value**: `OnPremises`
- The [Hybrid Configuration Wizard (HCW)](/en-us/exchange/hybrid-configuration-wizard). The inbound connector that's created by the HCW has the following settings:

    - **Name**: `Inbound from <TenantGUID>`
    - **ConnectorSource**: `HybridWizard`
    - **ConnectorType**: `OnPremises`

Inbound connectors from on-premises organizations are designed to support the following scenarios:

- Organizations that are still in Hybrid mode (send mail from their on-premises mailboxes to their Exchange Online mailboxes.
- On-premises mailboxes relaying email to the internet via Exchange Online.

Inbound connectors from on-premises organizations aren't designed to relay bulk email to the internet, so this activity is considered a misuse of the feature.

When you create or update an Inbound connector from an on-premises organization, you might see the following warning messages:

- "*Inbound connector for this service offering is created in a disabled state. Contact Support to enable it.*"
- "*For this service offering, you can't enable an inbound connector. Contact Support to enable it.*"

If you receive one of these errors, do the following steps:

1. Read this article to understand whether you need an Inbound connector from your on-premises organization.
2. If you believe your organization has a business justification for an Inbound connector from your on-premises organization, contact Microsoft Support with your business justification. Our service engineers will review your information. If approved, we'll enable the Inbound connector from your on-premises organization.

## FAQs

### Q: When do I need to create an Inbound connector of OnPremises type?

Typically, you don't need to manually create Inbound connectors from on-premises organizations. For more information, see [Configure mail flow using connectors in Exchange Online](use-connectors-to-configure-mail-flow).

### Q: I'm using a third party filtering service to filter emails from the internet for my organization. Do I need to create an Inbound connector of OnPremises type?

No. As long as you configure the third party service to deliver your messages using your organization's *.onmicrosoft.com* domain, your mail can be successfully delivered.

### Q: I'm using a third party add-on service to process emails that are composed by users of my Exchange Online organization before they're sent to the internet. I need to create an Inbound connector of OnPremises type to relay emails from the third party service for my organization. What do I need to do?

This scenario is valid for Inbound connectors from on-premises organizations. Follow the instructions in [Integrate Exchange Online with an email add-on service](integrate-office-365-with-an-email-add-on-service).

If you use the **New-InboundConnector** cmdlet in Exchange Online PowerShell to create the Inbound connector as described in [Step 4](integrate-office-365-with-an-email-add-on-service#step-4-create-a-connector-that-receives-messages-from-the-email-add-on-service), don't use the *SenderIPAddresses* parameter (ensure the `SenderIPAddresses` property value is empty on the connector). Only a unique certificate domain from the third party service is allowed and the domain must be an accepted domain in your organization.

If your organization provides the add-on service and your customers followed the instructions but still see a warning message, contact Microsoft support to address the issue.

### Q: Why do I see a warning message "Inbound connector for this service offering is created in a disabled state. Contact Support to enable it" when I try to create an Inbound Connector of OnPremiseType? What should I do, if my organization needs to create an Inbound Connector of OnPremises type?

These connectors are created as "Disabled" by default. Customers that experience this behavior must contact Microsoft support with a business justification to enable an Inbound connector of OnPremises type.

### Q: I'm running the Hybrid Configuration Wizard (HCW) and I see a warning message "Inbound Connectors created by HCW are in disabled state"? What do I need to do to enable the Inbound Connector by HCW?

You need to contact Microsoft support with a business justification to enable an Inbound connector of the type `OnPremises` for hybrid use within your Exchange Online organization.

### Q: Can I modify the HCW created connector `Inbound from <TenantGUID>` to use IP addresses versus certificates for their hybrid service connectors? Is this allowed?

No. Hybrid connectors are supported only with certificates, not with IP addresses.