---
layout: Conceptual
title: Configure mobile phones to access email in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/exchange-activesync/configure-email-on-mobile-phone
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
description: You can configure a mobile phone to use Microsoft Exchange ActiveSync. You should perform this procedure on each mobile phone in your organization.
ms.topic: article
author: AshaIyengar21
ms.author: lusassl
ms.assetid: 8d6e2cea-265a-43d9-a074-076f35658436
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2022-05-09T00:00:00.0000000Z
locale: en-us
document_id: 76e5ae32-b6bf-3623-cbf9-f39ebd842eaf
document_version_independent_id: 1d48750a-76ef-e18c-c50d-b5557248438f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/exchange-activesync/configure-email-on-mobile-phone.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/exchange-activesync/configure-email-on-mobile-phone
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/exchange-activesync/configure-email-on-mobile-phone.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/390894b2-8646-4f7e-b8cd-2209156272a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12b23b77-ab37-4318-a036-4f6690586386
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: a2c76f89-f68c-44d5-64f3-55bb8762c2d8
---

# Configure mobile phones to access email in Exchange Online | Microsoft Learn

You can configure a mobile phone to use Microsoft Exchange ActiveSync. You should perform this procedure on each mobile phone in your organization.

## Prerequisites

- You've reviewed the manufacturer's documentation for the mobile phone you want to configure.
- Exchange ActiveSync is enabled in your organization.

Note

For device-specific information about setting up Microsoft Exchange-based email on a phone or tablet, see [Set up Office apps and email on a mobile device](https://support.microsoft.com/office/7dabb6cb-0046-40b6-81fe-767e0b1f014f).

## Configure a mobile phone to use Exchange ActiveSync

Most mobile phones and devices are capable of using Autodiscover to configure the mobile email client to use Exchange ActiveSync. To configure an email account on most mobile phones, you'll need two pieces of information.

- The user's email address
- The user's password

If the mobile phone is unable to contact the Exchange server automatically through Autodiscover, you'll need to set up the mobile phone manually. Manual setup requires the user's email address and password, as well as the Exchange ActiveSync server name. In most organizations, the Exchange ActiveSync server name is the same as the Outlook on the web (formerly known as Outlook Web App) server name without the /owa, for example, mail.contoso.com.