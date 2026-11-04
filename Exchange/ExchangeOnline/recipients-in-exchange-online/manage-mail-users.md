---
layout: Conceptual
title: Manage mail users in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-mail-users
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
description: Mail users are similar to mail contacts. Both have external email addresses and both contain information about people outside your Exchange or Exchange Online organization that can be displayed in the shared address book and other address lists. However, unlike a mail contact, a mail user has sign in credentials in your Exchange, Microsoft 365, or Office 365 organization and can access resources. For more information, see Recipients.
ms.topic: how-to
author: AshaIyengar21
f1.keywords:
- CSH
ms.custom:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailUserWizardForm.NewMailUserIntroductionWizardPage
ms.author: serdars
ms.assetid: bb8b8804-f730-4ad7-9173-896a4965b90f
ms.reviewer: AkshayaPrakash-PM
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-22T00:00:00.0000000Z
locale: en-us
document_id: 3fa08719-f07a-a792-4ef3-9f9f8ae8a498
document_version_independent_id: d649e94b-e464-a4a0-b6b9-6d8ed31c2e73
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-mail-users.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-mail-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-mail-users.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: d84a81bc-3e71-efbe-fa08-7d7f3d24a43e
---

# Manage mail users in Exchange Online | Microsoft Learn

In Exchange Online organizations, mail users are similar to mail contacts. Both have external email addresses and both contain information about people outside your Exchange Online organization that can be displayed in the shared address book and other address lists. However, unlike a mail contact, a mail user has sign in credentials in your Microsoft 365 organization and can access resources. For more information about mail contacts and mail users, see [Recipients in Exchange Online](recipients-in-exchange-online).

You manage mail users in the Exchange admin center (EAC) or in PowerShell (Exchange Online PowerShell in organizations with Exchange Online mailboxes).

## What do you need to know before you begin?

- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../exchange-admin-center).
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell)..
- Mail users don't require licenses in Exchange Online.
- When you create mail users in Exchange Online PowerShell, you might encounter throttling.
- You need permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../permissions-exo/feature-permissions) article.
- For information about keyboard shortcuts that might apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).

## Use the Exchange admin center to manage mail users

In the EAC at https://admin.exchange.microsoft.com, go to **Recipients** &gt; **Contacts**. Or to go directly to the **Contacts** page, use https://admin.exchange.microsoft.com/#/contacts.

The following information is shown on the **Contacts** page for each entry:

- **Display name**
- **Email address**
- **Contact type**: This value is **MailUser** for mail users.

To change the list from normal to compact spacing, select ![](../exchangeonline/media/modern-eac-standard-icon.png)**Change view**, and then select ![](../exchangeonline/media/modern-eac-compact-icon.png)**Compact list**.

Use the ![](../exchangeonline/media/modern-eac-search-icon.png)**Search** box and a corresponding value to find specific mail users.

To filter the list of entries on the page, select ![](../exchangeonline/media/modern-eac-filter-icon.png)**Filter**, and then select one of the following values:

- **All contacts**
- **Mail contacts**
- **Mail users**
- **Guest mail users\*\*\*\*Groups with dynamic membership** or **Ownerless groups**.

To clear the filter, select ![](../exchangeonline/media/modern-eac-clear-filters-icon.png)**Clear filter**.

To create a custom filter, select ![](../exchangeonline/media/modern-eac-create-icon.png)**New filter**.

In the blank area next to the **Display name** column, select the round check box that appears next to one or more entries, or select all entries by selecting the round check box that appears in the column heading, and then select the ![](../exchangeonline/media/modern-eac-download-icon.png)**Export contacts** action that appears on the page. Select **Export contacts in current list** or **Export all contacts**. The default filename is **Contacts.csv** and the default location is the **Downloads** folder. If a file with that name already exists, the filename is appended with a number (for example, **Contacts (1).csv**).

### Use the EAC to create mail users

