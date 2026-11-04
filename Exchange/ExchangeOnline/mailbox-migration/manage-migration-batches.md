---
layout: Conceptual
title: Manage migration batches in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/manage-migration-batches
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
ms.assetid: d164b35c-f624-4f83-ac58-b7cae96ab331
ms.reviewer: 
description: Admin can learn how to migrate Exchange mailboxes, IMAP mailboxes, and Google Workspace mailboxes, calendars, and contacts to Microsoft 365 or Office 365.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2024-03-15T00:00:00.0000000Z
locale: en-us
document_id: 89a684ff-29af-b532-deea-01fecbd6b8cb
document_version_independent_id: a90ceb5c-8553-2636-ab85-14688435ee4d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/manage-migration-batches.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/manage-migration-batches
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/manage-migration-batches.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: 27d1a2d3-4952-4b50-e647-c556878dbd64
---

# Manage migration batches in Exchange Online | Microsoft Learn

You can use the Migration dashboard in the Microsoft 365 or Office 365 Exchange admin center (EAC) to manage mailbox migration to Microsoft 365 or Office 365 using a cutover or staged Exchange migration. You can also use the Migration dashboard to migrate the contents of users' mailboxes from an on-premises IMAP server, or the contents of Google Workspace (formerly G Suite) users' mailboxes, calendars, and contacts to existing Microsoft 365 or Office 365 mailboxes. The Migration dashboard displays statistics about the overall migration in addition to statistics about a specific migration batch. You can create, start, stop, pause, and edit migration batches.

## Migration batches

Migration batches that are created are listed in the migration queue. The following columns display information about each migration batch.

![Screenshot of Migration Batches page on Exchange Admin Center.](../exchangeonline/mailbox-migration/media/migrationbatches-image-1.png)

| Column | Description |
| --- | --- |
| **Name** | The name of the migration batch that was defined when it was created. |
| **Status** | The status of the migration batch. The following list describes the different status states for migration batches, along with what you can do with migration batches in each of these states: <br>- **Stopped**: Either the migration batch was created and not started, or it was stopped after running for some period of time. In this state, you can start, edit, or delete it.<br>- **Syncing**: The migration batch was started, and mailboxes in the migration batch are being actively migrated. When a migration batch is in this state, you can stop it.<br>- **Stopping**: Immediately after you run [Stop-MigrationBatch](/en-us/powershell/module/exchangepowershell/Stop-MigrationBatch) cmdlet.<br>- **Starting**: Immediately after you run [Start-MigrationBatch](/en-us/powershell/module/exchangepowershell/Start-MigrationBatch) cmdlet.<br>- **Completing**: Immediately after you run [Complete-MigrationBatch](/en-us/powershell/module/exchangepowershell/Complete-MigrationBatch) cmdlet.<br>- **Removing:** Immediately after you run [Remove-MigrationBatch](/en-us/powershell/module/exchangepowershell/Remove-MigrationBatch) cmdlet.<br>- **Synced**: The migration batch completed an initial sync of the data. A migration batch in this state might contain errors if mailboxes weren't migrated. For most types of migrations, the remote/on-premises mailboxes and the corresponding Microsoft 365 or Office 365 mailboxes are synchronized every 24 hours during incremental synchronization.<br>- **Completed**: The migration batch is complete.<br>- **Synced with errors**: The migration batch completed an initial sync of the data, but some mailboxes failed migration. Mailboxes that were successfully migrated in migration batches with errors are still synchronized every 24 hours during incremental synchronization. |
| **Data consistency score** | Indicates the risk of data loss during migration. |
| **Percentage synced** | Indicates the percentage of mailboxes that were successfully migrated in migration batches. |
| **Total** | Indicates the number of mailboxes in the migration batch. |
| **Synced** | Indicates the number of mailboxes that were successfully migrated. |
| **Finalized** | The number of finalized mailboxes in the migration batch. Finalization is done only for migration batches for remote move migrations in an Exchange hybrid deployment. For more information about the finalization process, see [Complete-MigrationBatch](/en-us/powershell/module/exchangepowershell/Complete-MigrationBatch). |
| **Failed** | The number of mailboxes in the migration batch for which the migration failed. You can display information about specific mailboxes that have migration errors. For more information, see [Migration users status report](migration-users-status-report). |

Important

Migration batches with a status of **Synced** that have no administrator-initiated activity (for example, no administrator stopped and restarted a migration batch or edited a migration batch) for the last 60 days will be stopped. All batches with **Stopped** or **Failed** status are removed after 90 days. All batches with **Completed** status are removed after 60 days.

The Migration dashboard contains a set of commands that you can use to manage migration batches. After you create a migration batch, you can select it, and then select one of the following commands.

