---
layout: Conceptual
title: Configure legacy on-premises public folders for a hybrid deployment in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/set-up-legacy-hybrid-public-folders
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
ms.topic: install-set-up-deploy
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- exchange-online
- M365-email-calendar
description: 'Summary: Use the steps in this article to synchronize public folders between Microsoft 365 and your Exchange Server 2010 on-premises deployment.'
audience: ITPro
f1.keywords:
- NOCSH
ms.date: 2026-06-03T00:00:00.0000000Z
locale: en-us
document_id: 45f5e210-5945-277a-12dc-f1eae01ba403
document_version_independent_id: a9a867e0-e3eb-ffbb-2013-47707a6b4364
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/set-up-legacy-hybrid-public-folders.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/set-up-legacy-hybrid-public-folders
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/set-up-legacy-hybrid-public-folders.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 222e3040-f53a-d47a-e3b6-8ae47d407bd7
---

# Configure legacy on-premises public folders for a hybrid deployment in Exchange Online | Microsoft Learn

**Summary**: Use the steps in this article to synchronize public folders between Microsoft 365 and your Exchange Server 2010 on-premises deployment.

In a hybrid deployment, your users can be in Exchange Online, on-premises, or both, and your public folders are either in Exchange Online or on-premises. Public folders can reside in only one place, so you must decide whether your public folders will be in Exchange Online or on-premises. They can't be in both locations. Public folder mailboxes are synchronized to Exchange Online by the Directory Synchronization service. However, mail-enabled public folders aren't synchronized across premises.

This article describes how to synchronize mail-enabled public folders if your users are in the cloud and your Exchange Server 2010 SP3 public folders are on-premises. However, a cloud 365 user who isn't represented by a MailUser object in on-premises Exchange (local to the target public folder hierarchy) can't access legacy or modern on-premises public folders.

Note

This topic refers to the Exchange Server 2010 SP3 servers as the legacy Exchange server.

You sync your mail-enabled public folders by using the following scripts, which are started by a Windows task that runs in the on-premises environment:

- `Sync-MailPublicFolders.ps1`: This script synchronizes mail-enabled public folder objects from your local Exchange on-premises deployment to the cloud. It uses the local Exchange on-premises deployment as authoritative to determine the changes to the make in the cloud environment. The script creates, update, or delete mail-enabled public folder objects in Microsoft Entra based on what exists in the local on-premises Exchange deployment.

When you complete this procedure, your on-premises and cloud users can access the same on-premises public folder infrastructure.

## What hybrid versions of Exchange work with public folders?

The following table describes the version and location combinations of user mailboxes and public folders that are supported. "Hybrid not applicable" is still a supported scenario, but isn't considered a hybrid scenario since both the public folders and the users are residing in the same location.

| Version | On-premises Exchange 2010 User Mailbox | On-premises Exchange 2013 User Mailbox | Exchange Online User Mailbox |
| --- | --- | --- | --- |
| On-premises Exchange 2010 Public Folders | Hybrid not applicable | Hybrid not applicable | Supported |
| On-premises Exchange 2013 Public Folders | Hybrid not applicable | Hybrid not applicable | Supported |
| Exchange Online Public Folders | Not supported | Supported | Hybrid not applicable |

Note

