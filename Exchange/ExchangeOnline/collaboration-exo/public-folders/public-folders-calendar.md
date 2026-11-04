---
layout: Conceptual
title: Create a public folder calendar in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/public-folders-calendar
Manager: serdars
ms.subservice: exo-groups
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.author: serdars
ms.topic: how-to
author: cichur
ms.collection:
- exchange-online
- M365-email-calendar
ms.assetid: b293b7e5-f9f7-4322-8d56-e30c75af6845
ms.reviewer: batre
description: This article describes how to create a public folder calendar.
audience: ITPro
f1.keywords:
- NOCSH
ms.service: exchange-online
ms.date: 2026-09-08T00:00:00.0000000Z
locale: en-us
document_id: a273f1fd-9cb5-f7f1-d8f5-8b7e159d1ab3
document_version_independent_id: e9cb295a-eb94-ad6c-80f9-7f8d38ab4876
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/public-folders-calendar.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/public-folders-calendar
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/public-folders-calendar.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 93292ba4-ed08-8d1f-ebda-78696364729c
---

# Create a public folder calendar in Exchange Online | Microsoft Learn

A public folder calendar is a good solution for people looking for only a shared calendar without having to maintain an additional mailbox along with it. This article explains how to set up and access public folder calendars in Microsoft Exchange Online.

Important

You must use the Microsoft Outlook desktop client to create the public folder calendar.

The Calendar type of public folder can be accessed from Outlook on the web and the Outlook desktop client. Public folders, including calendar, can't be accessed from mobile devices.

## Prerequisites

Before you create your public folder calendar, fulfill the following prerequisites.

1. Ensure public folders are [deployed](create-public-folder-mailbox) in Exchange Online.
2. Use the following command to see a list of any public folder mailboxes present in the organization:

    ```PowerShell
    Get-Mailbox -PublicFolder
    Get-PublicFolder \
    ```
3. If you don't see a list of the public folder mailboxes, then follow the steps to [create a public folder mailbox](create-public-folder-mailbox).
4. Verify that you have the necessary [access rights](/en-us/troubleshoot/exchange/public-folders/public-folder-permissions-for-exchange-server) to create the public folder.

    - If you want the user to be able to create a public folder on the root of the public folder hierarchy, along with all other access rights, run the following command:

        ```PowerShell
        Add-PublicFolderClientPermission -Identity "\" -AccessRights Owner -User User1
        ```
    - If you want the user to be able to create a public folder under the existing public folder, such as a folder named Marketing, then run the following command:

        ```PowerShell
        Add-PublicFolderClientPermission -Identity "\Marketing" -AccessRights Editor -User User1
        ```
5. Sign in to the Outlook desktop client and ensure you're able to access the public folder deployment.

## Create a public folder calendar

Once you have ensured that the prerequisites have been met, then you're ready to get started creating a public folder calendar.

1. Sign in to the Outlook desktop client with a user account that has the necessary [access rights](/en-us/troubleshoot/exchange/public-folders/public-folder-permissions-for-exchange-server) to create a public folder.
2. Expand the folders.
3. Create a new public folder of "calendar" type by performing either of the following sub-steps:

- Right-click **All Public Folders** and select **New Folder**, if you want to create a public folder calendar at the top level of the directories.
- Right-click a folder and select **New Folder**, if you want to create a public folder calendar under an existing public folder.

    ![The new folder dialog box.](../../exchangeonline/media/new-folder.png)

1. Name the new public folder and select **Calendar Items** from the **Folder contains** drop-down list.

    ![The Calendar option highlighted.](../../exchangeonline/media/folder-contains.png)
2. Select **OK**.

    The calendar type folder shows up with a different icon.

    ![The Calendar icon highlighted.](../../exchangeonline/media/different-icon.png)
3. For faster access to the new public folder calendar, right-click the folder and select **Add to Favorites...**. After doing so, you will find the calendar under **Calendars &gt; Other Calendars**.

## Share a public folder calendar

By default, everyone in the organization can access the public folder and create items in it. If you want to delegate additional access rights, add other users, and provide a required set of permissions, then follow the instructions in [public folder permissions](/en-us/troubleshoot/exchange/public-folders/public-folder-permissions-for-exchange-server).

## Access a public folder calendar in the Outlook on the web

1. Sign in to the Outlook on the web.
2. Right-click **Folders** and select **Add public folder to Favorites**.
3. Browse the directory and select the desired public folder.
4. Select **Add Public Folders**.

    ![The Add Public Folder option highlighted.](../../exchangeonline/media/holiday-folder-label.png)
5. Close the **Add Public Folder** menu.

    The calendar public folder shows up in Calendar area of the Outlook on the web.
6. Select the **Calendar** icon.

    You'll see the public folder calendar under **Other Calendars**.

    ![The new public folder calendar highlighted.](../../exchangeonline/media/public-folder-calendar-display.png)

## Receive emails to a public folder calendar

Follow the steps in [mail enable public folder calendar](enable-or-disable-mail-for-public-folder) to allow users to email:

- Calendar invites
- Appointments to the calendar.