---
layout: Conceptual
title: Simplified Gmail Migration (SGM) for Small and Medium Businesses | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/custom-migration-small-business-from-gmail
Manager: jtremper
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Documentation for small business admins looking to migrate their email from Google Gmail to Exchange Online.
author: MicrosoftHeidi
ms.author: heidip
ms.date: 2024-09-03T00:00:00.0000000Z
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: Medium
ms.collection: 
ms.reviewer: tonymathew
search.appverid: MET150
f1.keywords: 
audience: ITAdmin
locale: en-us
document_id: 4d5f063e-f0af-3316-829d-a24a8c52fe75
document_version_independent_id: e789d634-ac4f-b9bf-4d9e-15bb5a5275a9
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/custom-migration-small-business-from-gmail.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/custom-migration-small-business-from-gmail
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/custom-migration-small-business-from-gmail.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 5c5eeb84-ad58-1549-be77-d732177bf00f
---

# Simplified Gmail Migration (SGM) for Small and Medium Businesses | Microsoft Learn

Note

This feature isn't available worldwide. We're waiting for Google verification of the Google Marketplace app **Microsoft 365 Mail Migration**. The estimated time for worldwide launch is late October 2024.

## Introduction

Microsoft offers first-party solutions for migration of Google Workspace (**GWS**) email into Microsoft 365 Exchange Online (**EXO**). This solution was called *Classic Gmail Migration* (**CGM**) and was available for tenants in the Exchange Admin Center (**EAC**) from 2018 and Microsoft 365 Admin Center (**MAC**) from mid-2023. However, this solution is extensive in setup and solutions and is aimed at tenant admins who are IT professionals. The Microsoft 365 Exchange Online migration team is enhancing the CGM capabilities to additionally focus on admins at small and medium-sized businesses in the early stages of performing Exchange administration work. It's called *Simplified Gmail Migration* (**SGM**), and is only available in MAC. This document explains the features of this SGM solution, which makes migration from GWS mail to EXO a seamless experience.

Note

You (tenant admin) can experience this new SGM solution only if your total mailbox count on GWS source side is **&lt;=1000**. If your total mailbox count on source side is &gt; 1000, the solution routes you to CGM.

## Simplified Gmail Migration (SGM)

With SGM in MAC, a tenant admin looking to migrate from GWS are routed to an experience where the migration of all workloads – GWS Mail to EXO, GWS Drive to OneDrive and Sharepoint (**ODSP**), and so on, is centralized. The tenant admin can kick off Mail/Exchange migrations or Drive/ODSP from this centralized /consolidated dashboard.

When you (the tenant admin) begin the mail migration from the consolidated GWS dashboard in MAC, you see these steps:

1. Log in to Google using migration admin credentials.
2. Using your Google credentials, SGM reads information on the number of mailboxes for the tenant on the Google side. If the total mailbox count is &lt;=1000, you're guided to the SGM flow. If your total mailbox count is &gt;1000, you're guided to the CGM flow. The following steps are only applicable for the SGM flow.
3. Install a Google marketplace app custom built for GWS mail migrations, called "Microsoft 365 Mail Migration". See the details of the app [at this link](google-marketplace-app-migration).
4. The app performa the set-up tasks required in the Google Admin console (as opposed to CGM, where most of it was done manually).
5. When completed, the app directs you back to the MAC.
6. You need to confirm your Google credentials again to make sure access and permissions are in order.
7. Now you can see the results of the source scan showing a list of mailboxes and their sizes.
8. At this point, you can choose mailboxes (one, many, or all) to migrate from GWS to EXO.
9. Now you see two different workflows – one to migrate regular sized mailboxes, and other to migrate large mailboxes (&gt;80 GB).
10. In each of the workflows, can select the:
    - duration of data (all or from a date range).
    - type of data (mail, calendar, contacts, rules, permissions, delegates).
    - labels/folders you want to migrate.
11. Once the migration of all mailboxes is done, mark the completion of migration by choosing the option **Complete Migration** in the experience. This option is available to you only when the migration of all mailboxes is done.
12. Now you're asked to change your DNS entries in your DNS registrar to direct all new emails to EXO.
13. You're also asked to confirm that your DNS registrar entries are changed.
14. View your migrated data in Outlook.

Important

Since the DNS entry change propagation can take anywhere between a minute to 72 hours depending on your DNS registrar, the SGM solution keeps syncing new emails landing in GWS for 72 hours following your confirmation of DNS change.