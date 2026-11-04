---
layout: Conceptual
title: Create user mailboxes in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/create-user-mailboxes
Manager: serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Admins can learn how to create mailboxes in Exchange Online.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 6ed2f969-6c03-4b45-8e2d-05de787de48d
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 296cbb00-c2d3-1b29-fddd-545440f71103
document_version_independent_id: 39910e33-72e9-e281-bf9f-c7416db8746e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/create-user-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/create-user-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/create-user-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 58cd38f7-e9b6-1295-b2e0-9b66f623230b
---

# Create user mailboxes in Exchange Online | Microsoft Learn

You have to use the Microsoft 365 admin center or Exchange Online PowerShell to create an Exchange Online user mailbox. **You can't create new user mailboxes using the new Exchange admin center (EAC)**. However, after Exchange Online mailboxes are created, you can manage them using the new EAC. For more information on adding users in Microsoft 365 admin center, see [Add users and assign licenses](/en-us/microsoft-365/admin/add-users/add-users).

Note

After you create a new mailbox using Exchange Online PowerShell, you have to assign it an Exchange Online license or it will be disabled when the 30-day grace period ends.

## What do you need to know before you begin?

- Estimated time to complete: 3 minutes.
- You need permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../permissions-exo/feature-permissions) article.
- It's a good idea to use strong passwords that are at least eight characters long, and combine uppercase and lowercase letters, numbers, and symbols.
- To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use the Microsoft 365 admin center to create a new mailbox

You can use the Microsoft 365 admin center to create a new user account. When you assign the user account a license for Exchange Online, a mailbox is automatically created for the user. To create new user accounts in the Microsoft 365 admin center, see [Add users individually or in bulk](/en-us/microsoft-365/admin/add-users/add-users).

## Use Exchange Online PowerShell to create a new mailbox

This example creates an Exchange Online mailbox and user account for Holly Holt. You're prompted to enter the password. The optional parameter *ResetPasswordOnNextLogon* requires the user to reset their password the first time they sign in to Microsoft 365 or Office 365.

```PowerShell
New-Mailbox -Alias hollyh -Name hollyh -FirstName Holly -LastName Holt -DisplayName "Holly Holt" -MicrosoftOnlineServicesID hollyh@corp.contoso.com -Password (Read-Host "Enter password" -AsSecureString) -ResetPasswordOnNextLogon $true
```

After you create a mailbox by running the previous command, a user account is also created. You have to activate this user account by assigning a license. To assign a license in the Microsoft 365 admin center, see [Add users individually or in bulk](/en-us/microsoft-365/admin/add-users/add-users).

Note

Creation of a new Exchange Online mailbox requires a propagation time of at least 24 hours.