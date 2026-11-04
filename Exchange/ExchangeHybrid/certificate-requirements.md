---
layout: Conceptual
title: Certificate requirements for hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/certificate-requirements
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
ms.reviewer: 
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
ms.assetid: 48d532cc-29f9-4009-9d2d-f19a9c13c320
description: In a hybrid deployment, digital certificates are an important part of securing the communication between the on-premises Exchange organization and Microsoft 365 and Office 365. Certificates enable each Exchange organization to trust the identity of another. Certificates also help to ensure that each Exchange organization is communicating to the right source.
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 5fee8aac-fb8d-452b-7c1d-56db8cd1c3ff
document_version_independent_id: 61edeeae-af33-1074-ac0e-9311f9ddeca7
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/certificate-requirements.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: certificate-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/certificate-requirements.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a562bc51-1940-9aab-f124-a3e913511c7a
---

# Certificate requirements for hybrid deployments | Microsoft Learn

In a hybrid deployment, digital certificates are an important part of securing the communication between the on-premises Exchange organization and Microsoft 365 or Office 365. Certificates enable each Exchange organization to trust the identity of another. Certificates also help to ensure that each Exchange organization is communicating to the right source.

In a hybrid deployment, many services make use of certificates:

- **Microsoft Entra Connect (Microsoft Entra Connect) with Active Directory Federation Services (AD FS)**: If you choose to deploy Microsoft Entra Connect with AD FS as part of your hybrid deployment, a certificate issued by a trusted third-party certificate authority (CA) is used to establish a trust between web clients and federation server proxies, to sign security tokens, and to decrypt security tokens.

    Learn more at [Certificates](/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff641701%28v=ws.10%29).
- **Exchange federation**: A self-signed certificate is used to create a secure connection between the on-premises Exchange servers and the Microsoft Entra authentication system.

    Learn more at [Sharing](sharing-exchange-2013-help).
- **Exchange services**: Certificates issued by a trusted third-party CA are used to help secure Secure Sockets Layer (SSL) communication between Exchange servers and clients. Services that use certificates include Outlook on the web, Exchange ActiveSync, Outlook Anywhere, and secure message transport.
- **Existing Exchange servers**: Your existing Exchange servers may make use of certificates to help secure Outlook on the web communication, message transport, and so on. Depending on how you use certificates on your Exchange servers, you might use self-signed certificates or certificates issued by a trusted third-party CA.

## Certificate requirements for a hybrid deployment

When configuring a hybrid deployment, you must use and configure certificates that you have purchased from a trusted third-party CA. The certificate used for hybrid secure mail transport must be installed on all on-premises Mailbox (Exchange 2016 and newer), and Mailbox and Client Access (Exchange 2013 and older) servers.

Important

If you're configuring a hybrid deployment in an organization that has Exchange servers deployed in multiple Active Directory forests, you must use a separate third-party CA certificate for each Active Directory forest.

When Exchange Edge Transport servers are deployed in an on-premises organization, this certificate must also be installed on all Edge Transport servers. Each Edge transport server must use a certificate that shares the same issuing CA and the same subject for hybrid secure mail to function correctly.

Multiple services, such as AD FS, Exchange federation, services, and Exchange, each require certificates. Depending on your organization, you may decide to do one of the following:

- Use a third-party certificate that's used by all services across multiple servers.
- Use a third-party certificate for each server that provides services.

Whether you choose to use the same certificate for all services or dedicate a certificate for each service depends on your organization and the service you're implementing. Here are some things to consider about each option:

- **Third-party certificate across multiple servers**: Third-party certificates that are used by services across multiple servers may be slightly cheaper to obtain, but they may complicate renewal and replacement. The complication occurs because, when a certificate needs replacement, you need to replace the certificate on every server where it's installed.
- **Third-party certificate for each server**: Using a dedicated certificate for each server that hosts services allows you to configure the certificate specifically for the services on that server. If you need to replace the certificate or renew it, you only need to replace it on the server where the services are installed. Other servers aren't impacted.

We recommend that you use a dedicated third-party certificate for any optional AD FS server, another certificate for the Exchange services for your hybrid deployment, and if needed, another certificate on your Exchange servers for other needed services or features. The on-premises federation trust configured as part of federated sharing in a hybrid deployment uses a self-signed certificate by default. Unless you have specific requirements, there's no need to use a third-party certificate with the federation trust configured as part of a hybrid deployment.

The services that are installed on a single server may require that you configure multiple fully qualified domain names (FQDNs) for the server. You should purchase a certificate that allows for the maximum required number of FQDNs. Certificates consist of the subject (also called a principal name) and one or more subject alternative names (SAN). The subject name is the primary SMTP domain that is shared between the on-premises and Exchange Online organizations. SANs are additional FQDNs that can be added to a certificate in addition to the subject name. If you need a certificate to support five FQDNs, purchase a certificate that allows for five domains to be added to the certificate: one subject name and four SANs.

The following table outlines the minimum suggested FQDNs that should be included on certificates configured for use in a hybrid deployment.

| Service | Suggested FQDN | Field |
| --- | --- | --- |
| Primary shared SMTP domain | contoso.com | Subject name |
| Autodiscover | Label that matches the external Autodiscover FQDN of your Exchange 2013 Client Access server, such as autodiscover.contoso.com | Subject alternative name |
| Transport | Label that matches the external FQDN of your Edge Transport servers, such as edge.contoso.com | Subject alternative name |

If you don't have to relay email messages to the Internet through Office 365, you can use the transport service name in the subject name instead of the primary shared SMTP domain. For more information, see [Configure a certificate-based connector to relay email messages through Office 365](/en-us/exchange/troubleshoot/email-delivery/office-365-notice).