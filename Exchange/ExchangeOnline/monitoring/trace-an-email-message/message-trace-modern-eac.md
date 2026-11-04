---
layout: Conceptual
title: Message trace in the new EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/trace-an-email-message/message-trace-modern-eac
Manager: anaruxa
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
ms.author: lusassl
author: lusassl-msft
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
ms.custom: 
description: Admins can use message trace in the new Exchange admin center to find out what happened to messages.
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: b171f582-bbe1-0ddf-2b0b-cd43769dd3ca
document_version_independent_id: 2a03592e-719c-5004-655a-ce71e28ccbc0
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/trace-an-email-message/message-trace-modern-eac.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/trace-an-email-message/message-trace-modern-eac
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/trace-an-email-message/message-trace-modern-eac.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 5d567e0b-794d-83bd-98b6-73bb744016c1
---

# Message trace in the new EAC in Exchange Online | Microsoft Learn

Message trace in the Exchange admin center (EAC) follows email messages as they travel through your Microsoft 365 organization. You can determine if the service received, rejected, deferred, or delivered a message. Message trace also shows what actions were taken on the message before it reached its final status. You can use the information from message trace to efficiently answer user questions about what happened to messages, to troubleshoot mail flow issues, and to validate policy changes.

## What do you need to know before you begin?

- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Exchange Online permissions](../../permissions-exo/permissions-exo): Membership in the **Organization Management** role group.
    - [Microsoft Entra permissions](/en-us/microsoft-365/admin/add-users/about-admin-roles): Membership in the **Global Administrator**^\*^ or **Exchange Administrator** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.
- The maximum number of messages that are displayed in the results depends on the report type you selected. For more information, see the Message trace results. The [Get-HistoricalSearch](/en-us/powershell/module/exchangepowershell/get-historicalsearch) cmdlet in Exchange Online PowerShell returns all messages in the results.

## Open message trace

In the EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Message trace**. Or, to go directly to the **Message trace** page, use https://admin.exchange.microsoft.com/#/messagetrace.

## Message trace page

On the **Message trace** page, you can start a new default trace by selecting ![](../../exchangeonline/media/modern-eac-create-icon.png)**Start a trace**.

In the **New message trace** flyout that opens, the default selections search for all messages for all senders and recipients for the last two days. Or, you can use one of the stored queries from the available tabs (as-is or as a starting points for your own queries):

- **Default queries**: Built-in queries provided by Microsoft 365.
- **Custom queries**: Queries saved by admins in your organization for future use.
- **Autosaved queries**: The last 10 most recently run queries. This list makes it simple to pick up from where you left off.

The **Downloadable reports** tab shows the downloadable report requests and the reports themselves when they're available for download.

