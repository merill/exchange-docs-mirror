---
layout: Conceptual
title: Analyze source mailboxes before migrating from Google Workspace or IMAP to Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/source-mailbox-analysis-google-imap
Manager: aleeming
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: rahu
author: Rahu
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Learn how to analyze Google Workspace or IMAP mailboxes before migrating to Exchange Online. Use the analysis results to generate a content mapping file for large mailbox migrations.
ms.date: 2026-09-25T00:00:00.0000000Z
locale: en-us
document_id: 985f1255-d928-a484-3e02-b47c6bef330f
document_version_independent_id: e8366af6-15d7-68b0-e405-8ddbef3f837f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/source-mailbox-analysis-google-imap.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/source-mailbox-analysis-google-imap
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/source-mailbox-analysis-google-imap.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 9a218c8f-1591-a0a3-66b8-3222e7a00f92
---

# Analyze source mailboxes before migrating from Google Workspace or IMAP to Microsoft 365 | Microsoft Learn

Before migrating mailboxes from Google Workspace or an Internet Message Access Protocol (IMAP) source to Exchange Online (EXO), you can run a **Mailbox Analysis Request** to prescan the source mailbox content. The analysis produces a report of folder paths with item counts and sizes, which helps you:

- Identify oversized mailboxes before migration starts.
- Decide how to distribute content across primary, Main Archive, and Auxiliary Archive mailboxes in EXO.
- Generate an XML mapping file for [automated large mailbox migration](automated-large-mailbox-migration-from-imap-sources).

## What you need to know before you begin

- This feature is supported only for **Google Workspace** and **IMAP** migrations.
- It's available through **Exchange Online PowerShell** only. The Exchange Admin Center (EAC) doesn't support this feature yet.
- For Google Workspace, a simplified version of this analysis is also available through [Gmail migration in the Microsoft 365 Admin Center](custom-migration-small-business-from-gmail).
- The analysis produces two outputs:
    - **Analysis result**: folder paths with item counts and sizes. Folders with more than 1 million items or more than 100 GB are flagged with a warning.
    - **Mapping result**: a ready-to-use XML content mapping file that distributes source data across EXO mailboxes within per-mailbox quota limits.
- **For IMAP analysis:** A target EXO mailbox must already be created for the user before you run an analysis.
- **For Google Workspace analysis:** The analysis batch includes a provisioning step that can automatically convert a mail-enabled user (MailUser) into a mailbox. If the user already has an EXO mailbox, it's used as-is.

## Step 1: Create a mailbox analysis batch

The source endpoint and CSV format for a mailbox analysis batch are the same as for a standard Gmail or IMAP migration batch. To learn more about migration endpoints, see [Get-MigrationEndpoint](/en-us/powershell/module/exchange/get-migrationendpoint). For CSV file format details, see [CSV files for mailbox migration](csv-files-for-migration).

Set these variables before running the command:

```powershell
$endpointID = ""   # Identity of the IMAP or Gmail migration endpoint
$batchName  = ""   # Unique, descriptive name for this analysis batch
$csvPath    = ""   # Path to the CSV file listing EXO users to analyze
```

Create the analysis batch using [New-MigrationBatch](/en-us/powershell/module/exchange/new-migrationbatch) with the `-Analyze` parameter:

```powershell
New-MigrationBatch -Analyze -SourceEndpoint $endpointID -AutoStart -Name $batchName `
    -CsvData ([System.IO.File]::ReadAllBytes($csvPath))
```

**Example:**

```powershell
PS C:\> $endpointID = "IMAP_endpoint"
PS C:\> $batchName  = "IMAP_Analysis_Batch1"
PS C:\> $csvPath    = "C:\temp\IMAP_analyze.csv"

PS C:\> New-MigrationBatch -Analyze -SourceEndpoint $endpointID -AutoStart -Name $batchName `
    -CsvData ([System.IO.File]::ReadAllBytes($csvPath))

Identity             Status  Type          TotalCount
--------             ------  ----          ----------
IMAP_Analysis_Batch1 Syncing ImapAnalysis  1
```

## Step 2: Check analysis batch and user status

To check the status of the batch:

```powershell
Get-MigrationBatch $batchName
```

To check the estimated total item count and size for each user in the batch:

```powershell
Get-MigrationUser -BatchId $batchName | Format-Table Identity, Status, Estimate*
```

