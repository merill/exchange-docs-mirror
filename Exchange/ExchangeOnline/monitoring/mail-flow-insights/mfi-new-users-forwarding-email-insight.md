---
layout: Conceptual
title: New users forwarding email insight in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-insights/mfi-new-users-forwarding-email-insight
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
description: Admins can learn how to use the New users forwarding email insight in the new Exchange admin center to investigate when users in their organization are forwarding messages to new domains.
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: 7da39fe6-ea2e-c78e-24a9-2783987dbe34
document_version_independent_id: 6ab292ea-d1d3-1d46-ef20-043484031cdb
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-insights/mfi-new-users-forwarding-email-insight.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-insights/mfi-new-users-forwarding-email-insight
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-insights/mfi-new-users-forwarding-email-insight.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: be277c97-c886-f6b9-774d-dccf0bd71067
---

# New users forwarding email insight in the new EAC in Exchange Online | Microsoft Learn

It's suspicious when new user accounts in your organization suddenly start forwarding email messages to external domains.

The **New users fowarding email** insight in the Insights dashboard in the new Exchange admin center (new EAC) notifies you when new users accounts in your organization are forwarding messages to external domains.

![New domains being forwarded email insight in the Insights dashboard.](../../exchangeonline/media/mfi-new-users-forwarding-email-insight.png)

When you click **View details**, a flyout appears where you can find more details about the forwarded messages, including a link to the [Auto forwarded messages report](../mail-flow-reports/mfr-auto-forwarded-messages-report) for more information.

![Details flyout that appears after clicking View details in the New domains being forwarded email insight.](../../exchangeonline/media/mfi-new-users-forwarding-email-insight-details.png)

If you suspect the accounts have been compromised, see [Responding to a compromised email account](/en-us/defender-office-365/responding-to-a-compromised-email-account).