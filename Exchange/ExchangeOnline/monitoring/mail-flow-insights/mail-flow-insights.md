---
layout: Conceptual
title: Mail flow insights in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-insights/mail-flow-insights
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: serdars
author: serdars
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
description: Admins can learn how to use the mail flow insights dashboard in the new Exchange admin center to find and fix mail flow related issues.
ms.custom: 
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: fb4dc60f-f04e-9c34-9d49-1a909283b368
document_version_independent_id: 2a2ff855-fe63-f1fc-e137-3367acdbd128
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-insights/mail-flow-insights.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-insights/mail-flow-insights
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-insights/mail-flow-insights.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 1b6cbafb-9416-c0f0-26ae-d3b800f3b267
---

# Mail flow insights in the new EAC in Exchange Online | Microsoft Learn

Admins can use the insights dashboard in the new Exchange admin center (new EAC) to discover issues with mail flow and take corrective action. If an item appears in the mail flow insights dashboard, you need to investigate and likely fix the issue.

The following mail flow insights are available:

- [Fix possible mail loop insight](mfi-fix-possible-mail-loop-insight)
- [Fix slow mail flow rules insight](mfi-fix-slow-mail-flow-rules-insight)
- [New domains being forwarded email insight](mfi-new-domains-being-forwarded-email-insight)
- [New users forwarding email insight](mfi-new-users-forwarding-email-insight)
- [Domain expiring soon insight](domain-expiry-notification-feature)
- [Mailboxes exceeding receiving limits insight](mailboxes-exceeding-receiving-limits-insights)

## Permissions required to view and use mail flow insights

To use the mail flow insights to take corrective action, you need to be a member of one of the following role groups:

- Organization Management
- Security Administrator&lt;sup&gt;\*

For read only access to the mail flow insights, you need to be a member of one of the following role groups:

- Security Reader^\*^
- View-only Organization Management
- View-Only Recipients

For more information, see [Permissions in Exchange Online](../../permissions-exo/permissions-exo) and [Manage role groups in Exchange Online](../../permissions-exo/role-groups).

&lt;sup&gt;\* You manage these role groups in the [Microsoft Entra admin center](https://aad.portal.azure.com).

## Where to find mail flow insights

To see the mail flow insights, open the new EAC at https://admin.exchange.microsoft.com and select **Insights**.

To go directly to the mail flow insights dashboard, open https://admin.exchange.microsoft.com/#/insights.