---
layout: Conceptual
title: What you need to know about a staged email migration in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/what-to-know-about-a-staged-migration
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
ms.assetid: 7e2c82be-5f3d-4e36-bc6b-e5b4d411e207
ms.reviewer: 
description: "As part of a Microsoft 365 or Office 365 deployment, you can migrate the contents of user mailboxes from a source email system to Microsoft 365 or Office 365. When you do this over time, it's called a staged migration. A staged migration is recommended when:"
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- MBS150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: f38ef0d5-c0c1-b1cf-f687-f4f856157713
document_version_independent_id: 38f4deee-3b23-206d-df63-8fa6a4935419
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/what-to-know-about-a-staged-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/what-to-know-about-a-staged-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/what-to-know-about-a-staged-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 7e26ff08-838e-d280-933b-368d470970a6
---

# What you need to know about a staged email migration in Exchange Online | Microsoft Learn

As part of a Microsoft 365 or Office 365 deployment, you can migrate the contents of user mailboxes from a source email system to Microsoft 365 or Office 365. When you do this over time, it's called a staged migration. A staged migration is recommended when:

- Your source email system is Microsoft Exchange Server 2003 or Microsoft Exchange Server 2007.

    Note

    - Microsoft Exchange Server 2003 and Microsoft Exchange Server 2007 are out of support. Support for Exchange 2003 ended on April 8, 2014. Support for Exchange 2007 ended on April 11, 2017.
    - You can't use a staged migration to migrate Exchange 2013 or Exchange 2010 mailboxes to Microsoft 365 or Office 365. Consider using a cutover migration or a hybrid email migration instead.
- You have more than 2,000 mailboxes.

If a staged email migration won't work for you, see [Ways to migrate email](mailbox-migration) for other options.

## Things to consider

Here are a few items to be aware of:

- You must synchronize accounts between your on-premises Active Directory domain and Microsoft 365 or Office 365 by using Azure Active Directory Sync for a staged migration to work.
- The primary domain name used for your on-premises Exchange organization must be a domain verified to your Microsoft 365 or Office 365 organization.
- You can migrate only user mailboxes and resource mailboxes. Other recipient types, such as distribution groups, contacts, and mail-enabled users are migrated to Microsoft 365 or Office 365 through the process of directory synchronization.
- Out of Office messages aren't migrated with user mailboxes. If a user turns on the Out of Office feature before the migration, the feature remains enabled on the migrated mailbox, but the Out of Office message is blank. People who send messages to the mailbox won't receive an Out of Office notification. To allow Out of Office notifications to be sent, the user needs to recreate the Out of Office message after the mailbox is migrated.
- If you limited the connections to your source email system, it's a good idea to increase them to improve migration performance. Common connection limits include client/server total connections, per-user connections, and IP address connections on either the server or the firewall. If you didn't limit these connections, you can skip this task.

## Impact of migration to users

- **Administrators can access email**: To migrate email, you need access to the user mailboxes in your source email system.
- **Users must create new Outlook profiles**: After the mailboxes are migrated and the on-premises accounts are converted to mail-enabled accounts, the users must create a new Microsoft 365 or Office 365 profile in Outlook, and then Outlook automatically connects to Microsoft 365 or Office 365.

## How does staged migration work?

The main steps you perform for a staged migration, and the results for your users, are shown in the following illustration.

![Process for performing a staged email migration.](../exchangeonline/mailbox-migration/media/fcf22570-1d36-49d4-bfed-6ccddec7205f.png)

Here's a description of the staged migration shown in the illustration.

