---
layout: Conceptual
title: Decide on a migration path in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/decide-on-a-migration-path
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
ms.assetid: 0d4f2396-9cef-43b8-9bd6-306d01df1e27
ms.reviewer: 
description: Deciding on the best migration path of your users' email to Microsoft 365 or Office 365 can be difficult. This article gives guidance based on your current email system and other factors, such as how quickly you want to migrate to Microsoft 365 or Office 365. Your migration performance varies based on your network, mailbox size, migration speed, and so on.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MBS150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: 112349e0-4e03-7fd5-0ad8-bf94fef819b2
document_version_independent_id: 34d75478-b734-b814-59e3-b01dd2c7687d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/decide-on-a-migration-path.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/decide-on-a-migration-path
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/decide-on-a-migration-path.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 0e504a4f-fc11-e2ef-1eed-0024202e0b6b
---

# Decide on a migration path in Exchange Online | Microsoft Learn

Deciding on the best migration path of your users' email to Microsoft 365 or Office 365 can be difficult. This article gives guidance based on your current email system and other factors, such as how quickly you want to migrate to Microsoft 365 or Office 365. Your migration performance varies based on your network, mailbox size, migration speed, and so on.

Important

This topic is intended for administrators. If you want to migrate email for a single account, see [Migrate email and contacts to Microsoft 365 or Office 365](/en-us/microsoft-365/admin/setup/migrate-email-and-contacts-admin) instead.

## How do I decide which method to use?

Before you start an email migration, review the [limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits) and [Migration performance and best practices](office-365-migration-best-practices) for Exchange Online to make sure you get the performance and behavior you expect after migration.

