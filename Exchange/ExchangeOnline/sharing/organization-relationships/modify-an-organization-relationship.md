---
layout: Conceptual
title: Modify an organization relationship in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/organization-relationships/modify-an-organization-relationship
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
ms.custom:
- has-azure-ad-ps-ref
description: Admins can learn how to change the settings of an organization relationship, such as changing the name, temporarily disabling calendar sharing, changing the access level, or changing which security group members will share calendars.
ms.topic: how-to
author: alexcotsalas
ms.author: alexcotsalas
ms.assetid: 6875cd79-41d4-422c-80a7-549ded9a1ea7
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
document_id: 87e36b32-bb72-3c56-bfba-59748293fc46
document_version_independent_id: 7fbd3826-1bae-c7b4-9065-41a78843a99c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/organization-relationships/modify-an-organization-relationship.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/organization-relationships/modify-an-organization-relationship
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/organization-relationships/modify-an-organization-relationship.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: f831ef86-9715-93ca-b940-ee46cddc6671
---

# Modify an organization relationship in Exchange Online | Microsoft Learn

An organization relationship lets users in your Microsoft 365 or Office 365 organization share calendar free/busy information with other Microsoft 365, Office 365, or on-premises Exchange organizations. You might want to change the settings of an organization relationship, such as changing the name, temporarily disabling calendar sharing, changing the access level, or changing which security group members share calendars.

To learn more about organization relationships, see [Organization relationships in Exchange Online](organization-relationships).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the [Permissions in Exchange Online](../../permissions-exo/permissions-exo) article.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- If you want to share calendars with an on-premises Exchange organization, the on-premises Exchange administrator has to set up an authentication relationship with the cloud (also known as "federation") and must meet minimum software requirements.

## Use the Exchange admin center to add a domain to an organization relationship

1. In the [EAC](https://admin.exchange.microsoft.com/#/), go to **Organization &gt; Sharing** &gt; **Organization sharing** tab. Or, use [**Organization sharing**](https://admin.exchange.microsoft.com/#/organizationsharing).
2. On the **Organization sharing** tab of the **Sharing** page, select the organization relationship by clicking the name (don't select the round check box that appears next to the name).
3. In the details flyout that opens, verify that the **General** tab is selected, and then select **Manage general settings**.
4. In the **Manage general settings** flyout that opens, find the **Domain name** section, add the domain name in the box and then select **Add**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif). To remove an existing domain entry, select **Delete**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.gif) next to the domain.
5. When you're finished on the **Manage general settings** flyout, select **Save**.

## Use the Exchange admin center to disable free/busy sharing for the organization relationship

1. In the [EAC](https://admin.exchange.microsoft.com/#/), go to **Organization &gt; Sharing** &gt; **Organization sharing** tab. Or, use [**Organization sharing**](https://admin.exchange.microsoft.com/#/organizationsharing).
2. On the **Organization sharing** tab of the **Sharing** page, select the organization relationship by clicking the name (don't select the round check box that appears next to the name).
3. In the details flyout that opens, select the **Sharing** tab, and then select **Manage sharing settings**.
4. In the **Manage sharing settings** flyout that opens, toggle **Enable calendar free/busy information sharing** to **Off**.
5. When you're finished on the **Manage sharing settings** flyout, select **Save**.

## Use the Exchange admin center to change the free/busy access level for the organization relationship

1. In the [EAC](https://admin.exchange.microsoft.com/#/), go to **Organization &gt; Sharing** &gt; **Organization sharing** tab. Or, use [**Organization sharing**](https://admin.exchange.microsoft.com/#/organizationsharing).
2. On the **Organization sharing** tab of the **Sharing** page, select the organization relationship by clicking the name (don't select the round check box that appears next to the name).
3. In the details flyout that opens, select the **Sharing** tab, and then select **Manage sharing settings**.
4. In the **Manage sharing settings** flyout that opens, verify that the **Enable calendar free/busy information sharing** toggle is **On**, and then select one of the following values:

    - **Calendar free/busy information with time only** (default).
    - **Calendar free/busy information with time, subject, and location**.
5. When you're finished on the **Manage sharing settings** flyout, select **Save**.

## Use Exchange Online PowerShell to modify the organization relationship

- This example adds the domain name service.contoso.com to the organization relationship Contoso.

    ```PowerShell
    $domains = (Get-OrganizationRelationship Contoso).DomainNames
    
    $domains += 'service.contoso.com'
    
    Set-OrganizationRelationship -Identity Contoso -DomainNames $domains
    ```
- This example disables the organization relationship Contoso.

    ```PowerShell
    Set-OrganizationRelationship -Identity Contoso -Enabled $false
    ```
- This example enables calendar availability information access for the organization relationship WoodgroveBank and sets the access level to `AvailabilityOnly` (calendar free/busy information with time only).

    ```PowerShell
    Set-OrganizationRelationship -Identity Contoso -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly
    ```

For detailed syntax and parameter information, see [Get-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/get-organizationrelationship) and [Set-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/set-organizationrelationship).

## How do you know that you've successfully modified an organization relationship?

To verify that you've successfully updated the organization relationship, replace &lt;OrgRelationshipName&gt; with the name of the organization relationship and run the following command to verify the settings:

```PowerShell
Get-OrganizationRelationship -Identity "<OrgRelationshipName>" | Format-List
```