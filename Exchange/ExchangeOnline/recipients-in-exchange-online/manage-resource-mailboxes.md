---
layout: Conceptual
title: Manage resource mailboxes in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-resource-mailboxes
Manager: serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn how to create and modify resource mailboxes (room mailboxes and equipment mailboxes) in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: f70752ad-fce0-4e14-8428-fc5ac63f6c54
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2025-02-07T00:00:00.0000000Z
locale: en-us
document_id: aaf2b324-b835-5deb-346a-f1364a20becd
document_version_independent_id: 6e1a47a4-70f7-c8ca-4f1a-190d230b4707
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-resource-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-resource-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-resource-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 779d840e-ca21-df06-e1d5-4dd69d7a705a
---

# Manage resource mailboxes in Exchange Online | Microsoft Learn

Resource mailboxes are special mailboxes that users can include in meeting requests to easily reserve resources. Two types of resources mailboxes are available:

- **Room mailbox**: A resource assigned to a physical location, such as a conference room, an auditorium, or a training room.

    *Room lists* are special distribution groups that contain only room mailboxes. Room lists are useful in the following scenarios:

    - You have or plan to have more than 100 room mailboxes. Room lists help organize large numbers of room mailboxes.
    - Your organization has meeting rooms in multiple buildings. Room lists help organize meeting rooms by building.

    To create and manage room lists, see the Create room lists section later in this article.
- **Equipment mailbox**: A resource that's not location specific, such as a portable computer, projector, microphone, or a company car.

You can use the Exchange admin center (EAC) and Exchange Online PowerShell to manage room mailboxes and equipment mailboxes. You can create room lists only in Exchange Online PowerShell.

## What do you need to know before you begin?

- Estimated time to complete each procedure: less than 5 minutes.
- You must be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../permissions-exo/feature-permissions) article.
- For information about the EAC, see [Exchange admin center in Exchange Online](../exchange-admin-center). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- Don't use nested groups for group values in resource mailbox settings. Only non-nested groups work for group values in resource mailbox settings.
- Important

    If you're running Exchange Server in a hybrid scenario, ensure you create resource mailboxes in the appropriate location. Create room mailboxes for your on-premises organization in on-premises Exchange. Create room mailboxes for your Exchange Online organization in Exchange Online.
- For information about keyboard shortcuts that might apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to create resource mailboxes

Use the following steps to create room mailboxes and equipment mailboxes in the EAC.

1. In the Exchange admin center at https://admin.exchange.microsoft.com, go to **Recipients** &gt; **Resources**. Or, to go directly to the **Resources** page, use https://admin.cloud.microsoft/exchange#/resources.
2. On the **Resources** page, select one of the following actions:

    - ![](../exchangeonline/media/modern-eac-create-icon.png)**Add a room resource**.
    - ![](../exchangeonline/media/modern-eac-create-icon.png)**Add an equipment resource**.

    The new resource mailbox wizard that opens has the same options and steps for room mailboxes and equipment mailboxes.
3. On the **Set up room mailbox** or **Set up equipment mailbox** page, configure the following settings:

    - **Name**: Enter a unique and descriptive name.

        Tip

        Although other properties are available to describe the details of the resource (for example, **Location** and **Capacity**), consider summarizing the important details in the **Name** value using a consistent naming convention. Users can easily see the details in the resource name when they select the room mailbox or equipment mailbox from the address book.
    - **Resource mail address**: Enter a unique alias value on the left side of the @ symbol, and select an [accepted domain](../mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains) on the right side of the @ symbol.

    When you're finished on the **Resource setup** page, select **Next**.
4. On the **Set properties** page, configure any of the available optional settings:

    - **Capacity**
    - **Location**
    - **Phone number**
    - **Department**
    - **Company**
    - **Address book policy**: An address book policy (ABP) contains a global address list (GAL), an offline address book (OAB), a room list, and a set of address lists. For more information, see [Address book policies](../address-books/address-book-policies/address-book-policies).
    - **Street**
    - **City**
    - **State/Province**
    - **ZIP/Postal code**
    - **Country/Region**

    When you're finished on the **Set properties** page, select **Next**.
