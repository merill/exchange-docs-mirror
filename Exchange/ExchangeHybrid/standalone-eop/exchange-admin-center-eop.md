---
layout: Conceptual
title: Exchange admin center in the Built-in security add-on for on-premises mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/standalone-eop/exchange-admin-center-eop
Manager: deniseb
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: chrisda
author: chrisda
ms.date: 2025-07-18T00:00:00.0000000Z
audience: ITPro
ms.topic: overview
ms.localizationpriority: medium
search.appverid:
- MET150
ms.assetid: 97921f0e-832f-40c7-b56d-414faede5191
ms.collection:
- M365-security-compliance
description: Admins in on-premises organizations that use the Built-in security add-on for on-premises mailboxes can learn about the web management interface in the add-on.
ms.service: exchange-online
locale: en-us
document_id: 5b00016d-7034-4b83-420c-4ac5be89cb72
document_version_independent_id: a507e7cd-cfa4-feb4-e721-f4f5c8afd3d4
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/standalone-eop/exchange-admin-center-eop.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standalone-eop/exchange-admin-center-eop
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/standalone-eop/exchange-admin-center-eop.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: c053dddc-f71f-ddbe-067b-771d25ffddc2
---

# Exchange admin center in the Built-in security add-on for on-premises mailboxes | Microsoft Learn

The Exchange admin center (EAC) is a web-based management console that's available in the Built-in security add-on for on-premises mailboxes. This version of the EAC is a subset of the EAC in cloud organizations with Exchange Online mailboxes.

Looking for the Exchange Online version of this article? See [Exchange admin center in Exchange Online](/en-us/exchange/exchange-admin-center).

## Open the EAC in the Built-in security add-on for on-premises mailboxes

In the Built-in security add-on for on-premises mailboxes, the EAC is available at https://admin.exchange.microsoft.com, which is the same URL in Exchange Online.

## Common user interface elements in the EAC in the Built-in security add-on for on-premises mailboxes

This section describes the user interface elements that are found in the EAC.

### Feature Pane

The left navigation pane is the first level of navigation for most tasks in the EAC. The feature pane is organized into feature areas.

- **Home**: Various cards show information about your organization.
- **Recipients**:
    - [Groups](manage-groups-in-eop)
    - [Mail contacts](/en-us/exchange/recipients-in-exchange-online/manage-mail-contacts)
    - [Mail users](/en-us/exchange/recipients-in-exchange-online/manage-mail-users).
- **Mail flow**:
    - [Run a message trace](/en-us/exchange/monitoring/trace-an-email-message/run-a-message-trace-and-view-results)
    - [Exchange mail flow rules (also known as transport rules)](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules)
    - [Accepted domains](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains)
    - [Connectors](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow)
    - [Alert policies](/en-us/exchange/monitoring/mail-flow-insights/alert-policy-and-its-configuration)
- **Roles**:
    - [Admin roles](/en-us/exchange/permissions-exo/permissions-exo)
    - [User roles](/en-us/exchange/permissions-exo/role-assignment-policies) (role assignment policies for Microsoft 365 Groups)
- **Reports**:
    - [Mail flow reports](/en-us/exchange/monitoring/mail-flow-reports/mail-flow-reports)
- **Insights**: [Mail flow insights](/en-us/exchange/monitoring/mail-flow-insights/mail-flow-insights)
- **Settings**
- **Troubleshoot**
- **Migration**: Status and location of features moved from the classic Exchange admin center to the new Exchange admin center or other portals.

### Tabs

The tabs are your second level of navigation. Each feature area contains various tabs, each representing a feature.

### List View

When you select a tab, in most cases you see a list view. The viewable limit with the EAC list view is approximately 10,000 objects. Paging is included so that you can page to results.

### Details flyout

When you select an object from the list view, information about that object is displayed in a details flyout that opens. The details flyout often includes management tasks.

## Supported Browsers

For the best experience using the EAC, we recommend that you always use the latest browsers, Office clients, and apps. We also recommend that you install software updates when they become available. For more information about the supported browsers and system requirements for the service, see [System requirements for Office](https://products.office.com/office-system-requirements).