You can migrate mailboxes from an [Exchange Server](decide-on-a-migration-path#BK_Exchange) or [from another email system](decide-on-a-migration-path#BK_Other). The content in the following sections is organized by email system, and the linked topics help you decide on the best method based on number of mailboxes and your time and mailbox size constraints.

## Your existing system is an Exchange Server

For migrations from an existing on-premises Exchange Server environment, you can migrate all email, calendar items, tasks and contacts from user mailboxes to Office 365. The available methods are [cutover](cutover-migration-to-office-365), [staged](perform-a-staged-migration/perform-a-staged-migration), and [Exchange Hybrid](../mail-migration-jump) migrations. These migration methods copy over all mail data, including contacts, calendar items, and tasks. You can also use the Internet Message Access Protocol ([IMAP](migrating-imap-mailboxes/migrating-imap-mailboxes)) migration from Exchange servers, and if your Exchange server is older than Exchange 2003, IMAP migration is your only option. IMAP migration copies over only email data.

Important

Staged and Exchange Hybrid migrations require that you also set up directory synchronization. For more information, see [Microsoft 365 or Office 365 integration with on-premises environments](/en-us/office365/enterprise/office-365-integration).

For migration recommendations, expand one of the following sections based on your source system:

## Exchange 2003 or Exchange 2007

If your source system is Exchange 2003 or Exchange 2007, consider the following options.

Note

Even though cutover migration supports moving up to 2000 mailboxes, due to length of time it takes to create and migrate 2000 users, it is more reasonable to migrate 150 users or less.

| Number of mailboxes | How quickly do you want to migrate? | Use |
| --- | --- | --- |
| Fewer than 150 | Over a weekend or a few days. | [Cutover](cutover-migration-to-office-365) For an overview, see [What you need to know about a cutover email migration to Microsoft 365 or Office 365](what-to-know-about-a-cutover-migration). |
| Fewer than 150 | Slowly, by migrating a few users at a time. | [Staged](perform-a-staged-migration/perform-a-staged-migration) For an overview, see [What you need to know about a staged email migration](what-to-know-about-a-staged-migration). |
| Over 150 | Over a weekend or a few days. | [Staged](perform-a-staged-migration/perform-a-staged-migration) If you have more than 150 mailboxes , the best method is to use staged migration where you can migrate a limited number of users at a time. This is because cutover migration performance suffers when you try to migrate more than 150 mailboxes. |
| Over 150 | Slowly, by migrating a few users at a time. | [Staged](perform-a-staged-migration/perform-a-staged-migration) |

If the mailboxes you're migrating contain a large amount of data, you can also use the [Import service](/en-us/purview/importing-pst-files-to-office-365) to import PST files to Microsoft 365 or Office 365. You can use the Microsoft 365 or Office 365 Import Service to either ship the files or to import them across the network.

If you have a large number of mailboxes (5,000+), you might want to hire a partner to help you migrate your email data.

You can search for partners on the [Microsoft solution providers](https://www.microsoft.com/solution-providers/) page.

## Exchange 2010, 2013 or 2016

If your source system is Exchange 2010, Exchange 2013 , or Exchange Server 2016, consider the following options.

Note

Even though cutover migration support moving up to 2000 mailboxes, due to length of time it takes to create and migrate 2000 users, it is more reasonable to migrate 150 users or less.

| Number of mailboxes | How quickly do you want to migrate? | Use |
| --- | --- | --- |
| Fewer than 150 | Over a weekend or a few days. | [Cutover](cutover-migration-to-office-365) or [Express migration](use-minimal-hybrid-to-quickly-migrate). |
| Fewer than 150 | Slowly, by migrating a few users at a time. | [Exchange Hybrid](../mail-migration-jump) |
| Over 150 | Over a weekend or a few days. | [Exchange Hybrid](../mail-migration-jump) If you have more than 150 mailboxes, the best method is to use an Exchange hybrid migration where you can migrate a limited number of users at a time. This is because cutover migration performance suffers when you try to migrate more than 150 mailboxes. |
| Over 150 | Slowly, by migrating a few users at a time. | [Exchange Hybrid](../mail-migration-jump) |

If the mailboxes you're migrating contain a large amount of data, you can also use the [Import service](/en-us/purview/importing-pst-files-to-office-365) to import PST files to Microsoft 365 or Office 365. You can use the Import Service to either ship the files or to import them across the network.

If you have a large number of mailboxes (5,000+), you might want to hire a partner to help you migrate your email data.

You can search for partners on the [Microsoft solution providers](https://www.microsoft.com/solution-providers/) page.

## Exchange Server 2000 or earlier versions

For earlier versions of Exchange server, you must use [IMAP migration](migrating-imap-mailboxes/migrate-other-types-of-imap-mailboxes).

## Other email systems

For other email systems that support IMAP, you can use [IMAP migrations](migrating-imap-mailboxes/migrating-imap-mailboxes).

Depending on your source system, see one of the following:

- [Migrate Google Workspace (formerly G Suite) mailboxes to Microsoft 365 or Office 365](migrating-imap-mailboxes/migrate-g-suite-mailboxes)
- [Migrate other types of IMAP mailboxes to Microsoft 365 or Office 365](migrating-imap-mailboxes/migrate-other-types-of-imap-mailboxes)

    This topic includes the instructions for the migration CSV files for Exchange, Mirapoint, Dovecoat, and Courier IMAP.
- [IMAP migration in the Microsoft 365 admin center](migrating-imap-mailboxes/imap-migration-in-the-admin-center)

If the mailboxes you're migrating contain a large amount of data, you can also use the [Import service](/en-us/purview/importing-pst-files-to-office-365) to import PST files to Microsoft 365 or Office 365. You can use the Import Service to either ship the files or to import them across the network.

You can also hire a partner to help you migrate your email data. You can search for partners on the [Microsoft solution providers](https://www.microsoft.com/solution-providers/) page.

## Leave us a comment

Were these instructions helpful? If so, let us know at the bottom of this topic. If they weren't, and you're still having trouble deciding on a migration strategy, tell us what source email system you want to migrate from and we use your feedback to improve our content.