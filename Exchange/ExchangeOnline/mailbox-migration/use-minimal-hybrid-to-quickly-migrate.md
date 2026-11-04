---
layout: Conceptual
title: Use Minimal Hybrid to quickly migrate Exchange mailboxes to Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/use-minimal-hybrid-to-quickly-migrate
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
ms.author: serdars
ms.assetid: fdecceed-0702-4af3-85be-f2a0013937ef
ms.reviewer: 
description: Learn how to do an Express migration of on-premises Exchange mailboxes to Microsoft 365 or Office 365.
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
ms.custom:
- Adm_O365
- Adm_O365_Setup
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: 852cee18-246c-8c33-9834-fd96595b3e71
document_version_independent_id: 094c2d24-81dc-41c7-48be-c61df7b25fbc
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/use-minimal-hybrid-to-quickly-migrate.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/use-minimal-hybrid-to-quickly-migrate
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/use-minimal-hybrid-to-quickly-migrate.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: f2884504-168f-15bd-0d16-e0b3ef5f4c51
---

# Use Minimal Hybrid to quickly migrate Exchange mailboxes to Microsoft 365 or Office 365 | Microsoft Learn

You can use the minimal hybrid, also known as express migration, option in the Exchange Hybrid Configuration Wizard to migrate the contents of user mailboxes to Microsoft 365 or Office 365 over a course of couple of weeks or less.

## Pre-requisites

Use minimal hybrid to migrate emails if you:

- Are running at least one Exchange 2010, Exchange 2013, and/or Exchange 2016 server on-premises.
- Plan to move to Exchange Online over a course of few weeks or less.
- Don't plan to continue to run directory synchronization to manage your users.

## Step 1: Verify your own the domain

During the migration, the Simple Mail Transfer Protocol (SMTP) address of each on-premises mailbox is used to create the email address for a new Office 365 mailbox. To run an express migration, the on-premises domain must be a verified domain in your Microsoft 365 or Office 365 organization.

1. Sign in to Microsoft 365 or Office 365 with your work or school account.
2. Choose **Setup** &gt; **Domains**.
3. On the **Domains-** page, click **Add domain** to start the domain wizard.

    ![Choose Add domain.](../exchangeonline/mailbox-migration/media/b0267b62-3f20-4c76-be75-40f9c2274433.png)
4. On the **Add a domain** page, type in the domain name (for example, Contoso.com) you use for your on-premises Exchange organization, and then choose **Next**.
5. On the **Verify domain** page, select either **Sign in to GoDaddy** (if your DNS records are managed by GoDaddy) or **Add a TXT record instead** for any other registrars &gt; **Next**.
6. Follow the instructions provided for your DNS hosting provider. The TXT record usually is chosen to verify ownership.

    You can also find the instructions in [Create DNS records at any DNS hosting provider for Office 365](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).

    After you add your TXT or MX record, wait about 15 minutes before proceeding to the next step.
7. In the domain wizard, choose **done, verify now**, and you'll see a verification page. Choose **Finish**.

    If the verification fails at first, wait awhile, and try again.

    **Do not continue to the next step in the domains wizard**. You now have verified that you own the on-premises Exchange organization domain and are ready to continue with an email migration.

    You'll finish setting up your domain after the migrations are complete.

## Step 2: Start express migration

On a computer that is domain joined to your on-premises organization, sign in to your Microsoft 365 or Office 365 account by using your global admin credentials, and start the Exchange Hybrid Configuration Wizard on the **Data migration** page of the Microsoft 365 admin center.

1. In the Microsoft 365 Admin center, go to **Setup** &gt; **Migrations**.
2. On the **Migrations** page, choose **Email**.
3. On the **Migrate your email** page, choose **Get started**.
4. On the **Email sources** page, choose **Download the Hybrid Configuration Wizard**.
5. On the Download and run the **Office 365 Hybrid Configuration Wizard** page, choose **Download application**
6. On the first **Hybrid Configuration Wizard** page, choose **next** and on the **On-premises Exchange Server Organization** page, accept the default values and choose **next**.

    By default the wizard connects to the Exchange server running the latest version.
