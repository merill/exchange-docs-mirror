---
layout: Conceptual
title: Use the Microsoft 365 and Office 365 mail migration advisor | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-migration-jump
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: upgrade-and-migration-article
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
description: Use the Microsoft 365 and Office 365 mail migration advisor to perform a hybrid, cutover, staged, Gmail, or IMAP, migration to Microsoft 365 or Office 365.
ms.date: 2019-01-29T00:00:00.0000000Z
locale: en-us
document_id: dac90643-c8f6-2d5a-0113-27a48db85d5a
document_version_independent_id: 29a5b3fb-16df-df30-5eac-7b82b1b55a08
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/mail-migration-jump.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-migration-jump
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/mail-migration-jump.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/d9dfd2a0-aa13-46ef-a37d-ed697b490607
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/06404839-4766-4799-8cab-c0e1c3b55e48
platformId: 5c36f1ee-db4a-bf63-2e46-7b5c862fd1ef
---

# Use the Microsoft 365 and Office 365 mail migration advisor | Microsoft Learn

For migrations from an existing on-premises Exchange Server environment, you can migrate all email, calendar, and contacts from user mailboxes to Microsoft 365 or Office 365. Microsoft 365 and Office 365 provide a [mail migration advisor](https://aka.ms/MailSetupAdvisorFromEDA) to help you move mailboxes from your current mail system to Exchange Online in Microsoft 365 and Office 365 with automated tools and step-by-step guidance. The advisor will recommend the best migration path for your organization based on your current mail system, the number of mailboxes you want to migrate, and how you plan to manage users and user access.

## How do I run the migration advisor?

To run the Microsoft 365 and Office 365 migration advisor, you'll need the following:

- An Office 365 or Microsoft 365 subscription plan that includes Exchange Online. To see which plans support Exchange Online, see [Plan Options](/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-plan-options) and [Exchange Online Service Description](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description).
- A Microsoft 365 or Office 365 account with Global administrator permissions.

After you have everything you need, you can open the mail migration advisor by going to [Mail migration advisor](https://aka.ms/MailSetupAdvisorFromEDA). You'll need to log into your Microsoft 365 or Office 365 organization when you open this link.

## What options will I have when I run the migration advisor?

When you run the advisor, it'll ask you questions about your existing on-premises environment to help you figure out the best way to get your email to Microsoft 365 or Office 365. Depending on your answers, the advisor will choose one of the following migration options:

- **Hybrid**: Hybrid migrations come in a few different flavors - **full**, **minimal**, and **express**.

    - Full hybrid migrations are best for large organizations that have many thousands of mailboxes and need complete integration between their on-premises Exchange organization and Microsoft 365 or Office 365. Active Directory is synchronized with Microsoft 365 and Office 365, free/busy information can be exchanged, enhanced mail flow options become available, and more. If you want to learn more about full hybrid migrations, see [Exchange hybrid deployments](exchange-hybrid).
    - Minimal hybrid migrations are best for medium-sized organizations that have a few hundred to a couple thousand mailboxes and want to finish their migration within a couple months. Like full hybrid, minimal hybrid migrations set up on-going Active Directory synchronization with Microsoft 365 and Office 365 to help with recipient administration. However, features like free/busy synchronization and other enhanced features aren't available. If you want to learn more about minimal hybrid migrations, see [Minimal Hybrid Configuration](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/HCW-Improvement-The-Minimal-Hybrid-Configuration-option/ba-p/605072).
    - Express migrations are best for small organizations that want to finish their migration within a couple weeks. Express migration does a one-time Active Directory synchronization with Microsoft 365 and Office 365 to set up recipients and then helps move their mailboxes to Microsoft 365 or Office 365. No enhanced features are available. If you want to learn more about express hybrid migrations, see [Express Hybrid Migrations](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/New-Exchange-Online-migration-options/ba-p/606109).
- **Staged**: Staged migrations are available for organizations running Exchange 2003 or Exchange 2007 with more than 2000 mailboxes who want to move mailboxes over in batches over a couple weeks. With staged migrations, you perform a one-time Active Directory synchronization with Microsoft 365 or Office 365 to create recipients in Microsoft 365 or Office 365. When that's complete, you can select batches of mailboxes to move gradually to Microsoft 365 or Office 365. After a mailbox is moved, users are provided with new login credentials and need to reconfigure their Outlook and other mail app profiles. For more information about staged migrations, check out [What you need to know about a staged email migration to Microsoft 365 and Office 365](mailbox-migration/what-to-know-about-a-staged-migration).
- **Cutover**: Cutover migrations are best for organizations running Exchange 2003 or Exchange 2007 with fewer than 2000 mailboxes who want to move mailboxes over a couple days. While you can do cutover migrations with later versions of Exchange, we strongly recommend that you use the **Express** hybrid migration option instead. With cutover migrations, Microsoft 365 or Office 365 reads your Active Directory and creates new recipients in Microsoft 365 or Office 365. When that's complete, Microsoft 365 or Office 365 copies the contents of all users' mailboxes to their new mailboxes in Microsoft 365 or Office 365. When complete, users are provided with new login credentials and need to reconfigure their Outlook and other mail app profiles. For more information about cutover migrations, check out [What you need to know about a cutover email migration to Microsoft 365 or Office 365](mailbox-migration/what-to-know-about-a-cutover-migration).

If you want to learn more about these options or need more help deciding which option to use, check out [Ways to migrate multiple email accounts to Microsoft 365 or Office 365](mailbox-migration/mailbox-migration) and [Decide on a migration path](mailbox-migration/decide-on-a-migration-path).