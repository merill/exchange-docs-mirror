---
layout: Conceptual
title: Outlook on the web in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/outlook-on-the-web
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: A basic overview of Outlook on the web in Exchange Online.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: c30ff7b8-0f12-455b-a70e-3447634f17ce
ms.reviewer: serdars
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2023-10-31T00:00:00.0000000Z
locale: en-us
document_id: 981a7447-0bb9-0c4b-f5bd-87e4aab6470c
document_version_independent_id: 8477e6fb-c0d6-4b18-b4ca-7477f655c861
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/outlook-on-the-web.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-on-the-web/outlook-on-the-web
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/outlook-on-the-web.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: edbe4ccf-9e63-4729-7a7e-9b8c7a99f803
---

# Outlook on the web in Exchange Online | Microsoft Learn

By default, Outlook on the web (formerly known as Outlook Web App) is enabled in Exchange Online, and lets users access their mailbox from almost any web browser.

For information about client access mailbox methods in Exchange Online, see [Clients and mobile in Exchange Online](../clients-and-mobile-in-exchange-online).

## Overview of Outlook on the web

Fully supported web browsers give users access to features such as conversation view, Inbox rules, the reading pane, and the Scheduling Assistant. Browsers that aren't fully supported can still be used, but users will see the light version of Outlook on the web, which has fewer features.

## Managing Outlook on the web

In Exchange Online, the most common Outlook on the web management tasks can be accomplished in the Exchange admin center (EAC). All these tasks, and many others, can be accomplished by using Exchange Online PowerShell.

## Outlook on the web mailbox policies in Exchange Online

In Exchange Online, Outlook on the web mailbox policies control the availability of settings and features in Outlook on the web (formerly known as Outlook Web App). A mailbox can only have one Outlook on the web mailbox policy applied to it. You can create different policies for different types of users in your Exchange Online organization.

Every Exchange Online organization has a default Outlook on the web mailbox policy named OwaMailboxPolicy-Default that's applied to all user mailboxes. You can use this policy or create additional policies as necessary to meet the needs of your organization.

For the procedures that you can do on Outlook on the web mailbox policies, see [Outlook on the web mailbox policy procedures in Exchange Online](/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/outlook-on-the-web).

Note

**All mailbox policies set for Outlook on the web will also affect new Outlook for Windows**.