| Column | Description |
| --- | --- |
| `Identity` | Migration user in the batch |
| `Status` | `Syncing` while analysis is running; `Completed` when done |
| `EstimatedTotalCount` | Estimated total item count in the source mailbox |
| `EstimatedTotalSize` | Estimated total size in bytes |
| `EstimatedArchiveCount` | Estimated archive item count (if source has an archive) |
| `EstimatedArchiveSize` | Estimated archive size in bytes (if source has an archive) |

**Example:**

```powershell
PS C:\> Get-MigrationUser -BatchId $batchName | Format-Table Identity, Status, Estimate*

Identity                      Status    EstimatedTotalCount EstimatedTotalSize EstimatedArchiveCount EstimatedArchiveSize
--------                      ------    ------------------- ------------------ --------------------- --------------------
IMAPMailbox@contoso.com       Completed 1335                135824984515
```

To convert the size to GB:

```powershell
PS C:\> 135824984515 / 1GB
126.496874275617
```

## Step 3: View the analysis results

Once `Get-MigrationUser` shows `Status = Completed`, use `Get-MailboxAnalysisRequestStatistics` to view the detailed results.

Set the user variable:

```powershell
$user = ""   # Identity of the migration user to analyze
```

### Aggregated result (totals only)

```powershell
$stats = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult
$stats.MailboxAnalysisResult.AnalysisResultDataRows | Format-Table -AutoSize `
    FolderIsSelected, FolderPath, StartTime, ItemCount, ItemSize
```

**Example output:**

```
FolderIsSelected FolderPath StartTime ItemCount ItemSize
---------------- ---------- --------- --------- --------
                 Total                1335      126.5 GB (135,824,984,515 bytes)
```

### Per-folder result

Add `-IncludeFolderDetails` to break down the results by folder or label:

```powershell
$stats = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult -IncludeFolderDetails
$stats.MailboxAnalysisResult.AnalysisResultDataRows | Format-Table -AutoSize `
    FolderIsSelected, FolderPath, StartTime, ItemCount, ItemSize
```

**Example output:**

```
FolderIsSelected FolderPath               StartTime ItemCount ItemSize
---------------- ----------               --------- --------- --------
Yes              Tasks                    0001-01   0         0 B (0 bytes)
Yes              #SentItems#              0001-01   4         52.68 MB (55,243,759 bytes)
Yes              Outbox                   0001-01   0         0 B (0 bytes)
Yes              Notes                    0001-01   0         0 B (0 bytes)
Yes              MyFolder                 0001-01   0         0 B (0 bytes)
Yes              MyFolder/500.Rand        0001-01   500       45.9 GB (49,285,052,925 bytes)
Yes              #JunkEmail#              0001-01   0         0 B (0 bytes)
Yes              Journal                  0001-01   0         0 B (0 bytes)
Yes              #Inbox#                  0001-01   49        4.595 GB (4,934,076,159 bytes)
Yes              #Inbox#/100.Rand         0001-01   100       9.766 GB (10,486,202,625 bytes)
Yes              #Inbox#/300.Rand         0001-01   300       29.3 GB (31,458,607,875 bytes)
Yes              #Drafts#                 0001-01   0         0 B (0 bytes)
Yes              #DeletedItems#           0001-01   0         0 B (0 bytes)
Yes              Contacts                 0001-01   0         0 B (0 bytes)
Yes              Calendar                 0001-01   2         9.453 MB (9,912,480 bytes)
                 Total                             1335      126.5 GB (135,824,984,515 bytes)
```

Note

- `FolderIsSelected` indicates whether the folder is included in the analysis (`Yes` or `No`).
- `StartTime` is the earliest month from which items are counted (month-granular).
- The last `Total` row shows the aggregate of all selected items.
- In Google Workspace, an item with multiple labels is copied to multiple folders in EXO. The analysis accounts for this duplication.
- Well-known folders such as Inbox, Sent Items, and Deleted Items appear with a `#` prefix in IMAP and Google sources (for example, `#Inbox#`, `#SentItems#`).

### Filter by time window

Use `-ItemsStartTime` and/or `-ItemsEndTime` to analyze items within a specific time range. Both parameters accept dates in `"yyyy/MM/dd"` format and are treated with **month granularity**.For example, `-ItemsStartTime "2025/03/01"` and `-ItemsStartTime "2025/03/15"` both select all items from March 2025.

