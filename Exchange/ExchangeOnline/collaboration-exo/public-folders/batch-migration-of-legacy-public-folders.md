---
layout: Conceptual
title: Use batch migration to migrate legacy public folders to Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/batch-migration-of-legacy-public-folders
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
ms.custom:
- has-azure-ad-ps-ref
ms.author: lusassl
ms.topic: upgrade-and-migration-article
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms.collection:
- Strat_EX_EXOBlocker
- exchange-online
- M365-email-calendar
description: 'Summary: Use these procedures to move your Exchange 2010 public folders to Microsoft 365.'
audience: ITPro
f1.keywords:
- NOCSH
ms.date: 2026-06-03T00:00:00.0000000Z
locale: en-us
document_id: b4977532-9e3b-a1c3-3d00-563e01892417
document_version_independent_id: fc52a739-429e-730f-236d-29fe8da80db9
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/batch-migration-of-legacy-public-folders.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/batch-migration-of-legacy-public-folders
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/batch-migration-of-legacy-public-folders.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: d24ea953-7465-e38b-3372-e31cc5c2fe28
---

# Use batch migration to migrate legacy public folders to Microsoft 365 | Microsoft Learn

Note

Public folder migrations from Exchange Server 2010 and older versions to Exchange Online (Public folders and Microsoft 365 Groups) will be blocked starting October 1st, 2025. Organizations currently using Exchange Server 2010, or older versions are who are planning to migrate public folders to Exchange Online (Public Folders and Microsoft 365 Groups) using Microsoft native migration tools will be impacted by this change. Customers migrating public folders from Exchange Server 2010 and older to Exchange Online should complete their public folder migration by 1st October 2025. Please check [this announcement](batch-migration-of-legacy-public-folders) for more details.

**Summary**: Use these procedures to move your Exchange 2010 public folders to Microsoft 365.

This article describes how to migrate your public folders in a cutover or staged migration from Update Rollup 8 for Exchange Server 2010 Service Pack 3 (SP3) to Microsoft 365 and Exchange Online.

This article refers to the Exchange 2010 SP3 RU8 server as the legacy Exchange server. Also, the steps in this article apply to both Exchange Online and Microsoft 365. The terms might be used interchangeably in this article.

We recommend that you don't use Outlook's PST export feature to migrate public folders to Exchange Online. Microsoft 365 and Exchange Online public folder mailbox growth is managed using an auto-split feature that splits the public folder mailbox when it exceeds size quotas. Auto-split can't handle the sudden growth of public folder mailboxes when you use PST export to migrate your public folders and you might have to wait for up to two weeks for auto-split to move the data from the primary mailbox. We recommend that you use the cmdlet-based instructions in this document to migrate public folders to Exchange Online. However, if you elect to migrate public folders using PST export, see the Migrate Public Folders to Microsoft 365 by using Outlook PST export section later in this article.

You do the migration using the **\*-MigrationBatch** cmdlets, in addition to the following PowerShell scripts:

- `SourceSideValidations.ps1`: Source Side Validation script scans the public folders at source and reports issues found along with action to fix the issues. You run this script on the legacy on-premises Exchange server.
- `Export-PublicFolderStatistics.ps1`: This script creates the folder name-to-folder size mapping file. You run this script on the legacy Exchange server.
- `PublicFolderToMailboxMapGenerator.ps1`: This script creates the public folder-to-mailbox mapping file by using the output from the `Export-PublicFolderStatistics.ps1` script. You run this script on the legacy Exchange server.
- `Create-PublicFolderMailboxesForMigration.ps1`: This script creates the target public folder mailboxes for the migration. In addition, this script calculates the number of mailboxes necessary to handle the estimated user load, based on the guidelines for the number of user logons per public folder mailbox recommended in [Limits for Public Folders](../../limits-for-public-folders-exchange-2013-help).
- `Sync-MailPublicFolders.ps1`: This script synchronizes mail-enabled public folder objects between your local Exchange deployment and Microsoft 365. You run this script on the legacy Exchange server.

Step 1: Download the migration scripts provides details about where to download these scripts. Make sure all scripts are downloaded to the same location.

## What versions of Exchange are supported for migrating public folders to Microsoft 365 and Exchange Online?

Exchange supports moving your public folders to Microsoft 365 and Exchange Online from the following legacy versions of Exchange Server:

- Exchange 2010 SP3 RU8 or later

