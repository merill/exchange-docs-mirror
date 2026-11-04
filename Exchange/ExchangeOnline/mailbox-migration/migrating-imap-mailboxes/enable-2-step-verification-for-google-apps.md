---
layout: Conceptual
title: Enable 2-step verification for your Google apps users in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/enable-2-step-verification-for-google-apps
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
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 4c70c606-5e95-4cf7-abce-cf85f1ac4179
ms.reviewer: tonymathew
description: If you want to migrate email for your Google app users to Microsoft 365 or Office 365, the users need to create an app password that you use together with their Google apps password to connect to their Gmail. Before they can create an app password, you have to allow them to turn on two-step verification in the Google Admin console.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MBS150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: a437a2a0-990b-ac03-40f1-3d15797d70a3
document_version_independent_id: bcebb73e-7960-32ca-e964-a6c30e25ea25
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/enable-2-step-verification-for-google-apps.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrating-imap-mailboxes/enable-2-step-verification-for-google-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/enable-2-step-verification-for-google-apps.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 36d82908-9273-d58f-929a-2c8289a5ac76
---

# Enable 2-step verification for your Google apps users in Exchange Online | Microsoft Learn

If you want to migrate email for your Google app users to Microsoft 365 or Office 365, the users need to create an app password that you use together with their Google apps password to connect to their Gmail. Before they can create an app password, you have to allow them to turn on two-step verification in the Google Admin console.

## Enable two-step verification

In order for your users to create an app password, they have to first enable two-step verification.

**To enable two-step verification for your Google apps domain**

1. Sign in to the Google Admin console.
2. On the console, choose **Security**.

    ![In the Google Admin console choose Security.](../../exchangeonline/mailbox-migration/media/f0c0536d-527c-419d-b0c8-02e452fb4b4d.png)
3. On the **Security** page, choose **Basic settings**.

    ![On the Security page choose Basic settings.](../../exchangeonline/mailbox-migration/media/ff1dd30f-6e45-43ca-9fd0-ed7de9e12131.png)

    And then check the check-box next to **Allow users to turn on 2-step verification**.

    ![Check Allow users to turn on 2-step verification.](../../exchangeonline/mailbox-migration/media/e7870fee-90c5-47c8-8428-4130bf4c951c.png)
4. Your users can now turn on two-step verification and create an app password as described here: [Prepare your Gmail account for connecting to Outlook and Microsoft 365 or Office 365](prepare-gmail-or-g-suite-accounts).