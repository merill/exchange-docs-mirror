---
layout: Conceptual
title: Transport routing in Exchange 2013/Exchange 2010 hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/exchange-2013-and-2010-hybrid/transport-routing
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
ms.assetid: 7346bff7-41e0-401c-bd31-34498561f4c4
ms.reviewer: 
description: Admins can learn about message routing options in Exchange 2010 hybrid deployments.
ms.date: 2025-10-22T00:00:00.0000000Z
locale: en-us
document_id: 9ab14534-39c8-0314-2504-29e67b73e905
document_version_independent_id: 568c3b0c-f059-ec19-c58b-579d0dad4b49
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/exchange-2013-and-2010-hybrid/transport-routing.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: exchange-2013-and-2010-hybrid/transport-routing
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/exchange-2013-and-2010-hybrid/transport-routing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 52808052-2843-cce3-9835-f080c0722a2a
---

# Transport routing in Exchange 2013/Exchange 2010 hybrid deployments | Microsoft Learn

This article describes the inbound and outbound mail routing options in Exchange 2010 hybrid deployments. For more information about hybrid, see [Exchange Server hybrid deployments](/en-us/exchange/exchange-hybrid).

Important

Don't place servers, services, or devices that modify email messages between your on-premises Exchange servers and Microsoft 365. Secure mail flow between your on-premises Exchange organization and Microsoft 365 depends on information contained in messages sent between the organizations. Firewalls that allow SMTP traffic on TCP port 25 without modification are supported.

The examples in this article don't include Edge Transport servers. Edge Transport servers don't affect message routing between the on-premises organization, the cloud organization, and the internet. Edge Transport servers change message routing within the on-premises organization only. For more information, see [Edge Transport servers in Exchange 2013/Exchange 2010 hybrid deployments](edge-transport).

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

### Route incoming Internet messages through the Exchange Online organization

The steps and diagrams in the following subsections illustrate the inbound message path when you point your MX record to Microsoft 365.

Important

You might need to purchase licenses for the Built-in security add-on for on-premises mailboxes if your on-premises recipients are protected by the the built-in security features for all cloud mailboxes. Contact your Microsoft reseller for more information.

#### Centralized mail transport disabled (default)

1. An external sender on the internet sends a message to `chris@contoso.com` and `david@contoso.com`. Chris's mailbox is in the on-premises Exchange 2010 organization. David's mailbox is in the Exchange Online organization.
2. The MX record for contoso.com points to Microsoft 365, so the message is routed to the Exchange Online organization.
3. Exchange Online does a lookup for each recipient.
4. Exchange Online splits the message into two copies (also known as *bifurcation*).
5. One copy of the message is delivered directly to David's mailbox in Exchange Online.
6. The other copy of the message is sent from Exchange Online to a designated Exchange 2013 Client Access server in the on-premises Exchange 2010 organization.
7. The receiving Exchange 2013 Client Access server sends the message to an Exchange 2010 Hub Transport server.

    In this example, the Client Access and Mailbox server roles are installed on the same Exchange 2013 server.
8. The Exchange 2010 Hub Transport server sends the message to the Exchange 2010 Mailbox server that hosts the active copy of Chris's mailbox where the message is delivered.

![Diagram showing the inbound mail routing steps when mail is first delivered to Microsoft 365 with centralized mail transport disabled.](../exchangehybrid/media/itpro_hybrid_2010-2013_inbound_viaexo_nocentralized.png)

#### Centralized mail transport enabled

1. An external sender on the internet sends a message to `chris@contoso.com` and `david@contoso.com`. Chris's mailbox is in the on-premises Exchange organization. David's mailbox is in the Exchange Online organization.
2. The MX record for contoso.com points to Microsoft 365, so the message is routed to the Exchange Online organization.
3. Because centralized mail transport is enabled, Exchange Online routes the message to the designated Exchange 2013 server in the on-premises Exchange 2010 organization.

    In this example, the Client Access and Mailbox server roles are installed on the same Exchange 2013 server.
4. The receiving Exchange 2013 server does a lookup for each recipient.
5. The receiving Exchange 2013 server splits the message into two copies (also known as *bifurcation*). One copy of the message is delivered to an Exchange 2010 Hub Transport server and then to the Exchange 2010 Mailbox server that hosts the active copy of Chris's mailbox where the message is delivered.
6. The other copy of the message is sent through the receiving Exchange 2013 server back to the Exchange Online organization.
7. Exchange Online delivers the message to David's mailbox.

![Diagram showing the inbound mail routing steps when mail is first delivered to Microsoft 365 with centralized mail transport enabled.](../exchangehybrid/media/itpro_hybrid_2010-2013_inbound_viaexo_centralized.png)

### Route incoming internet messages through the on-premises Exchange 2010 organization

The following steps and diagram illustrate the inbound message path when you keep your MX record pointed to the on-premises Exchange organization.

