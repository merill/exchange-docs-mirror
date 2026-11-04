---
layout: Conceptual
title: Overview | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/admin-api-overview
Manager: bagol
ms.subservice: exo-address-books
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.topic: article
author: chrisda
ms.author: chrisda
ms.reviewer: vivepai
description: Learn about the Exchange Online Admin API as a replacement for specific Exchange Web Services (EWS) calls.
ms.collection:
- exchange-online
search.appverid: 
audience: Admin
f1.keywords: 
ms.custom: 
ms.service: exchange-online
ms.localizationpriority: medium
ms.date: 2026-09-25T00:00:00.0000000Z
locale: en-us
document_id: 06088e82-2387-fab0-66a8-acc6565b3349
document_version_independent_id: 299fb8f0-eb69-4558-6e49-3a59ff75c202
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/admin-api-overview.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/admin-api-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/admin-api-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: 1c7043d0-461f-1410-762c-8614c61048d1
---

# Overview | Microsoft Learn

Note

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

The Exchange Online Admin API is a REST-based administrative surface that enables a focused set of Exchange cmdlets and parameters as POST-only endpoints. The API enables access to a few key tasks that were previously available through Exchange Web Services (EWS), which is [planned for deprecation in October 2026](../clients-and-mobile-in-exchange-online/deprecation-of-ews-exchange-online). The API is built for these specific scenarios and *doesn't* replace the full Exchange administration surface in Exchange Online PowerShell.

The Exchange Online Admin API supports the following subset of Exchange management functions:

- **View organization Exchange configuration**: Retrieve organization settings such as accepted domains, MailTips configuration, and mailbox limits (for example, MaxSendSize).
- **View distribution group and dynamic distribution group membership**.
- **View and manage mailbox folder permissions**: Read and modify folder permissions for mailboxes (view, add, set, and remove permissions).
- **View and update Send on Behalf (delegation) for mailboxes**.

Organizations migrating away from EWS can use the Admin API to achieve comparable cmdlet-style administration over HTTP while integrating with modern automation and governance patterns.

The Exchange Online Admin API has the following features:

- **REST-based, cmdlet-style surface**: The Admin API exposes a focused set of Exchange administrative tasks as HTTP endpoints. It should feel familiar to Exchange admins who use PowerShell cmdlets, but you call it over HTTP.
- **POST-only operations**: Every operation uses the HTTP POST method. Each request specifies a cmdlet and the parameters that are supported for that cmdlet in the selected endpoint.
- **Scoped set of cmdlets and parameters**: The API doesn't surface every Exchange cmdlet or parameter. Each endpoint exposes only a subset of cmdlets, and each cmdlet supports a subset of parameters.
- **Focused scope**: The API covers a limited set of scenarios-organization settings, group membership, mailbox folder permissions, and mailbox delegation. It's not a full replacement for Exchange Online PowerShell. Instead, it's a complementary, REST-first surface for these specific tasks.
- **Paging and property selection**: Large result sets are returned in pages. On the client side, you can request only the properties you need to reduce payload size.
- **Routing hints**: For all operations, the API uses the **X-AnchorMailbox** header to route your request to the correct backend server. For more information, see [Get started with the Exchange Online API](admin-api-get-started).
- **Secure access**: Calls require OAuth tokens and appropriate Exchange RBAC roles. For more information, see [Authentication and authorization for the Exchange Online Admin API](admin-api-authentication).

## Admin API vs. Exchange Online PowerShell

The Admin API provides a targeted subset of Exchange management functionality as REST endpoints to cover scenarios affected by the EWS deprecation. [Exchange Online PowerShell](/en-us/powershell/exchange/exchange-online-powershell) continues to provide the *complete* Exchange management surface.

- **Admin API**: Use when you need a REST-first, cmdlet-equivalent surface for the previously described scenarios (organization config, group membership, folder permissions, and delegation) only.
- **Exchange Online PowerShell**: Use when you require the full breadth of Exchange cmdlets, advanced operations, or existing PowerShell scripts and runbooks.

The Exchange Online Admin API *isn't* a replacement for Exchange Online PowerShell. The API is a complementary, REST-based surface for a focused set of administrative tasks caused by the deprecated EWS scenarios. For all other Exchange management tasks, continue to use Exchange Online PowerShell.

## Exchange Online Admin API endpoints

Each Admin API endpoint provides one or more cmdlets to replace functionality previously available through EWS. The following table provides details about each endpoint and the corresponding EWS alternative.

| Endpoint | Description | EWS operation |
| --- | --- | --- |
| OrganizationConfig | Retrieve organization-level Exchange configuration, related to MailTips settings. | [GetServiceConfiguration](/en-us/exchange/client-developer/exchange-web-services/how-to-get-service-configuration-information-by-using-ews-in-exchange) |
| AcceptedDomain | View accepted domains and their configurations for the organization. | [GetServiceConfiguration](/en-us/exchange/client-developer/exchange-web-services/how-to-get-service-configuration-information-by-using-ews-in-exchange) |
| Mailbox | View mailbox properties. For example: display name, primary SMTP address, size limits, and delegate information (view and update). | [AddDelegate and RemoveDelegate](/en-us/exchange/client-developer/exchange-web-services/how-to-add-and-remove-delegates-by-using-ews-in-exchange) |
| MailboxFolderPermission | View and manage permissions on mailbox folders (add, set, and remove permissions). | [GetFolder, UpdateFolder, and CreateFolder](/en-us/exchange/client-developer/exchange-web-services/how-to-set-folder-permissions-for-another-user-by-using-ews-in-exchange) |
| DistributionGroupMember | Retrieve membership details for distribution groups. | [ExpandDL](/en-us/exchange/client-developer/web-service-reference/expanddl-operation) |
| DynamicDistributionGroupMember | Retrieve membership details for dynamic distribution groups. | [ExpandDL](/en-us/exchange/client-developer/web-service-reference/expanddl-operation) |