If you need to move your public folders to Exchange Online but your on-premises servers aren't running the minimum support versions of Exchange 2010, we strongly recommend that you upgrade your on-premises servers and use batch migration, which is the only supported public folder migration method.

You can't migrate public folders directly from Exchange 2003 or Exchange 2007. If you're running Exchange 2007 or earlier in your organization, you need to move all public folder databases and replicas to Exchange 2010 SP3 RU8 or later. No public folder replicas can remain on Exchange 2007 or earlier. Additionally, mail destined for an Exchange 2013 or later public folder can't be routed through an Exchange 2003 or Exchange 2007 server.

## What do you need to know before you begin?

- The Exchange 2010 server needs to be running Exchange 2010 SP3 RU8 or later.
- In Microsoft 365 and Exchange Online, you need to be a member of the Organization Management role group. This role group is different from the permissions assigned to you when you first enrolled. For details about how to enable the Organization Management role group, see [Manage role groups in Exchange Online](../../permissions-exo/role-groups).
- In Exchange 2010, you need to be a member of the Organization Management or Server Management RBAC role groups. For details, see [Add Members to a Role Group](/en-us/previous-versions/office/exchange-server-2010/dd638143%28v=exchg.141%29).
- Before you begin the public folder migration, if any single public folder in your organization is larger than 25 GB, we recommend that you delete content from that folder to make it smaller. Or, we recommend that you divide the public folder's content into multiple, smaller public folders. The 25 GB limit cited here only applies to the public folder and not to any child or subfolders. If neither option is feasible, we recommend that you don't move your public folders to Exchange Online. For more information, see [Exchange Online Limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits).

    Tip

    If your current public folder quotas in Exchange Online are less than 25 GB, you can use the [Set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/Set-OrganizationConfig) cmdlet to increase them with the `DefaultPublicFolderIssueWarningQuota` and `DefaultPublicFolderProhibitPostQuota` parameters.
- If you use a firewall and access control lists (ACLs), ensure that the [IP ranges used by Microsoft 365 in your region](/en-us/office365/enterprise/urls-and-ip-address-ranges) are permitted through your firewall.
- In Microsoft 365 and Exchange Online, you can create a maximum of 1,000 public folder mailboxes.
- Before you migrate your public folders, we recommend that you first move all user mailboxes to Microsoft 365 and Exchange Online. For details, see [Ways to migrate multiple email accounts to Microsoft 365](../../mailbox-migration/mailbox-migration). However, you still need to keep in the on-premises environment the mailbox for PF admin performing migration or create new PF admin account and assign a mailbox hosted on the legacy Exchange server.
- Outlook Anywhere needs to be enabled on the legacy Exchange server. For details about enabling Outlook Anywhere on Exchange 2010 servers, see [Enable Outlook Anywhere](/en-us/previous-versions/office/exchange-server-2010/bb123542%28v=exchg.141%29).
- You can't use the Exchange admin center (EAC) or the Exchange Management Console (EMC) to perform this procedure. On the legacy Exchange servers, you need to use the Exchange Management Shell. For Exchange Online, you need to use Exchange Online PowerShell. For more information, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You must use a single migration batch to migrate all of your public folder data. Exchange allows creating only one migration batch at a time. If you attempt to create more than one migration batch simultaneously, you get an error.
- Before you begin, we recommend that you read this article in its entirety as downtime is required for some steps.
- For information about keyboard shortcuts that might apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).
- Verify if the DefaultPublicFolderAgeLimit is configured on the organization level (`Get-OrganizationConfig | Format-List DefaultPublicFolderAgeLimit`) or if you have any AgeLimit (`Get-PublicFolder <FolderPath> | Format-List AgeLimit`) configured for the individual Public Folders, so that automatic deletions of the content to be prevented.

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Step 1: Download the migration scripts

