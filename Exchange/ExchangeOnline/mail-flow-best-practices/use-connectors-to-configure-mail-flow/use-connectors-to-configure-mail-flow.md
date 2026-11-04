---
layout: Conceptual
title: Configure mail flow using connectors in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow
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
description: Learn how to use connectors to control mail flow with Exchange Online.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 854b5a50-4462-4836-a092-37e208d29624
ms.reviewer: 
f1.keywords:
- CSH
ms.custom:
- ms.exch.eac.ConnectorSelection
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2026-08-27T00:00:00.0000000Z
locale: en-us
document_id: 5cc74a5d-5f48-0d14-d80b-d654dd33c934
document_version_independent_id: 2eb3f77f-f4e2-03c9-9bb2-e108aadce39f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: a23fa023-c3a0-b212-1fe2-41d95906e2ac
---

# Configure mail flow using connectors in Exchange Online | Microsoft Learn

Connectors are a collection of instructions that customize the way your email flows to and from your Microsoft 365 or Office 365 organization. Actually, most Microsoft 365 and Office 365 organizations don't need connectors for regular mail flow. This article describes the mail flow scenarios that require connectors.

## What do connectors do?

Connectors are used in the following scenarios:

- Enable mail flow between Microsoft 365 or Office 365 and email servers that you have in your on-premises environment (also known as on-premises email servers).
- Apply security restrictions or controls to email that's sent between your Microsoft 365 or Office 365 organization and a business partner or service provider.
- Relay mail from devices, applications, or other non-mailbox entities in your on-premises environment through Microsoft 365 or Office 365.
- Avoid *graylisting* that would otherwise occur due to the large volume of mail that's regularly sent between your Microsoft 365 or Office 365 organization and your on-premises environment or partners.

    Note

    Graylisting is a delay tactic that protects email systems from spam. In Microsoft 365 and Office 365, graylisting slows down suspiciously large amounts of email by throttling the message sources based on their IP addresses. Microsoft 365 or Office 365 responds to these abnormal influxes of mail by returning a temporary non-delivery report error (also known as an NDR or bounce message) in the range 451 4.7.500-699 (ASxxx). For more details on these types of delivery issues, see [Fix email delivery issues for error code 451 4.7.500-699 (ASxxx) in Exchange Online](../non-delivery-reports-in-exchange-online/fix-error-code-451-4-7-500-699-asxxx-in-exchange-online).

## What happened to inbound and outbound connectors?

Nothing. We just don't call them "inbound" and "outbound" anymore (although the PowerShell cmdlet names still contains these terms). If you previously set up inbound and outbound connectors, they will still function in exactly the same way.

The process for setting up connectors has changed; instead of using the terms "inbound" and "outbound", we ask you to specify the start and end points that you want to use. The way connectors work in the background is the same as before (inbound means into Microsoft 365 or Office 365; outbound means from Microsoft 365 or Office 365).

## When do I need a connector?

Exchange Online is ready to send and receive email from the internet right away. You don't need to set up connectors unless you use the Built-in security add-on for on-premises mailboxes or other specific scenarios described in the following table:

