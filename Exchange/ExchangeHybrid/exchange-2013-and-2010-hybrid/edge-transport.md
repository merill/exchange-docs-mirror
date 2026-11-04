---
layout: Conceptual
title: Edge Transport servers in Exchange 2013/Exchange 2010 hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/exchange-2013-and-2010-hybrid/edge-transport
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
ms.assetid: 924f895e-5987-48d0-b113-9d26dcbcdae0
ms.reviewer: 
description: Admins can learn about hybrid mail routing with Exchange 2010 SP3 or Exchange 2013 Edge Transport servers in Exchange 2010 hybrid deployments.
ms.date: 2025-10-21T00:00:00.0000000Z
locale: en-us
document_id: 66ba5631-5eb8-75e3-6dd8-855e553a6bec
document_version_independent_id: 2ae685be-4dff-6a5f-74ac-67a67bbb4cda
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/exchange-2013-and-2010-hybrid/edge-transport.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: exchange-2013-and-2010-hybrid/edge-transport
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/exchange-2013-and-2010-hybrid/edge-transport.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: f54e5004-01a2-2356-8ced-fe373a6102d9
---

# Edge Transport servers in Exchange 2013/Exchange 2010 hybrid deployments | Microsoft Learn

Hybrid deployments between Exchange Online and on-premises Exchange 2010 organizations with Edge Transport servers require direct mail routing between Microsoft 365 and the Edge Transport servers. The Edge Transport servers used in hybrid mail flow must run one of the following versions of Exchange:

- Exchange 2010 Service Pack 3 (SP3) with Update Rollup 11 (RU11) or later.
- Exchange 2013 Cumulative Update 15 (CU15) or later.

You deploy Edge Transport servers in your perimeter network to handle internet-facing mail flow and to act as an SMTP relay for Microsoft Exchange servers in your internal network. Edge Transport servers prevent exposure of internal Client Access or Mailbox servers directly to the internet.

For more information about Edge Transport servers, see the following articles:

- [Edge Transport servers in Exchange 2013](../edge-transport-servers-exchange-2013-help).
- [Overview of the Edge Transport Server Role in Exchange 2010](/en-us/previous-versions/office/exchange-server-2010/bb124701%28v=exchg.141%29).

Important

If you have other Exchange Edge Transport servers that aren't involved hybrid transport, they don't require a version of Exchange that supports hybrid. If you decide to use these Edge Transport servers in hybrid transport, you need to upgrade them to a supported version of Exchange for hybrid transport.

## Adding an Edge Transport server to a hybrid deployment

Edge Transport servers aren't required for hybrid deployments. The Hybrid Configuration wizard allows you to select one or more Client Access servers and Mailbox servers for hybrid mail transport. Or you can select one or more Edge Transport servers to handle hybrid mail transport.

When you add an Edge Transport server to your hybrid deployment, it communicates with Microsoft 365 on behalf of the internal Exchange 2013 Client Access and Mailbox servers. The Edge Transport server is responsible for the following actions:

- Mail relay between the on-premises Mailbox server and Microsoft 365 for outbound messaging from the on-premises Exchange organization to Exchange Online.
- Mail relay between the on-premises Client Access server for inbound messaging from the Exchange Online organization to the on-premises Exchange organization.

    The Edge Transport server handles connection security previously handled by the Client Access server. Recipient lookup, compliance policies, and other message inspection continue on the Client Access server.

### Hybrid mail flow without an Edge Transport server in Exchange 2010

The following steps and diagram describe mail flow between an on-premises Exchange 2010 organization with no Edge Transport Server and Exchange Online in hybrid deployments:

1. A sender in the on-premises Exchange 2010 organization sends a message to a recipient in the Exchange Online organization. The Exchange 2010 Mailbox server relays the message to an Exchange 2010 Hub Transport server.
2. The Exchange 2010 Hub Transport server relays the message to the Exchange 2013 Mailbox server designated for hybrid transport.

    In this example, the Client Access server role and Mailbox server roles are installed on the same Exchange 2013 server.
3. The Exchange 2013 Mailbox server relays the message directly to Microsoft 365.
4. Microsoft 365 delivers the message to the Exchange Online organization.

![Diagram showing Hybrid mail flow without an Edge Transport server from the on-premises Exchange 2010 organization to the Exchange Online organization.](../exchangehybrid/media/itpro_hybrid_2010-2013_onprem-noedge.png)

Messages sent from the Exchange Online organization to recipients in the on-premises Exchange 2010 organization follow the reverse route.

### Hybrid mail flow with an Edge Transport server in Exchange 2010

The following steps and diagram describe mail flow between an on-premises Exchange 2010 organization with an Edge Transport Server and Exchange Online in hybrid deployments:

1. A sender in the on-premises Exchange 2010 organization sends a message to a recipient in the Exchange Online organization. The Exchange 2010 Mailbox server relays the message to an Exchange 2010 Hub Transport server.
2. The Exchange 2010 Hub Transport server sends the message to the Exchange 2013 Mailbox server.

    In this example, the Client Access server role and Mailbox server roles are installed on the same Exchange 2013 server.
3. The Exchange 2013 Mailbox server relays the message to the Exchange 2013 or Exchange 2010 SP3 Edge Transport server designated for hybrid transport.
4. The Edge Transport server relays the message directly to Microsoft 365.
5. Microsoft 365 delivers the message to the Exchange Online organization.

![Diagram showing Hybrid mail flow with an Edge Transport server from the on-premises Exchange 2010 organization to the Exchange Online organization.](../exchangehybrid/media/itpro_hybrid_2010-2013_onprem-edge.png)

Messages sent from the Exchange Online organization to recipients in the on-premises Exchange 2010 organization follow the reverse route.