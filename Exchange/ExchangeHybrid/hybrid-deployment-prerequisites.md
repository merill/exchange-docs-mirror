---
layout: Conceptual
title: Hybrid deployment prerequisites | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment-prerequisites
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
- Ent_O365_Hybrid
- Strat_EX_EXOBlocker
- Hybrid
- M365-email-calendar
ms.assetid: e7454db0-fed4-4662-8890-9501126b1ba2
ms.reviewer: 
description: What your Exchange environment needs before you can set up a hybrid deployment.
ms.date: 2026-10-13T00:00:00.0000000Z
locale: en-us
document_id: a2ddce84-2ec9-3744-1a3f-20303275affa
document_version_independent_id: 2c5ba0fc-80c4-8de0-61ba-5e73bf558766
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment-prerequisites.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment-prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment-prerequisites.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 31d2cb84-944a-e2b1-1b4a-979f4db2606d
---

# Hybrid deployment prerequisites | Microsoft Learn

Before you create and configure a hybrid deployment using the Hybrid Configuration wizard, your existing on-premises Exchange organization needs to meet certain requirements. If you don't meet these requirements, you won't be able to complete the steps within the Hybrid Configuration wizard and you won't be able to configure a hybrid deployment between your on-premises Exchange organization and Exchange Online.

## Prerequisites for hybrid deployment

The following prerequisites are required for configuring a hybrid deployment:

- **On-premises Exchange organization**: The version of Exchange you have installed in your on-premises organization determines the hybrid deployment version you can install. You should typically configure the newest hybrid deployment version that's supported in your organization as described in the following table:

| On-premises environment | Exchange 2019-based hybrid deployment | Exchange 2016-based hybrid deployment | Exchange 2013-based hybrid deployment | Exchange 2010-based hybrid deployment |
| --- | --- | --- | --- | --- |
| Exchange 2019 | Supported | Not supported | Not supported | Not supported |
| Exchange 2016 | Supported | Supported | Not supported | Not supported |
| Exchange 2013 | Supported | Supported | Supported | Not supported |
| Exchange 2010 | Not supported | Supported | Supported | Supported |

Important

Federation Trust configuration for Exchange 2010 or earlier is no longer available in HCW.

- **Exchange server releases**: Hybrid deployments require the latest Cumulative Update (CU) or Update Rollup (RU) that's available for your version of Exchange. If you can't install the latest update, the immediately previous release is also supported.

    Exchange CUs are released twice a year, so keeping your Exchange servers up-to-date gives you some additional flexibility if you periodically need extra time to complete upgrades.
- **Exchange server roles**: The server roles you need to install in your on-premises organization depend on the version of Exchange you have installed.

    - **Exchange 2016 and newer**: At least one Mailbox server.
    - **Exchange 2013**: At least one instance of Mailbox and Client Access server roles installed (separately or on one server; we strongly recommend on one server).
    - **Exchange 2010**: At least one instance of Mailbox, Hub Transport, and Client Access server roles installed (separately or on one server; we strongly recommend on one server).

        Hybrid deployments also support Exchange servers running the Edge Transport server role. Edge Transport servers also need to be updated to the latest CU or RU. We strongly recommend that you deploy Edge Transport servers in a perimeter network. You can't deploy Mailbox or Client Access servers in a perimeter network.

    Note

    If you already started a migration process with Exchange 2010 Hybrid endpoints and do not plan to keep on-premises mailboxes, continue your migration as-is. If you plan to keep some mailboxes on-premises, we strongly recommend that you introduce Exchange 2016 Hybrid endpoints (because Exchange 2010 has reached its end of support lifecycle). Continue your migration of Exchange 2010 mailboxes to Office 365, and then move the mailboxes that will stay on-premises to Exchange 2016 servers. After you have removed all of your Exchange 2010 servers, you can then introduce Exchange 2019 servers as your new Hybrid endpoints and also move your remaining on-premises mailboxes to Exchange 2019 servers.
