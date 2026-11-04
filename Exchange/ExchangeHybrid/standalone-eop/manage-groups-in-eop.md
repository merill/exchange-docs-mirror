---
layout: Conceptual
title: Manage groups in the Built-in security add-on for on-premises mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/standalone-eop/manage-groups-in-eop
Manager: deniseb
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: chrisda
author: chrisda
ms.date: 2025-07-21T00:00:00.0000000Z
audience: ITPro
ms.topic: how-to
ms.localizationpriority: medium
ms.assetid: 212e68ac-6330-47e9-a169-6cf5e2f21e13
ms.custom:
- seo-marvel-apr2020
description: Admins in on-premises organizations that use the Built-in security add-on for on-premises mailboxes can learn how to create, modify, and remove distribution groups and mail-enabled security groups in the Exchange admin center (EAC) and in PowerShell.
ms.service: exchange-online
locale: en-us
document_id: 901f5a4c-0d5a-75c9-079c-579779dab855
document_version_independent_id: cb9d83e6-8fc3-1711-ae94-c84815ace2dd
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/standalone-eop/manage-groups-in-eop.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standalone-eop/manage-groups-in-eop
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/standalone-eop/manage-groups-in-eop.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: d8b48734-3b00-faca-6255-ca403c015505
---

# Manage groups in the Built-in security add-on for on-premises mailboxes | Microsoft Learn

If you use the Built-in security add-on for on-premises mailboxes, you can create, modify, and remove the following types of groups in the add-on:

- **Microsoft 365 Groups**: A collection of shared resources.
- **Distribution groups**: A collection of mail users or other distribution groups. For example, teams or other improvised groups who need to receive or send email in a common area of interest. Distribution groups are exclusively for distributing email messages, and aren't security principals (they can't have permissions assigned to them).
- **Mail-enabled security groups**: A collection of mail users and other security groups who need access permissions for admin roles. For example, you might want to give specific group of users admin permissions so they can configure anti-spam and anti-malware settings.

    Note

    - By default, new mail-enabled security groups reject messages from external (unauthenticated) senders.
    - Don't add distribution groups to mail-enabled security groups.
- **Dynamic distribution groups**: Uses recipient filters and conditions to periodically calculate the membership of the group.

You can manage groups in the Exchange admin center (EAC) and in PowerShell.

## What do you need to know before you begin?

- The EAC is available at https://admin.exchange.microsoft.com. For more information about the Exchange admin center in the Built-in security add-on for on-premises mailboxes, see [Exchange admin center in the Built-in security add-on for on-premises mailboxes](exchange-admin-center-eop).
- To connect to PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- When you manage groups in PowerShell, you might encounter throttling. The PowerShell procedures in this article use a batch processing method that results in a propagation delay of a few minutes before the results of the commands are visible.
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Manage distribution groups*: You need the **Distribution Groups** role, which is assigned to the **Recipient Management** and **Organization Management** role groups by default.
        - *Manage mail-enabled security groups*: You need the **Security Group Creation and Membership** role, which is assigned to the **Organization Management** role group by default.
        - *Manage dynamic distribution groups*: You need the **Distribution Groups** role, which is assigned to the **Recipient Management** and **Organization Management** role groups by default.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Exchange Administrator**, **Exchange Recipient Administrator**, or **Global Administrator**^\*^ roles.

        Important

        ^\*^ Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.
- For information about keyboard shortcuts that might apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center in Exchange Online](/en-us/Exchange/accessibility/keyboard-shortcuts-in-admin-center).

## Use the Exchange admin center to manage distribution groups

In the EAC at https://admin.exchange.microsoft.com, go to **Recipients** &gt; **Groups**. Or to go directly to the **Groups** page, use https://admin.exchange.microsoft.com/#/groups.

The **Groups** tab is organized by tabs based on the group type:

