---
layout: Conceptual
title: Microsoft 365 Mail migration app in Google Marketplace | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/google-marketplace-app-migration
Manager: jtremper
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Documentation regarding the Google Marketplace app that helps with the migration of mailboxes into Microsoft 365.
author: MicrosoftHeidi
ms.author: heidip
ms.date: 2024-08-01T00:00:00.0000000Z
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: Medium
ms.collection: 
ms.reviewer: tonymathew
search.appverid: MET150
f1.keywords: 
audience: ITAdmin
locale: en-us
document_id: d55c5f5c-a995-58b6-2d16-5a90fd4ff7ae
document_version_independent_id: 96ce0ffa-b48b-590a-254f-4bea361de710
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/google-marketplace-app-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/google-marketplace-app-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/google-marketplace-app-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 6347c52d-64e3-3fef-58c7-58e5c746770f
---

# Microsoft 365 Mail migration app in Google Marketplace | Microsoft Learn

## Introduction

Microsoft 365 Exchange Online migration is launching a Google Workspace (**GWS**) mailbox to Exchange Online (**EXO**) mail migration solution called Simplified Gmail Migration (**SGM**) in the Microsoft 365 Admin Center (**MAC**). This new solution enables admins at small and medium-sized businesses in the early stages of performing Exchange administration responsibilities to complete mail migration for their organization.

To make the migration from GWS mail to EXO a seamless experience, we're introducing a Google marketplace app called **Microsoft 365 Mail Migration**. This article explains the purpose and the details of the app, and also provides you a link to the SGM solution in MAC.

Note

To install this app in your Google Admin console, you need administrator privileges.

## Purpose

When you, the tenant admin in charge of migration, log into the MAC, you can start your SGM experience from the [Google Workspace Migration page](https://admin.microsoft.com/Adminportal/Home#/featureexplorer/migration/GoogleMigration).

You need to log in to the Google Admin Console using your admin credentials. The experience then guides you to install the Microsoft 365 Mail Migration app from the Google marketplace in your Google Admin Console.

By installing the app, you're granting the following permissions via the respective APIs:

| Purpose | API |
| --- | --- |
| Get primary domain when creating migration endpoint | https://www.googleapis.com/auth/admin.directory.customer.readonly |
| Get tenant user count | https://www.googleapis.com/auth/admin.reports.usage.readonly |
| Get ID token | https://www.googleapis.com/auth/userinfo.email |
| Scan tenant users | https://www.googleapis.com/auth/admin.directory.resource.calendar.readonly |
| Migrate Contacts | https://www.googleapis.com/auth/contacts |
| Migrate Tasks | https://www.googleapis.com/auth/tasks.readonly |
| Migrate Calendar | https://www.googleapis.com/auth/calendar |
| Migrate Gmail | https://www.googleapis.com/auth/gmail.settings.sharinghttps://www.googleapis.com/auth/userinfo.email[https://www.googleapis.com/auth/userinfo.profile]https://www.googleapis.com/auth/userinfo.profilehttps://mail.google.com/ |

The app includes an OAuth2 client and a service account. The OAuth2 client is used to do Google OAuth and the service account is used for migration purposes. The app will create a migration endpoint, and query the GWS primary domain to scan and present tenant user and resource information. With the permissions mentioned in this article being granted, the service account will sync the user's data of your selection from GWS to EXO. In this experience, you choose the data (Mail, Calendar, Contacts, Tasks, Rules, Permissions, and Delegates) as well as the duration (all or between date ranges) you want to migrate for each user.

Important

The app does **not** modify or delete your data from GWS mail, calendar, contacts, or tasks.

## Ready to migrate your GWS mailboxes to Microsoft 365 Exchange?

When you're ready to migrate, start your migration from the consolidated [Google Workspace Migration page](https://admin.microsoft.com/Adminportal/Home#/featureexplorer/migration/GoogleMigration), where you can migrate not only your GWS mailboxes but your GWS Drive contents as well.

Important

See the Microsoft privacy assurance for enterprise solutions in this article: [Privacy & Data Management Overview](/en-us/compliance/assurance/assurance-privacy).