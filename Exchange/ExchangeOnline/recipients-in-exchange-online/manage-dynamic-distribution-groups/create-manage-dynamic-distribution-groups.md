---
layout: Conceptual
title: Create and manage dynamic distribution groups in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/create-manage-dynamic-distribution-groups
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
description: Dynamic distribution groups are mail-enabled Active Directory group objects that are created to expedite the mass sending of email messages and other information within a Microsoft Exchange organization.
ms.topic: how-to
author: SerdarSoysal
f1.keywords:
- CSH
ms.custom:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDynamicGroupWizardForm.CreateDynamicGroupInformationWizardPage
ms.author: serdars
ms.assetid: 8ef85d0a-41df-4b5c-b8e7-ca8d09c048ca
ms.reviewer: AkshayaPrakash-PM
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-03-13T00:00:00.0000000Z
locale: en-us
document_id: 9b191041-23ca-3e1e-8082-3559392a325e
document_version_independent_id: 2ea0fa8f-ba58-9755-35c7-6ac13f717be8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-dynamic-distribution-groups/create-manage-dynamic-distribution-groups.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-dynamic-distribution-groups/create-manage-dynamic-distribution-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-dynamic-distribution-groups/create-manage-dynamic-distribution-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 31f907ce-d426-904e-6f5f-104b070b35b5
---

# Create and manage dynamic distribution groups in Exchange Online | Microsoft Learn

Dynamic distribution groups (DDGs) are mail-enabled group objects that are created to expedite the mass sending of email messages and other information within your Microsoft Exchange organization. Unlike regular distribution groups that contain a defined set of members, the membership list for DDGs is based on membership rules that you define.

DDGs in Exchange Online behave differently when compared to DDGs in the on-premises version of Exchange Server. For each DDG, its membership list is initially calculated and stored upon creation or when its membership rules are modified, and then refreshed at least once every 24 hours. When an email message is sent to a DDG, it's delivered to all the recipients present in the membership list at that time. For details on the timing of these operations, see Dynamic distribution group membership lifecycle.

Between refreshes, the list of DDG members might become stale. Here are some implications to be aware of:

1. **Recipient attribute changes don't affect DDG mail delivery until the next refresh**: For example, if a user leaves a department that's part of the group's membership rules, they might continue to receive emails sent to the DDG until the next refresh. Conversely, if a user newly matches the membership rules, they might not start receiving emails sent to the DDG until the next refresh.
2. **Mail flow rules (also known as transport rules) are affected the same way**: Mail flow rules use the same membership list, so they're subject to the same staleness.

A DDG includes any recipient with attribute values that match its membership rules. If a recipient's properties are modified to match the membership rules, the recipient could inadvertently become a group member and start receiving messages that are sent to the group. Well-defined, consistent account-provisioning processes reduce the chances of this issue occurring.

DDGs aren't synced from Exchange Online to Microsoft Entra ID or to your on-premises Active Directory. Therefore, features such as Azure Conditional Access don't support being scoped to an Exchange Online DDG.

## Types of membership rules

DDG membership rules are built either with a pre-canned filter or with a custom recipient filter.

### Pre-canned filters

Pre-canned filters are convenient if you want to construct a DDG with simple rules based on the supported attributes that are described in the following table:

| Attribute | Send message to a recipient if... |
| --- | --- |
| State or province | The specified value matches the recipient's State or Province property. |
| Company | The specified value matches the recipient's Company property. |
| Department | The specified value matches the recipient's Department property. |
| Custom attribute N (where N is a number from 1 to 15) | The specified value matches the recipient's CustomAttributeN property. |

You can combine multiple rules to define membership with pre-canned filters, but only the logical operator **AND** is supported. You can create DDGs with pre-canned filters using either the Exchange Admin Center (EAC) or the Exchange Online PowerShell.

### Custom recipient filters

If you want to specify rules for attributes other than the ones mentioned in the preceding table (in Pre-canned filters), or you want to combine multiple rules using logical operators other than **AND**, you must use a custom recipient filter. You can create DDGs with custom recipient filters by using only Exchange Online PowerShell, and by using the **RecipientFilter** parameter.

For more information about the filterable properties that you can use with the **RecipientFilter** parameter, see [Filterable properties for the RecipientFilter parameter](/en-us/powershell/exchange/recipientfilter-properties?view=exchange-ps&amp;preserve-view=true).

For more information about the supported operators that you can use in a custom recipient filter, see [Filters in the Exchange Online PowerShell module](/en-us/powershell/exchange/filters-v2?view=exchange-ps&amp;preserve-view=true).

Warning

