---
layout: Conceptual
title: Enable or disable access to Outlook for Windows | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/enable-disable-employee-access-new-outlook
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
author: Benny-54
ms.author: serdars
ms.localizationpriority: medium
description: Admins can learn how to enable or disable user access to the new Outlook (Outlook for Windows) for work or school mailboxes, and show or hide the 'Try the new Outlook' toggle in classic Outlook.
ms.topic: how-to
ms.assetid: 
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2025-03-07T00:00:00.0000000Z
locale: en-us
document_id: 9c57a985-2bd9-fa92-ae60-7ba86a91c7ca
document_version_independent_id: fa3fdd7d-1d07-4a0d-29b5-77e547ec3a5a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/enable-disable-employee-access-new-outlook.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-on-the-web/enable-disable-employee-access-new-outlook
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/enable-disable-employee-access-new-outlook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 0b89a0c3-47b1-bc17-578c-c55206833dc4
---

# Enable or disable access to Outlook for Windows | Microsoft Learn

By default, users in Microsoft 365 or Office 365 can access their work or school mailboxes using Outlook for Windows (formerly known as the new Outlook for Windows). Admins can use the following methods to control user access to work or school mailboxes in Outlook for Windows:

- Use Exchange Online PowerShell to prevent or allow access to work or school mailboxes using Outlook for Windows.
- Use registry keys to show or hide the **Try the new Outlook** toggle in classic Outlook.

The rest of this article describes these procedures.

Tip

See the following links for more procedures related to Outlook for Windows:

- [Block new Outlook preinstall on Windows](/en-us/microsoft-365-apps/outlook/get-started/control-install#block-new-outlook-preinstall-on-windows)
- [Block new Outlook installation as part of Mail and Calendar deprecation](/en-us/microsoft-365-apps/outlook/get-started/control-install#block-new-outlook-installation-as-part-of-mail-and-calendar-deprecation)
- [Prevent users from acquiring new Outlook from Microsoft Store](/en-us/microsoft-365-apps/outlook/get-started/control-install#prevent-users-from-acquiring-new-outlook-from-microsoft-store)
- [Opt-out of new Outlook migration](/en-us/microsoft-365-apps/outlook/get-started/control-install#opt-out-of-new-outlook-migration)

## What do you need to know before you begin?

- Estimated time to complete this procedure: 5 minutes.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- To use any version of Outlook with a work or school mailbox, you need the correct Microsoft 365 or Office 365 license. For more information, see [How licensing works for work and school accounts in the new Outlook for Windows](https://techcommunity.microsoft.com/blog/outlook/how-licensing-works-for-work-and-school-accounts-in-the-new-outlook-for-windows/4047361).
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Outlook on the web mailbox policies" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.

Tip

Having problems? Ask for help in the [Exchange Online forum](/en-us/answers/topics/office-exchange-server-itpro.html).

## Use Exchange Online PowerShell to enable or disable access to work or school mailboxes in Outlook for Windows

Admins can use the following methods in Exchange Online PowerShell to prevent or allow user access to work or school mailboxes:

- **Set-CasMailbox**: Allows granular control for **existing** work or school mailboxes (individual mailboxes or multiple mailboxes).
- **Set-OwaMailboxPolicy**: Applies to **existing** and **future** work or school mailboxes using a broad, policy-based approach.

These methods are described in the following subsections.

Tip

The default value for the *OneWinNativeOutlookEnabled* parameter on both cmdlets is blank (`$null`), which is equivalent to the value `$true` (users aren't restricted from accessing their work or school mailboxes using Outlook for Windows).

### Use the Set-CASMailbox cmdlet to control access to work or school mailboxes in Outlook for Windows

After you [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use any of the following methods:

- **Individual mailboxes**: Use the following syntax:

    ```powershell
    Set-CASMailbox -Identity <MailboxIdentity> -OneWinNativeOutlookEnabled <$true | $false | $null>
    ```

    Where &lt;MailboxIdentity&gt; is any value that uniquely identifies the mailbox. For example:

    - Name
    - Alias
    - Email address
    - User ID

    This example disables Outlook for Windows for the specified user.

    ```powershell
    Set-CASMailbox -Identity colin@contoso.onmicrosoft.com -OneWinNativeOutlookEnabled $false
    ```

    This example enables Outlook for Windows for the specified user.

    ```powershell
    Set-CASMailbox -Identity colin@contoso.onmicrosoft.com -OneWinNativeOutlookEnabled $true
    ```
- **Multiple mailboxes**: You have the following options:

    - **Filter mailboxes by attributes**: The target mailboxes share at least one unique filterable attribute. For example:

        - Title, Department, or address information for user accounts as seen by the **Get-User** cmdlet.
        - `CustomAttribute1` through `CustomAttribute15` for mailboxes as seen by the **Get-Mailbox** cmdlet.

        For more information, see [Filterable Properties for the -Filter Parameter](/en-us/powershell/exchange/filter-properties) and [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox).

        This method requires two commands:

        - Identify the mailboxes and store the results in a variable.
        - Use the results to enable or disable access to the mailboxes using Outlook for Windows.

        ```powershell
        $<VariableName> = <Get-User | Get-Mailbox> -ResultSize unlimited -Filter <Filter>
        
        $<VariableName> | foreach {Set-CASMailbox -Identity $_.MicrosoftOnlineServicesID -OneWinNativeOutlookEnabled <$true | $false | $null>}
        ```

        This example disables access to Outlook for Windows for all mailboxes where the **Title** attribute contains "Vendor" or "Contractor".

        ```powershell
        $Vend = Get-User -ResultSize unlimited -Filter "(RecipientType -eq 'UserMailbox') -and (Title -like '*Vendor*' -or Title -like '*Contractor*')"
        
        $Vend | foreach {Set-CASMailbox -Identity $_.MicrosoftOnlineServicesID -OneWinNativeOutlookEnabled $false}
        ```
    - **Specify mailboxes in a list**: Use a text file to identify the mailboxes. The text file contains one mailbox on each line like this:

> 
> `akol@contoso.com``ljohnston@contoso.com``kakers@contoso.com`

        This method requires two commands:

        - Specify the text file that identifies the mailboxes and store the results in a variable.
        - Use the results to enable or disable access to the mailboxes using Outlook for Windows.

        ```powershell
        $<VariableName> = Get-Content "<text file>"
        
        $<VariableName> | foreach {Set-CASMailbox -Identity $_ -OneWinNativeOutlookEnabled <$true | $false>}
        ```

        This example disables access to Outlook for Windows for the mailboxes specified in the file C:\My Documents\Management.txt.

        ```powershell
        $Mgmt = Get-Content "C:\My Documents\Management.txt"
        
        $Mgmt | foreach {Set-CASMailbox -Identity $_ -OneWinNativeOutlookEnabled $false}
        ```

        For detailed syntax and parameter information, see [Set-CASMailbox](/en-us/powershell/module/exchangepowershell/set-casmailbox).

#### How do you know you successfully used the Set-CASMailbox cmdlet to enable or disable access to work or school mailboxes in Outlook for Windows?

To verify you successfully used the **Set-CASMailbox** cmdlet to enable or disable access to work or school mailboxes in Outlook for Windows, use any of the following methods:

Tip

- The value True or blank for the *OneWinNativeOutlookEnabled* property means access is enabled.
- The value False for the *OneWinNativeOutlookEnabled* property means access is disabled.

- Replace &lt;MailboxIdentity&gt; with the name, alias, email address or user ID of the mailbox, and then run the following command to verify the value of the `OneWinNativeOutlookEnabled` property:

    ```powershell
    Get-CASMailbox -Identity <MailboxIdentity> | Format-List Name,OneWinNativeOutlookEnabled
    ```
- Run the following command to verify the value of the `OneWinNativeOutlookEnabled` property for all user mailboxes:

    ```powershell
    Get-CASMailbox -ResultSize unlimited -Filter "RecipientTypeDetailsValue -eq 'UserMailbox'" | Format-Table DisplayName,OneWinNativeOutlookEnabled
    ```
- If you modified the *OneWinNativeOutlookEnabled* value for multiple users, use the same variable to check the value for those users. For example:

    ```powershell
    $Vend | foreach {Get-CASMailbox -Identity $_.MicrosoftOnlineServicesID | Format-Table DisplayName,OneWinNativeOutlookEnabled}
    ```

    or

    ```powershell
    $Mgmt | foreach {Get-CASMailbox -Identity $_ | Format-Table DisplayName,OneWinNativeOutlookEnabled}
    ```

For detailed syntax and parameter information, see [Get-CASMailbox](/en-us/powershell/module/exchangepowershell/get-casmailbox).

### Use the Set-OwaMailboxPolicy cmdlet to control access to work or school mailboxes in Outlook for Windows

Outlook on the web mailbox policies (formerly known as Outlook Web App mailbox policies or OWA mailbox policies) control the Outlook on the web and Outlook for Windows experience for users.

By default, all organizations have default policy named `OwaMailboxPolicy-Default` applied to all mailboxes. Admins can create and apply custom policies to specific groups of users. For more information, see [Apply or remove mailbox policies for Outlook on the web and Outlook for Windows in Exchange Online](apply-or-remove-outlook-web-app-mailbox-policy).

After you [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), do the steps described in the following subsections.

#### Step 1 (Optional): Verify Outlook on the web is enabled for the target mailboxes

If users are blocked from using Outlook on the web to access their mailboxes, they also can't use Outlook for Windows to access their mailboxes.

By default, all users can access their mailboxes using Outlook on the web. To verify the status for all user mailboxes in the organization, run the following command to verify the value of the *OWAEnabled* property:

```powershell
Get-CASMailbox -ResultSize unlimited -Filter "RecipientTypeDetailsValue -eq 'UserMailbox'" | Format-Table DisplayName,OWAEnabled
```

- The value True means Outlook on the web access to the mailbox is enabled. You can proceed to the next step to enable or disable access to the mailboxes using Outlook for Windows.
- The value False means Outlook on the web access to the mailbox is disabled, which also means Outlook for Windows access to the mailbox is disabled. You can't enable access to the mailbox using Outlook for Windows until you enable access for Outlook on the web. The required commands are similar to the commands in the Use the Set-CasMailbox cmdlet to control access to work or school mailboxes in Outlook for Windows section: just replace *OneWinNativeOutlookEnabled* with *OWAEnabled* in the commands, and use the value `$true` or `$false` (`$null` isn't available).

For detailed syntax and parameter information, see [Get-OwaMailboxPolicy](/en-us/powershell/module/exchangepowershell/get-owamailboxpolicy).

### Step 2: Use the Set-OwaMailboxPolicy cmdlet to enable or disable access to work or school mailboxes in Outlook for Windows

Tip

The value you specify in the Outlook on the web mailbox policy affects all current and future mailboxes that have the policy applied to them. You can modify the default policy, modify custom policies, or you can create custom policies that apply the setting to specific groups of users.

To enable or disable access to mailboxes in Outlook for Windows in Outlook on the web mailbox policies, use the following syntax:

```powershell
Set-OwaMailboxPolicy -Identity <PolicyIdentity> -OneWinNativeOutlookEnabled <$true | $false | $null>
```

Where &lt;PolicyIdentity&gt; is any value that uniquely the policy. For example:

- Name
- Distinguished name (DN)
- GUID

This example disables access to Outlook for Windows for all mailboxes that use the default policy named `OwaMailboxPolicy-Default` (by default, all mailboxes):

```powershell
Get-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -OneWinNativeOutlookEnabled $false
```

This example disables access to Outlook for Windows for all mailboxes in the organization by disabling access in all policies:

```powershell
Get-OwaMailboxPolicy | Set-OwaMailboxPolicy -OneWinNativeOutlookEnabled $false
```

This example enables access to Outlook for Windows for all mailboxes in the organization by enabling access in all policies:

```powershell
Get-OwaMailboxPolicy | Set-OwaMailboxPolicy -OneWinNativeOutlookEnabled $true
```

For detailed syntax and parameter information, see [Get-OwaMailboxPolicy](/en-us/powershell/module/exchangepowershell/get-owamailboxpolicy) and [Set-OwaMailboxPolicy](/en-us/powershell/module/exchangepowershell/set-owamailboxpolicy).

#### How do you know you successfully used the Set-OwaMailboxPolicy cmdlet to enable or disable access to work or school mailboxes in Outlook for Windows?

To verify you successfully used the **Set-OwaMailboxPolicy** cmdlet to enable or disable access to work or school mailboxes in Outlook for Windows, run the following command to verify the value of the *OneWinNativeOutlookEnabled* property for all Outlook on the web mailbox policies:

```powershell
Get-OwaMailboxPolicy | Set-OwaMailboxPolicy | Format-Table Name,OneWinNativeOutlookEnabled
```

- The value True or blank for the *OneWinNativeOutlookEnabled* property means access is enabled, as long as the value of the *OWAEnabled* property in the output of the **Get-CASMailbox** cmdlet for the mailbox is also True.
- The value False for the *OneWinNativeOutlookEnabled* property means access is disabled. Access is also disabled if the value of the *OWAEnabled* property in the output of the **Get-CASMailbox** cmdlet for the mailbox is False, regardless of the *OneWinNativeOutlookEnabled* property value in the output of the **Get-OwaMailboxPolicy** cmdlet.

Note

Access to shared mailboxes and public folders in Outlook for Windows is controlled by Outlook on the web mailbox policy settings, not CAS mailbox settings. To enable or disable access to shared mailboxes and public folders using Outlook for Windows, see [Use the Set-OwaMailboxPolicy cmdlet to control access to work or school mailboxes in Outlook for Windows](enable-disable-employee-access-new-outlook#use-the-set-owamailboxpolicy-cmdlet-to-control-access-to-work-or-school-mailboxes-in-outlook-for-windows).

## Use the registry to enable or disable the "Try the new Outlook" toggle in classic Outlook

[![Screenshot of the Try the new Outlook toggle in classic Outlook.](../../exchangeonline/media/new-toggle.png)](../../exchangeonline/media/new-toggle.png#lightbox)

The **Try the new Outlook** toggle is available in all current versions of classic Outlook in all builds and channels. The setting to control the availability of the **Try the new Outlook**" toggle in classic Outlook is available as group policy object (GPO) that you can manage via cloud policy in the following channels and builds of classic Outlook:

- **Current Channel (Preview)**: Version 2209 (15629.20058) or later.
- **Current Channel**: Version 2304 (Build 16327.20214) or later.
- **Monthly Enterprise Channel**: Version 2303 (Build 16227.20318) or later.
- **Semi-Annual Enterprise Channel (Preview)**: Build 16731.20234 or later.
- **Semi-Annual Enterprise Channel**: Build 16731.20504 or later.

Or, you can use the registry to control the availability of the **Try the new Outlook**" toggle in classic Outlook as described in the following steps:

1. Copy one or more of the following text blocks into Notepad:

    - Select **one** of the following values:

        - **Hide** the **Try the new Outlook** toggle in classic Outlook:

            ```text
            Windows Registry Editor Version 5.00
            
            [HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Outlook\Options\General]
            "HideNewOutlookToggle"=dword:00000001
            ```
        - **Show** the **Try the new Outlook**" toggle in classic Outlook:

            ```text
            Windows Registry Editor Version 5.00
            
            [HKEY_CURRENT_USER\Software\Microsoft\office\16.0\Outlook\Options\General]
            "HideNewOutlookToggle"=dword:00000000
            ```
    - Prevent users from changing the registry value that shows or hides the **Try the new Outlook**" toggle in classic Outlook:

        ```text
        Windows Registry Editor Version 5.00
        
        [HKEY_CURRENT_USER\Software\Policies\Microsoft\office\16.0\outlook\options\general]
        "HideNewOutlookToggle"=dword:00000001
        ```

    Tip

    The text file requires only one instance of `Windows Registry Editor Version 5.00` if you copy multiple text blocks. For example:

    ```text
    Windows Registry Editor Version 5.00
    
    [HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Outlook\Options\General]
    "HideNewOutlookToggle"=dword:00000001
    
    [HKEY_CURRENT_USER\Software\Policies\Microsoft\office\16.0\outlook\options\general]
    "HideNewOutlookToggle"=dword:00000001
    ```
2. Save the file as .reg in a location that's easy to find. For example: `C:\Data\Disable New Outlook toggle in Outlook Desktop.reg` or `C:\Data\Enable New Outlook toggle in Outlook Desktop.reg`.
3. Double-click on the .reg file and select **Yes** in the confirmation dialog that opens.

## FAQ

### Q: If a user previously turned on "Try the new Outlook" in classic Outlook, how long does it take for the Set-CASMailbox command to disable access to the mailbox in Outlook for Windows? Do they need to restart Outlook for Windows?

A: If a user is already trying Outlook for Windows with their work or school account before an admin disables their access, their account is disabled in Outlook for Windows and they can no longer use Outlook for Windows with that account.

The user can delete the account from Outlook for Windows and then use Outlook for Windows with another account.

If an admin already used the *OneWinNativeOutlookEnabled* parameter on the **Set-CASMailbox** or **Set-OwaMailboxPolicy** cmdlets to disable access to the mailbox in Outlook for Windows, and the user tries to turn on the **Try the new Outlook** toggle, they receive the error shown in the following screenshot:

[![Screenshot of the error message users get when they try to turn on the Try the new Outlook toggle after an admin already disabled access to their mailbox.](../../exchangeonline/media/acc-blocked.jpg)](../../exchangeonline/media/acc-blocked.jpg#lightbox)

### Q: Do the Exchange Online PowerShell commands to enable or disable work or school mailbox access in Outlook for Windows affect the "Try the new Outlook" toggle in classic Outlook?

A: No.

The *OneWinNativeOutlookEnabled* parameter on the **Set-CASMailbox** or **Set-OwaMailboxPolicy** cmdlets doesn't affect the availability of the **Try the new Outlook** toggle in classic Outlook. The cmdlets determine whether users can open their work or school mailboxes in Outlook for Windows.

Admins can manage the toggle in classic Outlook separately using the registry settings. For example, an admin might want to allow users to try Outlook for Windows without having the toggle available in classic Outlook.

Also, users can install the Outlook for Windows app from the Microsoft Store, which further illustrates how the PowerShell cmdlets control access to work or school mailboxes only, regardless of where or how the users installed Outlook for Windows.

### Q: A user previously turned on "Try the new Outlook" in classic Outlook, but then the registry key to hide the toggle is configured on their computer. What happens?

A: It depends on how the user launches Outlook for Windows:

- **Using the classic Outlook icon**: The user is switched out of Outlook for Windows back to classic Outlook the next time they open classic Outlook.
- **Using the Outlook for Windows icon**: Outlook for Windows opens as if they selected **Try the new Outlook** in classic Outlook. The logic to switch back to classic Outlook runs only when the registry key is read (typically, when the computer restarts). Outlook for Windows doesn't recognize or use the registry key; only classic Outlook uses the registry key.

### Q: If user turns on "Try the new Outlook" in classic Outlook, and later turns off the toggle, what's required to stop using Outlook for Windows?

When the user decides to switch back, Outlook for Windows closes and classic Outlook opens. This action happens immediately. Outlook for Windows and classic Outlook are two separate apps that remain installed, regardless of the toggle setting.

The toggle allows users to switch quickly between the two apps, and allows the Outlook Team to ask for feedback when users switch back to classic Outlook.

### Q: Are group policies for classic Outlook honored in Outlook for Windows?

A: If your organization uses group policies to configure classic Outlook, you might want to implement corresponding policies for Outlook for Windows. All ADMX templates and most Cloud policies apply only to classic Outlook. For instructions, see [Map classic Outlook policies to new Outlook](/en-us/outlook/troubleshoot/installation/map-classic-outlook-policies-to-new-outlook?source=docs).