1. Download all scripts and supporting files from [Public Folders Migration Scripts](https://aka.ms/PublicFolderScripts).
2. Save the scripts to the local computer where you intend to run PowerShell. For example, C:\PFScripts. Make sure all scripts are saved in the same location.
3. Download the following file from [Mail-enabled Public Folders - directory sync script](https://github.com/microsoft/CSS-Exchange/releases/latest/download/Sync-MailPublicFolders.ps1):

    - `Sync-MailPublicFolders.ps1`
4. Download the source side validation script from https://aka.ms/ssv2.
5. Save the scripts to the same location you did for step 2. For example, C:\PFScripts.

## Step 2: Prepare for the migration

Perform the following prerequisite steps before you begin the migration.

Note

We strongly recommend running the Source Side Validation script from an on-premises Exchange 2010 server with the Mailbox role installed. The script scans and reports issues that are known to cause migration to be slow, along with guidance to fix these issues. Use the examples described [here](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/Making-your-public-folder-migrations-faster-and-more-reliable/ba-p/917622).

### General prerequisite steps

- Make sure that there are no orphaned public folder mail objects in Active Directory, meaning objects in Active Directory without a corresponding Exchange object.
- Confirm that SMTP email address configured for public folders in Active Directory match the SMTP email addresses on the Exchange objects.
- Make sure that there are no duplicate public folder objects in Active Directory, to avoid a situation where two or more Active Directory objects are pointing to the same mail-enabled public folder.

### Prerequisite steps on the legacy Exchange server

Note

We strongly recommend running the Source Side Validation script from an on-premises Exchange 2010 server with the Mailbox role installed. The script scans and reports issues that are known to cause migration to be slow, along with guidance to fix these issues. Use the examples as documented [here](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/Making-your-public-folder-migrations-faster-and-more-reliable/ba-p/917622). The script does all the following prerequisites.

1. On the legacy Exchange server, make sure that routing to the mail-enabled public folders in the cloud continues to work until all DNS caches over the internet are updated to point to the cloud DNS where your organization now resides. Run the following command to configure an accepted domain with a well-known name that properly routes email messages to the cloud domain.

    ```powershell
    New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName <target domain> -DomainType InternalRelay
    ```

    Example:

    ```powershell
    New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName 'contoso.mail.onmicrosoft.com' -DomainType InternalRelay
    ```

    If the accepted domain already exists in your on-premises environment, rename it to PublicFolderDestination\_78c0b207\_5ad2\_4fee\_8cb9\_f373175b3f99 and leave the other attributes intact.

    To check if the accepted domain is already present in your on-premises environment, run the following command:

    ```powershell
    Get-AcceptedDomain | Where {$_.DomainName -eq "<target domain>"}
    ```

    To rename the accepted domain to PublicFolderDestination\_78c0b207\_5ad2\_4fee\_8cb9\_f373175b3f99, run the following command:

    ```powershell
    Get-AcceptedDomain | Where {$_.DomainName -eq "<target domain>"} | Set-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99
    ```

    If you're expecting your mail-enabled public folders in Exchange Online to receive external emails from the Internet, you have to disable Directory Based Edge Blocking (DBEB) in Microsoft 365. See [Use Directory Based Edge Blocking](../../mail-flow-best-practices/use-directory-based-edge-blocking) to reject messages sent to invalid recipients for more information.

    If the name of a public folder contains a backslash ( **\** ) or a forward slash ( **/** ), the public folders might be created in the parent public folder when migration occurs. Before you migrate, we recommend that you rename any public folders that have a backslash or a forward slash in the name.

    In Exchange 2010, to locate public folders that have a backslash in the name, run the following command:

    ```powershell
    Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name,Identity
    ```
2. If any public folders are returned, you can rename them by running the following command:

    ```powershell
    Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>
    ```
3. Make sure there isn't a previous record of a successful migration. If there is, you need to set that value to `$false`. Otherwise, the migration request will fail.

    The following example checks the public folder migration status.

    ```powershell
    Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration,PublicFolderMigrationComplete
    ```
4. This step is required only if you're re-attempting a migration that failed previously.

    If the status of the *PublicFoldersLockedforMigration* or *PublicFolderMigrationComplete* properties is `$true`, run the following command to set the value to `$false`.

    ```powershell
    Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    ```

    Important

    After resetting these properties, you need to wait for Exchange to detect the new settings. This result might take up to two hours to complete.
5. For verification purposes at the end of migration, we recommend that you first run the following Exchange Management Shell commands on the legacy Exchange server to take snapshots of your current public folder deployment.

    Run the following command to take a snapshot of the original source folder structure.

    ```powershell
    Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    ```

    Run the following command to take a snapshot of public folder statistics such as item count, size, and owner.

    ```powershell
    Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    ```

    Run the following command to take a snapshot of the permissions.

    ```powershell
    Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    ```

    Save the information from the preceding commands for comparison at the end of the migration.
6. If you're using Microsoft Entra Connect (Microsoft Entra Connect) to synchronize your on-premises directories with Microsoft Entra ID, you need to do the following (if you aren't using Microsoft Entra Connect, you can skip this step):

    1. On an on-premises computer, open Microsoft Entra Connect, and then select **Configure**.
    2. On the **Additional tasks** screen, select **Customize synchronization options**, and then select **Next**.
    3. On the **Connect to Microsoft Entra ID** screen, enter the appropriate credentials, and then select **Next**. Once connected, keep selecting **Next** until you are on the **Optional Features** screen.
    4. Make sure that **Exchange Mail Public Folders** isn't selected. If it isn't selected, you can continue to the next section. If it's selected, clear the check box, and then select **Next**.

        Note

        If you don't see **Exchange Mail Public Folders** as an option on the **Optional Features** screen, you can exit Microsoft Entra Connect and proceed to the next section.
7. After you clear the **Exchange Mail Public Folders** selection, keep selecting **Next** until you're on the **Ready to configure** screen, and then select **Configure**.

For detailed syntax and parameter information, see the following articles:

- [New-AcceptedDomain](/en-us/powershell/module/exchangepowershell/new-accepteddomain)
- [Get-PublicFolder](/en-us/powershell/module/exchangepowershell/get-publicfolder)
- [Get-PublicFolderDatabase](/en-us/powershell/module/exchangepowershell/get-publicfolderdatabase)
- [Set-PublicFolder](/en-us/powershell/module/exchangepowershell/set-publicfolder)
- [Get-PublicFolderStatistics](/en-us/powershell/module/exchangepowershell/get-publicfolderstatistics)
- [Get-PublicFolderClientPermission](/en-us/powershell/module/exchangepowershell/get-publicfolderclientpermission)
- [Get-OrganizationConfig](/en-us/powershell/module/exchangepowershell/Get-OrganizationConfig)
- [Set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/Set-OrganizationConfig)

### Prerequisite steps in the cloud

1. Make sure there are no existing public folder migration requests. If there are, clear them or your own migration request will fail. This step isn't required in all cases; it's only required if you think there might be an existing migration request in the pipeline.

    Important

    Before removing a migration request, it's important to understand why there was an existing one. The following commands determine when a previous request was made and helps you diagnose any problems that might have happened. You might need to communicate with other administrators in your organization to determine why the change was made.

    The following example discovers any existing batch migration requests:

    ```powershell
    $batch = Get-MigrationBatch | Where-Object {$_.MigrationType.ToString() -eq "PublicFolder"}
    ```

    The following example removes any existing public folder batch migration requests.

    ```powershell
    $batch | Remove-MigrationBatch -Confirm:$false
    ```
2. Confirm that no public folders or public folder mailboxes exist in the cloud.

    Important

    If you see public folders in the cloud, it's important to determine why they're there, and who started a public folder hierarchy before you remove the public folders and public folder mailboxes.

    1. In Exchange Online PowerShell, run the following command to see if any public folders mailboxes exist:

        ```powershell
        Get-Mailbox -PublicFolder
        ```
    2. If the command didn't return any public folder mailboxes, continue to Step 3: Generate the .csv files. If the command returned any public folders mailboxes, run the following command to see if any public folders exist:

        ```powershell
        Get-PublicFolder
        ```
    3. If you have any public folders in the cloud, run the following command in Exchange Online PowerShell to remove them. Make sure you saved any information that was in the cloud-based public folders.

Caution

All information contained in the public folders is permanently deleted when you remove the public folders.

        ```powershell
        Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false
        Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
        ```
    4. After the public folders are removed, run the following commands to remove all public folder mailboxes.

        ```powershell
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
        ```

For detailed syntax and parameter information, see the following articles:

- [Get-MigrationBatch](/en-us/powershell/module/exchangepowershell/get-migrationbatch)
- [Get-PublicFolderMailboxMigrationRequest](/en-us/powershell/module/exchangepowershell/get-publicfoldermailboxmigrationrequest)
- [Remove-PublicFolderMailboxMigrationRequest](/en-us/powershell/module/exchangepowershell/remove-publicfoldermailboxmigrationrequest)
- [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox)
- [Get-PublicFolder](/en-us/powershell/module/exchangepowershell/get-publicfolder)
- [get-MailPublicFolder](/en-us/powershell/module/exchangepowershell/get-mailpublicfolder)
- [Disable-MailPublicFolder](/en-us/powershell/module/exchangepowershell/disable-mailpublicfolder)
- [remove-PublicFolder](/en-us/powershell/module/exchangepowershell/remove-publicfolder)
- [Remove-Mailbox](/en-us/powershell/module/exchangepowershell/remove-mailbox)

## Step 3: Generate the .csv files

1. On the legacy Exchange server, run the `Export-PublicFolderStatistics.ps1` script to create the folder name-to-folder size mapping file. A local administrator needs to run this script. The file contains two columns: **FolderName** and **FolderSize**. The **FolderSize** column is displayed in bytes. For example, **\PublicFolder01,10000**.

    ```powershell
    .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    ```

    - *FQDN of source server* equals the fully qualified domain name of the Mailbox server where the public folder hierarchy is hosted.
    - *Folder to size map path* equals the file name and path on a network shared folder where you want the .csv file saved. Later in this article, you need to use the Exchange Online PowerShell to access this file. If you specify only the file name, the file is generated in the current PowerShell directory on the local computer.
    - If necessary, remove any mail-enabled system folders from the script output before proceeding.
2. Run the `PublicFolderToMailboxMapGenerator.ps1` script to create the public folder-to-mailbox mapping file. This file is used to calculate the correct number of public folder mailboxes in Exchange Online.

    ```powershell
    .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    ```

    - Before you run the script, use the following command to check the current public folder limits in your Exchange Online tenant. Then, note the current quota values for public folders.

        ```powershell
        Get-OrganizationConfig | Format-List *quota*
        ```

        In Exchange Online, the default value is 1.7 GB for **DefaultPublicFolderIssueWarningQuota** and 2 GB for **DefaultPublicFolderProhibitPostQuota**.
    - *Maximum mailbox size in bytes* equals the maximum size that you want to set for the new public folder mailboxes. In Exchange Online, the maximum size of public folder mailboxes is 100 GB. We recommend that you use a setting of 75 GB so that each public folder mailbox has room to grow. Fewer public folder mailboxes mean fewer connections for the Outlook clients, which might help to avoid performance issues. The location is transparent for users, as they see the same hierarchy on the client side. Exchange Online has a default public folder "prohibit post" quota of 2 GB. If you have individual public folders that are larger than 2 GB, you can use any of the following options to fix this issue:
    - Before you start the migration batch, increase the default public folder "prohibit post" quota by running the following command:

        ```powershell
        Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>
        ```
    - Before you start the migration batch, delete public folder content to reduce the size of the content to 2 GB or less.
    - Before you start the migration batch, split the public folder into multiple public folders that are each 2 GB or less.

        Note

        If the public folder is larger than 30 GB, and if it isn't feasible to delete content or split it into multiple public folders, we recommend that you don't move your public folders to Exchange Online.
    - *Folder to size map path* equals the file path of the .csv file that you created when you ran the `Export-PublicFolderStatistics.ps1` script.
    - *Folder to mailbox map path* equals the file name and path of the folder-to-mailbox .csv file that you create in this step. If you specify only the file name, the file is generated in the current PowerShell directory on the local computer.

Note

After the scripts are run and the .csv files are generated, any new public folders or updates to existing public folders aren't collected.

## Step 4: Create the public folder mailboxes in Exchange Online

Run the following command to create the target public folder mailboxes. The script creates a target mailbox for each mailbox in the .csv file that you generated previously in Step 3, by running the `PublicFoldertoMailboxMapGenerator.ps1` script.

```powershell
.\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
```

*Mapping.csv* is the file generated by the `PublicFoldertoMailboxMapGenerator.ps1` script in Step 3. The estimated number of simultaneous user connections browsing a public folder hierarchy is usually less than the total number of users in an organization.

Note

Use Exchange Online PowerShell for running this script. For more information, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

## Step 5: Start the migration request

1. Perform the following steps on the Exchange server to fulfill the prerequisite for running the *Sync-MailPublicFolders.ps1* script.

    1. Sign in with the account that has Enterprise administrator permissions.
    2. Install EXO PowerShell as described in [Install and maintain the Exchange Online PowerShell module](/en-us/powershell/exchange/exchange-online-powershell-v2#install-and-maintain-the-exchange-online-powershell-module).
    3. Launch PowerShell in administrator mode.
    4. Run the following commands to start the synchronization:

        ```powershell
        Add-PSSnapin *exchange* | .\Sync-MailPublicFolders.ps1 -CsvSummaryFile:sync_summary.csv
        ```
    5. Once prompted, enter the credentials for your Microsoft 365 tenant administrator account.
2. On the legacy Exchange server, get the following information that's needed to run the migration request:

    1. Find the `LegacyExchangeDN` of the user's account who is a member of the Public Folder Administrator role. This account is the same user whose credentials you need in step 3 of this procedure.

        Note

        The account used must be mailbox enabled in the on-premises Exchange Server. Create a new on-premises mailbox for the Public Folder Administrator account if one doesn't exist there.

        ```powershell
        Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
        ```
    2. Find the `LegacyExchangeDN` of any Mailbox server that has a public folder database.

        ```powershell
        Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
        ```
    3. Find the FQDN of the Outlook Anywhere host name. If you have multiple instances of Outlook Anywhere, we recommend that you select the instance that is either closest to the migration endpoint or the one that is closest to the public folder replicas in the legacy Exchange organization. The following command finds all instances of Outlook Anywhere:

        ```powershell
        Get-OutlookAnywhere | Format-Table Identity,ExternalHostName
        ```
3. In Exchange Online PowerShell, run the following commands to pass the information that was returned in the previous step to variables that are used in the migration request.

    1. Pass the credential of a user who has administrative permissions on the legacy Exchange server into the variable `$Source_Credential`. The migration request that's run in Exchange Online uses this credential to gain access to your legacy Exchange servers to copy the content over.

        ```powershell
        $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
        ```
    2. Use the `ExchangeLegacyDN` of the migration user on the legacy Exchange server that you found in step 2a and pass it into the variable `$Source_RemoteMailboxLegacyDN`.

        ```powershell
        $Source_RemoteMailboxLegacyDN = "<paste the value here>"
        ```
    3. Use the `ExchangeLegacyDN` of the public folder server that you found in step 2b above and pass it into the variable `$Source_RemotePublicFolderServerLegacyDN`.

        ```powershell
        $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
        ```
    4. Use the External Host Name of Outlook Anywhere that you found in step 2c above and pass it into the variable `$Source_OutlookAnywhereExternalHostName`.

        ```powershell
        $Source_OutlookAnywhereExternalHostName = "<paste the value here>"
        ```
4. Finally, in Exchange Online PowerShell, run the following commands to create the migration request.

    Note

    The authentication method in the following example needs to match your Outlook Anywhere settings. Otherwise, the command will fail.

    ```powershell
    $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
    $bytes = [System.IO.File]::ReadAllBytes('folder_mapping.csv')
    New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    ```

    Where `folder_mapping.csv` is the map file that was generated in Step 3: Generate the .csv files.

    Note

    You might notice the above command failing with the error "Cannot find a recipient that has mailbox GUID" error, with the GUID mentioned of public folder mailbox in EXO. This issue can be caused by AD replication latency. Wait an hour and retry the command.
5. Start the migration using the following command:

    ```powershell
    Start-MigrationBatch PublicFolderMigration
    ```

While batch migrations need to be created using the **New-MigrationBatch** cmdlet in the Exchange Management Shell, the progress and completion of the migration can be viewed and managed in the EAC. Because the **New-MigrationBatch** cmdlet initiates a mailbox migration request for each public folder mailbox, you can view the status of these requests using the mailbox migration page. You can get to the mailbox migration page, and create migration reports that can be emailed to you, by doing the following:

1. Log into Exchange Online and open the EAC.
2. Navigate to **Mailbox** &gt; **Migration**.
3. Select the migration request that was just created, and then select **View Details** in the **Details** pane.

For detailed syntax and parameter information, see the following articles:

- [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox)
- [Get-ExchangeServer](/en-us/powershell/module/exchangepowershell/get-exchangeserver)
- [Get-OutlookAnywhere](/en-us/powershell/module/exchangepowershell/get-outlookanywhere)
- [New-MigrationBatch](/en-us/powershell/module/exchangepowershell/new-migrationbatch)
- [Get-PublicFolderDatabase](/en-us/powershell/module/exchangepowershell/get-publicfolderdatabase)
- [Get-PublicFolderMailboxMigrationRequest](/en-us/powershell/module/exchangepowershell/get-publicfoldermailboxmigrationrequest)
- [Get-PublicFolderMailboxMigrationRequestStatistics](/en-us/powershell/module/exchangepowershell/get-publicfoldermailboxmigrationrequeststatistics)

## Step 6: Lock down the public folders on the legacy Exchange server for final migration (downtime required)

Up to this point in the migration, users can still access public folders. The next steps disconnect users from the legacy public folders and lock the folders while the migration completes final synchronization. Users can't access public folders during this process. Also, any mail sent to mail-enabled public folders is queued and isn't delivered until the public folder migration is complete.

Note

The final sync might take substantial amount of time, depending on the changes made on the source environment, size of public folder deployment, server capacity, etc. Not cleaning up a large number of corrupt ACLs in the folder hierarchy before starting migration can cause a significant delay. We recommend that you plan for a minimum of 48 hours of downtime for the final sync to complete.

Ensure the migration batch and individual migration requests have successfully synced.

Run the following commands in Exchange Online PowerShell to get the details:

```powershell
Get-MigrationBatch | Where-Object {$_.MigrationType -like "*PublicFolder*"} | Format-Table *last*sync*

Get-PublicFolderMailboxMigrationRequest | Get-PublicFolderMailboxMigrationRequestStatistics | Format-Table targetmailbox,*last*sync*
```

The LastSyncedDate (on migration batch) and LastSuccessfulSyncTimestamp (on individual jobs) should be within last seven days. If it's too far off, like older than a month or so, you might want to take a look at public folder migration requests and ensure all the requests were synced recently.

Once you have confirmed the batch and all migration requests have successfully synced, on the legacy Exchange server, run the following command to lock the legacy public folders for finalization.

```powershell
Set-OrganizationConfig -PublicFoldersLockedForMigration:$true
```

For detailed syntax and parameter information, see [set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/set-organizationconfig).

If your organization has multiple public folder databases, you need to wait until public folder replication is complete to confirm that all public folder databases have picked up the `PublicFoldersLockedForMigration` flag and any pending changes users recently made to folders have converged across the organization. This processmight take several hours.

## Step 7: Finalize the public folder migration (downtime required)

To complete the public folder migration, run the following command:

```powershell
Complete-MigrationBatch PublicFolderMigration
```

Important

After a migration batch is completed, no additional data can be synchornized from Exchange servers on-premises and Exchange Online.

When you complete the migration, Exchange performs a final synchronization between the legacy Exchange server and Exchange Online. If the final synchronization is successful, the public folders in Exchange Online are unlocked and the status of the migration batch changes to **Completed**. It's common for the status of migration batch to remain on "Synced" for few hours before it switches to Completing. For migrations involving large number of target mailboxes, it's normal to see the status remain "Synced" state for more than 24 hours, provided none of underlying public folder migration requests have failed or were quarantined.

If you configured a hybrid deployment between your on-premises Exchange servers and Microsoft 365, you need to run the following command in Exchange Online PowerShell after migration is complete:

```powershell
Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local
```

## Step 8: Test and unlock the public folder migration

After you finalize the public folder migration, you should run the following test to make sure that the migration was successful. This allows you to test the migrated public folder hierarchy before you switch to using public folders in the cloud.

1. In Exchange Online PowerShell, assign some test mailboxes to use any newly migrated public folder mailbox as the default public folder mailbox.

    ```powershell
    Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>
    ```
2. Sign in Outlook 2010 or later with the test user identified in the previous step, and then perform the following public folder tests:

    - View the hierarchy.
    - Check permissions.
    - Create and delete public folders.
    - Post content to and delete content from a public folder.
3. If you run into any issues, see Roll back the migration later in this article. If the public folder content and hierarchy is acceptable and functions as expected, continue to the next step.
4. On the legacy Exchange server, run the following command to indicate that the public folder migration is complete:

    ```powershell
    Set-OrganizationConfig -PublicFolderMigrationComplete:$true
    ```
5. After you verify that migration is complete, run the following command in Exchange Online PowerShell to make sure that the *PublicFoldersEnabled* parameter on **Set-OrganizationConfig** is set to `Local`:

    ```powershell
    Set-OrganizationConfig -PublicFoldersEnabled Local
    ```

For detailed syntax and parameter information, see the following articles:

[Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox)

[Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox)

[Set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/set-organizationconfig)

## How do I know this worked?

In Step 2: Prepare for the migration, you were instructed to take snapshots of the public folder structure, statistics, and permissions before the migration began. The following steps help verify that your public folder migration was successful by taking the same snapshots after the migration is complete. You can then compare the data in both files to verify success.

1. In Exchange Online PowerShell, run the following command to take a snapshot of the new folder structure.

    ```powershell
    Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml
    ```
2. In Exchange Online PowerShell, run the following command to take a snapshot of the public folder statistics such as item count, size, and owner.

    ```powershell
    Get-PublicFolderStatistics | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml
    ```
3. In Exchange Online PowerShell, run the following command to take a snapshot of the permissions.

    ```powershell
    Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml
    ```

## Remove public folder databases from the legacy Exchange servers

After the migration is complete, and you have verified that your Exchange Online public folders are working as expected, you should remove the public folder databases on the legacy Exchange servers.

Important

Since all of your mailboxes were migrated to Microsoft 365 before the public folder migration, we strongly recommend that you route the traffic through Microsoft 365 (decentralized mail flow) instead of centralized mail flow through your on-premises environment. Choosing to keep mail flow centralized could cause delivery issues to your public folders, since you removed public folder mailbox databases from your on-premises organization.

- For details about how to remove public folder databases from Exchange 2010 servers, see [Remove Public Folder Databases](/en-us/previous-versions/office/exchange-server-2010/dd876883%28v=exchg.141%29).

## Roll back the migration

If you run into issues with the migration and need to reactivate your legacy Exchange public folders, perform the following steps.

Caution

If you roll your migration back to the legacy Exchange servers, you lose any email that was sent to mail-enabled public folders or content that was posted to public folders after the migration. To save this content, you need to export the public folder content to a .pst file and then import it to the legacy public folders when the rollback is complete.

1. On the legacy Exchange server, run the following command to unlock the legacy Exchange public folders. This process might take several hours.

    ```powershell
    Set-OrganizationConfig -PublicFoldersLockedForMigration:$False
    ```
2. In Exchange Online PowerShell, run the following commands to remove all Exchange Online public folders.

    ```powershell
    $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
    Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
    Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
    ```
3. On the legacy Exchange server, run the following command to set the `PublicFolderMigrationComplete` flag to `$false`.

    ```powershell
    Set-OrganizationConfig -PublicFolderMigrationComplete:$False
    ```

## Migrate Public Folders to Microsoft 365 by using Outlook PST export

We recommend that you don't use Outlook's PST export feature to migrate public folders to the cloud if your on-premises public folder hierarchy is greater than 30 GB. Microsoft 365 online public folder mailbox growth is managed using an auto-split feature that splits the public folder mailbox when it exceeds size quotas. Auto-split can't handle the sudden growth of public folder mailboxes when you use PST export to migrate your public folders and you might have to wait for up to two weeks for auto-split to move the data from the primary mailbox. In addition, consider the following before using Outlook PST to export public folders to the cloud:

- Public folder permissions are lost during this process. Capture the current permissions before migration and manually add them back once the migration is completed.
- If you use complex permissions or have many folders to migrate, we recommend that you use the cmdlet method for migration.
- Any item and folder changes made to the source public folders during the PST export migration are lost. Therefore, we recommend that you use the cmdlet method if this export and import process takes a long time to complete.

If you still want to migrate your public folders by using PST files, follow these steps to ensure a successful migration.

1. Use the instructions in Step 1: Download the migration scripts to download the migration scripts. You only need to download the `PublicFolderToMailboxMapGenerator.ps1` file.
2. Follow step 2 of Step 3: Generate the .csv files to create the public folder-to-mailbox mapping file. This file is used to calculate the correct number of public folder mailboxes in Exchange Online.
3. Create the public folder mailboxes that you need based on the mapping file. For more information, see [Create a public folder mailbox](create-public-folder-mailbox).
4. Use the **New-PublicFolder** cmdlet to create the top-most public folder in each of the public folder mailboxes by using the *Mailbox* parameter.
5. Export and import the PST files using Outlook.
6. Set the permissions on the public folders using the EAC. For more information, see [Step 3: Assign permissions to the public folder](set-up-public-folders#step-3-assign-permissions-to-the-public-folder).

Important

If you already started a PST migration and run into an issue where the primary mailbox is full, you have two options for recovering the PST migration:

- Wait for the auto-split to move the data from the primary mailbox. This process might take up to two weeks. However, all the public folders in a completely filled public folder mailbox can't receive new content until the auto-split completes.
- [Create a public folder mailbox](create-public-folder-mailbox) and then use the **New-PublicFolder** cmdlet with the *Mailbox* parameter to create the remaining public folders in the secondary public folder mailbox.

## Troubleshoot public folder migrations

Select the following button for common issues during public folder migration:

A flyout page opens in the Microsoft 365 admin center, sign in with your tenant admin account and select appropriate option.