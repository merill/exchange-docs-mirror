---
layout: Conceptual
title: Transport options in Exchange hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/transport-options
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
ms.assetid: da605a78-5429-4de8-8b04-bc4c45a41ba1
ms.reviewer: 
description: Admins can learn about options for mail flow in hybrid environments between on-premises Exchange and Exchange Online.
ms.date: 2025-10-22T00:00:00.0000000Z
locale: en-us
document_id: 05dac701-d68c-429a-4d10-725272b1645c
document_version_independent_id: 75d81a52-02ad-fa6f-a4d8-76a15d4d737b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/transport-options.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: transport-options
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/transport-options.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 9770212c-165f-8186-4ffc-7cb067b07b8f
---

# Transport options in Exchange hybrid deployments | Microsoft Learn

A hybrid deployment contains mailboxes in an on-premises Exchange organization and also in an Exchange Online organization. For more information about hybrid, see [Exchange Server hybrid deployments](exchange-hybrid).

A critical component of making these two separate organizations appear as one is hybrid transport. Messages sent between recipients in either organization are authenticated, encrypted, and transferred using Transport Layer Security (TLS). These messages appear as "internal" to Exchange components (for example, as transport rules, journaling, and anti-spam policies). The Hybrid Configuration wizard automatically configures hybrid transport in Exchange 2013.

For hybrid transport to work with the Hybrid Configuration wizard, the on-premises SMTP endpoint that accepts connections from Exchange Online must be one of the following Exchange servers:

- Exchange 2016 Cumulative Update 8 (CU8) or later:
    - Mailbox server
    - Edge Transport server.
- Exchange 2013 Cumulative Update 15 (CU15) or later:
    - Client Access server.
    - Edge Transport server.
- Exchange 2010 Service Pack 3 (SP3) with Update Rollup 11 (RU11) or later:
    - Hub Transport server.
    - Edge Transport server.

Important

Don't place SMTP hosts or services between Microsoft 365 and the on-premises Exchange organization endpoint. Information critical to hybrid transport is removed from messages that pass through an endpoint running an unsupported version of Exchange or a generic SMTP host.

## Hybrid routing options

You need to choose how to route inbound and outbound mail when you plan and configure your hybrid deployment:

- Do you want to route inbound mail from external internet senders to on-premises and cloud recipients through Microsoft 365 or through your on-premises Exchange organization? Configuration depends on various factors:

    - Are most of your mailboxes in the cloud or in on-premises Exchange?
    - Do you want to use the Built-in security add-on for on-premises mailboxes to protect your on-premises Exchange organization?
    - Where is your compliance infrastructure configured?

    The route for inbound messages to both organizations depends on whether you enable centralized mail transport in your hybrid deployment.
- Do you want to route outbound mail from Exchange Online senders to external recipients through your on-premises organization (centralized mail transport) or directly to the internet?

    *Centralized mail transport* routes all mail from Exchange Online senders through the on-premises organization before delivery to the internet. This approach is important in compliance scenarios where on-premises servers must process all mail sent to and from the internet. Or, you can send messages from Exchange Online senders to external recipients directly to the internet.

    Note

    We recommend centralized mail transport only for organizations with specific compliance-related transport needs. Our typical recommendation is to not use centralized mail transport due to the increased bandwidth and mail processing overhead on your on-premises organization.
- Do you want to deploy an Edge Transport server in your on-premises organization?

    If you don't want to expose your domain-joined, internal Exchange servers directly to the internet, you can deploy supported Edge Transport servers in your perimeter network. For more information, see [Edge Transport servers with hybrid deployments](edge-transport-servers).

Regardless of your selection, all messages sent between the on-premises Exchange organization and the Exchange Online organization use secure transport. For more information, see Trusted communication later in this article.

To learn more about how these options affect message routing in your organization, see [Transport routing in Exchange hybrid deployments](transport-routing).

## Built-in cloud security features in hybrid deployments

All Microsoft cloud organizations with cloud mailboxes include built-in security features to protect recipients from viruses, spam, phishing scams, and policy violations. These same built-in security features are also available to protect on-premises email environments (not just Exchange) in [the Built-in security add-on for on-premises mailboxes](standalone-eop/standalone-eop).

The built-in security features for all cloud mailboxes are the front door to your Exchange Online organization. All incoming messages (regardless of their origin) pass through these built-in security features before they reach recipients in your cloud organization. All messages sent from your Exchange Online organization pass through these built-in security features before they reach the internet.

## Trusted communication

Mail flow between the on-premises organization and the Exchange Online organization is configured to use forced TLS. This configuration helps ensure messages sent between the organizations aren't intercepted. Secure mail transport uses TLS certificates provided by a trusted commercial certification authority (CA).

In forced TLS transport, the sending and receiving servers examine each other's certificates. The certificate's **Subject** or **Subject Alternative Name** (SAN) field must contain the FQDN that identifies the other server.

For example, the Exchange Online organization is configured to accept and secure messages sent from the FQDN mail.contoso.com. The TLS certificate on the source on-premises Client Access server or Edge Transport server must contain mail.contoso.com in the **Subject** or **Subject Alternative Name** (SAN) field. Otherwise, Microsoft 365 refuses the connection.

Tip

The FQDN doesn't need to match the email domain name of recipients. The certificate's **Subject** or **Subject Alternative Name** (SAN) field must contain the FQDN that the receiving or sending servers are configured to accept.

In addition to using TLS, messages between the on-premises and cloud organizations are treated as "internal." This approach allows messages to bypass some threat protection filtering and other services.

For more information, see [Certificate requirements for hybrid deployments](certificate-requirements) and [Understanding TLS Certificates](/en-us/previous-versions/office/exchange-server-2010/aa998840%28v=exchg.141%29).