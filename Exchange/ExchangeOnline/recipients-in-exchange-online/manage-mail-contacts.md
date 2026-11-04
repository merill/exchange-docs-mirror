---
layout: Conceptual
title: Manage mail contacts in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-mail-contacts
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
description: Admins can learn how to create, modify, and delete mail contacts in Exchange Online.
ms.topic: how-to
author: Swatyario
f1.keywords:
- CSH
ms.custom:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailContactWizardForm.NewMailContactIntroductionWizardPage
ms.author: adbhale
ms.assetid: 74c72aed-e9ff-4927-8eb7-c08a86e79ae0
ms.reviewer: AkshayaPrakash-PM
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-02-28T00:00:00.0000000Z
locale: en-us
document_id: 601b7a39-638c-759b-4ba2-47171cdfd542
document_version_independent_id: f2f399ee-5d99-212b-5b21-0feb1c8aee08
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-mail-contacts.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-mail-contacts
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-mail-contacts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: 39a1632b-f596-256a-59d0-aafc5ebd516a
---

# Manage mail contacts in Exchange Online | Microsoft Learn

In Exchange Online organizations, mail contacts are mail-enabled objects that contain information about people who exist outside your organization. Each mail contact has an external email address. For more information about mail contacts, see [Recipients in Exchange Online](recipients-in-exchange-online).

You manage mail contacts in the Exchange admin center (EAC) or in Exchange Online PowerShell.

## What do you need to know before you begin?

- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../exchange-admin-center).
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need permissions before you can do this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../permissions-exo/feature-permissions) article.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).

## Use the Exchange admin center to manage mail contacts

### Use the EAC to create mail contacts

