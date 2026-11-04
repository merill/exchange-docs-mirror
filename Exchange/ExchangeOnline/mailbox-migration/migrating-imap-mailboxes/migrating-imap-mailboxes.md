---
layout: Conceptual
title: What you need to know about migrating your IMAP mailboxes to Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes
Manager: jtremper
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.topic: article
author: MicrosoftHeidi
ms.author: heidip
ms.assetid: 3fe19996-29bc-4879-aab9-5a622b2f1481
ms.reviewer: 
description: You can migrate the contents of user mailboxes from your source email system to Microsoft 365 or Office 365 using the Internet Message Access Protocol (IMAP).
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
ms.date: 2024-03-12T00:00:00.0000000Z
locale: en-us
document_id: 87d524e9-45c9-db6a-a0f3-f86fd0dfc937
document_version_independent_id: 5fce9a3e-b3a2-a809-d180-00a4abdb6b44
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 5bc61299-9864-4c43-f9c8-c401d57f9ac0
---

# What you need to know about migrating your IMAP mailboxes to Microsoft 365 or Office 365 | Microsoft Learn

You can migrate the contents of user mailboxes from your source email system to Microsoft 365 or Office 365. Use the Internet Message Access Protocol (IMAP) to migrate email when:

- Your source email system supports IMAP.

If this option won't work for you, see [Ways to migrate email to Microsoft 365 or Office 365](../mailbox-migration) for other options.

For Windows PowerShell steps, see [Use PowerShell to perform an IMAP migration to Microsoft 365 or Office 365](/en-us/office365/enterprise/powershell/use-powershell-to-perform-an-imap-migration-to-office-365).

## Things to consider

Here are a few limitations to be aware of:

- Microsoft's data migration tool is currently unaware of tools enforcing messaging records management (MRM) or archival policies. Because of this, any messages that are deleted or moved to archive by these policies will result in the migration process flagging these items as "missing". The result is perceived data loss rather than actual data loss, which makes it much harder to identify actual data loss during any content verification checks.

    Therefore, Microsoft strongly recommends disabling all MRM and archival policies before attempting any data migration to mailboxes.
- You can only migrate items in a user's inbox or other mail folders. This type of migration doesn't migrate contacts, calendar items, or tasks.
- You can migrate a maximum of 500,000 items from a user's mailbox (emails are migrated from newest to oldest).
- The biggest email you can migrate is 35 MB.
- If you limited the connections to your source email system, it's a good idea to increase them to improve migration performance. Common connection limits include client/server total connections, per-user connections, and IP address connections on either the server or the firewall.

## Impact of migration to users

To migrate email, you need access to the user mailboxes in your source email system. If you know the user passwords or can access their mailboxes by using administrator credentials, there won't be any impact to users until you shut down your source email system.

If you can't access user mailboxes, you'll have to reset the passwords. This lets you access the user mailboxes by using a new password that you know. If users don't know the new passwords, they won't be able to get to their old mailboxes during or after the email migration. You can distribute the new passwords after the migration if you want users to get to their old mailboxes.

## How does IMAP migration work?

The main steps you perform for an IMAP email migration are shown in the following illustration.

![Process for an IMAP email migration.](../../exchangeonline/mailbox-migration/media/9520806b-91a5-4a1a-ac9c-9cd1a3964ebc.png)

These general steps apply whether you're migrating from Gmail or another IMAP system.

1. First you have to create your users in Microsoft 365 or Office 365 and assign licenses to them. The mailboxes have to exist in Microsoft 365 or Office 365 to use IMAP migration.
2. Prepare your IMAP source email system and get the information you need to migrate. If you plan to migrate your domain to Microsoft 365 or Office 365, verify that you own your domain with your domain registrar.

    Depending on which type of email service you're migrating from, you might need to configure some settings or record the name of your email server or service to use later. You also need to verify your domain in your domain registry system if you have a custom domain.
3. Communicate changes to users.

    It's a good idea to let users know about the email migration and how it impacts them. Give users information about what tasks need to be done before, during, and after migration.
4. Set up admin credentials or get or reset user email passwords.

    To perform the migration, you need an administrator account that has permissions, or the username and password to each mailbox.
5. If you're using the steps described in [Migrate Google Apps mailboxes to Microsoft 365 or Office 365](migrate-g-suite-mailboxes) or [Migrate other types of IMAP mailboxes to Microsoft 365 or Office 365](migrate-other-types-of-imap-mailboxes), you'll create a list of mailboxes to migrate (CSV file). These migrations instructions start from the Exchange admin center, and you'll need to create a CSV file that lists the email addresses, usernames, and passwords for the mailboxes you want to migrate.

    You can also use the migrations page or setup instructions in the [Admin center preview to migrate from IMAP](imap-migration-in-the-admin-center) systems such as Gmail, Hotmail.com, or Outlook.com. These steps are the best if you plan to migrate mail for only a few users (less than 50). If you're migrating mail for more users, it's easier to use a CSV file to enter all the information for the accounts.
6. Connect Microsoft 365 or Office 365 to the source email system.

    To migrate email successfully, Microsoft 365 or Office 365 needs to connect and communicate with the source email system. To do this, Microsoft 365 or Office 365 uses a migration endpoint, the settings that are used to create the connection.
7. Migrate mailboxes and then verify the migration.

    To migrate mailboxes, you create a migration batch, and then start the migration. After the migration batch is run, verify that the email was migrated successfully.
8. Optimize email settings (optional).

    There are some settings you can configure so that it doesn't take as long for email to start showing up in your new Microsoft 365 or Office 365 mailboxes. See [Tips for optimizing IMAP migrations](optimizing-imap-migrations).
9. Begin routing email to Microsoft 365 or Office 365.

    You need to change a DNS record called an MX record so that your email system can start routing mail to Office 365.
10. Verify routing and then stop email synchronization.

    After you verify that all email is being routed to Microsoft 365 or Office 365, you can delete the migration batch to stop the synchronization between your source email system and Microsoft 365 or Office 365.
11. Send a welcome letter to users.

    Let your users know about Microsoft 365 or Office 365 and how to sign in to their new mailboxes.

## Ready to start?

To finish an email migration successfully, it's a good idea to be comfortable doing these tasks:

- You create a list of mailboxes to migrate in Excel. You add your users' email addresses, usernames, and passwords to this file.
- You use step-by-step wizards in Microsoft 365 or Office 365 to configure and start the migration process.
- After the mail has been migrated, you change your organization's MX record to point to Microsoft 365 or Office 365 when the migration is complete. Your MX record is how other mail systems find the location of your email system. Changing your MX record allows other mail systems to begin to send email directly to the new mailboxes in Microsoft 365 or Office 365. To learn how to update your MX record, see [Create DNS records at any DNS hosting provider](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider) as well.

If you're comfortable with what's involved in migrating mailboxes to Microsoft 365 or Office 365, you're ready to get started. The first step is to determine which source email system you're migrating from:

- [Gmail](migrate-g-suite-mailboxes)

    This procedure uses the Exchange admin center steps for an IMAP migration.
- [Some other IMAP enabled email system](migrate-other-types-of-imap-mailboxes)

    This procedure uses the Exchange admin center steps for an IMAP migration.
- [IMAP migration in the Admin center](imap-migration-in-the-admin-center)
- [Use PowerShell to perform an IMAP migration to Microsoft 365 or Office 365](/en-us/office365/enterprise/powershell/use-powershell-to-perform-an-imap-migration-to-office-365)