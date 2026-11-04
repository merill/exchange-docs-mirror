---
layout: Conceptual
title: Use PowerShell to move mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/move-mailboxes-using-powershell
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
audience: ITPro
ms.topic: upgrade-and-migration-article
f1.keywords:
- CSH
ms.custom:
- O365E_HRCMoveRequest_FL312271
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
- M365-email-calendar
ms.assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms.reviewer: 
description: This article describes how to use mailboxes using PowerShell.
ms.date: 2024-10-03T00:00:00.0000000Z
locale: en-us
document_id: f4855395-98fc-12ab-11b4-adf2ef2aa602
document_version_independent_id: 5ad59d56-53be-c742-d616-e84a6838fed8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/move-mailboxes-using-powershell.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/move-mailboxes-using-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/move-mailboxes-using-powershell.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 5d5da318-d31c-c4c7-af1b-9fb100584b3f
---

# Use PowerShell to move mailboxes | Microsoft Learn

You can use PowerShell to move mailboxes, in addition to the Exchange Admin Center (EAC).

## Move on-premises mailboxes to an Exchange Online organization

To move an on-premises mailbox to Exchange Online using PowerShell, perform the following steps:

1. **Connect to Exchange Online PowerShell**: Start PowerShell as administrator and [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps&amp;preserve-view=true) by running the following command:

    ```powershell
    PS C:\> Connect-ExchangeOnline
    ```
2. **Find migration endpoint name**: Get the name of the migration endpoint you will use by using the [Get-MigrationEndpoint](/en-us/powershell/module/exchangepowershell/get-migrationendpoint?view=exchange-ps&amp;preserve-view=true) cmdlet.

    ```powershell
    Get-MigrationEndpoint | Format-List Identity
    ```

    The following output appears:

    ```powershell
    PS C:\> Get-MigrationEndpoint | Format-List Identity
    
    Identity     : Hybrid Migration Endpoint - EWS (Default Web Site)
    ```