1. An external sender on the internet sends a message to `chris@contoso.com` and `david@contoso.com`. Chris's mailbox is in the on-premises Exchange organization. David's mailbox is in the Exchange Online organization and has the hybrid routing (secondary) address `david@contoso.mail.onmicrosoft.com`.
2. The MX record for contoso.com points to the on-premises Exchange organization, so the message is routed to an Exchange 2010 Hub Transport server.
3. The Exchange 2010 Hub Transport server uses an on-premises global catalog server to do a lookup for each recipient.
4. The Exchange 2010 Hub Transport server splits the message into two copies (also known as *bifurcation*). One copy of the message is delivered directly to Chris's mailbox on the Exchange 2010 Mailbox server that hosts the active copy of the mailbox.
5. The other copy of the message is sent using the `david@contoso.mail.onmicrosoft.com` address from the Exchange 2010 Hub Transport server to the Exchange 2013 Mailbox server designated for hybrid transport.

    In this example, the Client Access and Mailbox server roles are installed on the same Exchange 2013 server.
6. The Exchange 2013 Mailbox server sends the message to Microsoft 365 over a Send connector configured with Transport Layer Security (TLS).
7. Microsoft 365 sends the message to the Exchange Online organization where the message is delivered to David's mailbox.

    ![Diagram showing the inbound mail routing steps when mail is first delivered to the on-premises Exchange 2010 organization (centralized mail transport).](../exchangehybrid/media/itpro_hybrid_2010-2013_inbound_viaonprem.png)

## Outbound messages to the internet

You can also choose how to route outbound messages from Exchange Online senders. The Hybrid Configuration wizard has the following options:

- **Don't enable centralized mail transport**: This value is the default. Route outbound messages from the Exchange Online organization directly to the internet. Use this option if you don't need to apply on-premises compliance policies or other processing rules to messages from Exchange Online senders.
- **Enable centralized mail transport**: Route outbound messages from the Exchange Online organization through the on-premises Exchange organization. Messages sent to other recipients in the same Exchange Online organization aren't sent through the on-premises Exchange organization. Use this option to apply on-premises compliance policies or other processing rules to messages, regardless of whether recipients are in the Exchange Online organization or the on-premises Exchange organization.

    Tip

    We recommend centralized mail transport only for organizations with specific compliance needs. Otherwise, we don't typically recommend centralized mail transport.

Read the following sections to plan how to route outbound mail from Exchange Online to the internet in your hybrid deployment.

### Outbound message routing from on-premises Exchange senders to external recipients

Messages from senders in on-premises Exchange are always sent to internet recipients using DNS, regardless of which outbound routing option you select in the Hybrid Configuration wizard. The following steps and diagram illustrate the message path from senders in on-premises Exchange 2010 to external recipients.

1. Chris has a mailbox in the on-premises Exchange 2010 organization and sends a message to the external internet recipient `erin@cpandl.com`.
2. The Exchange 2010 Mailbox server sends the message to the Exchange 2010 Hub Transport server.
3. The Exchange 2010 Hub Transport server looks up the MX record for the cpandl.com domain and sends the message to the specified email server on the internet.

    ![Diagram showing outbound mail routing steps when mail is sent from the on-premises Exchange 2010 organization.](../exchangehybrid/media/itpro_hybrid_2010-2013_outbound_fromonprem.png)

Read the following sections to plan how to route outbound mail from Exchange Online to the internet in your hybrid deployment.

### Outbound message routing from Exchange Online to external recipients with centralized mail transport disabled (default)

The following steps and diagram illustrate the outbound message path for messages from Exchange Online to an external recipient when you select **Don't enable centralized mail transport** in the Hybrid Configuration wizard, which is the default configuration.

1. David has a mailbox in the Exchange Online organization and sends a message to the external internet recipient `erin@cpandl.com`.
2. Exchange Online looks up the MX record for the cpandl.com domain and sends the message to the specified email server on the internet.

    **Mail from Exchange Online senders routed directly to the Internet with centralized mail transport disabled (default configuration)**

    ![Diagram showing outbound mail routing steps when mail is sent from the Exchange Online organization to an external recipient with centralized mail transport disabled (default).](../exchangehybrid/media/itpro_hybrid_2010-2013_outbound_exodirect.png)

### Outbound message routing from Exchange Online to external recipients with centralized mail transport enabled

The following steps and diagram illustrate the outbound message path for messages from Exchange Online to an external recipient when you select **Enable centralized mail transport** in the Hybrid Configuration wizard.

1. David has a mailbox in the Exchange Online organization and sends a message to the external internet recipient `erin@cpandl.com`.
2. Exchange Online is configured to send messages to external recipients through the on-premises Exchange 2010 organization, so the message is routed to a designated on-premises Exchange 2013 Client Access server. The message is sent using TLS.
3. The Exchange 2013 Client Access server applies compliance, anti-virus, and any other processes configured by the administrator to the message.

    In this example, the Client Access and Mailbox server roles are installed on the same Exchange 2013 server.
4. The Exchange 2013 Client Access server forwards the message to an Exchange 2010 Hub Transport server.
5. The Exchange 2010 Hub Transport server looks up the MX record for the cpandl.com domain and sends the message to the specified email server on the internet.

    ![Diagram showing outbound mail routing steps when mail is sent from the Exchange Online organization to an external recipient with centralized mail transport enabled.](../exchangehybrid/media/itpro_hybrid_2010-2013_outbound_exoviaonprem.png)