| Parameter | Description |
| --- | --- |
| `-ItemsStartTime` | Include only items received on or after this month. Can be used alone or together with `-ItemsEndTime`. Supported with both `-IncludeAnalysisResult` and `-IncludeMappingResult`. |
| `-ItemsEndTime` | Include only items received **before** this month (exclusive). Must be used together with `-ItemsStartTime`. Supported with `-IncludeAnalysisResult` only. |

**Example: items from a specific start date onward (`-ItemsStartTime` only):**

```powershell
# All items from December 2024 onward
PS C:\> $stats = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult `
    -IncludeFolderDetails -ItemsStartTime "2024/12/01"
PS C:\> $stats.MailboxAnalysisResult.AnalysisResultDataRows | Format-Table -AutoSize `
    FolderIsSelected, FolderPath, StartTime, ItemCount, ItemSize

FolderIsSelected FolderPath         StartTime ItemCount ItemSize
---------------- ----------         --------- --------- --------
Yes              #SentItems#        2024-12   4         52.68 MB (55,243,759 bytes)
Yes              MyFolder/500.Rand  2024-12   500       45.9 GB (49,285,052,925 bytes)
Yes              #Inbox#            2024-12   49        4.595 GB (4,934,076,159 bytes)
...
                 Total                        1335      126.5 GB (135,824,984,515 bytes)
```

**Example: items within a specific time range (both parameters):**

```powershell
# Items from August 2022 through January 2023 (i.e., before February 2023)
PS C:\> $stats_select = Get-MailboxAnalysisRequestStatistics <exo user> -IncludeAnalysisResult `
    -ItemsStartTime "2022/08/01" -ItemsEndTime "2023/02/01"
PS C:\> $stats_select.MailboxAnalysisResult.AnalysisResultDataRows | Format-Table -AutoSize

FolderIsSelected FolderPath         StartTime ItemCount ItemSize
---------------- ----------         --------- --------- --------
Yes              #SentItems#        2022-08   3         27.37 MB (28,707,805 bytes)
Yes              MyFolder/500.Rand  2022-08   500       45.9 GB (49,285,052,925 bytes)
Yes              #Inbox#            2022-08   0         0 B (0 bytes)
...
                 Total                        582       52.61 GB (56,497,474,057 bytes)
```

Note

`-ItemsStartTime` and `-ItemsEndTime` must be in **different months** to produce meaningful results, since the analysis is month-granular.

In this example, the result shows items received from August 2022 up to (but not including) February 2023. `-ItemsEndTime` is exclusive, so the range is `[ItemsStartTime, ItemsEndTime)`.

## (Optional) Export analysis results to CSV

To save the per-folder analysis output to a CSV file for offline review:

```powershell
$stats       = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult -IncludeFolderDetails
$csvFilePath = ""   # Output path for the CSV file

$stats.MailboxAnalysisResult.AnalysisResultDataRows | Export-Csv $csvFilePath -NoTypeInformation
```

The CSV includes these columns: `FolderIsSelected`, `FolderPath`, `StartTime`, `ItemCount`, `ItemSize`, `Warning`.

## Step 4: Generate the mapping XML file

For large mailbox migrations, you need an XML mapping file that tells the system how to distribute content across EXO mailboxes. You can [download a sample mapping file](https://download.microsoft.com/download/7/d/d/7dd8c93f-8289-4521-9a46-614059687cea/mapping.xml) and edit it manually, or generate one automatically from the analysis result using `Get-MailboxAnalysisRequestStatistics -IncludeMappingResult`.

First, check the user's current mailbox locations and quotas to inform your mapping decisions:

```powershell
# View mailbox locations and GUIDs
PS C:\> Get-MailboxLocation -User $user | Format-List OwnerID, MailboxGuid, MailboxLocationType

OwnerId             : Mailbox27
MailboxGuid         : 57ce4524-3f4e-41a7-9ef7-d8d70864b118
MailboxLocationType : Primary

# View quotas and current storage usage
PS C:\> Get-Mailbox $user | Format-List ExchangeGuid, ArchiveGuid, *quota

