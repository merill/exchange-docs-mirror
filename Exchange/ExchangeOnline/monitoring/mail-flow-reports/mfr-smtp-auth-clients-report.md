---
layout: Conceptual
title: SMTP AUTH clients report in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/mfr-smtp-auth-clients-report
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
description: Admins can learn how to use the SMTP AUTH report in the new Exchange admin center to monitor email senders in your organization that use authenticated SMTP (SMTP AUTH) to send email messages.
ms.date: 2020-07-30T00:00:00.0000000Z
locale: en-us
document_id: bf2462cd-4224-c954-a1ed-59357a539238
document_version_independent_id: eb4d7ebd-926f-2ae4-4516-61a9e953f511
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-smtp-auth-clients-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/mfr-smtp-auth-clients-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/mfr-smtp-auth-clients-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 4c957719-8a06-1a3c-549e-935d69919db5
---

# SMTP AUTH clients report in the new EAC in Exchange Online | Microsoft Learn

The **SMTP AUTH Clients** report in the new Exchange admin center (new EAC) highlights the use of the SMTP AUTH client submission protocol by users or system accounts in your organization. By default, this legacy protocol (which uses the endpoint smtp.office365.com) supports Basic authentication, and is susceptible to being used to send email from compromised accounts. This report allows you to check for unusual activity. It also shows the TLS usage data for clients or devices using SMTP AUTH.

You can find this report at **Reports &gt; Mail Flow** in the new EAC.

Note

By default, the report shows data for the last 7 days. If the report is empty, try changing the date range.

For permissions that are required to use this report, see [Permissions required to view mail flow reports](mail-flow-reports#permissions-required-to-view-mail-flow-reports).

The overview section contains the following charts:

- The volume of messages per day for each sending domain.
- **Message volume by sender**^\*^
- **Message sent by domain**^\*^
- **Senders by TLS protocol**^\*^

^\*^ If you hover over a specific color in the chart, you'll see the number of messages.

![Overview of the SMTP AUTH clients report.](../../exchangeonline/media/mfr-smtp-auth-clients-report.png)

The **Messages sent using SMTP Auth** section shows the following information:

- **Sender address**
- **Domain**
- **Authentication Protocol**: Values are either Basic Auth or Modern Auth. Basic Auth is TlsAuthLogin and Modern Auth is XOAUTH2.
- **TLS 1.0** (percentage)
- **TLS 1.1** (percentage)
- **TLS 1.2** (percentage)
- **Messages sent**

To quickly filter the results, click **Search**![Search icon.](../../exchangeonline/media/modern-eac-search-icon.png) and start typing a value.

To filter the results by a date range, use the box. You can specify a date range up to 90 days.

For more advanced filters that you can also save and use later, click **Filter**![Filter icon.](../../exchangeonline/media/modern-eac-filter-icon.png) and select **New filter**. In the **Custom filter** flyout that appears, enter the following information:

- **Name your filter**: Enter a unique name.
- Click **Add new clause**. A clause contains the following elements that you need to enter:

    - **Field**: Select **Sender address**, **Domain**, **TLS 1.0**, **TLS 1.1**, **TLS 1.2**, or **Messages sent**.
    - **Operator**: Select **starts with** or **is**.
    - **Value**: Enter the value you want to search for.

    You can click **Add new clause** as many times as you need. Multiple clauses use AND logic (&lt;Clause1&gt; AND &lt;Clause2&gt;...).

    To remove a clause, click **Remove**![Remove icon.](../../exchangeonline/media/modern-eac-remove-icon.png)

    When you're finished, click **Save**. The new filter is automatically loaded, and the results are changed based on the filter. This is the same result as clicking **Filter** and selecting the customer filter from the list.

    To unload an existing filter (return to the default list), click **Filter**![Active filter icon.](../../exchangeonline/media/modern-eac-filter-active-icon.png) and select **Clear all filters**.

Click **Export** to export the displayed results to a .csv file.

If you select a row, a details pane for the sender appears that contains the same information from the main report.