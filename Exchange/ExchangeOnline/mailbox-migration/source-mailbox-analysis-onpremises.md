---
layout: Conceptual
title: Analyze source mailboxes before migrating from Exchange On-Premises to Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/source-mailbox-analysis-onpremises
Manager: aleeming
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: rahu
author: rahu-microsoft
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Learn how to analyze Exchange On-Premises mailboxes before migrating to Exchange Online. Use the analysis results to generate a content mapping file for large mailbox migrations.
ms.date: 2026-08-14T00:00:00.0000000Z
locale: en-us
document_id: f4d9bd43-66ff-27fc-e126-f5a0381c072c
document_version_independent_id: 0f0df5b3-067e-b768-ddc7-5bf45b72ef5f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/source-mailbox-analysis-onpremises.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/source-mailbox-analysis-onpremises
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/source-mailbox-analysis-onpremises.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 78faf78d-005a-2a31-93bd-ca07014d1880
---

# Analyze source mailboxes before migrating from Exchange On-Premises to Microsoft 365 | Microsoft Learn

Before migrating mailboxes from Exchange On-Premises to Exchange Online (EXO), you can run a **Mailbox Analysis Request** to prescan the source mailbox content. The analysis produces a report of folder paths with item counts and sizes, which helps you:

- Identify oversized mailboxes before migration starts.
- Decide how to distribute content across primary, Main Archive, and Auxiliary Archive mailboxes in EXO.
- Generate an XML mapping file for large mailbox migration

## What you need to know before you begin

- It's available through **Exchange Online PowerShell** only. The Exchange Admin Center (EAC) doesn't support this feature yet.
- Hybrid deployment needs to be configured between On-Premises and Exchange Online organizations. Also, the migration endpoint needs to be setup and working. See [Move mailboxes between on-premises and Exchange Online organizations in hybrid deployments](../hybrid-deployment/move-mailboxes).
- The analysis produces two outputs:
    - **Analysis result**: folder paths with item counts and sizes. Folders with more than 1 million items or more than 100 GB are flagged with a warning.
    - **Mapping result**: a ready-to-use XML content mapping file that distributes source data across EXO mailboxes within per-mailbox quota limits.

## Step 1: Verify migration endpoint

You can verify the availability of the migration endpoint using the Test-MigrationServerAvailability cmdlet. For more information on this cmdlet, see [Test-MigrationServerAvailability](/en-us/powershell/module/exchange/Test-MigrationServerAvailability).

## Step 2: Create a mailbox analysis batch

The source endpoint and CSV format for a mailbox analysis batch are the same as for a standard hybrid onboarding migration batch. To learn more about migration endpoints, see [Get-MigrationEndpoint](/en-us/powershell/module/exchange/get-migrationendpoint). For CSV file format details, see [CSV files for mailbox migration](csv-files-for-migration).

Set these variables before running the command:

```powershell
$endpointID = ""   # Identity of the hybrid migration endpoint
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
PS C:\> $endpointID = "hybrid_endpoint"
PS C:\> $batchName  = "OnPrem_Analysis_Batch1"
PS C:\> $csvPath    = "C:\temp\OnPrem_analyze.csv"

PS C:\> New-MigrationBatch -Analyze -SourceEndpoint $endpointID -AutoStart -Name $batchName `
    -CsvData ([System.IO.File]::ReadAllBytes($csvPath))
 
Identity               Status   Type            TotalCount
--------               ------   ----            ----------
OnPrem_Analysis_Batch1 Syncing  OnPremAnalysis  1
```

## Step 3: Check analysis batch and user status

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

Identity                        Status    EstimatedTotalCount EstimatedTotalSize EstimatedArchiveCount EstimatedArchiveSize
--------                        ------    ------------------- ------------------ --------------------- --------------------
OnPremMailbox@contoso.com       Completed 1335                135824984515
```

To convert the size to GB:

```powershell
PS C:\> 135824984515 / 1GB
126.496874275617
```

## Step 4: View the analysis results

Once `Get-MigrationUser` shows `Status = Completed`, use `Get-MailboxAnalysisRequestStatistics` with `IncludeAnalysisResult` to view the detailed results.

Set the user variable:

```powershell
$user = ""   # Identity of the migration user to analyze
```

If `Get-MailboxAnalysisRequestStatistics $user` fails, it might be due to a soft-deleted user, and the workaround is to use the following cmdlets.

```powershell
Get-MailboxLocation $user | Format-List ID                    # replace the below MailboxLocationIdParameter value with ID which is OrgGuid\MailboxGuid format
Get-MailboxAnalysisRequest $user | Format-List RequestGuid    # replace the below RequestGuid value with GUID
Get-MailboxAnalysisRequestStatistics "IND#MapiMailbox#MailboxLocationIdParameter#RequestGuid"
```

### Aggregated result (totals only)

