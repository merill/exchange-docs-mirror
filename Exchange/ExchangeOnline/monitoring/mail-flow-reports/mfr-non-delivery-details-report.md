---
layout: Conceptual
title: Non-delivery details report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-non-delivery-details-report
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
description: Admins can learn how to use the Non-delivery details report in the new Exchange admin center to monitor the most frequently encountered error codes in non-delivery reports (also known as NDRs or bounce messages) from senders in your organization.
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: 5526e3d5-9f9f-9f90-f86d-5fa1fb693fe9
document_version_independent_id: cfd1722f-cdb8-d5bb-732f-3b538eada9af
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-non-delivery-details-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-non-delivery-details-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-non-delivery-details-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 0421c2ce-139a-ded0-9031-8d18e81ca27f
---

# Non-delivery details report in the new EAC in Exchange Online | Microsoft Learn

The **Non-delivery details report** in the new Exchange admin center (new EAC) shows the most-encountered error codes in non-delivery reports (also known as NDRs or bounce messages) for users in your organization. This report shows the details of NDRs so you can troubleshoot email delivery problems.

Note

By default, the report shows data for the last 7 days. If the report is empty, try changing the date range.

For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

![Overview of the Non-delivery details report.](../../exchangeonline/media/mfr-non-delivery-details-report.png)

The chart in the overview section contains the most-encountered NDR error codes for a given day. If you hover over a specific color in the chart, you'll see the number of messages for that specific error code.

The **Non-delivery details** section shows the following information for each date-error code combination:

- **Date**
- **Count**
- **Error code**
- **Sample messages**: This field contains the internet message IDs (also known as the Client IDs) of a sample of the original messages. This value is stored in the **Message-ID** header field in the message header and is constant for the lifetime of the message.

To quickly filter the results, click **Search**![Search icon.](../../exchangeonline/media/modern-eac-search-icon.png) and start typing a value.

To filter the results by date range or error code, use the boxes. You can specify a date range up to 90 days.

For more advanced filters that you can also save and use later, click **Filter**![Filter icon.](../../exchangeonline/media/modern-eac-filter-icon.png) and select **New filter**. In the **Custom filter** flyout that appears, enter the following information:

- **Name your filter**: Enter a unique name.
- Click **Add new clause**. A clause contains the following elements that you need to enter:

    - **Field**: Select **Date**, **Count**, **Error code** or **Sample messages**.
    - **Operator**: Select **starts with** or **is**.
    - **Value**: Enter the value you want to search for.

    You can click **Add new clause** as many times as you need. Multiple clauses use AND logic (&lt;Clause1&gt; AND &lt;Clause2&gt;...).

    To remove a clause, click **Remove**![Remove icon.](../../exchangeonline/media/modern-eac-remove-icon.png)

    When you're finished, click **Save**. The new filter is automatically loaded, and the results are changed based on the filter. This is the same result as clicking **Filter** and selecting the customer filter from the list.

    To unload a existing filter (return to the default list), click **Filter**![Active filter icon.](../../exchangeonline/media/modern-eac-filter-active-icon.png) and select **Clear all filters**.

Click **Export** to export the displayed results to a .csv file.