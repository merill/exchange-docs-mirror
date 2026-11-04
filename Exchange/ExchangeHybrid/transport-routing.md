---
layout: Conceptual
title: Email routing in Exchange hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/transport-routing
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: install-set-up-deploy
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
ms.assetid: 36c2cea3-2e2f-40ac-88bd-7e1b6bd27828
ms.reviewer: 
description: Admins can learn about message routing options in Exchange hybrid deployments.
ms.date: 2025-10-17T00:00:00.0000000Z
locale: en-us
document_id: b002f0ce-5397-15cb-4c60-0eaaa87aaf52
document_version_independent_id: 32e3a594-2d2c-9f8a-9a38-e60e3ffaae85
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/transport-routing.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: transport-routing
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/transport-routing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 20b53b33-2f01-22b0-bbc9-ff49c396417a
---

# Email routing in Exchange hybrid deployments | Microsoft Learn

This article describes the inbound and outbound mail routing options in Exchange hybrid deployments. For more information about hybrid, see [Exchange Server hybrid deployments](/en-us/exchange/exchange-hybrid).

Important

Don't place servers, services, or devices that modify email messages between your on-premises Exchange servers and Microsoft 365. Secure mail flow between your on-premises Exchange organization and Microsoft 365 depends on information contained in messages sent between the organizations. Firewalls that allow SMTP traffic on TCP port 25 without modification are supported.

The examples in this article don't include Edge Transport servers. Edge Transport servers don't affect message routing between the on-premises organization, the cloud organization, and the internet. Edge Transport servers change message routing within the on-premises organization only. For more information, see [Edge Transport servers with hybrid deployments](edge-transport-servers).

## Inbound messages from the internet

You need to decide if you want external messages from internet senders to be routed through Exchange Online or your on-premises organization. All messages from internet senders are initially delivered to the organization you select and are then routed to the recipient location. The ideal configuration depends on various factors:

