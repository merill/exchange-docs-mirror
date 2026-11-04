---
layout: Conceptual
title: Domain expiring soon insight in the new Exchange admin center (new EAC) in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-insights/domain-expiry-notification-feature
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
ms.author: serdars
author: Benny-54
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
description: This notification feature monitors the accepted domains per organization and sends email notification to the admin when any accepted domains approach expiry.
ms.custom: 
ms.date: 2020-12-09T00:00:00.0000000Z
locale: en-us
document_id: fbf752d0-1e4b-1a22-027b-80f10a7cb3c7
document_version_independent_id: 915657cc-62cb-d670-d211-f50632f38a90
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-insights/domain-expiry-notification-feature.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-insights/domain-expiry-notification-feature
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-insights/domain-expiry-notification-feature.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 3e0f17ae-f34d-e4ff-1719-a9e5290304b6
---

# Domain expiring soon insight in the new Exchange admin center (new EAC) in Exchange Online | Microsoft Learn

Adding a domain to Microsoft 365 or Office 365 means the domain is an *accepted domain*. You can configure users in the organization to send and receive email using an accepted domain. To keep mail flow health, domains owned by customers must be active. Once domains expire, users configured under that domain no longer receive email.

The **Domain expiring soon** insight in the **Insights** dashboard in the new Exchange admin center (new EAC) reports the domains that are about to expire and the required actions to take.

![Domain expiring soon.](../../exchangeonline/media/domain-expiry-soon.png)

Select **View details** to see the identified domains that are about to expire.

![DES-details.](../../exchangeonline/media/domain-expiry_details.png)

If a domain is expiring within 90 days, 60 days, or 30 days and less, it triggers an alert. A single alert could have multiple domains. For example, the alert might contain one domain expiring in 90 days and another domain expiring in 60 days. These alerts are sent as email notifications to your registered email IDs.

These notifications list the domains that are expiring and require action to avoid disruption in your mail flow. You can ignore the notifications if you already renewed or deleted the domain.

You can also view these alerts in [new EAC](https://admin.exchange.microsoft.com), go to **Mail flow** &gt; **View alerts**.

## Related article

[Mail flow insights in the modern Exchange admin center](mail-flow-insights)