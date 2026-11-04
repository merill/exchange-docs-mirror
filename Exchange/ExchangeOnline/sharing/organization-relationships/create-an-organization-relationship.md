---
layout: Conceptual
title: Create an organization relationship in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/sharing/organization-relationships/create-an-organization-relationship
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
description: Set up an organization relationship to share calendar information with an external business partner. Microsoft 365 and Office 365 admins can set up an organization relationship with another Microsoft 365 or Office 365 organization or with an Exchange on-premises organization.
ms.topic: how-to
author: alexcotsalas
ms.author: alexcotsalas
ms.assetid: 8b9a1782-f6be-46bc-bec9-49633be0dc1f
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
document_id: e64e56f9-fbf4-f072-637b-5fa8e827a399
document_version_independent_id: 32a37550-af95-a0ce-2941-ff9ce7ba9150
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/sharing/organization-relationships/create-an-organization-relationship.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sharing/organization-relationships/create-an-organization-relationship
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/sharing/organization-relationships/create-an-organization-relationship.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 6c8a2bdb-46a3-1910-1d85-d8f1a64c8b3b
---

# Create an organization relationship in Exchange Online | Microsoft Learn

Set up an organization relationship to share calendar information with an external business partner. Microsoft 365 and Office 365 admins can set up an organization relationship with another Microsoft 365 or Office 365 organization or with an Exchange on-premises organization.

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the [Permissions in Exchange Online](../../permissions-exo/permissions-exo) article.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- If you want to share calendars with an on-premises Exchange organization, the on-premises Exchange administrator has to set up an authentication relationship with the cloud (also known as "federation") and must meet minimum software requirements.
- For information about changes made to the **Get-FederationInformation** cmdlet to improve security and privacy, see [Important Update to the Get-FederationInformation Cmdlet in Exchange Online](https://techcommunity.microsoft.com/blog/exchange/important-update-to-the-get-federationinformation-cmdlet-in-exchange-online/4410095).

## Use the Exchange admin center to create an organization relationship

1. In the [EAC](https://admin.exchange.microsoft.com/#/), go to **Organization &gt; Sharing** &gt; **Organization sharing** tab. Or, use [**Organization sharing**](https://admin.exchange.microsoft.com/#/organizationsharing).
2. On the **Organization sharing** tab of the **Sharing** page, select **Add organization relationship**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif).
3. The **New organization sharing** wizard opens. On the **Fill in the basic info** page, configure the following settings:

    - **Relationship name**: Type a friendly name for the organization relationship.
    - **Domains to share with**: Type the domain for the external Microsoft 365, Office 365, or Exchange on-premises organization you want to let see your calendars. If you need to add more than one domain, you can [edit the organization sharing relationship](modify-an-organization-relationship) after you create it.

    When you're finished on the **Fill in the basic info** page, select **Next**.
4. On the **Sharing options** page, turn on the **Calendar free/busy information sharing** toggle and then configure the following settings:

    - Select one of the following values:
        - **Calendar free/busy information with time only** (default).
        - **Calendar free/busy information with time, subject, and location**.
    - **Share calendar free/busy information for**: Select one of the following values:
        - **Everyone in your organization** (default).
        - **A specified security group**. In the box that appears, select the security group in your organization.

    When you're finished on the **Sharing options** page, select **Next**.
5. On the **Review organization relationship** page, verify the settings. To make changes, select **Back**. When you're finished on the **Review organization relationship** page, select **Next**.
6. On the **Status** page, select **Done**.
7. Back on the **Organization sharing** tab on the **Sharing** page, select **Refresh** if the organization relationship isn't shown.

## Use Exchange Online PowerShell to create an organization relationship

This example creates an organization relationship between your organization and Contoso, Ltd. with the following conditions:

- An organization relationship is set up with contoso.com, northamerica.contoso.com, and europe.contoso.com.
- Free/busy access is enabled.
- Contoso.com and the subdomains get free/busy time, subject, and location information from your organization.

```PowerShell
New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails
```

If you're setting up an organization relationship with an on-premises Exchange organization, you might want to provide the connection settings. This example creates an organization relationship with Fourth Coffee and specifies the connection settings to use. The following conditions apply:

- The organization relationship is established with the domain fourthcoffee.com.
- The Exchange Web Services application URL is mail.fourthcoffee.com.
- The Autodiscover URL is `https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity`.
- Free/busy access is enabled.
- Fourth Coffee sees free/busy information with the time.

```PowerShell
New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly -TargetAutodiscoverEpr "https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity" -TargetApplicationUri "mail.fourthcoffee.com"
```

For detailed syntax and parameter information, see [New-OrganizationRelationship](/en-us/powershell/module/exchangepowershell/new-organizationrelationship).

## How do you know that you've successfully created an organization sharing relations?

The successful completion of the **New organization relationship** wizard indicates that the organization relationship was created.

You can also replace &lt;OrgRelationshipName&gt; with the name of the organization relationship and run the following command to verify the settings:

```PowerShell
Get-OrganizationRelationship -Identity "<OrgRelationshipName>" | Format-List
```

## Organization relationships with GCC High

[Microsoft 365 Government Community Cloud High (GCC High)](/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc-high-and-dod) organizations can create organization relationships with World Wide and [Microsoft 365 Government Community Cloud (GCC)](/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc) organizations.

Important

Organization relationships between the [Microsoft 365 Department of Defense (DoD)](/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc-high-and-dod) cloud and other clouds is not supported.

### Create cross-cloud organization relationships

Using Exchange Online PowerShell is the best way to create organization relationships between clouds.

This example creates an organization relationship between Contoso, Ltd. in the World Wide cloud and Fourth Coffee in the GCC High cloud with the following conditions:

- Contoso domains are contoso.com, northamerica.contoso.com, and europe.contoso.com.
- Fourth Coffee domains are fourthcoffee.com
- Free/busy access is enabled.
- Each tenant gets free/busy time, subject, and location information from the other tenant

In Fourth Coffee, run the following command:

```PowerShell
New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails -TargetApplicationUri "outlook.com" -TargetAutodiscoverEpr "https://autodiscover-s.outlook.com/autodiscover/autodiscover.svc/WSSecurity"
```

In Contoso, run the following command:

```PowerShell
New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails -TargetApplicationUri "office365.us" -TargetAutodiscoverEpr "https://autodiscover-s.office365.us/autodiscover/autodiscover.svc/WSSecurity"
```

The configuration parameters that you need to set are described in the following table:

| Parameter | OrgRel in WW/GCC for GCC High tenant | OrgRel in GCC High for WW/GCC tenant |
| --- | --- | --- |
| ***DomainNames*** | All the domains for the remote org. You need to collect and add these values manually. | All the domains for the remote org. You need to collect and add these values manually. |
| ***TargetApplicationUri*** | Office365.us | Outlook.com |
| ***TargetAutodiscoverEpr*** | `https://autodiscover-s.office365.us/autodiscover/autodiscover.svc/WSSecurity` | `https://autodiscover-s.outlook.com/autodiscover/autodiscover.svc/WSSecurity` |