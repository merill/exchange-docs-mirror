---
layout: Conceptual
title: Dynamic Distribution Groups report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-dynamic-distribution-groups-report
Manager: dansimp
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
author: v-mathavale
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
ms.custom: 
description: Admins can learn how to use the Dynamic Distribution Groups report in the new Exchange admin center to get insight into the usage of dynamic distribution groups for their organization.
ms.date: 2023-02-22T00:00:00.0000000Z
locale: en-us
document_id: 7963eeec-e435-57a9-6680-39fa6f246615
document_version_independent_id: 40733c25-a6f1-7b11-09f2-ac5f39b1d0cc
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-dynamic-distribution-groups-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-dynamic-distribution-groups-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-dynamic-distribution-groups-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 8a195e74-1e07-682d-bed7-97d4ae747df7
---

# Dynamic Distribution Groups report in the new EAC in Exchange Online | Microsoft Learn

The Dynamic Distribution Groups report in the new Exchange admin center provides insight into the usage of dynamic distribution groups for your organization. You can find this report at **Reports** &gt; **Mail Flow** in the new EAC.

Note

By default, the report shows data for the last 30 days. If the report is empty, try changing the date range.

For permissions that are required to use this report, see [**Permissions required to view mail flow reports**](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

By default, the report shows data for "Used" Dynamic Distribution Groups. If the report is empty, try changing the filter to show "All" or "Unused" Dynamic Distribution Groups.

The table lists the dynamic distribution groups and the number of times it was used based on the date filter and the filter that allows you to select **All**, **Used**, or **Unused**. If you select **All**, it lists all dynamic distribution groups whether it was used or unused based on the date filter. If you select **Used**, it lists only the dynamic distribution groups that were used based on the date filter. If you select **Unused**, it lists only the dynamic distribution groups that were unused based on the date filter.

[![Screenshot of dynamic distribution group report.](../../exchangeonline/media/dynamic-distribution-group-report-2.jpg)](../../exchangeonline/media/dynamic-distribution-group-report-2.jpg#lightbox)

The dynamic distribution group report details section shows the following information about each dynamic distribution group:

- Group Name
- Group Email
- Last used on (date)
- Number of times used

To quickly filter the results, click **Search**![](../../exchangeonline/media/modern-eac-search-icon.png) and start typing a value.

To filter the results by date range, use the date filter. You can specify a date range up to 90 days.

For more advanced filters that you can save and use later, click **Filter**![](../../exchangeonline/media/modern-eac-filter-icon.png) and select **New filter**. In the **Custom filter** flyout that appears, enter the following information:

- **Name your filter**: Enter a unique name.
- Click **Add new clause**. A clause contains the following elements that you need to enter:
    - **Field**: Select **Group Name**, **Group Email**, **Last Used on**, or **Number of Times Used**.
    - **Operator**: Select **starts with** or **is**.
    - **Value**: Enter the value you want to search for.

You can click **Add new clause** as many times as you need. Multiple clauses use AND logic (&lt;Clause1&gt; AND &lt;Clause2&gt;...).

To remove a clause, click **Remove**![](../../exchangeonline/media/modern-eac-remove-icon.png) .

When you're finished, click **Save**. The new filter is automatically loaded and the results are changed based on the filter. This gives the same result as clicking **Filter** and selecting the customer filter from the list.

To unload an existing filter (return to the default list), click **Filter**![](../../exchangeonline/media/modern-eac-filter-active-icon.png) and select **Clear all filters**.

Click **Export** to export the displayed results to a .csv file.