- Are most of your mailboxes in the cloud or in on-premises Exchange?
- Do you want to use [the built-in security features for all cloud mailboxes](transport-options#built-in-cloud-security-features-in-hybrid-deployments) to protect your on-premises Exchange organization?
- Where is your compliance infrastructure configured?

The message path depends on how you decide to configure your MX record in your hybrid deployment. The Hybrid Configuration wizard doesn't configure routing for inbound internet messages. You need to manually configure your MX record if you want to change how inbound internet mail is delivered:

- **Point your MX record to Microsoft 365**: We recommend this configuration for hybrid deployments. All messages sent to any recipient are routed through Exchange Online. This configuration is required to use the built-in security features for all cloud mailboxes to protect your on-premises Exchange organization.
- **Keep your MX record pointed to your on-premises organization**: All messages sent to any recipient are routed through on-premises Exchange. This configuration can be helpful for organizations with an on-premises journaling solution. This configuration doesn't allow the built-in security features for all cloud mailboxes to protect your on-premises Exchange organization.

For more information, see [Mail flow best practices for Exchange Online, Microsoft 365, and Office 365 (Overview)](/en-us/exchange/mail-flow-best-practices/mail-flow-best-practices).

Read the following sections to plan how to route inbound mail in your hybrid deployment.

### Route incoming internet messages through the Exchange Online organization

The steps and diagrams in the following subsections illustrate the inbound message path when you point your MX record to Microsoft 365.

Important

You might need to purchase licenses for the Built-in security add-on for on-premises mailboxes if your on-premises recipients are protected by the the built-in security features for all cloud mailboxes. Contact your Microsoft reseller for more information.

#### Centralized mail transport disabled (default)

1. An external sender on the internet sends a message to `julie@contoso.com` and `david@contoso.com`. Julie's mailbox is in the on-premises Exchange organization. David's mailbox is in the Exchange Online organization.
2. The MX record for contoso.com points to Microsoft 365, so the message is routed to the Exchange Online organization.
3. Exchange Online does a lookup for each recipient.
4. Exchange Online splits the message into two copies (also known as *bifurcation*). One copy of the message is delivered directly to David's mailbox in Exchange Online.
5. The other copy of the message is sent from Exchange Online to an on-premises Exchange server in the on-premises organization.
6. The receiving Exchange server sends the message to Julie's mailbox on the Exchange Mailbox server that hosts the active copy of the mailbox.

    ![Diagram showing the inbound mail routing steps when mail is first delivered to Microsoft 365 with centralized mail transport disabled.](exchangehybrid/media/f98341e0-088d-49f0-bf8e-09f35255bf9e.png)

#### Centralized mail transport enabled

1. An external sender on the internet sends a message to `julie@contoso.com` and `david@contoso.com`. Julie's mailbox is in the on-premises Exchange organization. David's mailbox is in the Exchange Online organization.
2. The MX record for contoso.com points to Microsoft 365, so the message is routed to the Exchange Online organization.
3. Because centralized mail transport is enabled, Exchange Online routes the message to an on-premises Exchange server.
4. The receiving on-premises Exchange server does a lookup for each recipient.
5. The receiving on-premises Exchange server splits the message into two copies (also known as *bifurcation*). One copy of the message is delivered directly to Julie's mailbox on the Exchange Mailbox server that hosts the active copy of the mailbox.
6. The other copy of the message is sent from the receiving on-premises Exchange server back to the Exchange Online organization.
7. Exchange Online delivers the message to David's mailbox.

    ![Diagram showing the inbound mail routing steps when mail is first delivered to Microsoft 365 with centralized mail transport enabled.](exchangehybrid/media/062422d5-9cb6-42c2-9ec0-31962cd7ada6.png)

### Route incoming internet messages through the on-premises Exchange 2010 organization

The following steps and diagram illustrate the inbound message path when you keep your MX record pointed to the on-premises Exchange organization.

1. An external sender on the internet sends a message to `julie@contoso.com` and `david@contoso.com`. Julie's mailbox is in the on-premises Exchange organization. David's mailbox is in the Exchange Online organization and has the hybrid routing (secondary) address `david@contoso.mail.onmicrosoft.com`.
2. The MX record for contoso.com points to the on-premises Exchange organization, so the message is routed to an on-premises Exchange server.
3. The receiving on-premises Exchange server uses an on-premises global catalog server to do a lookup for each recipient.
4. The receiving on-premises Exchange server splits the message into two copies (also known as *bifurcation*). One copy of the message is delivered directly to Julie's mailbox on the Exchange Mailbox server that hosts the active copy of the mailbox.
5. The other copy of the message is sent using the `david@contoso.mail.onmicrosoft.com` address from the receiving on-premises Exchange server to the Exchange Online organization via a Send connector configured with Transport Layer Security (TLS).
6. Exchange Online delivers the message delivered to David's mailbox.

    ![Diagram showing the inbound mail routing steps when mail is first delivered to the on-premises Exchange organization (centralized mail transport).](exchangehybrid/media/a246a1e2-7593-4d13-9426-73622a545c9a.png)

## Outbound messages to the internet

You can also choose how to route outbound messages from Exchange Online senders. The Hybrid Configuration wizard has the following options:

- **Don't enable centralized mail transport**: This value is the default. Route outbound messages from the Exchange Online organization directly to the internet. Use this option if you don't need to apply on-premises compliance policies or other processing rules to messages from Exchange Online senders.
- **Enable centralized mail transport**: Route outbound messages from the Exchange Online organization through the on-premises Exchange organization. Messages sent to other recipients in the same Exchange Online organization aren't sent through the on-premises Exchange organization. Use this option to apply on-premises compliance policies or other processing rules to messages, regardless of whether recipients are in the Exchange Online organization or the on-premises Exchange organization.

    Tip

    We recommend centralized mail transport only for organizations with specific compliance needs. Otherwise, we don't typically recommend centralized mail transport.

Read the following sections to plan how to route outbound mail from Exchange Online to the internet in your hybrid deployment.

### Outbound message routing from on-premises Exchange senders to external recipients

Messages from senders in on-premises Exchange are always sent to internet recipients using DNS, regardless of which outbound routing option you select in the Hybrid Configuration wizard. The following steps and diagram illustrate the message path from senders in on-premises Exchange to external recipients.

1. Julie has a mailbox in the on-premises Exchange organization and sends a message to the external internet recipient `erin@cpandl.com`.
2. The Exchange server looks up the MX record for the cpandl.com domain and sends the message to the specified email server on the internet.

    ![Diagram showing outbound mail routing steps when mail is sent from the on-premises Exchange organization.](exchangehybrid/media/71f287d6-b814-4820-a0dc-575f17d13894.png)

### Outbound message routing from Exchange Online to external recipients with centralized mail transport disabled (default)

The following steps and diagram illustrate the outbound message path for messages from Exchange Online to an external recipient when you select **Don't enable centralized mail transport** in the Hybrid Configuration wizard, which is the default configuration.

1. David has a mailbox in the Exchange Online organization and sends a message to the external internet recipient `erin@cpandl.com`.
2. Exchange Online looks up the MX record for the cpandl.com domain and sends the message to the specified email server on the internet.

    ![Diagram showing outbound mail routing steps when mail is sent from the Exchange Online organization to an external recipient with centralized mail transport disabled (default).](exchangehybrid/media/fe1c4241-0d6e-47bf-b61d-5af732d2dbbc.png)

### Outbound message routing from Exchange Online to external recipients with centralized mail transport enabled

The following steps and diagram illustrate the outbound message path for messages from Exchange Online to an external recipient when you select **Enable centralized mail transport** in the Hybrid Configuration wizard.

1. David has a mailbox in the Exchange Online organization and sends a message to the external internet recipient `erin@cpandl.com`.
2. Exchange Online is configured to send messages to external recipients through the on-premises Exchange organization, so the message is routed to a designated on-premises Exchange server. The message is sent using TLS.
3. The receiving on-premises Exchange server applies compliance, anti-virus, and any other processes configured by the administrator to the message.
4. The receiving on-premises Exchange server looks up the MX record for the cpandl.com domain and sends the message to the specified email server on the internet.

    ![Diagram showing outbound mail routing steps when mail is sent from the Exchange Online organization to an external recipient with centralized mail transport enabled.](exchangehybrid/media/7ea9ffee-944b-45ae-ba4d-c3484100399b.png)