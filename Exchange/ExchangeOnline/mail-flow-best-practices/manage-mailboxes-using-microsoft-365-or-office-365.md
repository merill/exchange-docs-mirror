---
layout: Conceptual
title: Manage all mailboxes and mail flow using Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/manage-mailboxes-using-microsoft-365-or-office-365
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
description: 'Summary: How to use hosted mail flow with Microsoft 365 or Office 365.'
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 24cac303-c8de-474b-a894-e42683db30f1
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
audience: ITPro
ms.service: exchange-online
ms.date: 2020-06-23T00:00:00.0000000Z
locale: en-us
document_id: f0dc340e-a9e5-508f-cc45-03ecbdcbdebe
document_version_independent_id: 09c756cd-8e86-b303-047a-832f2f22cb9c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/manage-mailboxes-using-microsoft-365-or-office-365.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/manage-mailboxes-using-microsoft-365-or-office-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/manage-mailboxes-using-microsoft-365-or-office-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: b03526ac-06e8-472e-18c2-28831562a9d9
---

# Manage all mailboxes and mail flow using Microsoft 365 or Office 365 | Microsoft Learn

**Summary**: How to use hosted mail flow with Microsoft 365 or Office 365.

For most organizations, we recommend using hosted mail flow because it's the simplest configuration, in which Microsoft 365 or Office 365 manages all mailboxes and filtering. This simple configuration makes it easy to set up and manage mail flow.

## Manage all mailboxes and mail flow using Microsoft 365 or Office 365 (recommended)

### Hosted mail flow scenarios

- I'm a new Microsoft 365 or Office 365 customer, and all my users' mailboxes are in Microsoft 365 or Office 365. I want to use all filtering solutions that Office 365 offers.
- I'm a new Microsoft 365 or Office 365 customer. I have an existing email service, but I plan to immediately move all existing mailboxes to the cloud. I want to use all filtering solutions that Microsoft 365 and Office 365 offer.

For this scenario, your organization's mail flow setup looks like the following diagram:

![Mail flow diagram showing mail going from the internet to Microsoft 365 or Office 365, and from Microsoft 365 or Office 365 to the internet.](../exchangeonline/media/96ec9aca-fa95-4307-a992-479a1ed65e5c.png)

#### Best practices for hosted mail flow scenarios

To set up hosted mail flow, we recommend using the Microsoft 365 setup wizard. To get to the Microsoft 365 setup wizard, go to **Setup** in the Microsoft 365 admin center.

![interface of Microsoft 365 Admin center.](../exchangeonline/media/ms-365-admin-center.png)

The Microsoft 365 setup wizard walks you through the following steps.

1. Add your custom domains in Microsoft 365 or Office 365. To prove that you own the domains, follow the instructions in [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain).
2. [Create user mailboxes in Exchange Online](../recipients-in-exchange-online/create-user-mailboxes) or [move all users' mailboxes to Microsoft 365 or Office 365](../mailbox-migration/mailbox-migration).
3. Update the DNS records for the domains that you added in step 1. (Not sure how to do this task? Follow the instructions on [this page](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).)

    The following DNS records control mail flow:

    - **MX record** - Point your MX record to Microsoft 365 or Office 365 in the following format: &lt;domainKey&gt;.mail.protection.outlook.com.

    For example, the domain contoso.com should have the MX record contoso-com.mail.protection.outlook.com.

    - **SPF record** - This record is a special TXT record in DNS that identifies a service as a valid sender for a particular domain. Because Microsoft 365 and Office 365 are sending all your messages, list only Microsoft 365 or Office 365 as a valid sender for your domain. To do that, add an SPF record for your domain in the following format:

    ```text
    v=spf1 include:spf.protection.outlook.com -all
    ```

For a full list of setup instructions, check out [Set up Microsoft 365 for business](/en-us/microsoft-365/admin/setup/setup) or [Deploy Office 365 Enterprise for your organization](/en-us/office365/enterprise/setup-overview-for-enterprises).