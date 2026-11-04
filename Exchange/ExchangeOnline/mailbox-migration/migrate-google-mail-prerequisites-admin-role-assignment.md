---
layout: Conceptual
title: Prerequisite Step 4 - Verify Google migration administrator role assignments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrate-google-mail-prerequisites-admin-role-assignment
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how to verify Google migration administrator role assignments to migrate mail from Google Workspace to Microsoft 365.
author: MachelleTranMSFT
ms.author: dansimp
ms.service: exchange-online
ms.topic: how-to
ms.date: 2026-09-25T00:00:00.0000000Z
ms.custom: template-how-to
locale: en-us
document_id: 46234192-408f-bca2-54b2-676ca52a6b53
document_version_independent_id: a82641f7-05c3-68ae-0c54-d2bacdd38f2c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-prerequisites-admin-role-assignment.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrate-google-mail-prerequisites-admin-role-assignment
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-prerequisites-admin-role-assignment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: f86cb0f2-bbf9-e2b4-e94c-a71a282ec22f
---

# Prerequisite Step 4 - Verify Google migration administrator role assignments | Microsoft Learn

Note

This is the fourth and final required before migrating Google mail to Microsoft 365. Complete Steps 1-3 before continuing.

- [Step 1 - Create a subdomain in Google Workspace to route mail to Microsoft 365](migrate-google-mail-prerequisite-create-mail-routing-subdomain-m365)
- [Step 2 - Create a subdomain to route mail to Google Workspace](migrate-google-mail-prerequisite-create-mail-routing-subdomain-google-domain)
- [Step 3 - Provision mail users to migrate from Google Workspace to Microsoft 365](migrate-google-mail-prerequisite-provision-m365-users)

Check out our video on Google mail migration prerequisites:

## Assign roles to your Google migration administrator

Your Google migration administrator must be assigned the "Project Creator" role and "Service Accounts Creator" roles before performing mail migration from Google Workspace to Microsoft 365.

1. Sign into your [Google admin console](https://console.cloud.google.com/cloud-resource-manager) with your administrator credentials.
2. Navigate to **Manage Resources**.
3. Select your organization from the **Resources** list.
4. The **INFO PANEL** appears. Select **ADD PRINCIPAL**.
5. Enter the email address of the Google migration administrator in the **New principals** field.
6. In the **Select a role** drop-down, select **Resource Manager** and then select **Project Creator**.
7. Select **+ ADD ANOTHER ROLE**. Select **Service Accounts** from the drop-down and then select **Create Service Accounts**.

Now you're ready to perform your mail migration from Google Workspace to Microsoft 365.