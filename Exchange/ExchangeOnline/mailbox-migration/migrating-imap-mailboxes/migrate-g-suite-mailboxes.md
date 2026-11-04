---
layout: Conceptual
title: Migrate Google Workspace mailboxes to Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrate-g-suite-mailboxes
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
author: MicrosoftHeidi
ms.author: heidip
ms.assetid: 665dc56c-581c-4e35-8028-6bc1e8497016
ms.reviewer: tonymathew
description: For users who want to migrate their Gmail mailboxes to Microsoft 365 or Office 365 with IMAP and app passwords.
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
ms.custom:
- Adm_O365
- Adm_O365_Setup
ms.service: exchange-online
ms.date: 2024-03-15T00:00:00.0000000Z
locale: en-us
document_id: 75c68b82-8feb-80fd-2e70-49199991dcd7
document_version_independent_id: 875fbcea-7a00-ca24-2edb-20bbee3744a8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/migrate-g-suite-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrating-imap-mailboxes/migrate-g-suite-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/migrate-g-suite-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 9ee0a9af-7d7e-5c32-23e8-a533ef57ca4d
---

# Migrate Google Workspace mailboxes to Microsoft 365 or Office 365 | Microsoft Learn

Note

This article explains how to migrate consumer Gmail mailboxes to Microsoft 365 or Office 365. For organizations and enterprises interested in migrating Google Workspace content, including calendar and contacts information in addition to mailbox data, see [Perform a Google Workspace migration](../perform-g-suite-migration).

[Migrate your IMAP mailboxes to Microsoft 365 or Office 365](migrating-imap-mailboxes) gives you an overview of the migration process. Read it first and when you're familiar with the contents of that article, return to this topic to learn how to migrate mailboxes from Google Workspace Gmail to Microsoft 365 or Office 365. You must be a global admin in Microsoft 365 or Office 365 to complete IMAP migration steps.

Looking for Windows PowerShell commands? See [User PowerShell to perform an IMAP migration to Microsoft 365 or Office 365](/en-us/office365/enterprise/powershell/use-powershell-to-perform-an-imap-migration-to-office-365).

Want to migrate other types of IMAP mailboxes? See [Migrate other types of IMAP mailboxes to Microsoft 365 or Office 365](migrate-other-types-of-imap-mailboxes).

## Migration from Google Workspace mailboxes using the Microsoft 365 admin center

You can use the setup wizard in the Microsoft 365 admin center for an IMAP migration. See [IMAP migration in the Microsoft 365 admin center](imap-migration-in-the-admin-center) for instructions.

Important

IMAP migration will only migrate emails, not calendar, and contact information. Users can import their own email, contacts, and other mailbox information to Microsoft 365 or Office 365. See [Migrate email and contacts to Microsoft 365](/en-us/microsoft-365/admin/setup/migrate-email-and-contacts-admin) to learn how.

Before Microsoft 365 or Office 365 can connect to Gmail or Google Workspace, all account owners must create an app password to access their account. This is because Google considers Outlook to be a less secure app and won't allow a connection to it with a password alone. For instructions, see [Prepare your Google Workspace account for connecting to Outlook and Microsoft 365 or Office 365](prepare-gmail-or-g-suite-accounts). You'll also need to make sure your [Google Workspace users can turn on 2-step verification](enable-2-step-verification-for-google-apps).

### Gmail Migration tasks

The following list contains the migration tasks given in the order in which you should complete them.

### Step 1: Verify you own your domain

In this task, you'll first verify to Microsoft 365 or Office 365 that you own the domain you used for your Google Workspace accounts.

Note

Another option is to use the *your company name*.onmicrosoft.com domain that is included with your Microsoft 365 or Office 365 subscription instead of using your own custom domain. In that case, you can just add users as described in [Add users individually or in bulk](/en-us/microsoft-365/admin/add-users/add-users) and omit this task. Most people, however, prefer to use their own domain.

Domain verification is a task you'll go through as you set up Microsoft 365 or Office 365. During setup, the setup wizard provides you with a TXT record you'll add at your domain host provider. See [Add a domain to Microsoft 365](/en-us/microsoft-365/admin/setup/add-domain) for the steps to complete in Microsoft 365 admin center, and choose a domain registrar from the two following options to see how to add the TXT record that your DNS host provider.