5. On the **Booking delegate settings** page, configure the following options:

    - **Booking options** section:

        - **Allow repeating meetings**: Allows or prevents repeating meetings for the resource. By default, this setting is selected, so repeating meetings are allowed.
        - **Allow scheduling only during working hours**: Accepts or declines meeting requests that aren't during the working hours defined for the resource. By default, this setting isn't selected, so meeting requests are allowed outside the working hours. By default, working hours are 8:00 A.M. to 5:00 P.M. Monday through Friday. You can set the working hours on a mailbox in the following locations:
            - Outlook on the web (formerly known as Outlook Web App or OWA) in **Settings** &gt; **Calendar** &gt; **Work hours and location**.
            - The *WorkDays*, *WorkingHoursEndTime*\_, *WorkingHoursStartTime*, and *WorkingHoursTimeZone* parameters on the **Set-MailboxCalendarConfiguration** cmdlet in Exchange Online PowerShell.
        - **Automatically decline meetings outside of booking limits below**: By default, this setting is selected and controls the behavior of meetings outside the values of the following settings:
            - **Booking window (days)**: Specifies the maximum number of days in advance that the resource can be booked. The default value is 180 days.
            - **Maximum duration (hours)**: Specifies the maximum amount of time that the resource can be reserved. The default value is 24 hours.
            - **Enter an automatic reply to be sent to meeting organizers (optional)**: Enter the text of the message sent to users who send booking requests to reserve the resource.
    - **Booking delegates** section: Select one of the following values:

        - **Automatically accept/decline meeting requests**: Meeting requests are automatically accepted or declined based on the settings in the **Booking options** section. By default, this setting is selected.
        - **Specify users whom you want to accept/decline meetings manually**: All meeting requests are sent to one or more delegates for approval. Find and select delegates in the **Choose your booking delegates** box that's available when you select this setting.

        Tip

        After you create the resource mailbox, you can grant delegates **Send as** or **Send on behalf** permission, and **Full access** permission to the mailbox. For more information, see the Delegation tab section later in this article.

        For examples of common booking and delegation scenarios using the **Set-CalenderProcessing** cmdlet in Exchange Online PowerShell, see the Appendix: Common booking and delegation scenarios section later in this article.

    When you're finished on the **Booking delegate settings** page, select **Next**.
6. On the **Review resource** page, review the settings. Use **Back** to return to a previous page, and use **Next** to return to the **Review resource** page.

    When you're finished on the **Review resource** page, select **Create**.
7. The **Status** page shows the creation progress.

    After the resource mailbox is successfully created, select **Done**.

    Back on the **Resources** page, the resource mailbox appears in the list.

Tip

Additional settings are available after you create the mailbox. For more information, see the Use the EAC to modify resource mailboxes section.

### Use Exchange Online PowerShell to create resource mailboxes

To use PowerShell to create a room mailbox or equipment mailbox, use the following syntax:

```powershell
New-Mailbox -Name <Name> <-Room | -Equipment> [-Alias <Alias>] [-DisplayName "<DisplayName>"] [-PrimarySmtpAddress <EmailAddress>]
```

This example creates a room mailbox with the following options:

- Name: ConfRoom1. This value is also used as the alias value in the email address because we aren't using the Alias parameter.
- DisplayName: Conference Room 1. This is the value that users see.

```powershell
New-Mailbox -Name ConfRoom1 -Room -DisplayName "Conference Room 1"
```

This example creates an equipment mailbox with the following options:

- Name: MotorVehicle2
- DisplayName: Motor Vehicle 2. This is the value that users see.
- EmailAddress: `mv2@contoso.com`.

