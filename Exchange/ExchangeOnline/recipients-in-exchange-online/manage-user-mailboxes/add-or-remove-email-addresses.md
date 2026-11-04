---
layout: Conceptual
title: Add or remove email addresses for a mailbox in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/add-or-remove-email-addresses
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
description: You can configure more than one email address for the same mailbox. The additional addresses are called proxy addresses. A proxy address lets a user receive email that's sent to a different email address. Any email message sent to the user's proxy address is delivered to their primary email address, which is also known as the primary SMTP address or the default reply address.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-05-30T00:00:00.0000000Z
locale: en-us
document_id: 6c27828c-9c2d-cf0d-ebe5-a432776e00a0
document_version_independent_id: f71803ad-44cf-5922-9d19-65ff92e0d574
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/add-or-remove-email-addresses.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-user-mailboxes/add-or-remove-email-addresses
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/add-or-remove-email-addresses.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 29d77010-d350-e474-5005-a854aa58e2ed
---

# Add or remove email addresses for a mailbox in Exchange Online | Microsoft Learn

You can configure more than one email address for the same mailbox. The additional addresses are called proxy addresses. A proxy address lets a user receive email that's sent to a different email address. Any email message sent to the user's proxy address is delivered to their primary email address, which is also known as the primary SMTP address or the default reply address.

Tip

You can also use the Microsoft 365 admin center to add or remove email addresses for user mailboxes. For more information, see [Add another email alias for a user](/en-us/microsoft-365/admin/email/add-another-email-alias-for-a-user).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 2 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Add an email address to a user mailbox

### Use the Exchange admin center (EAC) to add an email address

1. In the EAC, navigate to **Recipients** &gt; **Mailboxes**.
2. In the list of user mailboxes, click the mailbox that you want to add an email address to. A display pane is shown for the selected user mailbox.
3. Under **General** &gt; **Email addresses**, click the **Manage email address types** link.
4. The **Manage email address types** display pane is shown. You can view all the email addresses associated with this user mailbox. Each email address type has one default reply address. The default reply address is displayed in bold.
5. Click ![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif)**Add email address type**, and then click **SMTP** to add an SMTP email address to this mailbox. SMTP is the default email address type. You can also add custom addresses to a mailbox.
6. Type the alias for the new SMTP address in the **Email address:\*** box, select the domain from the dropdown, and then click **OK**.
7. Click **Save** to save the change.

### Use Exchange Online PowerShell to add an email address

The email addresses associated with a mailbox are contained in the *EmailAddresses* property for the mailbox. Because it can contain more than one email address, the *EmailAddresses* property is known as a multivalued property. The following examples show different ways to modify a multivalued property.

This example shows how to add an SMTP address to the mailbox of Dan Jump.

```PowerShell
Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}
```

This example shows how to add multiple SMTP addresses to a mailbox.

```PowerShell
Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}
```

For more information about how to use this method of adding and removing values for multivalued properties, see [Modifying Multivalued Properties](../../modifying-multivalued-properties-exchange-2013-help).

For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).

## Remove an email address from a user mailbox

### Use the EAC to remove an email address

1. In the EAC, navigate to **Recipients** &gt; **Mailboxes**.
2. In the list of user mailboxes, click the mailbox that you want to remove an email address from. A display pane is shown for the selected user mailbox.
3. Under **General** &gt; **Email addresses**, click the **Manage email address types** link.
4. In the list of email addresses, select the address you want to remove, and then click the **Remove** icon.
5. Click **Save** to save the change.

### Use Exchange Online PowerShell to remove an email address

This example shows how to remove an email address from the mailbox of Janet Schorr.

```PowerShell
Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}
```

This example shows how to remove multiple addresses from a mailbox.

```PowerShell
Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}
```

For more information about how to use this method of adding and removing values for multivalued properties, see [Modifying Multivalued Properties](../../modifying-multivalued-properties-exchange-2013-help).

For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).

## Use Exchange Online PowerShell to add email addresses to multiple mailboxes

You can add a new email address to multiple mailboxes at one time by using Exchange Online PowerShell and a comma separated values (CSV) file.

This example imports data from C:\Users\Administrator\Desktop\AddEmailAddress.csv, which has the following format.

```console
Mailbox,NewEmailAddress
Dan Jump,danj@northamerica.contoso.com
David Pelton,davidp@northamerica.contoso.com
Kim Akers,kima@northamerica.contoso.com
Janet Schorr,janets@northamerica.contoso.com
Jeffrey Zeng,jeffreyz@northamerica.contoso.com
Spencer Low,spencerl@northamerica.contoso.com
Toni Poe,tonip@northamerica.contoso.com
```

The column names in the first row of this CSV file ( `Mailbox,NewEmailAddress`) are arbitrary. Whatever you use for column names, make sure you use the same column names in Exchange Online PowerShell command.

Run the following command to use the data in the CSV file to add the email address to each mailbox specified in the CSV file.

```PowerShell
Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}
```