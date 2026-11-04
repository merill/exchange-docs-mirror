---
layout: Conceptual
title: Exchange Server hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/exchange-hybrid
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
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
ms.assetid: 59e32000-4fcf-417f-a491-f1d8f9aeef9b
ms.reviewer: 
description: 'Summary: What you need to know to plan an Exchange hybrid deployment.'
ms.date: 2023-06-15T00:00:00.0000000Z
locale: en-us
document_id: c7e6349f-a40f-ea78-03c8-1506b195f8fa
document_version_independent_id: d97e8315-ddf1-1372-e9aa-bdb40a7de2b8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/exchange-hybrid.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: exchange-hybrid
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/exchange-hybrid.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: a7ef8257-bc4c-d073-44ab-1ed874aab043
---

# Exchange Server hybrid deployments | Microsoft Learn

**Summary**: What you need to know to plan an Exchange hybrid deployment.

A hybrid deployment offers organizations the ability to extend the feature-rich experience and administrative control they have with their existing on-premises Microsoft Exchange organization to the cloud. A hybrid deployment provides the seamless look and feel of a single Exchange organization between an on-premises Exchange organization and Exchange Online. In addition, a hybrid deployment can serve as an intermediate step to moving completely to an Exchange Online organization.

## Exchange hybrid deployment features

A hybrid deployment enables the following features:

- Secure mail routing between on-premises and Exchange Online organizations.
- Mail routing with a shared domain namespace. For example, both on-premises and Exchange Online organizations use the @contoso.com SMTP domain.
- A unified global address list (GAL), also called a "shared address book."
- Free/busy and calendar sharing between on-premises and Exchange Online organizations.
- Centralized control of inbound and outbound mail flow. You can configure all inbound and outbound Exchange Online messages to be routed through the on-premises Exchange organization.
- A single Outlook on the web URL for both the on-premises and Exchange Online organizations.
- The ability to move existing on-premises mailboxes to the Exchange Online organization. Exchange Online mailboxes can also be moved back to the on-premises organization if needed.
- Centralized mailbox management using the on-premises Exchange admin center (EAC).
- Message tracking, MailTips, and multi-mailbox search between on-premises and Exchange Online organizations.
- Cloud-based message archiving for on-premises Exchange mailboxes. Exchange Online Archiving can be used with a hybrid deployment. Learn more about Exchange Online Archiving at [Exchange Online Archiving service description](/en-us/office365/servicedescriptions/exchange-online-archiving-service-description/exchange-online-archiving-service-description).

## Exchange hybrid deployment considerations

Consider the following before you implement an Exchange hybrid deployment:

