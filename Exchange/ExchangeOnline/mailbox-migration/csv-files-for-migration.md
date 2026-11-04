---
layout: Conceptual
title: CSV files for mailbox migration in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/csv-files-for-migration
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
ms.topic: upgrade-and-migration-article
author: AshaIyengar21
ms.author: serdars
ms.assetid: b79fb81d-d6f4-4385-867e-7bdd0238366e
ms.reviewer: 
description: 'You can use a comma-separated values (CSV) file to bulk migrate a large number of user mailboxes. You can specify a CSV file when you use the Exchange admin center (EAC) or the New-MigrationBatch cmdlet in Exchange Online PowerShell to create a migration batch. Using a CSV to specify multiple users to migrate in a migration batch is supported in the following migration scenarios:'
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: 9ab48543-ee14-846d-c52a-d63ed9ef74ba
document_version_independent_id: 117e5534-f05b-7def-1d0b-e494c6e7325e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/csv-files-for-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/csv-files-for-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/csv-files-for-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: 4586e529-4ce7-0449-1966-9f1faf2d8f73
---

# CSV files for mailbox migration in Exchange Online | Microsoft Learn

You can use a comma-separated values (CSV) file to bulk migrate a large number of user mailboxes. You can specify a CSV file when you use the Exchange admin center (EAC) or the [New-MigrationBatch](/en-us/powershell/module/exchangepowershell/New-MigrationBatch) cmdlet in Exchange Online PowerShell to create a migration batch. Using a CSV to specify multiple users to migrate in a migration batch is supported in the following migration scenarios:

- **Onboarding and offboarding in Microsoft 365 or Office 365**

    - **Onboarding remote move migration**: In an Exchange hybrid deployment, you can move mailboxes from an on-premises Exchange organization to Microsoft 365 or Office 365. This is also known as an onboarding remote move migration because you onboard mailboxes to Microsoft 365 or Office 365.
    - **Offboarding remote move migration**: You can also perform an offboarding remote move migration, where you migrate Microsoft 365 or Office 365 mailboxes to your on-premises Exchange organization.

        Note

        Both onboarding and offboarding remote move migrations are initiated from your Microsoft 365 or Office 365 organization.
    - **Staged Exchange migration**: You can also migrate a subset of mailboxes from an on-premises Exchange organization to Microsoft 365 or Office 365. This is another type of onboarding migration. You can migrate only Exchange 2003 and Exchange 2007 mailboxes using a staged Exchange migration. Migrating Exchange 2010 and Exchange 2013 mailboxes isn't supported using a staged migration. Prior to running a staged migration, you have to use directory synchronization or some other method to provision mail users in your Microsoft 365 or Office 365 organization.
    - **IMAP migration**: This onboarding migration type migrates mailbox data from an IMAP server (including Exchange) to Microsoft 365 or Office 365. For an IMAP migration, you must provision mailboxes in Microsoft 365 or Office 365 before you can migrate mailbox data.

Note

A cutover Exchange migration doesn't support using a CSV file because all on-premises user mailboxes are migrated to Microsoft 365 or Office 365 in a single batch.

## Supported attributes for CSV files for bulk moves or migrations

The first row, or header row, of a CSV file used for migrating users lists the names of the attributes, or fields, specified on the rows that follow. Each attribute name is separated by a comma. Each row under the header row represents an individual user and supplies the information required for the migration. The attributes in each individual user row must be in the same order as the attribute names in the header row. Each attribute value is separated by a comma. If the attribute value for a particular record is null, don't type anything for that attribute. However, make sure that you include the comma to separate the null value from the next attribute.