![Screenshot of the Migration batches page on EAC, with the toolbar buttons highlighted.](../exchangeonline/mailbox-migration/media/migration-dashboard-commands.png)

| Command | Description |
| --- | --- |
| **Add migration batch** | Create a new migration batch. Use this command to migrate on-premises mailboxes to Microsoft 365 or Office 365 (also called onboarding) or to migrate Microsoft 365 or Office 365 mailboxes back to your on-premises Exchange organization in a hybrid deployment. |
| **Stop migration** | Stop the migration of mailboxes. After the batch is stopped, the status is changed to **Stopped**. |
| **Complete migration batch** | Complete the migration of mailboxes. After the migration is completed, the status is changed to **Completed**. |
| **Delete** | Delete a migration batch after you verify that all mailboxes in the migration batch were successfully migrated. Verify also that mail is being routed directly to cloud-based mailboxes after you configured your MX record to point to Microsoft 365 or Office 365. When you delete a migration batch, Microsoft 365 or Office 365 cleans up any records related to the migration batch and removes it from the list. |
| **Edit Batch** | Edit an existing migration batch. You can change the finalization semantics of batches that support finalization. You can also change the migration endpoint used for the migration batch. |
| **Resume migration** | Start an existing migration batch. After the batch is started, the status is changed to **Syncing**. <br> Also, resume the running of a migration batch that was paused and has a status of **Stopped**. If there are errors for a migration batch, you can restart it with this command, and Microsoft 365 or Office 365 attempts to migrate the mailboxes that failed. |
| **Refresh** | Refresh the Migration dashboard to update the information displayed for the overall migration statistics, the list of migration batches, and the statistics for the selected migration batch. |

### Migration batch statistics

The details pane in the Migration dashboard displays the following information about the selected migration batch.

![Screenshot of the Migration batches page on EAC with a batch selected and the property pane open that shows the migration details.](../exchangeonline/mailbox-migration/media/migrationbatches-image.png)

| Field | Description |
| --- | --- |
| **Type** | Indicates the migration type of the selected migration batch. The value of this field also denotes the type of migration endpoint associated with the migration batch. <br>**Exchange Outlook Anywhere**: The migration batch is either a cutover Exchange migration or a staged Exchange migration. <br><br>**ExchangeRemoteMove**: The migration batch is either an onboarding or offboarding remote move migration in an Exchange hybrid deployment. <br><br>**Gmail**: The migration batch is a Google Workspace migration. |
| **Direction** | Indicates if mailboxes are being migrated to Microsoft 365 or Office 365 or to your on-premises Exchange organization. <br>**Onboarding**: Indicates that mailboxes are being migrated to Microsoft 365 or Office 365. Onboarding migration types are staged migrations, cutover migrations, IMAP migrations, Google Workspace migrations, and onboarding remote move migrations. <br><br>**Offboarding**: Indicates that Microsoft 365 or Office 365 mailboxes are being migrated to your on-premises Exchange organization. Offboarding remote move migrations are the only type of offboarding migration. |
| **Status** | The current state of the selected migration batch. <br>**Completed**<br><br>**Syncing**<br><br>**Stopped**<br><br>**Synced**<br><br>**Synced with errors**<br><br> See the previous description of each of these states. |
| **Complete migration batch** | Select **Complete migration batch** to complete the migration of the selected batch. <br> This action is available only if the status of the migration batch is **Synced/Synced with errors**. |
| **View details** | Select **View details** to display status information for each mailbox in the migration batch. For more information, see [Migration users status report](migration-users-status-report). |
| **Synced mailboxes** | The number of mailboxes out of the total number of mailboxes in the migration batch that successfully completed initial synchronization. This field is updated during the migration. |
| **Finalized mailboxes** | The number of mailboxes out of the total number of mailboxes in the migration batch that were successfully finalized. Finalization only occurs in onboarding and offboarding remote move migrations. |
| **Failed mailboxes** | The number of mailboxes that failed initial synchronization. |
| **Created by** | The email address of the Microsoft 365 or Office 365 administrator who created the migration batch. |
| **Created time** | The date and time when the migration batch was created. |
| **Start time** | The date and time when the migration batch was started. |
| **Start after** | The date and time when the migration batch is scheduled to start later. |
| **Complete after** | The date and time when the migration batch is completed. |
| **Last synced time** | The last time the migration batch was restarted or the last time that incremental synchronization was performed for the batch. As previously stated, incremental synchronization occurs every 24 hours. |
| **Associated endpoint** | The name of the migration endpoint being used by the migration batch. You can select **View details** to view the migration endpoint settings. You can also edit the settings if none of the migration batches using the endpoint are currently running. |