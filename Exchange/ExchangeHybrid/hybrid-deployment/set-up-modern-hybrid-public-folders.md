---
layout: Conceptual
title: Configure Exchange Server public folders for a hybrid deployment | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/set-up-modern-hybrid-public-folders
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: install-set-up-deploy
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
ms.assetid: b828520f-022c-4fcb-ab68-e1c330e87c33
ms.reviewer: 
description: 'Summary: Instructions for enabling Exchange Online users to access on-premises public folders in your Exchange 2013 environment.'
ms.date: 2026-06-03T00:00:00.0000000Z
locale: en-us
document_id: 30a91350-4f21-d657-2a17-4700fce20acb
document_version_independent_id: 47f55e0e-a94b-c435-9174-c78d107e20c6
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/set-up-modern-hybrid-public-folders.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/set-up-modern-hybrid-public-folders
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/set-up-modern-hybrid-public-folders.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: b744fb31-65fa-d117-3e46-eeb3a7d8096f
---

# Configure Exchange Server public folders for a hybrid deployment | Microsoft Learn

**Summary**: Instructions for enabling Exchange Online users to access on-premises public folders in your Exchange 2013, Exchange 2016, or Exchange 2019 environment.

In a hybrid deployment, your users can be in Exchange Online, on-premises, or both, and your public folders are either in Exchange Online or on-premises. Sometimes your online users might need to access public folders in your Exchange Server on-premises environment.

Note

If you have Exchange 2010 public folders, see [Configure legacy on-premises public folders for a hybrid deployment](../collaboration/public-folders/configure-legacy-public-folders-for-hybrid).

This article describes how to enable your cloud users to access public folders in Exchange 2013, Exchange 2016, and Exchange 2019 (for the rest of this article, referred to as *Exchange Server*). To enable on-premises Exchange Server users to access public folders in Exchange Online see [Configure Exchange Online public folders for a hybrid deployment](../collaboration-exo/public-folders/set-up-exo-hybrid-public-folders#configure-exchange-online-public-folders-for-a-hybrid-deployment).

MailUser objects in the on-premises Exchange environment must represent cloud users in order to access Exchange Server public folders. This MailUser object must also be local to the target Exchange Server public folder hierarchy. If you have Exchange Online users who aren't currently represented on-premises by MailUser objects, refer to [Exchange Online users can't access legacy on-premises public folders](/en-us/exchange/troubleshoot/public-folders/cannot-access-legacy-on-premises-public-folders) to create matching on-premises entities.

## What do you need to know before you begin?

1. These instructions assume that Microsoft Entra Connect synchronization services (Microsoft Entra Connect Sync) is configured to synchronize public folder mailbox objects to Exchange Online. Ensure that your public folder mailbox objects are synchronized to Exchange Online and that they have auto-discoverable primary SMTP addresses.

    Here's an example of proper configuration in an on-premises environment:

    ![public folder synchronization in Exchange Server.](../exchangehybrid/media/hybrid-pfs-on-prem-config.png)

    Here's an example of proper configuration in Exchange Online:

    ![Public folder synchronization in Exchange Online.](../exchangehybrid/media/hybrid-pfs-exo-config.png)
2. These instructions assume the following facts:

    - You used the Hybrid Configuration wizard to configure and synchronize your on-premises and Exchange Online environments.
    - The Autodiscover DNS record for most users references an on-premises end-point.

    For more information, see [Hybrid Configuration wizard](../hybrid-configuration-wizard).
