---
layout: Conceptual
title: Troubleshoot a hybrid deployment | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/troubleshoot-a-hybrid-deployment
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
ms.topic: troubleshooting-general
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.custom:
- has-azure-ad-ps-ref
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
ms.assetid: bbae72f3-6a1e-4cbf-80da-d8f73d969c6b
ms.reviewer: 
description: Admins can learn about common issues in Exchange hybrid deployments and how to fix them.
ms.date: 2025-10-28T00:00:00.0000000Z
locale: en-us
document_id: bbe9b5a0-e41d-b92a-b221-cc12a3945618
document_version_independent_id: 6ff00d15-7376-c2b6-0d3f-c71a5ff1c7dd
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/troubleshoot-a-hybrid-deployment.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/troubleshoot-a-hybrid-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/troubleshoot-a-hybrid-deployment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: ea6e4c5e-6b67-f580-3e73-f782f22722d0
---

# Troubleshoot a hybrid deployment | Microsoft Learn

Configuring an Exchange hybrid deployment with the Hybrid Configuration wizard greatly reduces potential problems with the hybrid deployment. However, there are some typical areas outside the scope of the Hybrid Configuration wizard that, if misconfigured, might present problems. This article discusses the following common problem areas and outlines basic steps to verify or correct issues:

- On-premises Exchange servers
- Certificates
- Specific errors of the Hybrid Configuration wizard

Tip

In this article, "Exchange servers" has the following meanings:

- **Client Access servers**: Exchange 2013 and earlier.
- **Mailbox servers**: Exchange 2016 and later.

For more information, see [Exchange Server Hybrid Deployments](../exchange-hybrid).

For other management tasks related to hybrid deployments, see [Hybrid Deployment procedures](hybrid-deployment).

## What do you need to know before you begin?

- Estimated time to complete this task: Varies, depending on type of hybrid deployment issues
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Hybrid deployments" entry in the [Exchange and PowerShell infrastructure permissions](../permissions/feature-permissions/infrastructure-permissions) article.
- The guidance in this article applies to hybrid deployments configured using the Hybrid Configuration wizard. Manually configured hybrid deployments aren't supported.
- For information about keyboard shortcuts that might apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Hybrid forum at [Exchange | Hybrid management](/en-us/answers/tags/377/office-exchange-hybrid-management).

## Troubleshoot issues with on-premises Exchange servers

The configuration of the on-premises Exchange servers is typically where most problems might occur in a hybrid deployment. Typically, you need to examine the following areas:

- **Availability**: Correctly publishing the on-premises Exchange servers to the internet is vital to features working correctly.

    - Configure your firewall to allow inbound access from the internet to the Autodiscover and Exchange Web Services (EWS) endpoints on the on-premises Exchange servers.
    - Configure you on-premises Exchange servers to accept inbound SMTP mail. If Microsoft 365 can't reach the on-premises Exchange servers, secure mail transport from the Exchange Online organization to the on-premises organization can't function correctly.
- **Certificates**: Install the certificates used for secure mail transport between the on-premises and Exchange Online organizations on all on-premises, internet-facing Exchange servers that communicate with Exchange Online. The certificates must meet the following requirements:

    - Issued by a commercial certification authority (CA).
    - Not expired.
    - Has the Internet Information Service (IIS) and Simple Mail Transport Protocol (SMTP) services assigned.

    If these certificates don't meet the requirements, secure mail transport from the Exchange Online organization to the on-premises organization can't function correctly. For more information, see the Troubleshoot issues with certificates section later in this article.

### How do you know if your Exchange servers are configured correctly?

To verify that you successfully published your on-premises Exchange servers, use the Microsoft Remote Connectivity Analyzer to verify inbound Internet connectivity to your on-premises Exchange servers:

1. Go to the **Exchange Online** connectivity tests in the Remote Connectivity Analyzer at https://testconnectivity.microsoft.com/tests/exo.
2. Run the **Synchronization, Notification, Availability, and Automatic Replies** test for a general test of EWS tasks and EWS configuration. Identity and fix any errors you receive.
3. Run the **Outlook Connectivity** test for a general test of the Autodiscover service the Autodiscover endpoint. Identity and fix any errors you receive.
4. Run the **Inbound SMTP EMail** test for a general test of SMTP connectivity and the ability of Exchange servers to receive inbound internet mail. Identity and fix any errors you receive.

## Troubleshoot issues with certificates

In most cases, the following certificate-related issues affect hybrid functionality:

- **Certificate type**: The certificate used for secure hybrid transport and defined in the Hybrid Configuration wizard must be issued from a commercial CA. You can't use self-signed certificates for hybrid transport authentication. If you assigned a self-signed certificate, secure mail transport between the Exchange Online and the on-premises organizations can't function correctly.
- **Assigned services**: You need to assign the IIS and SMTP services to the certificate used for hybrid transport. If these services aren't assigned, secure mail transport between Exchange Online and the on-premises organizations can't function correctly.
- **Installation**: The certificate used for secure mail transport between the on-premises and Exchange Online organizations must be installed on all on-premises Exchange servers. If you deploy hybrid with on-premises Edge Transport servers, the certificate must also be installed on your Edge Transport servers. If the certificate isn't installed on the on-premises servers, secure mail transport between the Exchange Online and the on-premises organizations can't function correctly.
- **Expiration**: If the certificate used for secure mail transport between the on-premises and Exchange Online organizations is expired, secure mail transport between the Exchange Online and the on-premises organizations can't function correctly.

### How do you know if your certificates are configured correctly?

To verify the certificate used for hybrid mail transport is correctly configured on your on-premises Exchange servers, do the following steps in the [Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell):

1. Replace &lt;Thumbrpint&gt; with the certificate thumbprint value, and then run the following command and verify the property values:

    ```powershell
    Get-ExchangeCertificate -Thumbprint <Thumbprint> | Format-List Thumbprint,IsSelfSigned,RootCAType,Services,NotAfter
    ```

    - *IsSelfSigned*: The value should be `False`.
    - *RootCAType*: The value should be `Third Party`.
    - *Services*: The value should be `IIS, SMTP`.
    - *NotAfter*: The value is the certificate expiration date, which should be in the future.

## Troubleshooting specific errors of the Hybrid Configuration wizard

If you receive an error while running the Hybrid Configuration wizard, you can frequently resolve the issue by doing a few simple checks.

- **Default Receive Connector cannot be found on server &lt;Server Name&gt;**: This message appears if the Receive connector on any Exchange server listed in the following Exchange Management Shell command isn't listening on TCP port 25 for both the IPv4 and IPv6 protocols:

    ```powershell
    (Get-HybridConfiguration).ReceivingTransportServers
    ```

    To verify the Receive connectors from the previous command have the correct bindings, replace &lt;Server Name&gt; with the name of the Exchange server, and then run the following command in the Exchange Management Shell.

    ```powershell
    Get-ReceiveConnector -Server "<Server Name>" | Format-Table Identity,Bindings
    ```

    The command should return the following value for Bindings: `{[::]:25, 0.0.0.0:25}`.

    If this binding isn't listed, you need to add it to the Receive connector using the *Bindings* parameter on the **Set-ReceiveConnector** cmdlet. For details, see [Set-ReceiveConnector](/en-us/powershell/module/exchangepowershell/set-receiveconnector).

## Troubleshooting mail flow issues

Refer to the following blog post: [Demystifying and troubleshooting hybrid mail flow: when is a message internal?](https://techcommunity.microsoft.com/t5/exchange-team-blog/demystifying-and-troubleshooting-hybrid-mail-flow-when-is-a/ba-p/1420838).