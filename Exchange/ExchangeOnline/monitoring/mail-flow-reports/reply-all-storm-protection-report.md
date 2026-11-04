---
layout: Conceptual
title: Reply-all storm protection report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/reply-all-storm-protection-report
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
author: Benny-54
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
description: Admins can learn how to use the Reply-all storm protection report in the new Exchange admin center to identify and troubleshoot mail flow in your email domains.
ms.date: 2022-02-24T00:00:00.0000000Z
locale: en-us
document_id: bff78b83-f707-3b06-9c52-3eeff269ab0c
document_version_independent_id: c8693d47-49c8-0fe0-ff66-52921f006281
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/reply-all-storm-protection-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/reply-all-storm-protection-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/reply-all-storm-protection-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: ed67f405-8640-ad02-37dd-b3bab91fe563
---

# Reply-all storm protection report in the new EAC in Exchange Online | Microsoft Learn

The Reply-all storm protection report in the new Exchange admin center (new EAC), **Reports** &gt; **Mail flow** section displays information about detected reply-all storms in your organization and the reply-all messages that were blocked.

Note

For more information on permissions that are required to use this report, see [Permissions required to view mail flow reports](/en-us/exchange/monitoring/mail-flow-reports/mail-flow-reports#permissions-required-to-view-mail-flow-reports).

![Reply-all storm protection report1](../../exchangeonline/media/storm-protect-1.png)

The top of the report shows the current settings used by Reply-all Storm Protection for detecting and blocking reply-all messages during a reply-all storm.

- Status
- Minimum recipients
- Minimum reply-alls
- Block duration hours

To view the current feature settings here on the report, you must have read access to Transport configuration information (Get-TransportConfig) via the View-Only Configuration or Organization Transport Settings roles. Both the Organization Management and View-Only Organization Management role groups include both of these roles. For more information, see [View-only Organization Management](/en-us/exchange/view-only-organization-management-exchange-2013-help#:%7E:text=The%20View-Only%20Organization%20Management%20management%20role%20group%20is%2crequired%20to%20perform%20a%20given%20set%20of%20tasks).

Note that the current settings shown might not be the same as the settings that were used for past reply-all storms if they were previously changed. Changing the settings while a storm is happening might not apply those settings in time to affect the current storm, but it will apply to future storms.

Beneath the current settings is the time/date range drop-down from which you can select to view from 3 hours to 30 days of data (with the last 3 hours as the default). All times shown are based on your local time.

The overview section shows these two charts:

- **Detected reply-all storm messages**
- **Messages blocked**

The **Detected reply-all storm messages** chart shows the number of reply-all messages that were sent during the preceding time-interval for detected reply-all storms. For example, in the chart above the five reply-all messages for the "Happy Thanksgiving" storm shown at 3pm were detected between 2:45 and 3pm. While reply-all messages sent before a reply-all storm is detected won't get blocked, they're included in the **Detected reply-all storm messages** chart values, as are the messages that were blocked.

Note

This chart displays data only for declared reply-all storms where at least one reply-all message has been blocked. It can't be used to track potential storms before they're declared a reply-all storm.

The **Messages blocked** chart includes a subset of the messages shown in the **Detected reply-all storm messages** chart. It shows the number of reply-all messages blocked during the *Blocked duration hours* time frame.

Selecting any one of the reply-all storm names in either chart will pop up a side panel showing specific details about the selected reply-all storm, as shown below.

![Reply-all report](../../exchangeonline/media/storm-protect-2.png)

The reply-all storm details panel includes the following information about the storm:

| Item | Description |
| --- | --- |
| **Subject** | The message subject of the initial message. |
| **Original Sender** | The sender of the first message in the conversation thread. |
| **Start Date/Time** | When the first reply-all message was sent. |
| **Total Messages** | The total number of messages in the conversation thread (includes the first message). |
| **Blocked Messages** | The total number of reply-all storm messages blocked by the feature. This is always lower than the total number of messages in the thread. In some cases it might be lower than you'd expect based on the feature's Minimum reply-alls setting. It can take up to a few minutes to synchronize the block enforcement notification to all relevant servers in the service. During that time, a few reply-alls could still get through before blocking kicks-in. |
| **Block Start Time** | Time when message blocking started. |
| **Message ID** | The Message ID of the first message in the conversation thread. Clicking on this link will open Message Trace in a new tab and run a query for this message. |
| **Reply-all senders** | Users who sent (or tried to send) a reply-all to the thread. Includes whether or not the message they sent was allowed through or blocked. |

The final section of the main report page, **Reply-all storm details**, shows a table of all the reply-all storms shown in the charts for the selected time range. It also includes the key details about each of the following:

- **Start Date/Time**
- **End Date/Time**
- **Subject**
- **Original Sender**
- **Total Messages**
- **Blocked Messages**
- **Message ID**

Click **Export** to export the displayed results to a .csv file.