---
layout: Conceptual
title: Continuous error throttling for SMTP AUTH submissions  in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/continuous-error-throttling-smtp-auth-submissions
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.topic: article
author: Benny-54
ms.author: serdars
ms.reviewer: 
description: Learn how handle errors in for LOB applications and services that customers have configured to send out automated emails.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid: 
audience: Admin
f1.keywords: 
ms.custom: 
ms.service: exchange-online
ms.localizationpriority: high
ms.date: 2021-07-22T00:00:00.0000000Z
locale: en-us
document_id: 3d934181-40b4-fbae-2fc7-40a22c82b593
document_version_independent_id: e02c45b3-9029-b473-2604-6a7ba1288b27
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/continuous-error-throttling-smtp-auth-submissions.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/continuous-error-throttling-smtp-auth-submissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/continuous-error-throttling-smtp-auth-submissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 9ff53ad3-551a-a71c-80b3-9500ec2f925a
---

# Continuous error throttling for SMTP AUTH submissions  in Exchange Online | Microsoft Learn

Every day, our service sees millions of requests coming in to send emails via smtp.office365.com using the SMTP AUTH protocol. Many of these are for Line-of-Business (LOB) applications and services that customers have configured to send out automated emails.

Many of these requests that we receive, result in an error which if sent by a user from Outlook can result in the user seeing an error message that they could immediately take action on to unblock sending emails. However, many automated email applications aren't designed well to handle errors. On the contrary, they ignore errors and send continuously believing that the error will correct itself.

For some errors such as those involving **Send As** or **Mailbox Full**, the issue won't correct itself without human intervention. To protect our service from bombardment from these requests and to get the message to administrators that something is wrong with the mailbox or configuration, we're introducing continuous error throttling for SMTP AUTH.

The new errors that are seen if throttling is hit are:

- 550 5.2.251 Sender throttled due to continuous mailbox full errors.
- 550 5.2.252 Sender throttled due to continuous send as denied errors.
- 550 5.2.253 Sender throttled due to continuous invalid license errors.
- 550 5.2.254 Sender throttled due to continuous too many recipients errors.
- 550 5.2.255 Sender throttled due to continuous invalid recipients errors.

If Exchange Online sees too many errors during submissions for a mailbox related to the five issues covered, that mailbox is throttled from sending using SMTP AUTH specifically for a period of time.

In many of these cases, customers might fail to notice that anything is wrong and the forgotten application will continue trying to send to no avail. However, the mailbox could be configured to send out emails successfully with one application and misconfigured with another. In such a scenario, messages that were successfully sent will be blocked as well. Lastly, if a mailbox is left to reach its size limit, a previously working application hits this new error and be throttled if it's ignored.

It's up to administrators or users to test these applications to make sure that they work when configured. If and when these errors are hit, they need to investigate the misconfiguration in cases such as **Send As** denied or correct new issues such as a mailbox becoming full. Investigating this is on the client side. These messages aren't accepted by Microsoft 365 so **Message Trace** is of no help here.

After correcting the issue, the mailbox will begin working again after the throttling period expires in the same way that hitting the Recipient Rate Limit for a mailbox requires waiting for that throttling to elapse. The throttling period will be decided by Microsoft based on many factors.

If customers don't want to wait that long, they can switch to using another mailbox as long as the issue has been resolved. Support is unable to lift the throttling here.