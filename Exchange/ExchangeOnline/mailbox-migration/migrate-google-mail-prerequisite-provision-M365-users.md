---
layout: Conceptual
title: Prerequisite Step 3 - Provision Microsoft 365 mail users | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrate-google-mail-prerequisite-provision-m365-users
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how to provision mail users in Microsoft 365.
author: MachelleTranMSFT
ms.author: dansimp
ms.service: exchange-online
ms.topic: how-to
ms.date: 2023-08-06T00:00:00.0000000Z
ms.custom: template-how-to
locale: en-us
document_id: b7d59e13-92c9-dab8-6ba6-16ad8c3882ba
document_version_independent_id: 39ba2d9c-9bf4-f8ad-e8dd-89c16ce26832
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-prerequisite-provision-M365-users.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrate-google-mail-prerequisite-provision-m365-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-prerequisite-provision-M365-users.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 038ebc60-8b9f-640f-d3a8-25d724d6f8ce
---

# Prerequisite Step 3 - Provision Microsoft 365 mail users | Microsoft Learn

Note

This is the third of four steps required before migrating Google mail to Microsoft 365. Complete steps 1 and 2 before you continue.

- [Prerequisite Step 1 - Create a subdomain in Google Workspace to route mail to Microsoft 365](migrate-google-mail-prerequisite-create-mail-routing-subdomain-m365) and
- [Prerequisite Step 2 - Create a subdomain to route mail to Google Workspace](migrate-google-mail-prerequisite-create-mail-routing-subdomain-google-domain)

Important

As an IT administrator, you must have the "Recipient Management" role group assigned before starting the migration process. For more information, see [Permissions in Exchange Online](../permissions-exo/permissions-exo).

In Prerequisite Step 3, you create mail user accounts and proxy email addresses for all users you want to migrate from Google Workspace to Microsoft 365.

Check out our video on Google mail migration prerequisites:

## External mail contacts

In Exchange Online organizations, there are two types of external contacts: mail users and mail contacts.

A mail contact provides information about an external user. Mail contacts don't contain sign in credentials for your Microsoft 365 organization and aren't used for accessing resources.

A mail user entry contains an external email address, contact information, and sign-in credentials for your Microsoft 365 organization. Mail user accounts can access resources and services. You can manage mail users in the Exchange admin center or via PowerShell.

For more detailed information on mail contacts and mail users, see [Recipients in Exchange Online](../recipients-in-exchange-online/recipients-in-exchange-online).

## Provision mail users with Exchange admin center

Sign into the [Microsoft 365 admin center](https://admin.microsoft.com/AdminPortal)with your administrator credentials.

1. Select **Show all** and then select **Exchange**.
2. Expand **Recipients**, select **Contacts** and select **Add a mail user**.
3. On the **Set up the basic information** page, enter the information of the user you want to migrate.
4. Fill out the remaining information and select **Next**.
5. Select **Create**. Repeat this process for each user you want to migrate.

| Required | Setting | Example |
| --- | --- | --- |
| No | First name | "Alex" |
| No | Last name | "Wilber" |
| Yes | Display name | "Alex Wilber" |
| No | External email address | Enter the email that uses the Google Workspace mail routing subdomain. `alexw@gws.tailspintoysco.com` |
| Yes | Alias | Same as User ID and External email address. "alexw" |
| Yes | User ID and Domain | Enter the alias used for **External email address**. "alexw" In **Domain**, select the primary domain in the drop down menu. "tailspintoysco.com". Final result is `alexw@tailspintoysco.com`. |
| Yes | Password |  |
| Yes | Confirm password |  |

## Add proxy email addresses to mail users

Now you need to add a proxy email address for each user to route their mail to the Microsoft 365 subdomain.

1. Select **Mailboxes** and select a user from the list.
2. A panel with details of the user appears. Under **Email addresses**, select **Manage email address types**.
3. Select **+ Add email address type**.
4. Verify **STMP** option is selected.
5. Enter the user alias in the **Email address** field and select the Microsoft 365 routing subdomain you created. Select **OK** and then **Save**.
6. Repeat the process for any other users.

## Other ways to provision mail users

### Provision mail users with PowerShell

To manage mail users using PowerShell in Exchange Online, you can use the following cmdlets:

- Get-User
- Set-User
- Get-MailUser
- New-MailUser
- Remove-MailUser
- Set-MailUser

Note

When creating mail users using PowerShell, you may experience throttling limitations. PowerShell commands may also take a few minutes to become visible due to batch processing.

#### Example of mail user formatting in PowerShell

Use the following command in Exchange Online PowerShell to create a mail user for Alex Wilber:

- Name/display name: Alex Wilber
- Alias: alexw
- External email address: `alexw@tailspintoysco.com`
- Sign-in name: `alexw@contoso.onmicrosoft.com`
- You're prompted to enter the password.

```powershell
New-MailUser -Name "Alex Wilber" -Alias alexw -ExternalEmailAddress alexw@tailspintoysco.com -FirstName Alex -LastName Wilber -MicrosoftOnlineServicesID alexw@contoso.onmicrosoft.com -Password (Read-Host "Enter password" -AsSecureString)
```

For detailed syntax and parameter information, see [New-MailUser](/en-us/powershell/module/exchangepowershell/new-mailuser).

### Provision mail users with Microsoft Entra ID (advanced scenario)

1. See [Deploy Microsoft 365 Directory Synchronization in Microsoft Azure](/en-us/office365/enterprise/deploy-office-365-directory-synchronization-dirsync-in-microsoft-azure) for an overview.
2. Follow the setup instructions in [Set up directory synchronization for Microsoft 365](/en-us/office365/enterprise/set-up-directory-synchronization).
3. Set up an Exchange server in your on-premises environment to manage users and enable mail for them.
4. Check [How and when to decommission your on-premises Exchange servers in a hybrid deployment](../decommission-on-premises-exchange) and [Manage mail users](/en-us/Exchange/recipients/mail-users) for more information.
5. If you've created mail users in Microsoft 365, disable Microsoft Entra Connect so the migration process can convert them into mailboxes. See [Turn off directory synchronization for Microsoft 365](/en-us/office365/enterprise/turn-off-directory-synchronization) for details.

    - The primary address or User ID must be provisioned using the primary domain.
    - If a user's primary address is in a different domain, make sure the proxy email address in the primary domain.
    - Each user's `ExternalEmailAddress` should point to their Google Workspace routing subdomain.
    - Users should also have a proxy address that routes to their Microsoft 365 routing subdomain.
6. Disable the Default MRM Policy and Archive policies for users until the migration is complete. Keeping these policies enabled during migration may cause some messages to appear "missing" during content verification.
7. After configuring your Google Workspace environment, you can complete your migration in the Exchange admin center or Exchange Online PowerShell.