Using a wildcard as a prefix (for example, `Property -like '*abc'`) isn't supported in custom recipient filters for DDGs in Exchange Online due to low performance and degraded experience.

## Dynamic distribution group membership lifecycle

DDG membership is calculated at three points in a DDG's lifecycle: when it's created, when its membership rules are modified, and during the routine 24-hour refresh.

### Initial population and recalculation

When you create a DDG, a background process calculates the membership list within up to 2 hours. During this time, the DDG has no members and isn't ready for use.

When you modify the membership rules of an existing DDG, a background process recalculates the membership list within up to 2 hours. During recalculation, the DDG continues to use the previous membership list.

Important

**Starting in late May 2026,** the timing of initial membership population (on creation) and recalculation (on rule modification) depends on how many members the membership rules return:

- **5,000 members or fewer:** For new DDGs, the creation operation populates the membership list immediately, and the DDG is available for use right away. For modifications to membership rules of existing DDGs, the modification operation recalculates the membership list immediately.
- **More than 5,000 members:** A background process completes initial population (after creation) and recalculation (after rule modification) within up to 2 hours. The DDG continues to use the previous membership list during recalculation. A warning also appears at creation or modification time in both Exchange Admin Center (EAC) and Exchange Online PowerShell to indicate delayed population or recalculation.

### Routine refresh

After initial population, the system refreshes every DDG's membership list at least once every 24 hours, regardless of group size. The refresh keeps membership in sync with changes to recipient attributes—for example, a user who moves departments is added to or removed from DDGs that use department in their membership rules within 24 hours.

## Before you begin

- You need to be assigned permissions before you can perform these procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Create a dynamic distribution group

Note

For details on when membership becomes available after creation, see Dynamic distribution group membership lifecycle.

# [In the EAC](#tab/create-new-eac)
In the EAC, you can **only create DDGs with pre-canned filters.**

To create a DDG in EAC, perform the following steps:

1. In the [EAC](https://admin.exchange.microsoft.com), select **Recipients** &gt; **Groups**.
2. Select **Add a group** and follow the instructions in the **Details** pane.

    - Under **Choose a group type** section, select **Dynamic distribution** and select **Next**.
    - Under **Set up the basics** section, enter the details and select **Next**.
3. Under **Assign Users** section, select the group owner from the **Owner** drop-down list.
4. Use the **Members** section to specify the types of recipients for the group and to set up rules that determine membership. Select one of the following boxes:

    - **All recipient types**: Select this checkbox to send messages that meet the criteria defined for this group to all recipient types.
    - **Only the following recipient types**: Select this checkbox to send messages that meet the criteria defined for this group to one or more of the following recipient types:

        - **Users with Exchange mailboxes**: Select this checkbox if you want to include users that have Exchange mailboxes. Users that have Exchange mailboxes are those users that have a user domain account and a mailbox in the Exchange organization. Resource mailboxes are also included.
        - **Mail users with external email addresses**: Select this checkbox if you want to include users that have external email addresses. Users that have external email accounts have user domain accounts in Active Directory, but use email accounts that are external to the organization. This enables them to be included in the global address list (GAL) and to be added to distribution lists.
        - **Resource mailboxes**: Select this checkbox if you want to include Exchange resource mailboxes. Resource mailboxes allow you to administer company resources through a mailbox, such as a conference room or a company vehicle.
        - **Mail contacts with external email addresses**: Select this checkbox if you want to include contacts that have external email addresses. Contacts that have external email addresses don't have user domain accounts in Active Directory, but the external email address is available in the GAL.
        - **Mail-enabled groups**: Select this checkbox if you want to include security groups or distribution groups that have been mail-enabled. Mail-enabled groups are similar to distribution groups. Email messages that are sent to a mail-enabled group account will be delivered to several recipients.
5. Select one of the attributes specified in the table under Pre-canned filters from the **Select condition** drop-down list and provide a value to define the criteria for membership in this group.

    [![Screenshot that shows the Select condition drop-down list.](../../exchangeonline/media/select-condition-drop-down-list.png)](../../exchangeonline/media/select-condition-drop-down-list.png#lightbox)

    Important

    The values that you enter for the selected attribute must exactly match those that appear in the recipient's properties. For example, if you enter **Washington** for **State or province**, but the value for the recipient's property is **WA**, the condition won't be met. Also, text-based values that you specify aren't case-sensitive. For example, if you specify **Contoso** for the **Company** attribute, messages will be sent to a recipient if this value is **contoso**.
6. To add another rule to define the criteria for membership, select **Add another rule**. When you've finished, select **Next**.

    Important

    If you add multiple rules to define membership, a recipient must meet the criteria of each rule to be added as a member to the DDG. In other words, each rule is connected with the Boolean operator **AND**.
7. Under **Edit settings** section, enter the group email address and select **Next**.
8. Under **Review and finish adding group** section, verify all the details, select **Create group** and then select **Close**.

# [With Exchange Online PowerShell](#tab/create-powershell)
Tip

Before creating a DDG, you can preview which recipients match a custom recipient filter by using Exchange Online PowerShell. See Preview dynamic distribution group membership.

You can use Exchange Online PowerShell to create a DDG with **custom recipient filters**.

Filter and condition settings for DDGs that have custom recipient filters can be managed only by using Exchange Online PowerShell.

To create DDGs using Exchange Online PowerShell, execute the commands as shown in the following examples:

**Example 1**

This example shows how to create a DDG named "Mailbox Users DDG" that contains only mailbox users.

```powershell
New-DynamicDistributionGroup -IncludedRecipients MailboxUsers -Name "Mailbox Users DDG" -OrganizationalUnit Users
```

**Example 2**

This example shows how to create a DDG with a pre-canned filter. The DDG contains all mailbox users and contact recipients who have a **Department** field that equals the strings "Marketing" or "Sales".

```powershell
New-DynamicDistributionGroup -Name "Marketing Group" -IncludedRecipients "MailboxUsers,MailContacts" -ConditionalDepartment "Marketing","Sales"
```

**Example 3**

This example shows how to create a DDG with a custom recipient filter. The DDG contains all mailbox users that have a value of "FullTimeEmployee" in the **CustomAttribute10** property.

```powershell
New-DynamicDistributionGroup -Name "Full Time Employees" -RecipientFilter "(RecipientTypeDetails -eq 'UserMailbox') -and (CustomAttribute10 -eq 'FullTimeEmployee')"
```

For detailed syntax and parameter information, see [New-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/new-dynamicdistributiongroup). For more information about the filterable properties you can use with the **RecipientFilter** parameter, see [Filterable properties for the RecipientFilter parameter](/en-us/powershell/exchange/recipientfilter-properties?view=exchange-ps&amp;preserve-view=true).

---

### How do you know this worked?

To verify that you've successfully created a DDG, perform one of the following steps:

- In the EAC, select **Recipients** &gt; **Groups** &gt; **Dynamic distribution list**. The new DDG is displayed in the group list.
- In Exchange Online PowerShell, run the following command to display information about the new DDG, replacing **DDGIdentity** with the name, alias, or email address of the DDG.

    ```powershell
    Get-DynamicDistributionGroup -Identity <DDGIdentity>
    ```

After creating the DDG:

- For details on when the membership list becomes available, see Dynamic distribution group membership lifecycle.
- To preview the filter results before the membership list is populated, see Preview dynamic distribution group membership.
- To verify the membership list after it becomes available, see View members of a DDG.

## Change dynamic distribution group properties

Note

For details on when the new membership list becomes available after a change to the membership rules, see Dynamic distribution group membership lifecycle.

You can change the group properties, including the membership rules used to calculate the group's membership list, by performing the following steps:

# [With EAC](#tab/create-new-eac-2)
1. In the EAC, select **Recipients** &gt; **Groups** &gt; **Dynamic distribution list**.
2. In the list of groups, select the DDG that you want to view or change.
3. On the group's properties page, select one of the following sections to view or change properties:

    - General
    - Members
    - Settings

#### General

Use this section to view or change:

- The following properties of the group under **Basic information** section:

    - **Name**: This name appears in the address book, on the To: line when an email is sent to this group, and in the Groups list. The display name is required and should be user-friendly so that people recognize what it is. It also has to be unique in your domain.
    - **Description**: Use this option to describe the group so that people know what the purpose of the group is. This description appears in the address book and in the **Details** pane in the EAC.
- Under **Email addresses** section, you can view or change the email addresses associated with the group. These addresses include the group's primary SMTP addresses and any associated proxy addresses. Select **Edit** to change/edit the **Primary email address** and to add/delete **Aliases**, and then select **Save changes**.

    - You can also select the group and then select **Edit email addresses** from the toolbar to change/edit the **Primary email address** and to add/delete **Aliases**, and then select **Save changes**.

#### Members

Use this section to change/edit the following:

- Use **Members** section to change the conditions used to determine membership of the group. You can change the types of recipients for the group, delete or change existing membership rules, and add new rules. For procedures that tell you how to manage membership rules, see [Create a dynamic distribution group](create-manage-dynamic-distribution-groups).

Note

You aren't able to make changes to DDG membership rules with custom recipient filters in EAC. Use Exchange Online PowerShell to change membership rules for groups with custom recipient filters.

- Under **Owners** section, select **View all and manage owners** to add/remove group owners from the drop-down list and then select **Save changes**.

#### Settings

Under **General settings** section, select the checkbox **Hide from my organization's global address list** if you want to hide the group from the list.

##### Delivery management

Use this section to manage who can send emails to this group.

- **Sender options**

    By default, only people inside your organization can send messages to this group. You can also allow people outside the organization to send messages to this group.

    - **Only allow messages from people inside my organization**: Select this option to allow only senders in your organization to send messages to the group. This option's activation means that if someone outside your organization sends an email message to this group, it's rejected. This setting is the default setting.
    - **Allow messages from people inside and outside my organization**: Select this option to allow anyone to send messages to the group.
- **Specified senders**

    You can further limit who can send messages to the group by allowing only specific senders to send messages to this group. Select/remove one or more recipients/groups from the drop-down list. If you add senders to this list, they're the only ones who can send emails to the group. Emails sent by anyone not in the list are rejected.

    Important

    If you've configured the group to allow only senders inside your organization to send messages to the group, emails sent from a mail contact are rejected, even if they're added to this list.

##### Manage delegates

Use this section to assign permissions to a user (called a delegate) to allow them to send messages as the group or send messages on behalf of the group. You can assign the following permissions:

- **Send as**: This permission allows the delegate to send messages as the group. After this permission is assigned, the delegate has the option to add the group to the **From** line to indicate that the message was sent by the group.
- **Send on behalf**: This permission also allows a delegate to send messages on behalf of the group. After this permission is assigned, the delegate has the option to add the group on the **From** line. The message will appear to be sent by the group and will say that it was sent by the delegate on behalf of the group.

To assign permissions to delegates in EAC, select **Edit manage delegates**, add the delegates, select the **Permission type** from the drop-down list, and select **Save changes**.

##### Message approval

Use this section to set options for moderating the group. Moderators approve or reject messages sent to the group before the messages reach the group members.

- **Require moderator approval for messages sent to this group**: This option is a checkbox and it's not selected by default. If you select this checkbox, incoming messages are reviewed by the group moderators before delivery. Group moderators can approve or reject incoming messages.
- **Group moderators**: To add/remove group moderators, search/add users from the drop-down list. If you've selected **Require moderator approval for messages sent to this group** and you don't select a moderator, messages to the group are sent to the group owners for approval.

Note

This option is valid only if you have checked the **Require moderator approval for messages sent to this group** checkbox.

- **Add senders who don't require message approval**: To add/remove users that can bypass moderation for this group, search/add users from the drop-down list.
- **Notify a sender if their message isn't approved:**: This option contains three sub-options, each of which has a radio button for you to select. These sub-options enable you to set how users are notified about message approval.

    - **Only sender**: This setting is the default setting. When this setting is enabled, a notification is sent to all senders, inside and outside your organization, when their message isn't approved.
    - **Only senders in your organization**: When you select this option, only users or groups in your organization are notified when a message that they sent to the group isn't approved by a moderator.
    - **No notifications**: When you select this option, notifications aren't sent to senders whose messages aren't approved by the group moderators.

# [With Exchange Online PowerShell](#tab/create-powershell-2)
Tip

Before changing a DDG's membership rules, you can preview which recipients match the new custom recipient filter by using Exchange Online PowerShell. See Preview dynamic distribution group membership.

Use the **Get-DynamicDistributionGroup** and **Set-DynamicDistributionGroup** cmdlets to view and change properties for DDGs. Advantages of using Exchange Online PowerShell are **(a)** the ability to change membership rules for groups with custom recipient filters, **(b)** the ability to change properties that aren't available in the EAC, and **(c)** the ability to change properties for multiple groups. For information about what parameters correspond to DDG properties, see the following articles:

- [Get-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/get-dynamicdistributiongroup?view=exchange-ps&amp;preserve-view=true)
- [Set-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/set-dynamicdistributiongroup?view=exchange-ps&amp;preserve-view=true)

Here are some examples of using Exchange Online PowerShell to change DDG properties:

**Example 1**:

```powershell
Get-DynamicDistributionGroup -ResultSize unlimited | Set-DynamicDistributionGroup -HiddenFromAddressListsEnabled $true -MaxReceiveSize 5MB -ModerationEnabled $true -ModeratedBy administrator
```

The preceding PowerShell command syntax is an example of a command that changes the following parameters for all DDGs in the organization:

- Hide all DDGs from the address book
- Set the maximum message size that can be sent to the group to 5 MB
- Enable moderation
- Assign the administrator as the group moderator

**Example 2**:

```powershell
Set-DynamicDistributionGroup -Identity "All Employees" -EmailAddresses SMTP:All.Employees@contoso.com, smtp:Seattle.Employees@contoso.com
```

The preceding PowerShell command syntax is an example of a command that adds the proxy SMTP email address, Seattle.Employees@contoso.com, to the "All Employees" group.

**Example 3**:

```powershell
Set-DynamicDistributionGroup -Identity "Full Time Employees" -RecipientFilter "(RecipientTypeDetails -eq 'UserMailbox') -and (CustomAttribute1 -eq 'FullTimeEmployee')"
```

The preceding PowerShell command syntax is an example of a command that changes the custom recipient filter of the "Full Time Employee" DDG so that it contains all mailbox users that have a value of **FullTimeEmployee** in the **CustomAttribute1** property.

---

#### How do you know this worked?

To verify that you've successfully changed properties for a DDG:

- In EAC, select the group to view the property or feature that you changed. Depending on the property or feature that you changed, it might be displayed in the **Details** pane for the selected group.
- With Exchange Online PowerShell, use the **Get-DynamicDistributionGroup** cmdlet to verify the changes. One advantage of using Exchange Online PowerShell is that you can view multiple properties for multiple groups. Run the following command to verify the new values:

```powershell
Get-DynamicDistributionGroup -ResultSize Unlimited | Format-List Name,HiddenFromAddressListsEnabled,MaxReceiveSize,ModerationEnabled,ModeratedBy
```

If you changed the membership rules of the DDG:

- For details on when the new membership list becomes available, see Dynamic distribution group membership lifecycle.
- To preview the filter results before the membership list is recalculated, see Preview dynamic distribution group membership.
- To verify that the new membership list was calculated correctly, see View members of a dynamic distribution group.

## View members of a dynamic distribution group

You can view the members of a dynamic distribution group (DDG) by using EAC or Exchange Online PowerShell.

# [In EAC](#tab/create-new-eac-3)
To view the members of a DDG in EAC, perform the following steps after signing in to EAC:

1. Select **Recipients &gt; Groups &gt; Dynamic distribution list**.
2. Select the desired group from the group list.
3. Navigate to the **Members** tab.
4. Under the **Members** section, select **View all members**. On the resultant page, you can also search for members using the **Search members list** field.

[![Screenshot that shows the page on which you can view the members of a DDG.](../../exchangeonline/media/view-members-of-ddg.png)](../../exchangeonline/media/view-members-of-ddg.png#lightbox)

# [In Exchange Online PowerShell](#tab/create-powershell-3)
To view the members of a DDG using Exchange Online PowerShell, use the **Get-DynamicDistributionGroupMember** command. Replace `<DDGIdentity>` with the name, alias, or email address of the DDG and run the following command in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps&amp;preserve-view=true):

```powershell
Get-DynamicDistributionGroupMember -Identity <DDGIdentity>
```

For detailed parameter and syntax information, see [Get-DynamicDistributionGroupMember](/en-us/powershell/module/exchangepowershell/get-dynamicdistributiongroupmember?view=exchange-ps&amp;preserve-view=true).

---

## Preview dynamic distribution group membership

You can preview which recipients match a DDG's membership rules. This capability is useful for:

- Validating a custom filter before applying it to a DDG
- Previewing the future members of a newly created or recently modified DDG while the background process populates the membership list
- Testing changes to a custom filter before committing them

Previewing DDG membership is available only in Exchange Online PowerShell. You can't preview DDG membership in the Exchange admin center (EAC).

To preview the recipients that match a custom filter, run the following command in Exchange Online PowerShell:

```powershell
Get-Recipient -RecipientPreviewFilter "(RecipientTypeDetails -eq 'UserMailbox') -and (CustomAttribute1 -eq 'FullTimeEmployee')" -ResultSize 100
```

To preview the members of an existing DDG, run the following command in Exchange Online PowerShell, where `<DDGIdentity>` is the name, alias, or email address of the DDG:

```powershell
# Get existing DDG
$ddg = Get-DynamicDistributionGroup -Identity <DDGIdentity>

# Preview members with the DDG's filter
Get-Recipient -RecipientPreviewFilter $ddg.RecipientFilter -ResultSize 100
```

Adjust `-ResultSize` as needed. Preview results reflect the state of recipients at the time the command runs.

## Troubleshoot membership issues

If you find that the membership of your DDG doesn't match what you expect—for example, the group is empty, missing members, or includes members it shouldn't—see [Troubleshoot dynamic distribution group membership issues](troubleshoot-ddg-membership-issues#troubleshoot-dynamic-distribution-group-membership-issues) for diagnostic steps and remedies.