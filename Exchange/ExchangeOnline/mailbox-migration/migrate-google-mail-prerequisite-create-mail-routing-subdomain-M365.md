---
layout: Conceptual
title: Prerequisite Step 1 - Create a subdomain to route mail to Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrate-google-mail-prerequisite-create-mail-routing-subdomain-m365
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how to create a mail routing subdomain to Microsoft 365 when migrating from Google Workspace.
author: MachelleTranMSFT
ms.author: dansimp
ms.service: exchange-online
ms.topic: how-to
ms.date: 2026-09-25T00:00:00.0000000Z
ms.custom: template-how-to
locale: en-us
document_id: dc8701f7-acaf-d35b-33af-d6d3a81eddfa
document_version_independent_id: aac1db66-9944-2ee7-66f7-795fc2da2c3d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-prerequisite-create-mail-routing-subdomain-M365.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrate-google-mail-prerequisite-create-mail-routing-subdomain-m365
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-prerequisite-create-mail-routing-subdomain-M365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 0c30a4c1-94cb-cd52-4d92-203b1e3163c9
---

# Prerequisite Step 1 - Create a subdomain to route mail to Microsoft 365 | Microsoft Learn

Note

This is the first of four steps required before migrating Google mail to Microsoft 365.

Important

As an IT administrator, you must have the "Recipient Management" role group assigned before starting the migration process. Learn more: [Permissions in Exchange Online](../permissions-exo/permissions-exo).

Before you start your migration from Google Workspace to Microsoft 365, you must complete several tasks in the Google admin console and the Microsoft 365 admin center. Performing the prerequisite steps lets you move your data securely without loss.

Check out our video on Google mail migration prerequisites:

## Role of subdomains in mail migration

First, you need to create a subdomain in your Google admin console that routes mail from Google Workspace to Microsoft 365.

This step is important because mail migration occurs in batches. With each batch of users you migrate, you want to make sure migrated users can still exchange mail with users who haven't been migrated. The mail routing subdomain allows uninterrupted communication until you have migrated all users to Microsoft 365.

## Create a subdomain in Google admin console

To create a subdomain that routes mail from Google Workspace to Microsoft 365, sign into the Google admin console with your administrator credentials.

1. Sign into the Google admin console [Google Workspace Admin page](https://admin.google.com/AdminHome).
2. Select **Add a domain** in the **Domains** section.
3. Enter a name that is a subdomain of your primary domain. A subdomain makes the domain verification process easier.

    For example: If your primary domain is "tailspintoysco.com", your subdomain can be "m365.tailspintoysco.com".

    It's not recommended to create a subdomain with an unverified tenant like tenantname.***onmicrosoft.com***. Unverified tenants can cause issues with your migration. If you must use an unverified tenant, we recommend manually verifying the forwarding address or contacting Google support.
4. Select **User alias domain** and then select **ADD DOMAIN & START VERIFICATION**.

    Warning

> 
> If you see this error: **GmailForwardingAddressRequiresVerificationException has occurred**, do not create a subdomain in the Google admin console. Skip to the next step: Add a domain in Microsoft 365 admin center.

1. Select **CONTINUE** and follow the instructions to verify domain ownership. The domain verification process can take several minutes or up to 48 hours.

## Add a domain in Microsoft 365 admin center

1. Log into [Microsoft 365 admin center](https://admin.microsoft.com/AdminPortal) with your administrator credentials.
2. Select **Show all**. Expand **Settings** and select **Domains**.
3. On the **Domains** page, select **Add domain**.
4. Enter the subdomain name you previously created. **For example**: "m365.tailspintoysco.com".
5. Select **Use this domain** and then select **Continue**. Follow the host-specific instructions to connect and verify your domain.

Note

Depending on your primary domain's host provider, Microsoft 365 will try to automatically update your DNS records for the domain.