- **Hybrid deployment requirements**: Before you configure a hybrid deployment, you need to make sure your on-premises organization meets all of the prerequisites required for a successful deployment. For more information, see [Hybrid deployment prerequisites](hybrid-deployment-prerequisites).
- **Exchange ActiveSync clients**: When you move a mailbox from your on-premises Exchange organization to Exchange Online, all of the clients that access the mailbox need to be updated to use Exchange Online; this includes Exchange ActiveSync devices. Most Exchange ActiveSync clients will now be automatically reconfigured when the mailbox is moved to Exchange Online, however some older devices might not update correctly. For more information, see [Exchange ActiveSync device settings with Exchange hybrid deployments](activesync-settings).
- **Mailbox permissions migration**: On-premises mailbox permissions such as Send As, Full Access, Send on Behalf, and folder permissions, that are explicitly applied on the mailbox are migrated to Exchange Online. Inherited (non-explicit) mailbox permissions and permissions granted to objects that aren't mail enabled in Exchange Online are not migrated. You should ensure all permissions are explicitly granted and all objects are mail enabled prior to migration. Therefore, you have to plan for configuring these permissions in Exchange Online if applicable for your organization.
- **Support for cross-premises mailbox permissions**: Exchange hybrid deployments support the use of the Full Access and Send on Behalf Of permissions between mailboxes located in an on-premises Exchange organization and mailboxes located in Exchange Online. Additional steps are required for Send As permissions. Also, some additional configuration may be required to support cross-premises mailbox permissions depending on the version of Exchange installed in your on-premises organization. For more information, see [Delegate mailbox permissions](permissions#delegate-mailbox-permissions) in [Permissions in Exchange hybrid deployments](permissions) and [Configure Exchange to support delegated mailbox permissions in a hybrid deployment](hybrid-deployment/set-up-delegated-mailbox-permissions).
- **Offboarding**: As part of ongoing recipient management, you might have to move Exchange Online mailboxes back to your on-premises environment.

    For more information about how to move mailboxes in an Exchange 2010-based hybrid deployment, see [Move an Exchange Online mailbox to the on-premises organization](/en-us/previous-versions/exchange-server/exchange-141/hh882527%28v=exchg.141%29).

    For more information about how to move mailboxes in hybrid deployments based on Exchange 2013 or newer, see [Move mailboxes between on-premises and Exchange Online organizations in hybrid deployments](hybrid-deployment/move-mailboxes).
- **Mailbox forwarding settings**: Mailboxes can be set up to automatically forward mail sent to them to another mailbox. While mailbox forwarding is supported in Exchange Online, the forwarding configuration isn't copied to Exchange Online when the mailbox is migrated there. Before you migrate a mailbox to Exchange Online, make sure you export the forwarding configuration for each mailbox. The forwarding configuration is stored in the `DeliverToMailboxAndForward`, `ForwardingAddress`, and `ForwardingSmtpAddress` properties on each mailbox.

## Exchange hybrid deployment components

A hybrid deployment involves several different services and components:

- **Exchange servers**: At least one Exchange server needs to be configured in your on-premises organization if you want to configure a hybrid deployment. If you're running Exchange 2013 or older, you need to install at least one server running the Mailbox and Client Access roles. If you're running Exchange 2016 or newer, at least one server running the Mailbox role needs to be installed. If needed, Exchange Edge Transport servers can also be installed in a perimeter network and support secure mail flow with Microsoft 365 or Office 365.

    Note

    We don't support the installation of Exchange servers running the Mailbox or Client Access server roles in a perimeter network.

    Hybrid deployments require the latest Cumulative Update (CU) or Update Rollup (RU) that's available for your version of Exchange. We recommend using the Exchange Server with the latest CU and SU for configuring Hybrid. If you can't install the latest update, the immediately previous release is also supported.
- **Office 365 or Microsoft 365**: Several Office 365 and Microsoft 365 service subscriptions include an Exchange Online organization. Organizations configuring a hybrid deployment need to purchase a license for each mailbox that's migrated to or created in the Exchange Online organization.
- **Hybrid Configuration wizard**: Exchange includes the Hybrid Configuration wizard which provides you with a streamlined process to configure a hybrid deployment between on-premises Exchange and Exchange Online organizations.

    Learn more at [Hybrid Configuration wizard](hybrid-configuration-wizard).
- **Microsoft Entra authentication system**: The Microsoft Entra authentication system is a free cloud-based service that acts as the trust broker between your on-premises Exchange 2016 organization and the Exchange Online organization. On-premises organizations configuring a hybrid deployment must have a federation trust with the Microsoft Entra authentication system. The federation trust can either be created manually as part of configuring federated sharing features between an on-premises Exchange organization and other federated Exchange organizations or as part of configuring a hybrid deployment with the Hybrid Configuration wizard. A federation trust with the Microsoft Entra authentication system for your Exchange Online tenant is automatically configured when you activate your Microsoft 365 or Office 365 service account.

    Learn more at: [What is federation with Microsoft Entra ID?](/en-us/entra/identity/hybrid/connect/whatis-fed).
- **Microsoft Entra synchronization**: Microsoft Entra synchronization uses either [cloud sync](/en-us/entra/identity/hybrid/cloud-sync/what-is-cloud-sync) or [connect sync](/en-us/entra/identity/hybrid/connect/whatis-azure-ad-connect-v2) to replicate on-premises Active Directory information for mail-enabled objects to the cloud to support the unified global address list (GAL) and user authentication. Organizations configuring a hybrid deployment need to deploy cloud sync or connect sync on a separate, on-premises server to synchronize your on-premises Active Directory with Microsoft 365 or Office 365.

    Learn more at: [Exchange hybrid writeback for sync](https://aka.ms/ExchHybidWriteback).

## Hybrid deployment example

Take a look at the following scenario. It's an example topology that provides an overview of a typical Exchange 2016 deployment. Contoso, Ltd. is a single-forest, single-domain organization with two domain controllers and one Exchange 2016 server installed. Remote Contoso users use Outlook on the web to connect to Exchange 2016 over the Internet to check their mailboxes and access their Outlook calendar.

![On-premises Exchange deployment before hybrid deployment with Microsoft 365 or Office 365 is configured.](exchangehybrid/media/dad133ae-d18a-42ec-8f0a-dd1de391200e.png)

Let's say that you're the network administrator for Contoso, and you're interested in configuring a hybrid deployment. You deploy and configure a required Microsoft Entra Connect server and you also decide to use the Microsoft Entra Connect password synchronization feature to let users use the same credentials for both their on-premises network account and their Microsoft 365 or Office 365 account. After you complete the hybrid deployment prerequisites and use the Hybrid Configuration wizard to select options for the hybrid deployment, your new topology has the following configuration:

- Users will use the same username and password for logging on to the on-premises and Exchange Online organizations ("single sign-on").
- User mailboxes located on-premises and in the Exchange Online organization will use the same email address domain. For example, mailboxes located on-premises and mailboxes located in the Exchange Online organization will both use @contoso.com in user email addresses.
- All outbound mail is delivered to the Internet by the on-premises organization. The on-premises organization controls all messaging transport and serves as a relay for the Exchange Online organization ("centralized mail transport").
- On-premises and Exchange Online organization users can share calendar free/busy information with each other. Organization relationships configured for both organizations also enable cross-premises message tracking, MailTips, and message search.
- On-premises and Exchange Online users use the same URL to connect to their mailboxes over the Internet.

![On-premises Exchange deployment after hybrid deployment with Microsoft 365 or Office 365 is configured.](exchangehybrid/media/e8681849-f15d-4d0e-b77e-6105b6096c4b.png)

If you compare Contoso's existing organization configuration and the hybrid deployment configuration, you'll see that configuring a hybrid deployment has added servers and services that support additional communication and features that are shared between the on-premises and Exchange Online organizations. Here's an overview of the changes that a hybrid deployment has made from the initial on-premises Exchange organization.

| Configuration | Before hybrid deployment | After hybrid deployment |
| --- | --- | --- |
| Mailbox location | Mailboxes on-premises only. | Mailboxes on-premises and in Exchange Online. |
| Message transport | On-premises Mailbox servers handle all inbound and outbound message routing. | On-premises Mailbox servers handle internal message routing between the on-premises and Exchange Online organization. |
| Outlook on the web | On-premises Mailbox servers receive all Outlook on the web requests and displays mailbox information. | On-premises Mailbox servers redirect Outlook on the web requests to either on-premises Exchange 2016 Mailbox servers or provides a link to log on to Exchange Online. |
| Unified GAL for both organizations | Not applicable; single organization only. | On-premises Active Directory synchronization server replicates Active Directory information for mail-enabled objects to Exchange Online. |
| Single-sign on used for both organizations | Not applicable; single organization only. | On-premises Active Directory and Exchange Online use the same username and password for mailboxes located either on-premises or in Exchange Online. |
| Organization relationship established and a federation trust with Microsoft Entra authentication system | Trust relationship with the Microsoft Entra authentication system and organization relationships with other federated Exchange organizations may be configured. | Trust relationship with the Microsoft Entra authentication system is required. Organization relationships are established between the on-premises environment and the cloud. |
| Free/busy sharing | Free/busy sharing between on-premises users only. | Free/busy sharing between both on-premises and Exchange Online users. |

## Things to consider before configuring a hybrid deployment

Now that you're a little more familiar with what a hybrid deployment is, you need to carefully consider some important issues. Configuring a hybrid deployment could affect multiple areas in your current network and Exchange organization.

### Directory synchronization and single sign-on

Active Directory synchronization between the on-premises organization and the cloud, which is performed every 30 minutes by a server running Microsoft Entra Connect, is a requirement for configuring a hybrid deployment. Directory synchronization enables recipients in either organization to see each other in the global address list. It also synchronizes usernames and passwords which enables users to log in with the same credentials in both your on-premises organization and in Microsoft 365 or Office 365.

Note

If you choose to configure Microsoft Entra Connect with AD FS, usernames and passwords of on-premises users will still be synchronized to the cloud by default. However, users will authenticate with your on-premises Active Directory via AD FS as their primary method of authentication. If you wish to configure AD FS to fall back and authenticate against usernames and passwords that you have synchronized to the cloud in the event AD FS can't connect to your on-premises Active Directory, see [Tutorial: Set up password hash sync as backup for Azure Directory Federation Services](/en-us/entra/identity/hybrid/connect/tutorial-phs-backup).

All customers of Microsoft Entra ID and Microsoft 365 or Office 365 have a default limit of 50,000 objects (users, mail-enabled contacts, and groups) that determines how many objects you can create in your Microsoft 365 or Office 365 organization. After you verify your first domain, this limit is automatically increased to 500,000 objects for Microsoft Entra ID Free, or an unlimited number of objects for Microsoft Entra Basic or Premium. For more information, see [Microsoft Entra pricing](https://azure.microsoft.com/pricing/details/active-directory/).

In addition to a server running Microsoft Entra Connect, you'll also need to deploy a web application proxy server if you choose to configure AD FS. This server should be placed in your perimeter network and will act as an intermediary between your internal ADFS servers and the Internet. The web application proxy server needs to accept connections from clients and servers on the Internet using TCP port 443.

### Hybrid deployment management

You manage a hybrid deployment in Exchange 2016 via a single unified management console that allows for managing both your on-premises and Exchange Online organizations. The Exchange admin center (EAC), which replaces the Exchange Management Console and the Exchange Control Panel, allows you to connect and configure features for both organizations. When you run the Hybrid Configuration wizard for the first time, you will be prompted to connect to your Exchange Online organization. You need to use an account that is a member of the Organization Management role group to connect the EAC to your Exchange Online organization.

### Certificates

Secure Sockets Layer (SSL) digital certificates play a significant role in configuring a hybrid deployment. They help to secure communications between the on-premises Mailbox or Edge servers and the Exchange Online organization. Certificates are a requirement to configure several types of services. If you're already using digital certificates in your Exchange organization, you may have to modify the certificates to include additional domains or purchase additional certificates from a trusted certificate authority (CA). If you aren't already using certificates, you will need to purchase one or more certificates from a trusted CA.

Learn more at: [Certificate requirements for hybrid deployments](certificate-requirements)

### Bandwidth

Your network connection to the Internet will directly impact the communication performance between your on-premises organization and the Microsoft 365 or Office 365 organization. This is particularly true when moving mailboxes from your on-premises Exchange 2016 server to the Microsoft 365 or Office 365 organization. The amount of available network bandwidth, in combination with mailbox size and the number of mailboxes moved in parallel, will result in varied times to complete mailbox moves. Additionally, other services, such as SharePoint Server 2016 and Skype for Business, may also affect the available bandwidth for messaging services.

Before moving mailboxes to the cloud, you should:

- Determine the average mailbox size for mailboxes that will be moved.
- Determine the average connection and throughput speed for your connection to the Internet from your on-premises organization.
- Calculate the average expected transfer speed, and plan your mailbox moves accordingly.

Learn more at: [Networking](/en-us/office365/servicedescriptions/office-365-platform-service-description/networking).

### Unified Messaging

Note

Unified Messaging is not available in Exchange 2019.

Unified Messaging (UM) is supported in a hybrid deployment between your on-premises and Microsoft 365 or Office 365 organizations. Your on-premises telephony solution must be able to communicate with the cloud. This may require that you purchase additional hardware and software.

If you want to move mailboxes from your on-premises organization to the cloud, and those mailboxes are configured for UM, you should configure UM in your hybrid deployment prior to moving those mailboxes. If you move mailboxes before you configure UM in your hybrid deployment, those mailboxes will no longer have access to UM functionality.

### Information Rights Management

Information Rights Management (IRM) enables users to apply Active Directory Rights Management Services (AD RMS) templates to messages that they send. AD RMS templates can help prevent information leakage by allowing users to control who can open a rights-protected message, and what they can do with that message after it's been opened.

IRM in a hybrid deployment requires planning, manual configuration of the Microsoft 365 or Office 365 organization, and an understanding of how clients use AD RMS servers depending on whether their mailbox is in the on-premises or Exchange Online organization.

Learn more at: [IRM in Exchange hybrid deployments](irm)

### Mobile devices

Mobile devices are supported in a hybrid deployment. If Exchange ActiveSync is already enabled on your existing servers, they'll continue to redirect requests from mobile devices to mailboxes located on the on-premises Mailbox server. For mobile devices connecting to existing mailboxes that are moved from the on-premises organization to the cloud, Exchange ActiveSync profiles will automatically be updated to connect to the cloud on most phones. All mobile devices that support Exchange ActiveSync should be compatible with a hybrid deployment.

Learn more at: [Exchange ActiveSync](clients/exchange-activesync/exchange-activesync).

### Client requirements

We recommend that your clients use Outlook 2016 or Outlook 2013 for the best experience and performance in the hybrid deployment. Pre-Outlook 2010 clients aren't supported in hybrid deployments or with Microsoft 365 or Office 365.

### Licensing for Microsoft 365 and Office 365

To create mailboxes in, or move mailboxes to, Microsoft 365 or Office 365, you need to sign up for an appropriate subscription plan you must have licenses available. When you sign up, you'll receive a specific number of licenses that you can assign to new mailboxes or mailboxes moved from the on-premises organization. Each mailbox in the cloud must have a license.

### Antivirus and anti-spam services

Mailboxes moved to the cloud are automatically receive the built-in security features for all cloud mailboxes. If you chose to route all incoming email from the internet through Microsoft 365, you might need to purchase more Built-in security add-on for on-premises mailboxes licenses. We recommend you carefully evaluate whether the Built-in security add-on for on-premises mailboxes is appropriate to meet the antimalware and anti-spam needs of your on-premises organization. If you have protection in place for your on-premises organization, you might need to upgrade or configure your on-premises antivirus and anti-spam solutions for maximum protection across your organization.

For more information, see the following articles:

- [Built-in security features for all cloud mailboxes](/en-us/defender-office-365/eop-about)
- [Anti-malware protection in cloud organizations](/en-us/defender-office-365/anti-malware-protection-about)
- [Anti-spam protection in cloud organizations](/en-us/defender-office-365/anti-spam-protection-about)

### Public folders

Public folders are supported in the cloud and on-premises public folders can be migrated to the cloud. Additionally, public folders in the cloud can be moved to the on-premises Exchange organization. Both on-premises and cloud users can access public folders located in either organization using Outlook on the web, Outlook 2016, Outlook 2013, or Outlook 2010 SP2 or newer. Existing on-premises public folder configuration and access for on-premises mailboxes doesn't change when you configure a hybrid deployment.

Learn more at: [Public folders](collaboration/public-folders/public-folders).

### Accessibility

For information about keyboard shortcuts that may apply to the procedures in this checklist, see [Keyboard shortcuts for the Exchange admin center](accessibility/keyboard-shortcuts-in-admin-center).

## Key terminology

The following list provides you with definitions of the core components associated with hybrid deployments in Exchange 2013.

**centralized mail transport**

> 
> The hybrid configuration option in which all Exchange Online inbound and outbound Internet messages are routed via the on-premises Exchange organization. This routing option is configured in the Hybrid Configuration wizard. For more information, see [Transport options in Exchange hybrid deployments](transport-options).

**coexistence domain**

> 
> An accepted domain added to the on-premises organization for hybrid mail flow and Autodiscover requests for the Microsoft 365 or Office 365 service. This domain is added as a secondary proxy domain to any email address policies which have *PrimarySmtpAddress* templates for domains selected in the Hybrid Configuration wizard. By default, this domain is &lt;domain&gt;.mail.onmicrosoft.com.

***HybridConfiguration* Active Directory object**

> 
> The Active Directory object in the on-premises organization that contains the desired hybrid deployment configuration parameters defined by the selections chosen in the Hybrid Configuration wizard. The Hybrid Configuration Engine uses these parameters when configuring on-premises and Exchange Online settings to enable hybrid features. The contents of the *HybridConfiguration* object are reset each time the Hybrid Configuration wizard is run.

**hybrid configuration engine**

> 
> The Hybrid Configuration Engine (HCE) runs the core actions necessary for configuring and updating a hybrid deployment. The HCE compares the state of the *HybridConfiguration* Active Directory object with current on-premises Exchange and Exchange Online configuration settings and then executes tasks to match the deployment configuration settings to the parameters defined in the *HybridConfiguration* Active Directory object. For more information, see [Hybrid Configuration Engine](hybrid-configuration-wizard#hybrid-configuration-engine).

**hybrid configuration wizard (HCW)**

> 
> An adaptive tool offered in Exchange that guides administrators through configuring a hybrid deployment between their on-premises and Exchange Online organizations. The wizard defines the hybrid deployment configuration parameters in the *HybridConfiguration* object and instructs the Hybrid Configuration Engine to run the necessary configuration tasks to enable the defined hybrid features. For more information, see [Hybrid Configuration wizard](hybrid-configuration-wizard).

**Exchange 2010-based hybrid deployment**

> 
> A hybrid deployment configured using Service Pack 3 (SP3) and Update Rollup 11 (RU11) or later for Exchange Server 2010 on-premises servers as the connecting endpoint for the Microsoft 365 or Office 365 and Exchange Online services. A hybrid deployment option for on-premises Exchange 2010 and Exchange Server 2007 organizations.

**Exchange 2013-based hybrid deployment**

> 
> A hybrid deployment configured using Cumulative Update 15 (CU15) or later for on-premises Exchange 2013 servers as the connecting endpoint for the Microsoft 365, Office 365, and Exchange Online services. A hybrid deployment option for on-premises Exchange 2013, Exchange 2010, and Exchange 2007 organizations.

**Exchange 2016-based hybrid deployment**

> 
> A hybrid deployment configured using Cumulative Update 8 (CU8) or later for Exchange 2016 on-premises servers as the connecting endpoint for the Microsoft 365 or Office 365 and Exchange Online services. A hybrid deployment option for on-premises Exchange 2016, Exchange 2013, and Exchange 2010 organizations.

**secure mail transport**

> 
> An automatically configured feature of a hybrid deployment that enables secure messaging between the on-premises and Exchange Online organizations. Messages are encrypted and authenticated using transport layer security (TLS) with a certificate selected in the Hybrid Configuration wizard. Microsoft 365 or Office 365 organization is the endpoint for hybrid transport connections originating from the on-premises organization and the source for hybrid transport connections to the on-premises organization from Exchange Online.

## Exchange hybrid deployment documentation

The following table contains links to topics that will help you learn about and manage hybrid deployments in Microsoft Exchange.

| Topic | Description |
| --- | --- |
| [Hybrid Configuration wizard](hybrid-configuration-wizard) | Learn how the Hybrid Configuration wizard and the Hybrid Configuration Engine configure a hybrid deployment. |
| [Hybrid deployment prerequisites](hybrid-deployment-prerequisites) | Learn more about hybrid deployment prerequisites, including compatible Exchange Server organizations, Microsoft 365 or Office 365 requirements, and other on-premises configuration requirements. |
| [Certificate requirements for hybrid deployments](certificate-requirements) | Learn more about the requirements for digital certificates in hybrid deployments. |
| [Transport options in Exchange hybrid deployments](transport-options) | Learn more about the inbound and outbound message transport options in hybrid deployments. |
| [Transport routing in Exchange hybrid deployments](transport-routing) | Learn more about inbound and outbound message routing options in a hybrid deployment. |
| [Hybrid management in Exchange hybrid deployments](hybrid-management) | Learn more about managing your hybrid deployment with the Exchange admin center and Exchange Management Shell. |
| [Shared free/busy in Exchange hybrid deployments](shared-free-busy) | Learn more about calendar free/busy sharing between on-premises and Exchange Online organizations in a hybrid deployment. |
| [Server roles in Exchange hybrid deployments](server-roles) | Learn more about how the Exchange server roles function in a hybrid deployment. |
| [IRM in Exchange hybrid deployments](irm) | Learn more about how Information Rights Management functions in a hybrid deployment. |
| [Permissions in Exchange hybrid deployments](permissions) | Learn more about how a hybrid deployment uses Role-Based Access Control (RBAC) to control permissions. |
| [Edge Transport servers with hybrid deployments](edge-transport-servers) | Learn more about Exchange Edge Transport servers and how they are deployed and operate in a hybrid deployment. |
| [Single sign-on with hybrid deployments](single-sign-on) | Learn more about how single sign-on using password synchronization and AD FS function in a hybrid deployment. |
| [Hybrid Deployment procedures](hybrid-deployment/hybrid-deployment) | Explore procedures for creating and modifying hybrid deployments for your Exchange on-premises and Exchange Online organizations. |
| [Hybrid deployments with Exchange 2013 and Exchange 2010](exchange-2013-and-2010-hybrid/exchange-2013-and-2010-hybrid) | Learn more about Exchange 2013-based hybrid deployments with Exchange 2010 organizations. |
| [Hybrid deployments with Exchange 2013 and Exchange 2007](exchange-2013-and-2007-hybrid/exchange-2013-and-2007-hybrid) | Learn more about Exchange 2013-based hybrid deployments with Exchange 2007 organizations. |