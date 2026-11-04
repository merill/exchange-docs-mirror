---
layout: Conceptual
title: New domains being forwarded email insight in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-insights/mfi-new-domains-being-forwarded-email-insight
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
description: Admins can learn how to use the New domains being forwarded email insight in the new Exchange admin center to investigate when users in their organization are forwarding messages to external domains that have never been been forwarded to.
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: 383a4149-1cae-99d4-73f7-f70bacafbf29
document_version_independent_id: 4f3d5f39-f536-ed9c-9e47-fd890fd1471c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-insights/mfi-new-domains-being-forwarded-email-insight.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-insights/mfi-new-domains-being-forwarded-email-insight
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-insights/mfi-new-domains-being-forwarded-email-insight.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 43997d33-25b0-48da-c6e1-69514c783253
---

# New domains being forwarded email insight in the new EAC in Exchange Online | Microsoft Learn

Although you might have valid business reasons to forward email messages to external recipients in specific domains, it's suspicious when users in your organization suddenly start forwarding messages to external domains, and no one in the organization has ever forwarded messages to those domains (new domains).

The **New domains being forwarded email** insight in the Insights dashboard in the new Exchange admin center (new EAC) notifies you when users in your organization are forwarding messages to new domains.

![New domains being forwarded email insight in the Insights dashboard.](../../exchangeonline/media/mfi-new-domains-being-forwarded-email-insight.png)

When you click **View details**, a flyout appears where you can find more details about the forwarded messages, including a link to the [Auto forwarded messages report](../mail-flow-reports/mfr-auto-forwarded-messages-report) for more information.

![Details flyout that appears after clicking View details in the New domains being forwarded email insight.](../../exchangeonline/media/mfi-new-domains-being-forwarded-email-insight-details.png)

To prevent automatic message forwarding to external domains, configure a remote domain for some or all external domains. For more information, see [Manage remote domains in Exchange Online](../../mail-flow-best-practices/remote-domains/manage-remote-domains).

If you suspect the accounts have been compromised, see [Responding to a compromised email account](/en-us/defender-office-365/responding-to-a-compromised-email-account).