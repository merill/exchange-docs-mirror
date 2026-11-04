---
layout: Conceptual
title: Message Trace FAQ in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/trace-an-email-message/message-trace-faq
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
description: Frequently asked questions about message trace.
ms.topic: faq
author: AshaIyengar21
ms.author: serdars
ms.assetid: aa49e3f9-a5b1-4410-aac2-ddbbf3f5bfb2
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.custom: msecd-doc-authoring-1015
ms.date: 2026-08-11T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 902a5afc-2c7b-b41e-18ab-c31c87ef885c
document_version_independent_id: 698c4ad4-e857-1eda-7908-79d1d8325bf3
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/trace-an-email-message/message-trace-faq.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/trace-an-email-message/message-trace-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/trace-an-email-message/message-trace-faq.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: ae0a0845-3bf3-19a0-618c-6ad8e7bb4143
---

# Message Trace FAQ in Exchange Online | Microsoft Learn

This article presents messaging questions that a user might have, along with possible answers. It also describes how to use the message trace tool in order to get those answers and troubleshoot specific mail delivery issues.

## How long does it take to see results when running a message trace?

In the modern Exchange admin center (modern EAC), the search results appear immediately for messages that are less than 10 days old.

When you run a message trace for older messages, the results are returned within a few hours as a downloadable CSV file.

Note

The **Exchange message trace** link in the Microsoft Defender portal opens message trace in the modern EAC.

## How long does it take for a sent message to appear in a message trace?

When a message is sent, it should take between 5-10 minutes for the message to appear in the message trace data.

## Can I run a message trace in PowerShell? What are the cmdlets to use?

You can use the following cmdlets in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) to run a message trace:

[Get-MessageTraceV2](/en-us/powershell/module/exchangepowershell/get-messagetracev2): Search message data for the last 90 days. If you run this cmdlet without any parameters, only data from the last 48 hours is returned. You can only return 10 days worth of data per query.

[Get-MessageTraceDetailV2](/en-us/powershell/module/exchangepowershell/get-messagetracedetailv2): View the message trace event details for a specific message.

[Get-HistoricalSearch](/en-us/powershell/module/exchangepowershell/get-historicalsearch): Use this cmdlet to view information about historical searches done within the last 10 days.

[Start-HistoricalSearch](/en-us/powershell/module/exchangepowershell/start-historicalsearch): Start a new historical search for messages that are less than 90 days old.

[Stop-HistoricalSearch](/en-us/powershell/module/exchangepowershell/stop-historicalsearch): Stop queued historical searches that aren't started (the status value is `NotStarted`).

To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

## What is the message trace retention period?

Message trace data is retained for 90 days by default. This retention period is not configurable. After 90 days, message trace data is automatically purged from the system.

You can search for message data within this 90-day window using either the Exchange admin center (modern EAC) or Exchange Online PowerShell cmdlets like **Get-MessageTraceV2** and **Start-HistoricalSearch**.

## Why am I getting a timeout error when running a message trace in the user interface?

The likely cause of a timeout error is that the query is taking too long to process. Consider simplifying your search criteria. Consider using the **Get-MessageTraceV2** cmdlet, which has more liberal timeout requirements.

## Why didn't I receive an expected email message?

Here are some possible reasons:

- The message was detected as spam.
- The message was sent to quarantine due to a rule match.
- The message was rejected

    - By the malware filter
    - Because a file attached to the message contained malware
    - Because the message body contained malware
    - By a rule
    - Because the action was Reject
    - Because the action was Force TLS and TLS failed to be established
    - By a connector because TLS was required and failed to be established
- The message was sent for moderation and is awaiting approval or a moderator rejected it.
- The message was never sent.
- The message is still being processed because there was a previous failure and the service is reattempting delivery.
- The message failed to be delivered to your mailboxes

    - Because the destination isn't reachable
    - Because the destination rejected the message
    - Because the message timed out during the delivery attempt

To find out what happened:

[Run a message trace](run-a-message-trace-and-view-results#run-a-message-trace). Use as many search criteria as possible to narrow down the results. For example, you should know the sender and the intended recipient or recipients of the message, and the general time period when the message was sent.

View the results, locate the message, and then view specific details about the message. See [View message trace results for messages less than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-less-than-7-days-old) or [View message trace results for messages more than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-more-than-7-days-old). Look for the delivery status value **Failed** or **Pending** to explain why the message wasn't received.

Confirm that the message was sent, that the service successfully received it, that it wasn't filtered, redirected, or sent for moderation, and that it didn't experience any delivery failures or delays.

## Why did I receive an unexpected message?

Here are some possible reasons:

- The message was released from quarantine.
- The message was awaiting moderator approval and was released.
- The message was undetected spam.
- The message matched a rule that added you to the message.
- The message was sent to a distribution list of which you're a member.

To find out what happened:

[Run a message trace](run-a-message-trace-and-view-results#run-a-message-trace). Use as many search criteria as possible to narrow down the results. For example, specify the recipient who received the message, set the delivery status to **Delivered**, and set the time period based on when the message was received.

View the results, locate the message, and then view specific details about the message. See [View message trace results for messages less than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-less-than-7-days-old) or [View message trace results for messages more than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-more-than-7-days-old).

## Why didn't someone receive my message or why did I get this non-delivery report (also known as an NDR or bounce message)?

Here are some possible reasons:

- The message was detected as spam.
- The message was sent to quarantine due to a rule match.
- The message was rerouted because a connector sent it to another destination.
- The message was rejected:

    - By the malware filter
    - Because a file attached to the message contained malware
    - Because the message body contained malware
    - By a rule
    - Because the action was Reject
    - Because the action was Force TLS and TLS failed to be established
    - By a connector because TLS was required and failed to be established
- The message was sent for moderation and is awaiting approval a moderator rejected it.
- The message was never sent.
- The message is still being processed because there was a previous failure and the service is reattempting delivery.
- The message failed to be delivered to the destination:

    - Because the destination isn't reachable
    - Because the destination rejected the message
    - Because the message timed out during the delivery attempt
- The message was delivered to the destination but it was deleted before it was accessed (perhaps because it matched a rule).

To find out what happened:

[Run a message trace](run-a-message-trace-and-view-results). Use as many search criteria as possible to narrow down the results. For example, you should know the sender and the intended recipient or recipients of the message, and the general time period when the message was sent.

View the results, locate the message, and then view specific details about the message. See [View message trace results for messages less than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-less-than-7-days-old) or [View message trace results for messages more than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-more-than-7-days-old).

Look for a delivery status of **Failed** or **Pending** to explain why the message wasn't delivered. Confirm that the message was sent, that the service successfully received it, that it wasn't filtered, redirected, or sent for moderation, and that it didn't experience any delivery failures or delays. If the destination isn't reachable, you can use the **To IP** to help troubleshoot connectivity issues.

## Why is my message taking so long to arrive to its destination? Where is it in the pipeline?

Here are some possible reasons:

- The intended destination isn't responsive. This scenario is the most likely.
- It might be a large message that is taking a long time to process
- Latency in the service might be causing delays
- The message might have been blocked

To find out what happened:

[Run a message trace](run-a-message-trace-and-view-results#run-a-message-trace). Use as many search criteria as possible to narrow down the results. For example, you should know the sender and the intended recipient or recipients of the message, and the general time period when the message was sent.

View the results, locate the message, and then view specific details about the message. See [View message trace results for messages less than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-less-than-7-days-old) or [View message trace results for messages more than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-more-than-7-days-old).

The events section tells you why the message wasn't yet delivered. The timestamp information lets you follow the message through the messaging pipeline, and tell you how long the service takes to process each event. The event details inform you if the message being delivered is large or if the destination isn't responsive.

## Was a message marked as spam?

Messages can be marked as spam for several reasons. For example, the sending IP address might appear on one of the service's IP blocklists. A message can be marked as spam due to the content of the actual message, such as when it matches a rule in the spam content filter. The message trace tool only tracks spam content filter events; connection filter events (such as blocked IP addresses) aren't traceable. For more information about spam filtering, including spam content filtering, see [Anti-Spam Protection](/en-us/defender-office-365/anti-spam-protection-about).

To find out why a message was marked as spam:

[Run a message trace](run-a-message-trace-and-view-results#run-a-message-trace), locate the message in the results, and then view specific details about the message. See [View message trace results for messages less than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-less-than-7-days-old) or [View message trace results for messages more than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-more-than-7-days-old).

When anti-spam protection identifies a message as spam and sends it to the Junk Email folder or quarantine, the message has the status value **Delivered**. View the event details to see how the message arrived at its destination.

The details might identify the message as spam or high confidence spam, or indicate that an advanced spam filtering option matched. They also identify the action taken on the message. For example, the message was sent to quarantine, stamped with an X-header, or sent through the high risk delivery pool.

The spam confidence level (SCL) alone doesn't determine the cloud filtering verdict or action. For more information, see [Spam confidence level (SCL) in Microsoft 365](/en-us/defender-office-365/anti-spam-spam-confidence-level-scl-about).

## Was a message detected to contain malware?

Messages are detected as malware when its properties, either in the message body or in an attachment, match a malware definition in of one of the anti-malware engines. For more detailed information about malware filtering, see [Anti-malware protection](/en-us/defender-office-365/anti-malware-protection-about).

To find out why a message was detected to contain malware, [run a message trace](run-a-message-trace-and-view-results#run-a-message-trace). Use as many search criteria as possible to narrow down the results. Set the delivery status to **Failed**.

View the results, locate the message, and then view specific details about the message. See [View message trace results for messages less than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-less-than-7-days-old) or [View message trace results for messages more than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-more-than-7-days-old).

If the message wasn't yet delivered because it was determined to contain malware, this information is provided in the events section. For example, the following is a sample **Detail**: Malware: "*ZipBomb*" was detected in attachment *file*.*zip*. You're also informed of the action that occurred as a result of the message containing malware, for example if the entire message was blocked or if all attachments were deleted and replaced with an alert text file.

## Which mail flow rule (also known as a transport rule) or DLP policy was applied to a message?

To find out which mail flow rule (custom policy rule) or data loss prevention (DLP) policy (Exchange Online customers only) was applied to a message, [run a message trace](run-a-message-trace-and-view-results#run-a-message-trace). Use as many search criteria as possible to narrow down the results. Set the delivery status to **Failed**.

View the results, locate the message, and then view specific details about the message. See [View message trace results for messages less than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-less-than-7-days-old) or [View message trace results for messages more than seven days old](run-a-message-trace-and-view-results#view-message-trace-results-for-messages-more-than-7-days-old).

If the message wasn't delivered because the content matched a rule, the events section shows you the name of the mail flow rule. You're also informed of the action that occurred as a result of the mail flow rule match. For example the message was quarantined, rejected, redirected, sent for moderation, decrypted, or any number of other possible options. For information about how to create Exchange mail flow rules and set actions for them, see [Mail flow rules (transport rules) in Exchange Online](../../security-and-compliance/mail-flow-rules/mail-flow-rules).

## When I run a message trace, it returns rule ID-1. What does this mean?

Rule ID-1 is returned when the message trace comes across a mail flow rule that no longer exists. For example, the mail flow rule was modified or deleted after the original message was sent.

## Are there any known limitations or behavior clarifications that I should be aware of when using the message trace tool?

Be aware of the following issues when using the message trace tool:

- **IP-blocked messages**: Messages blocked by IP reputation block lists are included in the spam data for real time reports, but you can't perform a message trace on these messages.
- **Redirected messages**: If a recipient is rewritten by a mail flow rule or because the spam action for the domain is set to **Redirect to email address**, the message isn't traceable in a single search. The original message can be traced until to the point when the recipient is changed. After that, the message isn't traceable under the original recipient. You can trace the message again using the new recipient.
- **MAIL FROM**: The message trace tool uses the MAIL FROM value presented at the initiation of the SMTP conversation as the Sender in a search, regardless of what the DATA section of the message shows. The message might show a Reply-to address or different From: or Sender values. If the email message was sent by a process and not by an email client, there's an increased likelihood that the sender in the MAIL FROM doesn't match the sender in the actual message.
- **Mail flow rule updates**: When a message matches a mail flow rule, the rule ID is stored in the message trace and real time reporting databases. If you trace one of these messages or drill down on rule details in a report, the message trace and real time reporting user interfaces dynamically pull the current rule information from the hosted services network based on the rule ID in the reporting database. If you changed the attributes of that particular rule since the message was processed (for example, changed it from Reject to Allow), the rule ID stays the same in the message trace and real time reporting returned results, but the Exchange admin center shows the new mail flow rule properties. You can use the auditing reports feature in order to determine when the rule was changed and the properties that were changed.
- **Spam-filtered messages**: When the content filter marks a message as spam and sends it to the Junk Email folder or quarantine, it has the status value **Delivered**. Drill down to the event details to see how the message arrived at the destination.

## For more information

[Trace an email message](trace-an-email-message)