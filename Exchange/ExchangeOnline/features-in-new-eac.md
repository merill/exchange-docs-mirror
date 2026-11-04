---
layout: Conceptual
title: EAC in Exchange Online - Get to EAC and Features in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/features-in-new-eac
Manager: serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn about the features in EAC.
ms.topic: overview
author: Benny-54
ms.author: serdars
ms.assetid: 
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2021-04-14T00:00:00.0000000Z
locale: en-us
document_id: b729e505-d40d-fb06-1b01-ffa2a618b90b
document_version_independent_id: 05990383-f705-f8ad-ec30-a69f5503cb74
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/features-in-new-eac.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: features-in-new-eac
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/features-in-new-eac.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 35671b9b-43a9-5ac9-e59a-3bf263e80ccb
---

# EAC in Exchange Online - Get to EAC and Features in Exchange Online | Microsoft Learn

The Exchange admin center (EAC) is simple and accessible, and it enables you to perform tasks like restoring mailboxes, migrating data, and much more.

## Get to the EAC

You must have [Microsoft 365 admin permissions](/en-us/microsoft-365/admin/add-users/assign-admin-roles) to access the EAC. For more information, see [Permissions in Exchange Online](permissions-exo/permissions-exo).

1. [Sign in](https://support.microsoft.com/office/e9eb7d51-5430-4929-91ab-6157c5a050b4) to Microsoft 365 or Office 365 using your work or school account.
2. In the left navigation pane, choose **Admin centers** &gt; **Exchange**.

    ![EAC.](exchangeonline/media/new-eac-selection.png)

You can also get to the EAC directly by using the URL https://admin.exchange.microsoft.com and by signing in using your credentials.

Note

Ensure that you use a private browsing session (not a regular session) when trying to access the EAC using the direct URL. This private session will prevent the credential that you're currently signed in with from being used. To open an InPrivate Browsing session in Microsoft Edge or an incognito window in Google Chrome, press CTRL+SHIFT+N. To open an InPrivate Browsing session in Microsoft Edge Legacy, Internet Explorer, or to open a Private Browsing session in Mozilla Firefox, press CTRL+SHIFT+P.

## EAC features

Here's what the EAC looks like.

![EAC homepage.](exchangeonline/media/new-eac-home-page.png)

### Home page

You can personalize your home page by selecting a theme, and by setting your language and timezone from the **Settings** bubble.

1. To personalize your dashboard, select **+ Add card** on top of the homepage and drag any card to the location you want on the dashboard.
2. To learn about the new updates in the EAC, select **What's New?**.
3. To sign out of the EAC and sign in as a different user, select **My account tile**. You can also sign in with another account.
4. To learn about the EAC, in **Training & guide**, select **Training for admins** for a video tutorial and then select **Documentation**.
5. To get help from Microsoft 365 Support assistant, select ![get help.](exchangeonline/media/get-help-icon.png).
6. To give feedback to help improve the EAC, select ![give feedback.](exchangeonline/media/give-feedback-icon.png). While it's not necessary to provide your email ID, you can check the **You can contact me about this feedback** checkbox and provide your email ID to help the team resolve your concerns faster.

![EAC feature pane.](exchangeonline/media/new-eac-home-page-feature-pane.png)

### Feature pane

Here are the features available in the left-hand navigation.

| Area | What you do here |
| --- | --- |
| **Recipients** | View and manage your mailboxes (both user and shared mailboxes), groups, resource mailboxes, and contacts. |
| **Mail flow** | Trace messages; create rules; manage remote domains and accepted domains; add connectors; and manage alerts and alert policies. |
| **Roles** | Manage administrator roles. |
| **Migration** | Migrate mailboxes in batches. |
| **Reports** | View reports on mail flow and migration batches. |
| **Insights** | Use the recommendations to discover trends and/or insights, and take actions to fix issues related to mailbox and mail flow. |
| **Organization** | Manage organization sharing and apps for Outlook. |
| **Public folders** | Manage public folders and public folder mailboxes. |

### Tabs

The tabs are your second level of navigation. Each of the feature areas contains various tabs, with each tab representing a complete feature.

### Toolbar

When you select most tabs, you'll see a toolbar. The toolbar has icons that perform a specific action.

### List view

When you select a tab, in most cases you'll see a list view. The list view in the EAC is designed to remove limitations that existed in the Exchange Control Panel.

![EAC tabs.](exchangeonline/media/new-eac-home-page-details-pane.png)

### Details pane

When you select an item from the list view, information about that item is displayed in the **Details** pane.

**To bulk edit several items**: Select the objects you want to bulk edit, and use the options in the toolbar.