---
layout: Conceptual
title: Use favorite public folders in Outlook on the web in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/use-favorite-public-folders
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
description: In the Outlook client, users in your organization can add public folders to their Favorites folders. Then, depending on your organization's policies, they can use Outlook on the web to add those same public folders to their Favorites and perform certain functions in Outlook on the web that they use in the Outlook client.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: f6f1db72-4465-4eb8-b525-ac2c1fa10a69
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
document_id: 1322ea00-e4ee-5858-c224-c8b886f6a7d0
document_version_independent_id: 059da329-0f7f-cd54-31d7-cdec5eda9141
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/use-favorite-public-folders.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/use-favorite-public-folders
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/use-favorite-public-folders.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 3bd4b244-26fc-3f88-089b-a234a1c249e7
---

# Use favorite public folders in Outlook on the web in Exchange Online | Microsoft Learn

In the Outlook client, users in your organization can add public folders to their **Favorites** folders. Then, depending on your organization's policies, they can use Outlook on the web or the new Outlook for Windows to add those same public folders to their Favorites and perform certain functions in Outlook on the web that they use in the Outlook client.

## Add public folders to Favorites in Outlook

In order for users to perform certain tasks on public folders in their **Favorites** folder, they must first use the Outlook client to add public folders to the **Favorites** folder.

Note

For more information about creating and configuring public folders, users in your organization can see [Create a public folder in Outlook](https://support.microsoft.com/office/a2835011-d524-4a5c-a207-05c159bb2a97).

1. In Outlook, go to the **Folders** view. Click the three dots on the Navigation Bar, and the click **Folders**.

    ![Elipses in the Outlook 2013 Navigation Bar.](../../exchangeonline/media/7a949ccd-f0e0-4d20-aa4d-f97ae5c6fdff.png)

    ![Outlook 2013 Navigation Bar menu to access Folders.](../../exchangeonline/media/aaedd8fa-8a30-4e96-b4de-9625cd62e2b9.png)
2. If necessary, scroll to the **Public Folders** node in the Navigation Pane. Click to expand the **All Public Folders** folder.
3. Right-click the public folder that you want to add to **Favorites**, then select **Add to Favorites...**.

    Note

    By default, the **Favorites** folder is directly beneath the **All Public Folders** folder in the Navigation Bar.
4. In the **Add to Favorites** dialog, you have the option to rename the folder for your **Favorites** only. Click **Add** to add the folder to **Favorites**.

Important

There are several types of public folders. In order for users to be able to work with a favorite public folder in Outlook on the web, the public folder must be of type Mail and Post items, Calendar items, or Contact items.

## Add favorite public folders in Outlook on the web and the new Outlook for Windows

In order for users to access their Outlook favorite public folders, they must also add them to their Favorites in Outlook on the web or the new Outlook for Windows. The Outlook client does not automatically sync public folders with Outlook on the web or the new Outlook for Windows.

- To add a public folder in Outlook on the web or the new Outlook for Windows, right-click **Folders**, and then choose **Add public folder to Favorites**. Locate the folder and click **Add**.

    ![Add public folder to Favorites.](../../exchangeonline/media/dc2af75b-d1c3-4024-8759-00558799d34a.png)

Your users can now use Outlook on the web to perform the following tasks in their favorite Calendar, Contact, or Mail and Post public folders:

- Create items in the public folders
- Retrieve items
- Update items
- Delete items

Important

If you want to remove folders from the Favorites make sure to remove them instead of deleting them. When you remove a folder from Favorites, the original folder in the folder list remains. Deleting a folder from Favorites deletes the folder and its contents from Outlook. More information can be found [here](https://support.microsoft.com/office/8913f2d0-b167-48cc-8983-86fa9b0d945f).