- **Your current DNS host provider is Google**: If you purchased your domain from Google and they're the DNS hosting provider, follow these instructions: [Create DNS records when your domain is managed by Google (Go Daddy)](/en-us/microsoft-365/admin/dns/create-dns-records-at-godaddy).
- **You purchased your domain from another domain registrar**: If you purchased your domain from a different company, we provide [instructions](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider) for many popular domain hosting providers.

### Step 2: Add users to Microsoft 365 or Office 365

You can add your users either [one at a time](/en-us/microsoft-365/admin/add-users/add-users), or [several users at a time](/en-us/office365/enterprise/add-several-users-at-the-same-time). When you add users, you also add licenses to them. Each user has to have a mailbox on Microsoft 365 or Office 365 before you can migrate email to it. Each user also needs a license that includes an Exchange Online plan to use his or her mailbox.

Important

At this point you have verified that you own the domain and created your Google Workspace users and mailboxes in Microsoft 365 or Office 365 with your custom domain. Close the wizard at this step. Do not proceed to **Set up domain**, until your Gmail mailboxes are migrated to Microsoft 365 or Office 365. You'll finish the setup steps in task 7, Step 6: Update your DNS records to route Gmail directly to Microsoft 365 or Office 365.

### Step 3: Create a list of Gmail mailboxes to migrate

For this task, you create a migration file that contains a list of Gmail mailboxes to migrate to Microsoft 365 or Office 365. The easiest way to create the migration file is by using Excel, so we use Excel in these instructions. You can use Excel 2013, Excel 2010, or Excel 2007.

When you create the migration file, you need to know the app password of each Gmail mailbox that you want to migrate. We're assuming you don't know the user passwords, so you'll probably need to assign temporary passwords (by resetting the passwords) to all mailboxes during the migration. You must be an administrator in Google Workspace to reset passwords.

You don't have to migrate all Gmail mailboxes at once. You can do them in batches at your convenience. You can include up to 50,000 mailboxes (one row for each user) in your migration file. The file can be as large as 10 MB.

