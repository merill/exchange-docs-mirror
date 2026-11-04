---
layout: Conceptual
title: Manage role groups in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/permissions-exo/role-groups
Manager: dansimp
ms.subservice: exo-roles
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: 'Summary: Learn how to view, create, copy, modify, and remove management role groups in Exchange Online.'
ms.topic: how-to
author: Simonv100
ms.author: simonklan
ms.assetid: ab9b7a3b-bf67-4ba1-bde5-8e6ac174b82c
ms.reviewer: serdars
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
- essentials-manage
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-22T00:00:00.0000000Z
locale: en-us
document_id: c55eac72-c0ce-5ccf-e33d-f6439ea3dadc
document_version_independent_id: 364c5da3-822a-2350-4ae1-2ecf49672bf3
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/permissions-exo/role-groups.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: permissions-exo/role-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/permissions-exo/role-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: aab959fc-36be-f500-9f66-407458058c6b
---

# Manage role groups in Exchange Online | Microsoft Learn

A role group is a special universal security group (USG) in the Role Based Access Control (RBAC) permissions model in Exchange Online. The members of the role group are assigned the same set of roles, and you add and remove permissions from users by adding them to or removing them from the role group. For more information about role groups in Exchange Online, see [Permissions in Exchange Online](permissions-exo).

You can manage role groups in the Exchange admin center (EAC) and in Exchange Online PowerShell.

## What do you need to know before you begin?

- The EAC is available at https://admin.exchange.microsoft.com. For more information about the EAC, see the following articles:

    - [Exchange admin center in Exchange Online](../exchange-admin-center)
    - [Exchange admin center in the Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/exchange-admin-center-eop).
- To open Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. Specifically:

    - [Exchange Online permissions](permissions-exo): You need the **Role Management** role, which is assigned to the **Organization Management** role group by default.
