---
layout: Conceptual
title: Apply or remove mailbox policy on a mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/apply-or-remove-outlook-web-app-mailbox-policy
Manager: serdars
ms.subservice: outlook-services
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
description: You can apply an Outlook on the web mailbox policy to one or more mailboxes or remove one using either the EAC or Exchange Online PowerShell.
ms.topic: how-to
author: officedocspr
ms.author: odocspr
ms.assetid: 51d8e269-b0d5-4bc7-9b3d-0460871e54fa
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2023-11-17T00:00:00.0000000Z
locale: en-us
document_id: 31286d14-646b-df2f-842b-88ae26d088fb
document_version_independent_id: 9afcbe11-5ede-56e6-34bd-2bccdc3dda2f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/apply-or-remove-outlook-web-app-mailbox-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-on-the-web/apply-or-remove-outlook-web-app-mailbox-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/apply-or-remove-outlook-web-app-mailbox-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: afccbc11-152c-4d00-876e-1240a40b7679
---

# Apply or remove mailbox policy on a mailbox in Exchange Online | Microsoft Learn

The Outlook on the web mailbox policy (formerly known as an Outlook Web App mailbox policy) that's assigned to a mailbox controls the Outlook on the web and new Outlook for Windows experience for the user. You use the Exchange admin center (EAC) or Exchange Online PowerShell to apply Outlook on the web mailbox policies to one or more mailboxes or to remove the policy assignments from mailboxes.

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. For information on the permissions you need, see the "Outlook on the web mailbox policies" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- For information about how to open the EAC, see [Exchange admin center in Exchange Online](../../exchange-admin-center). For information about how to connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Apply mailbox policies for Outlook on the web and the new Outlook for Windows mailboxes

### Use the EAC to apply an Outlook on the web mailbox policy to a mailbox

