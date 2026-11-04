---
layout: Conceptual
title: Completion of migration batch in EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/completion-gspace-migration-batch-neweac
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: AshaIyengar21
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Instructions for completion of migration batch in EAC.
ms.custom: seo-marvel-jun2021
ms.date: 2021-07-13T00:00:00.0000000Z
locale: en-us
document_id: 4b1a5264-f3cb-dbce-1f05-3e52861aa661
document_version_independent_id: 76938add-7d50-2c96-9ed0-64da36e3d015
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/completion-gspace-migration-batch-neweac.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/completion-gspace-migration-batch-neweac
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/completion-gspace-migration-batch-neweac.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: 1cc9275c-a9aa-708a-c5f1-1c9175154a67
---

# Completion of migration batch in EAC in Exchange Online | Microsoft Learn

In EAC, when the migration batch has reached the state of **Synced**, it needs to be completed.

Note

When the batch starts, all the users to be migrated will be converted from MailUsers to Mailboxes. The Microsoft 365 or Office 365 Exchange license must be assigned only after this moment. You have 30 days to assign the license

To complete the batch in the Exchange admin center:

1. Go to **Migration**, and select the migration batch.
2. Click **Complete migration batch**
3. In the **Details** pane on the right, click **Confirm** to begin the completion of the migration batch.

The batch status will then be **Completed**.

During completion, another incremental sync is run to copy any changes that have been made to the Google Workspace mailbox. Additionally, during completion, the forwarding address that routes mail from Microsoft 365 or Office 365 to Google Workspace is removed, and a forwarding address that routes mail from Google Workspace to Microsoft 365 or Office 365 is added. This ensures that any messages received by migrated users at their Google Workspace mailboxes will be sent to their new Microsoft 365 or Office 365 address. Similarly, if any user who hasn't yet been migrated receives a message at their Microsoft 365 or Office 365 address, the message gets routed to their Google Workspace mailbox.