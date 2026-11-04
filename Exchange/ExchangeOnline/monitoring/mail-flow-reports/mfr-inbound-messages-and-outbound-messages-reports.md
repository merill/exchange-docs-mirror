---
layout: Conceptual
title: Inbound messages and Outbound messages reports in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-inbound-messages-and-outbound-messages-reports
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
description: Admins can learn how to use the Inbound messages report and the Outbound Messages report in the new Exchange admin center to monitor message volume and TLS encryption for messages to and from the internet and inbound and outbound messages over connectors.
ms.date: 2020-11-19T00:00:00.0000000Z
locale: en-us
document_id: 1b71f3c0-0139-18c1-7bf1-308c460083ae
document_version_independent_id: 93e8f0ab-8968-ecd7-1b57-ad162504492c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-inbound-messages-and-outbound-messages-reports.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-inbound-messages-and-outbound-messages-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-inbound-messages-and-outbound-messages-reports.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 763821e7-0f1c-897c-6879-159031e5dc2b
---

# Inbound messages and Outbound messages reports in the new EAC in Exchange Online | Microsoft Learn

The **Inbound messages report** and the **Outbound messages report** in the new Exchange admin center (new EAC) display information about email entering and leaving your organization. Specifically, the **Inbound messages report** shows information about email coming into your organization from the internet and over connectors. The **Outbound messages report** displays information about email leaving your organization to the internet and over connectors. Both reports also show the TLS encryption level that's being used.

Note

By default, the report shows data for the last 7 days. If the report is empty, try changing the date range.

For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

The overview section contains the following charts:

- **Message volume**: Shows the number of inbound or outbound messages to or from the internet and over connectors.
- **Messages by TLS used**: Shows the TLS encryption level. If you hover over a specific color in the chart, you'll see the number of messages for that specific version of TLS.

![Overview of the Auto forwarded messages report.](../../exchangeonline/media/mfr-inbound-message-report.png)

The **Connector report details** section shows the following information about each specific connector or email from the internet:

- **Date**
- **Connector direction and name**
- **Connector type**
- **Forced TLS?**
- **No TLS**
- **TLS 1.0**
- **TLS 1.1**
- **TLS 1.2**
- **Volume**

To quickly filter the results, click **Search**![Search icon.](../../exchangeonline/media/modern-eac-search-icon.png) and start typing a value.

To filter the results by date range or connector name, use the boxes. You can specify a date range up to 90 days.

For more advanced filters that you can also save and use later, click **Filter**![Filter icon.](../../exchangeonline/media/modern-eac-filter-icon.png) and select **New filter**. In the **Custom filter** flyout that appears, enter the following information:

- **Name your filter**: Enter a unique name.
- Click **Add new clause**. A clause contains the following elements that you need to enter:

    - **Field**: Select **Date**, **Connector direction**, **Connector type**, **Forced TLS**, **No TLS**, **TLS 1.0**, **TLS 1.1**, **TLS 1.2**, or **Volume**.
    - **Operator**: Select **starts with** or **is**.
    - **Value**: Enter the value you want to search for.

    You can click **Add new clause** as many times as you need. Multiple clauses use AND logic (&lt;Clause1&gt; AND &lt;Clause2&gt;...).

    To remove a clause, click **Remove**![Remove icon.](../../exchangeonline/media/modern-eac-remove-icon.png)

    When you're finished, click **Save**. The new filter is automatically loaded, and the results are changed based on the filter. This is the same result as clicking **Filter** and selecting the custom filter from the list.

    To unload an existing filter (return to the default list), click **Filter**![Active filter icon.](../../exchangeonline/media/modern-eac-filter-active-icon.png) and select **Clear all filters**.

Click **Export** to export the displayed results to a .csv file.

## Exceptions where messages will not be included in these reports

Cross-tenant scenarios where messages are sent from one Microsoft 365 tenant (including consumer organizations) directly to another Microsoft 365 tenant will not be included in the report.