- **Microsoft 365 or Office 365**: Hybrid deployments are supported in all Microsoft 365 and Office 365 plans that support Microsoft Entra synchronization. All Microsoft 365 Business Standard, Business Basic, Enterprise, Government, Academic and Midsize plans support hybrid deployments. Microsoft 365 Apps for business and Home plans don't support hybrid deployments.

    Learn more at [Microsoft 365](https://www.microsoft.com/microsoft-365).
- **Custom domains**: Register any custom domains you want to use in your hybrid deployment with Microsoft 365 or Office 365. You can do this by using the Microsoft 365 portal, or by optionally configuring Active Directory Federation Services (AD FS) in your on-premises organization.

    Learn more at [Add your domain to Microsoft 365 or Office 365](/en-us/microsoft-365/admin/setup/add-domain).
- **Active Directory synchronization**: Deploy the Microsoft Entra Connect or cloud sync tool to enable Active Directory synchronization with your on-premises organization.

    Learn more at [Microsoft Entra Connect User Sign-on options](/en-us/entra/identity/hybrid/connect/plan-connect-user-signin) and [What is Microsoft Entra Cloud Sync?](/en-us/entra/identity/hybrid/cloud-sync/what-is-cloud-sync).
- **Autodiscover DNS records**: Configure the Autodiscover record for your existing SMTP domains in your public DNS to point to your on-premises Exchange servers (an Exchange 2010/2013 Client Access server or an Exchange 2016/2019 Mailbox Server).
- **Certificates**: Assign Exchange services to a valid digital certificate that you purchased from a trusted public certificate authority (CA). You can't use self-signed certificates for Exchange services in a hybrid deployment.

    The Internet Information Services (IIS) instance on the Exchange servers that are configured in the hybrid deployment require a valid digital certificate purchased from a trusted CA.

    The EWS external URL and the Autodiscover endpoint that you specified in your public DNS must be listed in the Subject Alternative Name (SAN) field of the certificate. The certificates that you install on the Exchange servers for mail flow in the hybrid deployment must all be issued by the same certificate authority and have the same subject.

    Learn more at [Certificate requirements for hybrid deployments](certificate-requirements).
- **EdgeSync**: If you've deployed Edge Transport servers in your on-premises organization and want to configure the Edge Transport servers for hybrid secure mail transport, you need configure EdgeSync prior to using the Hybrid Configuration wizard. You also need to run EdgeSync each time you apply a new CU to an Edge Transport server.

    Important

    Although EdgeSync is a requirement in deployments with Edge Transport servers, additional configuration settings are required when you configure Edge Transport servers for hybrid secure mail transport.

    Learn more at [Edge Transport servers with hybrid deployments](edge-transport-servers).
- **Microsoft .NET Framework**: To verify the versions that can be used with your specific version of Exchange, see [Exchange Server supportability matrix - Microsoft .NET Framework](plan-and-deploy/supportability-matrix#net-framework).
- **Unified Messaging-enabled (UM) mailboxes**: If you have UM-enabled mailboxes and you want to move them to Microsoft 365 or Office 365, you need to meet the following requirements **before** you move them:

    - Lync Server 2010, Lync Server 2013, or Skype for Business Server 2015 or later integrated with your on-premises telephony system.

        or
    - Skype for Business Online integrated with your on-premises telephony system.

        or
    - A traditional on-premises PBX or IP-PBX solution.

        For more information, check out [Telephone system integration with UM in Exchange Online](voice-mail-unified-messaging/telephone-system-integration-with-um/telephone-system-integration-with-um), [Plan for Skype for Business Server and Exchange Server migration](/en-us/SkypeForBusiness/hybrid/plan-um-migration), and [Set up Cloud Voicemail](/en-us/microsoftteams/set-up-phone-system-voicemail).

## Hybrid deployment protocols, ports, and endpoints

You need to configure the following protocols, ports, and connection endpoints in the firewall that protects your on-premises organization as described in the following table.

Important

The related Microsoft 365 and Office 365 endpoints are vast, ever-changing, and aren't listed here. Instead, see the sections *Exchange Online* and *Microsoft 365 Common and Office Online* in [Microsoft 365 and Office 365 URLs and IP address ranges](/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges) to identify the endpoints for each port listed here.

Note

The ports required for mail flow and client connectivity in your on-premises Exchange organization not related to the hybrid configuration are described in [Network ports for clients and mail flow in Exchange](plan-and-deploy/deployment-ref/network-ports).

| Source | Protocol/Port | Target | Comments |
| --- | --- | --- | --- |
| Exchange Online endpoints | TCP/25 (SMTP/TLS) | Exchange 2019/2016 Mailbox/Edge <br> Exchange 2013 CAS/Edge <br><br> Exchange 2010 Hub/Edge | On-premises Exchange Servers configured to host receive connectors for secure mail transport with Exchange Online in the Hybrid Configuration wizard |
| Exchange 2019/2016 Mailbox/Edge <br> Exchange 2013 CAS/Edge <br><br> Exchange 2010 Hub/Edge | TCP/25 (SMTP/TLS) | Exchange Online endpoints | On-premises Exchange Servers configured to host send connectors for secure mail transport with Exchange Online in the Hybrid Configuration wizard |
| Exchange Online endpoints | TCP/443 (HTTPS) | Exchange 2019/2016 Mailbox <br> Exchange 2013/2010 CAS | On-premises Exchange Servers used to publish Exchange Web Services and Autodiscover to Internet |
| Exchange 2019/2016 Mailbox <br> Exchange 2013/2010 CAS | TCP/443 (HTTPS) | Exchange Online endpoints | On-premises Exchange Servers used to publish Exchange Web Services and Autodiscover to Internet |
| Exchange SE Mailbox | TCP/443 (HTTPS) | [Graph API endpoint](/en-us/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints) | On-premises Exchange Servers used to access Graph API for hybrid features like Free/Busy, MailTips, and Photos. More information can be found in the [Deploy dedicated Exchange hybrid app](hybrid-deployment/deploy-dedicated-hybrid-app) documentation. |
| Exchange 2019/2016 Mailbox/Edge <br> Exchange 2013 CAS/Edge <br><br> Exchange 2010 Hub/Edge | 80 | ctldl.windowsupdate.com/\* | For hybrid functionality, Exchange Servers needs outbound connectivity to various Certificate Revocation List (CRL) endpoints mentioned [here](/en-us/azure/security/fundamentals/azure-ca-details). We strongly recommend letting Windows maintain the [Certificate Trust List (CTL)](https://support.microsoft.com/topic/117bc163-d9e0-63ad-5a79-e61f38be8b77) on your machine. Otherwise, this must be maintained manually on a regular basis. To allow Windows to maintain the CTL, the URL must be reachable from the computer on which Exchange Server is installed. |

The following table provides more detailed information about the involved on-premises endpoints:

| Description | Port and protocol | On-premises endpoint | Authentication Provider | Authorization Method | Pre-Auth Supported? |
| --- | --- | --- | --- | --- | --- |
| SMTP mail flow between Microsoft 365 or Office 365 and on-premises Exchange | TCP 25 (SMTP/TLS) | Exchange 2019/2016 Mailbox/Edge <br> Exchange 2013 CAS/Edge <br><br> Exchange 2010 Hub/Edge | N/A | Certificate-based | No |
| Autodiscover | TCP 443 (HTTPS) | Exchange 2019/2016 Mailbox server: /autodiscover/autodiscover.svc/wssecurity <br> Exchange 2013/2010 CAS: /autodiscover/autodiscover.svc | Microsoft Entra authentication system | WS-Security Authentication | No |
| Free/busy, MailTips, and message tracking (EWS) | TCP 443 (HTTPS) | Exchange 2019/2016 Mailbox or Exchange 2013/2010 CAS: <br> /ews/exchange.asmx/wssecurity | Microsoft Entra authentication system | WS-Security Authentication | No |
| Multi-mailbox search (EWS) | TCP 443 (HTTPS) | Exchange 2019/2016 Mailbox or Exchange 2013/2010 CAS: <br> /ews/exchange.asmx/wssecurity <br><br> /autodiscover/autodiscover.svc/wssecurity <br><br> /autodiscover/autodiscover.svc | Auth Server | WS-Security Authentication | No |
| Mailbox migrations (EWS) | TCP 443 (HTTPS) | Exchange 2019/2016 Mailbox or Exchange 2013/2010 CAS: <br>/ews/mrsproxy.svc | NTLM | Basic | No |
| OAuth (Autodiscover and EWS) | TCP 443 (HTTPS) | Exchange 2019/2016 Mailbox or Exchange 2013/2010 CAS: <br> /ews/exchange.asmx/wssecurity <br><br> /autodiscover/autodiscover.svc/wssecurity <br><br> /autodiscover/autodiscover.svc | Auth Server | WS-Security Authentication | No |
| AD FS (Windows Server) | TCP 443 (HTTPS) | Windows 2012 R2/2016 Server: /adfs/\* | Microsoft Entra authentication system | Varies per config. | 2-factor |
| Microsoft Entra Connect | TCP 443 (HTTPS) | Windows 2012 R2/2016 Server (AD FS): /adfs/\* | Microsoft Entra authentication system | Varies per config. | 2-factor |

For even more detail about this information, see [Deep Dive: How Hybrid Authentication Really Works](https://techcommunity.microsoft.com/t5/exchange-team-blog/deep-dive-how-hybrid-authentication-really-works/ba-p/606780), [Demystifying and troubleshooting hybrid mail flow: when is a message internal?](https://techcommunity.microsoft.com/t5/exchange-team-blog/demystifying-and-troubleshooting-hybrid-mail-flow-when-is-a/ba-p/1420838), [Transport routing in Exchange hybrid deployments](transport-routing), [Configure mail flow using connectors](mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow), and [Manage mail flow with mailboxes in multiple locations (Exchange Online and on-premises)](mail-flow-best-practices/manage-mail-flow-for-multiple-locations).

## Recommended tools and services

The following tools and services are beneficial when you're configuring hybrid deployments with the Hybrid Configuration wizard:

- **Mail migration advisor**: Gives you step-by-step guidance to configure a hybrid deployment between your on-premises organization and Microsoft 365 or Office 365, or migrate completely to Microsoft 365 or Office 365.

    Learn more at [Use the mail migration advisor](mail-migration-jump).
- **Remote Connectivity Analyzer tool**: The Microsoft Remote Connectivity Analyzer tool checks the external connectivity of your on-premises Exchange organization and makes sure that you're ready to configure your hybrid deployment. We strongly recommend that you check your on-premises organization with the Remote Connectivity Analyzer tool prior to configuring your hybrid deployment with the Hybrid Configuration wizard.

    Learn more at [Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/).
- **Single sign-on**: Single sign-on enables users to access both the on-premises and Exchange Online organizations with a single username and password. It provides users with a familiar sign-on experience and allows administrators to easily control account policies for Exchange Online organization mailboxes by using on-premises Active Directory management tools.

    You have a couple of options when deploying single sign-on: password synchronization and Active Directory Federation Services. Both options are provided by Microsoft Entra Connect. Password synchronization enables almost any organization, no matter the size, to easily implement single sign-on. For this reason, and because the user experience in a hybrid deployment is significantly better with single sign-on enabled, we strongly recommend implementing it. For very large organizations, such as those with multiple Active Directory forests that need to join the hybrid deployment, Active Directory Federation Services is required.

    Learn more at [Single sign-on with hybrid deployments](single-sign-on).