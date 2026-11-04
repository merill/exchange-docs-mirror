---
layout: Conceptual
title: Exchange transport rule report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-exchange-transport-rule-report
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
description: Admins can learn how to use the Exchange transport rule report to view information about mail flow rules (also known as transport rules).
ms.date: 2021-12-15T00:00:00.0000000Z
locale: en-us
document_id: 4415d972-e123-6bf0-bfbc-3c555dc9bf51
document_version_independent_id: 3a79fad5-4ac5-9263-2ac8-8607a6f7ddf3
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-exchange-transport-rule-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-exchange-transport-rule-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-exchange-transport-rule-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: b8832a4c-bc7f-f749-9473-56d125be2922
---

# Exchange transport rule report in the new EAC in Exchange Online | Microsoft Learn

The **Exchange transport rule** report in the new Exchange admin center (new EAC) displays information on messages that were affected by mail flow rules (also known as transport rules).

Note

By default, the report shows data for the last 7 days. If the report is empty, try changing the date range. It could take up to 24 hours to reflect the Transport Rule data in the Transport Rule report. For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

To view the report in the new EAC at https://admin.exchange.microsoft.com, go to **Reports** &gt; **Mail flow** &gt; and then select **Exchange transport rule report** on the **Mail flow reports** page. To go directly to the report, open https://admin.exchange.microsoft.com/#/reports/transportruledetails.

![Overview of the Exchange transport rule report.](../../exchangeonline/media/mfr-exchange-transport-rule-report.png)

By default, **Chart breakdown by Severity** is selected, and the follow charts are shown:

- A line graph that shows the number of inbound and outbound messages per day that were affected by mail flow rules.^\*^
- **Message volume by direction**: A doughnut graph that shows the total number of messages and portion of **Outbound** and **Inbound** messages that were affected by mail flow rules.\*^\*\*^
- **Message volume by severity** A doughnut graph that shows the total number of messages and portion of messages that were affected by **High severity**, **Medium severity**, and **Low severity** mail flow rules.^\*\*^

^\*^ If you hover over the line on the chart for a specific day, you'll see the number of messages for that day.

^\*\*^ If you hover over a specific color in the chart, you'll see the total number of messages in the category for the entire time period.

If you change the chart view to **Chart breakdown by severity**, the line graph changes to show the number of messages that were affected by **High severity**, **Medium severity**, and **Low severity** mail flow rules.

By default, **Show data for all transport rules** is selected, but if you click on that value, you can select a specific mail flow rule to show data for.

The following information is shown in the details table below the graph:

- **Date**
- **Transport rule**
- **Subject**
- **Sender address**
- **Recipient address**
- **Severity**
- **Direction**

You can sort the information in the details table by clicking on a column header.

To quickly filter the results by **Transport rule** or **Subject**, click **Search**![Search icon.](../../exchangeonline/media/modern-eac-search-icon.png) and start typing a value.

To filter the results, use the boxes. The following filters are available:

- Date: **7 days** is selected by default, but you can select **30 days**, **90 days** or a **Custom start date** that's less than 90 days.
- Direction: **Outbound, Inbound** is selected by default, but you can select either value by itself.
- Severity: **High severity, Medium severity, Low severity** are selected by default, but you can select one or more severity values.

Click **Export** to export the displayed results to a .csv file.