[![The Message trace page in the new EAC.](../../exchangeonline/media/message-trace-page-new-eac.png)](../../exchangeonline/media/message-trace-page-new-eac.png#lightbox)

## Options for a new message trace

The following sections describe the available settings in the **New message trace** flyout that opens when you select ![](../../exchangeonline/media/modern-eac-create-icon.png)**Start a trace** or open an existing trace.

[![The New message trace flyout in the new EAC.](../../exchangeonline/media/message-trace-new-message-trace-flyout-new-eac.png)](../../exchangeonline/media/message-trace-new-message-trace-flyout-new-eac.png#lightbox)

### Senders and Recipients

The default value for **Senders** and **Recipients** is **All**, but you can enter specific values:

- **Senders**: Click in the box and start typing to enter or select one or more senders from your organization.
- **Recipients**: Click in the box and start typing to enter or select one or more recipients in your organization.

You can type the email addresses of external senders and recipients. Wildcards are supported (for example, `*@contoso.com`), but you can't use multiple wildcards in one value.

You can paste multiple sender or recipient lists separated by semicolons (`;`), spaces (`\s`), carriage returns (`\r`), or new lines (`\n`).

### Time range

In the **Time range** section, the default value is **2 days**, but you can specify date/time ranges up to 90 days. When you use date/time ranges, consider the following issues:

- By default, you select the time range in **Slider** view using a timeline.

    [![A Slider time range in a new message trace in the new EAC.](../../exchangeonline/media/message-trace-time-slider-new-eac.png)](../../exchangeonline/media/message-trace-time-slider-new-eac.png#lightbox)

    Saving a query in **Slider** view saves the relative time range (for example, two days from today).
- You can switch to **Custom time range** view to specify the following values:

    - **Time zone**: Applies to your query inputs and query results.
    - **Start date**: Date and time.
    - **End date**: Date and time.

    [![A Custom time range in a new message trace in the new EAC.](../../exchangeonline/media/message-trace-time-range-new-eac.png)](../../exchangeonline/media/message-trace-time-range-new-eac.png#lightbox)

    Saving a query in **Custom time range** view saves the absolute date/time range (for example, `2023-05-06 13:00 to 2023-05-08 18:00`).

For 10 days or less, the results are available instantly as a **Summary report**. You can also query up to 90 days of historical data for near real-time **Summary report** queries. However, you can only query 10 days' worth of data at a time.

If you specify a date/time range that's even slightly greater than 10 days:

- The results are available only as a downloadable CSV file (an **Enhanced summary report** or an **Extended report**).
- The results are prepared using archived message trace data. It might take several hours before the report is available to download. Depending on how many other admins also submitted report requests around the same time, you might also notice a delay before processing starts on a queued request.

### Detailed search options

In the **Detailed search options** section, the following options are available:

- **Subject filter:** The **Subject** filter for Message Trace queries has the following options: **starts with**, **ends with**, and **contains**. This filter also supports special characters.

    ![Screenshot of detailed search options.](../../exchangeonline/media/detailed-search-options-1.jpg)
- **Delivery status filter**: The **Delivery status filter** supports searches for status like, **Quarantined**, **Filtered as spam**, **Getting status** etc.

    [![Screenshot of delivery status filter.](../../exchangeonline/media/delivery-status-filter.jpg)](../../exchangeonline/media/delivery-status-filter.jpg#lightbox)

The following values are available:

- **All**: This is the default value.
- **Delivered**: The message was successfully delivered to the intended destination.
- **Expanded**: A distribution group recipient was expanded before delivery to the individual members of the group.
- **Failed**: The message wasn't delivered.
- **Pending**^\*^: Delivery of the message is being attempted or reattempted.
- **Recalled**: The message was recalled. For more information, see [Work with Cloud-based Message Recall.](/en-us/exchange/mail-flow-best-practices/work-with-cloud-based-message-recall)
- **Quarantined**^\*^: The message was quarantined (as spam, bulk mail, or phishing). For more information, see [Quarantined email messages](/en-us/defender-office-365/quarantine-about).
- **Filtered as spam**^\*^: The message was identified as spam, and was rejected or blocked (not quarantined).
- **Getting status:** Microsoft 365 recently received the message, but no other status data is yet available. You can check again within a few minutes.

^\*^ This value is available only in searches that are less than 10 days. If you need to query data that's older than 10 days, use the [Start-HistoricalSearch](/en-us/powershell/module/exchangepowershell/start-historicalsearch) cmdlet in Exchange Online PowerShell.

Note

There might be a five to ten minute delay between the reported and actual and reported delivery status values.

- **Message ID**: The internet message ID (also known as the Client ID) in the **Message-ID** header field in the message header. Users can give you this value to investigate specific messages.

    This value is constant for the lifetime of the message. For messages created in Microsoft 365 or Exchange, the **Message ID** value uses the format `<GUID@ServerFQDN>`, including the angled brackets. For example, `<d9683b4c-127b-413a-ae2e-fa7dfb32c69d@DM3NAM06BG401.Eop-nam06.prod.protection.outlook.com>`. Other email systems might use different syntax or values. This value is supposed to be unique, but not all email systems strictly follow this requirement. An arbitrary value is assigned if the **Message-ID:** header field doesn't exist or is blank for incoming messages from external sources.

    When you use **Message ID** to filter the results, ensure that you include the full string, including any angled brackets.
- **Network Message ID**: Network Message ID is a unique message ID value that prevails across copies of the message that might be created due to bifurcation, and across the message transport process. It's dynamic wherein its value differs for even a copy of the message's specific instance. Therefore, each copied version of the instance has a different **Network Message ID** value.

    The differences between **Network Message ID** and **Message ID** are summarized in the following table:

    | Network Message ID | Message ID |
    | --- | --- |
    | ID of the specific instance of an email message | ID of the email message |
    | Unique and persists across copies of the message that might be created due to message bifurcation | Constant for the lifetime of the message |

    For more information about **Network Message ID**, see the following information:

    - **Exchange Server**: [Message tracking logs](/en-us/exchange/mail-flow/transport-logs/message-tracking)
    - **Exchange Online**: [Enhanced message trace reports](message-trace-modern-eac)
    - **Outlook**: [Message headers](https://support.microsoft.com/office/cd039382-dc6e-4264-ac74-c048563d212c)

    To trace the **Network Message ID** value and use it to trace specific messages in Exchange Online, use any of the following message headers:

    - `X-MS-Exchange-Organization-Network-Message-Id`
    - `X-MS-Office365-Filtering-Correlation-Id`
    - `X-MS-Exchange-CrossTenant-Network-Message-Id`

    You can use the **Network Message ID** value from those headers to further retrieve specific messages. For example:

    - Messages sent by a specific sender.
    - Messages that were addressed to a specific recipient.
    - Message that were sent during a specified time period.

    You can also use the [Get-MessageTraceV2](/en-us/powershell/module/exchangepowershell/get-messagetracev2) cmdlet in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) to trace the **Network Message ID** value.

    The following example uses the **Network Message ID** value to find messages that were sent by `john@contoso.com` between June 13 2024, and June 15 2024:

    - The *MessageTraceID* parameter uses the **Network Message ID** value, which in this example is `2bbad36aa4674c7ba82f4b307fff549`.
    - The results of the **Get-MessageTraceV2** command are piped to the **Get-MessageTraceDetailV2**cmdlet. The results allow you to identify:
        - The **Network Message ID** value.
        - The specific messages this **Network Message ID** value helps in retrieving.

    ```powershell
    Get-MessageTraceV2 -MessageTraceId 2bbad36aa4674c7ba82f4b307fff549f -SenderAddress john@contoso.com -StartDate 06/13/2025 -EndDate 06/15/2025 | Get-MessageTraceDetailV2
    ```
- **Direction**: Select one of the following values:

    - **All**: This is the default value.
    - **Inbound**: Messages sent to recipients in your organization.
    - **Outbound**: Messages sent from users in your organization.
- **Original client IP address**: The IP address of the email sender's client computer or device. You can use this filter to investigate hacked computers that are sending large amounts of spam or malware. Although the messages might appear to come from multiple senders, it's likely that the same computer is generating all of the messages.

    Note

    Client IP address information is available only for 10 days and only in the **Enhanced summary report** or the **Extended report** (downloadable CSV files).

### Report type

The available report types are:

- **Summary report**: Available if the time range is less than 10 days, and requires no other filtering options. The results are available almost immediately after you select **Search**. The report returns up to 20,000 results.

    Select **Search** to start the message trace. You're taken to the **Message trace search results** page as described in the Summary report output section.

    The last 10 **Summary report** queries are available on the **Autosaved queries** tab on the **Message trace** page.
- **Enhanced summary report**: Includes the information in the summary report plus other details (for example, direction and original client IP address). Available only as a downloadable CSV file. The report returns up to 100,000 results.
- **Extended report**: Includes the same information as the extended summary report plus comprehensive routing and message event details. Available only as a downloadable CSV file. The report returns up to 1,000 results.

    The **Enhanced summary report** and the **Extended report** require one or more of the following filtering options, regardless of the time range: **Senders**, **Recipients**, or **Message ID**.

    The **Enhanced summary report** and the **Extended report** are prepared using archived message trace data. It might take several hours before the report is available to download. Depending on how many other admins also submitted report requests around the same time, you might also notice a delay before processing starts on a queued request.

    While you can select the **Enhanced summary report** or **Extended report** for any date/time range, the last 24 hours of archived data isn't typically available.

    The maximum size for a downloadable CSV file is 800 MB. If a downloadable report exceeds 800 MB, you can't open the report in Excel or Notepad.

    When you select **Next**, you're taken to a summary flyout that lists the selected filtering options, a unique (editable) title for the report, and the email address to receive the notification when the message trace completes (also editable, and must be in one of the accepted domains of your organization).

    Select **Prepare report** to submit the message trace. You can see the status of the report on the **Downloadable reports** tab. For more information about the data returned, see the Enhanced summary reports and Extended reports sections.

    Note

    The IP address of the outbound email protection server from the cloud is included in the Microsoft 365 SPF record, but isn't displayed in any message trace report types. This condition is by design, as message trace reports are generated before the involvement of the outbound email protection server.

## Message trace results

The different report types return different levels of information. The information that's available in the different reports is described in the following sections:

- Summary report output
- Enhanced summary reports
- Extended reports

### Summary report output

After you run the message trace, the results are sorted by descending date/time (most recent events first).

The **Summary report** contains the following information:

- **Date**: The date and time the service received the message, displayed using the configured UTC time zone.
- **Sender**: The email address of the sender (*alias*@*domain*).
- **Recipient**: The email address of the recipient. If the message has multiple recipients, each recipient is on a separate line. If the recipient is a distribution group, dynamic distribution group, or mail-enabled security group, the group is the first recipient, followed by each group member on a separate line.
- **Subject**: The first 256 characters of the message's **Subject:** field.
- **Status**: These values are described in the Detailed search options section.

By default, the first 250 results are loaded and readily available. When you scroll down, there's a slight pause as the next batch of results are loaded, up to a maximum of 10,000.

You can sort the entries by clicking on an available column header.

On the **Email** tab, you can decrease the vertical spacing in the list by clicking ![](../../exchangeonline/media/modern-eac-standard-icon.png)**Change view** and then selecting ![](../../exchangeonline/media/modern-eac-compact-icon.png)**Compact list**.

Use the ![](../../exchangeonline/media/modern-eac-search-icon.png)**Search** box and a corresponding value to find specific entries. Wildcards aren't supported

For more advanced filters that you can also save and use later, select ![](../../exchangeonline/media/modern-eac-filter-icon.png)**Filter** , and then select ![](../../exchangeonline/media/modern-eac-filter-icon.png)**New filter**. In the **Custom filter** flyout that opens, enter the following information:

- **Name your filter**: Enter a unique name.
- Add a filter clause by entering the following information:
    - **Field**: Select from the following values:
        - **Sender**
        - **Recipient**
        - **Subject**
        - **Status**
    - **Operator**: Select **starts with** or **is**.
    - **Value**: Enter the value you want to search for.

You can select **Add new clause** and repeat the previous step as many times as needed. Multiple clauses use AND logic (&lt;Clause1&gt; AND &lt;Clause2&gt;...).

To remove a filter clause, select ![](../../exchangeonline/media/modern-eac-remove-icon.png)**Remove clause** next to the entry.

When you're finished in the **Custom filter** flyout, select **Save**. The new filter is automatically loaded, and the filtered results are shown on the **Message trace search results** page. This result is the same as selecting ![](../../exchangeonline/media/modern-eac-filter-icon.png)**Filter** and then selecting the existing filter from the **Custom filters** section in the list.

To unload an existing filter and return to the default information on the **Message trace search results** page, select ![](../../exchangeonline/media/modern-eac-filter-active-icon.png) &gt; ![](../../exchangeonline/media/modern-eac-clear-filters-icon.png)**Clear all filters**.

Select ![](../../exchangeonline/media/itpro_eac_editicon.png)**Edit message trace** to edit the search criteria.

Use ![](../../exchangeonline/media/modern-eac-download-icon.png)**Export results** to export the displayed results to a CSV file.

Select ![](../../exchangeonline/media/itpro_eac_refreshicon.png)**Refresh** to refresh the results.

**Customizable columns:**

For your search results, you can select from the customizable columns.

[![Screenshot of customize column.](../../exchangeonline/media/customize-columns-1.png)](../../exchangeonline/media/customize-columns-1.png#lightbox)

**Wider flyout option**:

You can select the flyout option for a wider flyout for the Message trace detail.

[![Screenshot of flyout.](../../exchangeonline/media/flyout.jpg)](../../exchangeonline/media/flyout.jpg#lightbox)

**Time Zone Consistency**:

Message trace defaults to the time zone set in the Exchange account settings of the logged-on admin.

#### Find related records for this message

Related message records are records that share the same Message ID. Remember, even a single message sent between two people can generate multiple records. The number of records increases when the message is affected by distribution group expansion, forwarding, mail flow rules (also known as transport rules), and so on.

In the blank area next to the **Date** column, select the round check box that appears next to the entry. The following actions appear on the **Message traces results** page:

- ![](../../exchangeonline/media/modern-eac-copy-icon.png)**View in Explorer**: Opens the message in Explorer (Threat Explorer) in organizations with Microsoft Defender for Office 365 Plan 2. For more information, see [About Threat Explorer and Real-time detections in Microsoft Defender for Office 365](/en-us/defender-office-365/threat-explorer-real-time-detections-about).
- ![](../../exchangeonline/media/modern-eac-find-related-icon.png)**Go Hunting**: Looks for the message in Threat Explorer in organizations with Microsoft Defender for Office 365 Plan 2. For more information, see [Threat hunting in Threat Explorer for Microsoft Defender for Office 365](/en-us/defender-office-365/threat-explorer-threat-hunting)
- ![](../../exchangeonline/media/modern-eac-find-related-icon.png)**Find related**: Opens a new message trace to find the related records for the message.

For more information about the Message ID, see the Detailed search options section.

#### Message trace details

In the summary report output, you can view details about a message by clicking anywhere in the row other than the round check box that appears next to the **Date** value.

[![The details flyout that opens after clicking a row in the summary report message trace results in the new EAC.](../../exchangeonline/media/message-trace-message-details-full-modern-eac.png)](../../exchangeonline/media/message-trace-message-details-full-modern-eac.png#lightbox)

The details flyout contains the following information that's not present in the summary report:

- **Message events**: After you expand this section, you can see classifications that help categorize the actions that the service takes on messages. Some of the more interesting events that you might encounter are:

    - **Receive**: The service received the message.
    - **Send**: The service sent the message.
    - **Fail**: The message failed to be delivered.
    - **Deliver**: The message was delivered to a mailbox.
    - **Expand**: The message was sent to a distribution group that was expanded.
    - **Transfer**: Recipients were moved to a bifurcated message because of content conversion, message recipient limits, or agents.
    - **Defer**: The message delivery was postponed and might be reattempted later.
    - **Resolved**: The message was redirected to a new recipient address based on an Active Directory look up. When this event happens, the original recipient address is listed in a separate row in the message trace along with the final delivery status for the message.
    - **DLP rule**: The message had a DLP rule match.
    - **Sensitivity label:** A server-side labeling event occurred. For example, a label was automatically added to a message that includes an action to encrypt or was added via the web or mobile client. The Exchange server completes and logs the action. A label added via Outlook isn't included in the event field.

    **Notes**: An uneventful, successfully delivered message generates multiple **Event** entries in the message trace. For descriptions of more events, see [Event types in the message tracking log in on-premises Exchange](../../mail-flow/transport-logs/message-tracking#event-types-in-the-message-tracking-log).
- **More information**: After you expand this section, you can view the following details:

    - **Message ID**: This value is described in the Detailed search options section. An example of a **Message ID** value is `<d9683b4c-127b-413a-ae2e-fa7dfb32c69d@DM3NAM06BG401.Eop-nam06.prod.protection.outlook.com>`.
    - **Message size**: The size of the sent message, including attachments/pictures/text.
    - **From IP**: The IP address of the computer that sent the message. For outbound messages sent from Exchange Online, this value is blank.
    - **To IP**: The IP address or addresses where the service attempted to deliver the message. If the message has multiple recipients, these addresses are displayed. For inbound messages sent to Exchange Online, this value is blank.

### Enhanced summary reports

An **Enhanced summary report** is available on the **Downloadable reports** tab on the **Message trace** page:

- Reports that are available to download have the **Status** value **Complete**
- Reports that aren't available to download have the **Status** values **Not started** or **In progress**.

The following information is available in the **Enhanced summary report** CSV file:

- **origin\_timestamp**^\*^: The date and time the service initially received the message, displayed using the configured UTC time zone.
- **sender\_address**: The sender's email address (`alias@domain`).
- **Recipient\_status**: The status of the delivery of the message to the recipient. If the message was sent to multiple recipients, it shows all the recipients and the corresponding status for each, in the format: `<email address>##<status>`. Examples of the recipient statuses are:
    - **##Receive, Send** means the message was received by the service and was sent to the intended destination.
    - **##Receive, Fail** means the message was received by the service but delivery to the intended destination failed.
    - **##Receive, Deliver** means the message was received by the service and was delivered to the recipient's mailbox.
- **message\_subject**: The first 256 characters of the message's **Subject** field.
- **total\_bytes**: The size of the message in bytes, including attachments.
- **message\_id**: This value is described in the Detailed search options section. An example of a **message\_id** value is `<d9683b4c-127b-413a-ae2e-fa7dfb32c69d@DM3NAM06BG401.Eop-nam06.prod.protection.outlook.com>`.
- **network\_message\_id**: A unique message ID value that persists across all copies of the message that might be created due to bifurcation or distribution group expansion. An example of **network\_message\_id** value is `1341ac7b13fb42ab4d4408cf7f55890f`.
- **original\_client\_ip**: The IP address of the sender's SMTP server.
- **directionality**: Indicates whether the message was sent inbound (to your organization) or outbound (from your organization).
- **connector\_id**: The name of the source or destination connector. For more information about connectors in Exchange Online, see [Configure mail flow using connectors in Office 365](../../mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow).
- **delivery\_priority**^\*^: Whether the message was sent with **High**, **Low**, or **Normal** priority.

^\*^ These properties are available only in an **Enhanced summary report**.

### Extended reports

An **Extended report** is available on the **Downloadable reports** tab on the **Message trace** page:

- Reports that are available to download have the **Status** value **Complete**
- Reports that aren't available to download have the **Status** values **Not started** or **In progress**.

The following information is available in the **Enhanced report** CSV file:

- **client\_ip**: The IP address of the email server or messaging client that submitted the message.
- **client\_hostname**: The host name or FQDN of the email server or messaging client that submitted the message.
- **server\_ip**: The IP address of the source or destination server.
- **server\_hostname**: The host name or FQDN of the destination server.
- **source\_context**: Extra information associated with the **source** field. For example:

    - `Protocol Filter Agent`
    - `3489061114359050000`
- **source**: The Exchange Online component that's responsible for the event. For example:

    - `AGENT`
    - `MAILBOXRULE`
    - `SMTP`
- **event\_id**: This value corresponds to the **Message event** values that are explained in Find related records for this message.
- **internal\_message\_id**: A message identifier assigned by the Exchange Online server that's currently processing the message.
- **recipient\_address**: The email addresses of the message's recipients. Multiple email addresses are separated by the semicolon character (;).
- **recipient\_count**: The total number of recipients in the message.
- **related\_recipient\_address**: Present with `EXPAND`, `REDIRECT`, and `RESOLVE` events to display other recipients' email addresses that are associated with the message.
- **reference**: This field contains additional information for specific types of events. For example:

    - **DSN**: Contains the report link, which is the **message\_id** value of the associated delivery status notification (also known as a DSN, nondelivery report, NDR, or bounce message) if a DSN is generated subsequent to this event. If this message is a DSN message, this field contains the **message\_id** value of the original message that the DSN was generated for.
    - **EXPAND**: Contains the **related\_recipient\_address** value of the related messages.
    - **RECEIVE**: Might contain the **message\_id** value of the related message if the message was generated by other processes (for example, Inbox rules).
    - **SEND**: Contains the **internal\_message\_id** value of any DSN message.
    - **TRANSFER**: Contains the **internal\_message\_id** value of the message that's being forked (for example, by content conversion, message recipient limits, or agents).
    - **MAILBOXRULE**: Contains the **internal\_message\_id** value of the inbound message that caused the Inbox rule to generate the outbound message.

        For other types of events, this field (**internal\_message\_id**) is blank.
- **return\_path**: The return email address specified by the **MAIL FROM** command that sent the message. Although this field is never empty, it can have the null sender address value represented as `<>`.
- **message\_info**: Additional information about the message. For example:

    - The message origination date-time in UTC for `DELIVER` and `SEND` events. The origination date-time is the time when the message first entered the Exchange Online organization. The UTC date-time is represented in the ISO 8601 date-time format: `yyyy-MM-ddThh:mm:ss.fffZ`, where `yyyy` = year, `MM` = month, `dd` = day, `T` indicates the beginning of the time component, `hh` = hour, `mm` = minute, `ss` = second, `fff` = fractions of a second, and `Z` signifies `Zulu`, which is another way to denote UTC.
    - Authentication errors. For example, you might see the value `11a` and the type of authentication that was used when the authentication error occurred.
- **tenant\_id**: A GUID value that represents the Exchange Online organization (for example, `39238e87-b5ab-4ef6-a559-af54c6b07b42`).
- **original\_server\_ip**: The IP address of the original server.
- **custom\_data**: Contains data related to specific event types. For more information, see the following sections:

    - custom_data values
    - Spam filter agent
    - Malware filter agent
    - Transport Rule agent

#### custom\_data values

The **custom\_data** field for an `AGENTINFO` event is used by various Exchange Online agents to log message-processing details. Some of the more interesting agents are described in the following sections.

- Spam filter agent
- Malware filter agent
- Transport Rule agent

#### Spam filter agent

A **custom\_data** value that starts with `S:SFA` is from the spam filter agent. For more information, see [X-Forefront-Antispam-Report message header fields](/en-us/defender-office-365/message-headers-eop-mdo#x-forefront-antispam-report-message-header-fields).

An example of a **custom\_data** value for a spam-filtered message looks like this:

`S:SFA=SUM|SFV=SPM|IPV=CAL|SRV=BULK|SFS=470454002|SFS=349001|SCL=9|SCORE=-1|LIST=0|DI=SN|RD=ftmail.inc.com|H=ftmail.inc.com|CIP=98.129.140.74|SFP=1501|ASF=1|CTRY=US|CLTCTRY=|LANG=en|LAT=287|LAT=260|LAT=18;`

#### Malware filter agent

A **custom\_data** value that starts with `S:AMA` is from the malware filter agent. The key details are described in the following table:

| Value | Description |
| --- | --- |
| `AMA=SUM|v=1|` or `AMA=EV|v=1` | The message was determined to contain malware. <br>- `SUM`: Any number of engines could have detected the message as malware.<br>- `EV`: A specific engine detected the message as malware.<br><br> When an engine detects malware, the subsequent actions are triggered. |
| `Action=r` | The message was replaced. |
| `Action=p` | The message was bypassed. |
| `Action=d` | The message was deferred. |
| `Action=s` | The message was deleted. |
| `Action=st` | The message was bypassed. |
| `Action=sy` | The message was bypassed. |
| `Action=ni` | The message was rejected. |
| `Action=ne` | The message was rejected. |
| `Action=b` | The message was blocked. |
| `Name=<malware>` | The name of the malware that was detected. |
| `File=<filename>` | The name of the file that contained the malware. |

An example of a **custom\_data** value for a message that contains malware looks like this:

`S:AMA=SUM|v=1|action=b|error=|atch=1;S:AMA=EV|engine=M|v=1|sig=1.155.974.0|name=DOS/Test_File|file=filename;S:AMA=EV|engine=A|v=1|sig=201707282038|name=Test_File|file=filename`

#### Transport Rule agent

A **custom\_data** value that starts with`S:TRA` is from the Transport Rule agent for mail flow rules (also known as transport rules). The key details are described in the following table:

| Value | Description |
| --- | --- |
| `ETR|ruleId=<guid>` | The rule ID that was matched. |
| `St=<datetime>` | The date and time in UTC when the rule match occurred. |
| `Action=<ActionDefinition>` | The action that was applied. For a list of available actions, see [Mail flow rule actions in Exchange Online](../../security-and-compliance/mail-flow-rules/mail-flow-rule-actions). |
| `Mode=<Mode>` | The mode of the rule. Valid values are: <br>- **Enforce**: All actions on the rule are enforced.<br>- **Test with Policy Tips:**: Any Policy Tip actions are sent, but other enforcement actions aren't acted on.<br>- **Test without Policy Tips**: Actions are listed in a log file, but senders aren't notified in any way, and enforcement actions aren't acted on.&lt;/li? |

An example of a **custom\_data** value for a message that matches the conditions of a mail flow rule looks like this:

`S:TRA=ETR|ruleId=19a25eb2-3e43-4896-ad9e-47b6c359779d|st=7/17/2017 12:31:25 AM|action=ApplyHtmlDisclaimer|sev=1|mode=Enforce`

## Using PowerShell cmdlet Get-MessageTraceV2

To utilize the new Message trace functionality via the new PowerShell cmdlet `Get-MessageTraceV2`, ensure you're using version 3.7.0 or later of the [Exchange Online PowerShell V3 module](/en-us/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps&amp;preserve-view=true).

**Throttling limits**:

To reduce the risk of misuse and abuse of Exchange Online resources, ensure services availability for all users, and provide a predictable experience for our customers, we implemented a rate-based throttling limit based on the number of requests in a time period. For a tenant, a maximum of 100 query requests are accepted within a 5-minute running window. Throttling is automatically not applied if the request rate is lower than 100 requests in the past 5 minutes. If your tenant has automation set up to query more frequently than the throttling threshold, update your automation to fit below the throttling limit.

| Cmdlet | Tenant level limit |
| --- | --- |
| `Get-MesesageTraceV2` | 100 requests per 5 min |
| `Get-MessageTraceDetailV2` | 100 requests per 5 min |

***ResultSize* parameter**: The new Message trace supports a default value of 1000 results and a maximum of 5000 results (set via the `-ResultSize` parameter). This change is to ensure fair use of our resources, as pagination can create performance issues for our system.

***StartingRecipientAddress* parameter**: This parameter's main use is to help pulling subsequent data while minimizing duplication.

Since pagination is no longer supported, you can utilize the `EndTime` parameter with the `Received` time of the last record of the query results and fill in the `StartingRecipientAddresss` parameter with `RecipientAddress` of the last record of the previous result. For more information, see the example below.

![Screenshot of sample data.](../../exchangeonline/media/sample-data.png)

For the sample data above, you can pull the first 10 records using the following query:

```powershell
Get-MessageTraceV2 -StartDate '2024-11-01T00:00:00Z' -EndDate '2024-11-01T00:10:00Z' -ResultSize 10
```

In the V2 example below, we're using the `StartingRecipientAddress` of the last recipient (r\_1\_010@contoso) from the previous results. To pull the next subsequent records, use the following query.

```powershell
Get-MessageTraceV2 -StartDate '2024-11-01T00:00:00Z' -EndDate '2024-11-01T00:10:00Z' -ResultSize 10 -StartingRecipientAddress r_1_010@contoso.com
```

## Best practices

To improve query performance, specify as many and as precise filters as possible. We highly recommend that admins narrow the gap between `StartDate` and `EndDate` whenever possible. It's also advisable to set more parameters, such as `SenderAddress`, when the sender is known. Use `MessageTraceId` when applicable for PowerShell queries. This is required when querying data for messages sent to over 1,000 recipients. This is also supported in EAC now.

Set the `MessageTraceId` (also known as `NetworkMsgId` in the message tracking log) when investigating a specific message or when a message is sent to many recipients (for example, over 1,000). This is required to obtain complete results. When used together with `StartingRecipientAddress`, you can retrieve the full dataset in multiple rounds. For more information on `StartingRecipientAddress`, see the FAQ section.

## Frequently asked questions

### How can we tell if partial results are displayed?

For EAC users, scroll down to get more results until the data is complete. Users don't have to take any additional action, and V2 will load it automatically as user scrolls down to get additional results. For Exchange Online PowerShell cmdlet users, we're working on providing a hint in the output for the next query if the data is partial (expected within next few weeks). For now, users can utilize the sample script below to gather results continuously.

Sample script:

```powershell
$mt = Get-MessageTraceV2 -<filters>

$nextRound = Get-MessageTraceV2 -<filters> -EndDate $mt[-1].Received.ToString("O")
```

### How could pagination from V1 be achieved in V2?

Pagination is deprecated in V2 to ensure fair use of resources and query performance for all users. Instead, you can get results round by round. The results are ordered by `Received` in descending order first, then `RecipientAddress` in ascending order (case-insensitive). To get the next round of results, update the `EndDate` parameter to the `Received` value of the last data from the current round. Refer to the sample scripts in the previous section.

### When and how could we use the parameter: `StartingRecipientAddress`?

The `StartingRecipientAddress` parameter is used to get the next round of data. `StartingRecipientAddress` together with `Received`, can get the results round by round to get the complete results. In the next round, data that shares the same `Received` as the last result in the current round but has `RecipientAddress` that is alphabetically larger than the `StartingRecipientAddress`(case-insensitive), or older than the last result in the current round, will be output.

Sample script:

```powershell
$mt = Get-MessageTraceV2 -<filters>

$nextRound = Get-MessageTraceV2 -<filters> -EndDate $mt[-1].Received.ToString("O") -StartingRecipientAddress $mt[-1].RecipientAddress
```