```powershell
New-Mailbox -Name MotorVehicle2 -Equipment -DisplayName "Motor Vehicle 2" -PrimarySmtpAddress mv2@contoso.com
```

For detailed syntax and parameter information, see [New-Mailbox](/en-us/powershell/module/exchangepowershell/new-mailbox).

Tip

For examples of common booking and delegation scenarios using the **Set-CalenderProcessing** cmdlet in Exchange Online PowerShell, see the Appendix: Common booking and delegation scenarios section later in this article.

### How do you know you successfully created a resource mailbox?

To verify you successfully created a resource mailbox, use any of the following steps:

- On the **Resources** page in the EAC at https://admin.cloud.microsoft/exchange#/resources, verify the resource mailbox is listed.

    - Select ![](../exchangeonline/media/modern-eac-filter-icon.png)**Filter** &gt; **All rooms** or **All equipment** to filter the list.
    - Use the ![](../exchangeonline/media/modern-eac-search-icon.png)**Search** box to find resource mailboxes by **Display Name**.
- In Exchange Online PowerShell, replace &lt;MailboxIdentity&gt; with the Name, Alias, or Email address of the resource mailbox, and then run the following command to display information about the resource mailbox:

    ```powershell
    Get-Mailbox -Identity <MailboxIdentity> | Format-List Name,RecipientTypeDetails,PrimarySmtpAddress
    ```

## Use the EAC to modify resource mailboxes

Use the following steps to modify room mailboxes and equipment mailboxes in the EAC.

1. In the Exchange admin center at https://admin.exchange.microsoft.com, go to **Recipients** &gt; **Resources**. Or, to go directly to the **Resources** page, use https://admin.cloud.microsoft/exchange#/resources.
2. On the **Resources** page, select the room mailbox or equipment mailbox by clicking anywhere in the row other than the round check box next to the first column.
3. The details flyout that opens contains tabs with settings as described in the following subsections.

Tip

For examples of common booking and delegation scenarios using the **Set-CalenderProcessing** cmdlet in Exchange Online PowerShell, see the Appendix: Common booking and delegation scenarios section later in this article.

### General tab

The **General** tab in the details flyout of the resource mailbox contains the following information:

- Select **Manage resource details** to modify the following settings, which are also shown on the tab:

    - **Room name** or **Equipment name**
    - **Email address**
    - **Department**
    - **Capacity**
    - **Company**
    - **Address book policy**: An address book policy (ABP) contains a global address list (GAL), an offline address book (OAB), a room list, and a set of address lists. For more information, see [Address book policies](../address-books/address-book-policies/address-book-policies).
- Room mailboxes have the **Additional information** link where you can configure the following settings that aren't available when you create the room mailbox:

    - **Wheel chair accessible**
    - **Tags**
    - **Audio device name**
    - **Display device name**
    - **Video device name**
- Select **Manage resource contact information** in the **Resource contact information** section to configure the following settings:

    - **Location**
    - **Phone number**
    - **Street**
    - **City**
    - **State/Province**
    - **ZIP/Postal code**
    - **Country/Region**
    - **Notes**
- Select **Manage hide from GAL** in the **Hide from global address list (GAL)** section to turn on or turn off **Hide from global address list**.

    Tip

    If you hide the resource mailbox in the GAL, users can still send booking messages to it by using the email address.

### Booking tab

The **Booking** tab in the details flyout of the resource mailbox contains the same settings as when you created the mailbox:

- Select **Manage delegate settings** in the **Booking delegate settings** section to configure the following options:

    Select one of the following values:

    - **Accept or decline booking requests automatically**: A valid meeting request automatically reserves the resource. The resource automatically declines the meeting request in the following scenarios:
        - A scheduling conflict with an existing reservation.
        - A request that violates the scheduling limits of the resource (for example, the meeting is too long or the meeting is too far in advance).
    - **Select delegates who can accept or decline booking requests**: Resource delegates are responsible for accepting or declining all meeting requests sent to the resource mailbox. If you assign more than one resource delegate, only one of them has to act on a specific meeting request. Find and select delegates in the **Select delegates** box that's available when you select this setting.
