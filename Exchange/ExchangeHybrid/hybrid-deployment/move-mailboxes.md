---
layout: Conceptual
title: Move mailboxes between on-premises and Exchange Online organizations in hybrid deployments | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/move-mailboxes
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
audience: ITPro
ms.topic: install-set-up-deploy
f1.keywords:
- CSH
ms.custom:
- O365E_HRCMoveRequest_FL312271
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
- M365-email-calendar
ms.assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms.reviewer: 
description: With an Exchange-based hybrid deployment, you can choose to either move on-premises Exchange mailboxes to the Exchange Online organization or move Exchange Online mailboxes to the Exchange organization. When you move mailboxes between the on-premises and Exchange Online organizations, you use migration batches to perform the remote mailbox move request. This approach allows you to move existing mailboxes instead of creating new user mailboxes and importing user information. This approach is different than migrating user mailboxes from an on-premises Exchange organization to Exchange Online as part of a complete Exchange migration to the cloud. The mailbox moves discussed in this article are part of administrative Exchange management in a longer-term coexistence relationship between on-premises Exchange and Exchange Online organizations.
ms.date: 2024-10-03T00:00:00.0000000Z
locale: en-us
document_id: 35bd8438-69fb-3da3-1c75-25576fc92fd4
document_version_independent_id: 4dd5a61d-ef30-f893-00c7-bdb9132e074d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/move-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/move-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/move-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: d4caf620-1b3b-7580-9288-96b952d1e600
---

# Move mailboxes between on-premises and Exchange Online organizations in hybrid deployments | Microsoft Learn

With an Exchange-based hybrid deployment, you can choose to either move on-premises Exchange mailboxes to the Exchange Online organization or move Exchange Online mailboxes to the Exchange organization. When you move mailboxes between the on-premises and Exchange Online organizations, you use migration batches to perform the remote mailbox move request. This approach allows you to move existing mailboxes instead of creating new user mailboxes and importing user information. This approach is different than migrating user mailboxes from an on-premises Exchange organization to Exchange Online as part of a complete Exchange migration to the cloud. The mailbox moves discussed in this article are part of administrative Exchange management in a longer-term coexistence relationship between on-premises Exchange and Exchange Online organizations.

For more information about migrating mailboxes from on-premises Exchange organizations to Exchange Online organizations, see [Ways to migrate multiple email accounts to Microsoft 365 or Office 365](../mailbox-migration/mailbox-migration).

Important

You must have configured a hybrid deployment between your on-premises and Exchange Online organizations to complete the "mailbox moves" procedures in this topic. For more information about hybrid deployments, see [Exchange Server Hybrid Deployments](../exchange-hybrid).

Important

Before you move Unified Messaging (UM)-enabled mailboxes to Exchange Online, you need to make sure that on-premises Skype for Business 2015, Skype for Business Online, and Exchange Online, all meet the requirements specified in [Hybrid deployment prerequisites](../hybrid-deployment-prerequisites). For information on how to map your on-premises UM mailbox policies to policies in Exchange Online, see [Set-UMMailboxPolicy](/en-us/powershell/module/exchangepowershell/set-ummailboxpolicy).

## What do you need to know before you begin?

- Estimated time to complete: 10 minutes to configure the migration batch, but total time to complete the migration depends on the number of mailboxes included in each migration batch.
- You need to be assigned permissions before you can perform this procedure (or procedures). For information on what permissions you need, see the "Mailbox Move and Migration Permissions" section in the [Recipients permissions](../permissions/feature-permissions/recipient-permissions) article.
- Hybrid deployment is configured between your on-premises and Exchange Online organizations.
- If you're running Exchange 2013, make sure the Mailbox Replication Proxy Service (MRSProxy) is enabled on your on-premises Exchange 2013 Client Access servers.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).
- The Microsoft 365 or Office 365 Exchange license must be assigned only after the migration is complete. You then have 30 days to assign the license.

Tip

Having problems? Ask for help in the Exchange Hybrid forum at [Exchange | Hybrid management](/en-us/answers/tags/377/office-exchange-hybrid-management).

## Enable MRSProxy Service

If the MRSProxy service isn't already enabled for your on-premises Exchange servers, you must enable it manually. For information on how to enable the MRSProxy service manually, see [Enable the MRS Proxy endpoint in Exchange Server](../architecture/mailbox-servers/mrs-proxy-endpoint#enable-the-mrs-proxy-endpoint-in-exchange-server).

## Create a migration endpoint

The next step after enabling the MRSProxy Service is "creating a migration endpoint." For information on how to create migration endpoints, see [Creation of migration endpoints](create-migration-endpoint#creation-of-migration-endpoints).

## Use the EAC to move mailboxes

You can use the **Remote move migration** option under the **Select the migration type** drop-down list on the **Select the migration type** page in the EAC portal to move mailboxes between on-premises organizations and Exchange Online organizations. For information on how to move mailboxes, see [Use the EAC to move mailboxes](move-mailboxes-using-eac#use-the-eac-to-move-mailboxes).

Note

You can also use PowerShell to move mailboxes. For more information, see [Use PowerShell to move mailboxes](move-mailboxes-using-powershell#use-powershell-to-move-mailboxes).

## Remove completed migration batches

After the "mailbox moves" process has been completed, we recommend removing the completed migration batches to minimize the likelihood of errors if the same users are moved again. For more information, see [Remove completed migration batches](remove-completed-migration-batches#remove-completed-migration-batches).