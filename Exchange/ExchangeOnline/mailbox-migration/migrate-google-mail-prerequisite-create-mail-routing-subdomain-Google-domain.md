---
layout: Conceptual
title: Prerequisite Step 2 - Create a subdomain to route mail to Google Workspace | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrate-google-mail-prerequisite-create-mail-routing-subdomain-google-domain
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how to create a mail routing subdomain to your Google Workspace domain.
author: MachelleTranMSFT
ms.author: dansimp
ms.service: exchange-online
ms.topic: how-to
ms.date: 2026-09-25T00:00:00.0000000Z
ms.custom: template-how-to
locale: en-us
document_id: 7b0f8186-bad7-8e38-cc68-21c36dc4c279
document_version_independent_id: 66a52d5f-e852-c797-9a82-0de888838d9e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-prerequisite-create-mail-routing-subdomain-Google-domain.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrate-google-mail-prerequisite-create-mail-routing-subdomain-google-domain
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrate-google-mail-prerequisite-create-mail-routing-subdomain-Google-domain.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 85f98e2a-3bfe-1e0c-369e-cd184ed919e0
---

# Prerequisite Step 2 - Create a subdomain to route mail to Google Workspace | Microsoft Learn

Note

This is the second of four steps required before migrating Google mail to Microsoft 365. Complete Prerequisite Step 1 - Create a subdomain in Google Workspace to route mail to Microsoft 365migrate-google-mail-prerequisite-create-mail-routing-subdomain-M365.md)

Important

As an IT administrator, you must have the "Recipient Management" role group assigned before starting the migration process. Learn more: [Permissions in Exchange Online](../permissions-exo/permissions-exo).

## Role of subdomains in mail migration

In Prerequisite Step 1, you created a subdomain to let migrated users receive mail from Google Workspace users who haven't been migrated yet.

Now, you need to create a subdomain in your Google admin console that routes mail to your Google Workspace domain. Creating this subdomain lets Google Workspace users who haven't been migrated to receive mail from users who have been migrated to Microsoft 365.

Setting up your subdomains is important because you want migrated users to exchange mail with users who haven't been migrated. The mail routing subdomain allows uninterrupted communication until you have migrated all users in your organization to Microsoft 365.

Check out our video on Google mail migration prerequisites:

## Create a subdomain in Google admin console

Sign into your Google admin console [Google Workspace Admin page](https://admin.google.com/AdminHome) with your administrator credentials.

1. Select **Add a domain** in the **Domains** section.
2. Enter a name that is a subdomain of your primary domain. A subdomain makes the domain verification process easier.

    For example: If your primary domain is "tailspintoysco.com", your subdomain can be "gws.tailspintoysco.com".
3. Select **User alias domain** and then select **ADD DOMAIN & START VERIFICATION**.
4. Select **CONTINUE** and follow the instructions to verify domain ownership. The domain verification process can take several minutes or up to 48 hours.

## Non-default mail flow rules

If your Microsoft 365 organization uses non-default mail flow rules, verify that the mail flow from Microsoft 365 to Google Workspace is working.

If your organization uses a default remote domain, you must:

- Enable automatic forwarding for the default remote domain or
- Create a new remote domain with automatic forwarding enabled for your Google Workspace routing domain. For example: "gws.tailspintoysco.com".

If automatic forwarding is disabled, mail messages are blocked when users try to automatically forward email to another domain. For more information on remote domains and automatic forwarding, see [Remote domains in Exchange Online](../mail-flow-best-practices/remote-domains/remote-domains).