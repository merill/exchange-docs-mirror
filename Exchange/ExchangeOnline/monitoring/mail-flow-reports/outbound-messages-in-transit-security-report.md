---
layout: Conceptual
title: Outbound messages in Transit Security report in the Exchange Admin Center for Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/mail-flow-reports/outbound-messages-in-transit-security-report
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
author: alekyaj
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
description: Outbound messages in Transit Security report in the Exchange Admin Center for Exchange Online includes information about SMTP DANE with DNSSEC, MTA-STS, and Opportunistic TLS.
ms.date: 2023-01-05T00:00:00.0000000Z
locale: en-us
document_id: bd91f2f7-06f2-515b-f45b-cfa6742e64ce
document_version_independent_id: 234413fe-d1a9-5b6b-6efd-d4a0e95e7430
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/mail-flow-reports/outbound-messages-in-transit-security-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/mail-flow-reports/outbound-messages-in-transit-security-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/mail-flow-reports/outbound-messages-in-transit-security-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: cce79d15-08ac-7e4d-7966-9148fbbb5c4f
---

# Outbound messages in Transit Security report in the Exchange Admin Center for Exchange Online | Microsoft Learn

The Outbound messages in Transit Security report in the Exchange Admin Center (EAC) displays information about outbound [SMTP DNS-based Authentication of Named Entities (DANE)](/en-us/purview/how-smtp-dane-works), [MTA-Strict Transport Security (STS)](/en-us/purview/enhancing-mail-flow-with-mta-sts), and Opportunistic TLS usage data when being sent from Exchange Online.

Note

[SMTP DANE with DNSSEC](https://techcommunity.microsoft.com/t5/exchange-team-blog/releasing-outbound-smtp-dane-with-dnssec/ba-p/3100920) and [MTA-STS](https://techcommunity.microsoft.com/t5/exchange-team-blog/introducing-mta-sts-for-exchange-online/ba-p/3106386) are both turned on by default on the outbound path when the messages are being sent from Exchange Online.

The report consists of the following sections:

1. **Messages Blocked**: This section provides aggregated information for tenant admins regarding SMTP DANE with DNSSEC or MTA-STS errors experienced when trying to send to destination domains that have been configured with either of the security protocols. If no errors were detected, the section will consist of an empty table.
2. **Messages Sent**: This section provides time-series data for emails secured by SMTP DANE with DNSSEC, MTA-STS, TLS-Only, or No TLS.
3. **Recipient Domains Not Supporting TLS**: This section provides time series data for messages that were sent to a destination domain in plain text (unencrypted) because the destination didn't support TLS. Exchange Online always attempts to send messages using TLS, but if the destination doesn't support it, then the default behavior is "to send the email".

Note

The data in Exchange Admin Center mail flow reports lags by 24 hours.

## Messages Blocked

The "Messages Blocked" section is displayed by default and shows a table with the following four columns of information:

- **Recipient Domain**: The domain that is experiencing the error.
- **Security Type**: The security protocol attempted.
- **Count of Messages Blocked**: The summarized count of messages that were affected by an error over the selected time period, this is sorted by default as **descending**.
- **Distinct Error Generated for Domain**: The distinct error type that affected all the emails in the row.

[![Screenshot displaying the data of Messages Blocked section.](../../exchangeonline/media/report-messagesblocked1.png)](../../exchangeonline/media/report-messagesblocked1.png#lightbox)

The table aggregation works over a configurable time period. Filters can be created using **Starts With** or **Is** operators on the following columns:

- Recipient Domain
- Security Type
- Distinct Error Generated for Domain

To search for a specific piece of information, select **Search** and start typing a value.

To export the report data to a .csv file, choose any of the following three options:

- **Export all results**: This option enables you to export all messages affected by all SMTP DANE with DNSSEC or MTA-STS errors over the selected time period.
- **Export loaded results**: This option enables you to export the rows of aggregated data that are currently loaded into view.
- **Export selected**: This option enables you to export all messages of the selected rows that were affected by all SMTP DANE with DNSSEC or MTA-STS errors over the selected time period.

To drill into the nonaggregated data live, without having to wait on exporting the data, click on the domain, such as contoso.com from the row in the **Messages Blocked** table. A pop up immediately appears with a new table consisting of a row for each message that was affected by the selected rows' error. The new pop-up table includes the following columns:

- **Time**: Time of the failure event in UTC.
- **Security type**: The allowed values are: - SMTP DANE with DNSSEC - MTA-STS
- **Error Details**: Contains the error code and statement.
- **Sender**: Sender's email address.
- **Recipient**: Recipient's email address.
- **Recipient Domain**: The destination domain experiencing the error.
- **Message ID**: ID of the message affected by the error.

You can use the **Request report** option to receive the data and can filter based on *Security Type and Error*. The Request report generates a .csv file that includes the same fields with up to 90 days of data.

## Messages Sent

The "Messages Sent" section shows time series data for messages successfully sent using five methods, SMTP DANE with DNSSEC, MTA-STS, both SMTP DANE with DNSSEC and MTA-STS, TLS-Only, or No TLS (plain text).

The data is automatically visualized through a time series chart showing the volume of emails secured by each of the five methods over a configurable time period.

Note

The time period '7 days' is selected by default, but you can also select 30 days, 90 days, or custom time spans with options to filter by *Security Type*.

The bar chart from the report shows a summary of the volume of emails secured over the selected time period for an aggregated view.

[![Screenshot of the chart displaying the Messages Sent section of the report.](../../exchangeonline/media/report-messages-sent1.png)](../../exchangeonline/media/report-messages-sent1.png#lightbox)

Requesting a report generates a .csv file containing a table with the following fields:

- **Date**: Date of the *Send* event in UTC.
- **Security type**: SMTP DANE with DNSSEC, MTA-STS, SMTP DANE with DNSSEC and MTA-STS, TLS-only, or No TLS.
- **Count Of Secured Messages**: Number of emails secured by *Security Type*, over a selected time duration.

## Recipient Domains Not Supporting TLS

The "Recipient Domains Not Supporting TLS" section can be accessed by selecting **Recipient Domains Not Supporting TLS**. It shows time series data for messages that were sent to a destination domain in plain text (unencrypted) because the destination didn't support TLS.

Exchange Online always attempts to send messages with the help of TLS, but if the destination domain doesn't support it then the default behavior is to "send the email".

The domain that didn't support TLS and the number of emails sent to that domain for a configurable time period appear in the **Recipient Domains Not Supporting TLS** table.

Note

The default time period is '7 days', which is selected by default; however, you can also select 1 day, or 30 days.

You can export data regarding "the top 20 domains not supporting TLS" or "the top 100 domains not supporting TLS."

[![Screenshot of the chart showing Recipient Domains not Supporting TLS section of the report.](../../exchangeonline/media/recipient-domains-notsupporting-tls1.png)](../../exchangeonline/media/recipient-domains-notsupporting-tls1.png#lightbox)