---
layout: Conceptual
title: Perform manual Google Workspace migration in the Exchange admin center in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/manual-gspace-migration-neweac
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: AshaIyengar21
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Instructions for manually migrating from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches in EAC.
ms.custom: seo-marvel-jun2021
ms.date: 2024-03-15T00:00:00.0000000Z
locale: en-us
document_id: 43a69b65-0644-8591-428d-3df7a0f34ea3
document_version_independent_id: 17b874b6-54e2-7859-3a07-ef0402cbbe26
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/manual-gspace-migration-neweac.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/manual-gspace-migration-neweac
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/manual-gspace-migration-neweac.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 6eb4a40f-092f-27cc-6350-054b6ab5e565
---

# Perform manual Google Workspace migration in the Exchange admin center in Exchange Online | Microsoft Learn

The migration process takes several steps and can take from several hours to a couple of days depending on the amount of data you're migrating.

## Prerequisites

Before you begin Google Workspace migration:

1. Ensure you're signed into Google Workspace as a project creator.
2. You have completed the following procedures:
    - Create a subdomain for mail routing to Microsoft 365 or Office 365
    - Create a subdomain for mail routing to your Google Workspace domain
    - Provision users in Microsoft 365 or Office 365

[Learn more at Google Workspace Mail Migration Prerequisites](google-workspace-migration-prerequisites).

## Start a Google Workspace migration batch with the Exchange admin center

Important

Microsoft's data migration tool is currently unaware of tools enforcing messaging records management (MRM) or archival policies. Because of this, any messages that are deleted or moved to archive by these policies will result in the migration process flagging these items as "missing". The result is perceived data loss rather than actual data loss, which makes it much harder to identify actual data loss during any content verification checks.

Therefore, Microsoft strongly recommends disabling all MRM and archival policies before attempting any data migration to mailboxes.

1. In the [Exchange Admin center](https://admin.exchange.microsoft.com), go to **Migration** and then click **Add migration batch**.

    ![Screenshot of Add migration batch wizard where the user can specify the name for the migration and the migration path.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration1.png)
2. On the **Add migration batch** page, configure the following settings:

    - **Give the migration batch a unique name**: Enter a unique name.
    - **Select the mailbox migration path**: Verify that **Migration to Exchange Online** is selected.

    When you're finished, click **Next**. ![Screenshot of the second step of the migration batch wizard with the migration type selected as Google Workspace (Gmail) migration.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration2.png)
3. On the **Select the migration type** page, select **Google Workspace (Gmail) migration**, and then click **Next**

    ![Screenshot of the third steps of the migration batch wizard where the manually configure Google workspace migration is selected.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration-manual.png)
4. On the **Prerequisites for Google Workspace migration** page, expand the **Manually configure your Google Workspace for migration**. As described in the section, configure the following steps:

    1. [Create a Google Service Account](manually-configuring-gsuite-for-migration#create-a-google-service-account)
    2. [Enable API Usage in your project](manually-configuring-gsuite-for-migration#enable-api-usage-in-your-project)
    3. [Grant access to the service account for your Google tenant](manually-configuring-gsuite-for-migration#grant-access-to-the-service-account-for-your-google-tenant)

    When you're finished, click **Next**.

    ![Screenshot of the fourth step of the migration batch wizard with an existing migration endpoint selected.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration4.png)
5. On the **Set a migration endpoint** page of the wizard, select one of the following options:

    - **Select the migration endpoint**: Select the existing migration endpoint from the drop-down list.
    - **Create a new migration endpoint**: Select this option if you're a first-time user.

    Note

    To migrate Gmail mailboxes successfully, Microsoft 365 or Office 365 needs to connect and communicate with Gmail. To do this, Microsoft 365 or Office 365 uses a migration endpoint. Migration endpoint is a technical term that describes the settings that are used to create the connection so you can migrate the mailboxes.

    If you selected **Create a new migration endpoint**, do the following steps:

    1. On the **General Information** page, configure the following settings:

        - **Migration Endpoint Name**: Enter a value.
        - **Maximum concurrent migrations**: Leave the default value 20 or change the value as required.
        - **Maximum concurrent incremental syncs**: Leave the default value 10 or change the value as required.

        When you're finished, click **Next**.
    2. On the **Gmail migration configuration** page, configure the following settings:

        - **Email address**: Enter the email address that you use to sign in to the Google Workspace.
        - **JSON key**: Click **Import JSON**. In the dialog that appears, find and select the downloaded JSON file, and then click **Open**.

        Once the endpoint is successfully created, it will be listed under **Select migration endpoint** drop-down.

        Select the endpoint from the drop-down list, and click **Next**.

    ![Screenshot of the fifth step of the Add migration batch wizard where the user can add user mailboxes.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration5.png)
6. On the **Add user mailboxes** page, click **Import CSV file** and navigate to the folder where you have saved the CSV file.

    If you haven't already, create a CSV file containing the set of all of the users you want to migrate. You'll need its filename below. The allowed headers are:

    - **EmailAddress** (required): Contains the primary email address for an existing Microsoft 365 or Office 365 mailbox.
    - **Username** (optional). Contains the Gmail primary email address, if it differs from EmailAddress.

    ```CSV
    EmailAddress
    will@fabrikaminc.net
    user123@fabrikaminc.net
    ```

    When you're finished, click **Next**.

    ![Screenshot of the sixth step of the Add Migration Batch wizard showing the target delivery domain and the mail, calendar, contacts, and rules folders selected.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration6.png)
7. On the **Move configuration** page, select the **Target delivery domain** from the drop down, verify other details and click **Next**.
8. On the **Schedule batch migration** page, verify all the details, click **Save** and click **Done**.

Once the batch status changes from **Syncing** to **Synced**, you need to complete the batch.

To learn more, see the following topics:

- Completion of migration batch: See [Completion of migration batch in EAC](completion-gspace-migration-batch-neweac).
- How the migration happens on the backend: See [Overview of the process](how-it-all-works-in-the-backend).