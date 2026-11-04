---
layout: Conceptual
title: Apply a retention policy to mailboxes in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/messaging-records-management/apply-retention-policy
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
description: You can use retention policies to group one or more retention tags and apply them to mailboxes to enforce message retention settings. A mailbox can't have more than one retention policy.
ms.topic: how-to
author: k-reagle
ms.author: kreagle
ms.assetid: 6ccc80db-d201-44f7-8d4b-473a89c14b2f
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
document_id: d901572a-dd54-8968-4c9c-4e524dda485d
document_version_independent_id: 9f03490e-5aae-ec98-19b6-8caca2b83a4e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/apply-retention-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/messaging-records-management/apply-retention-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/apply-retention-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: d0944537-a17f-7f82-a6fb-246fe950a44b
---

# Apply a retention policy to mailboxes in Exchange Online | Microsoft Learn

Note

To proactively retain or delete mailbox content for data lifecycle management in Microsoft 365, we recommend that you use [retention policies and retention labels](/en-us/purview/retention) from the [Microsoft Purview portal](https://purview.microsoft.com/), instead of messaging records management that's described on this page. However, you should continue using messaging records management to move messages to archive mailboxes.

If you currently use messaging records management, this older feature will continue to work side-by-side with retention policies and retention labels. However, we recommend that going forward, you use retention policies and retention labels instead. They provide you with a single mechanism to centrally manage both retention and deletion of content across Microsoft 365.

You can use retention policies to group one or more retention tags and apply them to mailboxes to enforce message retention settings. A mailbox can't have more than one retention policy.

Caution

Messages are expired based on settings defined in the retention tags linked to the policy. These settings include actions such moving messages to the archive or permanently deleting them. Before applying a retention policy to one or more mailboxes, we recommended that you test the policy and inspect each retention tag associated with it.

For additional management tasks related to messaging records management (MRM), see [Messaging Records Management Procedures](/en-us/purview/inactive-mailboxes-in-office-365).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Retention policies" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use the new EAC to apply a retention policy to a single mailbox

1. Sign in to the [new Exchange admin center](https://admin.exchange.microsoft.com) and navigate to **Recipients** &gt; **Mailboxes**.
2. In the list view, select the mailbox to which you want to apply the retention policy.
3. In the details panes for that mailbox, select **Mailbox**, and then for the **Retention policy** section, select **Manage mailbox policies**.
4. In the **Mailbox policies** pane, use the dropdown list box for **Retention policy** to select the policy you want to apply to the mailbox, and then select **Save**.

## Use the new EAC to apply a retention policy to multiple mailboxes

1. Sign in to the [new Exchange admin center](https://admin.exchange.microsoft.com) and navigate to **Recipients** &gt; **Mailboxes**.
2. In the list view, select the multiple mailboxes to apply the same retention policy.
3. Above the list view, select **...** for more options, and select **Mailbox policies**.
4. In the **Mailbox policies** pane, use the dropdown list box for **Retention policy** to select the policy you want to apply to the multiple mailboxes, and then select **Save**.

## Use Exchange Online PowerShell to apply a retention policy to a single mailbox

The following example applies the retention policy RP-Finance to Morris's mailbox:

```PowerShell
Set-Mailbox "Morris" -RetentionPolicy "RP-Finance"
```

For detailed syntax and parameter information, see [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).

## Use Exchange Online PowerShell to apply a retention policy to multiple mailboxes

The following example applies the new retention policy New-Retention-Policy to all mailboxes that have the old policy Old-Retention-Policy:

```PowerShell
$OldPolicy=(Get-RetentionPolicy "Old-Retention-Policy").distinguishedName
Get-Mailbox -Filter "RetentionPolicy -eq '$OldPolicy'" -Resultsize Unlimited | Set-Mailbox -RetentionPolicy "New-Retention-Policy"
```

The following example applies the retention policy RetentionPolicy-Corp to all mailboxes in the Exchange organization:

```PowerShell
Get-Mailbox -ResultSize unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Corp"
```

The following example applies the retention policy RetentionPolicy-Finance to all mailboxes in the Finance organizational unit:

```PowerShell
Get-Mailbox -OrganizationalUnit "Finance" -ResultSize Unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Finance"
```

For detailed syntax and parameter information, see [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox) and [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox).

## How do you know this worked?

To verify that you have applied the retention policy, run the [Get-Mailbox](/en-us/powershell/module/exchangepowershell/get-mailbox) cmdlet to retrieve the retention policy for the mailbox or mailboxes.

The following example retrieves the retention policy for Morris's mailbox:

```PowerShell
Get-Mailbox Morris | Select RetentionPolicy
```

The following command retrieves all mailboxes that have the retention policy RP-Finance applied:

```PowerShell
Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionPolicy -eq "RP-Finance"} | Format-Table Name,RetentionPolicy -Auto
```