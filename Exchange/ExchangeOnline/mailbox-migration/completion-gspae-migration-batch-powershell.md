---
layout: Conceptual
title: Completion of migration batch in Exchange Online PowerShell | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/completion-gspae-migration-batch-powershell
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
description: Instructions for completion of migration batch in PowerShell.
ms.custom: seo-marvel-jun2021
ms.date: 2021-07-13T00:00:00.0000000Z
locale: en-us
document_id: cfb88594-a087-cde6-b968-55440d07d904
document_version_independent_id: 732188ed-1256-8214-25d1-e0f7c47ec0e2
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/completion-gspae-migration-batch-powershell.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/completion-gspae-migration-batch-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/completion-gspae-migration-batch-powershell.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: 894f6fcf-fd0f-2d09-24eb-3754f683ad58
---

# Completion of migration batch in Exchange Online PowerShell | Microsoft Learn

In PowerShell, when the migration batch has reached the state of **Synced**, it needs to be completed by running the `Complete-MigrationBatch` cmdlet.

Note

When the batch starts, all the users to be migrated will be converted from MailUsers to Mailboxes. The Microsoft 365 or Office 365 Exchange license must be assigned only after this moment. You have 30 days to assign the license.

During completion, another incremental sync is run to copy any changes that have been made to the Google Workspace mailbox. Additionally, the forwarding address that routes mail from Office 365 to Google Workspace is removed, and a forwarding address that routes mail from Google Workspace to Office 365 is added.

Note

Forwarding addresses are not needed when doing a cutover migration from Google Workspace to Exchange Online.