7. On the Credentials page, choose **Use current Windows credentials** for on-premises Exchange server, and enter admin credentials for it and your Microsoft 365 or Office 365 organization choose **next**, and then choose **next** again once the connections and credentials have validated.
8. On the **Hybrid Features** page, select **Minimal Hybrid Configuration** &gt; **next**.

    ![On the Hybrid Features page select Minimal Hybrid Configuration.](../exchangeonline/mailbox-migration/media/40e3c3b9-5a95-4226-835f-eb99a23f9c18.png)
9. On the **Ready for Update** page, choose **update** to prepare the on-premises mailboxes for migration.

## Step 3: Run directory synchronization to create users in Microsoft 365 or Office 365

1. On the **User Provisioning** page, select **Synchronize my users and passwords one time**.

    At this point you're prompted to download and install the **Microsoft Entra Connect wizard** to synchronize your users from on-premises to Microsoft 365 or Office 365.
2. Once Microsoft Entra Connect has downloaded, run it and choose the **default options for [Express settings](/en-us/entra/identity/hybrid/connect/how-to-connect-install-express)**.

    After synchronization is completed, you'll be taken to the **Data migration** page where you can see all of your users that were synchronized to Microsoft 365 or Office 365.

    After the one-time synchronization is done, directory synchronization is turned off for your Microsoft 365 or Office 365 organization.

![On the User Provisioning page select Synchronize my users and passwords one time.](../exchangeonline/mailbox-migration/media/8595f8d4-70d1-48f9-8e20-5106936dc148.png)

## Step 4: Give Microsoft 365 or Office 365 licenses to your users

After Microsoft Entra Connect synchronizes your users and their passwords to Microsoft 365 or Office 365, you have to assign licenses to them so that they have a cloud mailbox to which to migrate their on-premises mailbox data.

The status on the **Data migration** page indicates that a license is needed as shown in the figure.

In the Admin center, go to **Users** &gt; **Active users** and follow these instructions to [Add users individually or in bulk](/en-us/microsoft-365/admin/add-users/add-users).

![User status on the Data migration page indicate if a user needs a license.](../exchangeonline/mailbox-migration/media/f0f211f2-be43-493e-bf6b-e9279c76d03e.png)

## Step 5: Start migrating user mailbox data

After you assign licences to your users you can go to the Data migration page to start migrating their mailboxes.

1. Go to **Setup** &gt; **Data migration**, and on the **Migration** page choose **Exchange** for your data service.
2. On the **Data migration** page, select the users whose mailboxes you want to migrate and then choose **Start migration**.

    It's recommended that you migrate mailboxes for two or three users as a test before migrating all of your users to make sure everything works as expected.

    The Data migration page displays the migration status as it progresses. For a full list, see [Migration users status report](migration-users-status-report), which you can also view in the Exchange admin center.

![The Data migration page displays migrations status for each user.](../exchangeonline/mailbox-migration/media/e4433e1f-b071-4868-9b18-1ebca0d7c21e.png)

## Step 6: Update DNS records

Email systems use a DNS record called an MX record to figure out where to deliver emails. During the email migration process, your MX record was pointing to your on-premises Exchange email system. Now that the email migration to Microsoft 365 or Office 365 is complete, it's time to point your MX record at Microsoft 365 or Office 365. You'll also need to finish setting up your DNS records. In the Microsoft 365 admin center, go to **Settings** &gt; **Domains** and then choose the domain name you want to update, for example contoso.com. The domains wizard guides you through the update steps. See this article for instructions specific to your registrar or host: [Add DNS records to connect your domain](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider#add-an-mx-record-for-email-outlook-exchange-online).