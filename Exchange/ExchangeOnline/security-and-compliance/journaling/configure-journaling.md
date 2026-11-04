---
layout: Conceptual
title: Configure Journaling in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/journaling/configure-journaling
Manager: laurawi
ms.subservice: exo-security-compliance
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn about the requirements for the journaling mailbox and the alternate journaling mailbox in Exchange Online.
ms.topic: article
author: k-reagle
ms.author: kreagle
ms.assetid: 3033715d-a6d0-485e-af0d-15876550fd4d
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-06-26T00:00:00.0000000Z
locale: en-us
document_id: 598506d9-01d0-fd2e-2600-9b5557e427f1
document_version_independent_id: 88fdfd05-dcde-4745-03f4-fb271a3c7094
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/journaling/configure-journaling.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/journaling/configure-journaling
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/journaling/configure-journaling.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 1d10a9c7-9428-2096-e445-2ccea99cddda
---

# Configure Journaling in Exchange Online | Microsoft Learn

Journaling is an older compliance feature of Exchange that allows you to meet your organization's archiving requirements when you must store emails outside Exchange Online.

You can create journal rules and have messages matching the rule's conditions delivered to the journaling address specified in the rule. For more information about journaling, including the limitations and considerations for using this older feature, see [Journaling in Exchange Online](journaling).

Here are two things you need to know before you start creating journal rules.

## Specify a journaling mailbox

A journaling mailbox is the mailbox or recipient that receives journal reports for messages that match a journal rule's conditions. You can specify different journaling mailboxes for different journal rules. For example, you can create a journal rule to journal messages sent or received by users in Europe and another one to journal messages sent or received by users in North America, and configures each rule to deliver journal reports to an address in their own geography. Or configure different journal rules for users in the Finance and Legal departments and similarly, have the journal reports delivered to different addresses.

Exchange Online doesn't support delivering journal reports to an Exchange Online mailbox. You must specify the email address of an on-premises archiving system or a third-party archiving service as the journaling mailbox.

Important

If you've configured a journaling rule to send the journal reports to a journaling mailbox that doesn't exist or is an invalid destination, the journal report remains in the transport queue on Microsoft datacenter servers; delivery of queued items is periodically retried. If this happens, Microsoft datacenter personnel will attempt to contact your organization and ask you to fix the problem so that the journal reports can be successfully delivered to a journaling mailbox. If you haven't resolved the issue after two days of being contacted, Microsoft will disable the problematic journaling rule.

## Specify an alternate journaling mailbox for undeliverable journal reports

As previously explained, undeliverable journal reports are queued on Microsoft datacenter servers and will be retried periodically until the MessageExpirationTimeout. After expiration, undeliverable journal reports can't be returned to the sender in a non-delivery report (also known as an NDR or bounce message) because the sender is the Exchange Online service. To handle the NDRs for undelivered journal reports, you must specify an alternate journaling mailbox that accepts the NDRs for all undeliverable journal reports. Like the journaling mailbox, the alternate journaling mailbox can't be an Exchange Online mailbox.

![Select an alternative journaling mailbox to receive NDRs for undeliverable journal reports.](../../exchangeonline/media/23408455-a7d2-454b-8375-45be81563c36.png)

The original journal report is an attachment in the NDR. When the journaling mailbox for an undelivered journal report becomes available again, you can use the **Send Again** feature in Outlook on the NDRs in the alternate journaling mailbox to send the unaltered delivery report to the journaling mailbox.

![use the Send Again feature in Outlook on the NDRs in the alternate journaling mailbox.](../../exchangeonline/media/f0101a6f-280a-41a8-84c2-a5718fd1ab9c.png)