- Select **Manage booking settings** in the **Booking options settings** section to configure the following options:

    - **Allow repeating meetings**: Allows or prevents repeating meetings for the resource. By default, this setting is selected, so repeating meetings are allowed.
    - **Allow scheduling only during working hours**: Accepts or declines meeting requests that aren't during the working hours defined for the resource. By default, this setting isn't selected, so meeting requests are allowed outside the working hours. By default, working hours are 8:00 A.M. to 5:00 P.M. Monday through Friday. You can set the working hours on a mailbox in the following locations:
        - Outlook on the web (formerly known as Outlook Web App or OWA) in **Settings** &gt; **Calendar** &gt; **Work hours and location**.
        - The *WorkDays*, *WorkingHoursEndTime*\_, *WorkingHoursStartTime*, and *WorkingHoursTimeZone* parameters on the **Set-MailboxCalendarConfiguration** cmdlet in Exchange Online PowerShell.
    - **Automatically decline meetings outside this limit**: By default, this setting is selected and controls the behavior of meetings outside the values of the following settings:
        - **Booking window (days)**: Specifies the maximum number of days in advance that the resource can be booked. The default value is 180 days.
        - **Maximum duration (hours)**: Specifies the maximum amount of time that the resource can be reserved. The default value is 24 hours.
        - **If you want the meeting organizer to receive a reply, enter the text below**: Enter the text of the message sent to users who send booking requests to reserve the resource.

### Delegation tab

The **Delegation** tab in the details flyout of the resource mailbox contains settings that aren't available when you create the mailbox:

- **Send as (n)**: Select **Edit** to manage users who can send messages that appear to come from this mailbox.
- **Send on behalf (n)**: Select **Edit** to manage users who can send messages that are clearly identified as sent by the user on behalf of the mailbox.
- **Read and manage (Full Access) (n)**: Select **Edit** to manage users who have full access to the mailbox.

For complete instructions, see [Manage permissions for recipients in Exchange Online](manage-permissions-for-recipients).

### Others tab

The **Others** tab in the details flyout of the resource mailbox contains the following settings:

- Select **Manage MailTip** in the **MailTip** section to configure a MailTip for the resource mailbox. For more information, see [MailTips in Exchange Online](../clients-and-mobile-in-exchange-online/mailtips/mailtips).

    Tip

    MailTips can include HTML tags, but scripts aren't allowed. The length of a custom MailTip can't exceed 175 displayed characters. HTML tags aren't counted in the limit.
- Select **Manage email addresses** in the **Email address** section to edit the primary email address and/or remove additional email addresses for the mailbox (also known as *proxy addresses*). For more information, see [Add or remove email addresses for a mailbox in Exchange Online](manage-user-mailboxes/add-or-remove-email-addresses).
- Select **Manage custom attributes** in the **Custom attributes** section to configure values for the **Custom Attribute 1** to **Custom Attribute 15** properties on the mailbox.

### Use Exchange Online PowerShell to modify resource mailboxes

Use the following cmdlets to view and modify room mailboxes and equipment mailboxes in Exchange Online PowerShell:

- **Get-User** and **Set-User**: View and set general properties such as location, department, and company names. For more information, see [Get-User](/en-us/powershell/module/exchangepowershell/get-user) and [Set-User](/en-us/powershell/module/exchangepowershell/set-user).
- **Get-Mailbox** and **Set-Mailbox**: View and set mailbox properties, such as email addresses. For more information, see [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox) and [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).
- **Get-CalendarProcessing** and **Set-CalendarProcessing**: View and set booking options and delegates. For more information, see [Get-CalendarProcessing](/en-us/powershell/module/exchangepowershell/get-calendarprocessing) and [Set-CalendarProcessing](/en-us/powershell/module/exchangepowershell/set-calendarprocessing).
- **Get-MailboxFolderPermission** and **Set-MailboxFolderPermission**: View and modify delegate permissions on the Calendar folder of the resource mailbox. For more information, see [Get-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/get-mailboxfolderpermission) and [Set-MailboxFolderPermission](/en-us/powershell/module/exchangepowershell/set-mailboxfolderpermission).

