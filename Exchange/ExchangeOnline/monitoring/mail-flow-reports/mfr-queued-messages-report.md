---
layout: Conceptual
title: Queued messages report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-queued-messages-report
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
description: Admins can learn how to use the Non-delivery details report in the new Exchange admin center to monitor outbound messages that were sent over connectors from your organization that have been delayed for over an hour.
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: 84d7fa44-6f08-0fcb-e08e-363866400af5
document_version_independent_id: a1665832-08e4-7981-2ca4-d971e7a7fbbb
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-queued-messages-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-queued-messages-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-queued-messages-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: cd422950-6819-ed9f-443f-737146cce8d3
---

# Queued messages report in the new EAC in Exchange Online | Microsoft Learn

When messages can't be sent from your organization to your on-premises or partner email servers using connectors, the messages are queued in Microsoft 365. Common examples that cause this condition are:

- The connector is incorrectly configured.
- There are networking or firewall changes in your on-premises environment.

Microsoft 365 continues to retry to delivery for 24 hours. After 24 hours, the messages will expire and will be returned to the senders in non-delivery reports (also known as bounce messages).

If the queued email volume exceeds the pre-defined threshold (the default value is 2000 messages), the information is available in the following locations:

- The **Queued messages report** report in the new Exchange admin center (new EAC). For more information, see the Queues section in this topic.

    For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).
- An alert is displayed on the **Alerts** page in the Microsoft Defender portal (https://security.microsoft.com &gt; **Incidents & alerts** &gt; **Alerts** or https://security.microsoft.com/alerts).
- Admins will receive an email notification based on the configuration of the default alert policy named **Messages have been delayed**. To configure the notification settings for this alert, see the next section.

    For more information about alert policies, see [Alert policies in the Microsoft Purview compliance portal](/en-us/purview/alert-policies).

## Customize queue alerts

1. In the Microsoft Defender portal (https://security.microsoft.com), go to **Incidents & alerts** &gt; **Alerts** &gt; **Alert policy** or go directly to https://security.microsoft.com/alertpolicies.
2. On the **Alert policies** page, find and select the policy named **Messages have been delayed** by clicking on the name. You can sort the policies by name or use the **Search** box.
3. In the **Message have been delayed** flyout that appears, you can turn the alert on or off and configure the notification settings.

    ![Messages have been delayed alert policy details the Microsoft Defender portal.](../../exchangeonline/media/mfr-queued-messages-alert-policy.png)

    - **Status**: You can toggle the alert on or off.
    - **Email recipients** and **Daily notification limit**: Click the **Edit** link or the **Edit policy** button to configure the settings as described in the next step.
4. In the **Edit policy** flyout that appears, configure the following settings:

    - **Send email notifications**: The default value is **On** (selected).
    - **Email recipients**: The default value is **TenantAdmins**.
    - **Daily notification limit**: The default value is **No limit**.
    - **Threshold**: The default value is 2000.

    ![Notification settings in the Messages have been delayed alert policy details.](../../exchangeonline/media/mfr-queued-messages-alert-policy-notification-settings.png)
5. When you're finished, click **Save** and **Close**.

## Queues

Even if the queued message volume doesn't exceeded the threshold and generated an alert, you can still use the **Queued messages report** in the new Exchange admin center to see messages that have been queued for more than one hour, and take action before the number of queued messages becomes too large.

![Queued messages report in the new EAC.](../../exchangeonline/media/mfr-queued-messages-report.png)

The same information and fix option is displayed after you click **View queue** in the details of a **Messages have been delayed** alert.