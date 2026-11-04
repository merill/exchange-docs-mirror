---
layout: Conceptual
title: Remove an organization relationship in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/organization-relationships/remove-an-organization-relationship
Manager: dansimp
ms.subservice: outlook-services
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: An organization relationship lets users in your Microsoft 365 or Office 365 organization share calendar free/busy information with other Microsoft 365 or Office 365 or on-premises Exchange organizations. You can remove an organization relationship to disable calendar sharing with the other organization.
ms.topic: how-to
author: alexcotsalas
ms.author: alexcotsalas
ms.assetid: 3de9e885-73f5-4743-9b55-38ef59a387f2
ms.reviewer: AkshayaPrakash-PM
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-02-28T00:00:00.0000000Z
locale: en-us
document_id: 34c739ad-0fba-771e-b82d-9ff11df12c20
document_version_independent_id: f698db73-9a7e-2f68-574a-076a62051d81
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/organization-relationships/remove-an-organization-relationship.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/organization-relationships/remove-an-organization-relationship
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/organization-relationships/remove-an-organization-relationship.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 43ce7bcf-ed5d-e2b1-7025-d4d1c2c416e1
---

# Remove an organization relationship in Exchange Online | Microsoft Learn

An organization relationship lets users in your Microsoft 365 or Office 365 organization share calendar free/busy information with other Microsoft 365, Office 365, or on-premises Exchange organizations. You can remove an organization relationship to disable calendar sharing with the other organization.

To learn more about organization relationships, see [Organization relationships in Exchange Online](organization-relationships).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the [Permissions in Exchange Online](../../permissions-exo/permissions-exo) topic.

## Use the Exchange admin center to remove an organization relationship

1. From the Microsoft 365 admin center click **Exchange**.
2. Click **Organization &gt; Sharing** &gt; **Organization sharing** tab. Or, use [**Organization sharing**](https://admin.exchange.microsoft.com/#/organizationsharing).
3. In the **Organization Sharing**, select an organization relationship, and then click **Delete**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.gif).
4. In the warning that appears, click **Confirm**.

## Use Exchange Online PowerShell to remove an organization relationship

This example removes the organization relationship Contoso.

```PowerShell
Remove-OrganizationRelationship -Identity "Contoso"
```

For detailed syntax and parameter information, see [Remove-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/remove-organizationrelationship).

## How do you know this worked?

To verify that you have successfully removed the organization relationship, do one of the following:

- In the Exchange admin center, go to **Organization** &gt; **Sharing** and verify that the organization relationship isn't displayed in the list view under **Organization sharing**.
- Run the following command to verify the organization relationship information is removed.

    ```PowerShell
    Get-OrganizationRelationship | Format-List
    ```