---
layout: Conceptual
title: Non-accepted domain report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-non-accepted-domain-report
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
description: Admins can learn how to use the Non-accepted domain report in the new Exchange admin center to monitor messages from on-premises organizations where the sender's domain isn't configured in Microsoft 365.
ms.date: 2023-07-28T00:00:00.0000000Z
locale: en-us
document_id: 7be584df-feb8-8cf6-f507-dae6e1d51aee
document_version_independent_id: f74fef1c-04a9-5faf-4d9c-5d59c9b71ff7
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-non-accepted-domain-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-non-accepted-domain-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-non-accepted-domain-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 72f2e8e0-73ce-0ccd-436b-af1ced1d85fd
---

# Non-accepted domain report in the new EAC in Exchange Online | Microsoft Learn

The **Non-accepted domain** report in the new Exchange admin center (new EAC) displays information about messages from your on-premises email organization where the sender's domain isn't configured as an accepted domain in your Microsoft 365 organization.

Microsoft 365 might throttle these messages if we have data to prove that the intent of these messages is malicious. Therefore, it's important for you to understand what's happening and to fix the issue.

Note

By default, the report shows data for the last 7 days. If the report is empty, try changing the date range.

For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

In the new EAC at https://admin.exchange.microsoft.com, select **Reports** &gt; **Mail flow** &gt; **Non-accepted domain report**. Or, to go directly to the **Non-accepted domain report** page, use https://admin.exchange.microsoft.com/#/reports/nonaccepteddomain.

On **Non-accepted domain report** page, the overview section contains a chart that shows the number of messages sent per connector:

![Overview of the Auto forwarded messages report.](../../exchangeonline/media/mfr-non-accepted-domain-report.png)

The **Non-Accepted domain details** section contains the following information:

- **Date**
- **Inbound connector name**
- **Sender domain**
- **Count**
- **Sample messages**: This field contains the internet message IDs (also known as the Client IDs) of a sample of the original messages. This value is stored in the **Message-ID** header field in the message header and is constant for the lifetime of the message.

Click on the column headers to sort by those categories.

![Normal list icon.](../../exchangeonline/media/modern-eac-standard-icon.png)![Compact list icon.](../../exchangeonline/media/modern-eac-compact-icon.png)

To change the list from normal to compact spacing, select **Change view**![Normal list icon.](../../exchangeonline/media/modern-eac-standard-icon.png), and then select **Compact list**![Compact list icon.](../../exchangeonline/media/modern-eac-compact-icon.png).

Use the **Search**![Search icon.](../../exchangeonline/media/modern-eac-search-icon.png) box to filter the results by connector name.

Use the **7 days** box to filter the results by date. The following values are available in the dropdown list:

- **7 days**
- **30 days**
- **90 days**
- **Custom start date**. You can specify a start date up to 90 days old.

For more advanced filters that you can also save and use later, select **Filter**![Filter icon.](../../exchangeonline/media/modern-eac-filter-icon.png), and then select **New filter**![New filter icon.](../../exchangeonline/media/modern-eac-create-icon.png). In the **Custom filter** flyout that opens, enter the following information:

- **Name your filter**: Enter a unique name.
- Add a filter clause by entering the following information:

    - **Field**: Select from the following values:
        - **Date**
        - **Inbound connector**
        - **Sender domain**
        - **Count**
        - **Sample messages**.
    - **Operator**: Select **starts with** or **is**.
    - **Value**: Enter the value you want to search for.

    You can select **Add new clause** and repeat the previous step as many times as needed. Multiple clauses use AND logic (&lt;Clause1&gt; AND &lt;Clause2&gt;...).

    To remove a filter clause, select **Remove clause**![Remove clause icon.](../../exchangeonline/media/modern-eac-remove-icon.png) next to the entry.

    When you're finished in the **Custom filter** flyout, select **Save**. The new filter is automatically loaded, and the filtered results are shown on the **Non-accepted domain report** page. This result is the same as selecting **Filter**![Filter icon.](../../exchangeonline/media/modern-eac-filter-icon.png) and then selecting the existing filter from the list.

    To unload an existing filter and return to the default information that's shown on the **Non-accepted domain report** page, select **Filter**![Active filter icon.](../../exchangeonline/media/modern-eac-filter-active-icon.png) &gt; **Clear all filters**![Clear all filters icon.](../../exchangeonline/media/modern-eac-clear-filters-icon.png).

Use **Export**![Export icon.](../../exchangeonline/media/modern-eac-download-icon.png) to export the displayed results to a .csv file.

Use **Request report**![Request report icon.](../../exchangeonline/media/modern-eac-request-report-icon.png) to generate a non-accepted domain report with up to one million rows of data.