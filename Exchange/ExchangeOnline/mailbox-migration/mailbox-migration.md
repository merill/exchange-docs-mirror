---
layout: Conceptual
title: Ways to migrate multiple email accounts to Microsoft 365 or Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/mailbox-migration
Manager: jtremper
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
author: MicrosoftHeidi
ms.author: heidip
ms.assetid: 0a4913fe-60fb-498f-9155-a86516418842
ms.reviewer: 
description: Learn all the ways administrators can use to migrate user mailboxes to Microsoft 365 or Office 365.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- MBS150
audience: Admin
f1.keywords:
- CSH
ms.custom:
- Adm_O365
- Adm_O365_Setup
ms.service: exchange-online
ms.date: 2026-07-13T00:00:00.0000000Z
locale: en-us
document_id: 54d88bea-98ed-5884-ba22-6343f1737caa
document_version_independent_id: 40de1e1c-a2c6-590d-375f-c860aa8524d1
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/mailbox-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/mailbox-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/mailbox-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: bd9c669b-9774-183e-6178-5f5ab73f6593
---

# Ways to migrate multiple email accounts to Microsoft 365 or Office 365 | Microsoft Learn

Your organization can migrate email to Microsoft 365 or Office 365 from other systems. Your administrators can [migrate mailboxes from Exchange Server](mailbox-migration#StagedorCutover) or [migrate email from another IMAP-enabled email system](mailbox-migration#IMAP). And your users can [import their own email](mailbox-migration#Import), contacts, and other mailbox information to a Microsoft 365 or Office 365 mailbox created for them. Your organization can also [work with a partner to migrate email](mailbox-migration#Partner).

Before you start an email migration, review [limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits) and [best practices](office-365-migration-best-practices) for Exchange Online to ensure you get the performance and behavior you expect after migration.

For information on choosing the best option for your organization, see [Decide on a migration path](decide-on-a-migration-path) or [Exchange migration advisors](https://aka.ms/office365setup).

Tip

Another option available to assist you with your email migration is [FastTrack Center Benefit Overview](/en-us/fasttrack/fasttrack-benefit-overview). FastTrack specialists can help you plan and perform your migration. For more information, see [Data Migration](/en-us/fasttrack/data-migration).

You can also view an overview video:

## Migrate mailboxes from Exchange Server

For migrations from an existing on-premises Exchange Server environment, an administrator can migrate all email, calendar, and contacts from user mailboxes to Microsoft 365 or Office 365.

![An administrator performs a staged or cutover migration to Microsoft 365 or Office 365. All email, contacts, and calendar information can be migrated for each mailbox.](../exchangeonline/mailbox-migration/media/1e539e0e-bdc6-426b-aff1-2077f6f76eda.png)

There are three types of email migrations that can be made from an Exchange Server:

- **Migrate all mailboxes at once (cutover migration) or Express migration**

    Use this type of migration if you're running Exchange 2003, Exchange 2007, Exchange 2010, or Exchange 2013, and if there are fewer than 2,000 mailboxes. You can perform a cutover migration by starting from the Exchange Admin Center (EAC); for more information, see [Perform a cutover migration to Microsoft 365 or Office 365](cutover-migration-to-office-365). For information on how to use the Express migration, see [Use express migration to migrate Exchange mailboxes to Microsoft 365 or Office 365](use-minimal-hybrid-to-quickly-migrate).

Important

With cutover migration, you can move up to 2,000 mailboxes, but due to length of time it takes to create and migrate 2,000 users, it's more reasonable to migrate 150 users or less.

- **Migrate mailboxes in batches (staged migration)**

    Use this type of migration if you're running Exchange 2003 or Exchange 2007, and if there are more than 2,000 mailboxes. For an overview of staged migration, see [What you need to know about a staged email migration to Microsoft 365 or Office 365](what-to-know-about-a-staged-migration). To perform the migration tasks, see [Perform a staged migration of Exchange Server 2003 and Exchange 2007 to Microsoft 365 or Office 365](perform-a-staged-migration/perform-a-staged-migration).
- **Migrate using an integrated Exchange Server and Microsoft 365 or Office 365 environment (hybrid)**

    Use this type of migration to maintain both on-premises and online mailboxes for your organization and to gradually migrate users and email to Microsoft 365 or Office 365. Use this type of migration if:

    - You have Exchange 2010 and more than 150-2,000 mailboxes.
    - You have Exchange 2010 and want to migrate mailboxes in small batches over time.
    - You have Exchange 2013 or later.

        For more information, see [Use the Microsoft 365 and Office 365 mail migration advisor](../mail-migration-jump).

## Use the Import Service to migrate PST files

If your organization has many large PST files, you can use the Import Service to migrate email data to Microsoft 365 or Office 365.

![An administrator migrates PST files to Microsoft 365 or Office 365.](../exchangeonline/mailbox-migration/media/23459be8-cf49-41f9-85fc-14e4ad2c06f3.png)

You can use the Import Service either to upload the PST files through a network or to mail the PST files in a drive that you prepare.

For more information, see [Overview of importing your organization's PST files](/en-us/purview/importing-pst-files-to-office-365).

## Migrate email from another IMAP-enabled email system

You can use the Internet Message Access Protocol (IMAP) to migrate user email from Gmail, Exchange, Outlook.com, and other email systems that support IMAP migration. When you migrate the user's email by using IMAP, only the items in the users' inbox or other mail folders are migrated. Contacts, calendar items, and tasks can't be migrated with IMAP; a user can manually migrate them.

IMAP migration also doesn't create mailboxes in Microsoft 365 or Office 365. You'll have to create a mailbox for each user before you migrate their email.

![An administrator performs an IMAP migration to Microsoft 365 or Office 365. All emails, but not contacts or calendar information, can be migrated for each mailbox.](../exchangeonline/mailbox-migration/media/624879f0-305f-4893-b4c2-c64736a40d94.png)

To migrate email from another mail system, see [Migrate your IMAP mailboxes to Microsoft 365 or Office 365](migrating-imap-mailboxes/migrating-imap-mailboxes). After the email migration is done, any new mail sent to the source email isn't migrated.

## Have users import their own email

Users can import their own email, contacts, and other mailbox information to Microsoft 365 or Office 365. For information on how to do it, see [Migrate email and contacts to Microsoft 365 or Office 365](/en-us/microsoft-365/admin/setup/migrate-email-and-contacts-admin).

![A user can import email, contacts, and calendar information to Microsoft 365 or Office 365.](../exchangeonline/mailbox-migration/media/86255b6b-a1bf-413d-b3f2-95ad43a628c0.png)

## Work with a partner to migrate email

If none of the types of migrations described will work for your organization, consider working with a partner to migrate email to Microsoft 365 or Office 365.

For information on how to find a partner, see the [Microsoft solution providers](https://www.microsoft.com/solution-providers/) page.

### Users provisioning for the different migration types

| Exchange Migration Type | Source | Target | Recipient in Target |
| --- | --- | --- | --- |
| Hybrid onboarding | Exchange &gt; On-premises &gt; Hybrid Org A | Exchange &gt; Online &gt; Hybrid Org A | Mail User with ExchangeGuid |
| Hybrid offboarding | Exchange &gt; Online &gt; Hybrid Org A | Exchange &gt; On-premises &gt; Hybrid Org B | Mail User / Remote Mailbox with ExchangeGuid |
| Cross-tenant Migration | Exchange &gt; Online &gt; Tenant A | Exchange &gt; Online &gt; Tenant B | Mail User with ExchangeGuid + matching attributes |
| Cutover migration | Exchange &gt; On-premises | Exchange &gt; Online | No recipient (migration service creates the mailbox in EXO) |
| Gmail migration | Google Workspace | Exchange &gt; Online | Mail User (migration service converts to mailbox in EXO) |
| IMAP migration | IMAP server | Exchange &gt; Online | Mailbox |