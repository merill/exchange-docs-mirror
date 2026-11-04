---
layout: Conceptual
title: Track and Prevent Migration Data Loss in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/track-prevent-data-loss-dcs
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
description: 'Summary: Track and prevent migration data loss with DataConsistencyScore'
ms.topic: overview
author: AshaIyengar21
ms.author: serdars
ms.assetid: 
ms.reviewer: 
ms.collection: exchange-server
audience: ITPro
ms.service: exchange-server-it-pro
ms.date: 2024-03-15T00:00:00.0000000Z
locale: en-us
document_id: b40bce01-0b1f-1952-5198-d5a15211b533
document_version_independent_id: 3f0ac568-cfbd-5255-d803-b7883c32c50f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/track-prevent-data-loss-dcs.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/track-prevent-data-loss-dcs
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/track-prevent-data-loss-dcs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 8994d9aa-6284-0419-9dbc-44ccd7f39221
---

# Track and Prevent Migration Data Loss in Exchange Online | Microsoft Learn

When migrating to Exchange Online, the migration process might reveal inconsistencies that pose a risk of data loss. Such inconsistencies can occur during almost any migration, whether from on-premises Exchange Server, Public Folders, PST file imports, Google Workspace (formerly G Suite), or third-party IMAP servers. The migration process tracks and reports on any possible instances of data loss by generating a **DataConsistencyScore**.

## Migration and Data Consistency Score

When you attempt a migration, any inconsistencies between the source and target data stores will count towards the DataConsistencyScore. This score is then used to determine whether an Exchange Online migration will complete successfully or if intervention is needed.

There are 4 possible grades that are derived from the DataConsistencyScore.

| Grade | Description | Approval Required? |
| --- | --- | --- |
| **Perfect** | No inconsistencies noted during migration. | No approval is required. |
| **Good** | At least 1 inconsistency noted, but the data loss wasn't impactful. For example, if only metadata or folder permissions were lost during migration. | No approval is required |
| **Investigate** | A small amount of noticeable data loss was detected, caused by some common inconsistency types. | Approval of skipped items is required for migration types that have a built-in finalization phase, such as Hybrid migrations or Google Workspace onboarding. |
| **Poor** | Major data loss was detected. | Contact Microsoft Support for assistance. Approval of skipped items is required for migration types that have a built-in finalization phase. |

You can view the DataConsistencyScore for your migration in the Exchange admin center at a per-user and per-batch level. You can also find it using PowerShell cmdlets; the *DataConsistencyScore* property exists on **MigrationBatch**, **MigrationUser**, and **RequestStatistics** objects.

## How the DataConsistencyScore is calculated

There are various thresholds used to determine the DataConsistencyScore. Microsoft is constantly tuning these thresholds to ensure that problematic data loss doesn't occur during migrations. The details of these thresholds aren't presented to Exchange Online administrators.

For batches, the DataConsistencyScore is equal to the worst DataConsistencyScore of any user within that batch. This behavior helps administrators know immediately whether there's any data loss that should be investigated.

## Guidance for grades of Investigate or Poor

For migrations from third-party IMAP servers, PST file imports, or on-premises Exchange Server using Cutover or Staged Exchange Migration, there's no need to approve the set of skipped items. Approval of migrations with a score of Investigate or worse is required for the completion of Remote Move, Public Folder, and Google Workspace migrations.

If the migration receives a grade of **Investigate**, then you can approve skipped items manually to allow the migration to succeed.

If you're using batches, then run:

```PowerShell
Set-MigrationBatch -ApproveSkippedItems or Set-MigrationUser -ApproveSkippedItems
```

If you're using MoveRequests directly, then run:

```PowerShell
Set-MoveRequest -SkippedItemApprovalTime $([DateTime]::UtcNow)
```

For a batch scored as **Investigate**, approving the migration allows you to complete all migrations in the batch with a score of Perfect, Good, or Investigate.

For a batch scored as **Poor**, approving the migration allows you to complete all migrations in the batch with a score of Perfect, Good, or Investigate, but won't approve any migration in the batch with a score of Poor.

If the migration fails with a grade of **Poor**, you can't force the migration to succeed. Please contact Microsoft Support for assistance.

## How to see which items weren't migrated in EAC

1. In the Exchange admin center, go to **Migration**.

    ![Screenshot of EAC showing the details pane for a specific migration batch, with the View Details link highlighted.](../exchangeonline/mailbox-migration/media/migration-batches-view-details2.png)
2. Select the batch you would like to inspect. Click **View details** in the information pane on the right.

    ![Screenshot of EAC showing the details for a specific user in a migration batch with the View Skipped item details link highlighted.](../exchangeonline/mailbox-migration/media/migration-batches-view-details1.png)
3. Select the user you would like to inspect. Select **Skipped item details** in the information pane on the right.

### Using Exchange Online PowerShell

1. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
2. Determine the identity of the user you wish to investigate.
3. Run the following commands:

    ```PowerShell
    $userStats = Get-MigrationUserStatistics -Identity user@fabrikaminc.net -IncludeSkippedItems
    $userStats.SkippedItems | ft -a Subject, Sender, DateSent, ScoringClassifications
    ```
4. Inspect the information about skipped items provided in the SkippedItems property on the userStats object.