---
layout: Conceptual
title: Fix possible mail loop insight in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-insights/mfi-fix-possible-mail-loop-insight
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
description: Admins can learn how to use the Fix possible mail loop insight in the new Exchange admin center to identify and fix mail loops in their organization.
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: 386ea0c7-3f6e-a26d-df37-2ffa12135cca
document_version_independent_id: 2444dad4-91b5-29e8-9c6d-12d87b303f3f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-insights/mfi-fix-possible-mail-loop-insight.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-insights/mfi-fix-possible-mail-loop-insight
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-insights/mfi-fix-possible-mail-loop-insight.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0850fefd-e402-4507-ae98-46cfdfc2e16c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6ecf98a5-97c7-4249-b209-a9d9e42633a0
platformId: 6d0636ef-7728-b89c-e69b-e6818afb2d2d
---

# Fix possible mail loop insight in the new EAC in Exchange Online | Microsoft Learn

A mail loop is bad because it wastes system resources, consumes your organization's mail volume quota, and sends confusing non-delivery reports (also known as NDRs or bounce messages) to the original senders.

The **Fix possible mail loop** insight in the Insights dashboard in the new Exchange admin center (new EAC) reports when a mail loop is detected in your organization, the email domains that are involved in the loop, and the number of messages from the previous day that were in the loop.

![Fix possible mail loop insight in the Insights dashboard.](../../exchangeonline/media/mfi-fix-possible-mail-loop-insight.png)

You can click **View details** to see the details in a flyout where we identify the most common mail loop scenarios and provide the recommended actions (if available) to fix the loop.

![Details flyout that appears after clicking View details in the Fix possible mail loop insight.](../../exchangeonline/media/mfi-fix-possible-mail-loop-insight-details.png)