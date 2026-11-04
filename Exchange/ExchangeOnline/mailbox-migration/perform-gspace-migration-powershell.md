---
layout: Conceptual
title: Perform Google Workspace migration to Microsoft 365 or Office 365 using Exchange Online PowerShell | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/perform-gspace-migration-powershell
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
author: AshaIyengar21
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Instructions for migrating from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches using PowerShell
ms.custom: seo-marvel-jun2021
ms.date: 2021-07-13T00:00:00.0000000Z
locale: en-us
document_id: bf3e6c99-8dc8-a5e1-8d3e-ee42dc11aa22
document_version_independent_id: 6ce4bffc-15aa-cc88-bbec-ad41b4bd0dcb
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/perform-gspace-migration-powershell.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/perform-gspace-migration-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/perform-gspace-migration-powershell.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: b313c42b-d797-3ced-2e3f-1455392610ce
---

# Perform Google Workspace migration to Microsoft 365 or Office 365 using Exchange Online PowerShell | Microsoft Learn

## Create a migration endpoint in Microsoft 365 or Office 365

1. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
2. Find the email address for the super admin within the Google Workspace environment. This email address is used to test connectivity between Google Workspace and Microsoft 365 or Office 365. The following steps use 'admin123' as an example.
3. Run the following command:

    ```PowerShell
    Test-MigrationServerAvailability -Gmail -ServiceAccountKeyFileData $([System.IO.File]::ReadAllBytes("C:\\somepath\\yourkeyfile.json")) -EmailAddress admin123@fabrikaminc.net
    ```
4. Verify the test is successful.
5. If successful, run the following command:

    ```PowerShell
    New-MigrationEndpoint -Gmail -ServiceAccountKeyFileData $([System.IO.File]::ReadAllBytes("C:\\somepath\\yourkeyfile.json")) -EmailAddress admin123@fabrikaminc.net -Name gmailEndpoint
    ```

## Create a migration batch in Microsoft 365 or Office 365

1. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
2. Create a CSV file containing the set of all of the users you want to migrate. You need the filename in the upcoming command. The allowed headers are:

    - EmailAddress (required). Contains the primary email address for an existing Microsoft 365 or Office 365 mailbox.
    - Username (optional). Contains the Gmail primary email address, if it differs from EmailAddress.

    ```CSV
    EmailAddress
    will@fabrikaminc.net
    user123@fabrikaminc.net
    ```
3. Run the following command:

    ```PowerShell
    New-MigrationBatch -SourceEndpoint gmailEndpoint -Name gmailBatch -CSVData $([System.IO.File]::ReadAllBytes("C:\\somepath\\gmail.csv")) -TargetDeliveryDomain "o365.fabrikaminc.net"
    ```

    Tip

    See [New-MigrationBatch](/en-us/powershell/module/exchangepowershell/new-migrationbatch) for an explanation of all of the individual parameters you can use with this cmdlet.
4. Run the following command to start the migration batch:

    ```PowerShell
    Start-MigrationBatch -Identity gmailBatch
    ```

    Note

    When the batch starts, all the users to be migrated will be converted from MailUsers to Mailboxes. The Microsoft 365 or Office 365 Exchange license must be assigned only after this moment. You have 30 days to assign the license.

For more information, see the following articles:

- [Completion of migration batch in PowerShell](completion-gspae-migration-batch-powershell)
- [Overview of the process](how-it-all-works-in-the-backend)