---
layout: Conceptual
title: Behavior of retention tags and retention labels when items are moved to the Deleted Items folder in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/retention-deleted-items
Manager: robertoyms
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.topic: reference
author: brenle
ms.author: brenle
ms.reviewer: 
description: Learn about the behavior of retention tags and retention labels when items are moved to the Deleted Items folder.
ms.collection:
- exchange-online
- tier3
search.appverid: 
audience: Admin
f1.keywords: 
ms.custom: 
ms.service: exchange-online
ms.localizationpriority: medium
ms.date: 2023-07-14T00:00:00.0000000Z
locale: en-us
document_id: 5cf81ad4-880e-ccd7-a70d-ecd034fa1f03
document_version_independent_id: 6ccf3b5d-5486-1457-b8a5-ad44a68818d3
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/retention-deleted-items.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/retention-deleted-items
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/retention-deleted-items.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: 380b1662-2190-4c94-d3bd-27d1b9646034
---

# Behavior of retention tags and retention labels when items are moved to the Deleted Items folder in Exchange Online | Microsoft Learn

Use this article to understand the behavior of Exchange Online email items when they're moved to the Deleted Items folder and retention tags from [messaging records management (MRM)](/en-us/exchange/security-and-compliance/messaging-records-management/messaging-records-management) or [retention labels from Microsoft Purview](/en-us/purview/retention#retention-labels) are used for compliance requirements.

There was a change of behavior in June 2023 that completes rollout in August 2023 for items with retention tags or retention labels that are moved to the Deleted Items folder and either of the following scenarios apply:

- A retention tag or retention label was originally inherited from a parent folder
- A retention label was [autoapplied](/en-us/purview/apply-retention-labels-automatically)

These items with a retention tag or retention label applied in the ways listed are affected when moved to the Deleted Items folder by drag & drop or manual deletion.

Note

This change doesn't affect the behavior for items that are permanently deleted by a user (for example, using SHIFT+DEL), items that have no retention labels applied, or items that have a retention label or retention tag manually applied by a user. It also doesn't affect the behaviors of any other folders within the mailbox.

Before the change for the listed scenarios:

- A retention label or retention tag that was inherited from a parent folder isn't persisted when the item is moved to the Deleted Items folder.
- A retention label that was autoapplied is replaced with a retention policy tag (RPT) if one exists, after the item is moved to the Deleted Items folder.

After the change for the listed scenarios, the Deleted Items folder honors the [principles of retention](/en-us/purview/retention#the-principles-of-retention-or-what-takes-precedence). This means:

- Any retention label, regardless of how it's applied, remains applied to the item and is enforced if its settings are configured to retain the item when it's moved to the Deleted Items folder, even if the Deleted Items folder has a retention policy tag (RPT) applied.
- When the Deleted Items folder doesn't have a retention policy tag (RPT) applied, any retention label or retention tag, regardless of how it's applied, remains applied to the item and is enforced.
- For retention labels or retention tags that are configured for deletion-only rather than retention-only or retention and then delete, and the Deleted Items folder has a retention policy tag (RPT) applied:

    - An autoapplied retention label remains applied to the item and the deletion settings from the retention label are enforced.
    - When an inherited retention label or inherited retention tag is applied to an item, the item is deleted according to the shortest deletion period.