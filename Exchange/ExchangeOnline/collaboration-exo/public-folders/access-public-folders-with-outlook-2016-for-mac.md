---
layout: Conceptual
title: Accessing public folders with Outlook 2016 for Mac in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/access-public-folders-with-outlook-2016-for-mac
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: 'Summary: The most recent supported Exchange topologies that allow users to access public folders with Outlook 2016 for Mac.'
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: outlook
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: c87dbcfc-27e1-fe2f-6414-064aad816237
document_version_independent_id: d7bce5a2-0f22-7140-80d4-a1a2e7ce0649
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/access-public-folders-with-outlook-2016-for-mac.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/access-public-folders-with-outlook-2016-for-mac
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/access-public-folders-with-outlook-2016-for-mac.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 3262e551-ec93-3f1f-9f81-618cf4ffefcf
---

# Accessing public folders with Outlook 2016 for Mac in Exchange Online | Microsoft Learn

**Summary**: The most recent supported Exchange topologies that allow users to access public folders with Outlook 2016 for Mac.

Users of Outlook 2016 for Mac can now access public folders in Exchange Online in many different topologies.

## Outlook 2016 or 2019 for Mac

With the April 2016 update for Outlook 2016 for Mac, as well as CU14 for Exchange 2013 and CU2 for Exchange 2016, the above scenario will now work for Outlook 2016 or 2019 for Mac clients.

The following table summarizes the supported topologies for users with Outlook 2016 for Mac clients trying to access public folders in Exchange Online.

Note

The scenarios shown in the following table assume that the April 2016 update for Outlook 2016 for Mac has been applied to all clients.

| Public folders are deployed on... | User mailbox is on Exchange 2010 SP3 or later | User mailbox is on Exchange 2013 CU13 or later | User mailbox is on Exchange 2016 CU2 or later | User mailbox is in Microsoft 365, Office 365, or Exchange Online |
| --- | --- | --- | --- | --- |
| Exchange Server 2010 SP3 or later | Supported | Supported | Supported | Not supported |
| Exchange Server 2013 CU13 or later | Not supported | Supported | Supported | Supported |
| Exchange Server 2016 CU2 or later | Not supported | Supported | Supported | Supported |
| Microsoft 365, Office 365, or Exchange Online | Not supported | Supported | Supported | Supported |

The following articles describe how to deploy public folders in your Exchange organization in a coexistence or hybrid topology. As long as your Outlook 2016 for Mac clients have installed the April 2016 update, they'll be able to access public folders in the configurations detailed in these articles:

- [Configure legacy public folders where user mailboxes are on Exchange 2013 servers](../../configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help)
- [Configure Exchange 2013 public folders for a hybrid deployment](../../hybrid-deployment/set-up-modern-hybrid-public-folders)
- [Configure Exchange Online public folders for a hybrid deployment](set-up-exo-hybrid-public-folders)