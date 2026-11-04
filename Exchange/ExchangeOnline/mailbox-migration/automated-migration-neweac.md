---
layout: Conceptual
title: Perform an automated Google Workspace migration to Microsoft 365 or Office 365 in EAC in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/automated-migration-neweac
Manager: jtremper
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: heidip
author: MicrosoftHeidi
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Instructions for automatically migrating from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches in EAC.
ms.custom: seo-marvel-jun2021
ms.date: 2024-03-15T00:00:00.0000000Z
locale: en-us
document_id: c741294b-65a6-e854-def3-dfff716495c6
document_version_independent_id: b45d93d1-bfc8-ffdf-b191-70fcaba31117
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/automated-migration-neweac.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/automated-migration-neweac
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/automated-migration-neweac.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
platformId: ec3e28ca-2642-427e-1f9f-b0c35a13a24d
---

# Perform an automated Google Workspace migration to Microsoft 365 or Office 365 in EAC in Exchange Online | Microsoft Learn

With the Exchange admin center (EAC), the migration of mails, contacts, and calendar from Google Workspace to Microsoft 365 or Office 365 has been automated. The process has now been simplified to the extent that several of the manual steps that a user had to perform manually are no longer required.

Note

The EAC continues to offer manual migration of Google Workspace to Microsoft 365 or Office 365.

Important

You have to implement all the steps specified in [Google Workspace migration prerequisites in Exchange Online](google-workspace-migration-prerequisites) prior to starting the migration process. Otherwise, the Google Workspace migration to Microsoft 365 or Office 365 won't be successful.

## Watch: Migrate email, calendars, and contacts from Google Workspace through an automated batch migration

