---
layout: Conceptual
title: Provision recipients for offline address book downloads in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/offline-address-books/provision-recipients
Manager: serdars
ms.subservice: exo-address-books
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Admins can learn how to assign offline address books (OABs) to mailboxes in Exchange Online.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms.reviewer: 
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 9abd67f0-f80f-323d-83f4-5c310b29acf0
document_version_independent_id: 586603e3-619d-90e7-af7e-bb22296778c4
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/offline-address-books/provision-recipients.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/offline-address-books/provision-recipients
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/offline-address-books/provision-recipients.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 65024b1c-d2d9-5736-4f4e-da716047e4a5
---

# Provision recipients for offline address book downloads in Exchange Online | Microsoft Learn

If you use multiple offline address books (OABs) in your organization, you have only one option for assigning the OAB to users:

- **Per address book policy**: You can assign an address book policy (ABP) to a user, and the ABP specifies the OAB. If you assign an ABP to a user that already has an OAB assigned to their mailbox, the OAB that's assigned to the mailbox will take precedence. For more information, see [Assign an address book policy to mail users](../address-book-policies/assign-an-address-book-policy-to-mail-users).

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures).