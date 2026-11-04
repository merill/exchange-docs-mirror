---
layout: Conceptual
title: Monitoring, reporting, and message tracing in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/monitoring
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Exchange Online offers many different reports that can help you determine the overall status and health of your organization. There are also tools to help you troubleshoot specific events (such as a message not arriving to its intended recipients), and auditing reports to aid with compliance requirements. The following table describes the reports and troubleshooting tools that are available to Exchange Online administrators.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 87bdeeae-bd80-4a3b-95c5-62fbaf97c2e8
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 206471ee-963a-333f-6941-415a443b273c
document_version_independent_id: c0cd8f8a-5cdd-24f3-eace-3cb0930d65b5
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/monitoring.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: ce33fdff-a9f2-17fd-d282-8b14049dedf6
---

# Monitoring, reporting, and message tracing in Exchange Online | Microsoft Learn

Exchange Online offers many different reports that can help you determine the overall status and health of your organization. There are also tools to help you troubleshoot specific events (such as a message not arriving to its intended recipients), and auditing reports to aid with compliance requirements. The following table describes the reports and troubleshooting tools that are available to Exchange Online administrators.

| Feature | Reports | Location |
| --- | --- | --- |
| **Reports in the Microsoft 365 admin center** | [Email activity](/en-us/microsoft-365/admin/activity-reports/email-activity)[Email app usage](/en-us/microsoft-365/admin/activity-reports/email-apps-usage)[Mailbox usage](/en-us/microsoft-365/admin/activity-reports/mailbox-usage)[Microsoft 365 Groups activity](/en-us/microsoft-365/admin/activity-reports/office-365-groups) | In the [Microsoft 365 admin center](https://portal.office.com/adminportal/home), go to **Show all** (if necessary), click **Reports** &gt; **Usage**, and then select one of the reports on the page:<br>- **Email activity**<br>- **Active users - Microsoft 365 services** &gt; **View more**:<br>    - **Exchange**:<br>        - **Email activity**<br>        - **Email app usage**<br>        - **Mailbox usage**<br>    - **Office 365**:<br>        - **Groups activity** |
| **Reports in the Microsoft Purview compliance portal** | [DLP reports](/en-us/purview/dlp-learn-about-dlp#dlp-activity-explorer-and-reports)¹ | In the Microsoft Purview compliance portal (https://security.microsoft.com), go to **Reports**, and then select one of the available reports on the page. To go directly to the **Reports** page, use https://compliance.microsoft.com/reports. |
| **Reports in the Microsoft Defender portal** | [View Defender for Office 365 reports](/en-us/defender-office-365/reports-defender-for-office-365)² [View email security reports](/en-us/defender-office-365/reports-email-security) | In the Microsoft Defender portal (https://security.microsoft.com), go to **Reports** &gt; **Email & collaboration** &gt; **Email & collaboration reports**, and then select one of the available reports on the page. To go directly to the **Reports** page, use https://security.microsoft.com/emailandcollabreport. |
| **Reports using Microsoft Graph** | Programmatically create the reports that are available in the Microsoft 365 admin center by using Microsoft Graph. For more information, see the following topics: [Email activity reports](/en-us/microsoft-365/admin/activity-reports/email-activity-ww)[Email app usage reports](/en-us/microsoft-365/admin/activity-reports/email-apps-usage-ww)[Mailbox usage reports](/en-us/microsoft-365/admin/activity-reports/mailbox-usage)[Microsoft 365 groups activity reports](/en-us/microsoft-365/admin/activity-reports/office-365-groups-ww) | n/a |
| **Reports using reporting web services** | Programmatically create reports from the available Exchange Online PowerShell reporting cmdlets by using REST/ODATA2 query filtering.³  For more information, see [Reporting Web Services](/en-us/previous-versions/office/developer/o365-enterprise-developers/jj984325%28v=office.15%29). | https://reports.office365.com/ecp/reportingwebservice/reporting.svc |
| **Message trace** | [Message trace in the modern Exchange admin center](trace-an-email-message/message-trace-modern-eac) | In the Exchange admin center (https://admin.exchange.microsoft.com), go to **Mail flow** &gt; **Message trace**. **Note**: The **Exchange message trace** link in the Microsoft Defender portal opens message trace in the modern EAC. |
| **Audit logging** | [Search the audit log in the Microsoft Purview compliance portal](/en-us/purview/audit-search) | In the Microsoft Purview compliance portal (https://compliance.microsoft.com), go to **Solutions** &gt; **Audit** &gt; **Search** tab on the **Audit** page. |

¹ DLP is only available in certain Exchange Online subscription plans. For information, see the **Data Loss Prevention** entries in the [Exchange Online Service Description](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description).

² Defender for Office 365 is available in Office 365 Enterprise E5, but you can also purchase Defender for Office 365 as an add-on to other subscription plans. For more information, see the [Microsoft Defender for Office 365 Service Description](/en-us/office365/servicedescriptions/office-365-advanced-threat-protection-service-description).

³ Many of the original reporting cmdlets in Exchange Online PowerShell have been deprecated (the cmdlets are available, but they don't return useful data). For a list of available and unavailable reporting cmdlets, see [Exchange reporting cmdlets](/en-us/powershell/module/exchangepowershell/#reporting).

## Reporting and message trace data availability and latency

The following table describes when Exchange Online reporting and message trace data is available and for how long.

| Report type | Data available for (look back period) | Latency |
| --- | --- | --- |
| Mailbox summary reports | 60 days | Message data aggregation is mostly complete within 24-48 hours. Some minor incremental aggregated changes may occur for up to 5 days. |
| Mail protection summary reports | 90 days | Message data aggregation is mostly complete within 24-48 hours. Some minor incremental aggregated changes may occur for up to 5 days. |
| Mail protection detail reports | 90 days | For detail data that's less than 7 days old, data should appear within 24 hours but may not be complete until 48 hours. Some minor incremental changes may occur for up to 5 days.  To view detail reports for messages that are greater than 7 days old, results may take up to a few hours. |
| Message trace data | 90 days | When you run a message trace for messages that are less than 7 days old, the messages should appear within 5-30 minutes.  When you run a message trace for messages that are greater than 7 days old, results may take up to a few hours. |

Note

Data availability and latency doesn't depend on the user interface (it's the same in the admin centers as in PowerShell).