Check out this video and others on our [YouTube channel](https://go.microsoft.com/fwlink/?linkid=2198213).

## Start an automated Google Workspace migration batch in EAC

Important

Microsoft's data migration tool is currently unaware of tools enforcing messaging records management (MRM) or archival policies. Because of this unawareness, any messages that are deleted or moved to archive by these policies will result in the migration process flagging these items as "missing." The result is perceived data loss rather than actual data loss, which makes it much harder to identify actual data loss during any content verification checks.

Therefore, Microsoft strongly recommends disabling all MRM and archival policies before attempting any data migration to mailboxes.

1. In the [Exchange Admin center](https://admin.exchange.microsoft.com/), go to **Migration**, and then select **Add migration batch**.

    [![Screenshot that shows the page from which the user can Add a migration batch.](../exchangeonline/mailbox-migration/media/add-migration-batch-option.png)](../exchangeonline/mailbox-migration/media/add-migration-batch-option.png#lightbox)

    The **Add migration batch** page appears.
2. Configure the following settings:

    - **Give migration batch a unique name**: Enter a unique name.
    - **Select the mailbox migration path**: Verify that **Migration to Exchange Online** is selected.

    ![Screenshot of migration wizard that shows the Add migration batch page where the user can specify a unique batch name and select mailbox migration path.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration1.png)

    When you're finished, click **Next**.
3. On the **Select the migration type** page, select **Google Workspace (Gmail) migration** as migration type, and click **Next**.

    ![Screenshot of Select migration type dialog where the user can select the migration type.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration2.png)

    The **Prerequisites for Google Workspace migration** page appears.
4. Verify that the **Automate the configuration of your Google Workspace for migration** section is expanded, and then select **Start** in that section to automate the four required prerequisite steps.

    ![Screenshot of the Prerequisites for Google Workspace Migration dialog showing a list of configuration steps and the start button that will automate the process.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration3.png)
5. In the Google sign-in page that appears, sign in to your Google account to validate your APIs.

    ![Screenshot of the Prerequisites for Google Workspace Migration dialog that shows checkmarks for all the configuration steps indicating that the automation was successful.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration3a.png) Once the APIs are successfully validated, the following things happen:

    - A JSON file (projectid-\*.json) is downloaded to your local system.
    - The link to add the ClientID and the Scope is provided. The ClientID and Scope are also listed for your reference.
6. Select the API access link. You'll be redirected to Google Admin API Controls page.
7. Select **Add new**. Copy the ClientID and Scope from the EAC, paste it here, and then select **Authorize**.
8. Once the four prerequisites-related steps are completed, select **Next**. The **Set a migration endpoint** page appears.
9. Select one of the following options:

    - **Select the migration endpoint**: Select an existing migration endpoint from the drop-down list.
    - **Create a new migration endpoint**: Select this option if you're a first-time user.

    ![Screenshot of Set migration end point dialog where the user can select the migration endpoint or create a new migration endpoint, with the select migration endpoint option selected.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration4.png)

    Note

    To migrate Gmail mailboxes successfully, Microsoft 365 or Office 365 needs to connect and communicate with Gmail. To do this connection-communication, Microsoft 365 or Office 365 uses a migration endpoint. Migration endpoint is a technical term that describes the settings that are used to create the connection so you can migrate the mailboxes.

    If you've selected **Create a new migration endpoint**, do the following steps:

    1. On the **General Information** page, configure the following settings:

        - **Migration Endpoint Name**: Enter a value.
        - **Maximum concurrent migrations**: Leave the default value **20** or change the value as required.
        - **Maximum concurrent incremental syncs**: Leave the default value **10** or change the value as required.

        When you're finished, select **Next**.
    2. On the **Gmail migration configuration** page, configure the following settings:

        - **Email address**: Enter the email address that you use to sign in to the Google Workspace.
        - **JSON key**: Select **Import JSON**. In the dialog box that appears, find and select the downloaded JSON file, and then select **Open**.

        Once the endpoint is successfully created, it will be listed in the **Select migration endpoint** drop-down list.

        - Select the endpoint from the drop-down list, and select **Next**. The **Add user mailboxes** page appears.

    ![Screenshot of Add user mailboxes dialog where the user has the option to import the CSV file.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration5.png)
10. Select **Import CSV file** and navigate to the folder where you've saved the CSV file.

If you haven't already saved or created the CSV file, create a CSV file containing the set of names of the users you want to migrate. You'll need its filename below. The allowed headers are:

- **EmailAddress** (required): Contains the primary email address for an existing Microsoft 365 or Office 365 mailbox.
- **Username** (optional). Contains the Gmail primary email address, if it differs from EmailAddress.

```CSV
EmailAddress
will@fabrikaminc.net
user123@fabrikaminc.net
```

When you're finished, click **Next**. The **Move configuration** page appears.

1. From the **Target delivery domain** drop-down list, select the target delivery domain (the subdomain) that was created as part of fulfilling the [Google Workspace migration prerequisites in Exchange Online](google-workspace-migration-prerequisites), and click **Next**.

![Screenshot of Move configuration dialog where the user can select the target delivery domain. The dialog also shows the Migration filtering options with Mail, Calendar, Contacts, and Rules folders all checked.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration6.png)

Note

The target delivery domain (the subdomain) you select in this step can be either an existing one or the one that you've created in [Google Workspace migration prerequisites in Exchange Online](google-workspace-migration-prerequisites).

If you don't see the target delivery domain that you want to select in the **Target delivery domain** drop-down list, you can manually enter the name of the target delivery domain in the text box.

The text box in which you manually enter the name of the target delivery domain is **Target delivery domain**. That is, the text box is effectively the **Target delivery domain** drop-down list, which is taking the role of a text box when you manually enter text into it.

Filtering options have been introduced for the migration of Google Workspace to Microsoft 365 or Office 365. For more information on these filtering options, see Filtering Options for Google Workspace migration.

1. On the **Schedule batch migration** page, verify all the details, click **Save**, and then click **Done**.

    ![Screenshot of Schedule migration batch that gives the user the ability to list a recipient to notify, specify migration start and end times. eac_admin is listed as the user to notify and the migration start is set to automatically start. Migration batch end time is set to manually complete.](../exchangeonline/mailbox-migration/media/gmail-workspace-migration7.png)

Once the batch status changes from **Syncing** to **Synced**, you need to complete the batch.

To learn more, see the following topics:

- Completion of migration batch: See [Completion of migration batch in EAC](completion-gspace-migration-batch-neweac).
- How the migration happens on the backend: See [Overview of the process](how-it-all-works-in-the-backend).

### Filtering Options for Google Workspace migration

Filtering options enable you to determine what are the mail-related components to be migrated from the Google Workspace.

The filter options for the Google Workspace migration are:

- Mail
- Calendar
- Contacts
- Rules