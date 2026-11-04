---
layout: Conceptual
title: Migrate Gmail to Microsoft 365 or Office 365 using GoDaddy | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/migrating-mailboxes-using-third-party-tool-godaddy/migrate-gmail-to-m365-using-godaddy
Manager: dansimp
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: v-smandalika
author: v-smandalika
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Instructions for migrating mailboxes in Google Workspace to Microsoft 365 or Office 365 using GoDaddy.
ms.custom: seo-marvel-jun2021
ms.date: 2026-09-25T00:00:00.0000000Z
locale: en-us
document_id: 31f25bf9-3a02-0489-b086-b7334a023aea
document_version_independent_id: 14063963-077b-e6b6-80f0-813f09380dc9
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/migrating-mailboxes-using-third-party-tool-godaddy/migrate-gmail-to-m365-using-godaddy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/migrating-mailboxes-using-third-party-tool-godaddy/migrate-gmail-to-m365-using-godaddy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/migrating-mailboxes-using-third-party-tool-godaddy/migrate-gmail-to-m365-using-godaddy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 41038551-c911-1c5b-0a70-42d4a05a489d
---

# Migrate Gmail to Microsoft 365 or Office 365 using GoDaddy | Microsoft Learn

You can perform migration of Google Workspace to Microsoft 365 or Office 365 using the services offered by GoDaddy.

## Prerequisites

You have to fulfill a few prerequisites to avail GoDaddy's services in migrating Google Workspace mailboxes.

1. Download and install Outlook Migration Assistant.

    Note

    You must perform this step only if you set up your Outlook client with POP3 email settings.
2. Comply with [these](https://in.godaddy.com/help/what-is-the-outlook-migration-assistant-27814) requirements.

## Starting the migration

Before starting the mailbox migration process, contact a GoDaddy guide, who can guide you in customizing your migration, including:

1. Which mailboxes are migrating to Microsoft 365.
2. Setting up any add-ons like Advanced Email Security, Email Archiving, or Email Backup.
3. Adding email aliases, distribution groups, and/or forwarding addresses.
4. Choosing a date to start using Microsoft 365.

The following steps are involved in the mailbox migration process, in which you can avail the services of the GoDaddy guide:

- Domain verification
- Providing passwords
- Download the Outlook Migration Assistant
- Change DNS settings on migration day
- Provide a 48-hour window post-migration

### Domain verification

Microsoft 365 setup requires proof that you own your domain. You can prove it by entering a TXT record on the domain DNS. The GoDaddy guide sends you the instructions to update your DNS by email.

Important

You must get this step done as early as possible or else your migration might be delayed. This change doesn't interrupt your current email service.

Note

If you already set up your Microsoft 365 accounts before contacting a GoDaddy guide, or if your domain and DNS are in the same GoDaddy account as the migration, the guide performs this step for you. The TXT record for a GoDaddy managed-DNS is usually not required.

### Providing passwords

1. Provide your email address and password in the unique secure link that is provided by the GoDaddy migration partner **SkyKick** (email address is **`upgrades@skykick.com`**). These details enable GoDaddy to access your accounts and to start the data synchronization by migrating your emails from the current email service you're using to Microsoft 365 or Office 365.

    Note

    If you're migrating from GoDaddy Workspace Email, you don't have to enter your current email passwords. They already have everything they need to handle this part.
2. Set a password for your new Microsoft 365 account in the page that appears after you enter your current information.
3. Continue using your current email service while the GoDaddy guide and team begin migrating emails in the background.

    Note

    You can use your new Microsoft 365 account once the GoDaddy guide and team complete migrating your emails to Microsoft 365 or Office 365.

### Download the Outlook Migration Assistant

Download the [Outlook Migration Assistant](https://productivity.godaddy.com/app/outlook-migration-assistant#) to enable a smooth migration process in which more data and settings are migrated.

Important

This assistant is only available for Windows PC users. Download it before your scheduled upgrade date.

If the users download and install the Outlook Migration Assistant before the upgrade date, the Outlook Migration Assistant does the following things for you:

1. Automatically creates a new profile in Outlook that uses the new Microsoft 365 email.
2. Migrates local .PST content from the old email into the new profile. This content includes:
    - POP email data
    - Contacts/Calendars/Tasks
    - Signatures
    - Autocomplete Cache

Your account holder receives daily reports regarding downloads of Outlook Migration Assistant by you (and other such users as you).

If you're unable to use the Outlook Migration Assistant, you need to manually move any local content and set up the client. You receive instructions from the GoDaddy guide and team regarding this manual migration on the migration date.

Note

You can't use the Outlook Migration Assistant in the following scenarios:

- You're a Mac user.
- You haven't set up Outlook till now.

### Change DNS settings on migration day

On the date and time of your choosing to migrate your mailbox content to Microsoft 365, change your DNS settings to point to Microsoft 365 for the following reasons:

1. You can start using your new email once the migration is done.
2. The Outlook Migration Assistant (if you downloaded it) can finish setting up your Outlook client.

You receive the DNS settings through an email 8 hours before the migration. Instruct your DNS provider to change these DNS settings within the 8 hours before the start of the migration.

Note

If your domain and DNS are in the same GoDaddy account as the migration, the GoDaddy team changes the DNS settings for you.

### Provide a 48-hour window post-migration

Once the migration is complete, wait for 48 hours before you start using your new Microsoft 365 account. This 48-hour period is for the GoDaddy team to sync final emails from your previous email server to your new Microsoft 365 account. This delay ensures no new emails are missed during the migration.

Note

The GoDaddy team continues to monitor your old accounts for up to 72 hours from the time the migration completes. This monitoring is to check if any emails have been misrouted during the transition.