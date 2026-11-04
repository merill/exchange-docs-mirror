---
layout: Conceptual
title: Migrate mail from Google Workspace to Microsoft 365 (automated method) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrate-google-mail-automated-method
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
author: MachelleTranMSFT
ms.author: dansimp
audience: admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Learn how to migrate your mail from Google Workspace to Microsoft 365 using the automated method.
ms.date: 2026-09-25T00:00:00.0000000Z
locale: en-us
document_id: 9b0dc2f2-2858-42b0-bca7-2c5f10347013
document_version_independent_id: c7a7a259-6b77-c986-2ce2-cb81637037ee
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-automated-method.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrate-google-mail-automated-method
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-automated-method.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: d45c41ce-84cd-2e51-04dc-97fc58f27a8b
---

# Migrate mail from Google Workspace to Microsoft 365 (automated method) | Microsoft Learn

The Batch Migration Tool can perform different types of migrations like IMAP, staged migration or cutover migration. For this scenario, we focus on the Google Workspace migration type.

## Step 1 - Add a migration batch

Sign into Microsoft 365 admin center using your administrator credentials.

1. Select **Show all**. Now select **Exchange** in the **Admin centers** section.
2. In the Exchange Admin Center, select **Migration**.
3. On the **Migration batches** page, select **Add migration batch**.
4. Enter a name for your migration batch and select **Migrate to Exchange Online** and select **Next**.

## Step 2 - Select migration type

1. Select **Google Workspace (Gmail) migration** as your migration type.
2. Select **Next**.
3. Repeat the batch migration process until all mailboxes are migrated Google Workspace to Microsoft 365.

## Step 3 - Complete prerequisites

The automated method automatically configures four of the required steps. The list of prerequisites for Google Workspace now displays. Under **Automate the configuration of your Google Workspace for migration**, select **Start**.

1. Sign in with your Google administrator credentials and select **Next**.
2. On the **EAC Migration wants to access your Google Account** page, select **Continue**.

    The batch migration tool completes four of the required tasks.
3. Once all tasks are completed, select the **API access link** to take you to the **API Clients** page in the Google admin console.
4. Select **Add new**.
5. Return to the **Prerequisites** page of the Microsoft 365 batch migration tool. Copy the **ClientID** and **OAuth scopes** fields.
6. Select **Authorize**.
7. Once the prerequisites tasks are completed, select **Next**.

Note

A JSON file is created earlier during this step and has been downloaded to your local computer. You will need this file in the next step.

## Step 4 - Configure migration endpoint

An email migration endpoint is where your Google Workspace emails are moved to during a batch migration. This process can involve moving emails from a local email server to a cloud-based email service or switching between different email platforms.

You can create a migration endpoint in the Exchange Admin Center or by using PowerShell.

1. On the **Set a migration endpoint** page, select **Create a new migration endpoint**. Then, select **Next**.
2. Enter a migration endpoint name and use the default values. Select **Next**.
3. On the **Gmail migration configuration** page, enter the email address of the Google administrator performing the migration.
4. Select **Import JSON** and go to the location where a JSON filed was created and downloaded to your local computer. The JSON file was created earlier during the automated task configuration process. The file is found in your local downloads folder.
5. Select the JSON file, select **Open** and then select **Next**
6. After the endpoint is created, select **Next**.

## Step 5 - Add user mailboxes

### CSV files

To migrate mailbox contents from Google Workspace to Microsoft 365, you need a comma-separated values (CSV) file. The CSV file lists the email addresses of the mailboxes you want to migrate. The CSV file acts as a bridge, enabling Microsoft 365 to process the migration and create user mailboxes.

To create a CSV file, you can create a new spreadsheet in Microsoft Excel or any other tool that supports CSV file creation. You may also use a text editor and save the file as a CSV or TXT file.

When preparing the CSV file for migration, make sure your file follows the CSV format:

- **EmailAddress**: This attribute specifies the user ID for their Microsoft 365 mailbox. For example: "alexw@tailspintoysco.com"

Remember, if the **EmailAddress** is missing from the header row, the migration can. Be sure to type the attributes exactly as shown, without spaces and as single words. Avoid using **Email Address**; instead, use **EmailAddress** as the attribute name.

### Create a CSV file

Use any text editor, or an application like Excel, to create the CSV file.

1. Start Microsoft Excel.
2. Enter **EmailAddress** in cell A1.
3. Enter the email address of a user you want to migrate in A2. Repeat until you've listed all the users you want to migrate in this specific migration batch.
4. Save the file as a CSV file type.
5. On the **Add user mailboxes** page, select **Import CSV file**. Choose the CSV file you created and then select **Next**.
6. On the **Move configuration** page, enter the name of your **Target delivery domain**. The Target delivery domain is the same as the Microsoft 365 mail routing subdomain you created during the prerequisite stage. For example: "m365.tailspintoysco.com".

## Step 6 - Schedule migration

Select your target delivery domain from the dropdown menu and apply any filtering options before scheduling the batch migration.

1. On the **Schedule batch migration**page, choose:
    - who the migration report is sent to
    - when to start the migration batch
    - when to end the migration batch process
2. Select **Save**.
3. When the batch creation completes successfully, select **Done**.
4. On the **Migration** page, you're able to see the status of your migration batch. Initially, the batch is labeled as **Syncing**. The time the batch takes to complete depends on the number of users you're migrating. Select **Refresh**.
5. Once the status changes to **Synced**, select the check mark, and then select **Complete migration batch**.
6. Select **Confirm**.

After your migration has completed successfully, you can now assign Exchange licenses to your migrated users. Have your users verify their emails, contacts, calendars, and rules have been migrated.