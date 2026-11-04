---
layout: Conceptual
title: OrganizationConfig endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/admin-api-endpoints-organization-config
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
description: Learn about the OrganizationConfig endpoint in the Exchange Online Admin API.
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
document_id: e0610a0f-50d4-8cbf-7a4f-8fbeac6c1c23
document_version_independent_id: 0dc81045-49f9-37fc-9a6c-0ca7464cfd3e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/admin-api-endpoints-organization-config.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/admin-api-endpoints-organization-config
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/admin-api-endpoints-organization-config.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 33365987-8f9f-4e43-4109-2ef0abeed42f
---

# OrganizationConfig endpoint | Microsoft Learn

Note

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

The OrganizationConfig endpoint in the Exchange Online Admin API retrieves organization-wide settings related to MailTips and a few other associated service configurations.

The Exchange Online Admin API provides a REST-based way to execute specific PowerShell cmdlets, replacing legacy Exchange Web Services (EWS) scenarios. For more information, see [Overview of the Exchange Online Admin API](admin-api-overview).

## Endpoint URL

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/OrganizationConfig
```

Tip

Use the base URL for your environment as described in [Supported environments and base URLs](admin-api-get-started#supported-environments-and-base-urls).

## Request model

### Headers

```json
Authorization: Bearer <auth token>
Content-Type: application/json
X-AnchorMailbox: <routing hint>
```

For **X-AnchorMailbox** values, see [X-AnchorMailbox routing hint](admin-api-get-started#x-anchormailbox-routing-hint).

### Body

```json
{
  "CmdletInput": {
    "CmdletName": "Get-OrganizationConfig"
  }
}
```

### Pagination

Pagination isn't available. The **Get-OrganizationConfig** cmdlet returns a single organization configuration object.

## Supported cmdlets and parameters

The supported cmdlet for this endpoint is [Get-OrganizationConfig](/en-us/powershell/module/exchangepowershell/get-organizationconfig). Any other cmdlet in the body of this endpoint results in an error.

No parameters for the **Get-OrganizationConfig** cmdlet are available through through the REST endpoint.

## Response overview

Note

During Preview, the endpoint includes the full **Get-OrganizationConfig** cmdlet output in the API response. During the transition to public release, the response will be limited to the core properties listed in this section (properties needed for the EWS‑equivalent scenario). We recommend you use the properties listed in this section only. We'll document any changes to the available properties.

The **Get-OrganizationConfig** response is a single JSON object that represents the organization-level settings. The following properties are returned:

- **Name**: Exchange display name for the organization configuration object (there's only one in an organization).
- **Identity**: Canonical identity used by Exchange (often mirrors the **Name** value).
- **Id**: Service identifier for the organization configuration object.
- **Guid**: Stable GUID of the organization configuration object.
- **MailTipsAllTipsEnabled**: Indicates whether MailTips are enabled for all tips. The default value is `True`.
- **MailTipsExternalRecipientsTipsEnabled**: Indicates whether MailTips are shown for external recipients. The default value is `False`.
- **MailTipsLargeAudienceThreshold**: Threshold for large audiences that affects MailTips behavior. The default value is 25.

## Examples

- **Example 1**:

    This example returns the organization-wide configuration, including MailTips settings and core feature flags.

    ```json
    POST /adminapi/v2.0/<TenantID>/OrganizationConfig HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Get-OrganizationConfig"
      }
    }
    ```