Outlook 2016 does not support accessing Exchange 2007 legacy public folders. If you have users who are using Outlook 2016, you must move your public folders to a more recent version of Exchange Server. More information about Outlook 2016 and Office 2016 compatibility with Exchange 2007 and earlier versions can be found in [this article](https://support.microsoft.com/office/2ab9e8ef-4cd9-4041-9426-73e8f6c5aacc).

## Step 1: What do you have to know before you begin?

- These instructions assume that you used the Hybrid Configuration Wizard to:

    - Configure and synchronize your on-premises Exchange and Exchange Online environments.
    - The Autodiscover DNS records that are used for most users reference an on-premises endpoint.

    For more information, see [Hybrid Configuration Wizard](../../hybrid-configuration-wizard).
- These instructions assume that Outlook Anywhere is enabled and functional on all the on-premises legacy Exchange public folder servers. For information about how to enable Outlook Anywhere, see [Outlook Anywhere](../../outlook-anywhere-exchange-2013-help).
- Implementing legacy public folder coexistence for a hybrid deployment of Exchange with the cloud might require you to fix conflicts during the import procedure. The following example issues can cause conflicts:

    - Non-routable email addresses are assigned to mail-enabled public folders.
    - Conflicts with other cloud-based users and groups.
- These instructions assume that your Exchange Online organization is upgraded to a version that supports public folders. Install the latest update for your outlook version.
- To access public folders cross-premises, users must upgrade their Outlook clients to the November 2012 Outlook public update or a later version.

    1. To download the November 2012 Outlook update for Outlook 2010, see https://www.catalog.update.microsoft.com/Search.aspx?q=KB4052623.
    2. To download the November 2012 Outlook Update for Outlook 2007, see [Update for Microsoft Office Outlook 2007 (KB2687404)](https://www.catalog.update.microsoft.com/Search.aspx?q=outlook+2007)and download in your preferred language from the dialog box.
- Outlook 2016 for Mac (and earlier versions) and Outlook for Mac for Microsoft 365 aren't supported for cross-premises legacy public folders. Users must be in the same location as the public folders to access them with Outlook for Mac or Outlook for Mac for Microsoft 365.
- Users whose mailboxes are in Exchange Online can't access on-premises public folders using Outlook on the web.
- After you follow the instructions in this article to configure your on-premises public folders for a hybrid deployment, users who are external to your organization can't send messages to your on-premises public folders unless you take one of the following steps:

    - Set the accepted domain for the public folders to Internal Relay. For more information, see [Manage accepted domains in Exchange Online](../../mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains).
    - Disable Directory Based Edge Blocking (DBEB). For more information, see [Use Directory Based Edge Blocking to reject messages sent to invalid recipients](../../mail-flow-best-practices/use-directory-based-edge-blocking).

## Step 2: Make remote public folders discoverable

1. If your public folders are on Exchange 2010 or later servers, you must install the Client Access server (CAS) role on all mailbox servers that have a public folder database. This action allows the Microsoft Exchange RpcClientAccess service to be running so that all clients can access public folders. For more information, see [Install Exchange Server 2010](/en-us/previous-versions/office/exchange-server-2010/bb124778%28v=exchg.141%29).

    Note

    This server doesn't have to be part of the Client Access load balancing. For more information, see [Understanding Load Balancing in Exchange 2010](/en-us/previous-versions/office/exchange-server-2010/ff625247%28v=exchg.141%29).
2. Create an empty mailbox database on each public folder server.

    For Exchange 2010, run the following command. This command excludes the mailbox database from the mailbox provisioning load balancer. This prevents new mailboxes from being added automatically to this database.

    ```PowerShell
    New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true
    ```

    Note

    We recommend that the only mailbox that you add to this database is the proxy mailbox that you'll create in step 3. No other mailboxes should be created on this mailbox database.
3. Create a proxy mailbox within the new mailbox database, and hide the mailbox from the address book. The SMTP of this mailbox is returned by AutoDiscover as the *DefaultPublicFolderMailbox* SMTP, so that by resolving this SMTP the client can reach the legacy exchange server for public folder access.

    ```PowerShell
    New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs>
    ```

    ```PowerShell
    Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true
    ```
4. For Exchange 2010, enable AutoDiscover to return the proxy public folder mailboxes.

    ```PowerShell
    Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>
    ```
5. Repeat the preceding steps for every public folder server in your organization.

## Step 3: Download the scripts

1. Download the following file from [Mail-enabled Public Folders - directory sync script](https://github.com/microsoft/CSS-Exchange/releases/latest/download/Sync-MailPublicFolders.ps1):

    - `Sync-MailPublicFolders.ps1`
2. Save the files to the local computer where you run PowerShell. For example, C:\PFScripts.

## Step 4: Configure directory synchronization

The Directory Synchronization service doesn't synchronize mail-enabled public folders. Running the following script synchronizes the mail-enabled public folders across premises. Special permissions assigned to mail-enabled public folders need to be recreated in the cloud since cross-premises permissions aren't supported in Hybrid Deployment scenarios. For more information, see [Exchange Server Hybrid Deployment](../../exchange-hybrid).

Note

Synchronized mail-enabled public folders will appear as mail contact objects for mail flow purposes and will not be viewable in the Exchange admin center. See the Get-MailPublicFolder command. To recreate the SendAs permissions in the cloud, use the Add-RecipientPermission command.

On the legacy Exchange server, run the following command to synchronize mail-enabled public folders from your local on-premises Active Directory to the cloud.

```PowerShell
Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile "<sync_summary.csv>"
```

Where you're prompted for your cloud username and password, and *&lt;sync\_summary.csv&gt;* is the path to where you would like to log synchronization operations and errors, in .csv format.

Note

Before running the script, we recommend that you first simulate the actions that the script would take in your environment by running it as previously described, but with the *WhatIf* parameter.

We also recommend that you run this script daily to synchronize your mail-enabled public folders.

## Step 5: Configure Exchange Online users to access on-premises public folders

The final step in this procedure is to configure the Exchange Online organization and to allow access to the legacy on-premises public folders.

Enable the Exchange Online organization to access the on-premises public folders. You point to all of the proxy public folder mailboxes that you created in Step 2: Make remote public folders discoverable.

Run the following command in **Exchange Online PowerShell**:

```PowerShell
Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes 'PFMailbox1','PFMailbox2','PFMailbox3'
```

You must wait for Active Directory synchronization to complete before you see the changes. This process can take up to 3 hours. If you don't want to wait for the recurring synchronizations that occur every three hours, you can force directory synchronization at any time. For detailed steps to do force directory synchronization, see [Method 1: Manually verify that the service is started and that the admin account can sign in](/en-us/troubleshoot/azure/active-directory/directory-sync-stop-register#method-1-manually-verify-that-the-service-is-started-and-that-the-admin-account-can-sign-in). Microsoft 365 randomly selects one of the public folder mailboxes that's supplied in this command.

Important

A cloud user who isn't represented by a MailUser object on-premises (local to the target public folder hierarchy) can't access legacy or Exchange 2013 on-premises public folders. See the Knowledge Base article [Exchange Online users can't access legacy on-premises public folders](/en-us/exchange/troubleshoot/public-folders/cannot-access-legacy-on-premises-public-folders) for a solution.

## How do I know this procedure worked?

Sign in Outlook for a user who is in Exchange Online, and then run the following public folder tests:

- View the hierarchy.
- Check permissions.
- Create and delete public folders.
- Post content to and delete content from a public folder.