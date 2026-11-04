---
layout: Conceptual
title: Configure the large audience size for your organization in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/mailtips/configure-large-audience-size
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
ms.custom:
- has-azure-ad-ps-ref
description: You can use Exchange Online PowerShell to configure various settings that define how you use MailTips in your organization.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: b67b8c64-fa44-e6bf-98d9-ddc71cbd6042
document_version_independent_id: fd2dfd7a-19b3-348e-0cb5-644593d01679
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/mailtips/configure-large-audience-size.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/mailtips/configure-large-audience-size
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/mailtips/configure-large-audience-size.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: a6425d72-691c-d7cb-c246-ccbc2a235373
---

# Configure the large audience size for your organization in Exchange Online | Microsoft Learn

You can use Exchange Online PowerShell to configure various settings that define how you use MailTips in your organization.

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "MailTips" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- You can only use Exchange Online PowerShell to perform this procedure.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to configure the large audience size for your organization

You use the **Set-OrganizationConfig** cmdlet to configure the large audience size for your organization. When the sender adds a distribution group that has more members than the configured large audience size, they are shown the Large Audience MailTip. The large audience size is set to 25 by default. This example configures the large audience size to 50 in your organization.

```Set
Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50
```

For detailed syntax and parameter information, see [set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/set-organizationconfig).