3. The public folders in this configuration can't be accessed using Outlook on the web (formerly known as Outlook Web App).
4. Implementing public folder coexistence for a hybrid deployment of Exchange with Microsoft 365 might require you to fix conflicts during the import procedure. Conflicts can happen due to non-routable email addresses assigned to mail enabled public folders, conflicts with other users and groups in Microsoft 365, and other attributes.
5. In order to access public folders cross-premises, users must upgrade their Outlook clients to the November 2012 Outlook public update or later.
6. To download the November 2012 Outlook update for Outlook 2010, see [Update for Microsoft Outlook 2010 (KB2687623) 32-Bit Edition](https://support.microsoft.com/topic/c18dfea2-abaf-ec22-146f-83a387436ea2).
7. Outlook 2016 for Mac (and later versions) is supported for cross-premises public folders. If clients in your organization use Outlook 2016 for Mac, make sure they have the April 2016 or higher update installed. For more information, see [Accessing public folders with Outlook 2016 for Mac](/en-us/exchange/collaboration-exo/public-folders/access-public-folders-with-outlook-2016-for-mac).

## Step 1: Download the scripts

1. Download the following file from [Exchange Server Public Folders Migration Scripts](https://aka.ms/PublicFolderScripts#mail-public-folder-sync):

    - `Sync-ModernMailPublicFolders.ps1`

    Note

    The download package at this location contains extra files. To follow the instructions in this article, you only need the file listed above. These scripts now support modern authentication.
2. Save the files to the local computer. For example, C:\PFScripts.

## Step 2: Synchronize mail-enabled public folder objects to Exchange Online

Microsoft Entra Connect Sync doesn't synchronize mail-enabled public folders to Exchange Online. Running the following script synchronizes the mail-enabled public folders across your on-premises environment and Exchange Online. Special permissions assigned to mail-enabled public folders, such as **Send As**, need to be recreated in Microsoft 365 since cross-premises permissions aren't supported in hybrid deployment scenarios. For more information, see [Exchange hybrid deployment documentation](../exchange-hybrid#exchange-hybrid-deployment-documentation).

Note

Synchronized mail-enabled public folders aren't visible in the Exchange admin center (EAC). Instead, use the [Get-MailPublicFolder](/en-us/powershell/module/exchangepowershell/get-mailpublicfolder) cmdlet. To recreate Send As permissions in the cloud, use the [Add-RecipientPermission](/en-us/powershell/module/exchangepowershell/add-recipientpermission) cmdlet.

On the Exchange server, run the following command in the Exchange Management Shell to synchronize mail-enabled public folders from your local on-premises Active Directory to Microsoft 365:

```PowerShell
.\Sync-ModernMailPublicFolders.ps1 -CsvSummaryFile:sync_summary.csv
```

Where `CsvSummaryFile` is the path to where you would like to log synchronization operations and errors, in .csv format.

Important

Before running the script, we recommend that you first simulate the actions that the script would take in your environment by running it as described previously with the *WhatIf* switch. As part of the sync operation, the script, when appropriate, could create, update, or delete mail-enabled public folder objects on Exchange Online.

We also recommend that you run this script daily to synchronize your mail-enabled public folders.

Use the steps in [Troubleshooting mail enabled public folder synchronization failures when using PowerShell script](/en-us/exchange/troubleshoot/public-folders/mepf-sync-failures-script) if you see errors while running the script.

## Step 3: Configure Exchange Online users to access Exchange Server on-premises public folders

An Exchange Online mailbox that's not represented by a MailUser object in on-premises Exchange (local to the target public folder hierarchy) can't access on-premises public folders.

To identified cloud mailboxes that aren't represented by MailUser object in on-Premises Exchange, run the following command in the Exchange Management Shell:

```PowerShell
Get-Mailbox |?{$_.IsDirSynced -eq $false}
```

These users get credential prompts after public folder mailbox access is configured. Use one of the following solutions for such users before enabling public folder access:

1. Link the Exchange Online only mailboxes listed in the previous step to on-premises users as described in [Exchange Online users can't access legacy on-premises public folders](/en-us/exchange/troubleshoot/public-folders/cannot-access-legacy-on-premises-public-folders).
2. Use the steps provided in [Controlled Connections to Public Folders](https://aka.ms/ControlPF) to enable public folder access only to mailboxes with linked users on-premises.

The final step in this process is to configure the Exchange Online organization and to allow access to the Exchange Server public folders.

Run the following command in Exchange Online PowerShell to enable the Exchange Online organization to access the on-premises public folders. You'll point to all of your on-premises public folder mailboxes.

```PowerShell
Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3
```

Note

You must wait until Microsoft Entra synchronization is complete before you can see the changes. This process can take up to three hours to complete. If you don't want to wait for the recurring synchronizations that occur every three hours, you can force directory synchronization at any time. For detailed steps to do force directory synchronization, see [Microsoft Entra Connect Sync: Scheduler](/en-us/azure/active-directory/hybrid/how-to-connect-sync-feature-scheduler).

## How do I know this worked?

Run the following Exchange Online PowerShell command to verify Exchange Online mailboxes have an **EffectivePublicFolderMailbox** value:

```PowerShell
Get-Mailbox | Format-Table Name,EffectivePublicFolderMailbox
```

Next, sign in Outlook with the credentials of an Exchange Online user and perform the following public folder tests:

- View the hierarchy
- Check permissions
- Create and delete public folders
- Post content to and delete content from a public folder