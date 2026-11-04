---
layout: Conceptual
title: Sharing policies in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/sharing-policies/sharing-policies
Manager: dansimp
ms.subservice: sharing
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: People in your organization may want to share calendars with individual business associates, friends, or family members. Sharing policies control how your users share their calendars with people outside your organization. The sharing policy that an admin applies to the user's mailbox determines what level of access a user can share and with whom. If you don't change anything, then all users can invite anyone with an email address to view their calendar. You may decide to apply a more restrictive policy.
ms.topic: article
author: navanethan-msft
ms.author: nagangat
ms.assetid: a4f9c56a-cb9b-401b-9b45-d71c6e036871
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-26T00:00:00.0000000Z
locale: en-us
document_id: 7ff83223-f09a-7e1a-8c44-d0f8dee5df54
document_version_independent_id: bdbb368f-1254-75ce-26b3-e3e17779142b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/sharing-policies/sharing-policies.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/sharing-policies/sharing-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/sharing-policies/sharing-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: def522c6-7cfe-7c25-e2a5-2033c2a66a3e
---

# Sharing policies in Exchange Online | Microsoft Learn

People in your organization may want to share calendars with individual business associates, friends, or family members. Sharing policies control how your users share their calendars with people outside your organization. The sharing policy that an admin applies to the user's mailbox determines what level of access a user can share and with whom. If you don't change anything, then all users can invite anyone with an email address to view their calendar. You may decide to apply a more restrictive policy.

Note

Organization Sharing functionality of the Classic Exchange admin center experience is available in the new Exchange admin center as we continue to work on updated versions. If you're using **Edge** incognito and this page isn't working, enable the [third-party cookies](https://support.microsoft.com/microsoft-edge/temporarily-allow-cookies-and-site-data-in-microsoft-edge-597f04f2-c0ce-f08c-7c2b-541086362bd2).

An admin defines the rules that make up a sharing policy. You can specify the domains that users can share with, and the following levels of access to calendars:

- Free/busy information with time only
- Free/busy information with time, subject, and location
- Free/busy information, including time, subject, location, and title

After you create a new sharing policy, you have to apply that policy to mailboxes before it takes effect. Sharing policies are applied to individual user's mailboxes. An admin can also disable a user's sharing policy to prevent external access to calendars.

Users share their calendar by sending an email invitation to the external user. Outlook 2010 or later or Outlook on the web (formerly known as Outlook Web App) users can send this type of invitation. The calendar can be opened through a URL link, or can be accessed as an additional calendar folder if the external user has Outlook 2010 or later or is using Outlook on the web.

These articles will help you learn how to manage sharing policies for your Microsoft 365 or Office 365 organization:

[Create a sharing policy in Exchange Online](create-a-sharing-policy)

[Apply a sharing policy to mailboxes in Exchange Online](apply-a-sharing-policy)

[Modify, disable, or remove a sharing policy in Exchange Online](modify-a-sharing-policy)