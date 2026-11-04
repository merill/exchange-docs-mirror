---
layout: Conceptual
title: Mailboxes exceeding receiving limits report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mailboxes-exceeding-receiving-limits-report
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
description: This article is about mailboxes that receive large volumes of messages.
ms.custom: 
ms.date: 2021-06-14T00:00:00.0000000Z
locale: en-us
document_id: 590bc214-190e-0282-66df-3a1d67c6b79e
document_version_independent_id: 1d984a92-27f5-6438-8b2d-e2e01cdd3ebe
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mailboxes-exceeding-receiving-limits-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mailboxes-exceeding-receiving-limits-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mailboxes-exceeding-receiving-limits-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 5d6d50a6-f0c8-da5f-8b9f-02443bae063f
---

# Mailboxes exceeding receiving limits report in the new EAC in Exchange Online | Microsoft Learn

In the new Exchange Center (EAC), the Mailboxes exceeding receiving limits report displays information on mailboxes that are receiving large volumes of messages in a short amount of time.

This report shows details on three categories of the Exchange Online receiving limit (see [Exchange Online limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#receiving-and-sending-limits)):

1. **Hot limit**: The general receiving limit. When a mailbox exceeds the overall receiving limit, they won't receive any mail from the Internet or on-premises senders until the limit resets.
2. **Sender-recipient pair limit**: The receiving limit per sender-recipient pair. When a mailbox exceeds the SRP limit, they won't receive any mail from that sender, if the sender is from the Internet or on-premises.
3. **Warm limit**: The logging-only limit that indicates when messages are 'At risk' of being blocked, set to 1000 messages per rolling hour. When a mailbox exceeds the warm limit, they aren't yet impacted but will be displayed in reporting for admin awareness.

Note

For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

There are two sections to this report:

1. A heatmap that indicates:

    1. When a mailbox exceeded their receiving limit and can no longer receive mail until the limit is reset, which occurs 1 hour after the threshold is exceeded.

        - **Hot limit**: Mailboxes won't receive any mail from the Internet or on-premises senders if the overall receiving limit is exceeded.
    2. When a mailbox is at risk, which means they've exceeded one or both of the below limits. This mailbox hasn't exceeded the receiving (Hot) limit yet but is receiving large volumes of messages regularly.

        - **Sender-recipient pair (SRP) limit**: Mailboxes won't receive any mail from a specific sender if the mailbox has received too many messages from the sender. High volumes from specific senders should be paid attention to, as they can put the mailbox at risk of exceeding the receiving (Hot) limit.
        - **Warm limit**: When a mailbox hasn't exceeded their limit yet but is receiving large volumes of messages regularly.
2. A table that shows, in the selected time window:

    - The date
    - The impacted mailbox
    - The limit type (Hot, SRP, or Warm) based on the user's filter selection
    - The number of hours a mailbox has exceeded the limit
    - The number of hours a mailbox is at risk
    - The limit value, based on limit type
    - The maximum number of messages they received per hour
    - The top sender

The report includes a filter on Limit type, allowing the user to display mailboxes that hit the Hot, SRP, or Warm limit separately.

Note

The default view is for the last 24 hours for all types. If no data is showing, that means you had no mailboxes exceeding the limit (or at risk) in the last 24 hours.

The chart is limited to showing the top 10 mailboxes. If you'd like to see more mailboxes, you'll have to filter/search differently.

![Report.](../../exchangeonline/media/new-report-mailboxes.jpg)

1. Use the **Limit type** filter to display mailboxes affected by the Hot, SRP, or Warm limit.
2. Click **Export** to download the data as a csv.
3. Select a mailbox address to view in detail the mailbox owner's contact information. Contact the mailbox owner to understand why they're receiving so much email, so they can reduce their mail volume and have a better experience.