---
layout: Conceptual
title: What you need to know about a cutover email migration in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/what-to-know-about-a-cutover-migration
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
ms.topic: upgrade-and-migration-article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 961978ef-f434-472d-a811-1801733869da
ms.reviewer: 
description: Learn what happens and what you need to do to prepare for a cutover migration to Microsoft 365 and Office 365.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- MBS150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom:
- Adm_O365
- O365E_ExchSetupMigrStepsCutover
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: 7da1d7fb-89d4-855c-93ca-c7927128dc04
document_version_independent_id: d5a90737-6486-5f9a-2a64-6be76c97838c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/what-to-know-about-a-cutover-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/what-to-know-about-a-cutover-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/what-to-know-about-a-cutover-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 3b1541e6-17a8-e5f0-0212-ea761252958d
---

# What you need to know about a cutover email migration in Exchange Online | Microsoft Learn

As part of a Microsoft 365 or Office 365 deployment, you can migrate the contents of user mailboxes from a source email system to Microsoft 365 or Office 365. When you do this all at one time, it's called a cutover migration. Additionally, this migration method moves mail users, mail contacts, and mail-enabled groups with their membership. Choosing a cutover migration is suggested when:

- Your current on-premises Exchange organization is Microsoft Exchange Server 2003 or later.
- Your on-premises Exchange organization has fewer than 2,000 mailboxes.

    Note

    Even though cutover migration supports moving up to 2000 mailboxes, due to length of time it takes to create and migrate 2000 users, it is more reasonable to migrate 150 users or less.

If a cutover migration won't work for you, see [Ways to migrate email to Microsoft 365 or Office 365](mailbox-migration) for other options.

## Things to consider

Setting up an email cutover migration to Microsoft 365 or Office 365 requires careful planning. Before you begin, here are a few things to consider:

- You can move your entire email organization to Microsoft 365 or Office 365 over a few days and manage user accounts in Microsoft 365 or Office 365.
- A maximum of 2,000 mailboxes can be migrated to Microsoft 365 or Office 365 by using a cutover Exchange migration. However, it is recommended that you only migrate 150 mailboxes.
- The primary domain name used for your on-premises Exchange organization must be an accepted as a domain owned by you in your Microsoft 365 or Office 365 organization.
- After the migration is complete, each user who has an on-premises Exchange mailbox also will be a new user in Microsoft 365 or Office 365. But you'll still have to assign licenses to users whose mailboxes are migrated.

## Impact to users

After your on-premises and Microsoft 365 or Office 365 organizations are set up for a cutover migration, post-setup tasks could impact your users.

- **Administrators or users must configure desktop computers**: Make sure that desktop computers are updated and set up for use with Microsoft 365 or Office 365. These actions allow users to use local user credentials to sign in to Microsoft 365 or Office 365 from desktop applications. Users with permission to install applications can update and set up their own desktops. Or updates can be installed for them. After updates are made, users can send email from Outlook 2013, Outlook 2010, or Outlook 2007.
- **Potential delay in email routing**: Email sent to on-premises users whose mailboxes were migrated to Microsoft 365 or Office 365 are routed to their on-premises Exchange mailboxes until the MX record is changed.

## How does cutover migration work?

The main steps you perform for a cutover migration are shown in the following illustration.

![Process for performing a cutover email migration to Microsoft 365 or Office 365.](../exchangeonline/mailbox-migration/media/a607954b-1ab6-40e6-becc-d61ad5a35d69.png)

1. The administrator communicates upcoming changes to users and verifies domain ownership with the domain registrar.
2. The administrator prepares the servers for a cutover migration and creates empty mail-enabled security groups in Microsoft 365 or Office 365.
3. The administrator connects Microsoft 365 or Office 365 to the on-premises email system (this is called creating a migration endpoint).
4. The administrator migrates the mailboxes and then verifies the migration.
5. Grant Microsoft 365 or Office 365 licenses to your users.
6. The administrator configures the domain to begin routing email directly to Microsoft 365 or Office 365.
7. The administrator verifies that routing has changed, and then deletes the cutover migration batch.
8. The administrator completes post-migration tasks in Microsoft 365 or Office 365 (assigns licenses to users and creates an Autodiscover Domain Name System (DNS) record), and optionally decommissions the on-premises Exchange servers.

    See how-to steps in [Complete post migration tasks](cutover-migration-to-office-365#complete-post-migration-tasks).
9. The administrator sends a welcome letter to users to tell them about Microsoft 365 or Office 365 and to describe how to sign in to their new mailboxes.

## Ready to start?

If you're comfortable setting up a migration to Microsoft 365 or Office 365, here are the tasks that need to be done:

- Set up Exchange Server by using the Exchange admin center.
- Change your organization's MX record to point to Microsoft 365 or Office 365 when the migration is complete. Your MX record is how other mail systems find the location of your email system. Changing your MX record allows other mail systems to begin to send email directly to the new mailboxes in Microsoft 365 or Office 365. We provide instructions on how to do this for many DNS providers. To set up your public DNS servers, you need to change your organization's MX record to point to Microsoft 365 or Office 365 if you choose to route all incoming internet mail for your on-premises Exchange organization through Microsoft 365 or Office 365.

If you're ready to begin a cutover migration, go to [Perform a cutover migration of email](cutover-migration-to-office-365).