1. On the **Contacts** page at https://admin.exchange.microsoft.com/#/contacts, select ![](../exchangeonline/media/modern-eac-add-mail-user-icon.png)**Add a mail user** to open the new mail user wizard.
2. On the **Set up the basic information** page, configure the following settings. Settings marked with an ^\*^ are required.

    - **First name**
    - **Last name**
    - **Initials**: The person's middle initial.
    - **Display name**^\*^
    - **External email address**: Enter the user's email address. The domain should be external to your cloud-based organization.
    - **Alias**^\*^
    - **User ID**^\*^ and **Domain**^\*^: Enter the account that the person uses to sign in to the service.
    - **Password**^\*^ and **Confirm password**^\*^: Enter and reenter the account password. Verify that the password complies with the password length, complexity, and history requirements of your organization

    When you're finished on the **Set up the basic information** page, select **Next**.
3. On the **Review mail user** page, review the details. Select **Back** to make changes.

    When you're finished on the **Review mail user** page, select **Create**.
4. On the **Status** page, wait for the mail user creation to finish, and then select **Done**.

### Use the EAC to modify mail users

1. On the **Contacts** page at https://admin.exchange.microsoft.com/#/contacts, find the mail user that you want to modify (the **Contact type** value is **MailUser**), and select the mail user by clicking on the **Display name** value (don't select the checkbox).
2. In the details flyout that opens, the following tabs are available:

    - **General**tab:
        - **General information** section: Select **Manage general information**to modify the following properties:
            - **First name**
            - **Last name**
            - **Display name**
            - **Initials**
        - **Hide from global address list (GAL)**: Select **Manage hide from GAL** turn ![](../exchangeonline/media/toggle-off.png)**Off** or turn ![](../exchangeonline/media/toggle-on.png)**On** hiding the mail user from the GAL.
        - **MailTip** section: Select **Manage MailTip** to add a MailTip to the mail user.
    - **Personal information**section: The following settings are available:
        - **Contact information** section: Select **Contact information**to modify the following properties:
            - **Web site**
            - **Fax phone**
            - **Home phone**
            - **Mobile phone**
            - **Work phone**
            - **Office**
            - **Street**
            - **City**
            - **State/Province**
            - **ZIP/Postal code**
            - **Country/Region**
            - **Notes**
        - **Organization information** section: Select **Edit organization**to modify the following properties:
            - **Title**
            - **Department**
            - **Company**
            - **Manager**
            - **Direct reports** is available if the mail user is already designated as someone's manager.
    - **Others**tab:
        - **Custom attributes** section: Select **Manage custom attributes** to add text values to the **Custom 1** through **Custom 15** attributes.
        - **Member of (group membership)** section: Select **Manage member of** to remove the mail user from existing groups.
        - **Email addresses** section: Select **Manage email address types** to manage the proxy addresses for the mail user.
        - **Message delivery restrictions** section: Select **Manage message delivery restrictions**to change the following properties:
            - **Accept messages from**section:
                - Select **All senders** or **Selected senders**. If you select **Selected senders**, **Add sender** appears for you to select senders to allow.
                - Select or clear **Require senders to be authenticated**.
            - **Block messages from** section: Select **None** or **Selected senders**. If you select **Selected senders**, **Add sender** appears for you to select senders to block.

    When you're finished modifying the properties of the mail user, select **Save**.

### Use the EAC to remove mail users

1. On the **Contacts** page at https://admin.exchange.microsoft.com/#/contacts, find, select, and remove the mail user using either of the following methods:

    - Select the round check box that appears in the blank area next to the **Display name** column, and then select the ![](../exchangeonline/media/modern-eac-delete-icon.png)**Delete** action that appears on the page.
    - Click anywhere in the row other than the round check box next to the **Display name** column. In the details flyout that opens, select ![](../exchangeonline/media/modern-eac-delete-icon.png)**Delete contact** at the top of the flyout.
2. Select **Confirm** in the flyout that opens.

## Use Exchange Online PowerShell to manage mail users

To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

### Use Exchange Online PowerShell to view mail users

To return a summary list of all mail users, run the following command:

```powershell
Get-MailUser -ResultSize unlimited
```

To view detailed information about a specific mail user, replace &lt;MailUserIdentity&gt; with the name, alias, or account name of the mail user, and run the following commands:

