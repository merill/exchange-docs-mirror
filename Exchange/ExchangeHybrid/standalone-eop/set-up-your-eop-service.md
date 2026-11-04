---
layout: Conceptual
title: Set up the Built-in security add-on for on-premises mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/standalone-eop/set-up-your-eop-service
Manager: deniseb
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: chrisda
author: chrisda
ms.date: 2024-05-16T00:00:00.0000000Z
audience: ITPro
ms.topic: how-to
ms.custom:
- seo-marvel-apr2020
ms.localizationpriority: medium
ms.assetid: d74c6ddf-11b0-43ee-b298-8bb0340895f0
description: Admins in on-premises organizations that use the Built-in security add-on for on-premises mailboxes can learn how to set up the add-on.
ms.service: exchange-online
locale: en-us
document_id: 85d2ac2b-2ba4-a1e5-d3a6-cec505fb2e72
document_version_independent_id: 82fdc5d5-b9c3-b377-1e0c-e04ee41c65ec
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/standalone-eop/set-up-your-eop-service.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standalone-eop/set-up-your-eop-service
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/standalone-eop/set-up-your-eop-service.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: d96b71bd-b7c2-1a3d-bd45-705f6d0b086d
---

# Set up the Built-in security add-on for on-premises mailboxes | Microsoft Learn

If you use the Built-in security add-on for on-premises mailboxes, this article explains how to set up the add-on.

If you landed here from the Office 365 domains wizard, go back to the Office 365 domains wizard if you don't want to use the add-on.

If you're looking for more information on how to configure connectors, see [Configure mail flow using connectors in Office 365](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow).

Note

Hosting mailboxes in the cloud and in on-premises Exchange is known as a *hybrid deployment*. Hybrid deployments require advanced mail-flow settings. For more information, see [Exchange Server hybrid deployments](../exchange-hybrid).

## What do you need to know before you begin?

- Estimated time to complete this task: One hour
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo): You need the **Remote and Accepted Domains** role, which is assigned to the **Organization Management** and **Mail Flow Administrator** role groups by default.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator** role.

        Important

        Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.
- If you aren't already signed up for the Built-in security add-on for on-premises mailboxes, visit the [Exchange Online Protection product page](https://products.office.com/exchange/exchange-email-security-spam-protection) and choose to buy or try the service.
- For information about keyboard shortcuts that might apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center in Exchange Online](/en-us/Exchange/accessibility/keyboard-shortcuts-in-admin-center).

## Step 1: Use the Microsoft 365 admin center to add and verify your domain

1. In the Microsoft 365 admin center at https://admin.microsoft.com, go to **Setup** &gt; **Get your custom domain set up** to add your domain to the service.
2. Follow the steps to add the applicable DNS records to your DNS-hosting provider in order to verify domain ownership.

[Add a domain to Office 365](/en-us/microsoft-365/admin/setup/add-domain) and [Create DNS records at any DNS hosting provider for Office 365](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider) are helpful references as you add your domain to the service and configure DNS.

## Step 2: Add recipients and optionally enable DBEB

Before configuring your mail to flow to and from the cloud, we recommend adding your recipients to the service. There are different was to add recipients as documented in [Manage mail users in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-mail-users).

Also, if you want Directory Based Edge Blocking (DBEB) to enforce recipient verification, you need to set your domain type to Authoritative. For more information about DBEB, see [Use Directory Based Edge Blocking to reject messages sent to invalid recipients](/en-us/exchange/mail-flow-best-practices/use-directory-based-edge-blocking).

## Step 3: Use the EAC to set up mail flow

Create connectors in the Exchange admin center (EAC) that enable mail flow between the cloud and your on-premises mail servers. For detailed instructions, see [Set up connectors to route mail between Microsoft 365 and your own email servers](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail).

To verify mail flow between the cloud and your on-premises environment, see [Test mail flow by validating your Microsoft 365 connectors](/en-us/exchange/mail-flow-best-practices/test-mail-flow).

## Step 4: Allow inbound port 25 SMTP access

1. After you configure connectors, wait 72 hours to allow propagation of your DNS record updates.
2. Restrict inbound traffic on TCP port 25 (SMTP) on your firewall to accept mail only from the cloud datacenters as listed in [Microsoft 365 URLs and IP address ranges](/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges). This step protects your on-premises environment by limiting the scope of inbound messages you can receive.
3. Update any email server settings that control the IP addresses allowed to connect for mail relay.

Tip

Configure settings on the SMTP server with a connection time out of 60 seconds. This setting is acceptable for most situations, allowing for some delay in the case of a message sent with a large attachment, for example.

## Step 5: Ensure that spam is routed to each user's Junk Email folder

To ensure that spam (junk) email is routed correctly to each user's Junk Email folder in on-premises Exchange, you need to do a couple of configuration steps to translate cloud spam verdicts to values that on-premises Exchange can use. The steps are provided in [Deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes](configure-eop-spam-protection-hybrid).

If you don't want to move messages to each user's Junk Email folder, you can choose a different action by editing your anti-spam policies. For more information, see [Configure anti-spam policies in cloud organizations](/en-us/defender-office-365/anti-spam-policies-configure).

## Step 6: Use the Microsoft 365 admin center to point your MX record to Microsoft 365

Follow the domain configuration steps to update the MX record for your domain, so that your inbound email flows through Microsoft 365. Be sure to point your MX record directly to Microsoft 365 instead of a non-Microsoft service. For more information, you can again reference [Create DNS records for Office 365](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).

Note

If you must point your MX record to another server or service that sits in front of Microsoft 365, see [Enhanced Filtering for Connectors in Exchange Online](/en-us/Exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors).

### How do you know your MX record points to Microsoft 365?

At this point, you verified service delivery for a properly configured on-premises Send connector, and you verified your MX record points to Microsoft 365. You can now choose to run the following additional tests to verify that an email will be successfully delivered by the service to your on-premises environment:

- Check mail flow between the service and your environment. For more information, see [Test mail flow by validating your Microsoft 365 connectors](/en-us/exchange/mail-flow-best-practices/test-mail-flow).
- Send an email message from any web-based email account to a mail recipient in your organization whose domain matches the domain you added to the service. Confirm delivery of the message to the on-premises mailbox using Microsoft Outlook or another email client.
- If you want to run an outbound email test, you can send an email message from a user in your organization to an external email service.

Tip

After you've completed the setup steps in this article, you don't need to do extra steps in the Built-in security add-on for on-premises mailboxes to protect your on-premises organization from spam and malware. However, you can fine tune your settings based on your business requirements. For more information, see [Get started with Microsoft Defender for Office 365: Step 2: Configure protection policies](/en-us/defender-office-365/mdo-deployment-guide#step-2-configure-protection-policies).