| Scenario | Description | Connector required? | Connector settings |
| --- | --- | --- | --- |
| You use the Built-in security add-on for on-premises mailboxes. | You have your own on-premises email servers, no Exchange Online mailboxes, and you have licenses for the Built-in security add-on for on-premises mailboxes.  For more information, see [Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/standalone-eop) and the How connectors work with my on-premises email servers section later in this article. | Yes | **Connector for incoming email:**<br>- **From**: Your on-premises email server<br>- **To**: Office 365<br><br>**Connector for outgoing email**: <br>- **From**: Office 365<br>- **To**: Your on-premises mail server |
| Some of your mailboxes are on your on-premises email servers, and some are in Exchange Online. | Before you manually configure connectors, check whether an Exchange hybrid deployment better meets your business needs.  For details, see the I have my own email servers section later in this article and [Exchange Server Hybrid Deployments](../../exchange-hybrid). | Yes | **Connector for incoming email:**<br>- **From**: Your on-premises email server<br>- **To**: Office 365<br><br>**Connector for outgoing email:**<br>- **From**: Office 365<br>- **To**: Your on-premises email server |
| All of your mailboxes are in Exchange Online, you don't have any on-premises email servers, but you need to send email from printers, fax machines, apps, or other devices. | You can *relay* messages from these non-mailbox entities through Microsoft 365 or Office 365.  For details, see [SMTP relay: Configure a connector to relay email from your device or application through Microsoft 365 or Office 365](../how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365#smtp-relay-configure-a-connector-to-relay-email-from-your-device-or-application-through-microsoft-365-or-office-365) | Optional | **Only one connector for incoming email:**<br>- **From**: Your organization's email server<br>- **To**: Office 365 |
| You frequently exchange sensitive information with business partners, and you want to apply security restrictions. | You want to use Transport Layer Security (TLS) to encrypt sensitive information or you want to limit the source (IP addresses) for email from the partner domain.  For details, see [Set up connectors for secure mail flow with a partner organization](set-up-connectors-for-secure-mail-flow-with-a-partner). | Optional | **Connector for incoming email:**<br>- **From**: Partner organization<br>- **To**: Office 365<br><br>**Connector for outgoing email:**<br>- **From**: Office 365<br>- To: Partner organization |

Note

If you're looking for information about Send connectors and Receive connectors in Exchange 2016 or Exchange 2019, see [Connectors](../../mail-flow/connectors/connectors).

You can't have an "allow" by sender domain connector when there is a restrict by IP or certificate connector. The restrict connector will take precedence, as partner connectors are pulled up by IP or certificate lookup when restrictions and mail rejections are applied. You should not have IPs and certificates configured in the same partner connector. Instead, you should use separate connectors. Don't use associated accepted domains unless you're testing the connector for a subset of the accepted domains or recipient domains.

## I have my own email servers

If you have your own on-premises email servers, you definitely need connectors. This scenario is more complicated and has more options as described in the following table:

| Your on-premises email organization is | Your service subscription is | Have you completed an Exchange hybrid deployment? | Do I need to set up connectors manually? |
| --- | --- | --- | --- |
| Exchange 2016 or later | The Built-in security add-on for on-premises mailboxes (no cloud mailboxes) | Not available | Yes. Follow the instructions in [Set up connectors to route mail between Microsoft 365 and your own email servers](set-up-connectors-to-route-mail). |
| Exchange 2016 or later | Exchange Online (cloud mailboxes) | No | Consider whether an Exchange hybrid deployment will better meet your organization's needs by reviewing the article that matches your current situation in [Exchange Server Hybrid Deployments](../../exchange-hybrid).  If a hybrid deployment is the right option for your organization, use the [Hybrid Configuration wizard](../../hybrid-configuration-wizard) to integrate Exchange Online with your on-premises Exchange organization.  If you don't want a hybrid deployment and you only want connectors that enable mail routing, follow the instructions in [Set up connectors to route mail between Microsoft 365 and your own email servers](set-up-connectors-to-route-mail). |
| Exchange 2016 or later | Exchange Online (cloud mailboxes) | Yes | No. The Hybrid Configuration wizard creates connectors for you. To view or edit those connectors, go to the **Connectors** page in the Exchange admin center (EAC), or rerun the Hybrid Configuration wizard. |
| Non-Microsoft SMTP server | The Built-in security add-on for on-premises mailboxes or Exchange Online | Not available | Yes. Follow the instructions in [Set up connectors to route mail between Microsoft 365 and your own email servers](set-up-connectors-to-route-mail). |

### How connectors work with my on-premises email servers

Connectors enable mail flow in both directions (to and from Microsoft 365 or Office 365). You can enable mail flow with any SMTP server (for example, Microsoft Exchange or a third-party email server).

