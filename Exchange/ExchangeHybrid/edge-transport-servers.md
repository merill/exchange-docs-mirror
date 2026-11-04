---
layout: Conceptual
title: Edge Transport servers with hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/edge-transport-servers
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
ms.assetid: 166b1490-5c56-40df-a17b-e8bb36224fd9
ms.reviewer: 
description: Learn how Edge Transport servers are used in Hybrid deployments
ms.date: 2025-10-16T00:00:00.0000000Z
locale: en-us
document_id: d1c5c767-7732-ddb7-d11d-63f659a65bf0
document_version_independent_id: 0ed7596b-3fd1-7b73-b555-299d8bea81ed
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/edge-transport-servers.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: edge-transport-servers
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/edge-transport-servers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 1a520e1d-9b21-1cc3-b082-8585fc603321
---

# Edge Transport servers with hybrid deployments | Microsoft Learn

The Edge Transport server role in Exchange is an optional role that you typically deploy on a computer in the perimeter network to minimize the attack surface of the organization. The Edge Transport server role handles all internet-facing mail flow, which provides SMTP mail relay and smart host services for the internal, on-premises Exchange servers in your organization.

## Edge Transport servers in Exchange-based hybrid deployment organizations

Exchange 2016 organizations that want to use Edge Transport servers have the option of deploying Edge Transport servers running the latest release of Exchange 2010 or later. Use Edge Transport servers if you don't want to expose internal Exchange servers directly to the internet. When you deploy an Edge Transport server in a hybrid deployment, Microsoft 365 connects to your Edge Transport server to deliver messages. The Edge Transport server then delivers messages to the on-premises Exchange Mailbox server where the recipient mailbox is located.

Important

Don't place servers, services, or devices that modify email messages between your on-premises Exchange servers and Microsoft 365. Secure mail flow between your on-premises Exchange organization and Microsoft 365 depends on information contained in messages sent between the organizations. Firewalls that allow SMTP traffic on TCP port 25 without modification are supported.

Internal messages modified by a server, service, or device between your on-premises Exchange organization and Microsoft 365 are no longer considered internal. The modified messages are subject to anti-spam filtering, transport rules, journal rules, and other policies that you don't want to apply to internal message.

Using Edge Transport servers in Exchange hybrid requires Edge subscriptions. If you have other Exchange Edge Transport servers that aren't involved hybrid transport, they don't require a version of Exchange that supports hybrid. If you decide to use these Edge Transport servers in hybrid transport, you need to upgrade them to a supported version of Exchange for hybrid transport.

## Adding an Edge Transport server to a hybrid deployment

Deploying an Edge Transport server in your on-premises organization when you configure a hybrid deployment is optional. When you configure a hybrid deployment, you select internal Exchange servers or Edge Transport servers for hybrid mail transport in the Hybrid Configuration wizard (HCW).

When you add an Edge Transport server to your hybrid deployment, it communicates with Microsoft 365 on behalf of the internal Exchange servers. The Edge Transport server acts as a relay between the internal Exchange servers and Microsoft 365:

- Outbound messaging from the on-premises organization to the Exchange Online organization.
- Inbound messaging from the Exchange Online organization to the on-premises organization.

The Edge Transport server handles all connection security previously handled by internal Exchange servers. Recipient lookup, compliance policies, and other message inspection are still done on the internal Exchange servers.

You don't need to route mail set to the internet from on-premises users through an Edge Transport server in a hybrid deployment. Only messages sent between the on-premises and Exchange Online organizations are routed through the Edge Transport server.

After running the HCW, update the Receive Connector on the Edge Transport server to ensure it securely accepts mail from Microsoft 365 by using the following command in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell):

```powershell
Set-ReceiveConnector -Identity "<Edge server name>\Default internal receive connector <Edge server name>" -TlsDomainCapabilities <URL> -Fqdn "Subject name on the public certificate on the Edge Transport server"
```

&lt;URL&gt; for the *TlsDomainCapabilities* parameter is one of the following values:

- **Microsoft 365** and **Microsoft 365 Government Community Cloud (GCC)**: `mail.protection.outlook.com:AcceptCloudServicesMail`
- **Microsoft 365 GCC High**: `mail.protection.office365.us:AcceptCloudServicesMail`
- **Microsoft 365 DoD**: `mail.protection.apps.mil:AcceptCloudServicesMail`

For detailed syntax and parameter information, see [Set-ReceiveConnector](/en-us/powershell/module/exchangepowershell/set-receiveconnector).

Important

Recreating an Edge subscription removes settings require for mail flow between your on-premises organization and Exchange Online. Running the Hybrid Configuration wizard after you recreate an Edge subscription applies the required settings.

### Hybrid mail flow without an Edge Transport server

The following steps and diagram describe mail flow between an on-premises organization with no Edge Transport Server and Exchange Online in hybrid deployments:

1. An on-premises mailbox user sends a message to a recipient in the Exchange Online organization.
2. A designated internal Exchange server sends the message to Microsoft 365.
3. Microsoft 365 delivers the message to the Exchange Online organization.

![Diagram showing Hybrid mail flow without an Edge Transport server from the on-premises Exchange organization to the Exchange Online organization.](exchangehybrid/media/a95b4d1e-fd4a-4952-b891-22f84c9e71a3.png)

Messages sent from mailboxes in the Exchange Online organization to recipients in the on-premises organization follow the reverse route.

### Hybrid mail flow with an Edge Transport server

The following steps and diagram describe mail flow between an on-premises organization with an Edge Transport Server and Exchange Online in hybrid deployments:

1. An on-premises mailbox user sends a message to a recipient in the Exchange Online organization.
2. An internal Exchange server sends the message to a subscribed Edge Transport server.
3. The Edge Transport server sends the message to Microsoft 365.
4. Microsoft 365 delivers the message to the Exchange Online organization.

Note

Installing an Edge server and establishing an Edge subscription affects mail flow. This process automatically creates two Send connectors for internet mail flow:

- Send email from the internal Exchange organization to all internet domains.
- Send email from the Edge Transport server to the internal Exchange organization.

Review your connectors to verify mail flow is configured correctly.

![Diagram showing Hybrid mail flow with an Edge Transport server from the on-premises Exchange organization to the Exchange Online organization.](exchangehybrid/media/821fe099-56f5-4501-8e1a-e184ba07a653.png)

Messages sent from mailboxes in the Exchange Online organization to recipients in the on-premises organization follow the reverse route.