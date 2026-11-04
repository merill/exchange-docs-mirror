---
layout: Conceptual
title: Offline address books in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/offline-address-books/offline-address-books
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
description: Learn about offline address books (OABs) in Exchange Online.
ms.topic: overview
author: Srividyavaranasi
ms.author: srvar
ms.assetid: 3f4b2c64-6cbc-445f-bf65-05b8fdfe9a0b
ms.reviewer: 
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2026-10-27T00:00:00.0000000Z
locale: en-us
document_id: ea9985dd-585c-6cbe-6964-02f0b5d1c53d
document_version_independent_id: 96727ac8-6e44-0450-c505-7234483529fa
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/offline-address-books/offline-address-books.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/offline-address-books/offline-address-books
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/offline-address-books/offline-address-books.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: c6e31f7e-a118-e825-b679-1e8d6cf5ffdd
---

# Offline address books in Exchange Online | Microsoft Learn

An offline address book (OAB) is a downloadable address list collection that Outlook users can access while disconnected from Exchange Online. Admins can decide which address lists are made available to users who work offline.

Offline address books are generated every 8 hours.

For more information about address lists in Exchange Online, see [Address lists](../address-lists/address-lists).

For OAB procedures, see [Create an offline address book in Exchange Online](create-offline-address-book).

## How users download offline address books in classic Outlook for Windows

The following steps apply to classic Outlook for Windows when the Exchange account uses Cached Exchange Mode.

1. In classic Outlook for Windows, click **File** &gt; **Account Settings** &gt; **Download Address Book**.
2. On the **Offline address book** dialog box that's displayed, make the following selections:

    - **Download changes since last Send/Receive**: By default, this check box is selected. Unchecking this box causes a full download of the OAB.
    - **Choose address book**: This drop-down list will display the offline address books that are available to you. Depending on what an admin has configured, you might see only one value here (for example, the global address list).
3. Select **OK**. Outlook downloads and stores the OAB locally.

### Conditions that cause a full download of the OAB

There are situations where Outlook will always perform a full OAB download. For example:

- There's no OAB on the client computer (for example, this is the first time you've connected to your Exchange Online mailbox in Outlook on this computer).
- The version of the OAB on the server and the client don't match (a more recent version of the OAB is present on the server).
- One or more OAB files are missing from the client computer.
- A previous full download failed, and Outlook has to start over.
- When a user has multiple MAPI profiles on the same Outlook client computer and they switch between the two profiles that both use Cached Exchange Mode, multiple full OAB downloads of the same OAB files will occur.