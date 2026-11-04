---
layout: Conceptual
title: Test high volume email by using Send-MailMessage PowerShell cmdlet | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/test-high-volume-emails-powershell
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.author: serdars
ms.topic: how-to
author: serdars
ms.service: exchange-online
ms.assetid: e1da5f2f-c732-4010-85c9-878b2cef3fb3
ms.collection:
- exchange-online
- M365-email-calendar
description: Learn how to test high volume email by using the Send-MailMessage cmdlet.
f1.keywords:
- NOCSH
ms.reviewer: mgolda
audience: ITPro
ms.date: 2026-03-26T00:00:00.0000000Z
locale: en-us
document_id: 65e7eec3-72bc-d160-4ea8-0c39dd8d66dc
document_version_independent_id: 09dbcff3-e342-b46c-5ae2-ceb8a1d05d95
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/test-high-volume-emails-powershell.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/test-high-volume-emails-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/test-high-volume-emails-powershell.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: a6e2fe22-f83f-05f6-291c-9ae9394cdb11
---

# Test high volume email by using Send-MailMessage PowerShell cmdlet | Microsoft Learn

## Prerequisites

- A computer that can connect externally through port 587.
- PowerShell 5.1 or a later version installed. As a best practice, install the latest version of [PowerShell](https://aka.ms/PSWindows).
- [ExchangeOnlineManagement module](https://www.powershellgallery.com/packages/ExchangeOnlineManagement/3.5.1) 3.0 or a later version installed.

## Create an HVE account

1. Create an HVE account by using one of the following methods:

    - [Create an HVE account in the Exchange admin center (EAC)](high-volume-mails-m365#create-an-hve-account)
    - [Create an HVE account by using PowerShell](high-volume-mails-m365#powershell-management-for-high-volume-email-accounts)
2. Verify that you can send an email message using your HVE account credentials. For example, use the following information to [send an email message in Power Automate](/en-us/power-automate/desktop-flows/actions-reference/email#sendemail):

    - The email address and password that you selected when you created the HVE account
    - SMTP Server address: `smtp.hve.mx.microsoft` (recommended) or `smtp-hve.office365.com` (will be deprecated in the future)
    - Server port: 587

## Test High Volume Email

1. Connect to [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
2. Run the following commands in an admin PowerShell session to test HVE:

    ```powershell
    param (
        [Parameter(Mandatory = $true)]
        [string]$senderEmailAddress,
        [Parameter(Mandatory = $true)]
        [string]$recipientEmailAddresses,
        [Parameter(Mandatory = $true)]
        [string]$subject,
        [Parameter(Mandatory = $true)]
        [string]$body
    )
    
    $smtpServer = "smtp.hve.mx.microsoft"
    $smtpPort = "587"
    
    # Prompt user for sender credentials
    
    $credentials = Get-Credential -UserName $senderEmailAddress -Message "Enter sender credentials"
    
    # Test HVE account
    
    Send-MailMessage -From $senderEmailAddress -To $recipientEmailAddresses -Subject $subject -Body $body -SmtpServer $smtpServer -Port $smtpPort -UseSsl -Credential $credentials
    ```

    The [Send-MailMessage](/en-us/powershell/module/microsoft.powershell.utility/send-mailmessage) cmdlet output indicates whether the email is sent. If you encounter errors, see [Fix issues with high volume email for Microsoft 365](troubleshoot-high-volume-email-m365).

## Related article

[Manage high volume emails for Microsoft 365 in Exchange Online Public preview](high-volume-mails-m365)