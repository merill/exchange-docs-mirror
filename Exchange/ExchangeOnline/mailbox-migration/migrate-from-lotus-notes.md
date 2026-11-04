---
layout: Conceptual
title: Migrate from Lotus Notes to Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrate-from-lotus-notes
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.topic: upgrade-and-migration-article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 9a2909e3-c185-4217-94e3-806809147cb3
ms.reviewer: 
description: Use the tool MONTI to plan your migration from Lotus Notes to Microsoft 365 or Office 365.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: ce990e27-aa35-1c80-2d57-c07df2d35e88
document_version_independent_id: 78594f8e-6f98-21bd-4c68-be4facfade3e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrate-from-lotus-notes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrate-from-lotus-notes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrate-from-lotus-notes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 86de7f30-5416-0da0-e214-6166b75ac6a0
---

# Migrate from Lotus Notes to Microsoft 365 or Office 365 | Microsoft Learn

When planning to migrate email from IBM Lotus Notes to Microsoft 365 or Office 365, use the **Microsoft Online Notes Inspector (MONTI)** application. This tool will assist you in evaluating the amount data to be migrated from a customer's Lotus Notes environment to Microsoft 365 or Office 365.

Here's what MONTI does:

- It processes mail files to determine the total database size, document count (calendar, contacts, groups, mail, and tasks), and size by days.
- It processes Mail-In Databases to determine the total database size, and Size by Days.
- It posts results under the People, Mail-In Databases, and Logs views. You can create these reports manually or on a scheduled basis.

Download the [MONTI application and accompanying documentation](https://www.microsoft.com/download/details.aspx?id=29567) from the Microsoft Download Center.

To directly download only the application: [MONTI application](https://download.microsoft.com/download/F/F/D/FFD6C34A-C9DB-4BE5-8504-2F912AB820C3/MONTI.exe.)

The documentation describes how to deploy, configure, and run the MONTI application in a customer's Domino environment.