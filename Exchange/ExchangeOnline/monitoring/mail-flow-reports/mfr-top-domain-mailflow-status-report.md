---
layout: Conceptual
title: Top domain mailflow status report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-top-domain-mailflow-status-report
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
description: Admins can learn about the Top domain mailflow status report in the new Exchange admin center to identify and troubleshoot mail flow in email domains.
ms.date: 2026-04-16T00:00:00.0000000Z
locale: en-us
document_id: 26b1cdc2-dd20-670f-2f1e-011c03f271c8
document_version_independent_id: 9190f9e6-7ccf-1054-879c-16ac9fdd2b80
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-top-domain-mailflow-status-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-top-domain-mailflow-status-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-top-domain-mailflow-status-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 5d0e6097-4100-34aa-13e8-45c43568a84f
---

# Top domain mailflow status report in the new EAC in Exchange Online | Microsoft Learn

Note

This report will be deprecated. For more information, see in Message Center post [MC1272554](https://admin.cloud.microsoft/?#/MessageCenter/:/messages/MC1272554).

The Top domain mailflow status report in the new Exchange Admin Center (EAC) contains two tabs providing insight into your inbound and outbound mail flow status for your organization. You can find this report at **Reports &gt; Mail Flow** in the new EAC.

- On the **Inbound** page, you can find information on whether your email domains are receiving external messages or not. Typically, these types of issues are related to MX record problems or an expired domain.
- On the **Outbound** page, the report gives you insights into your outbound mail flow, for example, which outbound pools are used to send mail out of your organization.

Note

The **Outbound** page-based report provides information about only specific domains that fulfill certain criteria to use outbound pools to send emails. For more information on such domains, see Outbound page.

Note

For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

## Inbound page

![inbound-page](../../exchangeonline/media/top-domain-inbound-page.png)

Note

By default, the report shows data for the last seven days.

This page shows the following information for each domain:

- **Domain**
- **Domain status**: The value is **Healthy** or **Error**
- **Previous MX record**
- **Current MX record**
- **Email received (past 6 hours)**

To quickly filter the results, select **Search**![Search icon.](../../exchangeonline/media/modern-eac-search-icon.png) and start typing a value.

For more advanced filters that you can also save and use later, select **Filter**![Filter icon.](../../exchangeonline/media/modern-eac-filter-icon.png) and select **New filter**. In the **Custom filter** flyout that appears, enter the following information:

- **Name your filter**: Enter a unique name.
- Select **Add new clause**. A clause contains the following elements that you need to enter information for:

    - **Field**: Select **Domain**, **Domain status**, **Previous MX record**, **Current MX record**, or **Email received (past 6 hours)**.
    - **Operator**: Select **starts with** or **is**.
    - **Value**: Enter the value you want to search for.

    You can select **Add new clause** as many times as you need. Multiple clauses use AND logic (&lt;Clause1&gt; AND &lt;Clause2&gt;...).

    To remove a clause, select **Remove**![Remove icon.](../../exchangeonline/media/modern-eac-remove-icon.png).

    When you're finished, select **Save**. The new filter is automatically loaded, and the results change based on the filter. The "filter loading" and "change in results" are the same result as selecting **Filter** and selecting the customer filter from the list.

    To clear an existing filter (to return to the default list), select **Filter**![Active filter icon.](../../exchangeonline/media/modern-eac-filter-active-icon.png) and select **Clear all filters**.

Select **Export** to export the displayed results to a .csv file.

If you select a row, a details pane for the domain appears based on the value of **Domain status**:

- **Healthy**: An explanation about MX records and the same information from the main report is displayed.
- **Error**: Additional information about the cause of the error and how to fix it is available in the **Reason** and **How to fix** sections.

## Outbound page

The report on the Outbound page shows details of only domains that sent messages using high risk or relay pools or that sent more than 20 messages.

Note

Domains that don't use the high risk or relay pools or sent less than 20 messages are summarized together under **All other domains**. For more information on the summarized domains, use the **Request report** feature.

![outbound-page](../../exchangeonline/media/top-domain-outbound-page.png)

Note

By default, the report shows data for the last seven days.

To quickly filter the results, select **Search**![Search icon.](../../exchangeonline/media/modern-eac-search-icon.png) and start typing a value.

This page shows the following information for each domain:

- **Domain**
- Mail sent from each domain for the outbound pools:

    - **Normal**
    - **High Risk**
    - **Normal Relay**
    - **High Risk Relay**
    - **Bulk Risk**
    - **Low Risk**
- Pie charts:

    - Total outbound messages sent per domain
    - Total outbound messages by outbound pool

Select **Export** to export the displayed results to a .csv file.

For more information on the outbound pools, see [Outbound delivery pools](/en-us/defender-office-365/outbound-spam-high-risk-delivery-pool-about#relay-pool).