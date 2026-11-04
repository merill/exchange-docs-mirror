---
layout: Conceptual
title: Place a mailbox on retention hold in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold
Manager: laurawi
ms.subservice: exo-security-compliance
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
description: Placing a mailbox on retention hold suspends the processing of a retention policy or managed folder mailbox policy for that mailbox. Retention hold is designed for situations such as a user being on vacation or away temporarily.
ms.topic: how-to
author: k-reagle
ms.author: kreagle
ms.assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-06-26T00:00:00.0000000Z
locale: en-us
document_id: 951c413d-b397-8d30-387d-f8aa3118841b
document_version_independent_id: 276db9b3-d00c-b90c-464d-adf3eaa4b91b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/mailbox-retention-hold.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/messaging-records-management/mailbox-retention-hold
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/mailbox-retention-hold.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: b8ddffc9-1468-43dd-4b09-13df428fb96d
---

# Place a mailbox on retention hold in Exchange Online | Microsoft Learn

Placing a mailbox on retention hold suspends the processing of an MRM retention policy by the Managed Folder Assistant for that mailbox. Retention hold is designed for situations such as a user being on vacation or away temporarily.

During retention hold, users can log on to their mailbox and change or delete items. When you perform a mailbox search, deleted items that are past the deleted item retention period aren't returned in search results. To make sure items changed or deleted by users are preserved in legal hold scenarios, you must place a mailbox on legal hold. For more information, see [Create or remove an In-Place Hold](../create-or-remove-in-place-holds).

You can also include retention comments for mailboxes you place on retention hold. The comments are displayed in supported versions of Microsoft Outlook.

For additional management tasks related to messaging records management (MRM), see [Messaging Records Management Procedures](/en-us/purview/inactive-mailboxes-in-office-365).

## What do you need to know before you begin?

- Estimated time to complete: 1 minute.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Messaging records management" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- You can't use the Exchange admin center (EAC) to place a mailbox on retention hold. You must use Exchange Online PowerShell.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to place a mailbox on retention hold

This example places Michael Allen's mailbox on retention hold.

```PowerShell
Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true
```

For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).

## Use Exchange Online PowerShell to remove retention hold for a mailbox

This example removes the retention hold from Michael Allen's mailbox.

```PowerShell
Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false
```

For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).

## How do you know this worked?

To verify that you have successfully placed a mailbox on retention hold, use the [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox) cmdlet to retrieve the *RetentionHoldEnabled* property of the mailbox.

This command retrieves the *RetentionHoldEnabled* property for Michael Allen's mailbox.

```PowerShell
Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled
```

This command retrieves all mailboxes in the Exchange organization, filters the mailboxes that are placed on retention hold, and lists them along with the retention policy applied to each.

Important

Because *RetentionHoldEnabled* isn't a filterable property in Exchange Server, you can't use the *Filter* parameter with the **Get-Mailbox** cmdlet to filter mailboxes that are placed on retention hold on the server-side. This command retrieves a list of all mailboxes and filters on the client running Exchange Online PowerShell session. In large environments with thousands of mailboxes, this command may take a long time to complete.

```PowerShell
Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto
```

## Difference between *ElcProcessingDisabled* and *RetentionHoldEnabled*

*ElcProcessingDisabled* is another mailbox property that's related to the processing of a mailbox by the Managed Folder Assistant (the default value for this property is **False**). When the *ElcProcessingDisabled* property is set to **True** (by using the `Set-Mailbox -ElcProcessingDisabled $true` command), it prevents the Managed Folder Assistant from processing the mailbox at all. So in addition to not processing the MRM retention policy, other functions performed by the Managed Folder assistant, such as expiring items in the Recoverable Items folder by marking them for permanent removal, won't be performed. For more information, see [Set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/set-organizationconfig).

In contrast, when *RetentionHoldEnabled* is set to **True**, the Managed Folder Assistant continues to process the MRM retention policy on the mailbox (including applying retention tags to items), but it doesn't expire or archive items in folders that are visible to the user (that is, in folders in the IPM subtree of the mailbox). However, the Managed Folder Assistant continues to process items in the Recoverable Items folder, including purging expired items and archiving older items. So, setting *ElcProcessingDisabled* to **True** is more restrictive and has more consequences than setting the *RetentionHoldEnabled* property to **True**.

Another significant difference between these two mailbox properties is that the *ElcProcessingDisabled* property can be set at the organizational level with the `Set-OrganizationConfig -ElcProcessingDisabled $true` command (the default setting is **False**). This means that you could prevent the Managed Folder Assistant from processing all mailboxes in your organization. In contrast, you can only set the *RetentionHoldEnabled* property on a per mailbox basis.

Keep the following things in mind when managing the *ElcProcessingDisabled* property for a mailbox:

- If the *ElcProcessingDisabled* property is set to **False** on a mailbox, but the organizational setting is set to **True**, the organizational setting overrides the mailbox setting and the Managed Folder Assistant won't process the mailbox.
- If the *ElcProcessingDisabled* property is set to **True** on a mailbox, but the organizational setting is set to **False**, the Managed Folder Assistant won't process the mailbox.
- If an Office 365 or Microsoft 365 retention policy with a Preservation Lock is applied to a mailbox, then the setting of the *ElcProcessingDisabled* property (at both the mailbox and organizational level) will be ignored. In other words, the Managed Folder Assistant can't be disabled for any mailbox that's been assigned a retention policy that's been locked. For more information, see [Locking a retention policy](/en-us/purview/retention?tabs=table-overriden#use-preservation-lock-to-restrict-changes-to-policies).