Attribute values in the CSV file override the value of the corresponding parameter when that same parameter is used when creating a migration batch with the EAC or Exchange Online PowerShell. For more information and examples, see the section [Attribute values in the CSV file override the values for the migration batch](csv-files-for-migration#BK-Sttributes).

Tip

You can use any text editor to create the CSV file, but using an application like Microsoft Excel will make it easier to import data and configure and organize CSV files. Be sure to save CSV files as a .csv or .txt file.

The following sections describe the supported attributes for the header row of a CSV file for each migration type. Each section includes a table that lists each supported attribute, whether it's required, an example of a value to use for the attribute, and a description.

Note

- In the following sections, source environment denotes the current location of a user mailbox or a database. Target environment denotes the location that the mailbox will be migrated to or the database that the mailbox will be moved to.
- All mailboxes that are specified in the CSV file will be migrated, even if they are outside of the RBAC scope (for example, an OU) that gives the admin permissions to migrate mailboxes.

### Staged Exchange migrations

You have to use a CSV file to identify the group of users for a migration batch when you want to use a staged Exchange migration to migrate Exchange 2003 and Exchange 2007 on-premises mailboxes to Microsoft 365 or Office 365. There isn't a limit for the number of mailboxes that you can migrate to the cloud using a staged Exchange migration. However, the CSV file for a migration batch can contain a maximum of 2,000 rows. To migrate more than 2,000 mailboxes, you have to create additional CSV files and then use each one to create a new migration batch. For more information about staged Exchange migrations, see [What you need to know about a staged email migration to Microsoft 365 or Office 365](what-to-know-about-a-staged-migration).

The following table describes the supported attributes for a CSV file for a staged Exchange migration.

| Attribute | Required or optional | Accepted values | Description |
| --- | --- | --- | --- |
| EmailAddress | Required | SMTP address for the user | Specifies the email address for the mail-enabled user (or a mailbox if you're retrying the migration) in Microsoft 365 or Office 365 that corresponds to the on-premises user mailbox that will be migrated. Mail-enabled users are created in Microsoft 365 or Office 365 as a result of directory synchronization or another provisioning process. The email address of the mail-enabled user must match the *WindowsEmailAddress* property for the corresponding on-premises mailbox. |
| Password | Optional | A password has to have a minimum length of eight characters, and satisfy any password restrictions that are applied to your Microsoft 365 or Office 365 organization. | This password is set on the user account when the corresponding mail-enabled user in Microsoft 365 or Office 365 is converted to a mailbox during the migration. |
| ForceChangePassword | Optional | `True` or `False` | Specifies whether a user must change the password the first time they sign in to their Microsoft 365 or Office 365 mailbox. **Note**: If you've implemented a single sign-on (SSO) solution by deploying Active Directory Federation Services 2.0 (AD FS 2.0) in your on-premises organization, you must use `False` for the value of this attribute. |

### IMAP migrations

A CSV file for an IMAP migration batch can have maximum of 50,000 rows. But it's a good idea to migrate users in several smaller batches. For more information about IMAP migrations, see the following topics:

- [Migrate your IMAP mailboxes to Microsoft 365 or Office 365](migrating-imap-mailboxes/migrating-imap-mailboxes)
- [CSV files for IMAP migration batches](migrating-imap-mailboxes/csv-files-for-imap-migrations)

The following table describes the supported attributes for a CSV file for an IMAP migration.

| Attribute | Required or optional | Accepted values | Description |
| --- | --- | --- | --- |
| EmailAddress | Required | SMTP address for the user. | Specifies the user ID for the user's Microsoft 365 or Office 365 mailbox |
| UserName | Required | String that identifies the user on the IMAP messaging system, in a format supported by the IMAP server. | Specifies the logon name for the user's account in the IMAP messaging system (the source environment). In addition to the username, you can use the credentials of an account that has been assigned the necessary permissions to access mailboxes on the IMAP server. For more information, see [CSV files for IMAP migration batches](migrating-imap-mailboxes/csv-files-for-imap-migrations). |
| Password | Required | Password string. | Specifies the password for the user account specified by the UserName attribute. |

## Attribute values in the CSV file override the values for the migration batch

Attribute values in the CSV file override the value of the corresponding parameter when that same parameter is used when creating a migration batch with the EAC or Exchange Online PowerShell. If you want the migration batch value to be applied to a user, you would leave that cell blank in the CSV file. This lets you mix and match certain attribute values for selected users in one migration batch.

In this example, let's say you create a batch for an onboarding remote move migration in a hybrid deployment to move archive mailboxes to Microsoft 365 or Office 365 with the following [New-MigrationBatch](/en-us/powershell/module/exchangepowershell/New-MigrationBatch) command.

```PowerShell
New-MigrationBatch -Name OnBoarding1 -SourceEndpoint RemoteEndpoint1 -TargetDeliveryDomain cloud.contoso.com -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\OnBoarding1.csv")) -ArchiveOnly:$true -AutoStart
```

But you also want to move the primary mailboxes for selected users, so a portion of the OnBoarding1.csv file for this migration batch would look like this:

```PowerShell
EmailAddress,MailboxType
user1@contoso.com,
user2@contoso.com,
user3@cloud.contoso.com,PrimaryAndArchive
user4@cloud.contoso.com,PrimaryAndArchive
...
```

Because the value for mailbox type in the CSV file overrides the values for the *MailboxType* parameter in the command to create the batch, only the archive mailbox for user1 and user2 is migrated to Microsoft 365 or Office 365. But the primary and archive mailboxes for user3 and user4 are moved to Microsoft 365 or Office 365.