1. The administrator synchronizes the list of users between their on-premises environment and Microsoft 365 or Office 365.

    See how-to steps in [Prepare for a staged migration](perform-a-staged-migration/perform-a-staged-migration#prepare-for-a-staged-migration).
2. The administrator creates a comma-separated value (CSV) file that contains a row for each user whose on-premises mailbox is going to be migrated in the migration batch.

    See how-to steps in [Create a list of mailboxes to migrate](perform-a-staged-migration/perform-a-staged-migration#create-a-list-of-mailboxes-to-migrate).
3. The administrator creates and runs a staged migration batch by using the migration dashboard in the Exchange admin center.

    See how-to steps in [Connect Office 365 to your email system](perform-a-staged-migration/perform-a-staged-migration#connect-microsoft-365-or-office-365-to-your-email-system), [Migrate your mailboxes](perform-a-staged-migration/perform-a-staged-migration#migrate-your-mailboxes), and [Start the staged migration batch](perform-a-staged-migration/perform-a-staged-migration#start-the-staged-migration-batch).

    After the administrator starts the migration batch, Exchange Online does the following:

    - Verifies that directory synchronization is enabled.
    - Checks that a mail-enabled user exists in the Microsoft 365 or Office 365 organization for each user listed in the CSV file. Mail-enabled users are created in Microsoft 365 or Office 365 as a result of the directory synchronization process.
    - Converts the Microsoft 365 or Office 365 mail-enabled user to an Exchange Online mailbox for each user in the migration batch.
    - Begins initial synchronization. Exchange Online processes up to *N* migration requests at one time. *N* represents the maximum number of concurrent migrations that the administrator specified when creating the migration endpoint used for the migration batch. By default, initial synchronization is performed on 20 mailboxes at a time until all mailboxes in the migration batch are migrated.
    - Configures mail forwarding. The *TargetAddress* property on the on-premises mailbox is configured with the email address of the Exchange Online mailbox. This process means that mail sent to the on-premises mailbox is forwarded to the corresponding Exchange Online mailbox.
4. After it creates the Exchange Online mailbox and configures mail forwarding for each user in the CSV file, Exchange Online sends a status email message to the administrator. This status message lists the number of mailboxes that were successfully migrated and how many couldn't be migrated. The message also includes links to migration statistics and error reports that contain more detailed information. At this point, users can start using their Exchange Online mailboxes.
5. As part of initial synchronization, Exchange Online then migrates all email messages, contacts, and calendar items from the on-premises mailboxes to Exchange Online mailboxes. Exchange Online sends a final migration report when the data migration is complete.
6. After a migration batch is complete and the administrator verifies that all mailboxes in the batch are successfully migrated, the administrator can convert the on-premises mailboxes to mail-enabled users.

    See how-to steps in [Convert on-premises mailboxes to mail-enabled users so migrated users can get to their email](perform-a-staged-migration/perform-a-staged-migration#convert-on-premises-mailboxes-to-mail-enabled-users-so-migrated-users-can-get-to-their-email).
7. If a user opens their mailbox with Outlook, the Autodiscover service tries to connect to the on-premises mailbox. After you convert on-premises mailboxes to mail-enabled users, the Autodiscover service uses the mail-enabled user to connect Outlook to the Exchange Online mailbox after the user creates a new Outlook profile.
8. The administrator creates additional migration batches, submitting a CSV file for each one.
9. The administrator runs additional migration batches.
10. The administrator resolves any issues. After all on-premises mailboxes in a batch are successfully migrated, the administrator deletes the migration batch.

    See how-to steps in [Delete the staged migration batch](perform-a-staged-migration/perform-a-staged-migration#delete-the-staged-migration-batch).
11. Users can use their Exchange Online mailboxes.
12. The administrator, to complete the transition to Exchange Online and Microsoft 365 or Office 365, performs post-configuration tasks such as:

    - Assign licenses to Microsoft 365 or Office 365 users.
    - Configure the MX record to point to your Microsoft 365 or Office 365 organization so that email is delivered directly to Exchange Online mailboxes.
    - Create an Autodiscover Domain Name System (DNS) record for your Microsoft 365 or Office 365 organization.

    See how-to steps in [Route your email directly to Microsoft 365 or Office 365](perform-a-staged-migration/perform-a-staged-migration#route-your-email-directly-to-microsoft-365-or-office-365) and [Complete post migration tasks](perform-a-staged-migration/perform-a-staged-migration#complete-post-migration-tasks).

    The administrator can decommission the on-premises Exchange Servers (optional).

    Note

    If you implement a single sign-on solution, it is strongly recommended that you maintain at least one Exchange Server so that you can access Exchange System Manager (Exchange 2003) or the Exchange Management Console/Exchange Management Shell (Exchange 2007) to manage mail-related attributes on the on-premises mail-enabled users. For Exchange 2007, the Exchange Server that you maintain should have the Hub Transport, Client Access, and Mailbox server roles installed.

## Ready to start?

If you're comfortable setting up a migration to Microsoft 365 or Office 365, here are the tasks that need to be done.

- Using either Microsoft Entra Synchronization Tool or Microsoft Azure Active Directory Sync Services (Azure AD Sync) to synchronize and create your on-premises users in Microsoft 365 or Office 365.
- Configuring Exchange Server by using the Exchange admin center.
- Changing your organization's MX record to point to Microsoft 365 or Office 365 when the migration is complete. Your MX record is how other mail systems find the location of your email system. Changing your MX record allows other mail systems to begin to send email directly to the new mailboxes in Microsoft 365 or Office 365.

To finish a staged email migration successfully, it's a good idea to be comfortable doing these tasks:

- You configure or verify that directory synchronization is working.
- You configure or verify that Outlook Anywhere is working.
- You create one or more lists of mailboxes to migrate in Excel.
- You use step-by-step wizards in Microsoft 365 or Office 365 to configure and start the migration process.
- You add or change your organization's DNS records, such as the Autodiscover and MX records.
- You mail-enable on-premises mailboxes.

If you're ready to begin a staged email migration, you can use the steps given in [Perform a staged migration email](perform-a-staged-migration/perform-a-staged-migration).