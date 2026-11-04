---
layout: Conceptual
title: Use batch migration to migrate Exchange Online public folders to Microsoft 365 Groups | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/batch-migration-of-exchange-online-public-folders
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
ms.topic: upgrade-and-migration-article
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: e0be0727-f27f-4673-8a6f-af6ab5dbdace
ms.reviewer: 
ms.collection:
- Strat_EX_EXOBlocker
- exchange-online
- M365-email-calendar
description: How to move your Exchange Online public folders to Microsoft 365 Groups.
audience: ITPro
f1.keywords:
- NOCSH
ms.date: 2026-06-03T00:00:00.0000000Z
locale: en-us
document_id: 8a64bc33-37b2-5448-76b4-ec6bdb7a5f5a
document_version_independent_id: 1da420e5-5ad8-3484-5a3b-5f1d44ca97f0
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/batch-migration-of-exchange-online-public-folders.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/batch-migration-of-exchange-online-public-folders
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/batch-migration-of-exchange-online-public-folders.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 2be212b5-c856-9b09-c66d-4521dbc09dd7
---

# Use batch migration to migrate Exchange Online public folders to Microsoft 365 Groups | Microsoft Learn

**Summary**: How to move your Exchange Online public folders to Microsoft 365 Groups.

Through a process known as batch migration, you can move some or all of your Exchange Online public folders to Microsoft 365 Groups. Groups are a new collaboration offering from Microsoft that offers certain advantages over public folders. See [Migrate your public folders to Microsoft 365 Groups](migrate-your-public-folders-to-microsoft-365-groups) for an overview of the differences between public folders and Groups, and reasons why your organization may or may not benefit from switching to Groups.

This article contains the step-by-step procedures for performing the actual batch migration of your Exchange Online public folders.

## What do you need to know before you begin?

Ensure that all of the following conditions are met before you begin preparing your migration.

- Only public folders of type calendar and mail can be migrated to Microsoft 365 Groups at this time; migration of other types of public folders isn't supported. Also, the target Microsoft 365 groups are expected to exist prior to the migration.
- Microsoft 365 Groups don't support the permission roles and access rights that are available in public folders. In Microsoft 365 Groups, the users are designated as either **members** or **owners**.
- The batch migration process only copies messages and calendar items from public folders for migration to Microsoft 365 Groups. It doesn't copy other types of public folder content like rules and permissions, since that type of content isn't supported in Microsoft 365 Groups.
- Microsoft 365 Groups come with a 50 GB mailbox. Ensure that the sum of public folder data that you're migrating totals less than 50 GB. In addition, leave storage space for future content additions. We recommend migrating public folders no bigger than 25 GB in total size.
- This migration isn't "all or nothing". You can pick and choose specific public folders to migrate, and only those public folders are migrated. If the public folder being migrated has subfolders, those subfolders won't be automatically included in the migration. If you need to migrate them, you need to explicitly include them.
- The public folders will not be affected in any manner by this migration. However, once you use our lock-down script to make the migrated public folders read-only, your users will be forced to use Microsoft 365 Groups instead of public folders.
- Use a single migration batch to migrate all of your public folder data. Exchange allows creating only one migration batch at a time. If you attempt to create more than one migration batch simultaneously, the result will be an error.
- Before you begin, we recommend that you read this article in its entirety, as downtime is required for some steps.

## Step 1: Get the scripts

