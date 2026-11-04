---
layout: Conceptual
title: Creation of migration endpoints using different methods | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/create-migration-endpoint
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
ms.topic: upgrade-and-migration-article
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
description: A migration endpoint which is a vital component in onboarding and offboarding mailboxes from Microsoft 365 or Office 465 can be created using Hybrid Configuration wizard (HCW), EAC, and PowerShell.
ms.date: 2024-10-03T00:00:00.0000000Z
locale: en-us
document_id: 6cf95ac5-3d6f-b4d7-a9f3-8a867e3c765b
document_version_independent_id: 81f9ef83-ae6e-f201-a143-c30c40862db0
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/create-migration-endpoint.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/create-migration-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/create-migration-endpoint.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: e44a930a-ae7c-0bf8-cc4f-09a6f097ce42
---

# Creation of migration endpoints using different methods | Microsoft Learn

A migration endpoint contains the connection settings for an on-premises Exchange server that is running the MRS proxy service. These connection settings are required to perform remote move migrations to and from Exchange Online. Hence, migration endpoints can be the facilitators of the "move mailboxes" process.

A migration endpoint must be created prior to on-boarding and off-boarding remote move migrations in an Exchange hybrid deployment.

Important

Prior to even creating migration endpoints, you must ensure that the target server is available. Else, the remote move migrations fail despite prevalence of migration endpoints. You can verify the availability of the target server using the `Test-MigrationServerAvailability` cmdlet. For more information on this cmdlet and how it helps in verifying the availability of the target server, see [Test-MigrationServerAvailability](/en-us/powershell/module/exchangepowershell/test-migrationserveravailability?view=exchange-psv&amp;preserve-view=true).

A migration endpoint can be created through the following methods:

- EAC
- PowerShell

Important

The Hybrid Configuration wizard (HCW) is the preferred method to create migration endpoints because it helps in seamlessly creating migration endpoint. For more information on HCW, see [Hybrid Configuration wizard](/en-us/exchange/hybrid-configuration-wizard).

## EAC

Important

HCW is the preferred method to create migration endpoint. The EAC method of creating endpoint is required only to create further migration endpoints, in addition to the one created using HCW.

Creation of migration endpoints through EAC portal involves:

- Creation of migration endpoint using a migration batch
- Creation of an endpoint directly

### Creation of migration endpoint using a migration batch

The process of creating a migration endpoint through a migration batch includes:

- Create a migration endpoint to move Exchange Online mailboxes to on-premises organizations
- Create a migration endpoint to move on-premises mailboxes to Exchange Online organization

#### Create a migration endpoint to move Exchange Online mailboxes to on-premises organizations

1. Sign in to the Exchange Online EAC (https://admin.exchange.microsoft.com) and select **Migration** from the left navigation menu.
2. Select **Add a migration batch**.
3. On the **Add migration batch**page:
    1. In the **Give migration endpoint a unique name** text box, enter a name for the migration batch.
    2. From the **Select the mailbox migration path** drop-down list, select **Migrate from Exchange Online**.
    3. Select **Next**.
4. Select **Create a new migration endpoint**, and then select **Next**.
5. Enter the values for the following mandatory fields:
    1. **Migration endpoint name**: The name of choice for the endpoint you are going to create.
    2. **Account with privileges (domain\user name)**: The username of the user with extra privileges for whom you want to facilitate mailbox moves, in the format `domain\user name`.
    3. **Password of account with privileges**: The password for the account of the user with extra privileges.
    4. **Remote MRS Proxy server**: The on-premises Exchange server on which the MRSProxy service has been deployed.
6. Select **Next**.
7. Retain the default values of **20** and **10** for the **Maximum concurrent migrations** and **Maximum concurrent incremental syncs** text boxes, respectively.
8. Select **Next**.
9. Close the page that displays a notification message regarding creation of the migration endpoint.
10. On the **Migration batches** page, select **Endpoints** on the top-right side of the page, and verify that the name of the endpoint that you created is displayed.

#### Create a migration endpoint to move on-premises mailboxes to Exchange Online organization

1. Sign in to the on-premises EAC (https://admin.exchange.microsoft.com) and select **Migration** from the left navigation menu.
2. Select **Add a migration batch**.
3. On the **Add migration batch**page:
    1. In the **Give migration endpoint a unique name** text box, enter a name for the migration endpoint that you want to create.
    2. From the **Select the mailbox migration path** drop-down list, select **Migrate to Exchange Online**.
    3. Select **Next**.
4. From the **Select the migration type** drop-down list, select **Remote move migration**, and then select **Next**.
5. On the **Prerequisites for remote migration** page, select **Next**.
6. Select **Create a new migration endpoint**, and then select **Next**.
7. Enter the values for all the mandatory fields, and then select **Next**.
8. Retain the default values of **20** and **10** for the **Maximum concurrent migrations** and **Maximum concurrent incremental syncs** text boxes, respectively.
9. Select **Next**.
10. Close the page displaying a notification message for the creation of the migration endpoint.
11. On the **Migration batches** page, select **Endpoints** on the top-right side of the page and then verify whether your migration endpoint is displayed.

### Creation of an endpoint directly

Direct creation of a migration endpoint denotes "not using the 'batch migration creation' process as part of creating a migration endpoint."

To directly create a migration endpoint using EAC, and without using the "migration batch creation" process, perform the following steps:

1. Sign in to the EAC (https://admin.exchange.microsoft.com).
2. Select **Migration** from the left navigation menu.
3. Select **Endpoints** on the top-right side, and then select **+ Add**.
4. On the **Add Endpoint**page:
    1. From the **Select the migration type** drop-down list, select **Exchange Remote**.
    2. Enter the values for the mandatory fields, and then select **Create**.
5. Close the page that displays the message **Created successfully**.
6. On the **Migration batches** page, select **Endpoints** on the top-right side of the page, and verify that your migration endpoint is displayed.

## PowerShell

For information on how to create a migration endpoint using PowerShell, see [New-MigrationEndpoint](/en-us/powershell/module/exchangepowershell/new-migrationendpoint?view=exchange-ps&amp;preserve-view=true).

To implement the next step of moving mailboxes, see [Methods to move mailboxes between on-premises and Exchange Online organizations](methods-to-move-mailboxes#methods-to-move-mailboxes-between-on-premises-and-exchange-online-organizations).