The diagram below shows how connectors in Exchange Online or work with your own email servers.

![Connectors between Microsoft 365 or Office 365 and your e-mail server.](../../exchangeonline/media/0df5ec3d-29c1-4add-9e22-5b0c26bec750.png)

In this example, John and Bob are both employees at your company. John has a mailbox on an email server that you manage, and Bob has a mailbox in Exchange Online. John and Bob both exchange mail with Sun, a customer with an internet email account:

- When email is sent between John and Bob, connectors are needed
- When email is sent between John and Sun, connectors are needed. (All internet email is delivered via Microsoft 365 or Office 365).
- When email is sent between Bob and Sun, no connector is needed.

Important

Always confirm that your internet-facing email servers aren't accidentally configured to allow open relay. An *open relay* allows mail from any source (spammers) to be transparently re-routed through the open relay server. This behavior masks the original source of the messages, and makes it look like the mail originated from the open relay server.

### What if I've already run the Hybrid Configuration Wizard?

If you've already run the Hybrid Configuration wizard, the required connectors are already configured for you. You can view your hybrid connectors on the **Connectors** page in the EAC. You can view, troubleshoot, and update these connectors using the procedures described in [Set up connectors to route mail between Microsoft 365 or Office 365 and your own email servers](set-up-connectors-to-route-mail), or you can re-run the Hybrid Configuration wizard to make changes.

## Connectors for mail flow with a partner organization

You can create connectors to add additional security restrictions for email sent between Microsoft 365 or Office 365 and a partner organization. A partner can be an organization you do business with, such as a bank. It can also be a cloud email service provider that provides services such as archiving, antispam, and so on. You can create a partner connector that defines boundaries and restrictions for email sent to or received from your partners, including scoping the connector to receive email from specific IP addresses, or requiring TLS encryption.

### Example use of connectors with a partner organization

The diagram below shows an example where ContosoBank.com is a business partner that you share financial details with via email. Because you are sharing financial information, you want to protect the integrity of the mail flow between your businesses. Connectors with TLS encryption enable a secure and trusted channel for communicating with ContosoBank.com. In this example, two connectors are created in Microsoft 365 or Office 365. TLS is required for mail flow in both directions, so ContosoBank.com must have a valid encryption certificate. A certificate from a commercial certification authority (CA)that's automatically trusted by both parties is mandatory.

![Connectors between Microsoft 365 or Office 365 and a partner organization.](../../exchangeonline/media/0f9319ae-84bb-4b05-a79f-12fb988f1d10.png)

### Additional partner organization connector options: specify a domain or IP address ranges

When you create a connector, you can also specify the domain or IP address ranges that your partner sends mail from. If email messages don't meet the security conditions that you set on the connector, the message will be rejected. For more information about creating connectors to exchange secure email with a partner organization, see [Set up connectors for secure mail flow with a partner organization](set-up-connectors-for-secure-mail-flow-with-a-partner).

## Connectors for mail notifications from printers and devices

This scenario applies only to organizations that have all their mailboxes in Exchange Online (no on-premises email servers) and allows an application or device to send mail (technically, *relay* mail) through Microsoft 365 or Office 365. For example, if you want a printer to send notifications when a print job is ready, or you want your scanner to email documents to recipients, you can use a connector to relay mail through Microsoft 365 or Office 365 on behalf of the application or device.

Keep in mind that there are other options that don't require connectors. For details about all of the available options, see [How to set up a multifunction device or application to send email](../how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365).

## How do I set up connectors?

Before you set up a connector, you need to configure the accepted domains for Microsoft 365 or Office 365. For more information, see [Manage accepted domains in Exchange Online](../manage-accepted-domains/manage-accepted-domains).

Connector setup articles:

- [Set up connectors to route mail between Microsoft 365 or Office 365 and your own email servers](set-up-connectors-to-route-mail)
- [Set up connectors for secure mail flow with a partner organization](set-up-connectors-for-secure-mail-flow-with-a-partner)