The batch migration to Microsoft 365 Groups requires running multiple scripts at different points in the migration as described in this article. Download the scripts and their supporting files [from this location](https://aka.ms/PublicFolderScripts#migration-to-microsoft-365-groups). After all the scripts and files are downloaded, save them to the same location, such as `c:\PFtoGroups\Scripts`.

Before proceeding, verify you have downloaded and saved all of the following scripts and files:

Note

Make sure to save all scripts and files to the same location.

- **AddMembersToGroups.ps1**: Adds members and owners to Microsoft 365 groups based on permission entries in the source public folders.
- **LockAndSavePublicFolderProperties.ps1**: Makes public folders read-only to prevent any modifications, and it transfers the mail-related public folder properties (provided the public folders are mail-enabled) to the target groups, which will reroute email from the public folders to the target groups. This script also backs up the permission entries and the mail properties before modifying them.
- **UnlockAndRestorePublicFolderProperties.ps1**: Restores access rights and mail properties of the public folders using backup files created by `LockandSavePublicFolderProperties.ps1`.
- **WriteLog.ps1**: Allows the `AddMembersToGroups.ps1`, `LockAndSavePublicFolderProperties.ps1`, and `UnlockAndRestorePublicFolderProperties.ps1` scripts to write logs.
- **RetryScriptBlock.ps1**: Allows the `AddMembersToGroups`, `LockAndSavePublicFolderProperties`, and `UnlockAndRestorePublicFolderProperties` scripts to retry certain actions if they encounter transient errors.

For details about the `AddMembersToGroups.ps1`, `LockAndSavePublicFolderProperties.ps1`, and `UnlockAndRestorePublicFolderProperties.ps1` scripts and the tasks they run in your environment, see the Migration scripts section later in this article.

## Step 2: Prepare for the migration

The following steps are necessary to prepare your organization for the migration:

1. Compile a list of public folders (mail and calendar types) that you want to migrate to Microsoft 365 Groups.
2. Have a list of corresponding target groups for each public folder being migrated. You can either create a new group in Microsoft 365 for each public folder or use an existing group. If you're creating a new group, see [Learn about Microsoft 365 Groups](https://support.microsoft.com/office/b565caa1-5c40-40ef-9915-60fdb2d97fa2) to understand the settings a group must have. If a public folder that you're migrating has the default permission set to **Author** or above, you should create the corresponding group in Microsoft 365 with the **Public** privacy setting. However, for users to see the public group under the **Groups** node in Outlook, they'll still have to join the group.
3. Rename any public folders that contain a backslash ( **\**) in their name. Otherwise, those public folders may not get migrated correctly.
4. The migration feature name PAW must be enabled for your organization. To verify that PAW is enabled, run the following command in Exchange Online PowerShell:

    ```PowerShell
    Get-MigrationConfig
    ```

    If the output under **Features** lists **PAW**, the feature is enabled and you can continue.

    If you have any existing user or public folder migration batches in any state (including **Completed**), **PAW** won't be enabled. Complete any remove any existing migration batches until no records are returned in the output of `Get-MigrationBatch`. After you remove all existing migration batches, PAW should be enabled automatically. The change may not reflect in `Get-MigrationConfig` immediately.

    Once this step is completed, you can continue creating new batches of user migrations.

## Step 3: Create the .csv file

Create a .csv file, which provides input for one of the migration scripts.

The .csv file needs to contain the following columns:

- **FolderPath**. Path of the public folder to be migrated.
- **TargetGroupMailbox**. SMTP address of the target Microsoft 365 group. You can run the following command to see the primary SMTP address.

    ```PowerShell
    Get-UnifiedGroup <alias of the group> | Format-Table PrimarySmtpAddress
    ```

An example .csv:

```csv
"FolderPath","TargetGroupMailbox"
"\Sales","sales@contoso.onmicrosoft.com"
"\Sales\EMEA","emeasales@contoso.onmicrosoft.com"
```

You can merge a mail folder and a calendar folder into a single Microsoft 365 group. However, any other scenario of multiple public folders merging into one group isn't supported within a single migration batch. If you need to map multiple public folders to the same Microsoft 365 group, run separate migration batches consecutively, one after another. You can have up to 500 entries in each migration batch.

One public folder should be migrated to only one group in one migration batch.

## Step 4: Start the migration request

In this step, you gather information from your Exchange environment, and then you use that information in Exchange Online PowerShell to create a migration batch. After that, you start the migration.

1. In Exchange Online PowerShell, run the following command to create a new public folder-to-Microsoft 365 group migration batch.

    ```PowerShell
    New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData ([System.IO.File]::ReadAllBytes('<path to .csv file>')) -PublicFolderToUnifiedGroup [-AutoStart]
    ```

    In this command:

    - *CSVData* is the .csv file created above in Step 3: Create the .csv file. Be sure to provide the full path to this file. If the file was moved for any reason, be sure to verify and use the new location.
    - *AutoStart* is an optional switch that starts the migration batch as soon as it's created.
    - *PublicFolderToUnifiedGroup* indicates that this is a public folder to Microsoft 365 Groups migration batch.
2. If you didn't use the *AutoStart* switch in the first command, start the migration by running the following command in Exchange Online PowerShell:

    ```PowerShell
    Start-MigrationBatch PublicFolderToGroupMigration
    ```

While batch migrations need to be created using the `New-MigrationBatch` cmdlet in Exchange Online PowerShell, the progress of the migration can be viewed and managed in Exchange admin center. You can also view the progress of the migration by running the [Get-MigrationBatch](/en-us/powershell/module/exchangepowershell/get-migrationbatch) and [Get-MigrationUser](/en-us/powershell/module/exchangepowershell/get-migrationuser) cmdlets. The `New-MigrationBatch` cmdlet initiates a migration user for each Microsoft 365 group mailbox, and you can view the status of these requests using the mailbox migration page.

To view the mailbox migration page:

1. In Exchange Online, open Exchange admin center.
2. Navigate to **Recipients**, and then select **Migration**.
3. Select the migration request that was just created and then, on the **Details** pane, select **View Details**.

When the batch status is **Completed**, you can move on to *Step 5: Add members to Microsoft 365 groups from public folders*.

## Step 5: Add members to Microsoft 365 groups from public folders

You can add members to the target Microsoft 365 group manually as required. However, if you want to add members to the group based on the permission entries in public folders, you need to do that by running the script `AddMembersToGroups.ps1` as shown in the following command. To know which public folder permissions are eligible to be added as members of a Microsoft 365 group, see Migration scripts later in this article.

In the following command:

- **MappingCsv** is the .csv file created above in *Step 3: Create the .csv file*. Be sure to provide the full path to this file. If the file was moved for any reason, be sure to verify and use the new location.
- **BackupDir** is the directory where the migration log files will be stored.
- **ArePublicFoldersOnPremises** is a parameter to indicate whether public folders are located on-premises or in Exchange Online.

```PowerShell
.\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $false
```

Once users have been added to a Microsoft 365 group, they can begin using it.

## Step 6: Lock down the public folders (public folder downtime required)

When most of the data in your public folders has migrated to Microsoft 365 Groups, you can run the script `LockAndSavePublicFolderProperties.ps1` to make the public folders read-only. This step ensures that no new data is added to public folders before the migration completes.

Note

If there are mail-enabled public folders (MEPFs) among the public folders being migrated, this step will copy some properties of MEPFs, such as SMTP addresses, to the corresponding Microsoft 365 group and then mail-disable the public folder. Because the migrating MEPFs will be mail-disabled after the execution of this script, you will start seeing emails sent to MEPFs instead being received in the corresponding groups. For details, see the Migration scripts section later in this article.

In the following command:

- **MappingCsv** is the .csv file created above in *Step 3: Create the .csv file*. Be sure to provide the full path to this file. If the file was moved for any reason, be sure to verify and use the new location.
- **BackupDir** is the directory where the backup files for permission entries, MEPF properties, and migration log files are stored. This backup is useful in case you need to roll back to public folders.
- **ArePublicFoldersOnPremises** is a parameter to indicate whether public folders are located on-premises or in Exchange Online.

```PowerShell
.\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $false
```

## Step 7: Finalize the public folder to Microsoft 365 Groups migration

1. After you've made your public folders read-only, you'll need to perform the migration again. This step is required for a final incremental copy of your data. Before you can run the migration again, you have to remove the existing batch, which you can do by running the following command:

    ```PowerShell
    Remove-MigrationBatch <name of migration batch>
    ```
2. Create a new batch with the same .csv file by running the following command:

    ```PowerShell
    New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData ([System.IO.File]::ReadAllBytes('<path to .csv file>')) -PublicFolderToUnifiedGroup [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]
    ```

    In this command:

    - *CSVData* is the .csv file created above in Step 3: Create the .csv file. Be sure to provide the full path to this file. If the file was moved for any reason, be sure to verify and use the new location.
    - *NotificationEmails* is an optional parameter that can be used to set email addresses that will receive notifications about the status and progress of the migration.
    - *AutoStart* is an optional switch that starts the migration batch as soon as it's created.
3. If you didn't use the *AutoStart* switch in the previous command, start the migration by running the following command in Exchange Online PowerShell:

    ```PowerShell
    Start-MigrationBatch PublicFolderToGroupMigration
    ```

    After you have finished this step (the batch status is **Completed**), verify that all data has been copied to Microsoft 365 groups. At that point, provided you're satisfied with the Groups experience, you can begin deleting the migrated public folders from your Exchange Online environment.

Important

While there are supported procedures for rolling back your migration and returning to public folders, this isn't possible after the source public folders have been deleted. See How do I roll back to public folders from Microsoft 365 Groups? for more information.

## Known issues

The following issues might occur during a typical public folders to Microsoft 365 Groups migration:

- The script that transfers SMTP address from mail-enabled public folders to Microsoft 365 groups only adds the addresses as secondary email addresses in Exchange Online. If you use Centralized Mail Flow, you'll have issues sending email to the groups (to the secondary email addresses) after the migration.
- If the .csv mapping file has an entry with invalid public folder path, the migration batch displays as **Completed** without throwing an error, and no further data is copied.

## Migration scripts

For your reference, this section provides in-depth descriptions for three of the migration scripts and the tasks they execute in your Exchange environment. You can download all of the scripts and supporting files [from this location](https://aka.ms/PublicFolderScripts#migration-to-microsoft-365-groups).

### AddMembersToGroups.ps1

This script will read the permissions of the public folders being migrated and then add members and owners to Microsoft 365 groups as follows:

- Users with the following permission roles will be added as members to a Microsoft 365 group. **Permission roles**: Owner, PublishingEditor, Editor, PublishingAuthor, Author
- In addition to the above, users with the following minimum access rights will also be added as members to a Microsoft 365 group. **Access rights**: ReadItems, CreateItems, FolderVisible, EditOwnedItems, DeleteOwnedItems
- Users with access right "Owner" will be added as owners to a group and users with other eligible access rights will be added as members.
- Security groups can't be added as members to Microsoft 365 groups. Therefore they'll be expanded, and then the individual users are added as members or owners to the groups based on the access rights of the security group.
- When users in security groups that have access rights over a public folder have themselves explicit permissions over the same public folder, explicit permissions are given preference. For example, consider a case in which a security group called "SG1" has members User 1 and User 2. Permission entries for the public folder "PF1" are as follows:

    - SG1: Author in PF1
    - User 1: Owner in PF1

        In this case, User 1 is added as an owner to the Microsoft 365 group.
- When the default permission of a public folder being migrated is 'Author' or above, the script will suggest setting the corresponding group's privacy setting as 'Public'.

This script can be run even after the lock-down of public folders, with parameter `ArePublicFoldersLocked` set to `$true`. In this scenario, the script will read permissions from the backup file that was created during lock-down.

### LockAndSavePublicFolderProperties.ps1

This script makes the public folders that are being migrated read-only. When mail-enabled public folders are migrated, they will first be mail-disabled and their SMTP addresses will be added to the respective Microsoft 365 groups. Then the permission entries will be modified to make them read-only. A backup of the mail properties of mail-enabled public folders, as well as the permission entries of all the public folders, will be copied, before performing any modification on them.

If there are multiple migration batches, a separate backup directory should be used with each mapping .csv file.

The following mail properties will be stored, along with respective mail-enabled public folders and Microsoft 365 groups:

- PrimarySMTPAddress
- EmailAddresses
- ExternalEmailAddress
- EmailAddressPolicyEnabled
- GrantSendOnBehalfTo
- SendAs Trustee list

The above mail properties will be stored in a .csv file, which can be used in the rollback process (if you want to return to using public folders, see How do I roll back to public folders from Microsoft 365 Groups? for more information). A snapshot of the mail-enabled public folders' properties will also be stored in a file called PfMailProperties.csv. This file isn't necessary for the rollback process, but can still be used for your reference.

The following mail properties are migrated to target group as part of the lockdown:

- PrimarySMTPAddress
- EmailAddresses
- SendAs Trustee list
- GrantSendOnBehalfTo

The script ensures that the PrimarySMTPAddress and EmailAddresses of migrating mail-enabled public folders will be added as secondary SMTP addresses of the corresponding Microsoft 365 groups. Also, SendAs and SendOnBehalfTo permissions of users on mail-enabled public folders will be given equivalent permission in the corresponding target groups.

### Access rights allowed

Only the following access rights will be allowed for users to ensure that the public folders are made read-only for all users. These are stored in **ListOfAccessRightsAllowed**.

- ReadItems
- CreateSubfolders
- FolderContact
- FolderVisible

1. The permission entries will be modified as follows:

    | Before lockdown | After lockdown |
    | --- | --- |
    | None | None |
    | AvailabilityOnly | AvailabilityOnly |
    | LimitedDetails | LimitedDetails |
    | Contributor | FolderVisible |
    | Reviewer | ReadItems, FolderVisible |
    | NonEditingAuthor | ReadItems, FolderVisible |
    | Author | ReadItems, FolderVisible |
    | Editor | ReadItems, FolderVisible |
    | PublishingAuthor | ReadItems, CreateSubfolders, FolderVisible |
    | PublishingEditor | ReadItems, CreateSubfolders, FolderVisible |
    | Owner | ReadItems, CreateSubfolders, FolderContact, FolderVisible |
2. Access rights for users without read permissions will be left untouched, and they'll continue to be blocked from read rights.
3. For users with custom roles, all the access rights that aren't in **ListOfAccessRightsAllowed** will be removed. If users don't have access rights from the allowed list after filtering, their access right will be set to 'None'.

There might be an interruption in sending emails to mail-enabled public folders during the time between when the folders are mail-disabled and their SMTP addresses are added to Microsoft 365 Groups.

### UnlockAndRestorePublicFolderProperties.ps1

This script will re-assign permissions back to public folders, based on the backup file that was taken during public folder lock-down. This script will also mail-enable public folders that had been mail-disabled, after it removes the folders' SMTP addresses from their respective Microsoft 365 groups. There might be slight downtime during this process.

## How do I roll back to public folders from Microsoft 365 Groups?

If you change your mind and want to return to using public folders after using Microsoft 365 Groups, the command listed below will restore your environment to the state it was pre-migration. A roll back can be performed as long as the backup files exist and as long as you didn't delete the public folders post-migration.

Run the following command. In this command:

- **BackupDir** is the directory where the backup files for permission entries, MEPF properties, and migration log files will be stored. Make sure you use the same location you specified in Step 6: Lock down the public folders to cut-over (public folder downtime required).
- **ArePublicFoldersOnPremises** is a parameter to indicate whether public folders are located on-premises or in Exchange Online.

```PowerShell
.\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $false
```

Any items added to the Microsoft 365 groups, or any edit operations performed in the groups, aren't copied back to your public folders. Therefore there will be data loss, assuming new data was added while the public folder was a group.

Note also that it's not possible to restore a subset of public folders, which means all of the public folders there were migrated should be restored.

The corresponding Microsoft 365 groups won't be deleted as part of the roll back process. You'll have to clean or delete those groups manually.