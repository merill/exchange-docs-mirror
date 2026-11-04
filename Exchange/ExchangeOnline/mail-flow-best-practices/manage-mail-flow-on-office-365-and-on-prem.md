---
layout: Conceptual
title: Manage mail flow using a third-party cloud service with Exchange Online and on-premises mailboxes in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/manage-mail-flow-on-office-365-and-on-prem
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
description: Learn how to manage mail flow with a third-party cloud service in an Exchange hybrid environment (where your mailboxes are in both an on-premises organization and in Exchange Online).
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: fb335522-11ba-48d7-956f-2d980c22ab51
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 884ccdaf-c60f-293a-b7f7-b4edc559546c
document_version_independent_id: 6265a100-939a-75b3-d2ae-86798aaf79b4
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/manage-mail-flow-on-office-365-and-on-prem.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/manage-mail-flow-on-office-365-and-on-prem
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/manage-mail-flow-on-office-365-and-on-prem.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 5f78ee4d-2a8c-5baa-c7d9-e26641e01a40
---

# Manage mail flow using a third-party cloud service with Exchange Online and on-premises mailboxes in Exchange Online | Microsoft Learn

This topic covers the most complex mail flow scenario using Microsoft 365 or Office 365.

Note

Examples in this guide use the fictitious organization, Contoso, which owns the domain contoso.com. The IP address of the Contoso mail server is 131.107.21.231, and its third-party provider uses 10.10.10.1 for their IP address. These are just examples. You can adapt these examples to fit your organization's domain name and public-facing IP address where necessary.

## Using a third-party cloud service with mailboxes in Exchange Online and on my organization's email servers

### Scenario

- I'm migrating my mailboxes to Exchange Online, and I want to keep some mailboxes on my organization's on-premises email server. I want to use a third-party cloud service to filter spam from the internet. My messages to the internet must route through Microsoft 365 or Office 365 to prevent my on-premises servers' IP addresses from being added to external block lists.

In this scenario, your organization's mail flow setup looks like the following diagram.

![Mail flow diagram showing mail from the internet going to a third-party service then to Microsoft 365 or Office 365 and then to on-premises servers. Mail from on-premises servers goes to Microsoft 365 or Office 365 then to the internet (bypassing the third-party service).](../exchangeonline/media/fc2c46f3-a1e4-45b7-845b-ff6197113673.png)

#### Best practices

1. Add your custom domains in Microsoft 365 or Office 365. To prove that you own the domains, follow the instructions in [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).
2. [Create user mailboxes in Exchange Online](../recipients-in-exchange-online/create-user-mailboxes) or [move all users' mailboxes to Microsoft 365 or Office 365](../mailbox-migration/mailbox-migration).
3. Update the DNS records for the domains that you added in step 1. (Not sure how to do this? Follow the instructions on [this page](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).) The following DNS records control mail flow:

    - **MX record**: Point your MX record to your third-party service. Follow their guidelines for configuring your MX record.
    - **SPF record**: Because your domain's MX record must point to a third-party service (in other words, you require complex routing), include the third-party service in your SPF record. Follow the third-party provider's guidelines for adding them to your SPF record. Also add Microsoft 365 or Office 365 and the IP addresses of your on-premises servers as valid senders. For example, if contoso.com is your domain name, the third-party cloud service IP address is 10.10.10.1, and your on-premises server IP address is 131.107.21.231, the SPF record for contoso.com should be:

    ```text
    v=spf1 ip4:10.10.10.1 ip4:131.107.21.231 include:spf.protection.outlook.com -all
    ```

    Alternatively, depending on the third-party's requirements, you might need to include the domain from the third-party, as shown in the following example:

    ```text
    v=spf1 ip4:131.107.21.231 include:spf.protection.outlook.com include:third_party_cloud_service.com -all
    ```

### More information

There are additional considerations in hybrid deployments between on-premises Exchange and Microsoft 365 or Office 365. For more information, see [Exchange Server hybrid deployments](../exchange-hybrid).