ExchangeGuid              : 57ce4524-3f4e-41a7-9ef7-d8d70864b118
ArchiveGuid               : 00000000-0000-0000-0000-000000000000
ProhibitSendQuota         : 99 GB (106,300,440,576 bytes)
ProhibitSendReceiveQuota  : 100 GB (107,374,182,400 bytes)
IssueWarningQuota         : 98 GB (105,226,698,752 bytes)
ArchiveQuota              : 100 GB (107,374,182,400 bytes)
ArchiveWarningQuota       : 90 GB (96,636,764,160 bytes)

PS C:\> Get-MailboxStatistics $user | Format-List Total*Size, MailboxGuid

TotalDeletedItemSize : 0 B (0 bytes)
TotalItemSize        : 2.462 MB (2,581,965 bytes)
MailboxGuid          : 57ce4524-3f4e-41a7-9ef7-d8d70864b118
```

The cmdlet supports three methods for generating the mapping. Choose based on how you want to control the content distribution:

| Method | When to use |
| --- | --- |
| `ItemsStartTime` | You want to control which data goes to the EXO primary mailbox by specifying a cutoff date. |
| `Auto` | You want the system to automatically select the cutoff date to keep EXO primary within quota limits. |

Note

`-ItemsEndTime` isn't supported with `-IncludeMappingResult`.

### Example 1: Map by cutoff date (`-ItemsStartTime`)

Use `-ItemsStartTime` to specify a cutoff date. Source data on or after this date is mapped to the EXO primary mailbox. Data before this date is mapped to EXO Main Archive and Auxiliary Archive mailboxes.

Ensure the estimated size of data on or after the cutoff date doesn't exceed your EXO primary mailbox quota before choosing a cutoff date.

```powershell
$stats_select = Get-MailboxAnalysisRequestStatistics <exo user> -IncludeMappingResult -ItemsStartTime "2022/08/01"
$ipgeo = New-Object System.Xml.XmlDocument
$ipgeo = [xml]$stats_select.MappingResult
$ipgeo.Save("mapping_output.xml")
```

**Example XML output:**

```xml
<User EmailAddress="foo@contoso.com">
    <Mapping ContentFilter="Received -lt '2021-01-01'" Target="MainArchive" />
    <Mapping ContentFilter="Received -ge '2021-01-01' -and Received -lt '2022-08-01'" Target="AuxArchive0" />
    <Mapping ContentFilter="Received -ge '2022-08-01'" Target="Primary" />
</User>
```

In this example:

- Source primary items before January 1, 2021 → EXO **Main Archive**
- Source primary items from January 1, 2021 to July 31, 2022 → EXO **Auxiliary Archive**
- Source primary items from August 1, 2022 onward → EXO **primary mailbox**

### Example 2: Automated mapping (`-Auto`)

Use `-Auto` to let the system automatically select a cutoff date that keeps the data mapped to the EXO primary mailbox within quota limits. Use this option when you don't want to manually determine the cutoff date.

```powershell
$stats_select = Get-MailboxAnalysisRequestStatistics <exo user> -IncludeMappingResult -Auto
$ipgeo = [xml]$stats_select.MappingResult
$ipgeo.Save("mapping_output.xml")
```

Note

`-Auto` can't be combined with `-ItemsStartTime`, `-CSVData`, or `-IncludeFolderDetails`.

### Limitations

Important

The mapping generation fails if a single month contains more data than the target mailbox quota allows. Because the analysis tool is month-granular, it can't split a single month into a smaller time range. In that case, you must create the XML mapping file manually. Additionally, two mappings that share the same start month, the same end month, and different target archive mailboxes aren't supported.

### Use the mapping XML in a migration batch

The XML output from `-IncludeMappingResult` contains a single `<User>` element. To use it in a large mailbox migration batch, wrap it in a `<Users>` root element:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Users>
    <User EmailAddress="foo@contoso.com">
        <Mapping ContentFilter="Received -lt '2021-01-01'" Target="MainArchive" />
        <Mapping ContentFilter="Received -ge '2021-01-01' -and Received -lt '2022-08-01'" Target="AuxArchive0" />
        <Mapping ContentFilter="Received -ge '2022-08-01'" Target="Primary" />
    </User>
    ...
</Users>
```

For full instructions on creating the migration batch with this file, see [Automated large mailbox migration from IMAP sources](automated-large-mailbox-migration-from-imap-sources).