1. In the [EAC](https://admin.exchange.microsoft.com), go to **Recipients** &gt; **Mailboxes**. Or, use [**Outlook web app policies**](https://admin.exchange.microsoft.com/#/owapolicies).
2. On the **Manage mailboxes**page, perform one of the following steps:
    - Select an individual mailbox by clicking anywhere in the row other than the button option that appears in the blank area next to the **Display name** column.

        1. In the **Details** flyout that opens, select **Manage email apps settings** under **Email apps & mobile devices** section.
        2. In the **Manage settings for email apps** flyout that opens, delete the existing value **OwaMailboxPolicy-Default** from the **Outlook web app mailbox policy** box.
        3. In the **Outlook web app mailbox policy** box, start typing the name of the policy, and then select it from the results.
        4. When you're finished in the **Manage settings for email apps** flyout, select **Save**.
    - Select multiple mailboxes by selecting the button option that appears in the blank area next to the **Display name** column in each row.

        1. Select the **Edit** action that appears, and then select **App settings** from the drop-down list.
        2. In the **Manage email apps settings** flyout that opens, if the **Outlook web app mailbox policy** box isn't visible, select **Enable** for **Outlook on the web**.
        3. In the **Outlook Web App mailbox policy** box, start typing the name of the policy, and then select it from the results.
        4. When you're finished in the **Manage settings for email apps** flyout, select **Save**.

### Use Exchange Online PowerShell to apply an Outlook on the web mailbox policy to a mailbox

There are three basic methods that you can use to apply an Outlook on the web mailbox policy to a mailbox:

- **Individual mailboxes**: Use the following syntax:

    ```PowerShell
    Set-CasMailbox -Identity <MailboxIdentity> -OwaMailboxPolicy "<Policy Name>"
    ```

    This example applies the mailbox policy named "Sales Associates" to tony@contoso.com for Outlook on the web and the new Outlook for Windows.

    ```PowerShell
    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy "Sales Associates"
    ```
- **Filter mailboxes by attributes**: This method requires that the mailboxes all share a unique filterable attribute. For example:

    - Title, Department, or address information for user accounts as seen by the **Get-User** cmdlet.
    - CustomAttribute1 through CustomAttribute15 for mailboxes as seen the **Get-Mailbox** cmdlet.

    The syntax uses the following two commands (one to identify the mailboxes, and the other to apply the policy to the mailboxes):

    ```PowerShell
    $<VariableName> = <Get-User | Get-Mailbox> -ResultSize unlimited -Filter <Filter>
    
    $<VariableName> | foreach {Set-CasMailbox -Identity $_.MicrosoftOnlineServicesID -OwaMailboxPolicy "<Policy Name>"}
    ```

    This example assigns the policy named "Managers and Executives" to all mailboxes whose **Title** attribute contains "Manager" or "Executive".

    ```PowerShell
    $Mgmt = Get-User -ResultSize unlimited -Filter "(RecipientType -eq 'UserMailbox') -and (Title -like '*Manager*' -or Title -like '*Executive*')"
    
    $Mgmt | foreach {Set-CasMailbox -Identity $_.MicrosoftOnlineServicesID -OwaMailboxPolicy "Managers and Executives"}
    ```
- **Use a list of specific mailboxes**: This method requires a text file to identify the mailboxes. Values that don't contain spaces (for example, the user account) work best. The text file must contain one user account on each line like this:

> 
> akol@contoso.onmicrosoft.com  ljohnston@contoso.onmicrosoft.com  kakers@contoso.onmicrosoft.com

    The syntax uses the following two commands (one to identify the user accounts, and the other to apply the policy to those users):

    ```PowerShell
    $<VariableName> = Get-Content "<text file>"
    
    $<VariableName> | foreach {Set-CasMailbox -Identity $_ -OwaMailboxPolicy "<Policy Name>"}
    ```

    This example assigns the policy named "Managers and Executives" to the mailboxes specified in the file C:\My Documents\Management.txt.

    ```PowerShell
    $Mgrs = Get-Content "C:\My Documents\Management.txt"
    
    $Mgrs | foreach {Set-CasMailbox -Identity $_ -OwaMailboxPolicy "Managers and Executives"}
    ```

For detailed syntax and parameter information, see [Set-CASMailbox](/en-us/powershell/module/exchangepowershell/set-casmailbox).

### How do you know that you've successfully applied an Outlook on the web mailbox policy to a mailbox?

To verify that you've applied a mailbox policy to a mailbox for Outlook on the web and the new Outlook for Windows, perform any of the following steps:

- In the EAC, go to **Recipients** &gt; **Mailboxes** and select the mailbox. In the **Details** flyout that opens, select **Manage email apps settings** under **Email apps & mobile devices**, and verify the name of the policy in the **Outlook web app mailbox policy** box.
- In Exchange Online PowerShell, replace &lt;MailboxIdentity&gt; with the name, alias, email address, or account name of the mailbox, and run the following command to verify the value of the **OwaMailboxPolicy** property:

    ```PowerShell
    Get-CasMailbox -Identity "<MailboxIdentity>" | Format-List OwaMailboxPolicy
    ```
- In Exchange Online PowerShell, run the following command to verify the value of the **OwaMailboxPolicy** property for all mailboxes:

    ```PowerShell
    Get-CasMailbox -ResultSize unlimited | Format-Table Name,OwaMailboxPolicy -Auto
    ```

## Remove mailbox policy assignments from mailboxes for Outlook on the web or the new Outlook for Windows

### Use the EAC to remove the Outlook on the web mailbox policy assignment from a mailbox

1. In the [EAC](https://admin.exchange.microsoft.com), select **Recipients** &gt; **Mailboxes**. Or, use [**Outlook web app policies**](https://admin.exchange.microsoft.com/#/mailboxes).
2. On the **Manage mailboxes** page, select an individual mailbox by clicking anywhere in the row other than the button option that appears in the blank area next to the **Display name** column.
3. In the **Details** flyout that opens, select **Manage email apps settings** under **Email apps & mobile devices**.
4. In the **Manage settings for email apps** flyout that opens, delete the existing value **OwaMailboxPolicy-Default** from the **Outlook web app mailbox policy** box.
5. When you're finished in the **Manage settings for email apps** flyout, select **Save**.

### Use Exchange Online PowerShell to remove the Outlook on the web mailbox policy assignment from a mailbox

To remove the Outlook on the web mailbox policy assignment from a mailbox, use the following syntax:

```PowerShell
Set-CasMailbox -Identity "<MailboxIdentity>" -OwaMailboxPolicy $null
```

This example removes the mailbox policy from mailbox of the user tony@contoso.com for Outlook on the web and the new Outlook for Windows.

```PowerShell
Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy $null
```

For detailed syntax and parameter information, see [Set-CASMailbox](/en-us/powershell/module/exchangepowershell/set-casmailbox).

### How do you know that you've successfully removed an Outlook on the web mailbox policy assignment from a mailbox?

To verify that you've removed an Outlook on the web mailbox policy assignment from a mailbox, perform any of the following steps:

- In the EAC, go to **Recipients** &gt; **Mailboxes** and select the mailbox. In the **Details** flyout that opens, select **Manage email apps settings**, and verify the **Outlook web app mailbox policy** box is empty.
- In Exchange Online PowerShell, replace &lt;MailboxIdentity&gt; with the name, alias, email address, or account name of the mailbox, and run the following command to verify that the **OwaMailboxPolicy** property is blank:

    ```PowerShell
    Get-CasMailbox -Identity "<MailboxIdentity>" | Format-List OwaMailboxPolicy
    ```