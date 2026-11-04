---
layout: Conceptual
title: Fix slow mail flow rules insight in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-insights/mfi-fix-slow-mail-flow-rules-insight
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
description: Admins can learn how to use the Fix slow mail flow rules insight in the new Exchange admin center to identify and fix inefficient or broken mail flow rules (also known as transport rules) in their organization.
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: 61fbe51f-8247-9b0c-6738-4414b59bb0ec
document_version_independent_id: ba2d4870-df3b-bb1e-ea6a-560e5b979d68
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-insights/mfi-fix-slow-mail-flow-rules-insight.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-insights/mfi-fix-slow-mail-flow-rules-insight
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-insights/mfi-fix-slow-mail-flow-rules-insight.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 70165bc6-7132-4a0e-bd3d-4a2479ce141d
---

# Fix slow mail flow rules insight in the new EAC in Exchange Online | Microsoft Learn

Inefficient mail flow rules (also known as transport rules) can lead to mail flow delays for your organization. This insight reports mail flow rules that have an impact on your organization's mail flow. Examples of these types of rules are:

- Conditions that use **Is member of** for large groups.
- Conditions that use complex regular expression (regex) pattern matching.
- Conditions that use content checking in attachments.

The **Fix slow mail flow rules** insight in the Insights dashboard in the new Exchange admin center (new EAC) will notify you when a mail flow rule is taking too long to complete. You can use this notification to help you to identify and fine-tune mail flow rules to help reduce mail flow delays.

![Fix slow mail flow rules insight in the Insights dashboard.](../../exchangeonline/media/mfi-fix-slow-mail-flow-rules-insight.png)

When you click **View details**, a flyout appears where you can review the rule by clicking **View rules**. You can also click **View sample messages** to see what kind of messages are impacted by the rule.

![Details flyout that appears after clicking View details in the Fix slow mail flow rules insight.](../../exchangeonline/media/mfi-fix-slow-mail-flow-rules-insight-details.png)

For more information about conditions and exceptions in mail flow rules in Exchange Online, see [Mail flow rule conditions and exceptions (predicates) in Exchange Online](../../security-and-compliance/mail-flow-rules/conditions-and-exceptions).