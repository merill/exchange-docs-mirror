---
layout: Conceptual
title: Manage address lists in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-lists/manage-address-lists
Manager: serdars
ms.subservice: exo-address-books
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Admins can learn how to create, view the membership of, update, modify, remove, and hide recipients from address lists in Exchange Online.
ms.topic: how-to
author: Srividyavaranasi
ms.author: srvar
ms.assetid: cac74760-7bd1-482c-8d43-b0165e988ec0
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2026-10-26T00:00:00.0000000Z
locale: en-us
document_id: b19aca72-9b59-60a2-e8d5-45553b636975
document_version_independent_id: a2348dfb-013a-69d7-3e87-af7899569296
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-lists/manage-address-lists.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-lists/manage-address-lists
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-lists/manage-address-lists.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: 2bf5f41f-154c-c145-c419-edb255a793a6
---

# Manage address lists in Exchange Online | Microsoft Learn

An address list is a collection of mail-enabled recipient objects in Exchange Online. Address lists are based on recipient filters. For more information about address lists, see [Address lists in Exchange Online](address-lists).

Looking for the Exchange Server version of this article? See [Create address lists](../../email-addresses-and-address-books/address-lists/address-list-procedures#create-address-lists).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- You can only use Exchange Online PowerShell to perform virtually all of the procedures in this article (everything except hiding recipients from address lists). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to create address lists

You create an address list by using either a precanned recipient filter or a custom recipient filter. For details about recipient filters, see [Recipient filters for address lists in Exchange Online PowerShell](use-recipient-filters-to-create-an-address-list).

To create an address list, use the following syntax:

```powershell
New-AddressList -Name "<Address List Name>" [-Container <ExistingAddressListPath>] [<Precanned recipient filter | Custom recipient filter>] [-RecipientContainer <OrganizationalUnit>]
```

This example creates an address list with a precanned recipient filter:

- **Name**: Southeast Offices
- **Location**: Under the root (`\`, also known as All Address Lists) because we didn't use the *Container* parameter, and the default value is `\`.
- **Precanned recipient filter**: All users with mailboxes where the **State or province** value is GA, AL, or LA (Georgia, Alabama, or Louisiana).

```powershell
New-AddressList -Name "Southeast Offices" -IncludedRecipients MailboxUsers -ConditionalStateorProvince "GA","AL","LA"
```

This example creates an address list with a custom recipient filter:

- **Name**: Northwest Executives
- **Location**: Under the existing address list named North America.
- **Custom recipient filter**: All users with mailboxes where the **Title** value contains Director or Manager, and the **State or province** value is WA, OR, or ID (Washington, Oregon, or Idaho).

```powershell
New-AddressList -Name "Northwest Executives" -Container "\North America" -RecipientFilter "(RecipientType -eq 'UserMailbox') -and (Title -like '*Director*' -or Title -like '*Manager*') -and (StateOrProvince -eq 'WA' -or StateOrProvince -eq 'OR' -or StateOrProvince -eq 'ID')"
```

For detailed syntax and parameter information, see [New-AddressList](/en-us/powershell/module/exchangepowershell/new-addresslist).

This example creates the address list named Oregon and Washington Users by using the *RecipientFilter* parameter and includes recipients that are mailbox users and have **StateOrProvince** set to `Washington` or `Oregon`.

```powershell
New-AddressList -Name "Oregon and Washington" -RecipientFilter "((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))"
```

This example creates the child address list Building 34 Meeting Rooms in the All Rooms parent container, using built-in conditions.

```powershell
New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"
```

For detailed syntax and parameter information, see [New-AddressList](/en-us/powershell/module/exchangepowershell/new-addresslist).

### How do you know you successfully created an address list?

To verify you successfully created an address list, replace *&lt;AddressListIdentity&gt;* with the path\name of the address list, and run the following command in Exchange Online PowerShell to verify the property values:

```powershell
Get-AddressList -Identity "<AddressListIdentity>" | Format-List Name,RecipientFilterType,RecipientFilter,IncludedRecipients,Conditional*
```

## Use Exchange Online PowerShell to view members of address lists

Technically, this procedure returns *all* recipients (including hidden recipients) that match the recipient filters for the address list. The recipients that are visible in the address list have the **HiddenFromAddressListsEnabled** property value `False`.

To view the members of an address list, use the following syntax:

```powershell
$<VariableName> = Get-AddressList -Identity <AddressListIdentity>

Get-Recipient -ResultSize unlimited -RecipientPreviewFilter $<VariableName>.RecipientFilter | select Name,PrimarySmtpAddress,HiddenFromAddressListsEnabled
```

This example returns the members of the address list named Southeast Offices.

```powershell
$AL = Get-AddressList -Identity "Southeast Offices"

Get-Recipient -ResultSize unlimited -RecipientPreviewFilter $AL.RecipientFilter | select Name,PrimarySmtpAddress,HiddenFromAddressListsEnabled
```

This example exports the results to the file C:\My Documents\Southeast Offices Export.csv.

```powershell
$AL = Get-AddressList -Identity "Southeast Offices"

Get-Recipient -ResultSize unlimited -RecipientPreviewFilter $AL.RecipientFilter | select Name,PrimarySmtpAddress,HiddenFromAddressListsEnabled | Export-Csv -NoTypeInformation -Path "C:\My Documents\Southeast Offices Export.csv"
```

## Use Exchange Online PowerShell to update address lists

The **Update-AddressList** cmdlet (or **Update-GlobalAddressList**) isn't available in Exchange Online PowerShell. If recipients don't appear in an address list where they should appear, change the required property value for those users to a temporary value, and then back to the value required by the address list. You can update the user property values in the Exchange admin center (EAC) or Exchange Online PowerShell, but it's quicker to do bulk operations in PowerShell.

For example, suppose the address list named Oregon and Washington Users uses the filter `"((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))"`, but the address list doesn't include everyone whose **StateOrProvince** property values are set correctly. To update the address list, perform the following steps:

1. Use the query from the address list to find all users that should be in the address list. For example:

    ```powershell
    $Before = Get-User -Filter "((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Oregon') -or (StateOrProvince -eq 'Washington')))" -ResultSize Unlimited
    ```
2. Change the required property to a temporary value. For example, change the **StateOrProvince** values from `Oregon` to `OR`, and `Washington` to `WA`:

    ```powershell
    $Before | where {$_.StateOrProvince -eq 'Oregon'} | foreach {Set-User $_.Identity -StateOrProvince OR}
    ```

    ```powershell
    $Before | where {$_.StateOrProvince -eq 'Washington'} | foreach {Set-User $_.Identity -StateOrProvince WA}
    ```
3. Find those same users again by using the temporary property values. For example:

    ```powershell
    $After = Get-User -Filter "((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'OR') -or (StateOrProvince -eq 'WA')))" -ResultSize Unlimited
    ```
4. Change the temporary value back to the required value. For example, change the **StateOrProvince** values from `OR` to `Oregon`, and `WA` to `Washington`:

    ```powershell
    $After | where {$_.StateOrProvince -eq 'OR'} | foreach {Set-User $_.Identity -StateOrProvince Oregon}
    ```

    ```powershell
    $After | where {$_.StateOrProvince -eq 'WA'} | foreach {Set-User $_.Identity -StateOrProvince Washington}
    ```

Note

- Title, department, and address properties require the **Get-User** and **Set-User** cmdlets. CustomAttribute1 through CustomAttribute15 properties require the **Get-Mailbox** and **Set-Mailbox** cmdlets. For more information about what properties are available on which cmdlet, see the following articles:

    - [Set-User](/en-us/powershell/module/exchangepowershell/set-user)
    - [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox)
- If only small number of users don't appear in the address list, you can modify the required property value for each user. For example:

    1. Set a temporary property value for the user: 

        ```powershell
         Set-User -Identity <UserIdentity> -StateOrProvince WA
        ```
    2. Change the temporary value back to the required value: 

        ```powershell
         Set-User -Identity <Identity> -StateOrProvince Washington
        ```

### How do you know you successfully updated an address list?

To verify you successfully updated an address list, replace *&lt;AddressListIdentity&gt;* with the name of the address list, and run the following command in Exchange Online PowerShell to verify the **RecipientFilterApplied** property value:

```powershell
Get-AddressList -Identity <AddressListIdentity> | Format-Table Name,RecipientFilterApplied -Auto
```

## Use Exchange Online PowerShell to modify address lists

The same basic settings are available as when you created the address list. For more information, see the Use Exchange Online PowerShell to create address lists section in this article.

To modify an existing address list, use the following syntax:

```powershell
Set-AddressList -Identity <AddressListIdentity> [-Name <Name>] [<Precanned recipient filter | Custom recipient filter>] [-RecipientContainer <OrganizationalUnit>]
```

When you modify the *Conditional* parameter values, you can use the following syntax to add or remove values without affecting other existing values: `@{Add="<Value1>","<Value2>"...; Remove="<Value1>","<Value2>"...}`.

This example modifies the existing address list named Southeast Offices by adding the **State or province** value TX (Texas) to the precanned recipient filter.

```powershell
Set-AddressList -Identity "Southeast Offices" -ConditionalStateOrProvince @{Add="TX"}
```

For detailed syntax and parameter information, see [Set-AddressList](/en-us/powershell/module/exchangepowershell/set-addresslist).

### How do you know you successfully modified an address list?

To verify you successfully modified an address list, replace *&lt;AddressListIdentity&gt;* with the path\name of the address list, and run the following command in Exchange Online PowerShell to verify the property values:

```powershell
Get-AddressList -Identity "<AddressListIdentity>" | Format-List Name,RecipientFilterType,RecipientFilter,IncludedRecipients,Conditional*
```

## Use Exchange Online PowerShell to delete address lists

To remove an address list, use the following syntax:

```powershell
Remove-AddressList -Identity "<AddressListName>"
```

This example removes the address list Sales Department, which doesn't contain child address lists.

```powershell
Remove-AddressList -Identity "Sales Department"
```

For detailed syntax and parameter information, see [Remove-AddressList](/en-us/powershell/module/exchangepowershell/remove-addresslist).

### How do you know you successfully deleted an address list?

To verify you successfully removed an address list, run the following command in Exchange Online PowerShell to verify that the address list isn't listed:

```powershell
Get-AddressList
```

## Hide recipients from address lists

Hiding a recipient from address lists doesn't prevent the recipient from receiving email messages; it prevents users from finding the recipient in address lists. The recipient is hidden from **all** address lists and GALs (effectively, they're exceptions to the recipient filters in all address lists). If you want to selectively include the recipient in some address lists but not others, you need to adjust the recipient filters in the address lists to include or exclude the recipient.

Hiding a recipient from address lists can also prevent users from being found through an address book search. For example, [Auto Attendant service voice recognition](/en-us/microsoftteams/dial-voice-reference) can't find and redirect calls to the recipient.

### Use the EAC to hide recipients from address lists

For more information about the EAC, see [Exchange admin center in Exchange Online](../../exchange-admin-center).

1. In the EAC at https://admin.exchange.microsoft.com, go to one of the following locations based on the recipient type:

    - **Recipients** &gt; **Mailboxes**: User mailboxes.
    - **Recipients** &gt; **Groups**: One of the following tabs:
        - **Microsoft 365** (Microsoft 365 Groups)
        - **Distribution list** (distribution groups)
        - **Dynamic distribution list** (dynamic distribution groups)
        - **Mail-enabled security** (mail-enabled security groups)
    - **Recipients** &gt; **Resources**: Room and equipment mailboxes.
    - **Recipients** &gt; **Contacts**: Mail users and mail contacts.
    - **Public folders** &gt; **Public folders** tab: Mail-enabled public folders.
2. Select the recipient that you want to hide from address lists.
3. In the recipient details flyout that opens, what you do next depends on the recipient type:

    - **User mailboxes**: On the **General** tab, select **Manage hide from GAL** in the **Hide from global address list (GAL)** section. In the **Hide from address list** flyout that opens, slide the toggle to **On**, and then select **Save**.
    - **Groups**: On the **Settings** tab, select **Hide this group from the global address list**.
    - **Resource mailboxes**: On the **General** tab, select **Manage hide from GAL** in the **Hide from global address list (GAL)** section. In the **Manage hide from global address list (GAL)** flyout that opens, slide the toggle to **On**, and then select **Save**.
    - **Mail contacts and mail users**: On the **General** tab, select **Manage hide from GAL** in the **Hide from global address list (GAL)** section. In the **Manage hide from global address list (GAL)** flyout that opens, slide the toggle to **On**, and then select **Save**.
    - **Mail-enabled public folders**: On the **Mail properties** tab, select **Hide from Exchange address list**.
4. When you're finished, select **Save**.

### Use Exchange Online PowerShell to hide recipients from address lists

To hide a recipient from address lists, use the following syntax:

```powershell
Set-<RecipientType> -Identity <RecipientIdentity> -HiddenFromAddressListsEnabled $true
```

*&lt;RecipientType&gt;* is one of these values:

- `DistributionGroup`
- `DynamicDistributionGroup`
- `Mailbox`
- `MailContact`
- `MailPublicFolder`
- `MailUser`
- `UnifiedGroup`

This example hides the distribution group named Internal Affairs from address lists.

```powershell
Set-DistributionGroup -Identity "Internal Affairs" -HiddenFromAddressListsEnabled $true
```

This example hides the mailbox `michelle@contoso.com` from address lists.

```powershell
Set-Mailbox -Identity michelle@contoso.com -HiddenFromAddressListsEnabled $true
```

Tip

To make the recipient visible in address lists again, use the value `$false` for the *HiddenFromAddressListsEnabled* parameter.

### How do you know you successfully hid a recipient from address lists?

To verify you successfully hid a recipient from address lists, use any of the following procedures:

- In the EAC, select the recipient and verify the "hide" setting in the details flyout.
- In Exchange Online PowerShell, do one of the following steps:

    - **Individual recipient**: Replace &lt;Identity&gt; with the name, alias, or email address of the recipient, and then run the following command:

        ```powershell
        Get-Recipient -Identity "<Identity>" | Format-List Name,HiddenFromAddressListsEnabled
        ```
    - **All recipients**: Run the following command and verify the recipient is listed:

        ```powershell
        Get-Recipient -ResultSize unlimited -Filter 'HiddenFromAddressListsEnabled -eq $true'
        ```
- Open the GAL in Outlook or Outlook on the web (formerly known as Outlook Web App), and verify the recipient isn't visible.