---
layout: Conceptual
title: Assign an address book policy to users in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/address-books/address-book-policies/assign-an-address-book-policy-to-mail-users
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
ms.custom:
- has-azure-ad-ps-ref
description: Admins can learn how to assign address book policies (ABPs) to users in Exchange Online
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2024-03-15T00:00:00.0000000Z
locale: en-us
document_id: f0e75c97-a4a0-cce1-be41-543a1d9d6da9
document_version_independent_id: 83918c37-fd6b-dfb4-ff27-096aa7af53a8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/address-books/address-book-policies/assign-an-address-book-policy-to-mail-users.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-books/address-book-policies/assign-an-address-book-policy-to-mail-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/address-books/address-book-policies/assign-an-address-book-policy-to-mail-users.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 32ca0315-4f6f-7f39-a3c1-f09b2d1f1e44
---

# Assign an address book policy to users in Exchange Online | Microsoft Learn

Address book policies (ABPs) allow you to segment users into specific groups to give them customized global address lists (GALs) in Outlook and Outlook on the web (formerly known as Outlook Web App). For more information about ABPs, see [Address book policies in Exchange Online](address-book-policies).

Users aren't automatically assigned an ABP when you create mailboxes. If you don't assign an ABP to a mailbox, the GAL for your entire organization is visible to the user in Outlook and Outlook on the web. Furthermore, a user that's assigned an ABP needs to exist in the GAL that's specified for the ABP.

To identify your virtual organizations for ABPs, we recommend that you use the **CustomAttribute1** to **CustomAttribute15** attributes on mailboxes, contacts, and groups, because these attributes are the most widely available and manageable for all recipient types.

To assign ABPs to mailboxes, you select the ABP in Exchange admin center (EAC), or specify the ABP in Exchange Online PowerShell.

## What do you need to know before you begin?

- Estimated time to complete: Less than 5 minutes.
- By default, the Address List role isn't assigned to any role groups in Exchange Online. To use any cmdlets or features that require the Address List role, you need to add the role to a role group. For more information, see [Modify role groups](../../permissions-exo/role-groups#use-the-eac-to-modify-role-groups).
- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to assign an ABP to a mailbox

1. In the [EAC](https://admin.exchange.microsoft.com), click **Recipients** &gt; **Mailboxes**.
2. In the list of mailboxes, find the mailbox that you want to modify. You can:

    - Scroll through the list of mailboxes.
    - Click **Search**![Search icon.](../../exchangeonline/media/itpro_eac_.png) and enter part of the user's name, email address, or alias.
    - Click on **Filter** icon for more filter options.
3. On the **Manage mailboxes** page, select an individual mailbox by clicking anywhere in the row including the button option that appears in the blank area next to the **Display name** column.
4. On the **User mailbox** page that opens, click **Mailbox** &gt; **Manage mailbox policies**.
5. In the **Manage mailbox policies** page, click the drop-down arrow in **Address book policy**, and select the ADP that you want to apply.

    ![Screenshot that shows Address book policy settings for a mailbox in the EAC at Recipients &gt; select mailbox &gt; Edit &gt; Mailbox features.](../../exchangeonline/media/eac-address-book-policy-mailbox.png)
6. When you're finished, click **Save**.

## Use the EAC to assign an ABP to multiple mailboxes

1. In the [EAC](https://admin.exchange.microsoft.com), click **Recipients** &gt; **Mailboxes**.
2. On the **Manage mailboxes** page, select the mailboxes and click **Mailbox policies**.
3. In the **Mailbox policies** details pane, click the drop-down arrow in **Address book policy**, and select the ADP that you want to apply.

    ![Screenshot that shows Bulk select mailboxes in the EAC to assign an address book policy.](../../exchangeonline/media/eac-address-book-policy-multiple.png)
4. Click **Save**.

## Use Exchange Online PowerShell to assign an ABP to mailbox users

There are three basic methods you can use to apply an ABP to mailboxes:

- **Individual mailboxes**: Use the following syntax:

    ```PowerShell
    Set-Mailbox -Identity <MailboxIdentity> -AddressBookPolicy <ABPIdentity>
    ```

    This example assigns the ABP named All Fabrikam to the mailbox joe@fabrikam.com.

    ```PowerShell
    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"
    ```
- **Filter mailboxes by attributes**: This method uses the unique filterable attribute that defines the virtual organization (for example, the **CustomAttribute1** through **CustomAttribute15** attribute value).

    The syntax uses the following two commands (one to identify the mailboxes, and the other to apply the ABP to the mailboxes):

    ```PowerShell
    $<VariableName> = Get-Mailbox -ResultSize unlimited -Filter <Filter>
    ```

    ```PowerShell
    $<VariableName> | foreach {Set-Mailbox -Identity $_.MicrosoftOnlineServicesID -AddressBookPolicy <ABPIdentity>}
    ```

    This example assigns the ABP named All Fabrikam to all mailbox users whose **CustomAttribute15** value is `FAB`.

    ```PowerShell
    $Fabrikam = Get-Mailbox -Filter "CustomAttribute15 -eq 'FAB'"
    ```

    ```PowerShell
    $Fabrikam | foreach {Set-Mailbox -Identity $_.MicrosoftOnlineServicesID -AddressBookPolicy "All Fabrikam"}
    ```
- **Use a list of specific mailboxes**: This method requires a text file to identify the mailboxes. Values that don't contain spaces (for example, the user account) work best. The text file must contain one user account on each line like this:

> 
> akol@contoso.com  tjohnston@contoso.com  kakers@contoso.com

    The syntax uses the following two commands (one to identify the user accounts, and the other to apply the policy to those users):

    ```PowerShell
    $<VariableName> = Get-Content "<text file>"
    ```

    ```PowerShell
    $<VariableName> | foreach {Set-Mailbox -Identity $_.MicrosoftOnlineServicesID -AddressBookPolicy <ABPIdentity>}
    ```

    This example assigns the ABP policy named All Fabrikam to the mailboxes specified in the file C:\My Documents\Fabrikam.txt.

    ```PowerShell
    $Fab = Get-Content "C:\My Documents\Fabrikam.txt"
    ```

    ```PowerShell
    $Fab | foreach {Set-Mailbox -Identity $_.MicrosoftOnlineServicesID -AddressBookPolicy "All Fabrikam"}
    ```

For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox) and [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox).

### How do you know this worked?

To verify that you've successfully applied an ABP to a mailbox, use any of the following steps:

- In the EAC, go to **Recipients** &gt; **Mailboxes**, In the properties of the mailbox window that opens, click **Manage mailbox policies**, and verify the ABP in the **Address book policy** field.
- In Exchange Online PowerShell, replace &lt;MailboxIdentity&gt; with the name, alias, email address, or account name of the mailbox, and run the following command to verify the value of the **AddressBookPolicy** property:

    ```PowerShell
    Get-Mailbox -Identity "<MailboxIdentity>" | Format-List AddressBookPolicy
    ```
- In Exchange Online PowerShell, run the following command to verify the value of the **AddressBookPolicy** property:

    ```PowerShell
    Get-Mailbox -ResultSize unlimited | Format-Table Name,AddressBookPolicy -Auto
    ```

## More information

To remove the ABP assignment from a mailbox, you select the value **[No Policy]** in the EAC, or use the value `$null` for the *AddressBookPolicy* parameter in Exchange Online PowerShell.