---
layout: Conceptual
title: Trace an email message in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/trace-an-email-message/trace-an-email-message
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
description: Sometimes an email message gets lost in transit, or it can take a lot longer than expected for delivery, and your users can wonder what happened. As an administrator, you can use the message trace feature to follow messages as they pass through your cloud email service. With message tracing, you can determine whether a targeted email message was received, rejected, deferred, or delivered by the service. It also shows what events have occurred to the message before reaching its final status. Getting detailed information about a specific message lets you efficiently answer your user's questions, troubleshoot mail flow issues, validate policy changes, and alleviates the need to contact technical support for assistance.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 0c83cde6-5b09-4106-8587-c200cdc59094
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 1175d954-24d6-3bd7-b083-1a383ece1c5a
document_version_independent_id: 0598b95d-18ad-7d48-8cc2-53d6e380366f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/trace-an-email-message/trace-an-email-message.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/trace-an-email-message/trace-an-email-message
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/trace-an-email-message/trace-an-email-message.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: f42d6463-ced8-6efe-40ec-2560aee886ff
---

# Trace an email message in Exchange Online | Microsoft Learn

Sometimes an email message gets lost in transit, or it can take a lot longer than expected for delivery, and your users can wonder what happened. As an administrator, you can use the message trace feature to follow messages as they pass through your cloud email service. With message trace, you can determine whether a targeted email message was received, rejected, deferred, or delivered by the service. It also shows what events have occurred to the message before reaching its final status. Getting detailed information about a specific message lets you efficiently answer your user's questions, troubleshoot mail flow issues, validate policy changes, and alleviates the need to contact technical support for assistance.

Tip

For troubleshooting general issues and trends, use the **Reports** page in the Microsoft Defender portal (https://security.microsoft.com/emailandcollabreport). For single point specifics where details are needed about a message, use the message trace tool.

The following topics describe how to run a message trace to narrow down your search criteria, how to view message trace results, and how to view details about a specific message:

- [Run a message trace in the classic EAC](run-a-message-trace-and-view-results)
- [Message trace in the modern EAC](message-trace-modern-eac)

Note

The **Exchange message trace** link in the Microsoft Defender portal opens message trace in the modern EAC.

The [Message Trace FAQ](message-trace-faq) topic presents common messaging questions that arise and how to best answer these questions using the message trace tool.