---
layout: Conceptual
title: Manage accepted domains in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Admins can learn how to view and modify accepted domains in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 0fc0ecc0-e133-48fa-9d72-cb4793a73960
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-19T00:00:00.0000000Z
locale: en-us
document_id: b1640bb5-ca97-15ff-28e5-5efe4e73193f
document_version_independent_id: e957bd3e-5d4c-333c-45ff-6fd694f34670
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 151ade08-67ee-ef6e-6d93-d2690751b978
---

# Manage accepted domains in Exchange Online | Microsoft Learn

When you add your domain to Microsoft 365 or Office 365, it's called an accepted domain. This functionality of an accepted domain means that users in this domain can send and receive mail. For more information on how to add your domain to Microsoft 365 or Office 365 using the Microsoft 365 admin center, see [Add a domain to Microsoft 365 or Office 365](/en-us/microsoft-365/admin/setup/add-domain).

After you add your domain using the Microsoft 365 admin center, you can use the Exchange admin center (EAC) to view your accepted domains and configure the domain type.

There are two types of accepted domains in Exchange Online:

- **Authoritative**: Email is delivered to email addresses that are listed for recipients in Microsoft 365 or Office 365 for this domain. Emails for unknown recipients are rejected.

    - If you just added your domain to Microsoft 365 or Office 365 and you select this option, it's critical that you add your recipients to Microsoft 365 or Office 365 before setting up mail to flow through the service.
    - Typically, you use this option when all the email recipients in your domain are using Microsoft 365 or Office 365. You can also use it if some recipients exist on your own email servers. However, if recipients exist on your own email servers, you must add your recipients to this Microsoft 365 or Office 365 domain in order to make sure that mail is delivered as expected. For more information about how to manage your recipients, see [Manage mail users in Exchange Online](../../recipients-in-exchange-online/manage-mail-users).
    - Setting this option enables Directory-Based Edge Blocking (DBEB), which rejects messages for invalid recipients at the service network perimeter. For more information about configuring DBEB during a migration, see [Use Directory-Based Edge Blocking to reject messages sent to invalid recipients](../use-directory-based-edge-blocking).
- **Internal relay (also known as non-authoritative)**: Recipients for this domain can be in Microsoft 365 or Office 365 or your own email servers. Email is delivered to known recipients in Office 365 or is relayed to your own email server if the recipients aren't known to Microsoft 365 or Office 365.

    - **You should not select this option if all of the recipients for this domain are in Microsoft 365 or Office 365.**
    - If you select this option, you must create a connector for mail flow from Microsoft 365 or Office 365 to your on-premises email server; otherwise recipients on the domain who are not hosted in Microsoft 365 or Office 365 won't be able to receive mail on your own email servers. For more information about setting up connectors, see [Set up connectors to route mail between Microsoft 365 or Office 365 and your own email servers](../use-connectors-to-configure-mail-flow/set-up-connectors-to-route-mail).
    - This option is required if you enable the subdomain routing option on a domain in order to let email pass through the service and be delivered to any subdomains of your accepted domains. For more information, see [Enable mail flow for subdomains in Exchange Online](enable-mail-flow-for-subdomains).

## What do you need to know before you begin?

- Estimated time to complete: 10 minutes.
- You need permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Domains" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## View accepted domains

### Use Exchange admin center (EAC) to view accepted domains

1. Navigate to **Mail flow** &gt; **Accepted domains**. The **Accepted domains** screen appears.
2. Click the **Name**, **Accepted Domain**, or **Domain Type** column heading to sort alphabetically in ascending or descending order. By default, accepted domains are sorted alphabetically by name in ascending order.

![The screen on which the column heading values are displayed in ascending order.](../../exchangeonline/media/accepted-domains-ascending-detail.png)

## Configure the domain type

After you add a domain to your Exchange Online organization in the Microsoft 365 admin center, you can configure the domain type.

### Use the EAC to set the domain type

1. Navigate to **Mail flow** &gt; **Accepted domains**. The **Accepted domains** screen appears.
2. Select an accepted domain and click it. The accepted domain's details screen appears.
3. Under the **This accepted domain is** section, select the domain type. The possible values are **Authoritative** and **Internal relay**.

    - If you select **Authoritative**, you must confirm that you want to enable Directory-Based Edge Blocking.
    - If you select **Internal Relay**, you can enable the match-subdomains to enable mail flow to all subdomains. For more information, see [Enable mail flow for subdomains in Exchange Online](enable-mail-flow-for-subdomains).
4. Click **Save**.

### Use the EAC to change the domain type

This section describes the procedure to change an accepted domain's type from **Internal relay** to **Authoritative**.

1. Navigate to **Mail flow** &gt; **Accepted domains**. The **Accepted domains** screen appears.
2. Select the accepted domain that has **Internal relay** as its type. The accepted domain's details screen appears.
3. Under the **This accepted domain is** section, select **Authoritative**.
4. Select **Save**.

    Important

    The **Save** button is displayed for the admins only when they have the specific permissions required to change the type for an accepted (or even remote) domain. Hence, it's important for admins to ensure that they have the permissions needed to change the accepted domain's type, prior to implementing the steps in this section. For more information on the permissions required to change the domain type, contact your administrator.

The resultant screen displays the **Accepted domain updated successfully** notification message. This message notifies that the Accepted domain's type has been changed from **Internal relay** to **Authoritative**.

### Use Exchange Online PowerShell to view accepted domains

To view summary information about all accepted domains, run the following command:

```powershell
Get-AcceptedDomain
```

To view details about a specific accepted domain, use the following syntax.

```powershell
Get-AcceptedDomain -Identity <Name> | Format-List
```

This example shows details about the accepted domain named contoso.com.

```powershell
Get-AcceptedDomain -Identity contoso.com | Format-List
```

### Use Exchange Online PowerShell to change the domain type

To configure the domain type, use the following syntax:

```powershell
Set-AcceptedDomain -Identity <Name> -DomainType <Authoritative | InternalRelay>
```

This example configures the accepted domain named contoso.com as an internal relay domain.

```powershell
Set-AcceptedDomain -Identity contoso.com -DomainType InternalRelay
```

For detailed syntax and parameter information, see [Set-AcceptedDomain](/en-us/powershell/module/exchangepowershell/set-accepteddomain).