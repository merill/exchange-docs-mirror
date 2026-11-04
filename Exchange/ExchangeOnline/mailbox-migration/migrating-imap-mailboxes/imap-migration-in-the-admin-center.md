---
layout: Conceptual
title: IMAP migration in the Microsoft 365 admin center | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/imap-migration-in-the-admin-center
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
ms.assetid: 4682f2e4-f720-4868-91ab-207f5b0c325d
ms.reviewer: tonymathew
description: Learn how to perform an IMAP migration in the Admin Center preview.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MED150
- MBS150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom:
- Adm_O365
- Adm_O365_Setup
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: 2ed16f16-09d6-ad84-7c01-50ef9232ced9
document_version_independent_id: e794838b-02fa-9dce-d7bb-f05c6145f047
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/imap-migration-in-the-admin-center.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrating-imap-mailboxes/imap-migration-in-the-admin-center
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/imap-migration-in-the-admin-center.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: e0b88afe-9d62-b856-f47b-2731a1ccfaa7
---

# IMAP migration in the Microsoft 365 admin center | Microsoft Learn

After you've added your users to Microsoft 365 or Office 365, you can use Internet Message Access Protocol (IMAP) to migrate email for those users from their IMAP-enabled email servers.

Important

Before you can use an IMAP migration for your users, they must have been first added to your Microsoft 365 or Office 365 organization. For instructions, see [Add users individually or in bulk](/en-us/microsoft-365/admin/add-users/add-users).

Before you migrate, read [What you need to know about migrating your IMAP mailboxes to Microsoft 365 or Office 365](migrating-imap-mailboxes).

Important

IMAP migration in the Microsoft 365 admin center has been replaced by IMAP migration by using the Exchange admin center (EAC). To perform an IMAP migration by using the EAC, see [Migrate other types of IMAP mailboxes to Microsoft 365 or Office 365](migrate-other-types-of-imap-mailboxes).

To migrate Exchange mail to Microsoft 365 or Office 365, see [Use express migration to migrate Exchange mailboxes to Microsoft 365 or Office 365](../use-minimal-hybrid-to-quickly-migrate)