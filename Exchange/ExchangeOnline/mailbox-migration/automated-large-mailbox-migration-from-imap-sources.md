---
layout: Conceptual
title: Perform automated migration of large mailboxes from Google or IMAP to Microsoft 365 Exchange | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/automated-large-mailbox-migration-from-imap-sources
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: serdars
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Learn how to automatically migrate large mail data from Google or other IMAP source to Microsoft 365 Exchange primary and archive mailboxes.
ms.custom: seo-marvel-jun2021
ms.date: 2024-02-15T00:00:00.0000000Z
locale: en-us
document_id: 94c54597-d19a-de4d-c561-a55496feeb5f
document_version_independent_id: 6c1d3006-3cf1-def0-81ad-0c9f26bb8f02
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/automated-large-mailbox-migration-from-imap-sources.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/automated-large-mailbox-migration-from-imap-sources
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/automated-large-mailbox-migration-from-imap-sources.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 66711544-d6c3-cefb-7d72-b21ced9aca88
---

# Perform automated migration of large mailboxes from Google or IMAP to Microsoft 365 Exchange | Microsoft Learn

## Introduction

This document provides comprehensive guidance for tenant administrators on migrating emails from Internet Mail Access Protocol (IMAP) sources, including Gmail, to Microsoft 365 Primary and [Archive mailboxes](/en-us/purview/archive-mailboxes) concurrently. Known as Large Mailbox Onboarding (LMO), this solution empowers tenant admins to seamlessly migrate mailboxes exceeding 100 GB from IMAP sources by harnessing the auto-expanding archives feature within Microsoft 365.

Note

