---
layout: Conceptual
title: Hybrid Configuration wizard | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-configuration-wizard
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
ms.topic: article
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
ms.assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms.reviewer: 
description: Admins can learn about Exchange Hybrid configuration and the Hybrid Configuration wizard.
ms.date: 2026-10-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e7024d10-1b59-3ee5-b8e4-8542e0a5d93d
document_version_independent_id: ccabd014-2431-b29a-5f79-259bcc3afc17
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-configuration-wizard.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-configuration-wizard
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-configuration-wizard.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: c8f1022f-9caa-7041-4fd7-663c5f8d3e83
---

# Hybrid Configuration wizard | Microsoft Learn

This article gives you an overview of the Exchange hybrid deployment process using the Hybrid Configuration wizard.

For more information about hybrid deployments, check out [Exchange Server Hybrid Deployments](exchange-hybrid).

## Hybrid configuration process

Here's a quick overview of what the Hybrid Configuration wizard does:

1. Create the **HybridConfiguration** object in your on-premises Active Directory. This object stores the hybrid configuration information for the hybrid deployment.
2. Complete the following steps:
    1. Gather existing on-premises Exchange and Active Directory topology configuration data, cloud organization data, and Exchange Online configuration data.
    2. Define several organization parameters.
    3. Run an extensive sequence of configuration tasks in both on-premises Exchange and Exchange Online.

Important

There are several important considerations and prerequisites that you need to complete before you use the Hybrid Configuration wizard. These requirements are described in [Hybrid deployment prerequisites](hybrid-deployment-prerequisites). After you meet all of these requirements, you'll be ready to use the Hybrid Configuration wizard.

The general phases of the hybrid deployment configuration process are described in the following section:

### Verify prerequisites and do topology checks

Verify that your on-premises and Exchange Online organizations can support a hybrid deployment. For example, the following items are checked:

- On-premises Exchange server versions
- Exchange Online version
- Active Directory synchronization presence and configuration
- Federated and accepted domains
- Existing federation trust and organization relationships
- Web Services virtual directories
- Exchange certificates

### Account permissions requirements

Verify that the on-premises and cloud accounts have the appropriate permissions to connect to both environments. Hybrid deployment management accounts require the following role group memberships as outlined in the next section.

#### Exchange Server on-premises

The account that is used to configure Exchange hybrid, must be a member of the `Organization Management` role group.

#### Exchange Online

In the next section of the documentation, we describe the permissions required to successfully run the HCW to either establish a new hybrid configuration or update an existing one. Note that `Global admin` permissions are required if Exchange hybrid is configured for the first time!

##### Minimal Hybrid Configuration

This table shows the permissions that are required, when you have a `Minimal Hybrid Configuration` configured:

| Granular hybrid configuration | Classic Hybrid permissions needed | Modern Hybrid permissions needed |
| --- | --- | --- |
| Not available | `Exchange admin` | `Global admin` |

##### Full Hybrid Configuration

This table shows the permissions that are required, when you have a `Full Hybrid Configuration` configured:

| Granular hybrid configuration | Classic Hybrid permissions needed | Modern Hybrid permissions needed |
| --- | --- | --- |
| `Oauth, Intra Organization Connector and Organization Relationship` | `Global admin` | `Global admin` |
| `Dedicated Exchange Server Application in Entra ID` | `Global admin` | `Global admin` |
| `Update Coexistence Domain in Exchange Server Accepted domain and Email Address Policy` | `Exchange admin` | `Global admin` |
| `Migration Endpoint` | `Exchange admin` | `Global admin` |
| `Organization Configuration Transfer` | `Exchange admin` | `Global admin` |
| `Outbound Connector in M365 Organization` | `Exchange admin` | `Global admin` |
| `Inbound Connector in M365 Organization` | `Exchange admin` | `Global admin` |
| `Receive Connector on Exchange Hybrid Server` | `Exchange admin` | `Global admin` |
| `Send Connector on Exchange Hybrid Server` | `Exchange admin` | `Global admin` |
| `Enable Centralized Mail Transport` | `Exchange admin` | `Global admin` |
| `Update Secure Mail Certificate for connectors` | `Exchange admin` | `Global admin` |

Tip