```powershell
$stats = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult
$stats.MailboxAnalysisResult.AnalysisResultDataRows | Format-Table -AutoSize `
    SourceMailbox, FolderIsSelected, FolderPath, StartTime, ItemCount, ItemSize
```

**Example output 1**

User only has primary mailbox

```
SourceMailbox FolderIsSelected FolderPath  StartTime ItemCount ItemSize
------------- ---------------- ----------  --------- --------- --------
                               Total                 39        17.95 MB (18,818,259 bytes)
```

**Example output 2**

User has both primary mailbox and archive mailbox

```
SourceMailbox FolderIsSelected FolderPath StartTime ItemCount ItemSize    
------------- ---------------- ---------- --------- --------- --------    
MainArchive                    Total                6088      128.7 MB (134,960,198 bytes)
                               Total                1858      14.91 MB (15,630,350 bytes)
```

| Column | Description |
| --- | --- |
| `SourceMailbox` | Which mailbox (MainArchive or Primary) the data is in. Empty means primary mailbox |
| `FolderIsSelected` | No meaning in the aggregated view |
| `StartTime` | Items after this time are selected for analysis; empty means all the items are selected |
| `FolderPath` | "Total" is to present the whole mailbox in the aggregated view |

As shown in the 1st example, when user has only primary mailbox in Exchange On-Premise, the last row “Total” shows the total size and count of the selected items in primary mailbox. As shown in the 2nd example, when user has primary and archive mailboxes, the last two rows “Total” show the statistics of both mailboxes, respectively.

Important

It’s highly recommended to run `Get-MailboxStatistics` on Exchange On-Premises PowerShell and compare the size with the analysis result to ensure the analysis job works as expected. See [Get-MailboxStatistics](/en-us/powershell/module/exchange/get-mailboxstatistics).

- Run Get-MailboxStatistics, compare its sum of TotalItemSize and TotalDeletedItemSize with the analysis result’s Primary total ItemSize.
- Run Get-MailboxStatistics -Archive, compare its sum of TotalItemSize and TotalDeletedItemSize with the analysis result’s MainArchive total ItemSize.

### Per-folder result

Add `-IncludeFolderDetails` to break down the results by folder or label:

```powershell
$stats = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult -IncludeFolderDetails
$stats.MailboxAnalysisResult.AnalysisResultDataRows | Format-Table -AutoSize `
    SourceMailbox, FolderIsSelected, FolderPath, StartTime, ItemCount, ItemSize
```

| Column | Description |
| --- | --- |
| `SourceMailbox` | Which mailbox (MainArchive or Primary) the data is in. Empty means primary mailbox |
| `FolderIsSelected` | Whether the folder is included in the analysis (Yes or No) |
| `StartTime` | The earliest month from which items are counted (month-granular) |
| `FolderPath` | The folder path. Well-known folders such as Inbox, Sent Items, and Deleted Items appear with a # prefix (for example, #Inbox#, #SentItems#). The last one row or two rows “Total” show the aggregated statistics of mailboxes. |

Important

It’s highly recommended to run `Get-MailboxFolderStatistics` on Exchange On-Premises PowerShell and compare the size with the analysis per-folder result. See [Get-MailboxFolderStatistics](/en-us/powershell/module/exchange/get-mailboxfolderstatistics).

`Get-MailboxFolderStatistics $user | Format-Table FolderPath,ItemsInFolder`

`Get-MailboxFolderStatistics $user -Archive | Format-Table FolderPath,ItemsInFolder`

### Filter by time window

Use `-ItemsStartTime` and/or `-ItemsEndTime` to analyze items within a specific time range. Both parameters accept dates in `"yyyy/MM/dd"` format and are treated with **month granularity**. For example, `-ItemsStartTime "2025/03/01"` and `-ItemsStartTime "2025/03/15"` both select all items from March 2025.

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
Yes              MyFolder/Foo       2024-12   500       45.9 GB (49,285,052,925 bytes)
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
```

Note

`-ItemsStartTime` and `-ItemsEndTime` must be in **different months** to produce meaningful results, since the analysis is month-granular. `-ItemsEndTime` is exclusive, so the range is `[ItemsStartTime, ItemsEndTime)`.

## (Optional) Export analysis results to CSV

To save the per-folder analysis output to a CSV file for offline review:

```powershell
$stats       = Get-MailboxAnalysisRequestStatistics $user -IncludeAnalysisResult -IncludeFolderDetails
$csvFilePath = ""   # Output path for the CSV file

