---
layout: Conceptual
title: Server roles in Exchange 2013/Exchange 2010 hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/exchange-2013-and-2010-hybrid/server-roles
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
ms.assetid: 7d774948-94f9-4405-af2b-0c67c0405c0f
ms.reviewer: 
description: Admins can learn about the Exchange 2013 server roles you need to install in an Exchange 2010 organization for a hybrid deployment with Exchange Online.
ms.date: 2025-10-22T00:00:00.0000000Z
locale: en-us
document_id: 96aac873-999b-79ab-d326-f22156242af6
document_version_independent_id: 338ee4dd-62d6-d92c-1b89-5a897b60bc71
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/exchange-2013-and-2010-hybrid/server-roles.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: exchange-2013-and-2010-hybrid/server-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/exchange-2013-and-2010-hybrid/server-roles.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 52871240-45b1-e823-3053-b62da31a4375
---

# Server roles in Exchange 2013/Exchange 2010 hybrid deployments | Microsoft Learn

When you configure a hybrid deployment in an Exchange 2010 organization, we strongly recommend at least one Exchange 2013 server with the Client Access and Mailbox server roles. The Exchange 2013 Client Access and Mailbox servers coordinate message transport and messaging features between your existing on-premises Exchange 2010 organization and the Exchange Online organization.

We highly recommend installing more than one Exchange 2013 server in your on-premises Exchange 2010 organization to help increase reliability and availability of hybrid deployment features.

## Server roles in a hybrid deployment

Here's a quick overview of the Exchange 2013 server roles in a hybrid deployment:

- **Client Access server role**: Provides many of the same functions as Exchange 2010 Client Access servers, with some required additions for hybrid deployments and coexistence with Exchange 2010:

    - Secure messages sent from the Exchange Online organization to the on-premises organization
    - Transport rules.
    - Journaling policies.
    - Message delivery to Mailbox servers in a hybrid deployment.

    A dedicated Receive connector is configured by default to support secure hybrid mail transport.

    All client connectivity (for example, Outlook client access, Outlook Web App, and Outlook Anywhere) goes through the Client Access server role.

    The Exchange 2013 Client Access server also handles organization relationship features between the on-premises and Exchange Online organizations (for example free/busy sharing).

    For more information, see [Client Access server role in Exchange 2013](../client-access-server-exchange-2013-help).
- **Mailbox server role**: Handles secure mail sent from the on-premises Exchange 2010 organization to the Exchange Online organization.

    Although not typical, it can also host mailboxes and proxy communicate with the Exchange Online organization via the on-premises Client Access server.

    By default, a dedicated Send connector is configured on the Mailbox server role to support secure hybrid mail transport.

    For more information, see [Mailbox server role in Exchange 2013](../mailbox-server-exchange-2013-help).

Depending on the hybrid deployment configuration you want, an Exchange 2013 server requires one or both server roles:

- **Single Exchange server**: You need to install both the Client Access and Mailbox server roles on the single server.
- **More than one Exchange server**: The best practice and recommended server configuration is the Client Access and Mailbox server roles on each Exchange 2013 server. But you can also install each role individually on Exchange 2013 servers.

For more information about Exchange capacity planning, see [Understanding Multiple Server Role Configurations in Capacity Planning](../exchange-2013-sizing-and-capacity-planning-exchange-2013-help).

## Exchange server functionality in hybrid deployments

Exchange 2013 servers provide several important functions for your on-premises Exchange 2010 organization in a hybrid deployment:

- **Federation**: Exchange 2013 servers enable you to create a federation trust for your on-premises Exchange 2010 organization with the Microsoft Federation Gateway. The Microsoft Federation Gateway is a free, cloud-based service offered by Microsoft that acts as the trust broker between your on-premises Exchange organization and the Microsoft 365 or Office 365 organization. Federation is a requirement for creating an organization relationship between the on-premises and the Exchange Online organizations.

    For more information, see [Understanding Federation](../federation-exchange-2013-help).
- **Organization relationships**: Exchange 2013 Client Access servers enable organization relationships between the on-premises Exchange 2010 and Exchange Online organizations. Organization relationships are required for many services in a hybrid deployment. For example:

    - Calendar free/busy information sharing.
    - Message tracking.
    - Mailbox moves between the on-premises and Exchange Online organizations.

    For more information, see [Sharing](../sharing-exchange-2013-help).
- **Message transport**: Exchange 2013 servers with the Client Access and Mailbox server roles are responsible for message transport in a hybrid deployment. The servers use Send and Receive connectors to:

    - Receive incoming messages from external senders on the internet.
    - Provide outbound message delivery to the internet and the Exchange Online organization.

    For more information, see [Transport options in Exchange 2013/Exchange 2010 hybrid deployments](transport-options).
- **Message transport security**: Exchange 2013 servers with the Client Access and Mailbox server roles use the Domain Security feature to secure message communication between the on-premises Exchange 2010 organization and the Exchange Online organization. You can increase security by using mutual Transport Layer Security (TLS) authentication and encryption for mail.

    For more information, see [Understanding Domain Security](/en-us/previous-versions/office/exchange-server-2010/bb124392%28v=exchg.141%29).
- **Outlook Web App**: Exchange 2013 Client Access servers support a single URL endpoint for external connections to on-premises Exchange 2010 mailboxes and Exchange Online mailboxes:

    - **On-premises mailboxes**: Exchange 2013 Client Access servers service Outlook Web App requests.
    - **Exchange Online mailboxes**: Exchange 2013 Client Access servers display a link to the Outlook on the web URL in Exchange Online.

    For more information, see [Outlook Web App](../outlook-web-app-exchange-2013-help).

## Exchange server topology

As you introduce Exchange 2013 servers into an Exchange 2010 organization for hybrid deployments, the Exchange servers must meet the following requirements:

- **Exchange 2010**: Exchange 2010 Service Pack 3 (SP3) with Update Rollup 11 (RU11) or later.
- **Exchange 2013**: Exchange 2013 Cumulative Update 15 (CU15) or later to enable compatibility and full hybrid functionality with Microsoft 365.

The following table summarizes the changes in services after configuring a hybrid deployment:

| Service | Before hybrid deployment | After hybrid deployment | Description |
| --- | --- | --- | --- |
| Message transport (inbound and outbound) | Exchange 2010 Client Access server | Exchange 2013 Client Access server or Microsoft 365 | You can leave the MX record for the domain pointed at the on-premises Exchange organization, or you can point the MX record to Microsoft 365. |
| Outlook Web App public URL | Exchange 2010 Client Access server | Exchange 2013 Client Access server | **On-premises mailboxes**: Exchange 2013 Client Access servers service Outlook Web App requests.- **Exchange Online**: Exchange 2013 Client Access servers display a link to the Outlook on the web URL in Exchange Online. |

## Exchange server software

Exchange 2013 CU15 or later enables hybrid deployment functionality with the Hybrid Configuration wizard (HCW). You can use any Exchange 2013 CU15 or later media when installing more Exchange 2013 servers.

For information on how to download the latest version of Exchange Server, see [Updates for Exchange Server](../new-features/updates).

Important

You need to license your hybrid server when you configure a hybrid deployment. The HCW can detect and license your designated Exchange 2010 SP3, Exchange 2013, or Exchange 2016 hybrid servers for free. You don't need to visit a separate web site or contact Microsoft support. You download the HCW at https://aka.ms/HybridWizard.

The free Exchange Server license isn't available for Exchange 2019 or later hybrid servers.