You can find more information about each hybrid configuration scenario in the [Choose Exchange Hybrid Configuration](hybrid-configuration-wizard-choose-configuration-feature#how-to-use-the-new-choose-exchange-hybrid-configuration-feature) documentation.

### Hybrid deployment configuration changes

Make the required configuration changes to create and enable the hybrid deployment. All changes are automatically logged in the hybrid configuration log. By default, the hybrid configuration log is located on the on-premises Mailbox server at `%UserProfile%\AppData\Roaming\Microsoft\Exchange Hybrid Configuration`.

Important

Inbound mail flow is controlled by your organization's MX record. Inbound internet mail for a hybrid deployment isn't configured by the Hybrid Configuration wizard.

## Hybrid configuration features

By default, the Hybrid Configuration wizard automatically enables all hybrid deployment features each time it runs. To disable specific hybrid configuration features, you need to use the **Set-HybridConfiguration** in the Exchange Management Shell. The wizard enables the following hybrid deployment features by default:

- **Free/busy sharing**: Enables calendar information to be shared between on-premises and Exchange Online users. Free/busy sharing is enabled as part of the federated sharing and organization relationship configuration for on-premises and cloud environments. Learn more at [Sharing](sharing-exchange-2013-help).
- **MailTips**: MailTips are informative messages that users see as they compose messages. Users can adjust messages before they're sent to avoid undesirable situations or non-delivery reports (NDRs). For more information, see [MailTips in Exchange](mailtips-exchange-2013-help) and [MailTips in Exchange Online](clients-and-mobile-in-exchange-online/mailtips/mailtips).
- **Online archiving**: Exchange Online host user email archive for both on-premises and cloud users. For more information, see [Configure Exchange Online Archiving](/en-us/purview/enable-archive-mailboxes).
- **Outlook on the web redirection**: Provides one URL to access both on-premises and Exchange Online mailboxes via Outlook on the web (formerly known as Outlook Web App or OWA). Client Access servers automatically redirect requests to on-premises mailbox servers or provide the link to Exchange Online mailboxes.
- **Exchange ActiveSync redirection**: Most Exchange ActiveSync clients will now be automatically reconfigured when the mailbox is moved to Exchange Online. For more information, see [Exchange ActiveSync device settings with Exchange hybrid deployments](activesync-settings).
- **Secure mail**: Uses Transport Layer Security (TLS) for secure mail delivery between the on-premises and cloud environments. On-premises Exchange and Exchange Online are mutually authenticated through digital certificate subjects and email headers. Rich-text message formatting is preserved across the organizations.

## Hybrid configuration options

The Hybrid Configuration wizard allows many customizations for the hybrid deployment. To update a hybrid configuration setting after you initially configured hybrid, you can use the Hybrid Configuration wizard or the Exchange Management Shell.

The following table describes the major options:

| Configuration area | Description |
| --- | --- |
| Dedicated Exchange Server Application in Entra ID | The Hybrid Configuration wizard (HCW) provisions a [dedicated Exchange hybrid application](hybrid-deployment/deploy-dedicated-hybrid-app) in Microsoft Entra ID to support hybrid features such as Free/Busy, MailTips, and Photos. This approach isolates the on-premises Exchange server's identity from Exchange Online by replacing the previously used shared (first-party) service principal.This feature is available starting with specific Exchange Server builds, which are listed in the [Deploy dedicated Exchange hybrid app](hybrid-deployment/deploy-dedicated-hybrid-app#before-you-begin) documentation. This feature isn't available if HCW is executed by using a tenant hosted in Microsoft 365 operated by 21Vianet. To configure it in that environment, follow the steps in the [dedicated Exchange hybrid application](hybrid-deployment/deploy-dedicated-hybrid-app) documentation. |
| Domains | Adds Exchange Online as accepted domain to on-premises Exchange for hybrid mail flow and Autodiscover requests. By default, this domain is `<domain>.mail.onmicrosoft.com`, and is called the *coexistence domain*. The coexistence domain is used for secondary email addresses (proxy addresses) in any email address policies that contain the domains you specified in the Hybrid Configuration wizard. <br>You can only view the accepted domain by either running the following Exchange Online PowerShell command: `Get-AcceptedDomain| Format-List DomainName, IsCoexistenceDomain` or by going to the Exchange admin center and looking at accepted domains underneath Mail flow. *The domain **is not listed** in the Microsoft 365 admin center.* |
| Secure mail certificate | Select certificate that was issued by a trusted third-party Certificate Authority (CA). This certificate is used to authenticate and secure mail sent between the on-premises and Exchange Online organizations. |
| Exchange federated sharing | HCW configures OAuth authentication and organization relationships for the selected hybrid features. Federation Trust configuration is no longer available in HCW. <br> The wizard creates and configures organization relationships for both the on-premises and Exchange Online organizations to enable features such as: <br><br>- Free/busy sharing<br>- Outlook on the web redirection<br>- MailTips |
| Mail flow | Client Access servers- Exchange 2010: Hub Transport servers<br><br> The wizard configures any new and existing connectors as required: <br><br>- On-premises Exchange: Send connectors and Receive connectors<br>- Exchange Online: Inbound and Outbound connectors<br><br><br> For Exchange Online, you choose how to route outbound messages to the internet: <br><br>- Direct<br>- Routed through your on-premises Exchange servers<br><br><br>**Important**: Mail flow from the internet to recipients in your domain is controlled by the domain's MX record in DNS, not by the Hybrid Configuration wizard. |

## Hybrid Configuration Engine

The Hybrid Configuration Engine runs the core actions for configuring and updating a hybrid deployment, based on the `Update-HybridConfiguration` cmdlet. The Hybrid Configuration Engine compares the state of the *HybridConfiguration* Active Directory object with current on-premises Exchange and Exchange Online configuration settings. Tasks are run to match the deployment configuration settings to the parameters that are defined in the *HybridConfiguration* Active Directory object. No changes are made if the current configuration states already match what's defined in the *HybridConfiguration* Active Directory object.

The Hybrid Configuration Engine does the following steps to compare and update an existing hybrid deployment:

1. The *Update-HybridConfiguration* cmdlet triggers the Hybrid Configuration Engine to start.
2. The Hybrid Configuration Engine reads the "desired state" stored on the `HybridConfiguration` Active Directory object.
3. The Hybrid Configuration Engine discovers topology data and current configuration from the on-premises Exchange organization.
4. The Hybrid Configuration Engine discovers topology data and current configuration from the Exchange Online organization.
5. The Hybrid Configuration Engine establishes the "difference" between the on-premises Exchange and Exchange Online organizations.
6. The Hybrid Configuration Engine runs configuration tasks to establish the desired state.

The following figure describes how the Hybrid Configuration Engine retrieves and modifies configuration settings during the hybrid deployment process.

![Hybrid Configuration Engine flow.](exchangehybrid/media/hybridconfigurationengine.gif)