1. In the [EAC](https://admin.exchange.microsoft.com), click **Recipients** &gt; **Contacts**.
2. Click **Add a mail contact** and configure the following settings in the details pane. Settings marked with an ^\*^ are required.

    - **Basic information**: Update the following:

        - **First name**
        - **Last name**
        - **Initials**
        - ^\*^**Display name**: By default, this box shows the values from the **First name**, and **Last name** boxes. You can accept this value or change it.
        - ^\*^**Alias**:
        - ^\*^**Email**: Enter the user's email address. The domain should be external to your cloud-based organization.
    - **Mail contact information (Optional)**
    - **Review mail contact**
3. When you're finished, click **Create**.

### Use the EAC to modify mail contacts

1. In the EAC, click **Recipients** &gt; **Contacts**.
2. In the list of contacts, select the mail contact by clicking anywhere in the row other than the button option that appears in the blank area next to the **Display name** column.
3. In the **Mail contact** details pane, view or edit the user's contact details under the following sections:

    - General
    - Personal information
4. When you're finished, click **Save**.

#### Contact Information

    Use the **Contact information** section, to view, or edit the user's contact information. The information on this page is displayed in the address book.

    - **Web site**
    - **Fax phone**
    - **Street**
    - **City**
    - **State/Province**
    - **ZIP/Postal code**
    - **Country/Region**

#### Organization Information

    Use the **Edit Organization** section, to record detailed information about the user's role in the organization. This information is displayed in the address book. Also, you can create a virtual organization chart that's accessible from email clients such as Outlook.

    - **Title**: Use this box to view or change the recipient's title.
    - **Department**: Use this box to view or change the department in which the user works. You can use this box to create recipient conditions for dynamic distribution groups, email address policies, or address lists.
    - **Manager**: To add a manager, enter the name and select from the drop-down list.
    - **Direct reports**: You can't modify this box. A direct report is a user who reports to a specific manager. If you've specified a manager for the user, that user appears as a direct report in the details of the manager's mailbox. For example, Kari manages Chris and Kate, so Kari is specified in the **Manager** box for Chris and Kate, and Chris and Kate appear in the **Direct reports** box in the properties of Kari's account.

### Use the EAC to remove mail contacts

1. In the EAC, click **Recipients** &gt; **Contacts**.
2. Select the mail contact that you want to remove, and then click **Delete**.

    Note

    EAC doesn't allow bulk edit of mail contacts yet.
3. Click **Confirm**.

## Use PowerShell to manage mail contacts

### Use Exchange Online PowerShell to create mail contacts

This example creates a mail contact for Debra Garcia

- The name and display name is Debra Garcia (if you don't use the *DisplayName* parameter, the value of the *Name* parameter is used for the display name).
- The alias is dgarcia.

```PowerShell
New-MailContact -Name "Debra Garcia" -ExternalEmailAddress dgarcia@tailspintoys.com -Alias dgarcia
```

For detailed syntax and parameter information, see [New-MailContact](/en-us/powershell/module/exchangepowershell/new-mailcontact).

### Use Exchange Online PowerShell to modify mail contacts

In general, use the **Get-Contact** and **Set-Contact** cmdlets to view and change organization and contact information properties. Use the **Get-MailContact** and **Set-MailContact** cmdlets to view or change mail-related properties, such as email addresses, the MailTip, custom attributes, and whether the contact is hidden from address lists.

For more information, see the following articles:

- [Get-Contact](/en-us/powershell/module/exchangepowershell/get-contact)
- [Set-Contact](/en-us/powershell/module/exchangepowershell/set-contact)
- [Get-MailContact](/en-us/powershell/module/exchangepowershell/get-mailcontact)
- [Set-MailContact](/en-us/powershell/module/exchangepowershell/set-mailcontact)

Here are some examples of using Exchange Online PowerShell to change mail contact properties:

This example configures the Title, Department, Company, and Manager properties for the mail contact Kai Axford.

```PowerShell
Set-Contact "Kai Axford" -Title Consultant -Department "Public Relations" -Company Fabrikam -Manager "Karen Toh"
```

This example sets the CustomAttribute1 property to a value of PartTime for all mail contacts and hides them from the organization's address book.

```PowerShell
$Contacts = Get-MailContact -Resultsize unlimited
$Contacts | foreach {Set-MailContact -Identity $_ -CustomAttribute1 PartTime -HiddenFromAddressListsEnabled $true}
```

This example sets the CustomAttribute15 property to a value of TemporaryEmployee for all mail contacts in the Public Relations department.

```PowerShell
$PR = Get-Contact -ResultSize unlimited -Filter "Department -eq 'Public Relations'"
$PR | foreach {Set-MailContact -Identity $_ -CustomAttribute15 TemporaryEmployee}
```

### Use Exchange Online PowerShell to remove mail contacts

To remove a mail contact, use the following syntax:

```powershell
Remove-MailContact -Identity <MailUserIdentity>
```

This example removes the mail contact for Pilar Pinilla:

```powershell
Remove-MailContact -Identity "Pilar Pinilla"
```

For detailed syntax and parameter information, see [Remove-MailContact](/en-us/powershell/module/exchangepowershell/remove-mailcontact).

## How do you know these procedures worked?

To verify that you've successfully created, modified, or removed mail contacts, do any of the following steps:

- In the EAC, click **Recipients** &gt; **Contacts**. Verify the mail contact is listed (or not listed). The **Contact Type** value is **MailContact**. Select the mail contact from the list, by clicking anywhere in the row other than the button option that appears in the blank area next to the **Display name** column to view or edit the user's details.
- In the Exchange Online PowerShell, replace &lt;MailContactIdentity&gt; with the name, email address, or alias of the mail contact, and run the following command to verify that the mail contact is listed (or not listed).

    ```PowerShell
    Get-MailContact -Identity <MailContactIdentity> | Format-List Name,Alias,DisplayName,ExternalEmailAddress
    ```
- In Exchange Online PowerShell, use the **Get-Contact** and **Get-Contact** cmdlets to verify the property changes you made.

    ```PowerShell
    Get-MailContact | Format-List Name,CustomAttribute1,HiddenFromAddressListsEnabled
    ```

    ```PowerShell
    Get-Contact -Filter "Department -eq 'Public Relations'" | Get-MailContact | Format-List Name,CustomAttribute15
    ```