1. Sign in to [Google Workspace admin console](http://admin.google.com/) using your administrator username and password.
2. After you're signed in, choose **Users**.

    ![List of users in the Google admin center.](../../exchangeonline/media/google-users-im11.png)
3. Select each user to identify each user's email address. Write down the address.

    ![User details in the Google apps admin center.](../../exchangeonline/media/google-users-account-im12.png)
4. Open the [Microsoft 365 admin center](https://admin.microsoft.com), and go to **Users** &gt; **Active users**. Keep an eye on the **Username** column. You'll use this information in a minute. Keep the Microsoft 365 admin center window open, too.

    ![Username column in the Microsoft 365 admin center.](../../exchangeonline/media/microsoft365-accounts-im12.png)
5. Start Excel.
6. Use the following screenshot as a template to create the migration file in Excel. Start with the headings in row 1. Make sure they match the picture exactly and don't contain spaces. The exact heading names are:

    - **EmailAddress** in cell A1.
    - **UserName** in cell B1.
    - **Password** in cell C1.

    ![Cell headings in the Excel migration file.](../../exchangeonline/media/excel-im14.png)
7. Next enter the email address, username, and app password for each mailbox you want to migrate. Enter one mailbox per row.

    - **Column A** is the email address of the Microsoft 365 or Office 365 mailbox. This is what's shown in the **username** column in **Users** &gt; **Active users** in the Microsoft 365 admin center.
    - **Column B** is the sign-in name for the user's Gmail mailbox (for example, aaronharper@lemonteatest.com).
    - **Column C** is the app password for the user's Gmail mailbox. Creating the app password is described in Migration from Google Workspace mailboxes using the Microsoft 365 admin center.

    ![A completed sample migration file.](../../exchangeonline/media/excel-im15.png)
8. Save the file as a CSV file type, and then close Excel.

    ![Shows the Save As CSV option in Excel.](../../exchangeonline/media/excel-im16.png)

### Step 4: Connect Microsoft 365 or Office 365 to Gmail

To migrate Gmail mailboxes successfully, Microsoft 365 or Office 365 needs to connect and communicate with Gmail. To do this, Microsoft 365 or Office 365 uses a migration endpoint. Migration endpoint is a technical term that describes the settings that are used to create the connection so you can migrate the mailboxes. Do the following to create a migration endpoint in Exchange admin center.

1. In the Exchange admin center, go to **Migration**.
2. Click **Endpoints** in the top right corner of the page.
3. On the **Endpoints** page, Click **Add**![New icon.](../../exchangeonline/mailbox-migration/media/457cd93f-22c2-4571-9f83-1b129bcfb58e.gif) to create a new migration endpoint.
4. On the **Add Endpoint** page, choose **IMAP** as the migration type.
5. Enter the appropriate information in the following fields:

    - **Migration endpoint name**: Type a unique endpoint name, for example, Test5-endpoint
    - **IMAP server**: Type the *messaging server name* (for example, imap.contoso.com) of the source email server.
    - Leave the remaining information as the default settings; these will work for most cases.
6. Click **Create**.

You successfully created the migration endpoint!

### Step 5: Create a migration batch and start migrating Gmail mailboxes in Exchange admin center

You use a migration batch to migrate groups of Gmail mailboxes to Microsoft 365 or Office 365 at the same time. The batch consists of the Gmail mailboxes that you listed in the migration file in the previous Step 4: Connect Microsoft 365 or Office 365 to Gmail.

Tip

It's a good idea to create a test migration batch with a small number of mailboxes to first test the process. &gt; Use migration files with the same number of rows, and run the batches at similar times during the day. Then compare the total running time for each test batch. This helps you estimate how long it could take to migrate all your mailboxes, how large each migration batch should be, and how many simultaneous connections to the source email system you should use to balance migration speed and internet bandwidth.

1. In the [Exchange admin center](../../exchange-admin-center), go to **Migration**.
2. Click **Add migration batch**.
3. On the **Add migration batch page**, type the name (no spaces or special characters) of the migration batch in the **Give migration batch a unique name** field. For example, Test5-migration.
4. Select **Migrate to Exchange Online** in the dropdown as migration type, and then click **Next**.
5. On the **Select the migration type** page, select **IMAP migration** as migration type and then click **Next**.
6. On the **Prerequisites for IMAP migration** page, check to see if you completed all the prerequisites and then click **Next**.
7. On the **Set a migration endpoint** page, select a migration endpoint from the dropdown list and then click **Next**.
8. On the **Add user mailboxes** page,

    - Download a CSV file with headers only or with sample user information.
    - Open the downloaded file in Excel or other similar app add the users' information that needs to be migrated
    - Click **Import CSV file** and upload the file with the users' information

    After finishing, click **Next**.
9. On the **Select configuration settings** page, click **Next**.
10. In the **Schedule batch migration** page, select the desired options for reporting and start and end migration batch modes.
11. Click **Save** and then click **Done**.

Note

If you have large user mailboxes and the status shows **Syncing** for a long time, you may be experiencing bandwidth limits set by Google. For more information, see [Bandwidth limits](https://support.google.com/a/answer/1071518) and [Sync limits](https://support.google.com/a/answer/2751577). You can try to unlock the Gmail user or use alternative method to migrate the users. For more information, see [Use network upload to import your organization PST files to Microsoft 365 or Office 365](/en-us/purview/use-network-upload-to-import-pst-files) and [Third-party tools for Microsoft 365 or Office 365 migrations](../office-365-migration-best-practices#third-party-tools-for-microsoft-365-or-office-365-migrations).

#### Verify that the migration worked

In the Exchange admin center, go to **Migration**. Verify that the batch is listed. If the migration completed successfully, the status is **Completed**.

- If this task fails, check the associated Mailbox status reports for specific errors, and double-check that your migration file has the correct Microsoft 365 or Office 365 email address in the **EmailAddress** column.

#### Verify a successful mailbox migration to Microsoft 365 or Office 365

- Ask your migrated users to complete the following tasks:
    - Go to the [Microsoft 365 or Office 365 sign-in page](https://login.microsoftonline.com) and sign in with your username and temporary password.
    - Update your password, and set your time zone. It's important that you select the correct time zone to make sure your calendar and email settings are correct.
    - When Outlook on the web (formerly known as Outlook Web App) opens, send an email message to another Microsoft 365 or Office 365 user to verify that you can send email.
    - Choose **Outlook**, and check that your email messages and folders are all there.

### Optional: Reduce email delays

Although this task is optional, doing it can help avoid delays in the receiving email in the new Microsoft 365 or Office 365 mailboxes.

When people outside of your organization send you email, their email systems don't double-check where to send that email every time. Instead, their systems save the location of your email system based on a setting in your DNS server known as a time-to-live (TTL). If you change the location of your email system before the TTL expires, the sender's email system tries to send email to the old location before figuring out that the location changed. This can result in a mail delivery delay. One way to avoid this is to lower the TTL that your DNS server gives to servers outside of your organization. This will make the other organizations refresh the location of your email system more often.

Most email systems ask for an update each hour if a short interval such as 3,600 seconds (one hour) is set. We recommend that you set the interval at least this low before you start the email migration. This setting allows all the systems that send you email enough time to process the change. Then, when you make the final switch over to Microsoft 365 or Office 365, you can change the TTL back to a longer interval.

The place to change the TTL setting is on your email system's mail exchanger record, also called an MX record. This lives in your public facing DNS. If you have more than one MX record, you need to change the value on each record to 3,600 seconds or less.

Don't worry if you skip this task. It might take longer for email to start showing up in your new Microsoft 365 or Office 365 mailboxes, but it will get there.

If you need some help configuring your DNS settings, see [Add DNS records to connect your domain](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).

### Step 6: Update your DNS records to route Gmail directly to Microsoft 365 or Office 365

Email systems use a DNS record called an MX record to figure out where to deliver email. During the email migration process, your MX record was pointing to your Gmail system. Now that you've completed your email migration to Microsoft 365 or Office 365, it's time to point your MX record to Microsoft 365 or Office 365. After you change your MX record following these steps, email sent to users at your custom domain is delivered to Microsoft 365 or Office 365 mailboxes

For many DNS providers, there are specific instructions to change your MX record, see [Add DNS records to connect your domain](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider) for instructions. If your DNS provider isn't included, or if you want to get a sense of the general directions, general MX record instructions are provided as well. See [Add DNS records to connect your domain](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider) for instructions.

1. Sign in to Microsoft 365 or Office 365 with your work or school account.
2. Choose **Setup** &gt; **Domains**.
3. Select your domain and then choose **Fix issues**.

    The status shows **Fix issues** because you stopped the wizard partway through so you could migrate your Gmail email to Microsoft 365 or Office 365 before switching your MX record.

    ![Domain that needs to be fixed.](../../exchangeonline/mailbox-migration/media/35c93050-4eb2-49a4-b1e8-cdb137bba946.jpg)
4. For each DNS record type that you need to add, choose **What do I fix?**, and follow the instructions to add the records for Microsoft 365 or Office 365 services.
5. After you've added all the records, you'll see a message that your domain is set up correctly: **Contoso.com is set up correctly. No action is required.**

It can take up to 72 hours for the email systems of your customers and partners to recognize the changed MX record. Wait at least 72 hours before you proceed to stopping synchronization with Gmail.

### Step 7: Stop synchronization with Gmail

During the last task, you updated the MX record for your domain. Now it's time to verify that all email is being routed to Microsoft 365 or Office 365. After verification, you can delete the migration batch and stop the synchronization between Gmail and Microsoft 365 or Office 365. Before you take this step:

- Make sure that your users are using Microsoft 365 or Office 365 exclusively for email. After you delete the migration batch, email that is sent to Gmail mailboxes isn't copied to Microsoft 365 or Office 365. This means your users can't get that email, so make sure that all users are on the new system.
- Let the migration batch run for at least 72 hours before you delete it. This makes the following two things more likely:

    - Your Gmail mailboxes and Microsoft 365 or Office 365 mailboxes have synchronized at least once (they synchronize once a day).
    - The email systems of your customers and partners have recognized the changes to your MX records and are now properly sending email to your Microsoft 365 or Office 365 mailboxes.

When you delete the migration batch, the migration service cleans up any records related to the migration batch and removes it from the migration dashboard.

#### Delete a migration batch

In the Exchange admin center, go to **Migration**, select the intended batch and click **Delete**. The migration batch is no longer listed.

### Step 8: Users migrate their calendar and contacts

After migration of mailboxes, you can import your Gmail calendar and contacts to Outlook:

- [Import contacts to Outlook](https://support.microsoft.com/office/bb796340-b58a-46c1-90c7-b549b8f3c5f8)
- [Import Google Calendar to Outlook](https://support.microsoft.com/office/098ed60c-936b-41fb-83d6-7e3786437330)

## Leave us a comment

Were these steps helpful? If so, please let us know at the bottom of this topic. If they weren't, and you're still having trouble migrating your email, tell us about it and we'll use your feedback to double-check our steps.