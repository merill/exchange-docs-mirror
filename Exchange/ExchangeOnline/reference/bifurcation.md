---
layout: Conceptual
title: Bifurcation and its technicalities with implications | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/bifurcation
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
author: v-smandalika
ms.author: serdars
ms.reviewer: 
description: Learn about bifurcation and its technicalities, and about the implications when bifurcation occurs.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid: 
audience: Admin
f1.keywords: 
ms.custom: 
ms.service: exchange-online
ms.localizationpriority: high
ms.date: 2022-10-03T00:00:00.0000000Z
locale: en-us
document_id: 3d15f63d-152f-04bb-127d-cc994338fff9
document_version_independent_id: 3893f783-9474-1a59-b976-2b14144501b8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/bifurcation.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/bifurcation
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/bifurcation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/390894b2-8646-4f7e-b8cd-2209156272a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12b23b77-ab37-4318-a036-4f6690586386
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: c6567e62-1fc2-b1f4-bc47-4137b557c4cd
---

# Bifurcation and its technicalities with implications | Microsoft Learn

Bifurcation (also known as forking) refers to the process of creating multiple copies of a given message. All these copies will have the same message content, but different envelopes.

Bifurcation occurs through Microsoft Exchange while messages are in transit.

## Why bifurcation?

There are different purposes for which bifurcation can occur to a message in transit, such as (including but not limited) recipient-based customization, routing, security, and performance.

### Recipient-based customization

Bifurcation enables customization of the message based on the recipient. Specifically, the need for the occurrence of bifurcation to customize the message is created by the following scenarios:

- **When policies apply to a subset of the recipients**: For example, if a policy is in place to add a disclaimer to messages sent to external recipients, Exchange will bifurcate the message, resulting in:
    - One copy for the internal recipients with the original message content, and
    - A second copy for the external recipients with the modified content and disclaimer.
- **When recipients require different message settings**: Exchange will bifurcate a message when the **read receipts** setting is enabled for some recipients and blocked for others.
- **When the message sender in MAIL FROM in the message envelope is updated**: For example, a message is sent to a user and a distribution group. In such a case, if the group has been configured to not report non-delivery reports (NDRs), the message needs to be bifurcated since the copy sent to the group will have the envelope sender (**MAIL FROM:**) set to **&lt;&gt;** (the null reverse path) to suppress NDRs.
- When auto-response messages [for example, delivery status notifications (DSNs), out of office (OOF) messages, and recall reports] need to be suppressed.
- When alternative recipients are expanded.
- **When a "Resent-From:" header field is added to the message header**. Resent header fields are informational header fields that can be used to determine whether a message has been forwarded by a user. Resent header fields make the message appear to the recipient in such a way that it was sent directly by the original sender. The recipient can view the message header to discover who forwarded the message. Resent header fields are defined in section 3.6.6 of RFC 5322.
- When the expansion history of the group needs to be transmitted.

### Routing

Bifurcation enables routing, and the need for the occurrence of bifurcation to route the message is created by the following scenarios:

- When mail flow rules (also known as Transport Rules) are applicable to only a subset of recipients.
- When the recipients have different next hop domains.

### Security

Features such as anti-spam and other security-related ones might perform forking for security and threat protection purposes.

### Performance

Bifurcation facilitates good performance, and the need for the occurrence of bifurcation to optimize performance is created by the following scenario:

- **To limit the number of envelope recipients in a single message**: Expanding large groups can generate thousands of individual recipients. Instead of creating a single copy of the message that has thousands of envelope recipients, Exchange creates multiple copies of the same message, which have a limited number of recipients in the message envelope.

## What are the implications of bifurcation?

Bifurcation can impact the way some of our Exchange features work, and therefore it's important to understand how this impact can change some of their behavior.

A few implications of the occurrence of bifurcation are described in the following table:

| It can affect | How? |
| --- | --- |
| Mail flow rules (also known as Transport Rules) | Rule conditions (or exceptions) that are met/fulfilled by the original message might not be met/fulfilled by some of the forks. Rule actions will be executed independently for all the forks (for example, generating a notification or incident report for each copy of the message). |
| Moderation | Each copy of the message will result in a separate approval request. |
| Journaling | Multiple copies of a message will be archived, leading to increased storage costs. |
| Data Loss Prevention (DLP) Policies | Policies that might have applied to the original message might no longer apply to some of the forks. Rule actions will be executed independently for all the forks (for example, generating a notification or incident report for each copy of the message). |