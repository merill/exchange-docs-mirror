---
layout: Conceptual
title: Overview of the G Suite migration process in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/how-it-all-works-in-the-backend
Manager: serdars
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: AshaIyengar21
audience: Admin
ms.topic: upgrade-and-migration-article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Overview of the backend process that takes place while you are migrating from G-Suite to Microsoft 365 or Office 365
ms.custom: seo-marvel-jun2021
ms.date: 2021-07-13T00:00:00.0000000Z
locale: en-us
document_id: 6cfce80b-b1bd-e02c-8392-596d8e55e9b9
document_version_independent_id: 06b48596-0f88-afe1-db71-29973b6582b5
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/how-it-all-works-in-the-backend.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/how-it-all-works-in-the-backend
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/how-it-all-works-in-the-backend.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: ac86da59-a5f4-1ef8-bc94-3f8262492e69
---

# Overview of the G Suite migration process in Exchange Online | Microsoft Learn

Before beginning your migration, review the following diagrams to understand how a Google Workspace staged migration works. The diagrams show how a fictitious company named Fabrikam, Inc., with the domain name *fabrikaminc.net* performed their migration.

![Original setup before G Suite migration.](../exchangeonline/media/gsuite-mig-original-setup.png)

Prior to their migration, the MX record for the base "fabrikaminc.net" domain points to the Google Workspace tenant or mail server where all or most of Fabrikam, Inc.'s users are. Note that users have their primary email addresses at that domain.

![Before the G Suite migration begins.](../exchangeonline/media/gsuite-mig-before-migration.png)

The MX record for the primary domain "fabrikaminc.net" still points to Google Workspace, where all the primary mailboxes reside. To prepare for the migration, new routing domains have been created: the *gsuite.fabrikaminc.net* domain points to Google Workspace and the *o365.fabrikaminc.net* domain points to Microsoft 365 or Office 365.

On the Google Workspace side, aliases have been added for all of the users in the Google Workspace routing domain. On the Microsoft 365 or Office 365 side, MailUsers have been provisioned for all of the users from the Google Workspace tenant. The ExternalEmailAddress field for MailUsers on the Microsoft 365 or Office 365 side were configured to point back to the primary mailbox using the address at the routing domain for the Google Workspace side. Additionally, there should be aliases for the user in the Microsoft 365 or Office 365 routing domain.

The green arrow indicates how, at this point in the migration, User 2 still contacts User 1 through their Google Workspace email addresses.

![During a single batch of a G Suite migration.](../exchangeonline/media/gsuite-mig-during-batch.png)

User 1 and User 2 are part of the first migration batch to Microsoft 365 or Office 365, while User 3 and User 4 will be part of a later batch. The MX record for the primary domain "fabrikaminc.net" still points to Google Workspace, where all the primary mailboxes still reside. Because User 1 and User 2 have had their migrations started, they've been converted from MailUsers to Mailboxes on the Microsoft 365 or Office 365 side.

The ExternalEmailAddress for each user has been moved to a ForwardingSmtpAddress, so that messages sent to User 1 and User 2 will be delivered back to their source mailboxes on the Google Workspace side by rerouting the message back to the Google Workspace routing domain. This is indicated by the red arrows in the above diagram. Mail is still being synced from the source Google Workspace side to the Microsoft 365 or Office 365 side.

![After a single batch of a G Suite migration.](../exchangeonline/media/gsuite-mig-after-batch.png)

The MX record for the primary domain "fabrikaminc.net" still points to Google Workspace. Now that User 1 and User 2 have been fully migrated to Microsoft 365 or Office 365, they should start working out of Microsoft 365 or Office 365. On the Google Workspace side, automatic mail forwarding has been set up for migrated users, so that new emails sent to their Google Workspace address will be delivered instead to the Microsoft 365 or Office 365 address via the routing domain. This is shown by the green arrows in the above diagram.

Important

If your organization has disabled a user's ability to set a forwarding address, the Google Workspace migration tool will also be unable to set the forwarding address. You must enable permissions to set SMTP forwarding in order for forwarding to be set successfully during your migration.

Meanwhile, the forwarding address has been removed from the Microsoft 365 or Office 365 user object, so emails will be delivered to that user in the Microsoft 365 or Office 365 routing domain (as shown by the red arrows above).

![After G Suite migration is complete.](../exchangeonline/media/gsuite-mig-after-migration.png)

After all migration batches have been completed, all users can use their migrated mailboxes on Microsoft 365 or Office 365 as their primary mailbox. A manual MX record update for the primary domain "fabrikaminc.net" then points to the Microsoft 365 or Office 365 organization instead of the Google Workspace tenant. The routing domains and extra aliases can now be removed, as can the Google Workspace tenant. The migration of mail, calendar, and contacts from Google Workspace to Microsoft 365 or Office 365 is now complete.