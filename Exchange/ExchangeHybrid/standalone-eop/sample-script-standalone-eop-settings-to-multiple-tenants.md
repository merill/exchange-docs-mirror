---
layout: Conceptual
title: Sample script to view settings for the Built-in security add-on for on-premises mailboxes in multiple organizations | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/standalone-eop/sample-script-standalone-eop-settings-to-multiple-tenants
Manager: deniseb
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: chrisda
author: chrisda
ms.date: 2025-12-11T00:00:00.0000000Z
audience: ITPro
ms.topic: how-to
ms.localizationpriority: medium
ms.assetid: e87e84e1-7be0-44bf-a414-d91d60ed8817
ms.custom:
- seo-marvel-apr2020
description: Admins in on-premises organizations that use the Built-in security add-on for on-premises mailboxes can use the PowerShell script in this article to view the add-on configuration settings in multiple organizations.
ms.service: exchange-online
locale: en-us
document_id: a7a801b7-c2ea-2c53-b163-5eb09e7fabc6
document_version_independent_id: ffa694ce-fdba-31ff-009a-7dc4af468fde
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/standalone-eop/sample-script-standalone-eop-settings-to-multiple-tenants.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standalone-eop/sample-script-standalone-eop-settings-to-multiple-tenants
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/standalone-eop/sample-script-standalone-eop-settings-to-multiple-tenants.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/60932d05-feee-4685-a73b-595e25dd9318
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/c43bb58b-1190-419b-8d18-e6052371b599
platformId: 7decb2cc-801f-745a-acb8-a81aced8ee90
---

# Sample script to view settings for the Built-in security add-on for on-premises mailboxes in multiple organizations | Microsoft Learn

If you use the Built-in security add-on for on-premises mailboxes, you can use the script in this article to view (and with modification, configure) the configuration settings in the different organizations you manage.

## To run a script or cmdlet in multiple organizations with the Built-in security add-on for on-premises mailboxes

1. If you haven't already, [install the Exchange Online PowerShell module](/en-us/powershell/exchange/exchange-online-powershell-v2#install-and-maintain-the-exchange-online-powershell-module).
2. Using Microsoft Excel or another spreadsheet app, create a .csv file with the following details:

    - **UserName** column: The account you use to connect to the cloud (for example, `admin@contoso.onmicrosoft.com`).
    - **Cmdlet** column: The cmdlet or command to run (for example, `Get-AcceptedDomain` or `Get-AcceptedDomain | Format-Table Name`).

    The .csv file looks like this:

    ```text
    UserName,Cmdlet
    admin@contoso.onmicrosoft.com,Get-AcceptedDomain | Format-Table Name
    admin@fabrikam.onmicrosoft.com,Get-AcceptedDomain | Format-Table Name
    ```
3. Save the .csv file in a location that's easy to find (for example, c:\scripts\inputfile.csv).
4. Copy the RunCmdletOnMultipleTenants.ps1 script into Notepad or another text editor, and then save the file to a location that's easy to find (for example, c:\scripts).
5. Run the script by using the following syntax:

    ```powershell
    & "<file path>\RunCmdletOnMultipleTenants.ps1" "<file path>\inputfile.csv"
    ```

    Here's an example:

    ```powershell
    & "c:\scripts\RunCmdletOnMultipleTenants.ps1" "c:\scripts\inputfile.csv"
    ```
6. The script signs in to and runs in each cloud organization.

## RunCmdletOnMultipleTenants.ps1

```powershell
# This script runs Windows PowerShell cmdlets on multiple tenants.
#
# Usage: RunCmdletOnMultipleTenants.ps1 inputfile.csv
#
# .csv input file sample:
#
# UserName,Cmdlet
# admin@contoso.onmicrosoft.com,Get-AcceptedDomain | FT Name
# admin@fabrikam.onmicrosoft.com,Get-AcceptedDomain | FT Name

# Get the .csv file name as an argument to this script.
$FilePath = $args[0]

# Import the UserName and Cmdlet values from the .csv file.
$CompanyList = Import-CSV $FilePath

# Load the Exchange Online PowerShell module
Import-Module ExchangeOnlineManagement

# Loop through each entry from the .csv file.
ForEach ($Company in $CompanyList) {

# Get the current entry's UserName.
$UserName = $Company.UserName

# Get the current entry's Cmdlet.
$Cmdlet = $Company.Cmdlet

# Connect to Exchange Online PowerShell by using the current entry's UserName. Prompt for the password.
Connect-ExchangeOnline -UserPrincipalName $UserName

# Here's where the script to be run on the tenant goes.
# In this example, the cmdlet in the .csv file runs.
Invoke-Expression $Cmdlet

# End the current PowerShell session.
Disconnect-ExchangeOnline -Confirm:$false
}
```