$stats.MailboxAnalysisResult.AnalysisResultDataRows | Export-Csv $csvFilePath -NoTypeInformation
```

The CSV includes these columns: `SourceMailbox`, `FolderIsSelected`, `FolderPath`, `StartTime`, `ItemCount`, `ItemSize`, `Warning`.

## Step 5: Generate the mapping XML file

For large mailbox migrations, you need an XML mapping file that tells the system how to distribute content across EXO mailboxes. You can [download a sample mapping file](https://download.microsoft.com/download/7/d/d/7dd8c93f-8289-4521-9a46-614059687cea/mapping.xml) and edit it manually, or generate one automatically from the analysis result using `Get-MailboxAnalysisRequestStatistics -IncludeMappingResult`. Using `IncludeMappingResult` ensures:

- Total size mapped to a target mailbox is less than 80 GB.
- Item count mapped to a regular folder in a target mailbox is less than 900,000.
- Item count mapped to a Recoverable Items folder is less than 2.8 million.

The cmdlet supports two methods for generating mapping. Which method you choose should be based on how you want to control the content distribution:

| Method | When to use |
| --- | --- |
| `ItemsStartTime` | You want to control which data goes to the EXO primary mailbox by specifying a cutoff date. |
| `Auto` | You want the system to automatically select the cutoff date to keep EXO primary within quota limits. |

Note

`-ItemsEndTime` isn't supported with `-IncludeMappingResult`.

### Example 1: Map by cutoff date (`-ItemsStartTime`)

Use `-ItemsStartTime` to specify a cutoff date. Data on or after this date from source primary mailbox is mapped to the EXO primary mailbox. Data before this date from source primary mailbox is mapped to EXO Main Archive and Auxiliary Archive mailboxes. If user has archive mailbox on Exchange On-Premises, all contents will be mapped to EXO Main Archive and Auxiliary Archive mailboxes.

Ensure the estimated size of data on or after the cutoff date doesn't exceed your EXO primary mailbox quota before choosing a cutoff date.

To map all content in the Exchange On-Premises primary mailbox to the EXO primary mailbox, use 0001/01/01 as the ItemsStartTime value.

```powershell
$stats_select = Get-MailboxAnalysisRequestStatistics <exo user> -IncludeMappingResult -ItemsStartTime "2022/08/01"
$ipgeo = New-Object System.Xml.XmlDocument
$ipgeo = [xml]$stats_select.MappingResult
$ipgeo.Save("mapping_output.xml")
```

**Example XML output 1**

User has primary mailbox on Exchange On-Premises.

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

**Example XML output 2**

```xml
<User EmailAddress="foo@contoso.com">
    <Mapping ContentFilter="" Target="MainArchive" SourceIsArchive="true" />
    <Mapping ContentFilter="Received -lt '2022-08-01'" Target="AuxArchive0" />
    <Mapping ContentFilter="Received -ge '2022-08-01'" Target="Primary" />
</User>
```

In this example:

- Source archive all items → EXO **Main Archive**
- Source primary items before August 1, 2022 → EXO **Auxiliary Archive**
- Source primary items from August 1, 2022 onward → EXO **primary mailbox**

### Example 2: Automated mapping (`-Auto`)

Use `-Auto` to let the system automatically select a cutoff date that keeps the data mapped to the EXO primary mailbox within quota limits. Use this option when you don't want to manually determine the cutoff date.

```powershell
$stats_select = Get-MailboxAnalysisRequestStatistics <exo user> -IncludeMappingResult -Auto
$ipgeo = [xml]$stats_select.MappingResult
$ipgeo.Save("mapping_output.xml")
```

Note

`-Auto` can't be combined with `-ItemsStartTime` or `-IncludeFolderDetails`.

Note

User `EmailAddress` in the output XML might be different from the one in the CSV file which is used when creating the analysis batch. Change the value to the one in the CSV file.

### Limitations

Important

Mapping generation can fail with the error "The folder XXX with size YYY cannot be mapped automatically." This usually happens because a single month contains more data than the target mailbox quota allows. The analysis tool is month-granular, so it can't split a single month into a smaller time range. In that case, the administrator must create the XML mapping file manually and carefully.

Additionally, two mappings that share the same start month, the same end month, and different target archive mailboxes aren't supported.

**Unsupported mapping example 1**

```xml
<Mapping ContentFilter="Received -ge '2021-01-01' -and Received -lt '2022-01-15'" Target="AuxArchive0" />
<Mapping ContentFilter="Received -ge '2021-01-15' -and Received -lt '2022-01-31'" Target="AuxArchive1" />
```

**Unsupported mapping example 2**

```xml
<Mapping ContentFilter="Received -ge '2021-01-01' -and Received -lt '2022-01-15'" Target="AuxArchive0" />
<Mapping ContentFilter="Received -ge '2021-01-15' -and Received -lt '2022-01-31'" Target="AuxArchive1" SourceIsArchive="true"/>
```

If user has archive mailbox on Exchange On-Premises, mapping any item from source Primary to target MainArchive is not supported.

**Unsupported mapping example 3**

```xml
<Mapping ContentFilter="" Target="MainArchive" SourceIsArchive="true" />
<Mapping ContentFilter="Received -lt '2022-08-01'" Target="MainArchive" />
<Mapping ContentFilter="Received -ge '2022-08-01'" Target="Primary" />
```

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

This file can be used in [large mailbox onboarding from Exchange On-Premises](large-mailbox-migration-from-onpremises-xml-mapping).