---
layout: Conceptual
title: Specify the administrators and users who can install and manage add-ins for Outlook in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/specify-who-can-install-and-manage-add-ins
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: You can specify which administrators in your organization have permissions to install and manage add-ins for Outlook. You can also specify which users in your organization have permission to install and manage add-ins for their own use.
ms.topic: install-set-up-deploy
author: AshaIyengar21
ms.author: serdars
ms.assetid: 7ee4302d-b8bb-40a0-9810-10d3a0271bcb
ms.reviewer: 
ms.collection: exchange-online
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2024-06-21T00:00:00.0000000Z
locale: en-us
document_id: f86c9e05-c68b-8f00-3a94-c902d3352590
document_version_independent_id: e299bde7-ee34-96eb-b7f3-2ae75db017d3
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/add-ins-for-outlook/specify-who-can-install-and-manage-add-ins.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/add-ins-for-outlook/specify-who-can-install-and-manage-add-ins
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/add-ins-for-outlook/specify-who-can-install-and-manage-add-ins.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: f7608526-ddbf-40b5-6615-50c1b551ee02
---

# Specify the administrators and users who can install and manage add-ins for Outlook in Exchange Online | Microsoft Learn

You can specify which administrators in your organization have permissions to install and manage add-ins for Outlook. You can also specify which users in your organization have permissions to install and manage add-ins for their own use.

This configuration is done by assigning or removing management roles specific to add-ins. There are five built-in roles you can use.

## Administrative roles

- **Org Marketplace Apps**: Enables an administrator to install and manage add-ins that are available from the Office Store for their organization.
- **Org Custom Apps**: Enables an administrator to install and manage custom add-ins for their organization.

By default, all administrators who are in the **Organization Management** role group have both these administrative roles enabled.

Note

