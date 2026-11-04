---
layout: Conceptual
title: Add retention tags to or remove retention tags from a retention policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/messaging-records-management/add-or-remove-retention-tags
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
description: You can add retention tags to a retention policy when the policy is created or any time thereafter. For details about how to create a retention policy, including how to simultaneously add retention tags, see Create a Retention Policy.
ms.topic: how-to
author: k-reagle
ms.author: kreagle
ms.assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
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
document_id: 653668e6-323e-340e-9939-7d4eeaad80da
document_version_independent_id: cd8acecd-1a17-1419-51c7-a8331d01894d
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/add-or-remove-retention-tags.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/messaging-records-management/add-or-remove-retention-tags
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/add-or-remove-retention-tags.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 4bf0171e-21c5-3515-4ed6-3a853d60b930
---

# Add retention tags to or remove retention tags from a retention policy in Exchange Online | Microsoft Learn

Important

Refer to the [Microsoft 365 security center](https://security.microsoft.com/homepage) and the [Microsoft Purview portal](https://purview.microsoft.com/) for Exchange security and compliance features. They are no longer available in the new [Exchange admin center](https://admin.exchange.microsoft.com).

Note

To proactively retain or delete mailbox content for information governance in Microsoft 365, we recommend that you use [Microsoft 365 retention policies and retention labels](/en-us/purview/retention) from the [Microsoft Purview portal](/en-us/purview/purview-portal), instead of messaging records management that's described on this page. However, you should continue using messaging records management to move messages to archive mailboxes.

If you currently use messaging records management, this older feature will continue to work side-by-side with retention policies and retention labels. However, we recommend that going forward, you use Microsoft 365 retention policies and retention labels instead. They provide you with a single mechanism to centrally manage both retention and deletion of content across Microsoft 365.

You can add retention tags to a retention policy when the policy is created or anytime thereafter. For details about how to create a retention policy, including how to simultaneously add retention tags, see [Create a Retention Policy](create-a-retention-policy).

A retention policy can contain the following retention tags:

- One or more retention policy tags (RPTs) for supported default folders
- One default policy tag (DPT) with the **Move item to archive** (Microsoft Purview portal) or **Move to Archive** (Classic EAC) action
- One DPT with the **Delete and allow recovery** or **Permanently delete** actions
- One DPT for voice mail
- Any number of personal tags

For more information about retention tags, see [Retention tags and retention policies](retention-tags-and-policies).

## What do you need to know before you begin?

- Estimated time to completion: 10 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Messaging records management" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- Configuration to add or remove retention tags is in the [Microsoft Purview portal](/en-us/purview/purview-portal).
- Retention tags aren't applied to a mailbox until they're linked to a retention policy and the Managed Folder Assistant processes the mailbox. Use the [Start-ManagedFolderAssistant](/en-us/powershell/module/exchangepowershell/start-managedfolderassistant) cmdlet to manually trigger the assistant to process a specified mailbox.

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use the Microsoft Purview portal to add or remove retention tags

1. Sign in to the [Microsoft Purview portal](https://purview.microsoft.com/) and navigate to **Solutions** &gt; **Data lifecycle management** &gt; **Exchange (legacy)** &gt; **MRM Retention policies**.
2. In the list view, select the retention policy to which you want to add retention tags, and then select **Edit**.
3. On the **Configure your policy** page, use the following options:

    - To add and remove retention tags to and from the retention policy: Select **+ Add tag**, and on the **Choose retention tags** pane, you can select new retention tags and remove already selected retention tags. When the required retention tags are selected, select **Add**.
    - To just remove retention tags: In the view list of retention tags, use the Delete icon for a retention tag that you want to remove.

## Use Exchange Online PowerShell to add or remove retention tags

The following example adds the retention tags VPs-Default, VPs-Inbox, and VPs-DeletedItems to the retention policy RetPolicy-VPs, which doesn't already have retention tags linked to it:

Caution

If the policy has retention tags linked to it, this command replaces the existing tags.

```PowerShell
Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"
```

The following example adds the retention tag VPs-DeletedItems to the retention policy RetPolicy-VPs, which already has other retention tags linked to it:

```PowerShell
$TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
$TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList
```

The following example removes the retention tag VPs-Inbox from the retention policy RetPolicy-VPs:

```PowerShell
$TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
$TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList
```

For detailed syntax and parameter information, see [set-RetentionPolicy](/en-us/powershell/module/exchangepowershell/set-retentionpolicy) and [get-RetentionPolicy](/en-us/powershell/module/exchangepowershell/get-retentionpolicy).

## How do you know this worked?

To verify that you have successfully added or removed a retention tag from a retention policy, use the [get-RetentionPolicy](/en-us/powershell/module/exchangepowershell/get-retentionpolicy) cmdlet to verify the *RetentionPolicyTagLinks* property.

This example uses the **Get-RetentionPolicy** cmdlet to retrieve retention tags added to the Default MRM Policy and pipes them to the **Format-Table** cmdlet to output only the name property of each tag.

```PowerShell
(Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name
```