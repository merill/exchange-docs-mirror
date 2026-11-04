---
layout: Conceptual
title: Built-in security add-on for on-premises mailboxes in China | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/standalone-eop/standalone-eop-china
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
ms.localizationpriority: medium
search.appverid:
- GEU150
- GMA150
- GPA150
- MET150
ms.assetid: c5e95951-da67-4ec7-92c5-982abd477e69
ms.collection:
- M365-security-compliance
ms.custom:
- seo-marvel-apr2020
description: Admins in China using Office 365 operated by 21Vianet can learn how to use the Built-in security add-on for on-premises mailboxes to protect their on-premises mailboxes.
ms.service: exchange-online
locale: en-us
document_id: 4f3131a8-16b3-757b-04fa-2f9abc725595
document_version_independent_id: 0d8e589c-3c0c-e435-857e-f5230e0373e3
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/standalone-eop/standalone-eop-china.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standalone-eop/standalone-eop-china
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/standalone-eop/standalone-eop-china.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: c5019527-b385-7a57-fae0-78ab35014db7
---

# Built-in security add-on for on-premises mailboxes in China | Microsoft Learn

Note

This article applies only to Office 365 operated by 21Vianet in China.

If some or all of your mailboxes are in an on-premises email organization in China, you can use the Built-in security add-on for on-premises mailboxes as described in this article.

## What do you need to know before you begin?

To configure connectors, your account needs to be a member of one of the following roles:

- Global Administrator.
- Exchange Company Administrator (the Organization Management role group).

For information about how Office 365 permissions relate to Exchange permissions, see [Assigning admin roles in Office 365 operated by 21Vianet](/en-us/microsoft-365/admin/add-users/assign-admin-roles?preserve-view=true&amp;view=o365-21vianet).

Important

Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Step 1: Use the Microsoft 365 admin center to add and verify your domain

1. In the Microsoft 365 admin center, go to **Setup** to add your domain to the service.
2. Follow the steps in the portal to add the applicable DNS records to your DNS-hosting provider to verify domain ownership.

Tip

[Add your domain and users to Office 365 operated by 21Vianet](/en-us/microsoft-365/admin/setup/add-domain?preserve-view=true&amp;view=o365-21vianet) and [Create DNS records for Office 365 when you manage your DNS records](/en-us/microsoft-365/admin/services-in-china/create-dns-records-when-you-manage-your-dns-records?preserve-view=true&amp;view=o365-21vianet) are helpful references as you add your domain to the service and configure DNS.

### Step 2: Add recipients and configure the domain type

Before configuring your mail to flow to and from Office 365, we recommend adding your recipients to the service. There are different was to add recipients as described in [Manage mail users in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-mail-users).

Also, if you want Directory Based Edge Blocking (DBEB) to enforce recipient verification, you need to set your domain type to Authoritative. For more information about DBEB, see [Use Directory Based Edge Blocking to Reject Messages Sent to Invalid Recipients](/en-us/exchange/mail-flow-best-practices/use-directory-based-edge-blocking).

## Step 3: Use the EAC to set up mail flow

Use the Exchange admin center (EAC) to create connectors to enable mail flow between Office 365 and your on-premises mail servers. For detailed instructions, see [Configure mail flow using connectors in Office 365](/en-us/Exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow).

To verify mail flow between Office 365 and your on-premises environment, see [Test mail flow by validating your Microsoft 365 connectors](/en-us/exchange/mail-flow-best-practices/test-mail-flow).

## Step 4: Allow inbound port 25 SMTP access

1. After you configure connectors, wait 72 hours to allow propagation of your DNS record updates.
2. Restrict inbound TCP port 25 (SMTP) traffic on your firewall to accept mail only from the Office 365 datacenters, specifically from the IP addresses listed at [Managing Microsoft 365 endpoints](/en-us/microsoft-365/enterprise/managing-office-365-endpoints). This action protects your on-premises environment by limiting the scope of inbound messages you can receive.
3. Update any email server settings that control the IP addresses allowed to connect for mail relay.

Tip

Configure settings on the SMTP server with a connection time out of 60 seconds. This setting is acceptable for most situations, allowing for some delay in the case of a message sent with a large attachment, for instance.

## Step 5: Ensure that spam is routed to each user's Junk Email folder

To ensure that spam (junk) email identified by cloud email protection is routed correctly to Junk Email folders in on-premises mailboxes, you need to configure two Exchange mail flow rules (also known as transport rules) in your on-premises Exchange organization. For instructions, see [Deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes](configure-eop-spam-protection-hybrid).

If you don't want messages delivered to the Junk Email folder, you can choose a different action by editing your anti-spam policies. For more information, see [Configure anti-spam policies in cloud organizations](/en-us/defender-office-365/anti-spam-policies-configure).

## Step 6: Point your MX record to Office 365

Follow the domain configuration steps to update the MX record for your domain, so inbound email from the internet flows through Office 365. Be sure to point your MX record directly to Office 365, not to a non-Microsoft filtering service first. For more information, you can again reference [Create DNS records for Office 365](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider?preserve-view=true&amp;view=o365-21vianet).

To test mail flow, see [Test mail flow by validating your Office 365 connectors](/en-us/exchange/mail-flow-best-practices/test-mail-flow).

At this point, you verified service delivery for a properly configured Outbound on-premises connector, and you verified that your MX record is pointing to Microsoft 365. You can now choose to run the following tests to further verify that an email can be successfully delivered by the service to your on-premises environment:

- In the Remote Connectivity Analyzer, select the **Office 365** tab, and then run the **Inbound SMTP Email** test located under **Internet Email Tests**.
- Send an email message from any web-based email account to a mail recipient in your organization whose domain matches the domain you added to the service. Confirm delivery of the message to the on-premises mailbox using Microsoft Outlook or another email client.
- If you want to run an outbound email test, you can send an email message from a user in your organization to a web-based email account and confirm that the message is received.

## Less common: A hybrid setup with on-premises mailboxes and cloud mailbox

If you have on-premises Exchange mailboxes and one or more cloud mailboxes in Exchange Online, you have a *hybrid deployment*. In a hybrid deployment, features such as free/busy calendar sharing and mail routing work together in your on-premises and cloud environments. You might have a hybrid setup while you transition all mailboxes to Exchange Online. Cloud protection features in hybrid deployments with both on-premises Exchange and Exchange Online mailboxes are set up differently than the Built-in security add-on for on-premises mailboxes.

You might choose a hybrid scenario to take advantage of cloud-based email for most of your employees. You can do this hybrid scenario while also hosting some mailboxes on-premises; for example, for your legal department.

A hybrid setup can be complex, but it has many benefits. To learn more about setting up hybrid scenarios with Exchange, see (/Exchange/exchange-hybrid)[Exchange Server hybrid deployments](../exchange-hybrid).