- For information about keyboard shortcuts that might apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center in Exchange Online](../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to manage role groups

In the EAC at https://admin.exchange.microsoft.com, go to **Permissions** &gt; **Admin roles**. Or, to go directly to the **Admin roles** page, use https://admin.exchange.microsoft.com/#/adminRoles.

### Use the EAC to view role groups and role group details

On the **Admin roles** page in the EAC at https://admin.exchange.microsoft.com/#/adminRoles, the following information is shown for all built-in and customer role groups:

- **Role group**: The name of the role group.
- **Description**

To sort the list of role groups, select on a column header.

To change the list of entries from normal to compact spacing, select ![](../exchangeonline/media/modern-eac-standard-icon.png)**Change view**, and then select ![](../exchangeonline/media/modern-eac-compact-icon.png)**Compact list**.

Use the ![](../exchangeonline/media/modern-eac-search-icon.png)**Search** box and a corresponding value to find specific role groups.

To view the details of a role group, select the group from the list by clicking on the name. The details flyout that opens contains the following tabs:

- **General** tab: This tab contains the following information about the role:

    - **Name**
    - **Description**: Select **Edit basics** to change the Name.
    - **Managed by**
    - **Write scope**
- **Assigned** tab: This tab shows the users who are members of the role. The tab has the same ![](../exchangeonline/media/modern-eac-standard-icon.png)**Change view** and ![](../exchangeonline/media/modern-eac-search-icon.png)**Search** capabilities as the main role group view.

    To modify group membership, see the section.

### Use the EAC to create role groups

1. On the **Admin roles** page in the EAC at https://admin.exchange.microsoft.com/#/adminRoles, do one of the following steps:

    - **Create a new role group**: Verify that no role groups are selected, and then select ![](../exchangeonline/media/add-role-group.png)**Add role group**.
    - **Copy an existing role group**: Select the role group that you want to copy by selecting the round check box that appears in the blank area next to the role group name column, and then select the ![](../exchangeonline/media/modern-eac-copy-icon.png)**Copy role group** action that appears\*\*.

    Either one of these steps starts the role creation wizard as described in the remaining steps.
2. On the **Basics** page, configure the following settings:

    - **Name**: Enter a unique name for the role group.
    - **Description**: Enter an optional description for the role group.
    - **Write scope**: Leave the default value **Default**, or select an existing write scope object that you previously created in PowerShell.

    If you're copying a role group, the default **Name** value is **Copy of &lt;Role group name&gt;** and the existing **Description** value is copied, but you can change these values.

    When you're finished on the **Basics** page, select **Next**.
3. On the **Permission** page, select the roles to assign to the role group by selecting the check box next to the **Role** column.

    To sort the roles, select on a column heading:

    - **Role**
    - **Description**
    - **Default recipient scope**
    - **Default configuration scope**

    To change the list of entries from normal to compact spacing, select ![](../exchangeonline/media/modern-eac-standard-icon.png)**Change view**, and then select ![](../exchangeonline/media/modern-eac-compact-icon.png)**Compact list**.

    Use the ![](../exchangeonline/media/modern-eac-search-icon.png)**Search** box and a corresponding value to find a specific role group.

    If you're copying a role group, the permissions from the original role group are already selected, but you can change them.

    When you're finished on the **Permission** page, select **Next**.
4. On the **Admins** page, select the users to add to the role group.

    Click in the box to see all eligible accounts and role groups to select from, or start typing a name or display name to filter the results.

    If you're copying a role group, the members from the original role group are already selected, but you can change them.

    To remove users from the group, select ![](../exchangeonline/media/modern-eac-remove-icon.png)**Remove** on the entry.

    When you're finished on the **Admins** page, select **Next**
5. On the **Review and finish** page, verify your selections.

    Use the **Edit** links in each section to change the value, or use the **Back** button.

    When you're finished on the **Review and finish** page, select **Add role group** or **Copy role group** to create the role group.

### Use the EAC to modify role groups

Tip

You can't change the name or description of a built-in role group.

Don't change the roles that are assigned to built-in role groups. Copy the existing role group and modify the copy, or create a custom role group instead.

1. On the **Admin roles** page in the EAC at https://admin.exchange.microsoft.com/#/adminRoles, select a role group by clicking on the role group name.
2. In the details flyout that opens, configure one or more of the following settings:

    - **General** tab: Select **Edit basics** to change the name or description of the group in the flyout that opens, and then select **Save**.
    - **Assigned** tab: Change the membership of the role group:

        - **Add members**: Select ![](../exchangeonline/media/modern-eac-create-icon.png)**Add**. In the **Add admins** flyout that opens, click in the box to see all eligible accounts and role groups to select from, or start typing a name or display name to filter the results. Select the user by clicking on the entry below the box, and then select **Add**.
        - **Remove members**: Select the check box next to one or more existing members in the list, and then select the ![](../exchangeonline/media/modern-eac-delete-icon.png)**Delete** action that appears, and then select **Yes, remove** in the confirmation dialog.
    - **Permission** tab: Select the roles to assign to the role group by selecting the check box next to the **Role** column.

        To sort the roles, select on a column heading:

        - **Role**
        - **Default recipient scope**
        - **Default configuration scope**

        To change the list of entries from normal to compact spacing, select ![](../exchangeonline/media/modern-eac-standard-icon.png)**Change view**, and then select ![](../exchangeonline/media/modern-eac-compact-icon.png)**Compact list**.

        Use the ![](../exchangeonline/media/modern-eac-search-icon.png)**Search** box and a corresponding value to find a specific role group.

        When you're finished on the tab, select **Save**.

    Tip

    Users may have to sign out and sign in again to see the change in their administrative rights after you add or remove members from the role group.

### Use the EAC to remove role groups

You can't remove built-in role groups, but you can remove custom role groups.

1. On the **Admin roles** page in the EAC at https://admin.exchange.microsoft.com/#/adminRoles, select the role group that you want to remove by selecting the round check box that appears in the blank area next to the role group name column, and then select the ![](../exchangeonline/media/modern-eac-delete-icon.png)**Delete** action that appears.
2. In the confirmation flyout that opens, select **Confirm**.

## Use Exchange Online PowerShell to manage role groups

To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

### Use Exchange Online PowerShell to view role groups

To view a role group, use the following syntax:

```powershell
Get-RoleGroup [-Identity "<Role Group Name>"] [-Filter <Filter>]
```

This example returns a summary list of all role groups.

```powershell
Get-RoleGroup
```

This example returns detailed information for the role group named Recipient Administrators.

```powershell
Get-RoleGroup -Identity "Recipient Administrators" | Format-List
```

This example returns all role groups where the user Julia is a member. You need to use the DistinguishedName (DN) value for Julia, which you can find by running the command: `Get-User -Identity Julia | Format-List DistinguishedName`.

```powershell
Get-RoleGroup -Filter "Members -eq 'CN=Julia,OU=contoso.onmicrosoft.com,OU=Microsoft Exchange Hosted Organizations,DC=NAMPR001,DC=PROD,DC=OUTLOOK,DC=COM'"
```

For detailed syntax and parameter information, see [Get-RoleGroup](/en-us/powershell/module/exchangepowershell/Get-RoleGroup).

### Use Exchange Online PowerShell to create role groups

To create a new role group, use the following syntax:

```powershell
New-RoleGroup -Name "Unique Name" -Description "Descriptive text" -Roles <"Role1","Role2"...> -ManagedBy <Managers> -Members <Members> -CustomRecipientWriteScope "<Existing Write Scope Name>"
```

- The *Roles* parameter specifies the management roles to assign to the role group by using the following syntax `"Role1","Role1",..."RoleN"`. You can see the available roles by using the **Get-ManagementRole** cmdlet.
- The *Members* parameter specifies the members of the role group by using the following syntax: `"Member1","Member2",..."MemberN"`. You can specify users, mail-enabled universal security groups (USGs), or other role groups (security principals).
- The *ManagedBy* parameter specifies the delegates who can modify and remove the role group by using the following syntax: `"Delegate1","Delegate2",..."DelegateN"`. This setting isn't available in the EAC.
- The *CustomRecipientWriteScope* parameter specifies the existing custom recipient write scope to apply to the role group. You can see the available custom recipient write scopes by using the **Get-ManagementScope** cmdlet.

This example creates a new role group named "Limited Recipient Management" with the following settings:

- The Mail Recipients and Mail Enabled Public Folders roles are assigned to the role group.
- The users Kim and Martin are added as members. Because no custom recipient write scope was specified, Kim and Martin can manage any recipient in the organization.

```powershell
New-RoleGroup -Name "Limited Recipient Management" -Roles "Mail Recipients","Mail Enabled Public Folders" -Members "Kim","Martin"
```

This example uses a custom recipient write scope, which means Kim and Martin can only manage recipients that are included in the Seattle Recipients scope (recipients who have their **City** property set to the value Seattle).

```powershell
New-RoleGroup -Name "Limited Recipient Management" -Roles "Mail Recipients","Mail Enabled Public Folders" -Members "Kim","Martin" -CustomRecipientWriteScope "Seattle Recipients"
```

For detailed syntax and parameter information, [New-RoleGroup](/en-us/powershell/module/exchangepowershell/New-RoleGroup).

### Use Exchange Online PowerShell to copy role groups

1. Store the role group that you want to copy in a variable using the following syntax:

    ```powershell
    $RoleGroup = Get-RoleGroup "<Existing Role Group Name>"
    ```
2. Create the new role group using the following syntax:

    ```powershell
    New-RoleGroup -Name "<Unique Name>" -Roles $RoleGroup.Roles [-Members <Members>] [-ManagedBy <Managers>] [-CustomRecipientWriteScope "<Existing Custom Recipient Write Scope Name>"]
    ```

    - The *Members* parameter specifies the members of the role group by using the following syntax: `"Member1","Member2",..."MemberN"`. You can specify users, mail-enabled universal security groups (USGs), or other role groups (security principals).
    - The *ManagedBy* parameter specifies the delegates who can modify and remove the role group by using the following syntax: `"Delegate1","Delegate2",..."DelegateN"`. This setting isn't available in the EAC.
    - The *CustomRecipientWriteScope* parameter specifies the existing custom recipient write scope to apply to the role group. You can see the available custom recipient write scopes by using the **Get-ManagementScope** cmdlet.

    This example copies the Organization Management role group to the new role group named "Limited Organization Management." The role group members are Isabelle, Carter, and Lukas and the role group delegates are Jenny and Katie.

    ```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    
    New-RoleGroup "Limited Organization Management" -Roles $RoleGroup.Roles -Members "Isabelle","Carter","Lukas" -ManagedBy "Jenny","Katie"
    ```

    This example copies the Organization Management role group to the new role group called Vancouver Organization Management with the Vancouver Users recipient custom recipient write scope.

    ```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    
    New-RoleGroup "Vancouver Organization Management" -Roles $RoleGroup.Roles -CustomRecipientWriteScope "Vancouver Users"
    ```

For detailed syntax and parameter information, [New-RoleGroup](/en-us/powershell/module/exchangepowershell/New-RoleGroup).

### Use Exchange Online PowerShell modify the list of members in role groups

- The **Add-RoleGroupMember** and **Remove-RoleGroupMember** cmdlets add or remove individual members one at a time. The **Update-RoleGroupMember** cmdlet can replace or modify the existing list of members.
- The members of a role group can be users, mail-enabled universal security groups (USGs), or other role groups (security principals).

To modify the members of a role group, use the following syntax:

```powershell
Update-RoleGroupMember -Identity "<Role Group Name>" -Members <Members>
```

- To *replace* the existing list of members with the values you specify, use the following syntax: `"Member1","Member2",..."MemberN"`.
- To *selectively modify* the existing list of members, use the following syntax: `@{Add="Member1","Member2"...; Remove="Member3","Member4"...}`.

This example replaces all current members of the Help Desk role group with the specified users.

```powershell
Update-RoleGroupMember -Identity "Help Desk" -Members "Gabriela Laureano","Hyun-Ae Rim","Jacob Berger"
```

This example adds Daigoro Akai and removes Valeria Barrio from the list of members on the Help Desk role group.

```powershell
Update-RoleGroupMember -Identity "Help Desk" -Members @{Add="Daigoro Akai"; Remove="Valeria Barrios"}
```

For detailed syntax and parameter information, see [Update-RoleGroupMember](/en-us/powershell/module/exchangepowershell/Update-RoleGroupMember).

### Use Exchange Online PowerShell to add roles to custom role groups (create role assignments)

To add roles to custom role groups in Exchange Online PowerShell, you create *management role assignments* by using the following syntax:

```powershell
New-ManagementRoleAssignment [-Name "<Unique Name>"] -SecurityGroup "<Role Group Name>" -Role "<Role Name>" [-RecipientRelativeWriteScope <MyGAL | MyDistributionGroups | Organization | Self>] [-CustomRecipientWriteScope "<Role Scope Name>]
```

- The role assignment name is created automatically if you don't specify one.
- If you don't use the *RecipientRelativeWriteScope* parameter, the implicit read scope and implicit write scope of the role is applied to the role assignment.
- If a predefined scope meets your business requirements, you can use the *RecipientRelativeWriteScope* parameter to apply the scope to the role assignment.
- To apply a custom recipient write scope, use the *CustomRecipientWriteScope* parameter.

This example assigns the Transport Rules management role to the Seattle Compliance role group.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Compliance" -Role "Transport Rules"
```

This example assigns the Message Tracking role to the Enterprise Support role group and applies the Organization predefined scope.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Enterprise Support" -Role "Message Tracking" -RecipientRelativeWriteScope Organization
```

This example assigns the Message Tracking role to the Seattle Recipient Admins role group and applies the Seattle Recipients scope.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Message Tracking" -CustomRecipientWriteScope "Seattle Recipients"
```

For detailed syntax and parameter information, see [New-ManagementRoleAssignment](/en-us/powershell/module/exchangepowershell/new-managementroleassignment).

### Use Exchange Online PowerShell to remove roles from custom role groups (remove role assignments)

To remove roles from custom role groups in Exchange Online PowerShell, you remove *management role assignments* by using the following syntax:

```powershell
Get-ManagementRoleAssignment -RoleAssignee "<Role Group Name>" -Role "<Role Name>" -Delegating <$true | $false> | Remove-ManagementRoleAssignment
```

- To remove *regular* role assignments that grant permissions to users, use the value `$false` for the *Delegating* parameter.
- To remove *delegating* role assignments that allow the role to be assigned to others, use the value `$true` for the *Delegating* parameter.

This example removes the Distribution Groups role from the Seattle Recipient Administrators role group.

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Seattle Recipient Administrators" -Role "Distribution Groups" -Delegating $false | Remove-ManagementRoleAssignment
```

For detailed syntax and parameter information, see [Remove-ManagementRoleAssignment](/en-us/powershell/module/exchangepowershell/remove-managementroleassignment).

### Use Exchange Online PowerShell to modify the scope of role assignments in custom role groups

The write scope of a role assignment in a role group defines the objects that the members of the role group can operate on (for example, all users, or only the users whose **City** property has the value Vancouver). You can modify the write scope of the roles assigned to a custom role group to:

- The implicit scope from the roles themselves. This means you didn't specify any custom scopes when you created the role group, or you set the value of all role assignments in an existing role group to the value `$null`.
- The same custom scope for all role assignments.
- Different custom scopes for each individual role assignment.

To set the scope on all of the role assignments on a role group at the same time, use the following syntax:

```powershell
Get-ManagementRoleAssignment -RoleAssignee "<Role Group Name>" | Set-ManagementRoleAssignment [-CustomRecipientWriteScope "<Recipient Write Scope Name>"] [-RecipientRelativeScopeWriteScope <MyDistributionGroups | Organization | Self>] [-ExclusiveRecipientWriteScope "<Exclusive Recipient Write Scope name>"]
```

This example changes the recipient scope for all role assignments on the Sales Recipient Management role group to Direct Sales Employees.

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Sales Recipient Management" | Set-ManagementRoleAssignment -CustomRecipientWriteScope "Direct Sales Employees"
```

To change the scope on an individual role assignment between a role group and a management role, do the following steps:

1. Replace &lt;Role Group Name&gt; with the name of the role group and run the following command to find the names of all the role assignments on the role group:

    ```powershell
    Get-ManagementRoleAssignment -RoleAssignee "<Role Group Name>" | Format-List Name
    ```
2. Find the name of the role assignment you want to change. Use the name of the role assignment in the next step.
3. To set the scope on the individual role assignment, use the following syntax:

    ```powershell
    Set-ManagementRoleAssignment -Identity "<Role Assignment Name"> [-CustomRecipientWriteScope "<Recipient Write Scope Name>"] [-RecipientRelativeScopeWriteScope <MyDistributionGroups | Organization | Self>] [-ExclusiveRecipientWriteScope "<Exclusive Recipient Write Scope name>"]
    ```

    This example changes the recipient scope for the role assignment named Mail Recipients\_Sales Recipient Management to All Sales Employees.

    ```powershell
    Set-ManagementRoleAssignment "Mail Recipients_Sales Recipient Management" -CustomRecipientWriteScope "All Sales Employees"
    ```

    For detailed syntax and parameter information, see [Set-ManagementRoleAssignment](/en-us/powershell/module/exchangepowershell/set-managementroleassignment).

### Use Exchange Online PowerShell to modify the list of delegates in role groups

Role group delegates define who is allowed to modify and delete the role group. You can't manage role group delegates in the EAC.

To modify the list of delegates in a role group, use the following syntax:

```powershell
Set-RoleGroup -Identity "<Role Group Name>" -ManagedBy <Delegates>
```

- To *replace* the existing list of delegates with the values you specify, use the following syntax: `"Delegate1","Delegate2",..."DelegateN"`.
- To *selectively modify* the existing list of delegates, use the following syntax: `@{Add="Delegate1","Delegate2"...; Remove="Delegate3","Delegate4"...}`.

This example replaces all current delegates of the Help Desk role group with the specified users.

```powershell
Set-RoleGroup -Identity "Help Desk" -ManagedBy "Gabriela Laureano","Hyun-Ae Rim","Jacob Berger"
```

This example adds Daigoro Akai and removes Valeria Barrio from the list of delegates on the Help Desk role group.

```powershell
Set-RoleGroup -Identity "Help Desk" -ManagedBy @{Add="Daigoro Akai"; Remove="Valeria Barrios"}
```

For detailed syntax and parameter information, see [Set-RoleGroup](/en-us/powershell/module/exchangepowershell/set-rolegroup).

### Use Exchange Online PowerShell to remove custom role groups

You can't remove built-in role groups, but you can remove custom role groups.

To remove a custom role group, use the following syntax:

```powershell
Remove-RoleGroup -Identity "<Role Group Name>" [-BypassSecurityGroupManagerCheck]
```

This example removes the Training Administrators role group.

```powershell
Remove-RoleGroup -Identity "Training Administrators"
```

For detailed syntax and parameter information, see [Remove-RoleGroup](/en-us/powershell/module/exchangepowershell/Remove-RoleGroup).

### How do you know these procedures worked?

To verify that you successfully created, modified, or removed a role group, do either of the following steps:

- In the EAC, go to the **Admin roles** page at https://admin.exchange.microsoft.com/#/adminRoles, and verify the role group is listed (or not listed). Select the role group by clicking on the name, and verifying the settings in the details flyout that opens.
- In Exchange Online PowerShell, replace &lt;Role Group Name&gt; with the name of the role group, and run the following command to verify the role group exists (or doesn't exist) and verify the settings:

    ```powershell
    Get-RoleGroup -Identity "<Role Group Name>" | Format-List
    ```