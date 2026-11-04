---
layout: Conceptual
title: Completion of migration batch in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/completion-gspace-migration-batch
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
description: Overview to completion of migration batch
ms.custom: seo-marvel-jun2021
ms.date: 2021-07-13T00:00:00.0000000Z
locale: en-us
document_id: 1cc48705-e64b-5df4-b40e-d0096b858342
document_version_independent_id: 9f537fbd-cdc9-1e72-53fa-ef52a6a0dc4f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/completion-gspace-migration-batch.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/completion-gspace-migration-batch
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/completion-gspace-migration-batch.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: fef2f8e0-ea61-2152-a2d3-790040b85380
---

# Completion of migration batch in Exchange Online | Microsoft Learn

Based on whether you're using EAC, or PowerShell cmdlets to perform the migration, the completion process differs.

## Finalizing your migration

After you have successfully migrated all of your Google Workspace users to Microsoft 365 or Office 365, you can switch your primary MX record to point to Microsoft 365 or Office 365. The update to the MX record propagates slowly, taking up to the length of time in the record's previous TTL (time to live). At this point, you're free to decommission your source Google Workspace tenant.