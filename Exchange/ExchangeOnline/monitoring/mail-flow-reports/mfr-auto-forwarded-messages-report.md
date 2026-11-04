---
layout: Conceptual
title: Auto forwarded messages report in the new Exchange admin center (EAC) in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-auto-forwarded-messages-report
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
ms.author: srvar
author: serdars
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
description: Admins can learn how to use the Auto forwarded messages report in the new Exchange admin center to see the internal senders and external recipients of forwarded messages from your organization.
ms.date: 2026-07-09T00:00:00.0000000Z
locale: en-us
document_id: c10f6e93-cb4a-1f68-36b9-0a86a8c07df0
document_version_independent_id: c077a7ba-44ed-c8dc-80de-4f0944417476
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-auto-forwarded-messages-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-auto-forwarded-messages-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-auto-forwarded-messages-report.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: df4fb246-ad30-7b34-0266-b4deab8f8802
---

# Auto forwarded messages report in the new Exchange admin center (EAC) in Exchange Online | Microsoft Learn

The **Auto-forwarded messages** report in the new Exchange admin center (new EAC) displays information on messages that are automatically forwarded from your organization to recipients in external domains. You can use this report to look for potential data leaks.

Note

By default, the report shows data for the last 7 days. If the report is empty, try changing the date range.

The summary page allows you to query up to the last 90 days of data. The new activity page shows the activity of the last 7 days. The request report feature has a limit of the last 30 days.

> 
> For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

The overview section contains the following charts:

- **Forwarding type**: Typical values are:
    - **Mail flow rules**
    - **Inbox rules**
    - **SMTP forwarding**: This is automatic forwarding that admins can configure on a mailbox as described in [Configure email forwarding for a mailbox](../../recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding).
- **Recipient domain**
- **Forwarding users**

If you hover over a specific color in the chart, you'll see the associated numbers for that specific forwarding type, recipient domain, or forwarding user.

![Overview of the Auto forwarded messages report.](../../exchangeonline/media/mfr-auto-forwarded-messages-report.png)

The **Auto forwarded message details** section shows the following information about each-specific forwarder (the user account that's doing the forwarding):

- **Forwarders**
- **Forwarding type**
- **Recipient name**
- **Recipient domain**
- **Details**: If the message was auto-forwarded by a Transport rule, the ID of the rule is shown. Otherwise, this value is blank. In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), you can use the [Get-TransportRule](/en-us/powershell/module/exchangepowershell/get-transportrule) cmdlet to identify the rule by running the following command: `Get-TransportRule -Identity <RuleIDParameter>`. For example, `Get-TransportRule -Identity 8754395095991580000`.
- **Forward count**
- **First forward date**

Click **Export** to export the displayed results to a .csv file.

## Insights

Two insights are generated based on the report data: [New domains being forwarded email](../mail-flow-insights/mfi-new-domains-being-forwarded-email-insight) and [New users forwarding email](../mail-flow-insights/mfi-new-users-forwarding-email-insight). Each insight provides a summary of the number of new forwarders or domains with a link back to this report.