---
layout: Conceptual
title: Email issues for priority accounts report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-email-issues-for-priority-accounts-report
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
ms.custom: 
description: Admins can learn how to use the Email issues for priority accounts monitoring in the new Exchange admin center to see delayed and failed email messages that were sent to or from priority accounts.
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: 4bd4f3b5-d4cb-f815-56a5-3d0b62d5c904
document_version_independent_id: a5a5c668-6c55-c792-9b38-773dbeaccc7d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-email-issues-for-priority-accounts-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-email-issues-for-priority-accounts-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-email-issues-for-priority-accounts-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 3c6d2ccb-3f4f-1338-dc34-1a000224768a
---

# Email issues for priority accounts report in the new EAC in Exchange Online | Microsoft Learn

Note

The priority accounts report that's described in this topic is available only to organizations that meet both of the following requirements:

- At least 5,000 licenses for one or more of the following products: Office 365 E3, Microsoft 365 E3, Office 365 E5, or Microsoft 365 E5. For example, 3,000 Office 365 E3 licenses and 2,500 Microsoft 365 E5 licenses.
- Your organization needs to have at least 50 monthly active users for one or more core workloads – Teams, One Drive for Business, SharePoint Online, Exchange Online and Office apps

For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

The **Email issues for priority accounts** report in the new Exchange admin center (new EAC) allows Exchange admins and global admins^\*^ to view failed events from the last 15 minutes and delayed email messages from last 6 hours that were sent to or sent from priority accounts. If no issues are found, the report will be empty. Users can configure to receive email notifications for failed and delayed messages which will provide information at the time alert is fired.

Important

^\*^ Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

Priority users are people in your Microsoft 365 organization who have a high business impact, like your CEO, executives, or other users who have access to sensitive or high priority information. For more information about priority accounts, see [Manage and monitor priority account](/en-us/microsoft-365/admin/setup/priority-accounts). For more reporting for priority accounts, see [Exchange Online monitoring for Microsoft 365](/en-us/microsoft-365/enterprise/microsoft-365-exchange-monitoring).

The **Unhealthy email status** section shows the following information about messages where a priority user is a sender or a recipient:

- **Date**
- **Sender**
- **Recipient**
- **Subject**
- **Status**: The value is **Failed** or **Delayed**.

To quickly filter the results by recipient, click **Search**![Search icon.](../../exchangeonline/media/modern-eac-search-icon.png) and start typing the recipient's email address.

For more advanced filters that you can also save and use later, click **Filter**![Filter icon.](../../exchangeonline/media/modern-eac-filter-icon.png) and select **New filter**. In the **Custom filter** flyout that appears, enter the following information:

- **Name your filter**: Enter a unique name.
- Click **Add new clause**. A clause contains the following elements that you need to enter:

    - **Field**: Select **Date**, **Sender**, **Recipient**, **Subject** or **Status**.
    - **Operator**: Select **starts with** or **is**.
    - **Value**: Enter the value you want to search for.

    You can click **Add new clause** as many times as you need. Multiple clauses use AND logic (&lt;Clause1&gt; AND &lt;Clause2&gt;...).

    To remove a clause, click **Remove**![Remove icon.](../../exchangeonline/media/modern-eac-remove-icon.png)

    When you're finished, click **Save**. The new filter is automatically loaded, and the results are changed based on the filter. This is the same result as clicking **Filter** and selecting the custom filter from the list.

    To unload a existing filter (return to the default list), click **Filter**![Active filter icon.](../../exchangeonline/media/modern-eac-filter-active-icon.png) and select **Clear all filters**.

Select an entry in the list to be taken to the [message trace](../trace-an-email-message/message-trace-modern-eac) search results for the message. Select the message trace entry to view details about the message and what happened to it.

![Message trace detail in message trace in the new EAC.](../../exchangeonline/media/mfr-priority-users-message-trace-detail.png)

Note

For the following procedures, you need to be a Security Reader to see the alerts, and a Security Administrator to edit the policy.

Click **Export** to export the displayed results to a .csv file.

Click **Manage priority accounts** to add or remove users from the priority accounts list.

Click **Edit policy** to configure email notifications related to priority accounts:

- **Send email notification**: Select or clear this checkbox.
- **Send email notifications to these users or groups**: Click in the box to find or enter a user or group to receive email notifications.
- **Daily notification limit**: Select from the following values: **No limit**, 1 (default), 5, 10, 25, 50, 150, or 200.
- **Threshold**: An email notification is sent when the number of failed or delayed email messages for priority accounts exceeds the specified value. The default value is 100.

You can see alerts for delayed and failed messages under **View Alerts**. Selecting the alert will provide details about the messages that were delayed or failed at the time alert is fired.

When you're finished, click **Save**.