3. Copy the **Identity** value as you need it in the next part.
4. **Move one or multiple mailboxes to Exchange Online using PowerShell**

    - Create a CSV file named **Users.csv** and place it in the directory **C:\migration**.
    - Open the CSV file, name the header column **EmailAddress**, and fill in all the mailboxes that you like to move to Exchange Online.

        [![Screenshot that shows the CSV on which the details of mailboxes to move are entered.](../exchangehybrid/media/csv-file-with-details-of-mailboxes.png)](../exchangehybrid/media/csv-file-with-details-of-mailboxes.png#lightbox)
    - Create and start a migration batch by running the following:

        ```powershell
        $OnboardingBatch = New-MigrationBatch -Name YourBatchName -SourceEndpoint "Identity of the Migration Endpoint you want to use" -TargetDeliveryDomain yourOffice365DomainPrefix.mail.onmicrosoft.com -CSVData ([System.IO.File]::ReadAllBytes("C:\temp\CSVForMigrationBatch.csv"))
        Start-MigrationBatch -Identity $OnboardingBatch.Identity.Name
        ```
5. **Move primary mailbox only to Exchange Online using PowerShell**

    There's a scenario wherein the archive mailbox location is in Exchange Online and the primary mailbox location is in Exchange on-premises. On this scenario once the migration batch is created, you will see the user in the batch fail with an error saying you must specify the PrimaryOnly parameter, so we run this instead:

    ```powershell
    $OnboardingBatch = New-MigrationBatch -Name YourBatchName -SourceEndpoint "Identity of the Migration Endpoint you want to use" -TargetDeliveryDomain yourOffice365DomainPrefix.mail.onmicrosoft.com -CSVData ([System.IO.File]::ReadAllBytes("C:\temp\CSVForMigrationBatch.csv")) -PrimaryOnly
    Start-MigrationBatch -Identity $OnboardingBatch.Identity.Name
    ```
6. **Move only archive mailbox to Exchange Online using PowerShell**

    ```powershell
    $OnboardingBatch = New-MigrationBatch -Name YourBatchName -SourceEndpoint "Identity of the Migration Endpoint you want to use" -TargetDeliveryDomain yourOffice365DomainPrefix.mail.onmicrosoft.com -CSVData ([System.IO.File]::ReadAllBytes("C:\temp\CSVForMigrationBatch.csv")) -ArchiveOnly
    Start-MigrationBatch -Identity $OnboardingBatch.Identity.Name
    ```
7. **Get mailbox move status**

    - Get the status of the mailbox move request by using the [Get-MoveRequest](/en-us/powershell/module/exchangepowershell/get-moverequest?view=exchange-ps&amp;preserve-view=true) cmdlet.

        ```powershell
        Get-MoveRequest -Identity "Maisha.Lee@contoso.com" | Get-MoveRequestStatistics
        ```
    - Run the following command to get all the mailbox move requests:

        ```powershell
        Get-MoveRequest | Get-MoveRequestStatistics
        ```

        The output shows the mailbox move status as **Completed** status, as shown in the following screenshot:

        [![Screenshot that shows the command that enables the user to get the mailbox move status.](../exchangehybrid/media/get-mailbox-move-status.png)](../exchangehybrid/media/get-mailbox-move-status.png#lightbox)

        If that isn't the case and you can't complete the mailbox move request, you can suspend and resume the move request.

## Move Exchange Online mailboxes to an on-premises organization

To move an Exchange Online mailbox to the on-premises organization using PowerShell, perform the following steps:

1. **Connect to Exchange Online PowerShell**: Start PowerShell as administrator and [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps&amp;preserve-view=true) by running the following command:

    ```powershell
    PS C:\> Connect-ExchangeOnline
    ```

    Note

    You aren't pulling the Exchange Online mailbox to on-premises. In fact, you are pushing the Exchange Online mailbox to on-premises. That's why you need to connect to Exchange Online and run the commands from Exchange Online PowerShell.
2. **Find migration endpoint name**: Get the name of the migration endpoint you will use by using the [Get-MigrationEndpoint](/en-us/powershell/module/exchangepowershell/get-migrationendpoint?view=exchange-ps&amp;preserve-view=true) cmdlet.

    ```powershell
    Get-MigrationEndpoint | Format-List Identity
    ```

    The following output appears:

    ```powershell
    PS C:\> Get-MigrationEndpoint | Format-List Identity
    
    Identity     : Hybrid Migration Endpoint - EWS (Default Web Site)
    ```
3. Copy the **Identity** value as you need it in the next part.
4. **Move one or multiple mailboxes from Exchange Online to Exchange on-premises using PowerShell**

    - Create a CSV file named **Users.csv** and place it in the directory **C:\migration**.
    - Open the CSV file, name the header column **EmailAddress**, and fill in all the mailboxes that you like to move to Exchange Online.

        [![Screenshot that shows the CSV on which the details of mailboxes to move are entered.](../exchangehybrid/media/csv-file-with-details-of-mailboxes.png)](../exchangehybrid/media/csv-file-with-details-of-mailboxes.png#lightbox)
    - Create and start a migration batch by running the following:

        ```powershell
        $OffboardingBatch = New-MigrationBatch -Name YourBatchName -TargetEndpoint "Identity of the Migration Endpoint you want to use" -TargetDeliveryDomain contoso.com -TargetDatabases @(YourDB1,YourDB2,YourDB3) -CSVData ([System.IO.File]::ReadAllBytes("C:\temp\CSVForMigrationBatch.csv"))
        Start-MigrationBatch -Identity $OffboardingBatch.Identity
        ```
5. **Move primary mailbox only from Exchange Online to Exchange on-premises using PowerShell**

    There's a scenario wherein the archive mailbox location is in Exchange Online and the primary mailbox location is in Exchange on-premises. On this scenario once the migration batch is created, you will see the user in the batch fail with an error saying you must specify the PrimaryOnly parameter, so we run this instead:

    ```powershell
      $OffboardingBatch = New-MigrationBatch -Name YourBatchName -TargetEndpoint "Identity of the Migration Endpoint you want to use" -TargetDeliveryDomain contoso.com -TargetDatabases @(YourDB1,YourDB2,YourDB3) -CSVData ([System.IO.File]::ReadAllBytes("C:\temp\CSVForMigrationBatch.csv")) -PrimaryOnly
      Start-MigrationBatch -Identity $OffboardingBatch.Identity
    ```
6. **Get mailbox move status**

    - Get the status of the mailbox move request by using the [Get-MoveRequest](/en-us/powershell/module/exchangepowershell/get-moverequest?view=exchange-ps&amp;preserve-view=true) cmdlet.

        ```powershell
        PS C:\> Get-MoveRequest -Identity "Jordy.Twin@contoso.com" | Get-MoveRequestStatistics | ft DisplayName,StatusDetail,TotalMailboxSize,TotalArchiveSize,PercentComplete
        
        DisplayName StatusDetail TotalMailboxSize             TotalArchiveSize PercentComplete
        ----------- ------------ ----------------             ---------------- ---------------
        Jordy Twin  Completed    231.6 MB (242,877,775 bytes) 0 B (0 bytes)                100
        ```

        The mailbox move completes. If that isn't the case and you can't complete the mailbox move request, you can suspend and resume the move request.

To implement the next step of removing the completed migrated batches, see [Remove completed migration batches](remove-completed-migration-batches#remove-completed-migration-batches).