- **Microsoft 365** tab (default):

    The following information is shown for each Microsoft 365 Group. You can sort the groups by clicking on an available column header. Select ![](../exchangehybrid/media/modern-eac-choose-columns-icon.png)**Choose columns** to change the columns that are shown. By default, all available columns are selected:

    - **Group name** (you can't deselect this value)
    - **Group email**
    - **Sync status**
    - **Teams status**
    - **Membership type**
    - **Group privacy**
    - **Created on**

    To filter the list of Microsoft 365 Groups on the tab, select ![](../exchangehybrid/media/modern-eac-filter-icon.png)**Filter**, and then select **Groups with dynamic membership** or **Ownerless groups**. To clear the filter, select ![](../exchangehybrid/media/modern-eac-clear-filters-icon.png)**Clear filter**.
- **Distribution list** tab:

    The following information is shown for each distribution group. You can sort the groups by clicking on an available column header. Select ![](../exchangehybrid/media/modern-eac-choose-columns-icon.png)**Choose columns** to change the columns that are shown. By default, all available columns are selected:

    - **Group name** (you can't deselect this value)
    - **Group email**
    - **Sync status**
    - **Created on**
- **Dynamic distribution list** tab:

    The following information is shown for each dynamic distribution group. You can sort the groups by clicking on an available column header. Select ![](../exchangehybrid/media/modern-eac-choose-columns-icon.png)**Choose columns** to change the columns that are shown. By default, all available columns are selected:

    - **Group name** (you can't deselect this value)
    - **Group email**
    - **Sync status**
    - **Teams status**
    - **Membership type**
    - **Group privacy**
    - **Created on**
    - **Last refreshed**
    - **Next scheduled refresh**
- **Mail-enabled security** tab:

    The following information is shown for each dynamic distribution group. You can sort the groups by clicking on an available column header. Select ![](../exchangehybrid/media/modern-eac-choose-columns-icon.png)**Choose columns** to change the columns that are shown. By default, all available columns are selected:

    - **Group name** (you can't deselect this value)
    - **Group email**
    - **Sync status**
    - **Created on**

To change the list of groups on a tab from normal to compact spacing, select ![](../exchangehybrid/media/modern-eac-standard-icon.png)**Change view**, and then select ![](../exchangehybrid/media/modern-eac-compact-icon.png)**Compact list**.

Use the ![](../exchangehybrid/media/modern-eac-search-icon.png)**Search** box and a corresponding value to find specific groups on a tab.

To export the list of groups from a tab, select ![](../exchangehybrid/media/modern-eac-download-icon.png)**Export**, and then select **Export groups in this list** or **Export all groups**. In the confirmation dialog that opens, select **Continue**. The default filename is **Groups.csv** and the default location is the **Downloads** folder. If a file with that name already exists, the filename is appended with a number (for example, **Groups(1).csv**).

### Use the EAC to create groups

1. On the **Groups** page at https://admin.exchange.microsoft.com/#/groups, select ![](../exchangehybrid/media/modern-eac-add-a-group-icon.png)**Add a group** to start the new group wizard.
2. On the **Choose a group type** page, select one of the following values:

    - **Microsoft 365**
    - **Distribution**
    - **Mail-enabled security**
    - **Dynamic distribution**

    When you're finished on the **Choose a group type** page, select **Next**.
3. On the **Set up the basics** page, configure the following settings:

    - **Name**: Enter a unique name.
    - **Description**: Enter an optional description.

    When you're finished on the **Set up the basics** page, select **Next**.

    Tip

    If you selected **Dynamic distribution** on the **Choose a group type** page, the next page is **Assign users**. Otherwise, the next page is **Assign owners**.
4. On the **Assign users** page, configure the following settings for the dynamic distribution group:

    - **Owner**: Select one or more group owners.
    - **Members** section: Specify the types of recipients for the group and set up rules that determine membership. Select one of the following boxes:

        - **All recipient types**
        - **Only the following recipient types**: Messages that meet the criteria defined for this group are sent to one or more of the following recipient types:
            - **Users with Exchange mailboxes**
            - **Mail users with external email addresses**
            - **Resource mailboxes**
            - **Mail contacts with external email addresses**
            - **Mail-enabled groups**
    - **Conditions**: Select one of the following attributes from the drop-down list and provide a value to define the criteria for membership in this group:

        - **State or province**
        - **Company**
        - **Department**
        - **Custom Attribute 1** to **Custom Attribute 15**

        Note

        The values that you enter for the selected attribute must exactly match the values in the recipient's properties. For example, if you enter **Washington** for **State or province**, but the value for the recipient's property is **WA**, the condition isn't met.

        Text values aren't case-sensitive. For example, if you enter **Contoso** for the **Company** attribute, messages are sent to a recipient if this value is **contoso**.

        To add another rule to define the criteria for membership, select **Add another rule**. Each rule is connected with the Boolean operator **AND**.

        When you're finished on the **Assign users** page, select **Next** to go to the **Edit settings** page (you skip the **Assign owners** and **Add members** pages).
5. On the **Assign owners** page, select ![](../exchangehybrid/media/modern-eac-create-icon.png)**Assign owners**. In the **Assign owners** flyout that opens, find and select one or more owners, and then select **Add**.

    When you're finished on the **Assign users** page, select **Next**.
6. On the **Add members** page, select ![](../exchangehybrid/media/modern-eac-create-icon.png)**Add members**. In the **Add members** flyout that opens, find and select one or more members, and then select **Add**.

    When you're finished on the **Add members** page, select **Next**.

    If you selected **Dynamic distribution** as the group type, this page isn't available.
7. On the **Edit settings** page, what you see depends on the group type you selected on the **Group type** page:

    - **Microsoft 365 Groups**:

        - **Group email address**
        - **Privacy**: Select **Public** or **Private**
    - **Distribution groups**:

        - **Group email address**
        - **Communication: Allow people outside of my organization to send email to this distribution group**.
        - **Joining the group**section: Select one of the following values:
            - **Open**
            - **Closed**
            - **Owner approval**
        - **Leaving the group**section: Select one of the following values:
            - **Open**
            - **Closed**
    - **Mail-enabled security groups**:

        - **Group email address**
        - **Communication: Allow people outside of my organization to send email to this distribution group**.
        - **Approval: Require owner approval to join the group**
    - **Dynamic distribution groups**:

        - **Group email address**

    When you're finished on the **Edit settings** page, select **Next**.
8. On the **Review and finish adding group** page, review the settings. You can select **Edit** in each section or select **Back** to make changes.

    When you're finished on the **Review and finish adding group** page, select **Create group**.

    After the group creation is complete, select **Close**.

### Use the EAC to modify groups

1. On the **Groups** page at https://admin.exchange.microsoft.com/#/groups, select the tab that corresponds to the group type:

    - **Microsoft 365**
    - **Distribution**
    - **Dynamic distribution**
    - **Mail-enabled security**
2. Find the group that you want to modify, and then select it by using either of the following methods:

    - Select the round check box that appears in the blank area next to the first column. The following group modification actions appear on the page:

        - ![](../exchangehybrid/media/modern-eac-edit-icon.png)**Edit name and description**.
        - ![](../exchangehybrid/media/modern-eac-edit-email-addresses-icon.png)**Edit email addresses**

        In the related flyout that opens, make changes, and then select **Save changes**.
    - Click anywhere in the row other than the round check box next to the first column. The details flyout that opens contains the following tabs where you can modify the group settings. The available settings depend on the type of group:

        - **Microsoft 365 Groups**:

            - **General**tab:
                - **Basic information** section: Select **Edit** to modify the **Name** and **Description** values.
                - **Email addresses**: Select **Edit** to edit the **Primary** email address, **Aliases**, and domains of the group's email addresses.
            - **Members**tab:
                - **Owners** section: Select **View all and manage owners** to modify the group owners.
                - **Members** section: Select **View all and manage members** to modify the group members.
            - **Settings**tab:
                - **General settings**section: Configure one or more of the following values:
                    - **Allow external senders to email this group**
                    - **Send copies of group conversations and events to group members**
                    - **Hide this group from the global address list**
                - **Privacy** section: Select **Public** or **Private**.
                - **Delivery management** section: Select **Edit delivery management**to configure the following settings:
                    - **Accept messages from** section: Select**All senders** or **Only senders in the following list**.
                    - **Decline messages from** section: Select **No senders** or **Only senders in the following list**.
                - **Manage delegates** section: Select **Edit manage delegates** to add or remove delegates and set **Send as** and **Send on behalf** permissions.
            - **Microsoft Teams** tab: Select the link to manage Microsoft Teams settings for the Microsoft 365 Group in the Teams admin center.

            When you're finished in the details flyout, select **Save**.
        - **Distribution groups** and **Mail-enabled security groups**:

            - **General**tab:
                - **Basic information** section: Select **Edit** to modify the **Name** and **Description** values.
                - **Email addresses** section: Select **Edit** to edit the **Primary** email address, **Aliases** and domains of the group's email addresses.
            - **Members**tab:
                - **Owners** section: Select **View all and manage owners** to modify the group owners.
                - **Members** section: Select **View all and manage members** to modify the group members.
            - **Settings**tab:
                - **General settings** section: **Hide this group from the global address list**
                - **Delivery management** section: Select **Edit delivery management**to configure the following settings:
                    - **Sender options**: Select one of the following values:
                        - **Only allow messages from people inside my organization**
                        - **Allow messages from people inside and outside my organization**
                    - **Specified senders** section: Specify senders who are allowed to send messages to the group.
                - **Manage delegates** section: Select **Edit manage delegates** to add or remove delegates and set **Send as** and **Send on behalf** permissions.
                - **Message approval** section: Select **Edit message approval**to configure the following settings:
                    - **Require moderator approval for messages sent to this group**: Selecting this option activates the **Notify a sender if the message isn't approved**setting where you select one of the following values:
                        - **Only sender**
                        - **Only senders in your organization**
                        - **No notifications**
                    - **Group moderators**
                    - **Add senders who don't require message approval**
                - **Membership approvals** section: Select **Edit membership approvals**to configure the following settings:
                    - **Joining the group**section: Select one of the following values:
                        - **Open**
                        - **Closed**
                        - **Owner approval**
                    - **Leaving the group** section: Select **Open** or **Closed**.

            When you're finished in the details flyout, select **Save**.
        - **Dynamic distribution groups**

            - **General** tab:

                - **Basic information** section: Select **Edit** to modify the **Name** and **Description** values.
                - **Email addresses**: Select **Edit** to edit the **Primary** email address, \*\*Aliases, and domains of the group's email addresses.
            - **Members** tab:

                - **Owner** section: Select **View all and manage owners** to add and remove group owners.
                - **Members**section:
                    - Select **View all members** to see the group members.
                    - Modify the recipient filter of the dynamic distribution group by selecting one of the following values:

                        - **All recipient types**
                        - **Only the following recipient types**: Messages that meet the criteria defined for this group are sent to one or more of the following recipient types:
                            - **Users with Exchange mailboxes**
                            - **Mail users with external email addresses**
                            - **Resource mailboxes**
                            - **Mail contacts with external email addresses**
                            - **Mail-enabled groups**
                        - Modify the conditions of the dynamic group in the recipient attribute and value drop-down lists:
                            - **State or province**
                            - **Company**
                            - **Department**
                            - **Custom Attribute 1** to **Custom Attribute 15**

                        Remove existing recipient filter conditions by selecting ![](../exchangehybrid/media/modern-eac-red-remove-icon.png) next to the condition.

                        Select **Add another rule** to add more recipient filter conditions.
            - **Settings** tab:

                - **General settings** section: **Hide this group from the global address list**
                - **Delivery management** section: Select **Edit delivery management**to configure the following settings:
                    - **Sender options**: Select one of the following values:
                        - **Only allow messages from people inside my organization**
                        - **Allow messages from people inside and outside my organization**
                    - **Specified senders** section: Specify senders who are allowed to send messages to the group.
                - **Manage delegates** section: Select **Edit manage delegates** to add or remove delegates and set **Send as** and **Send on behalf** permissions.
                - **Message approval** section: Select **Edit message approval**to configure the following settings:
                    - **Require moderator approval for messages sent to this group**: Selecting this option activates the **Notify a sender if the message isn't approved** setting where you select one of the following values:

            When you're finished in the details flyout, select **Save**.

### Use the EAC to remove groups

1. On the **Groups** page at https://admin.exchange.microsoft.com/#/groups, select the tab that corresponds to the group type:

    - **Microsoft 365**
    - **Distribution**
    - **Dynamic distribution**
    - **Mail-enabled security**
2. Find, select, and remove the group using either of the following methods:

    - Select the round check box that appears in the blank area next to the first column, and then select the ![](../exchangehybrid/media/modern-eac-delete-icon.png)**Delete group** action that appears on the page.
    - Click anywhere in the row other than the round check box next to the first column. In the details flyout that opens, select ![](../exchangehybrid/media/modern-eac-delete-icon.png)**Delete group** at the top of the flyout.
3. Select **Delete group** in the flyout that opens.

### Use the EAC to add a group naming policy

For instructions, see [Use the EAC to create a group naming policy in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy).

## Use Exchange Online PowerShell to manage groups

To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

### Use PowerShell to view groups

#### View distribution groups and mail-enabled security groups in PowerShell

To return a summary list of all distribution groups and mail-enabled security groups in Exchange Online PowerShell, run the following command:

```powershell
Get-Recipient -RecipientType MailUniversalDistributionGroup,MailUniversalSecurityGroup -ResultSize unlimited
```

To return the list of group members, replace &lt;GroupIdentity&gt; with the name, alias, or email address of the group, and run the following command:

```powershell
Get-DistributionGroupMember -Identity <GroupIdentity>
```

For detailed syntax and parameter information, see [Get-Recipient](/en-us/powershell/module/exchangepowershell/get-recipient) and [Get-DistributionGroupMember](/en-us/powershell/module/exchangepowershell/get-distributiongroupmember).

#### View Microsoft 365 Groups in PowerShell

To return a summary list of all Microsoft 365 Groups, run the following command:

```powershell
Get-UnifiedGroup
```

To return information about the members, owners, or subscribers of a Microsoft 365 Group, use the following syntax:

```powershell
Get-UnifiedGroupLinks -Identity <Group name, alias or email address> -LinkType <Members | Owners | Subscribers>
```

For detailed syntax and parameter information, see [Get-UnifiedGroup](/en-us/powershell/module/exchangepowershell/get-unifiedgroup) and [Get-UnifiedGroupLinks](/en-us/powershell/module/exchangepowershell/get-unifiedgrouplinks).

#### View dynamic distribution groups in PowerShell

To return a summary list of all dynamic distribution groups, run the following command:

```powershell
Get-DynamicDistributionGroup
```

To return the membership of a dynamic distribution group, replace &lt;Identity&gt; with the name, alias, or email address of the group, and then run the following command:

```powershell
Get-DynamicDistributionGroupMember -Identity <Identity>
```

For detailed syntax and parameter information, see [Get-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/get-dynamicdistributiongroup) and [Get-DynamicDistributionGroupMember](/en-us/powershell/module/exchangepowershell/get-dynamicdistributiongroupmember).

### Use PowerShell to create groups

#### Create distribution groups and mail-enabled security groups in PowerShell

To create distribution groups or mail-enabled security groups, use the following syntax:

```PowerShell
New-DistributionGroup -Name "<Unique Name>" -ManagedBy @("UserOrGroup1","UserOrGroup2",..."UserOrGroupN">) [-Alias <text>] [-DisplayName "<Descriptive Name>"] [-Members @("UserOrGroup1","UserOrGroup2",..."UserOrGroupN">)] [-Notes "<Optional Text>"] [-PrimarySmtpAddress <SmtpAddress>] [-Type <Distribution | Security>]
```

- The *Name* parameter is required, has a maximum length of 64 characters, and must be unique. If you don't use the *DisplayName* parameter, the value of the *Name* parameter is used for the display name.
- If you don't use the *Alias* parameter, the *Name* parameter is used for the alias value. Spaces are removed and unsupported characters are converted to question marks (?).
- If you don't use the *PrimarySmtpAddress* parameter, the alias value is used in the *PrimarySmtpAddress* parameter.
- If you don't use the *Type* parameter, the default value is Distribution.

This example creates a distribution group named IT Administrators with the specified properties.

```PowerShell
New-DistributionGroup -Name "IT Administrators" -Alias itadmin -Members @("michelle@contoso.com","laura@contoso.com","julia@contoso.com") -ManagedBy "chris@contoso.com"
```

For detailed syntax and parameter information, see [New-DistributionGroup](/en-us/powershell/module/exchangepowershell/New-DistributionGroup).

#### Create Microsoft 365 Groups in PowerShell

To create Microsoft 365 groups, use the following syntax:

```powershell
New-UnifiedGroup -DisplayName "<Unique Name>" -Alias <Alias>
```

This example creates a new Microsoft 365 Group named Engineering Department.

```powershell
New-UnifiedGroup -DisplayName "Engineering Department" -Alias "engineering"
```

For detailed syntax and parameter information, see [New-UnifiedGroup](/en-us/powershell/module/exchangepowershell/New-UnifiedGroup).

#### Create dynamic distribution groups in PowerShell

To create dynamic distribution groups, use the following syntax:

```powershell
New-DynamicDistributionGroup -Name "<Unique Name>" [-Alias <text>] [-DisplayName "<Descriptive Name>"] <PrecannedFilters | CustomFilters>
```

This example creates a dynamic distribution group named Marketing Group using precanned filters: mail users who have a Department field that equals the strings "Marketing" or "Sales."

```powershell
New-DynamicDistributionGroup -Name "Marketing Group" -IncludedRecipients "MailUsers" -ConditionalDepartment "Marketing","Sales"
```

This example creates a dynamic distribution group named Washington Management Team using custom filters: all users from Washington State whose titles start with "Director" or "Manager."

```powershell
New-DynamicDistributionGroup -Name "Washington Management Team" -RecipientFilter "(Title -like 'Director*' -or Title -like 'Manager*') -and (StateOrProvince -eq 'WA')"
```

For detailed syntax and parameter information, see [New-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/new-dynamicdistributiongroup).

### Use PowerShell to modify groups

#### Modify distribution groups and mail-enabled security groups in PowerShell

To modify distribution groups and mail-enabled security groups, use the following syntax:

```powershell
Set-DistributionGroup -Identity <GroupIdentity> [-Alias <Text>] [-DisplayName <Text>] [-ManagedBy @("User1","User2",..."UserN")] [-PrimarySmtpAddress <SmtpAddress>]
```

```powershell
Update-DistributionGroupMember -Identity <GroupIdentity> -Members @("User1","User2",..."UserN")
```

This example uses changes the primary SMTP address (also called the reply address) for the Seattle Employees group to `sea.employees@contoso.com`.

```PowerShell
Set-DistributionGroup "Seattle Employees" -PrimarySmtpAddress "sea.employees@contoso.com"
```

This example replaces the current members of the Security Team group with Kitty Petersen and Tyson Fawcett.

```powershell
Update-DistributionGroupMember -Identity "Security Team" -Members @("Kitty Petersen","Tyson Fawcett")
```

This example adds a new user named Tyson Fawcett to the group named Security Team while preserving the current members of the group.

```powershell
$CurrentMemberObjects = Get-DistributionGroupMember "Security Team"

$CurrentMemberNames = $CurrentMemberObjects | % {$_.name}

$CurrentMemberNames += "Tyson Fawcett"

Update-DistributionGroupMember -Identity "Security Team" -Members $CurrentMemberNames
```

For detailed syntax and parameter information, see [Set-DistributionGroup](/en-us/powershell/module/exchangepowershell/set-distributiongroup) and [Update-DistributionGroupMember](/en-us/powershell/module/exchangepowershell/update-distributiongroupmember).

#### Modify Microsoft 365 Groups in PowerShell

To modify Microsoft 365 Groups, use the following syntax:

```powershell
Set-UnifiedGroup -Identity <GroupIdentity> [-AccessType <Public | Private>] [-AlwaysSubscribeMembersToCalendarEvents] [-AutoSubscribeNewMembers] [-CalendarMemberReadOnly] [-Alias <Text>] [-DisplayName <Text>] [-ManagedBy @("User1","User2",..."UserN")] [-PrimarySmtpAddress <SmtpAddress>]
```

```powershell
<Add-UnifiedGroupLinks | Remove-UnifiedGroupLinks> -Identity <GroupIdentity> [-LinkType <Members | Owners | Subscribers>] [-Links User1,User2,...UserN]
```

This example changes the Microsoft 365 Group named Legal Department from a public group to a private group.

```powershell
Set-UnifiedGroup -Identity "Legal Department" -AccessType Private
```

This example adds members chris@contoso.com and michelle@contoso.com to the Microsoft 365 Group named Legal Department.

```powershell
Add-UnifiedGroupLinks -Identity "Legal Department" -LinkType Members -Links chris@contoso.com,michelle@contoso.com
```

For detailed syntax and parameter information, see [Set-UnifiedGroup](/en-us/powershell/module/exchangepowershell/set-unifiedgroup), [Add-UnifiedGroupLinks](/en-us/powershell/module/exchangepowershell/add-unifiedgrouplinks), and [Remove-UnifiedGroupLinks](/en-us/powershell/module/exchangepowershell/remove-unifiedgrouplinks).

#### Modify dynamic distribution groups in PowerShell

To modify dynamic distribution groups, use the following syntax:

```powershell
Set-DynamicDistributionGroup -Identity <GroupIdentity> <Settings to change>
```

This example applies the following changes to the existing dynamic distribution group named Developers:

- Change the ConditionalCompany query filter to Contoso.
- Add the value Internal to the ConditionalCustomAttribute1 attribute.

```powershell
Set-DynamicDistributionGroup -Identity Developers -ConditionalCompany "Contoso" -ConditionalCustomAttribute1 "Internal"
```

For detailed syntax and parameter information, see [Set-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/set-dynamicdistributiongroup).

### Use PowerShell to remove groups

#### Remove distribution groups and mail-enabled security groups in PowerShell

To remove distribution groups or mail-enabled security groups, use the following syntax:

```powershell
Remove-DistributionGroup -Identity <GroupIdentity>
```

This example uses removes the distribution group named IT Administrators.

```PowerShell
Remove-DistributionGroup -Identity "IT Administrators"
```

For detailed syntax and parameter information, see [Remove-DistributionGroup](/en-us/powershell/module/exchangepowershell/remove-distributiongroup).

#### Remove Microsoft 365 Groups in PowerShell

To remove Microsoft 365 Groups, use the following syntax:

```powershell
Remove-UnifiedGroup -Identity <GroupIdentity>
```

This example removes the Microsoft 365 Group named Research Department.

```powershell
Remove-UnifiedGroup -Identity "Research Department"
```

For detailed syntax and parameter information, see [Remove-UnifiedGroup](/en-us/powershell/module/exchangepowershell/remove-unifiedgroup).

#### Remove dynamic distribution groups in PowerShell

To remove dynamic distribution groups, use the following syntax:

```powershell
Remove-DynamicDistributionGroup -Identity <GroupIdentity>
```

This example deletes the dynamic distribution group named Test Users.

```powershell
Remove-DynamicDistributionGroup -Identity "Test Users"
```

For detailed syntax and parameter information, see [Remove-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/remove-dynamicdistributiongroup).

## How do you know these procedures worked?

To verify you successfully created, modified, or removed a group, do any of the following steps:

- **EAC**: On the **Groups** page at https://admin.exchange.microsoft.com/#/groups, select the tab that corresponds to the group type:

    - **Microsoft 365**
    - **Distribution**
    - **Dynamic distribution**
    - **Mail-enabled security**

    Find the group, click on the group name, and view the details in the flyout that opens.
- **Exchange Online PowerShell**:

    - **Distribution groups or mail-enabled security groups**:

        - Run the following command to verify the group is or isn't listed:

            ```powershell
            Get-Recipient -RecipientType MailUniversalDistributionGroup,MailUniversalSecurityGroup -ResultSize unlimited
            ```
        - Replace &lt;GroupIdentity&gt; with the name, alias, or email address of the group and run the following command to verify the settings:

            ```powershell
            Get-Recipient -Identity <GroupIdentity> | Format-List
            ```
        - To view the group members, replace &lt;GroupIdentity&gt; with the name, alias, or email address of the group and run the following command:

            ```powershell
            Get-DistributionGroupMember -Identity "<GroupIdentity>"
            ```
    - **Microsoft 365 Groups**:

        - Run the following command to verify the group is or isn't listed:

            ```powershell
            Get-UnifiedGroup -ResultSize unlimited
            ```
        - Replace &lt;GroupIdentity&gt; with the name, alias, or email address of the group and run the following command to verify the settings:

            ```powershell
            Get-UnifiedGroup -Identity <GroupIdentity> | Format-List
            ```
        - To view the group members, owners, or subscribers, replace &lt;GroupIdentity&gt; with the name, alias, or email address of the group, choose the LinkType value, and then run the following command:

            ```powershell
            Get-UnifiedGroupLinks -Identity "<GroupIdentity>" -LinkType <Members | Owners | Subscribers>
            ```
    - **Dynamic distribution groups**

        - Run the following command to verify the group is or isn't listed:

            ```powershell
            Get-DynamicDistributionGroup -ResultSize unlimited
            ```
        - Replace &lt;GroupIdentity&gt; with the name, alias, or email address of the group and run the following command to verify the settings:

            ```powershell
            Get-DynamicDistributionGroup -Identity <GroupIdentity> | Format-List
            ```
        - To view the group members, replace &lt;GroupIdentity&gt; with the name, alias, or email address of the group and run the following command:

            ```powershell
            Get-DynamicDistributionGroupMember -Identity "<GroupIdentity>"
            ```