---
layout: Conceptual
title: Migrate mail from Google Workspace to Microsoft 365 (manual method) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/manually-configuring-gsuite-for-migration
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
description: Instructions to manually configure G-Suite for migration
ms.custom: seo-marvel-jun2021
ms.date: 2023-08-06T00:00:00.0000000Z
locale: en-us
document_id: a0b140ec-7770-5047-3e57-b9f1f2647b10
document_version_independent_id: 3542b0ec-4e55-d833-9dd1-7211cbca9406
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/manually-configuring-gsuite-for-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/manually-configuring-gsuite-for-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/manually-configuring-gsuite-for-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 1f3bf92c-5f29-631a-561e-998549dbd601
---

# Migrate mail from Google Workspace to Microsoft 365 (manual method) | Microsoft Learn

Following procedures are to be performed, if you are attempting manual migration of Google Workspace with either Classic or New EAC:

- Migrate mail from Google Workspace to Microsoft 365 (manual method)
    - Create a Google Service Account
    - Enable API usage in your project
    - Grant access to the service account for your Google tenant

## Create a Google Service Account

1. Using a Chrome browser, sign into your Google Workspace admin console at https://admin.google.com.
2. In a new tab or window, navigate to the [Service Accounts](https://console.developers.google.com/iam-admin/serviceaccounts) page.
3. Select **Create project**, name the project and choose **Create**.
4. Select **+ Create service account**, enter a name, choose **Create** and then **Done**.
5. Open the **Actions** menu, select **Edit**, and take note of the Unique ID. You'll need this ID later in the process.
6. Open the **Show domain-wide delegation** section.
7. Select **Enable G Suite Domain-wide Delegation**, enter a product name for the consent screen, and choose **Save**.

    Note

    The product name is not used by the migration process, but is needed to save in the dialog.
8. Open the **Actions** menu again and select **Create key**.
9. Choose **JSON**, then **Create**. The private key is saved to the download folder on your device.
10. Select **Close**.

## Enable API usage in your project

If your project doesn't already have all of the required APIs enabled, you must enable them.

1. Go to the [Developer page for API Library](https://console.developers.google.com/apis/library) and sign in as the Google user you used above in **Create a Google Service Account**.
2. Select the project that you used above.
3. Search for the following APIs; each one must be enabled. Select **Enable** to enable them for your project:

    - Gmail API
    - Google Calendar API
    - Contacts API
    - People API

## Grant access to the service account for your Google tenant

1. Go to the [Google Workspace Admin page](https://admin.google.com/AdminHome) and sign in as Google Workspace admin for your tenant.
2. Click **Security**, then click **API Controls**, and then click **Manage Domain Wide Delegation**.
3. Next to the **API Clients** list, click **Add new**.
4. In **Client ID**, type the ClientId for the service account you created in the Create a Google Service Account section above.

    ![Add new API client.](../exchangeonline/media/add-a-new-client-id-im7.png)
5. In **OAuth Scopes**, add the required scopes in comma-separated format, with no spaces in between. For example:

    `https://mail.google.com/,https://www.googleapis.com/auth/calendar,https://www.google.com/m8/feeds/,https://www.googleapis.com/auth/gmail.settings.sharing,https://www.googleapis.com/auth/contacts`

    If the OAuth Scopes are entered incorrectly, the resulting list won't match and the migration process will fail later, after you start the migration batch.
6. Click **Authorize**. Verify that the resulting list shows the expected four (4) OAuth scopes.

    Important

    It may take anywhere from 15 minutes to 24 hours for these settings to propagate.