For a list of admins who can install apps from the Integrated Apps page, see [Who can access Integrated Apps](/en-us/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps#who-can-access-integrated-apps).

## User roles

- **My Marketplace Apps**: Enables a user to install and manage Office Store add-ins for their own use.
- **My Custom Apps**: Enables a user to install and manage custom add-ins for their own use.
- **My ReadWriteMailbox Apps**: Enables a user to install and manage add-ins that request the `ReadWriteMailbox` permission level in their manifest.

By default, all end users have all of these user roles enabled.

Note

If you're testing Outlook add-ins and none are showing up, then as a first troubleshooting step, use the `Get-OrganizationConfig` PowerShell cmdlet to query the **AppsForOfficeEnabled** parameter. If the query returns a value of **False**, set this parameter to **True** using the `Set-OrganizationConfig` cmdlet; then the add-ins should appear as expected.

We don't recommend that the **AppsForOfficeEnabled** parameter be set to **False**. A value of **False** overrides all the Administrative and User role settings and prevent any new apps from being activated by any user in the organization.

For information about add-ins, see [Add-ins for Outlook](add-ins-for-outlook).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can run this cmdlet. Although all parameters for this cmdlet are listed in this article, you may not have access to some parameters if they're not included in the permissions assigned to you. For information on the permissions you need, see the "Role assignments" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- Access to the Office Store isn't supported for mailboxes or organizations in specific regions. If you don't see **Add from the Office Store** as an option in the Exchange admin center (EAC) under **Organization** &gt; **Add-ins** &gt; **New**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif), you may be able to install an add-in for Outlook from a URL or file location. For more information, contact your service provider.

    Note

    URLs with redirections aren't supported in Exchange Server 2016, Exchange Server 2019, and Exchange Online. Use a direct URL to the manifest.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Assign administrators the permissions required to install and manage add-ins for your organization

### Use the EAC to assign permissions to administrators

You can use the EAC to assign administrators the permissions required to install and manage add-ins that are available from the Office Store for your organization.

1. Sign in to [EAC](https://admin.exchange.microsoft.com) with an account that's assigned the **Role Management** role. This role is assigned to the **Organization Management** role group by default.
2. Go to **Roles** &gt; **Admin Roles**.
3. Select an existing group or create a new one.
4. If you're modifying an existing role, go to the existing role's details page and select the **Permissions** tab, add the permissions required to install and manage add-ins, and then select **Save**. If you are creating a new group, follow the wizard.

For detailed information about how to do this, see [Manage role groups in Exchange Online](../../permissions-exo/role-groups).

## Assign users the permissions required to install and manage add-ins for their own use

### Use the EAC to assign permissions to users

You can use the EAC to assign users the permissions required to view and modify custom add-ins for their own use.

1. Sign in to [EAC](https://admin.exchange.microsoft.com) with an account that's assigned the **Role Management** role. This role is assigned to the **Organization Management** role group by default.
2. Go to **Roles** &gt; **User Roles**.
3. Select an existing role assignment policy or create a new one.
4. Select **New role assignment policy**![Add icon.](../../exchangeonline/media/itpro_eac_addicon.png) and update the following sections:

    - **Set up the basics**: Type a name for the policy if you are creating a new one.
    - **Add permissions**
    - **Contact information**
    - **Profile information**
    - **Distribution groups**
    - **Distribution group memberships**
    - **Other roles** (Select some or all of the roles: **My Custom Apps**, **My MarketPlace Apps**, and **My ReadWriteMailbox Apps**.)
5. Select **Next**. The **Review role assignment policy and finish** page appears.
6. Select **Create**.

    Note

    Select Create only if you are okay with the configured settings that are displayed on the **Review role assignment policy and finish** page. After reviewing the settings, if you want to edit the settings, select **Back** to navigate to the settings page, make the edits, select **Next**, and then select **Create** on the **Review role assignment policy and finish** page.

    The **Status** page appears, displaying a notification message that the role assignment policy has been successfully created.

    [![Screenshot that shows the Status page that displays the status of the policy creation.](../../exchangeonline/media/status-page.png)](../../exchangeonline/media/status-page.png#lightbox)
7. Select **Done**.

    For detailed information about how to do manage role groups, see [Manage role groups in Exchange Online](../../permissions-exo/role-groups).

## Prevent add-in downloads by turning off the Office Store across Outlook

The following steps ensure that all end users with the default policy will no longer be able to install or manage Add-ins for Outlook.

1. Sign in to the EAC with an account that's assigned the **Role Management** role. This role is assigned to the **Organization Management** role group by default.
2. Go to **Roles** &gt; **User Roles**.
3. Double-click **Default Role with Add-Ins Management** to open the **Edit** window.
4. Select **Manage permissions** under **Permissions**. The **Default Role Assignment Policy** page appears.
5. Modify **Default Role Assignment Policy** by deselecting **My Custom Apps**, **My MarketPlace Apps**, and **My ReadWriteMailbox Apps** under **Other roles**.
6. Select **Save changes**.

Note

If a user is assigned a single admin role (for example, Security Reader), removing the user roles **My Custom Apps**, **My MarketPlace Apps**, and **My ReadWriteMailbox Apps** won't prevent add-in downloads for the user. Our recommenddation is to have separate accounts for admin privileges and end-user day-to-day use.

## How do you know this worked?

To verify that you've successfully assigned permissions for a user, replace &lt;Role Name&gt; with the name of the role to verify, and run the following command in Exchange Online PowerShell:

```PowerShell
Get-ManagementRoleAssignment -Role "<Role Name>" -GetEffectiveUsers
```

The following example shows you how to verify whom you've assigned permissions to install add-ins from the Office Store for the organization:

```PowerShell
Get-ManagementRoleAssignment -Role "Org Marketplace Apps" -GetEffectiveUsers
```

In the results, review the entries in the **Effective Users** column.

For detailed syntax and parameter information, see [Get-ManagementRoleAssignment](/en-us/powershell/module/exchangepowershell/get-managementroleassignment).