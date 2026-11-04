---
layout: Conceptual
title: Prepare your Gmail or Google Workspace account for connecting to Outlook and Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/prepare-gmail-or-g-suite-accounts
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
ms.assetid: b650957d-4446-425a-ab78-01b89cbead93
ms.reviewer: 
description: Before you connect to your Gmail account from Outlook on the web, or add a Gmail account to Outlook, you need to prepare your Gmail account. You need to turn on 2-step verification for Gmail and then create an app password that Microsoft 365 or Office 365 uses with your Gmail address to make the connection.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- ZOL150
- MET150
- MOW150
- MOP150
- MOE150
- MEW150
- MED150
- MBS150
- MPP160
- ZOL160
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom:
- Adm_O365_Setup
- O365P_MigrationsIMAPGmailAppPass
- O365M_MigrationsIMAPGmailAppPass
- O365E_MigrationsIMAPGmailAppPass
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: e62f5860-4f99-6794-f8d6-2207b7f19979
document_version_independent_id: c28b87f8-1984-6522-021f-bae92e46d08c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/prepare-gmail-or-g-suite-accounts.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrating-imap-mailboxes/prepare-gmail-or-g-suite-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrating-imap-mailboxes/prepare-gmail-or-g-suite-accounts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: c29630e3-24eb-1e1b-05ca-e3fc157fcbec
---

# Prepare your Gmail or Google Workspace account for connecting to Outlook and Microsoft 365 or Office 365 | Microsoft Learn

Important

The ability to add new accounts to Outlook on the web using the Connected accounts feature was removed in September 2018.

Before you [connect to your Gmail](https://support.microsoft.com/office/d7012ff0-924f-4f78-8aca-c3912d886c4d) account from Outlook on the web, or [add a Gmail](https://support.microsoft.com/office/6e27792a-9267-4aa4-8bb6-c84ef146101b) account to Outlook, you need to prepare your Gmail account. You need to turn on 2-step verification for Gmail and then create an app password that Office 365 uses with your Gmail address to make the connection.

You also need to take this action if your admin is planning to migrate your [Gmail](https://support.microsoft.com/office/20fdb8f2-fed8-4b14-baf0-bf04b9c44bf7) or [Google Workspace Gmail](migrate-g-suite-mailboxes) to Microsoft 365 or Office 365.

## Enable IMAP for Gmail and Google Workspace Accounts

**Please make sure that you have enabled IMAP *before* you start the migration process.** Failure to do so results in migration-related issues.

To enable IMAP for Gmail or Google Workspace Accounts:

1. Sign in to your Gmail/Google Workspace account using a supported browser.
2. Select the **gear icon** located at the top right of the screen.
3. In the drop-down menu that appears, select **Settings**.
4. Switch to the **Forwarding and POP/IMAP** tab.
5. Scroll down to the **IMAP access**, and make sure that **Enable IMAP** is selected.
6. Scroll to the bottom. Select **Save Changes**.

## Enable your Gmail to be connected by Microsoft 365 or Office 365

To use an app password with Gmail, you have to first turn on 2-step verification, and then obtain the app password. Once you have an app password, you can use that in combination with your username to connect to Gmail.

### To turn on 2-step verification

1. Sign in to your Gmail account
2. Select **Google apps** &gt; **My Account**.

    ![Choose Google apps and  then My Account.](../../exchangeonline/mailbox-migration/media/9f193437-3e31-46b3-8844-ed30d8f950fa.png)
3. On the My Account page, choose **Sign-in & security**.
4. Under the **Password & sign-in method**, choose the arrow next to the **2-Step verification**, and provide your password if asked.

    ![Choose 2-step verification Off to start turning it on.](../../exchangeonline/mailbox-migration/media/9c75b26b-e987-483b-af0a-82443801a428.png)

    Note

    If you have a google apps account and you can't see this setting, your admin has to first turn it on. For instructions (for admin), see [Enable 2-step verification for your Google Workspace users](enable-2-step-verification-for-google-apps).
5. On the **Signing in with 2-step verification** page, choose **Start setup**.
6. Re-enter your password if asked, and in the **Set up your phone** step, enter or verify your cell phone. On the next step, enter the verification number sent to your cell phone and choose **Verify**.
7. In the Trust this computer step, choose **Next**, and in the **Turn on 2-step verification** step choose **Confirm**.

### To create an app password

1. Sign in to your Gmail account
2. Select **Google apps** &gt; **My Account**.
3. On the My Account page, choose **Sign-in & security**.
4. Under the **Password & sign-in method**, choose the arrow next to the **App passwords**, and provide your password if asked.
5. On the **App passwords** page, in the **Select app** drop-down choose **Other (custom name)**.

    ![Choose Other (Custom name) in the Select app drop-down.](../../exchangeonline/mailbox-migration/media/af7e9293-61a3-4c02-9507-68d529085db5.png)
6. Type in a name, for example Myconnection &gt; **GENERATE**.

    Note the app password under **Your app password for your device**. You can use this password with your Gmail address in the app you're connecting to your Gmail account (or adding you Gmail account to). This combination grants complete access to your Gmail account by the app that's using it.

    After you enter the app password, you don't have to remember it.

    ![Your 16-character passcode.](../../exchangeonline/mailbox-migration/media/0616963f-074b-4ccd-be03-b24a515ea3c3.png)

    Important

    The 16-character app password is displayed with spaces so it's easier to read. When you enter it to the app you want to connect, ignore the spaces and enter it as an unbroken string of 16 characters.
7. Now you're ready to add your Gmail account to Outlook. When you're prompted for a password, you *enter this app password for your Gmail account*. Don't enter your Gmail password. For instructions on adding your Gmail account to Outlook, see these articles:

    - [Add an email account to Outlook](https://support.microsoft.com/office/6e27792a-9267-4aa4-8bb6-c84ef146101b)
    - [Connect email accounts in Outlook on the web (Microsoft 365)](https://support.microsoft.com/office/connect-email-accounts-in-outlook-on-the-web-microsoft-365-d7012ff0-924f-4f78-8aca-c3912d886c4d)

### Optionally revoke the app password

If you need the Gmail connection for a brief time only, for example for an IMAP mailbox migration that your admin is running, you can later revoke the App password.

**To revoke the app password code**:

1. Sign in to you Gmail account
2. Select **Google apps** &gt; **My Account**.
3. On the My Account page, choose **Sign-in & security**.
4. Under the **Password & sign-in method**, choose the arrow next to the **App passwords**, and provide your password if asked.
5. On the **App passwords** page, select **REVOKE** next to the app password you want to revoke.

    ![Choose trash can icon next to the app password you want to revoke.](../../exchangeonline/mailbox-migration/media/54680383-474d-4625-92b8-879fd7af62de.png)