```powershell
Get-MailUser -Identity <MailUserIdentity> | Format-List

Get-User -Identity <MailUserIdentity> | Format-List
```

For detailed syntax and parameter information, see [Get-MailUser](/en-us/powershell/module/exchangepowershell/get-mailuser) and [Get-User](/en-us/powershell/module/exchangepowershell/get-user).

### Use Exchange Online PowerShell to create mail users

To create a mail user, use the following syntax:

```powershell
New-MailUser -Name "<UniqueName>" -MicrosoftOnlineServicesID <Account> -Password (Read-Host "Enter password" -AsSecureString) [-Alias <AliasValue>] [-DisplayName "<Display Name>"] [-ExternalEmailAddress <ExternalEmailAddress>] [-FirstName <Text>] [-Initials <Text>] [-LastName <Text>]
```

This example creates a mail user for Felipe Apodaca:

- The name and display name is Felipe Apodaca (if you don't use the *DisplayName* parameter, the value of the *Name* parameter is used for the display name).
- The alias is fapodaca.
- The external email address is `fapodaca@fabrikam.com`.
- The sign in name is `fapodaca@contoso.onmicrosoft.com`.
- You're prompted to enter the password.

```powershell
New-MailUser -Name "Felipe Apodaca" -Alias fapodaca -ExternalEmailAddress fapodaca@fabrikam.com -FirstName Felipe -LastName Apodaca -MicrosoftOnlineServicesID fapodaca@contoso.onmicrosoft.com -Password (Read-Host "Enter password" -AsSecureString)
```

For detailed syntax and parameter information, see [New-MailUser](/en-us/powershell/module/exchangepowershell/new-mailuser).

### Use Exchange Online PowerShell to modify mail users

To modify existing mail users, use the following syntax:

```powershell
Set-MailUser -Identity <MailUserIdentity> [-Alias <Text>] [-DisplayName <Text>] [-EmailAddresses <ProxyAddressCollection>] [-MicrosoftOnlineServicesID <SmtpAddress>]
```

```powershell
Set-User -Identity <MailUserIdentity> [-City <Text>] [-Company <Text>] [-CountryOrRegion <CountryInfo>] [-Department <Text>] [-Fax <PhoneNumber>] [-FirstName <Text>] [-HomePhone <PhoneNumber>] [-Initials <Text>] [-LastName <Text>] [-MobilePhone <PhoneNumber>] [-Notes <Text>] [-Office <Text>] [-Phone <PhoneNumber>] [-PostalCode <String>] [-StateOrProvince <String>] [-StreetAddress <Tet>] [-Title <Text>] [-WebPage <Text>]
```

This example sets the external email address for Pilar Pinilla.

```powershell
Set-MailUser -Identity "Pilar Pinilla" -EmailAddresses pilarp@tailspintoys.com
```

This example sets the Company property for all mail users to Contoso.

```powershell
$Recip = Get-Recipient -RecipientType MailUser -ResultSize unlimited

$Recip | foreach {Set-User -Identity $_.Alias -Company Contoso}
```

This example sets the CustomAttribute1 property to the value of "Contoso Employee" for all mail users where the Company property value is Contoso.

```powershell
$Contoso = Get-User -ResultSize unlimited -Filter "(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Contoso')"

$Contoso | foreach {Set-MailUser -Identity $_ -CustomAttribute1 "Contoso Employee"}
```

This example hides all mail users from the organization's address book:

```powershell
$MEU = Get-MailUser -ResultSize unlimited

$MEU | foreach {Set-MailUser -Identity $_ -HiddenFromAddressListsEnabled $true}
```

### Use Exchange Online PowerShell to remove mail users

To remove mail users, use the following syntax:

```powershell
Remove-MailUser -Identity <MailUserIdentity>
```

This example removes the mail user for Jeffrey Zeng.

```powershell
Remove-MailUser -Identity "Jeffrey Zeng"
```

For detailed syntax and parameter information, see [Remove-MailUser](/en-us/powershell/module/exchangepowershell/remove-mailuser).

## How do you know these procedures worked?

To verify that you successfully created, modified, or removed mail users, do any of the following steps:

- In the EAC, go to the **Recipients** &gt; **Contacts** and Verify the mail user is listed (or not listed). The **Contact Type** value is **MailUser**. Select the mail contact from the list by clicking anywhere in the row other than the round check box that appears in the blank area next to the **Display name** column to view or edit the mail user's details.
- In Exchange Online PowerShell, replace &lt;MailUserIdentity&gt; with the name, email address, or alias of the mail user, and run the following command to verify that the mail user is listed (or not listed).

    ```powershell
    Get-MailUser -Identity <MailUserIdentity> | Format-List Name,Alias,DisplayName,ExternalEmailAddress
    ```
- In Exchange Online PowerShell, use the **Get-User** and **Get-MailUser** cmdlets to verify the property changes you made.

    ```powershell
    Get-MailUser | Format-List Name,CustomAttribute1
    ```

    ```powershell
    Get-User -ResultSize unlimited -Filter "RecipientTypeDetails -eq 'mailuser'" | Format-List Name,Company
    ```

## Use directory synchronization to manage mail users

In Exchange Online, directory synchronization is available for hybrid customers with on-premises and cloud mailboxes, and for fully hosted Exchange Online customers who use on-premises Active Directory exclusively.

In the Built-in security add-on for on-premises mailboxes, directory synchronization is available for customers with on-premises Active Directory.

- If you use directory synchronization to manage recipients, you can still add and manage users in the Microsoft 365 admin center, but they aren't synchronized with your on-premises Active Directory. Directory synchronization only syncs recipients from your on-premises Active Directory to the cloud, not the other direction.
- Using directory synchronization is recommended for use with the following features:

    - **Outlook Safe Sender lists and Blocked Sender lists**: For more information about how these lists affect or don't affect filtering in the service, see [User allows and blocks](/en-us/defender-office-365/how-policies-and-protections-are-combined#user-allows-and-blocks).
    - **Directory Based Edge Blocking (DBEB)**: For more information, see [Use Directory Based Edge Blocking to reject messages sent to invalid recipients](../mail-flow-best-practices/use-directory-based-edge-blocking).
    - **End user access to quarantine**: To access their quarantined messages, recipients must have a valid user ID and password in the service. For more information, see [Manage quarantined messages and files as a user](/en-us/defender-office-365/quarantine-end-user).
    - **Mail flow rules (also known as transport rules)**: When you use directory synchronization, your existing Active Directory users and groups are automatically uploaded to the cloud, so you can create mail flow rules that target specific users and/or groups without having to manually add them in the service. [Dynamic distribution groups](manage-dynamic-distribution-groups/create-manage-dynamic-distribution-groups) can't be synchronized via directory synchronization.

Get the necessary permissions and prepare for directory synchronization, as described in [What is Microsoft Entra Connect?](/en-us/entra/identity/hybrid/connect/whatis-azure-ad-connect).

### Synchronize directories with Microsoft Entra Connect

1. Activate Directory synchronization as described in [Microsoft Entra Connect Sync: Understand and customize synchronization](/en-us/azure/active-directory/hybrid/how-to-connect-sync-whatis).
2. Install and configure an on-premises computer to run Microsoft Entra Connect as described in [Prerequisites for Microsoft Entra Connect](/en-us/entra/identity/hybrid/connect/how-to-connect-install-prerequisites).
3. [Select which installation type to use for Microsoft Entra Connect](/en-us/entra/identity/hybrid/connect/how-to-connect-install-select-installation):

    - Express
    - Custom
    - [Pass-through authentication](/en-us/azure/active-directory/hybrid/how-to-connect-pta-quick-start)

Important

When you finish the Azure Active Directory Sync Tool Configuration Wizard, the **MSOL\_AD\_SYNC** account is created in your Active Directory forest. This account is used to read and synchronize your on-premises Active Directory information. In order for directory synchronization to work correctly, make sure that TCP 443 on your local directory synchronization server is open.

After configuring your sync, be sure to verify that Microsoft Entra Connect is synchronizing correctly. On the **Contacts** page in the EAC at https://admin.exchange.microsoft.com/#/contacts, verify that the list of users was correctly synchronized from your on-premises environment.