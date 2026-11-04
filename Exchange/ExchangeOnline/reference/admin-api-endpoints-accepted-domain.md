---
layout: Conceptual
title: AcceptedDomain endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/reference/admin-api-endpoints-accepted-domain
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
description: Learn about the AcceptedDomain endpoint in the Exchange Online Admin API.
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
document_id: 84c76e8b-f9b9-2f6e-4dd6-bacccaf0f93b
document_version_independent_id: c9d6506c-ec7a-f500-03b8-124981dcfee0
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/reference/admin-api-endpoints-accepted-domain.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: reference/admin-api-endpoints-accepted-domain
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/reference/admin-api-endpoints-accepted-domain.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: d19d595d-a695-10f3-f9e3-d2a804245c32
---

# AcceptedDomain endpoint | Microsoft Learn

Note

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

The AcceptedDomain endpoint in the Exchange Online Admin API retrieves the list of accepted domains configured for the organization. This endpoint returns a collection of domain objects with key property values for each domain.

Typical use cases include:

- List accepted domains for mail flow configuration.
- Review property values for each configured domain.

The Exchange Online Admin API provides a REST-based way to execute specific PowerShell cmdlets, replacing legacy Exchange Web Services (EWS) scenarios. For more information, see [Overview of the Exchange Online Admin API](admin-api-overview).

## Endpoint URL

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/AcceptedDomain
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
    "CmdletName": "Get-AcceptedDomain",
    "Parameters": {
      "Identity": "<domain name>",           // optional
      "ResultSize": <Integer | "Unlimited">  // optional (pagination)
    }
  }
}
```

### Pagination

The *ResultSize* parameter controls pagination. By default, up to 1,000 results are returned.

If more results are available, the response includes an `@odata.nextLink` property with a continuation URL. To fetch the next page, issue a new POST request to the URL in `@odata.nextLink` with the same body.

### Property selection

This endpoint supports the `$select` query parameter to return only specific properties in the response. For example:

```json
POST https://outlook.office365.com/adminapi/v2.0/<TenantID>/AcceptedDomain?$select=DomainName,Default
```

## Supported cmdlets and parameters

The supported cmdlet for this endpoint is [Get-AcceptedDomain](/en-us/powershell/module/exchangepowershell/get-accepteddomain). Any other cmdlet in the body of this endpoint results in an error.

Only the parameters described in the following table are available through the REST endpoint:

| Parameter | Required | Type | Description |
| --- | --- | --- | --- |
| Identity | Optional | String | Specifies the accepted domain to retrieve information about. Valid values are the domain name (for example, contoso.com) or GUID. If omitted and subject to *ResultSize*, the cmdlet returns all accepted domains. |
| ResultSize | Optional | Integer or string | Limits the number of results returned. Valid values are an integer (for example, 10) or the value `"Unlimited"`. |

## Response overview

Note

During Preview, the endpoint includes the full **Get-AcceptedDomain** cmdlet output in the API response. During the transition to public release, the response will be limited to the core properties listed in this section (properties needed for the EWS‑equivalent scenario). We recommend you use the properties listed in this section only. We'll document any changes to the available properties.

The response is a JSON array of accepted domain objects. Each object contains domain configuration and metadata information. The returned properties include:

- **DomainName**: The fully qualified domain name (FQDN). For example, contoso.com.
- **AdminDisplayName**: Optional label for the domain.
- **DomainType**: Domain mode for mail routing. For example, `Authoritative`, `InternalRelay`, or` ExternalRelay`.
- **Name**: Unique Exchange display name for the accepted domain object.
- **Id**: Service identifier for the object.
- **Identity**: Canonical identity used by Exchange. Often mirrors the **Name** value. Used in management operations.
- **Guid**: Globally unique identifier of the accepted domain object.

## Examples

- **Example 1: View all accepted domains**:

    This example retrieves a maximum of 1,000 accepted domains configured for the organization because we aren't using the *ResultSize* parameter.

    ```json
    POST /adminapi/v2.0/<TenantID>/AcceptedDomain HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Get-AcceptedDomain"
      }
    }
    ```
- **Example 2: Limit results using ResultSize**:

    This example limits the results to one accepted domain by setting the *ResultSize* parameter to the value 1.

    ```json
    POST /adminapi/v2.0/<TenantID>/AcceptedDomain HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Get-AcceptedDomain",
        "Parameters": {
          "ResultSize": 1
        }
      }
    }
    ```
- **Example 3: Get results for a specific accepted domain**:

    This example retrieves details for the specified contoso.com accepted domain.

    ```json
    POST /adminapi/v2.0/<TenantID>/AcceptedDomain HTTP/1.1
    Host: outlook.office365.com
    Authorization: Bearer <auth token>
    Content-Type: application/json
    X-AnchorMailbox: <Routing Hint>
    
    {
      "CmdletInput": {
        "CmdletName": "Get-AcceptedDomain",
        "Parameters": {
          "Identity": "contoso.com"
        }
      }
    }
    ```