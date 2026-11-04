---
layout: Conceptual
title: Role assignment policies in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/permissions-exo/role-assignment-policies
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
ms.custom:
- has-azure-ad-ps-ref
description: Admins can learn about role assignment policies, and how to view, create, modify, remove, and assign them in Exchange Online.
ms.topic: how-to
author: Simonv100
ms.author: simonklan
ms.assetid: 
ms.reviewer: serdars
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
- essentials-manage
audience: ITPro
ms.service: exchange-online
ms.date: 2023-10-31T00:00:00.0000000Z
locale: en-us
document_id: 8a48f4ef-7c6a-6daa-086d-e664b97ce239
document_version_independent_id: c734e063-fa2f-6606-c268-d78501cae271
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/permissions-exo/role-assignment-policies.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: permissions-exo/role-assignment-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/permissions-exo/role-assignment-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: e6a6357c-ceb4-aae4-e61d-160ee3b5d9e6
---

# Role assignment policies in Exchange Online | Microsoft Learn

A role assignment policy is a collection of one or more end-user roles that enable users to manage their mailbox settings and distribution groups in Exchange Online. End-users roles are part of the role based access control (RBAC) permissions model in Exchange Online. You can assign different role assignment policies to different users to allow or prevent specific self-management features in Exchange Online.

In Exchange Online, a default role assignment policy named Default Role Assignment Policy is specified by the mailbox plan that's assigned to users when their account is licensed. For more information about mailbox plans, see [Mailbox plans in Exchange Online](../recipients-in-exchange-online/manage-user-mailboxes/mailbox-plans).

Role assignment policies are how end-user roles (as opposed to management roles) are assigned to users in Exchange Online. There are several ways you can use role assignment policies to assign permissions to users:

- **New users**:

    - Change the end-user roles that are assigned to the default role assignment policy.
    - Create a custom role assignment policy and set it as the default. Note that this method only affects mailboxes that you create without specifying a role assignment policy or assigning a license (the license specifies the mailbox plan, which specifies the role assignment policy).
    - Specify a custom role assignment policy in the mailbox plan. For more information, see [Use Exchange Online PowerShell to modify mailbox plans](../recipients-in-exchange-online/manage-user-mailboxes/mailbox-plans#use-exchange-online-powershell-to-modify-mailbox-plans).
- **Existing users**:

    - Assign a different license to the user. This will apply the settings of the different mailbox plan, which specifies the role assignment policy to apply.
    - Manually assign a custom role assignment policy to mailboxes.

[![Role, role assignment policy, mailbox relationship.](../exchangeonline/media/itpro_security_rbac_exo_simplifiedraprelationship.png)](../exchangeonline/media/itpro_security_rbac_exo_simplifiedraprelationship.png#lightbox)

The available end-user roles that you can assign to mailbox plans are described in the following table:

| Role | Assigned to Default Role Assignment Policy by default? | Description |
| --- | --- | --- |
| My Custom Apps | Yes | Install custom apps. |
| My Marketplace Apps | Yes | Install marketplace apps. |
| My ReadWriteMailbox Apps | Yes | Install apps with ReadWriteMailbox permissions. |
| MyBaseOptions | Yes | Required for users to access options in Outlook on the web from their own mailbox. |
| MyContactInformation | Yes | Edit their address and telephone number in the global address list (GAL). <br> This role contains the following child roles: <br><br>- **MyAddressInformation**: Change all elements of their mailing address, work telephone number, and fax number.<br>- **MyMobileInformation**: Change their mobile phone and pager numbers.<br>- **MyPersonalInformation**: Change their home telephone number and web page.<br><br><br> If you think this role gives users too much power, you can remove the role from the role assignment policy, and assign one or more of the child roles. For instructions, see the Add or remove roles from a role assignment policy section in this topic. |
| MyDistributionGroupMembership | Yes | Join or leave existing distribution groups (if the group is configured to let members join or leave the group). |
| MyDistributionGroups | Yes | Create new distribution groups, delete groups they own, modify groups they own, and manage group membership for groups they own. |
| MyMailboxDelegation | No | Allows users to grant send on behalf of permissions to other users on their mailbox. Messages clearly show the sender in the From field (&lt;Sender&gt; on behalf of &lt;Mailbox&gt;), but replies are delivered to the mailbox, not the sender. |
| MyMailSubscriptions | Yes | Connected accounts were removed from Outlook on the web in November 2018. For more information, see [Connected accounts are no longer supported in Outlook on the web](https://support.microsoft.com/office/5cc526bf-e928-4a99-8b9f-5e089df7d887). |
| MyProfileInformation | Yes | Edit their first name, middle initial, last name, and display name in the GAL. <br> This role contains the following child roles: <br><br>- **MyDisplayName**: Change their display name.<br>- **MyName**: Change their first name, middle initial, last name and Notes property.<br><br><br> If you think this role gives users too much power, you can remove the role from the role assignment policy, and assign one of the child roles. For instructions, see the Add or remove roles from a role assignment policy section in this topic. |
| MyRetentionPolicies | Yes | Allows users to add personal tags that aren't part of their assigned retention policy.^\*^ |
| MyTeamMailboxes | Yes | Site mailboxes were discontinued in favor of Microsoft 365 groups in September 2017. For more information, see [Deprecation of Site Mailboxes](https://techcommunity.microsoft.com/blog/spblog/deprecation-of-site-mailboxes/93028). |
| MyTextMessaging | Yes | Enable text message notifications for meetings and new email messages.^\*^ |
| MyVoiceMail | Yes | Update their voice mail settings.^\*^ |

^\*^This feature isn't available in all regions or organizations.

## What do you need to know before you begin?

- Estimated time to complete each procedure: less than 5 minutes.
- The procedures in this topic require the Role Management RBAC role in Exchange Online. Typically, you get this permission via membership in the Organization Management role group. For more information, see [Manage role groups in Exchange Online](role-groups).
- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../exchange-admin-center). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- Changes to permissions take effect after the user logs out and logs in again.

## View roles assigned to a role assignment policy

### Use the EAC to view roles assigned to a role assignment policy

1. In the EAC, click **Roles** &gt; **Admin roles**. All of the role groups in your organization are listed here.
2. Select a role group. The details pane shows the **Name**, **Description**, and add the Permissions of the role group.

### Use Exchange Online PowerShell to view roles assigned to a role assignment policy

To view the roles assigned to a role assignment policy, use the following syntax:

```PowerShell
Get-ManagementRoleAssignment -RoleAssignee "<RoleAssignmentPolicyName>" | Format-Table Name,Role -Auto
```

This example returns the roles that are assigned to the policy named Default Role Assignment Policy.

```PowerShell
Get-ManagementRoleAssignment -RoleAssignee "Default Role Assignment Policy" | Format-Table Name,Role -Auto
```

For detailed syntax and parameter information, see [Get-ManagementRoleAssignment](/en-us/powershell/module/exchangepowershell/get-managementroleassignment).

**Note**: To return a list of all available end-user roles, run the following command:

```PowerShell
Get-ManagementRole | Where {$_.IsEndUserRole -eq $true} | Format-Table Name,Parent
```

## Add or remove roles from a role assignment policy

### Use the EAC to add or remove roles from a role assignment policy

1. In the EAC, click **Roles** &gt; **User roles**, select the role assignment policy, and then click **Edit**![Edit button.](../exchangeonline/media/itpro_eac_editicon.png).
2. In the policy properties window that opens, do one of the following steps:

    - To add a role, select the check box next to the role.
    - To remove a role that's already assigned, clear the check box.

    If you select a check box for a role that has child roles, the check boxes for the child roles are also selected. If you clear the check box of the parent role, the check boxes for the child roles are also cleared. You can select a child role by clearing the check box of the parent role and then selecting the individual child role.
3. When you're finished, click **Save**.

### Use Exchange Online PowerShell to add roles to a role assignment policy

Adding a role to a role assignment policy creates a new role assignment with a unique name that's a combination of the names of the role and the role assignment policy.

To add roles to a role assignment policy, use the following syntax:

```PowerShell
New-ManagementRoleAssignment -Role <RoleName> -Policy "<RoleAssignmentPolicyName>"
```

This example adds the role MyMailboxDelegation to the role assignment policy named Default Role Assignment Policy.

```PowerShell
New-ManagementRoleAssignment -Role MyMailboxDelegation -Policy "Default Role Assignment Policy"
```

For detailed syntax and parameter information, see [New-ManagementRoleAssignment](/en-us/powershell/module/exchangepowershell/new-managementroleassignment).

### Use Exchange Online PowerShell to remove roles from a role assignment policy

1. Use the procedure from the Use Exchange Online PowerShell to view roles assigned to a role assignment policy section earlier in this topic to find the name of the **role assignment** for the role that you want to remove (it's a combination of the names of the role and the role assignment policy).
2. To remove the role from the role assignment policy, use this syntax:

    ```PowerShell
    Remove-ManagementRoleAssignment -Identity "<RoleAssignmentName>"
    ```

    This example removes the MyDistributionGroups role from the role assignment policy named Default Role Assignment Policy.

    ```PowerShell
    Remove-ManagementRoleAssignment -Identity "MyDistributionGroups-Default Role Assignment Policy"
    ```

For detailed syntax and parameter information, see [Remove-ManagementRoleAssignment](/en-us/powershell/module/exchangepowershell/remove-managementroleassignment).

## Create role assignment policies

### Use the EAC to create role assignment policies

1. In the EAC, go to **Roles** &gt; **Admin roles** and then click **Add role group**.
2. In the **Add role group** window, click **Set up the basics** section, configure the following settings and click **Next**:

    - **Name**: Enter a unique name for the role group.
    - **Description**: Enter an optional description for the role group.
    - Select the roles that you want to assign to the policy.
3. In the **Add permissions** section, select the roles and click **Next**. Roles define the scope of the tasks that the members assigned to this role group have permission to manage.
4. In the **Assign admins** section, select the users to assign to this role group and click **Next**. They'll have permissions to manage the roles that you assigned.
5. In the **Review role group and finish** section, verify all the details, and then click **Add role group**.
6. Click **Done**.

### Use Exchange Online PowerShell to create role assignment policies

To create a role assignment policy, use the following syntax:

```PowerShell
New-RoleAssignmentPolicy -Name <UniqueName> [-Description "<Descriptive Text>"] [-Roles "<EndUserRole1>","<EndUserRole2>"...] [-IsDefault]
```

This example creates a new role assignment policy named Contoso Contractors that include the specified end-user roles.

```PowerShell
New-RoleAssignmentPolicy -Name "Contoso Contractors" -Description "Limited self-management capabilities for contingent staff."] -Roles "MyBaseOptions","MyContactInformation","MyProfileInformation"
```

For detailed syntax and parameter information, see [New-RoleAssignmentPolicy](/en-us/powershell/module/exchangepowershell/new-roleassignmentpolicy).

## Modify role assignment policies

You can use the EAC or Exchange PowerShell to Add or remove roles from a role assignment policy.

You can only use Exchange Online PowerShell to specify the default role assignment policy that's applied to new mailboxes that aren't assigned a license or a role assignment policy when they're created.

Otherwise, all you can do in the EAC or Exchange Online PowerShell is modify the name and description of the role assignment policy.

### Use Exchange Online PowerShell to specify the default role assignment policy

To specify the default role assignment policy, use the following syntax:

```PowerShell
Set-RoleAssignmentPolicy -Identity "<RoleAssignmentPolicyName>" -IsDefault
```

This example configures Contoso Users as the default role assignment policy.

```PowerShell
Set-RoleAssignmentPolicy -Identity "Contoso Users" -IsDefault
```

**Note**: The *IsDefault* switch is also available on the **New-RoleAssignmentPolicy** cmdlets.

For detailed syntax and parameter information, see [Set-RoleAssignmentPolicy](/en-us/powershell/module/exchangepowershell/set-roleassignmentpolicy).

## Remove role assignment policies

You can't remove the role assignment policy that's currently specified as the default. You first need to specify another role assignment policy as the default before you can delete the policy.

You can't remove a role assignment policy that's assigned to mailboxes. Use the procedures described in the Use Exchange Online PowerShell to modify role assignment policy assignments on mailboxes section to replace the role assignment policy that's assigned to mailboxes.

### Use the EAC to remove role assignment policies

1. In the EAC, go to **Roles** &gt; **Admin roles**.
2. Select the role group and click **Delete**.
3. Click **Confirm** in the confirmation window.

### Use Exchange Online PowerShell to remove role assignment policies

To remove a role assignment policy, use the following syntax:

```PowerShell
Remove-RoleAssignmentPolicy -Identity "<RoleAssignmentPolicyName>"
```

This example removes the role assignment policy named Contoso Managers.

```PowerShell
Remove-RoleAssignmentPolicy -Identity "Contoso Managers"
```

For detailed syntax and parameter information, see [Remove-RoleAssignmentPolicy](/en-us/powershell/module/exchangepowershell/remove-roleassignmentpolicy).

## View role assignment policy assignments on mailboxes

### Use the EAC to view role assignment policy assignments on mailboxes

1. In the EAC, go to **Recipients** &gt; **Mailboxes**, select the mailbox, and click **Edit**![Edit button.](../exchangeonline/media/itpro_eac_editicon.png).
2. In the mailbox properties window that opens, click **Mailbox features**. The role assignment policy is shown in the **Role assignment policy** field.
3. When you're finished, click **Save**.

### Use Exchange Online PowerShell to view role assignment policy assignments on mailboxes

To see the role assignment policy assignment on a specific mailbox, use the following syntax:

```PowerShell
Get-Mailbox -Identity <MailboxIdentity> | Format-List RoleAssignmentPolicy
```

This example returns the role assignment policy for the mailbox named Pedro Pizarro.

```PowerShell
Get-Mailbox -Identity "Pedro Pizarro" | Format-List RoleAssignmentPolicy
```

To return all mailboxes that have a specific role assignment policy assigned, use the following syntax:

```PowerShell
$<VariableName> = Get-Mailbox -ResultSize unlimited
```

```PowerShell
$<VariableName> | where {$_.RoleAssignmentPolicy -eq '<RoleAssignmentPolicyName>'}
```

This example returns all mailboxes that have the role assignment policy named Contoso Managers assigned.

```PowerShell
$Mgrs = Get-Mailbox -ResultSize unlimited
```

```PowerShell
$Mgrs | where {$_.RoleAssignmentPolicy -eq 'Contoso Managers'}
```

## Modify role assignment policy assignments on mailboxes

A mailbox can have only one role assignment policy assigned. The role assignment policy that you assign to the mailbox will replace the existing role assignment policy that's assigned.

### Use the EAC to modify role assignment policy assignments on mailboxes

In the EAC, click **Recipients** &gt; **Mailboxes**, and do one of the following steps:

- **Individual mailboxes**: Select the mailbox &gt; click **Edit**![Edit button.](../exchangeonline/media/itpro_eac_editicon.png) &gt; click **Mailbox features** in the window that opens &gt; click the dropdown next to **Role assignment policy** &gt; select a new role assignment policy &gt; click **Save**.
- **Multiple mailboxes**: Select multiple mailboxes of the same type (for example, **User**) by selecting a mailbox, holding down the Shift key, and select another mailbox farther down in the list or by holding down the Ctrl key as you select each mailbox. In the details pane (that's now titled **Bulk Edit**): click **More options** &gt; click **Update**. In the **Role Assignment Policy** section, select the role assignment policy in the window that appears &gt; click **Save**.

### Use Exchange Online PowerShell to modify role assignment policy assignments on mailboxes

To change the role assignment policy assignment on a specific mailbox, use this syntax:

```PowerShell
Set-Mailbox -Identity <MailboxIdentity> -RoleAssignmentPolicy "<RoleAssignmentPolicyName>"
```

This example applies the role assignment policy named Contoso Managers to the mailbox named Pedro Pizarro.

```PowerShell
Get-Mailbox -Identity "Pedro Pizarro" -RoleAssignmentPolicy "<RoleAssignmentPolicyName>"
```

To change the assignment for all mailboxes that have a specific role assignment policy assigned, use the following syntax:

```PowerShell
$<VariableName> = Get-Mailbox -ResultSize unlimited
```

```PowerShell
$<VariableName> | where {$_.RoleAssignmentPolicy -eq '<CurrentRoleAssignmentPolicyName>'} | Set-Mailbox -RoleAssignmentPolicy '<NewRoleAssignmentPolicyName>'
```

This example changes the role assignment policy from Default Role Assignment Policy to Contoso Staff for all mailboxes that currently have Default Role Assignment Policy assigned.

```PowerShell
$Users = Get-Mailbox -ResultSize unlimited
```

```PowerShell
$Users | where {$_.RoleAssignmentPolicy -eq 'Default Role Assignment Policy'} | Set-Mailbox -RoleAssignmentPolicy 'Contoso Staff'
```