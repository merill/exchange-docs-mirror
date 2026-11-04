---
layout: Conceptual
title: Opt in to the Exchange Online endpoint for legacy TLS clients using POP3 or IMAP4 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/opt-in-exchange-online-endpoint-for-legacy-tls-using-pop3-or-imap4
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn how to opt in to Exchange Online endpoint for legacy TLS clients using POP3/IMAP4.
ms.topic: overview
author: alekyaj
ms.author: serdars
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2022-12-15T00:00:00.0000000Z
locale: en-us
document_id: 06769aa2-9df7-8567-4099-4d04da11291d
document_version_independent_id: d5d94eac-041c-746d-658d-b2d1ac8dc059
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/opt-in-exchange-online-endpoint-for-legacy-tls-using-pop3-or-imap4.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/opt-in-exchange-online-endpoint-for-legacy-tls-using-pop3-or-imap4
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/opt-in-exchange-online-endpoint-for-legacy-tls-using-pop3-or-imap4.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 4f555414-699d-5edf-b0ea-ed9d1e0722d0
---

# Opt in to the Exchange Online endpoint for legacy TLS clients using POP3 or IMAP4 | Microsoft Learn

Exchange Online no longer supports use of TLS1.0 and TLS1.1 in the service as of October 2020. This change is due to security and compliance requirements for our service. While no longer supported, our servers still allow clients to use those older versions of TLS when connecting to the POP3/IMAP4 endpoint (outlook.office365.com).

In 2022, we plan to completely disable those older TLS versions to secure our customers, and meet those security and compliance requirements. However, due to significant usage, we've created an opt-in endpoint that legacy clients can use with TLS1.0 and TLS1.1.

Note

This opt-in endpoint isn't available in GCC, GCC-High, or DoD environments that have legacy TLS permanently turned off.

## Configuring the new endpoint

If customers have POP3/IMAP4 clients that only support older TLS versions, they need to be configured to use the new endpoint for worldwide:

- pop-legacy.office365.com
- imap-legacy.office365.com

Customers who use Microsoft 365 operated by 21 Vianet need to configure their clients to use the endpoint:

- pop-legacy.partner.outlook.cn
- imap-legacy.partner.outlook.cn

Consumer users can use these less secure endpoints directly. For Enterprise users, tenant admins need to enable the following setting:

- The value `$true` for the AllowLegacyTLSClients parameter on the `Set-TransportConfig` cmdlet.

## Opt in to legacy client endpoint

You can opt in (or opt out) for your organization in the new EAC or by using [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

To opt in with the new EAC, go to the **Mail Flow** settings page under [Settings](https://admin.exchange.microsoft.com/#/settings) and toggle the setting labeled **Turn on use of legacy TLS clients**.

To opt in with Exchange Online PowerShell, run the following command:

```powershell
Set-TransportConfig -AllowLegacyTLSClients $true
```

To view the current status of the property, run the following command in Exchange Online PowerShell:

```powershell
Get-TransportConfig | Format-List AllowLegacyTLSClients
```