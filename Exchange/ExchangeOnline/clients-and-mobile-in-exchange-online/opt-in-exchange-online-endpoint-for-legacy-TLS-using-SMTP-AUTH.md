---
layout: Conceptual
title: Opt in to the Exchange Online endpoint for legacy TLS clients using SMTP AUTH | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/opt-in-exchange-online-endpoint-for-legacy-tls-using-smtp-auth
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn how to opt in to Exchange Online endpoint for legacy TLS clients using SMTP AUTH.
ms.topic: overview
author: AshaIyengar21
ms.author: serdars
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2024-05-29T00:00:00.0000000Z
locale: en-us
document_id: 950369cf-a20f-3079-23f9-bc52fc043873
document_version_independent_id: ab0315ac-b4d0-cb35-f29e-857ed9796ab9
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/opt-in-exchange-online-endpoint-for-legacy-TLS-using-SMTP-AUTH.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/opt-in-exchange-online-endpoint-for-legacy-tls-using-smtp-auth
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/opt-in-exchange-online-endpoint-for-legacy-TLS-using-SMTP-AUTH.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: d3112f97-668c-a8ed-21ca-deb36746cd12
---

# Opt in to the Exchange Online endpoint for legacy TLS clients using SMTP AUTH | Microsoft Learn

Note

We have already disabled TLS 1.0 and 1.1 for most Microsoft 365 services in the world wide environment. For Microsoft 365 operated by 21 Vianet, TLS1.0 and TLS1.1 was disabled on June 30, 2023.

Exchange Online no longer supports use of TLS1.0 and TLS1.1 in the service as of October 2020. This change is due to security and compliance requirements for our service. While no longer supported, our servers still allow clients to use those older versions of TLS when connecting to the SMTP AUTH endpoint (smtp.office365.com).

In 2022, we plan to completely disable those older TLS versions to secure our customers and meet those security and compliance requirements. However, due to significant usage, we've created an opt-in endpoint that legacy clients can use with TLS1.0 and TLS1.1. Note that this endpoint is not available in GCC, GCC-High, or DoD environments that have legacy TLS permanently turned off.

## Configuring the new endpoint

If customers have SMTP AUTH clients that only support older TLS versions, they need to be configured to use the new endpoint for world wide:

- `smtp-legacy.office365.com`

Customers who use Microsoft 365 operated by 21 Vianet need to configure their clients to use the endpoint

- `smtp-legacy.partner.outlook.cn`

To use this less secure endpoint, admins need to enable the following setting:

- The value `$true` for the *AllowLegacyTLSClients* parameter on the **Set-TransportConfig** cmdlet.

Make sure that the mailbox is configured to allow sending using SMTP AUTH. For more info, visit: [Enable or disable authenticated client SMTP submission (SMTP AUTH) in Exchange Online](/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission)

## Opt in to legacy client endpoint

You can opt in (or opt out) for your organization in the new EAC or by using [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

To opt in with the new EAC, go to the **Mail Flow** settings page under [Settings](https://admin.exchange.microsoft.com/#/settings) and toggle the setting labeled "Turn on use of legacy TLS clients"

To opt in, run the following command:

```PowerShell
Set-TransportConfig -AllowLegacyTLSClients $true
```

To view the current status of the property, run the following command in Exchange Online PowerShell:

```powershell
Get-TransportConfig | Format-List AllowLegacyTLSClients
```