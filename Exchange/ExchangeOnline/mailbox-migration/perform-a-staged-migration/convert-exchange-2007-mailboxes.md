---
layout: Conceptual
title: Convert Exchange 2007 mailboxes to mail-enabled users in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/perform-a-staged-migration/convert-exchange-2007-mailboxes
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
ms.topic: how-to
author: AshaIyengar21
ms.author: lusassl
ms.assetid: a1f79f3c-4967-4a15-8b3a-f4933aac0c34
ms.reviewer: 
description: Convert Exchange 2007 mailboxes to mail enabled users
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- GMA150
- GPA150
- GEA150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: c9e3b4d0-a18c-2cef-f81e-26535a0cdadc
document_version_independent_id: 381d80b9-9223-4928-0b95-1326402a0116
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/perform-a-staged-migration/convert-exchange-2007-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/perform-a-staged-migration/convert-exchange-2007-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/perform-a-staged-migration/convert-exchange-2007-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: e320bf95-9433-3413-8fe2-9a6109eabe33
---

# Convert Exchange 2007 mailboxes to mail-enabled users in Exchange Online | Microsoft Learn

After you've completed a staged migration, convert the on-premises mailboxes to mail-enabled users so the on-premises users can automatically connect to their cloud mailboxes.

## Why convert mailboxes to mail-enabled users?

You need to convert the migrated on-premises mailboxes to mail-enabled users (MEUs) so you can manage cloud-based users from your on-premises organization using Active Directory.

Two things happen after a mailbox is migrated to the cloud in a staged Exchange migration:

- A user has an on-premises mailbox and a cloud mailbox.
- Mail sent to the user's on-premises mailbox is forwarded to their cloud mailbox. This happens because during the migration process, the **TargetAddress** property on the on-premises mailbox contains the remote routing address of the cloud mailbox. Users need to connect to their cloud mailboxes to access their e-mail.

This behavior results in the following issues:

- The user won't be able to connect to their cloud mailbox in Microsoft Outlook. The Autodiscover service in the on-premises organization still tries to connect to their on-premises mailbox. You can't point your on-premises Autodiscover CNAME record to the cloud until all users have been migrated.
- Messaging-related user information on cloud mailboxes is lost if you decommission Exchange after all mailboxes have been migrated to the cloud. Directory synchronization removes data from the cloud mailbox object (for example, proxy addresses), because the on-premises mailbox no longer exists. directory synchronization can't match the data to the corresponding cloud mailbox.

The solution is to convert the user's on-premises mailbox to a mail-enabled user (MEU) after the mailbox has been migrated to the cloud. When you convert an on-premises mailbox to an MEU, the following actions occur:

- The proxy addresses from the cloud-based mailbox are copied to the new MEU. If you decommission Exchange, these proxy addresses are still retained in Active Directory.
- The properties of the MEU enables directory synchronization to match the MEU with its corresponding cloud mailbox.
- The Autodiscover service uses the MEU to connect Outlook to the cloud mailbox after the user creates a new Outlook profile.

## PowerShell scripts to create MEUs

Use the scripts in this section to collect information about the cloud-based mailboxes, and to convert the Exchange 2007 mailboxes to MEUs.

The PowerShell script collects information from your cloud mailboxes and saves it to a CSV file. Run this script first.

Copy the script into Notepad and save the file as ExportO365UserInfo.ps1.

Note

- Before you run the PowerShell script, you need to install the Exchange Online PowerShell module. For instructions, see [Install and maintain the Exchange Online PowerShell module](/en-us/powershell/exchange/exchange-online-powershell-v2#install-and-maintain-the-exchange-online-powershell-module). The module uses modern authentication.
- Typically, you can use the script as-is if your organization is Microsoft 365 or Microsoft 365 GCC. If your organization is Office 365 Germany, Microsoft 365 GCC High, or Microsoft 365 DoD, you need to edit the `Connect-ExchangeOnline` line in the script. Specifically, you need to use the *ExchangeEnvironmentName* parameter and the appropriate value for your organization type. For more information, see the examples in [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

```PowerShell
Param($migrationCSVFileName = "migration.csv")
function O365Logon
{
    #Check for current open O365 sessions and allow the admin to either use the existing session or create a new one
    $session = Get-PSSession | ?{$_.ConfigurationName -eq 'Microsoft.Exchange'}
    if($session -ne $null)
    {
        $a = Read-Host "An open session to Exchange Online PowerShell already exists. Do you want to use this session?  Enter y to use the open session, anything else to close and open a fresh session."
        if($a.ToLower() -eq 'y')
        {
            Write-Host "Using existing Exchange Online Powershell session." -ForeGroundColor Green
            return
        }
        Disconnect-ExchangeOnline -Confirm:$false
    }
    Import-Module ExchangeOnlineManagement
    Connect-ExchangeOnline -Prefix "Cloud"
}
function Main
{
    #Verify the migration CSV file exists
    if(!(Test-Path $migrationCSVFileName))
    {
        Write-Host "File $migrationCSVFileName does not exist." -ForegroundColor Red
        Exit
    }
    #Import user list from migration.csv file
    $MigrationCSV = Import-Csv $migrationCSVFileName

    #Get mailbox list based on email addresses from CSV file
    $MailBoxList = $MigrationCSV | %{$_.EmailAddress} | Get-CloudMailbox
    $Users = @()

    #Get LegacyDN, Tenant, and On-Premises Email addresses for the users
    foreach($user in $MailBoxList)
    {
        $UserInfo = New-Object System.Object

        $CloudEmailAddress = $user.EmailAddresses | ?{($_ -match 'onmicrosoft') -and ($_ -match 'smtp:')}
        if ($CloudEmailAddress.Count -gt 1)
        {
            $CloudEmailAddress = $CloudEmailAddress[0].ToString().ToLower().Replace('smtp:', '')
            Write-Host "$user returned more than one cloud email address. Using $CloudEmailAddress" -ForegroundColor Yellow
        }
        else
        {
            $CloudEmailAddress = $CloudEmailAddress.ToString().ToLower().Replace('smtp:', '')
        }

        $UserInfo | Add-Member -Type NoteProperty -Name LegacyExchangeDN -Value $user.LegacyExchangeDN
        $UserInfo | Add-Member -Type NoteProperty -Name CloudEmailAddress -Value $CloudEmailAddress
        $UserInfo | Add-Member -Type NoteProperty -Name OnPremiseEmailAddress -Value $user.PrimarySMTPAddress.ToString()
        $UserInfo | Add-Member -Type NoteProperty -Name MailboxGUID -Value $user.ExchangeGUID
        $Users += $UserInfo
    }
    #Check for existing csv file and overwrite if needed
    if(Test-Path ".\cloud.csv")
    {
        $delete = Read-Host "The file cloud.csv already exists in the current directory. Do you want to delete it?  Enter y to delete, anything else to exit this script."
        if($delete.ToString().ToLower() -eq 'y')
        {
            Write-Host "Deleting existing cloud.csv file" -ForeGroundColor Red
            Remove-Item ".\cloud.csv"
        }
        else
        {
            Write-Host "Will NOT delete current cloud.csv file. Exiting script." -ForeGroundColor Green
            Exit
        }
    }
    $Users | Export-CSV -Path ".\cloud.csv" -notype
    (Get-Content ".\cloud.csv") | %{$_ -replace '"', ''} | Set-Content ".\cloud.csv" -Encoding Unicode
    Write-Host "CSV File Successfully Exported to cloud.csv" -ForeGroundColor Green
}
O365Logon
Main
```

The Visual Basic script converts on-premises Exchange 2003 mailboxes to MEUs. Run this script after you run the PowerShell script to collect information from the cloud mailboxes.

Copy the script into Notepad and save the file as Exchange2007MBtoMEU.vbs.

```PowerShell
param($DomainController = [String]::Empty)
function Main
{
    #Script Logic flow
    #1. Pull User Info from cloud.csv file in the current directory
    #2. Lookup AD Info (DN, mail, proxyAddresses, and legacyExchangeDN) using the SMTP address from the CSV file
    #3. Save existing proxyAddresses
    #4. Add existing legacyExchangeDN's to proxyAddresses
    #5. Delete Mailbox
    #6. Mail-Enable the user using the cloud email address as the targetAddress
    #7. Disable RUS processing
    #8. Add proxyAddresses and mail attribute back to the object
    #9. Add msExchMailboxGUID from cloud.csv to the user object (for offboarding support)

    if($DomainController -eq [String]::Empty)
    {
        Write-Host "You must supply a value for the -DomainController switch" -ForegroundColor Red
        Exit
    }

    $CSVInfo = Import-Csv ".\cloud.csv"
    foreach($User in $CSVInfo)
    {
        Write-Host "Processing user" $User.OnPremiseEmailAddress -ForegroundColor Green
        Write-Host "Calling LookupADInformationFromSMTPAddress" -ForegroundColor Green
        $UserInfo = LookupADInformationFromSMTPAddress($User)

        #Check existing proxies for On-Premises and Cloud Legacy DN's as x500 proxies. If not present add them.
        if($UserInfo.ProxyAddresses -notcontains ("X500:"+$UserInfo.CloudLegacyDN))
        {
            $X500Proxy = "x500:" + $UserInfo.CloudLegacyDN
            Write-Host "Adding $X500Proxy to EmailAddresses" -ForegroundColor Green
            $UserInfo.ProxyAddresses.Add($X500Proxy)
        }
        if($UserInfo.ProxyAddresses -notcontains ("X500:"+$UserInfo.LegacyDN))
        {
            $X500Proxy = "x500:" + $UserInfo.LegacyDN
            Write-Host "Adding $X500Proxy to EmailAddresses" -ForegroundColor Green
            $UserInfo.ProxyAddresses.Add($X500Proxy)
        }

        #Disable Mailbox
        Write-Host "Disabling Mailbox" -ForegroundColor Green
        Disable-Mailbox -Identity $UserInfo.OnPremiseEmailAddress -DomainController $DomainController -Confirm:$false

        #Mail Enable
        Write-Host "Enabling Mailbox" -ForegroundColor Green
        Enable-MailUser  -Identity $UserInfo.Identity -ExternalEmailAddress $UserInfo.CloudEmailAddress -DomainController $DomainController

        #Disable RUS
        Write-Host "Disabling RUS" -ForegroundColor Green
        Set-MailUser -Identity $UserInfo.Identity -EmailAddressPolicyEnabled $false -DomainController $DomainController

        #Add Proxies and Mail
        Write-Host "Adding EmailAddresses and WindowsEmailAddress" -ForegroundColor Green
        Set-MailUser -Identity $UserInfo.Identity -EmailAddresses $UserInfo.ProxyAddresses -WindowsEmailAddress $UserInfo.Mail -DomainController $DomainController

        #Set Mailbox GUID. Need to do this via S.DS as Set-MailUser doesn't expose this property.
        $ADPath = "LDAP://" + $DomainController + "/" + $UserInfo.DistinguishedName
        $ADUser = New-Object -TypeName System.DirectoryServices.DirectoryEntry -ArgumentList $ADPath
        $MailboxGUID = New-Object -TypeName System.Guid -ArgumentList $UserInfo.MailboxGUID
        [Void]$ADUser.psbase.invokeset('msExchMailboxGUID',$MailboxGUID.ToByteArray())
        Write-Host "Setting Mailbox GUID" $UserInfo.MailboxGUID -ForegroundColor Green
        $ADUser.psbase.CommitChanges()

        Write-Host "Migration Complete for" $UserInfo.OnPremiseEmailAddress -ForegroundColor Green
        Write-Host ""
        Write-Host ""
    }
}

function LookupADInformationFromSMTPAddress($CSV)
{
    $Mailbox = Get-Mailbox $CSV.OnPremiseEmailAddress -ErrorAction SilentlyContinue

    if($Mailbox -eq $null)
    {
        Write-Host "Get-Mailbox failed for" $CSV.OnPremiseEmailAddress -ForegroundColor Red
        continue
    }

    $UserInfo = New-Object System.Object

    $UserInfo | Add-Member -Type NoteProperty -Name OnPremiseEmailAddress -Value $CSV.OnPremiseEmailAddress
    $UserInfo | Add-Member -Type NoteProperty -Name CloudEmailAddress -Value $CSV.CloudEmailAddress
    $UserInfo | Add-Member -Type NoteProperty -Name CloudLegacyDN -Value $CSV.LegacyExchangeDN
    $UserInfo | Add-Member -Type NoteProperty -Name LegacyDN -Value $Mailbox.LegacyExchangeDN
    $ProxyAddresses = New-Object Microsoft.Exchange.Data.ProxyAddressCollection
    $ProxyAddresses = $Mailbox.EmailAddresses
    $UserInfo | Add-Member -Type NoteProperty -Name ProxyAddresses -Value $ProxyAddresses
    $UserInfo | Add-Member -Type NoteProperty -Name Mail -Value $Mailbox.WindowsEmailAddress
    $UserInfo | Add-Member -Type NoteProperty -Name MailboxGUID -Value $CSV.MailboxGUID
    $UserInfo | Add-Member -Type NoteProperty -Name Identity -Value $Mailbox.Identity
    $UserInfo | Add-Member -Type NoteProperty -Name DistinguishedName -Value (Get-User $Mailbox.Identity).DistinguishedName

    $UserInfo
}
Main
```

## Setup steps to convert on-premises mailboxes to MEUs

Follow these steps to complete the process.

1. Copy ExportO365UserInfo.ps1, Exchange2007MBtoMEU.ps1, and the CSV file used to run the migration batch to the same directory in your on-premises server.
2. Rename the migration CSV file to migration.csv.
3. In the Exchange Management Shell, run the following command. The script assumes that the CSV file is in the same directory and is named migration.csv.

    ```PowerShell
    .\ExportO365UserInfo.ps1
    ```

    You will be prompted to use the existing session or open a new session.
4. Type n and press **Enter** to open a new session.

    The script runs and then saves the Cloud.csv file to the current working directory.
5. Enter the administrator credentials for your cloud-based organization and then click **OK.**
6. Run the following command in a new Exchange Management Shell session. This command assumes that ExportO365UserInfo.ps1 and Cloud.csv are located in the same directory.

    ```PowerShell
    .\Exchange2007MBtoMEU.ps1 <FQDN of on-premises domain controller>
    ```

    For example:

    ```PowerShell
    .\Exchange2007MBtoMEU.ps1 DC1.contoso.com
    ```

    The script converts on-premises mailboxes to MEUs for all users included in the Cloud.csv.
7. Verify that the new MEUs have been created. In **Active Directory Users and Computers**, do the following steps:

    1. Click **Action** &gt; **Find**.
    2. Click the **Exchange** tab.
    3. Select **Show only Exchange recipients**, and then select **Users with external email address**.
    4. Click **Find Now**.

        The mailboxes that were converted to MEUs are listed under **Search results**.
8. Use **Active Directory Users and Computers**, **ADSI Edit**, or **Ldp.exe** to verify that the following MEU properties are populated with the correct information.

    - legacyExchangeDN
    - mail
    - msExchMailboxGuid
    - proxyAddresses
    - targetAddress