Tip

For examples of common booking and delegation scenarios using the **Set-CalenderProcessing** cmdlet in Exchange Online PowerShell, see the Appendix: Common booking and delegation scenarios section later in this article.

Here are some examples of using Exchange Online PowerShell to modify resource mailboxes:

- This example changes the display name, the primary SMTP address (called the default reply address), and the room capacity. Also, the previous reply address is kept as a proxy address.

    ```powershell
    Set-Mailbox "Conf Room 123" -DisplayName "Conf Room 31/123 (12)" -EmailAddresses SMTP:Rm33.123@contoso.com,smtp:rm123@contoso.com -ResourceCapacity 12
    ```
- This example configures room mailboxes to allow booking requests to be scheduled only during working hours and sets a maximum duration of 9 hours.

    ```powershell
    Get-Mailbox -ResultSize unlimited -Filter "RecipientTypeDetails -eq 'RoomMailbox'" | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true -MaximumDurationInMinutes 540
    ```
- This example modifies room mailboxes:

    - The **Get-User** cmdlet finds all room mailboxes that correspond to private conference rooms.
    - The **Set-CalendarProcessing** cmdlet sends booking requests to a delegate named Robin Wood to accept or decline.
    - The **Set-MailboxFolderPermission** cmdlet gives Robin the required Calendar folder permissions to the private conference room mailboxes.

    ```powershell
    $P = Get-User -ResultSize unlimited -Filter "(RecipientTypeDetails -eq 'RoomMailbox') -and (DisplayName -like 'Private*')"
    
    $P | foreach {Set-CalendarProcessing -Identity $_.Identity -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Robin Wood"}
    
    $P | foreach {Set-MailboxFolderPermission -Identity "$_`:\Calendar" -User "Robin Wood" -AccessRights Editor -SharingPermissionFlags Delegate}
    ```
- This example modifies equipment mailboxes:

    - The **Get-User** cmdlet finds all equipment mailboxes in the Audio Visual department.
    - The **Set-CalendarProcessing** cmdlet sends booking requests to a delegate named Ann Beebe to accept or decline.
    - The **Set-MailboxFolderPermission** cmdlet gives Ann the required Calendar folder permissions to the equipment mailboxes.

    ```powershell
    $AV = Get-User -ResultSize unlimited -Filter "(RecipientTypeDetails -eq 'EquipmentMailbox') -and (Department -eq 'Audio Visual')"
    
    $AV | foreach {Set-CalendarProcessing -Identity $_.Identity -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Ann Beebe"}
    
    $AV | foreach {Set-MailboxFolderPermission -Identity "$_`:\Calendar" -User "Ann Beebe" -AccessRights Editor -SharingPermissionFlags Delegate}
    ```

### How do you know you successfully modified a resource mailbox?

To verify you successfully modified a resource mailbox, use any of the following steps:

- On the **Resources** page in the EAC at https://admin.cloud.microsoft/exchange#/resources, find and select the resource mailbox:

    - Select ![](../exchangeonline/media/modern-eac-filter-icon.png)**Filter** &gt; **All rooms** or **All equipment** to filter the list.
    - Use the ![](../exchangeonline/media/modern-eac-search-icon.png)**Search** box to find resource mailboxes by **Display Name**.

    In the details flout, verify the value of the feature or property you changed.
- In Exchange Online PowerShell, replace &lt;MailboxIdentity&gt; with the Name, Alias, or Email address of the resource mailbox, and then run the following command to display information about the resource mailbox:

    ```powershell
    Get-Mailbox -Identity <MailboxIdentity> | Format-List
    ```

    An advantage of using PowerShell is you can view multiple properties on multiple mailboxes. For example, run the following commands to see the ScheduleOnlyDuringWorkHours and MaximumDurationInMinutes property values for all room mailboxes:

    ```powershell
    $R = Get-User -ResultSize unlimited -Filter "RecipientTypeDetails -eq 'RoomMailbox'"
    
    $R | foreach {Get-CalendarProcessing -Identity $_.Identity | Format-List Identity,ScheduleOnlyDuringWorkHours,MaximumDurationInMinutes}
    ```

## Use the EAC to remove resource mailboxes

Use the following steps to remove room mailboxes and equipment mailboxes in the EAC.

1. In the Exchange admin center at https://admin.exchange.microsoft.com, go to **Recipients** &gt; **Resources**. Or, to go directly to the **Resources** page, use https://admin.cloud.microsoft/exchange#/resources.
2. On the **Resources** page, do either of the following steps:

    - Select the room mailbox or equipment mailbox by clicking anywhere in the row other than the round check box next to the first column. In the details flyout that opens, select ![](../exchangeonline/media/modern-eac-create-icon.png)**Delete resource** at the top of the flyout.
    - Select one or more room mailboxes or equipment mailboxes by selecting the round check box next to the first column, and then select ![](../exchangeonline/media/modern-eac-create-icon.png)**Delete**.
3. In the confirmation flyout that opens, select **Confirm**.

    After the room mailbox or equipment mailbox is successfully deleted, select **Close**.

Back on the **Resources** page, the resource mailbox is no longer listed.

### Use Exchange Online PowerShell to remove resource mailboxes

To use PowerShell to remove a room mailbox or equipment mailbox, use the following syntax:

```powershell
Remove-Mailbox -Identity <MailboxIdentity>
```

This example removes the specified resource mailbox:

- Name: ConfRoom1. This value is also used as the alias value in the email address because we aren't using the Alias parameter.
- DisplayName: Conference Room 1. This is the value that users see.

```powershell
Remove-Mailbox -Identity "Conference Room 99"
```

For detailed syntax and parameter information, see [Remove-Mailbox](/en-us/powershell/module/exchangepowershell/remove-mailbox).

### How do you know you successfully removed a resource mailbox?

To verify you successfully removed a resource mailbox, use any of the following steps:

- On the **Resources** page in the EAC at https://admin.cloud.microsoft/exchange#/resources, verify the resource mailbox isn't listed.
- In Exchange Online PowerShell, run the following command to verify the resource mailbox doesn't exist:

    ```powershell
    Get-Mailbox -ResultSize Unlimited -RecipientTypeDetails EquipmentMailbox,RoomMailbox
    ```
- In Exchange Online PowerShell, replace &lt;MailboxIdentity&gt; with the Name, Alias, or Email address of the resource mailbox, and then run the following command to verify the resource mailbox doesn't exist:

    ```powershell
    Get-Mailbox -Identity <MailboxIdentity>
    ```

## Create room lists

*Room lists* are special distribution groups that contain only room mailboxes. Room mailboxes are useful for organizing conference rooms by building.

### Use Exchange Online PowerShell to create a room list

Tip

You can create room lists in Exchange Online PowerShell only. You can't create room lists in the EAC.

To create a room list, use the following syntax:

```powershell
New-DistributionGroup -Name <Name> -RoomList [-Alias <Alias>] [-DisplayName "<DisplayName>"] [-PrimarySmtpAddress <EmailAddress>]
```

This example creates a room list with the Name value Building 32 Conference Rooms. Because we aren't using the Alias, DisplayName, or PrimarySmtpAddress parameters, the Name value results in the following default values for those parameters:

- DisplayName: Building 32 Conference Rooms.
- Alias: Building32ConferenceRooms
- PrimarySmtpAddress: `Building32ConferenceRooms@Mcontoso.com`

```powershell
New-DistributionGroup -Name "Building 32 Conference Rooms" -RoomList
```

For detailed syntax and parameter information, see [New-DistributionGroup](/en-us/powershell/module/exchangepowershell/new-distributiongroup).

### Use Exchange Online PowerShell to add rooms to room lists

Tip

You can add room mailboxes to room lists in the EAC or in PowerShell. For EAC instructions, see [Use the EAC to modify distribution groups](manage-distribution-groups/manage-distribution-groups#use-the-eac-to-modify-distribution-list-groups).

To add room mailboxes to a room list, use the following syntax:

```powershell
Add-DistributionGroupMember -Identity <RoomListIdentity> -Member <RoomMailboxIdentity>
```

This example adds conference room 3223 to the building 32 room list.

```powershell
Add-DistributionGroupMember -Identity "Building 32 Conference Rooms" -Member confroom3223@contoso.com
```

For detailed syntax and parameter information, see [Add-DistributionGroupMember](/en-us/powershell/module/exchangepowershell/add-distributiongroupmember).

### Use Exchange Online PowerShell to convert a distribution group to a room list

Tip

You can convert distribution groups to room lists in Exchange Online PowerShell only. You can't convert distribution groups to room lists in the EAC.

If you previously created regular distribution groups that contain room mailboxes, you can convert them to room lists by using the following syntax:

```powershell
Set-DistributionGroup -Identity <GroupIdentity> -RoomList
```

This example converts the specified distribution group to a room list.

```powershell
Set-DistributionGroup -Identity "Building 34 Conference Rooms" -RoomList
```

For detailed syntax and parameter information, see [Set-DistributionGroup](/en-us/powershell/module/exchangepowershell/set-distributiongroup).

### How do you know you successfully created, updated, or converted a room list?

To verify you successfully created, updated, or converted a room list, do any of the following steps:

- In Exchange Online PowerShell, run the following commands to return all room lists and their members:

    ```powershell
    $RL = Get-DistributionGroup -ResultSize Unlimited -RecipientTypeDetails RoomList
    
    $RL | foreach {Get-DistributionGroup -Identity $_.Identity | Format-Table Name,DisplayName,PrimarySmtpAddress; Get-DistributionGroupMember -Identity $_.Identity}
    ```
- In Exchange Online PowerShell, replace &lt;RoomListIdentity&gt; with the Name, Alias, or Email address of the room list, and then run the following commands to verify the details of the room list and the room list members:

    ```powershell
    Get-DistributionGroup -Identity <RoomListIdentity> | Format-List
    
    Get-DistributionGroupMember -Identity <RoomListIdentity>
    ```

## Appendix: Common booking and delegation scenarios

This section describes common booking and delegation scenarios for resource mailboxes, and the required settings to achieve them using the **Set-CalendarProcessing** cmdlet:

- **Default Booking**: By default, anyone can book resources. The bookings are automatically accepted if the resource is available.
    - *AutomateProcessing*: `AutoAccept`
    - *AllBookInPolicy*: True
- **Delegate Approval**: Users can request meetings, but a delegate needs to approve the requests.
    - *AutomateProcessing*: `AutoAccept`
    - *ForwardRequestsToDelegates*: True
    - *AllBookInPolicy*: False
    - *AllRequestInPolicy*: True
    - ResourceDelegates: {users or groups}
- **Scoped Auto-Approval**: Specified users are auto-approved when booking the resource. Other users can't book the resource (the request is automatically denied).
    - *AutomateProcessing*: `AutoAccept`
    - *ForwardRequestsToDelegates*: False
    - *AllBookInPolicy*: False
    - *AllRequestInPolicy*: False
    - *BookInPolicy*: {users or groups}

Note

Don't use nested groups for group values in resource mailbox settings. Only non-nested groups work for group values in resource mailbox settings.