---
layout: Conceptual
title: Mailboxes exceeding receiving limits insight in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-insights/mailboxes-exceeding-receiving-limits-insights
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
description: This article describes the delays due to mailboxes exceeding their limits.
ms.custom: 
ms.date: 2021-06-14T00:00:00.0000000Z
locale: en-us
document_id: 48a81eee-a58e-f972-0fb1-35433eb09690
document_version_independent_id: f74c8f79-fc1d-6b90-7be4-3474e705f61f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-insights/mailboxes-exceeding-receiving-limits-insights.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-insights/mailboxes-exceeding-receiving-limits-insights
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-insights/mailboxes-exceeding-receiving-limits-insights.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: d2b782bc-aeeb-2b90-a46c-b88964eec68d
---

# Mailboxes exceeding receiving limits insight in the new EAC in Exchange Online | Microsoft Learn

Mailboxes that receive large volumes of messages in a short amount of time can lead to mail flow delays for those mailboxes, and other mailboxes in your organization. The mailboxes exceeding receiving limits insight in the Insights dashboard in the new Exchange admin center (new EAC) highlights:

1. Mailboxes that have exceeded their receiving limit (For more information, see [Exchange Online limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#receiving-and-sending-limits)), which means they can no longer receive mail until the limit is reset (which is 1 hour after the threshold is exceeded).

    - Mailboxes won't receive any mail at all if the overall receiving limit is exceeded.
    - Mailboxes won't receive any mail from a specific sender, if the mailbox has received too many messages from the sender.
2. Mailboxes that are at risk. They haven't exceeded their limit but are receiving large volumes of messages regularly.

The insight will only appear if:

1. Mailboxes have exceeded their receiving limit in the past 24 hours.
2. A mailbox has become newly warm in the past 24 hours.
3. A mailbox has been warm for &gt;12 hours of the past 24 hours.

The insight will appear in the dashboard:

![Insight.](../../exchangeonline/media/mailbox-exceeding-insight.png)

When you click on **View details**, the following flyout will appear:

![Detailed insight.](../../exchangeonline/media/mailboxes-exceeding-limit-insight.png)

1. Select **Learn more about receiving limits** to view documentation about Exchange's limits.
2. Select **receiving limits report** to view a detailed report that shows up to seven days of data. Each section shows at least 20 mailboxes – if there are more, you may view them in the report.
3. Mailboxes that appear in the **Mailboxes exceeded the receiving limit** section are mailboxes that have exceeded their receiving limit in the past 24 hours (includes overall receiving limit, and single sender sending too much email).
4. Mailboxes that appear in the **Mailboxes at risk now** section are mailboxes that have newly started receiving large volumes of mail.
5. Mailboxes that appear in the **Mailboxes repeatedly at risk** section are mailboxes that have received large volumes of mail for &gt; 12 hours of the past 24 hours.
6. Select the email address of the mailbox to view the contact information of the owner of the mailbox. Contact the mailbox owner to understand why their receiving so much email, so they can reduce their mail volume and have a better experience.