- For migrating regular sized (&lt;100G) mailboxes from IMAP sources, please use [Exchange Admin Center (EAC) migration features](https://admin.exchange.microsoft.com/#/migrationbatch). If your source is GMail, you can also use [GMail migration features in M365 Admin Center (MAC).](https://portal.office.com/Adminportal/Home/?#/featureexplorer/migration/GsuiteMailboxMigration)
- Currently, LMO is available only through PowerShell cmdlets. Automated UI experience will be added later.

Important

- Microsoft 365 offers a resultant cumulative mailbox size of up to 1.6 TB. This includes 100 GB of Primary Mailbox, and 1.5 TB of Archives (including 100 GB Main Archive). For more information, see [archive-mailboxes](/en-us/purview/archive-mailboxes) and [autoexpanding-archiving](/en-us/purview/autoexpanding-archiving).
- You require at least "Recipient Management" role to execute this. Read through the documentation, especially the linked documents to help kickstart migrations for large mailboxes.
- Run the cmdlet to disable ELCProcessing before creating LMO migration batch. If it's not disabled, the folders might be moved by ELC during LMO, and the LMO migration might be blocked. **Set-Mailbox $user -ELCProcessingDisabled:$true**

## What do you need to know before you begin?

Before creating the migration, you need to know:

1. The list of users with large mailboxes (&gt;100 GB) on the source side.
2. If you have a large mailbox, the content (time, type) that you intend to migrate and to where (primary, main archive, auxiliary archives).

For each user, the content can be selected based on time range or folder. See the following examples.

1. **Time-range-based mapping**:

    **Table 1**

    | Time range | Target Mailbox |
    | --- | --- |
    | **After 2023/01/01** | Primary |
    | **From 2022/01/01 to 2023/01/01** | Archive mailbox 1 |
    | **From 2021/01/01 to 2022/01/01** | Archive mailbox 2 |
    | **Before 2021/01/01** | Archive mailbox 3 |
2. **Folder-based mapping**:

    **Table 2**

    | Folder Name | Target Mailbox |
    | --- | --- |
    | **Inbox** | Primary |
    | **SentItems** | Primary |
    | **DeletedItems** | Archive mailbox 1 |

    Important

    **Well-Known Folders**: The folders that come under this categorization include but are not limited to Inbox, Deleted Items, Sent Items, and Drafts. Full list [here.](/en-us/powershell/module/exchangepowershell/new-migrationbatch#-includefolders)

    Except Deleted Items, all these well-known folders and customer created labels/folders can be migrated to either primary or any archive mailboxes (both Main Archive and Auxiliary Archives). However, Deleted Items of a user **can be migrated only to** the Primary or Main Archive, and not Auxiliary Archive.

If a single source folder is larger than 100 GB, it can't fit in one Exchange mailbox, so the end user needs to separate it to several smaller folders.

## Prepare XML file

To migrate large mailboxes automatically, you need to prepare an XML file that advises the system on the content-to-mailbox mapping.

Download a sample XML file here [Download a copy of the large mailbox migration XML mapping file](https://download.microsoft.com/download/7/d/d/7dd8c93f-8289-4521-9a46-614059687cea/mapping.xml) and take a quick look before you proceed.

### Mapping tool

Mailbox analysis tool is provided to **automatically** generate the XML mapping file after running analysis on the source mailbox. See [Analyze source mailboxes before migrating from Google Workspace or IMAP](source-mailbox-analysis-google-imap) for guidance.

Important

It's highly recommended to use the Mailbox Analysis tool before migrating large mailboxes.

Note

The analysis tool runs on the monthly level. It can't split a single month into a smaller time range if a single month of data is larger than 100 GB. If that is the case, the administrator must manually and carefully create the XML mapping file.

### Time-range-based mapping

In the XML file, you need to specify the time range in ContentFilter. Unlike [Filterable properties for the -ContentFilter parameter](../filterable-properties-for-the-contentfilter-parameter), only Received property is supported, which means that the filtering is based on the "Received" parameters and not the "Sent" parameters in the mail item metadata. For example, filtering is executed on the Received TimeStamp (time when the mail landed in the user's mailbox) vs the Sent TimeStamp (time when the sender of the mail sent it to the user) of a mail, which the users received in their mailbox.

Four operators are supported:

- gt: greater than
- ge: greater than or equal to
- lt: less than
- le: less than or equal to

The value of EmailAddress should be the SMTP address of EXO user.

The value of Target can be the following four types:

- Primary
- MainArchive
- AuxArchive\* (AuxArchive1, AuxArchive2, AuxArchive3)
- GUID-of-Existing-Mailbox

Following is the XML file for time range based mapping for the example shown in table 1.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Users>
    <User EmailAddress="user1@contoso.onmicrosoft.com">
        <Folder Name="/*">
            <Mapping ContentFilter="Received -gt '2023/1/1'" Target="Primary" />
            <Mapping ContentFilter="Received -gt '2022/1/1' -and Received -le '2023/1/1'" Target="MainArchive" />
            <Mapping ContentFilter="Received -gt '2021/1/1' -and Received -le '2022/1/1'" Target="AuxArchive1" />
            <Mapping ContentFilter="Received -le '2021/1/1'" Target="AuxArchive2" />
        </Folder>
   </User>
</Users>
```

You can use [Get-MailboxLocation](/en-us/powershell/module/exchangepowershell/get-mailboxlocation) to get the mailbox 'GUID' of a user's primary mailbox and archive mailboxes if any, and put the mailbox 'GUID' in the Target property.

Important

If the time range in the XML file is changed during the migration process, there may be duplicated items. We recommend tenant admin have clear communication with end users before starting the migration.

Important

When you create time ranges, ensure that you use continuous time ranges. If it's not continuous, there will be missing items that the migration process can't detect.

Note

Multiple mappings that use the same start month and end month but target different archive mailboxes aren't supported.

**Unsupported mapping example 1**

```xml
<Mapping ContentFilter="Received -ge '2022-01-01' -and Received -lt '2022-01-15'" Target="AuxArchive0" />
<Mapping ContentFilter="Received -ge '2022-01-15' -and Received -lt '2022-01-31'" Target="AuxArchive1" />
```

**Supported mapping example 2**

The mapping in **Unsupported mapping example 1** can be restructured by adjusting the date boundaries so that the mappings no longer share the same start and end months.

```xml
<Mapping ContentFilter="Received -ge '2021-12-31' -and Received -lt '2022-01-15'" Target="AuxArchive0" />
<Mapping ContentFilter="Received -ge '2022-01-15' -and Received -lt '2022-02-01'" Target="AuxArchive1" />
```

### Folder-based mapping

In the XML file, you need to specify the folder names in Name properties.

The value of EmailAddress should be the SMTP address of EXO user.

The value of Target can be the following four types:

- Primary
- MainArchive
- AuxArchive\* (AuxArchive1, AuxArchive2, AuxArchive3)
- GUID-of-Existing-Mailbox

Following is an example of the XML file for folder based mapping for the example shown in Table 2.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Users>
    <User EmailAddress="user1@contoso.onmicrosoft.com">
        <Folder Name="#Inbox#/*">
            <Mapping Target="Primary" />
        </Folder>
        <Folder Name="#SentItems#/*">
            <Mapping Target="Primary" />
        </Folder>
        <Folder Name="#DeletedItems#/*">
            <Mapping Target="MainArchive" />
        </Folder>
   </User>
</Users>
```

## Create large mailbox migration using PowerShell

LMO migration steps are very similar to regular IMAP migration and GWS migration. Following are the links to learn more about the prerequisites and steps.

- [What you need to know about migrating your IMAP mailboxes to Microsoft 365 or Office 365](migrating-imap-mailboxes/migrating-imap-mailboxes)
- [Perform a Google Workspace (formerly G Suite) migration to Microsoft 365 or Office 365](perform-g-suite-migration)

To create a large mailbox migration batch, you need to use `New-MigrationBatch` with `-XMLData` parameter.

**Example:**

```powershell
New-MigrationBatch -SourceEndpoint MigEndpoint -Name LMO\_User1 -CSVData $([System.IO.File]::ReadAllBytes(".\user1.csv")) -XMLData $([System.IO.File]::ReadAllBytes(".\user1mapping.xml")) -TargetDeliveryDomain "contoso.onmicrosoft.com" -AutoStart
```

## Monitor LMO migration progress

### Check migration batch, migration user status

To check batch’s status, use Get-MigrationBatch. To check user’s status, use Get-MigrationUser and Get-MigrationUserStatistics.

```powershell
Get-MigrationBatch $batchNameOrId | Format-Table Identity, Status, IsLargeArchiveOnboarding
Get-MigrationUser -BatchId $batchNameOrId                                             # to get all migration job items in a batch
Get-MigrationUser -EmailAddress $user                                                 # to get all migration job items for this user
Get-MigrationUserStatistics $migrationUserId -IncludeSkippedItems -IncludeReport
```

### Understand migration user Identities

In LMO migration, a user has multiple migration user objects. Each migration user object corresponds to a specific source-to-target migration path. The Identity value indicates the source mailbox location and the target mailbox location associated with that migration user.

- **"Primary"** represents migration from the source mailbox to the target Primary mailbox.
- **"AuxArchive0"** represents migration from the source mailbox to the target AuxArchive0 mailbox.

Use the following command to view migration user identities and status:

```powershell
Get-MigrationUser -BatchId $batchNameOrId  | Format-Table Identity, Status

# Example output:

Identity                                   Status
--------                                   ------
alice@contoso.com/Primary                  Synced
alice@contoso.com/AuxArchive0              Synced
alice@contoso.com/AuxArchive1              Synced
```

During migration, monitor the item synchronization progress for each migration user. Use the following command to review the migration status and item counts:

```powershell
Get-MigrationUser -BatchId $batchNameOrId | Format-Table Identity, Status, SkippedItemCount, SyncedItemCount
```

## Best Practices

### Use a single CSV file per user

Each LMO user can create multiple migration users and migration requests. To simplify monitoring, troubleshooting, and error isolation, create a separate LMO migration batch for each user by including only one user in the CSV file.

### Manage users using LMO at the same time

Each LMO user can create multiple migration users and migration requests. Running too many LMO users concurrently can increase load on the source Gmail or IMAP environment, causing source-side throttling and slower migration performance. Consider onboarding users in smaller batches and review your migration concurrency settings before scaling up.

### Performance

Before beginning a migration of any mailbox, but particularly for large mailboxes, be familiar with the concepts and recommendations in the [Microsoft 365 email migration performance and best practices guide](/en-us/exchange/mailbox-migration/office-365-migration-best-practices).

## Troubleshooting

### Determine whether a batch is an LMO batch

LMO migration batches have the `IsLargeArchiveOnboarding` property set to True.

```powershell
Get-MigrationBatch $batch | Format-Table IsLargeArchiveOnboarding
```

### Retrieve migration errors

Use the following commands to view the migration user's error summary and detailed error information.

```powershell
Get-MigrationUser -BatchId $lmoBatchId | Format-Table Identity, Status, ErrorSummary

Get-MigrationUser $migrationUserId | Format-Table ErrorSummary
Get-MigrationUserStatistics $migrationUserId | Format-List Error
```

### Quota-Related Failures

If a LMO migration fails because of mailbox quota limits, start by identifying which target mailbox quota was exceeded. In most cases, troubleshooting involves three steps:

- Verify the target mailbox quota configuration.
- Validate the mailbox analysis results used to create the XML mapping.
- Verify the actual source mailbox content and size.

Following these steps helps determine whether the failure is caused by mailbox configuration, mailbox growth after analysis, or unbalanced content distribution in the XML mapping.

#### 1) Verify Target Mailbox Quotas

Review the target mailbox configuration and quota settings:

```powershell
Get-Mailbox $user | Format-List *Quota
```

Determine which mailbox location exceeded its quota, such as Primary, MainArchive, or an AuxArchive mailbox. Verify that the target mailbox configuration matches the intended XML mapping design.

#### 2) Determine How the XML Mapping Was Created

After identifying the affected mailbox location, determine how the XML mapping file was created:

- If the XML file was created manually, the quota failure typically indicates that the content distribution is unbalanced. Review the mappings and redistribute content across mailbox locations.
- If the XML file was automatically generated by the Mailbox Analysis Tool, validate the analysis results against the actual mailbox statistics and mailbox contents

#### 3) Validate mailbox-level analysis results

For Gmail migrations, the mailbox size reported in the Gmail admin portal may differ from the size shown in the mailbox analysis results. This difference is expected because Gmail labels are converted to **Exchange Online folders** during migration. As a result, the mailbox analysis tool estimates the size of the mailbox **after label-to-folder conversion**, reflecting how the content will be represented in Exchange Online rather than the source mailbox size reported by Gmail.

To review mailbox analysis results, run the following commands:

```powershell
$stats = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult
$stats.MailboxAnalysisResult.AnalysisResultDataRows | Format-Table -AutoSize SourceMailbox, FolderIsSelected, FolderPath, StartTime, ItemCount, ItemSize
```

#### 4) Validate folder-level analysis results

Get per-label data from Gmail side and compare the size with the per-folder analysis result to ensure the analysis job works as expected.

To review folder-level analysis results, run the following commands:

```powershell
$stats = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult -IncludeFolderDetails
$stats.MailboxAnalysisResult.AnalysisResultDataRows | Format-Table -AutoSize SourceMailbox, FolderIsSelected, FolderPath, StartTime, ItemCount, ItemSize
```

#### 5) Validate XML mapping ranges

If a specific mapping is suspected to exceed a mailbox quota, run mailbox analysis for the corresponding date range and compare the results with the XML mapping.

```powershell
# Items from August 2022 through January 2023 (i.e., before February 2023)
$stats_select = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult -ItemsStartTime "2022/08/01" -ItemsEndTime "2023/02/01"
$stats_select.MailboxAnalysisResult.AnalysisResultDataRows | Format-Table -AutoSize
```

### Get MRS request GUID

To correlate an LMO migration user with its underlying MRS request, use the following command to retrieve request GUID and corresponding mailbox target information for further troubleshooting.

```powershell
Get-MigrationUser -Identity $migrationUser  | Format-Table Identity, RequestGuid, MailboxGuid, WorkflowStep, WorkflowStage
```

If `RequestGuid` is empty, the MRS request hasn't been created. In this case, the failure likely occurred before MRS processing started, such as during validation, mailbox provisioning, or request injection. If `RequestGuid` is populated, use the GUID to investigate the corresponding MRS request and review its detailed status, failure information and report.

### Information to Collect for Support Requests

If additional investigation is required and you need to open a support case, collect the following information:

- The XML mapping file used for the migration.
- The migration batch ID and migration user ID.
- Mailbox analysis results.
- Relevant migration error messages, migration user statistics, and MRS request information.

The XML mapping file and mailbox analysis results are the most important artifacts for investigating content distribution and quota-related issues.