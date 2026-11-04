---
layout: Conceptual
title: Migrate data from Google Workspace to Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/consolidated-gws-migration
Manager: tonymathew
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Migrating all Google Workspace workloads to Microsft 365, Mail and Drive migration.
ms.author: tonymathew
author: tonymathew
ms.topic: upgrade-and-migration-article
ms.date: 2024-10-31T00:00:00.0000000Z
ms.service: exchange-online
ms.localizationpriority: medium
ms.reviewer: tonymathew
search.appverid: MET150
f1.keywords: 
audience: ITAdmin
locale: en-us
document_id: 1f5b6e0f-8dc6-cb2a-98cb-8462580c90ac
document_version_independent_id: 1d98b3a0-2dc3-dca3-53b4-e0f74d2770dc
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/consolidated-gws-migration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/consolidated-gws-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/consolidated-gws-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 489d2399-32c7-bc4c-4535-fa7969b8a521
---

# Migrate data from Google Workspace to Microsoft 365 | Microsoft Learn

## Introduction

This article provides comprehensive guidance for tenant administrators to the new Microsoft toolset for migrating Google Workspace (**GWS**) workloads to Microsoft 365. In the new experience, the tenant admin (**TA**) gets a one-stop shop for migration from GWS in Microsoft 365 Admin Center (**MAC**). Additionally, the tenant admin also has access to a new mail migration feature called Simplified Gmail migration (**SGM**) aimed at small- and medium-sized businesses (less than 1000 seats) to complete the mail migration from GWS to Microsoft 365 in one go without the use of batching mechanisms.

Note

In October 2024, the experience for consolidated migration from Google is being launched for Mail and Drive. New workloads from Groups, Teams, and other areas will be added in the near future.

In this new experience, the tenant admin is guided through the following high-level steps:

1. The TA navigates to the migration page in MAC: [Migrate your business productivity workloads to Microsoft 365](https://admin.microsoft.com/adminportal/home#/featureexplorer/collections/Migrations).
2. The TA selects the Google migration option at the top of the page and opens the Consolidated Google migration dashboard: [Migrate from Google Workspace to Microsoft 365](https://admin.microsoft.com/adminportal/home#/featureexplorer/migration/GoogleMigration/).
3. For a First Run Experience (**FRE**), the TA adds the source domain to migrate.
4. After domains are added in FRE or when the TA returns later for a returning user experince (**RUE**), the TA sees tiles specific to workloads. The TA sees a **Mail** tile listing metadata about mail users and mailbox details from the Google source domain. Similarly, TA also sees a **Drive** tile listing metadata about the source Google drive.
5. The TA can choose to migrate the workload of their choice.
    1. When the tenant admin chooses to migrate data from Google mail to Microsoft 365, the solution looks up the numbers of users in the domain and guides the TA to the appropriate experience - [Migrate mail from Google Workspace to Microsoft 365](https://admin.microsoft.com/adminportal/home#/featureexplorer/migration/GsuiteMailboxMigration).
        1. If the user count in the source domain is greater than 1000 users, the TA is guided to the large tenant Gmail Migration experience in MAC. The large tenant migration experience focuses on making sure that both the source GWS Mail and target Microsoft 365 Exchange are both usable in the duration of migration. See details here: [Large tenant migration from Google Workspace Mail to Microsoft 365 Exchange Online](/en-us/microsoft-365/admin/moveto-microsoft-365/migrate-email).
        2. If the user count in the source domain is less than on equal to 1000 users, the TA is guided to the SGM experience. See details here: [Simplified Gmail migration for small and medium businesses](custom-migration-small-business-from-gmail).
    2. When the tenant admin choeses to migrate from Google Drive to Microsoft 365, they're directed to the Drive migration experience: [Migrate from Google Workspace Drive to Microsoft 365 OneDrive and Sharepoint](https://admin.microsoft.com/adminportal/home#/featureexplorer/migration/GoogleMigration/GDrive).
        1. See the details of migrating from Google Drive to Microsoft 365 OneDrive and Sharepoint here: [Migrate Google files to Microsoft 365 for business with Migration Manager](/en-us/microsoft-365/admin/moveto-microsoft-365/migrate-files-migration-manager).

Note

In October 2024, both Mail and Drive mgirations from GWS to Microsoft 365 require the installation of workload-specific apps in the Google Admin Console of the source Google tenant. Make sure you have Administrator privileges to install the apps in Google.