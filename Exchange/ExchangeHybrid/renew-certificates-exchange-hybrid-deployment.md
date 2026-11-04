---
layout: Conceptual
title: Renew certificates in Exchange Hybrid deployment | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/renew-certificates-exchange-hybrid-deployment
Manager: dscontentpm
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: steps to renew TLS certificates in an Exchange Hybrid deployment
ms.date: 2026-08-07T00:00:00.0000000Z
ms.author: arindamt
author: arindamthokder
audience: Admin
ms.topic: install-set-up-deploy
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.custom:
- Exchange Hybrid
ms.reviewer: arindamt
locale: en-us
document_id: 4688381e-61e5-0a6d-5b97-1e2cf605b3b9
document_version_independent_id: 01e595ea-d532-bd5e-4aa4-40fa6252ecb1
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/renew-certificates-exchange-hybrid-deployment.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: renew-certificates-exchange-hybrid-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/renew-certificates-exchange-hybrid-deployment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 395bb8c8-eb2d-609b-782e-669a5924844e
---

# Renew certificates in Exchange Hybrid deployment | Microsoft Learn

## Summary

In an Exchange Hybrid deployment, Transport Layer Security (TLS) certificates securely share information between users in Exchange on-premises and Exchange Online. This secure sharing includes mail flow, free/busy sharing, and other features. While a self-signed certificate is enough for internal mail flow between servers in an on-premises organization, when you configure a hybrid deployment, you must use and configure certificates that you purchase from a trusted third-party CA for hybrid mail flow - [Certificate requirements for hybrid deployments](/en-us/exchange/certificate-requirements#certificate-requirements-for-a-hybrid-deployment).

If you renew an Exchange certificate without updating the associated hybrid configuration, you can disrupt secure communication between Exchange Online and Exchange on-premises. This disruption results in hybrid mail flow failures and other hybrid feature issues.

This article describes how to safely renew a certificate in an Exchange hybrid environment without affecting the rich hybrid services like secure mail flow, availability, and more.

The following diagram shows the major steps involved in the process:

[![Screenshot of Exchange hybrid certificate renewal workflow with decision point for subject/issuer changes.](exchangehybrid/media/renew-certificates-exchange-hybrid-deployment/certificate-flow.png)](exchangehybrid/media/renew-certificates-exchange-hybrid-deployment/certificate-flow.png#lightbox)

## Important considerations when renewing Exchange Certificate

- Hybrid mail flow depends on connectors and their TLS configuration.
- When you renew certificates, connectors might still reference the previous certificate, which can disrupt mail flow.

## Step 1: Identify current certificate used for hybrid mailflow

Send and Receive Connector don't store the thumbprint of the certificate. Connectors use the `TLSCertificateName` parameter to choose the certificate for Hybrid mail flow. Set this parameter in the format: **&lt;I&gt;Issuer&lt;S&gt;SubjectName**, where the values correspond to the issuer and subject name of the third-party CA certificate.

**Check Send and Receive Connector’s TLScertificatename parameter**

Get-SendConnector "Outbound to Office 365\*" | fl Name,TlsCertificateName

Get-ReceiveConnector "Server\ Default Frontend Server" | fl Name,TlsCertificateName

Note

By default, Exchange Server on-premises receives emails from Exchange Online through the **Default Frontend** Receive connector. Enter the name of this connector unless your environment uses a custom Receive connector to accept mail from your Exchange Online tenant.

### Verify if the certificate you plan to renew is used by current Hybrid Mailflow

Copy the subject name derived from the preceding step and run the following command (the example uses contoso as the subject name in the command)-

Get-ExchangeCertificate | where {$\_.Subject -like "\*contoso\*"} | fl Thumbprint,Subject,Services

If the output matches the certificate you plan to renew, the certificate is currently used for hybrid mailflow. If there are multiple **trusted 3rd-party** certificates with the same subject name and issuer name, Exchange server usually uses the one that's **valid (non-expired)** and has the **most recent Valid from date.**

If you're still not sure, you can [Analyze Exchange Server protocol logs](/en-us/exchange/mail-flow/connectors/analyze-protocol-logs#what-to-look-for-in-the-protocol-log) which clearly shows the certificate with thumbprint used by the connectors.

## Step 2: Verify certificate requirements and install it

Ensure the new certificate:

- Is issued by a trusted third-party certificate authority
- Has a valid certificate chain with root and intermediate certificates installed
- The certificate has an associated private key.

[Use the steps here](/en-us/exchange/architecture/client-access/renew-certificates) to generate a new certificate request and get the certificate issued by your certificate provider. When generating the Certificate Signing Request (CSR), set `PrivateKeyExportable` to `TRUE` and submit the request to the third-party certificate provider.

After you receive the certificate from the provider, follow the steps to [complete the pending Exchange Server certificate request](/en-us/exchange/architecture/client-access/complete-pending-certificate-requests). If more than one server is involved in routing email with Exchange Online, make sure you [export the certificate from Exchange server](/en-us/exchange/architecture/client-access/export-certificates) and [import or install the certificate](/en-us/exchange/architecture/client-access/import-certificates) on all other Exchange servers.

To learn about important considerations when renewing Exchange certificates, see [TLS Certificates in Exchange Hybrid - Common Issues & How to Fix them](https://techcommunity.microsoft.com/blog/exchange/tls-certificates-in-exchange-hybrid---common-issues--how-to-fix-them/4420592).

## Step 3: Assign the renewed certificate to SMTP

Enable the SMTP service on the new certificate. You can do this from EAC by following [assign certificates to Exchange Server services](/en-us/exchange/architecture/client-access/assign-certificates-to-services#use-the-eac-to-assign-a-certificate-to-exchange-services). Or run the following command from ```powershell

Enable-ExchangeCertificate -Thumbprint &lt;NewCertificateThumbprint&gt; -Services SMTP

When you assign the SMTP service to a renewed certificate, Exchange prompts you to overwrite the existing certificate set for transport services. Select **No** if you want to use the existing self-signed certificate for internal communication with other Transport Services and Edge server (if any). Continue using the self-signed certificate for internal transport communication because of higher validity.

## Step 4: Update hybrid connectors with new certificate

If the old and renewed certificate use the same subject and issuer name, you usually don't need to do anything. Exchange matches the new certificate with the existing `TlsCertificateName` parameter and automatically uses the new certificate based on the latest `Valid from` date. However, if they're different, run the Hybrid Configuration wizard (HCW) again and select the new certificate for hybrid mailflow. HCW automatically updates the required parameters.

If you don't want to run HCW, you can manually update the certificate configuration on connectors by using the following PowerShell commands:

> 
> $cert = Get-ExchangeCertificate -Thumbprint "&lt;new certificate thumbprint&gt;"
> 
> $TLSCertificateName = "&lt;i&gt;$($Cert.Issuer)&lt;s&gt;$($Cert.Subject)"
> 
> Set-ReceiveConnector -Identity "Receive Connector Identity" -TlsCertificateName $TLSCertificateName
> 
> Set-SendConnector -Identity “"Outbound to Office 365\*" -TlsCertificateName $TLSCertificateName

## Step 5: Restart transport services

Restart Exchange transport services to apply changes.

PowerShell

Restart-Service MSExchangeTransport

## Step 6: Edge Transport considerations (if applicable)

If your environment includes Edge Transport servers:

- Install the new certificate on the Edge server and enable it for SMTP Service.

> 
> When you assign the SMTP service to a renewed certificate, Exchange prompts you to overwrite the existing certificate set for transport services. Select **No** if you want to use the existing self-signed certificate for internal communication with other Transport Services and Edge server (if any).

- Using Exchange Management Shell on the Edge server, manually set the `TlsDomainCapabilities` and `Fqdn` parameters of the Receive connector of the Edge server. Follow the procedure mentioned at [Edge Transport servers with hybrid deployments](/en-us/exchange/edge-transport-servers).

## Step 7: Validate configuration

### Verify Send Connector configuration

PowerShell

Get-SendConnector "Outbound to Office 365" | fl TlsCertificateName

Make sure the TlsCertificateName has the current certificate’s issuer name and subject name in the format: **&lt;I&gt;Issuer&lt;S&gt;SubjectName**

Send test email from Exchange On-Premises to Exchange online and check [Exchange Server protocol logs](/en-us/exchange/mail-flow/connectors/analyze-protocol-logs#what-to-look-for-in-the-protocol-log) to know which certificate with thumbprint is used by the connector.

### Confirm mail flow

- Send test messages from:

    - On-premises → Exchange Online
    - Exchange Online → On-premises

## Common issues and best practices

Based on field experience and Exchange Team guidance:

- Always update connectors after certificate renewal to avoid mail flow disruption [\[techcommun...rosoft.com\]](https://techcommunity.microsoft.com/blog/exchange/tls-certificates-in-exchange-hybrid---common-issues--how-to-fix-them/4420592).
- Avoid importing certificates too early - Exchange might select the newest certificate unexpectedly.
- Maintain complete certificate chain (root + intermediate).
- Use HCW for consistent configuration updates across environments.