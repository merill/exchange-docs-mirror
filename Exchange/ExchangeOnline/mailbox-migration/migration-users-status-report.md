---
layout: Conceptual
title: Migration users status report in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migration-users-status-report
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.topic: upgrade-and-migration-article
author: AshaIyengar21
ms.author: serdars
ms.assetid: acbc7b28-6a20-4390-a6b0-107e4cddb999
ms.reviewer: 
description: You can use the Migration dashboard in the Exchange administration center (EAC) to display the migration status information for all users in a migration batch. You can also display detailed migration information for each user in a migration batch. This information, also called migration user statistics, can help you troubleshoot issues that might prevent the migration of a user's mailbox or mailbox items. You can display this migration status information for migration batches that are currently running, that have been stopped, or that are complete.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- GMA150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2024-03-15T00:00:00.0000000Z
locale: en-us
document_id: b1855efc-70ec-efef-0621-a032d079903c
document_version_independent_id: 3a311f88-aab0-da43-516f-3ac00e2e21ae
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migration-users-status-report.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migration-users-status-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migration-users-status-report.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: 70ddde50-4ed3-e373-7d1b-8c5c66551a59
---

# Migration users status report in Exchange Online | Microsoft Learn

You can use the Migration dashboard in the Exchange administration center (EAC) to display the migration status information for all users in a migration batch. You can also display detailed migration information for each user in a migration batch. This information, also called migration user statistics, can help you troubleshoot issues that might prevent the migration of a user's mailbox or mailbox items. You can display this migration status information for migration batches that are currently running, that have been stopped, or that are complete.

You can also use Exchange Online PowerShell to display migration user statistics. For more information, see:

- [Get-MigrationUser](/en-us/powershell/module/exchangepowershell/Get-MigrationUser)
- [Get-MigrationUserStatistics](/en-us/powershell/module/exchangepowershell/Get-MigrationUserStatistics)

## Migration users report in EAC

![Screenshot of the EAC Migration batches page, with the properties of a migration batch showing in the slideout pane with View Details link highlighted.](../exchangeonline/mailbox-migration/media/migration-batches-view-details2.png)

To access the migration users report for a migration batch in the [Exchange Admin center](https://admin.exchange.microsoft.com/#/), go to **Migration**, select the migration batch and then in the details pane, under **Migration details**, click **View details**.

![Screenshot of the EAC showing the specific page for the migration batch.](../exchangeonline/mailbox-migration/media/migrationbatches-image-3.png)

The name of the migration batch and the following commands are displayed at the top of the window.

| Command | Description |
| --- | --- |
| **Delete** | Delete the selected user from the list of migration users. |
| **Refresh** | Refresh the list of migration users to update the information displayed for the users in the migration batch. |
| **Resume migration** | Resume the migration of mailboxes that failed. The status is changed to **Starting**. |
| **Stop migration** | Stop the migration of mailboxes. After the batch is stopped, the status is changed to **Stopped**. |

Note

**Resume Migration/Stop Migration** button appears based on the status of the user selected.

### Columns in the list of migration users

| Column | Description |
| --- | --- |
| **Name** | The user's email address. |
| **Status** | The user's migration status. See the status descriptions in the table in the next section. |
| **Data consistency score** | Indicates the risk of data loss during migration. |
| **Items Synced** | The number of items in the user's on-premises mailbox that were successfully migrated to the Microsoft 365 or Office 365 mailbox. |
| **Items Skipped** | The number of items in the user's on-premises mailbox that weren't migrated to the Microsoft 365 or Office 365 mailbox. |

## Migration user statistics for a specific user in EAC

![Screenshot of EAC showing the migration batch properties for a specific user.](../exchangeonline/mailbox-migration/media/migrationbatches-image-2.png)

To view status information (also called migration user statistics) for a specific mailbox, mail contact, or distribution group, click on the mailbox, contact, or distribution group in the list. Status information for the selected mail object is displayed in the details pane. The following table describes each field displayed in the details pane.

| Field | Description |
| --- | --- |
| **Status** | Identifies the specific point in the migration process for each mail object in the migration batch. This status is more specific than the high-level status summary displayed in the list of migration users. The following list describes each status state. <br>- **Completed**: The migration process is successfully completed and all mailbox items were migrated to the cloud-based mailbox.<br>- **Queued**: The object is in a migration batch that is running, but the migration of the object hasn't started yet. Objects typically have a status of **Queued** when all of the connections in the migration endpoint associated with the migration batch are being used.<br>- **Synced**: The migration process successfully provisioned the Microsoft 365 or Office 365 mailbox and completed the initial synchronization where all mailbox items were copied to the cloud-based mailbox. For cutover Exchange migrations and IMAP migrations, this status can also indicate that incremental synchronization completed successfully.<br>- **Failed**: The provisioning or the initial synchronization of the mail object failed. If a Microsoft 365 or Office 365 mailbox is successfully created for a user, but the migration of mailbox items fails, the status for the user will be **Failed**. |
| **Skipped item details** | Click **Skipped item details** to display information about each item that was skipped for the selected user. The following information about each skipped item is displayed: <br>- **Date**: The time stamp of the mailbox item.<br>- **Subject**: The subject line of the message.<br>- **Kind**: The type of error that caused the item to be skipped.<br>- **Folder name**: The folder where the skipped item is located. |
| **Data migrated** | The total amount of data (in bytes and megabytes (MB)) for the mailbox items that have been migrated to the Microsoft 365 or Office 365 mailbox. This number includes items migrated in both the initial and incremental synchronizations. This field doesn't have a value for IMAP migrations. |
| **Migration rate** | The average transfer rate (in bytes or MB per minute) of data copied to the Microsoft 365 or Office 365 mailbox. This field doesn't have a value for IMAP migrations. |
| **Error** | If the migration for the user failed, this field displays a description of the error. This error description is also included in the Migration Errors report. |
| **Report** | Click **Download the report for this user** to open or save a detailed migration report that contains diagnostic information about the migration status of the user. You or Microsoft Support can use the information in this report to troubleshoot failed migrations. |
| **Last successful sync date** | The last time that any new items in the on-premises mailbox were copied to the cloud-based mailbox. |