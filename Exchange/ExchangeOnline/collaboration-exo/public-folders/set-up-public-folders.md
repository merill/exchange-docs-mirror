---
layout: Conceptual
title: Set up public folders in a new organization in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/set-up-public-folders
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
description: 'Summary: How to set up public folders, including assigning permissions to them in the EAC.'
ms.topic: install-set-up-deploy
author: AshaIyengar21
ms.author: serdars
ms.assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: c0f6d99e-005a-235f-dad0-ea1182669ab9
document_version_independent_id: 7bad943c-d900-84e2-95af-fa1bb0137110
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/set-up-public-folders.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/set-up-public-folders
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/set-up-public-folders.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: e120bcf4-2308-bc51-1b86-84f9e27aa219
---

# Set up public folders in a new organization in Exchange Online | Microsoft Learn

**Summary**: How to set up public folders, including assigning permissions to them in the EAC.

This topic shows you how to get public folders configured and running in a new organization or in an organization that has never previously had public folders.

Note

For more information about the storage quotas and limits for public folders, see [Exchange Online Limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits).

OWA for devices refers to the old *"OWA for Android"* and *"OWA for iPhone/iPad"* applications that have since been deprecated. For more details, see [Microsoft OWA mobile apps are being retired](https://support.microsoft.com/office/076ec122-4576-4900-bc26-937f84d25a4b).

The procedure in this article guides you through the process of creating public folders for the first time.

## What do you need to know before you begin?

- Estimated time to complete this task: 30 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Step 1: Create the primary public folder mailbox

The primary public folder mailbox contains a writeable copy of the public folder hierarchy plus content and is the first public folder mailbox that you create for your organization. Subsequent public folder mailboxes will be secondary public folder mailboxes, which will contain a read-only copy of the hierarchy plus content.

For detailed steps, see [Create a public folder mailbox](create-public-folder-mailbox).

## Step 2: Create your first public folder

For detailed steps, see [Create a public folder](create-public-folder).

## Step 3: Assign permissions to the public folder

After you create the public folder, you'll need to assign the **Owner** permissions level so that at least one user can access the public folder from the client and create subfolders. Any public folders created after this one will inherit the permissions of the parent public folder.

1. In the Exchange admin center (EAC), navigate to **Public folders** &gt; **Public folders**.
2. In the list view, select the public folder.
3. In the details pane, under **Folder permissions**, click **Manage**.
4. In **Public Folder Permissions**, click **Add**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif).
5. Click **Browse** to select a user.
6. In the **Permission level** list, select a level. At least one user should be an **Owner**.
7. Click **Save**.
8. You can add multiple users by clicking **Add**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif) and assigning the appropriate permissions using the steps above. You can also customize the permission level by selecting or clearing the check boxes. When you edit a predefined permission level such as **Owner**, the permission level will change to **Custom**.

For information about how to use Exchange Online PowerShell to assign permissions to a public folder, see [Add-PublicFolderClientPermission](/en-us/powershell/module/exchangepowershell/add-publicfolderclientpermission).

## Step 4 (Optional): Mail-enable the public folder

If you want users to send mail to the public folder, you can mail-enable it. This step is optional. If you don't mail-enable the public folder, users can post messages to the public folder by dragging items into it from within Outlook.

1. In the EAC, navigate to **Public folders** &gt; **Public folders**.
2. In the list view, select the public folder you want to mail-enable.
3. In the details pane, under **Mail settings - Disabled**, click **Enable**.

    A warning displays asking if you are sure you want to enable mail for the public folder. Click **Yes**.

The public folder will be mail-enabled and the name of the public folder will become the alias of the public folder. If you have multiple recipients with that name, the public folder's alias will be appended with a number. For example, if you have a distribution group named SalesTeam and you create a public folder named SalesTeam and then mail-enable it, the alias of that public folder will be SalesTeam1.

For information about how to use Exchange Online PowerShell to mail-enable a public folder, see [Enable-MailPublicFolder](/en-us/powershell/module/exchangepowershell/enable-mailpublicfolder).

Note

If you have a hybrid configuration, the public folders created on Exchange Online are only visible to cloud-based mailboxes. Conversely, public folders created on-premises are only visible to on-premises mailboxes.

To complete a migration from Exchange Server 2010 to Exchange Online with public folders, see [Configure legacy on-premises public folders for a hybrid deployment](set-up-legacy-hybrid-public-folders).