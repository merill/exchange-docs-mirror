---
layout: Conceptual
title: Override the distribution group naming policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/override-group-naming-policy
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
ms.custom:
- has-azure-ad-ps-ref
description: The group naming policy for distribution groups is applied only to groups created by users. When you or other administrators use the Exchange admin center (EAC) to create distribution groups, the group naming policy is ignored and not applied to the group name.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 9eb23fc9-3f59-4d09-9077-85c89a051ee0
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: d3788cc9-87d3-6634-95f6-8227f74642a3
document_version_independent_id: 5fc77421-6377-eb9d-b523-d718cb1d3843
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/override-group-naming-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-distribution-groups/override-group-naming-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/override-group-naming-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 56de867a-9239-b9b5-338a-6d2d4ff19db9
---

# Override the distribution group naming policy in Exchange Online | Microsoft Learn

The group naming policy for distribution groups is applied only to groups created by users and to groups created by administrators using the new Exchange admin center (new EAC). When you or other administrators use the classic Exchange admin center (classic EAC) to create distribution groups, the group naming policy is ignored and not applied to the group name.

However, if you use Exchange Online PowerShell to create or rename a distribution group, the group naming policy is applied to groups created by administrators unless you use the *IgnoreNamingPolicy* parameter to override the group naming policy.

## What do you need to know before you begin?

- Estimated time to complete: 2 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to override the group naming policy when you create a new group

To override the group naming policy, run the following command.

```PowerShell
New-DistributionGroup -Name <Group Name> -IgnoreNamingPolicy
```

For example, if the group naming policy for your organization is DG\_&lt;Group Name&gt;\_Users, run the following command to create a group named All Administrators.

```PowerShell
New-DistributionGroup -Name "All Administrators" -IgnoreNamingPolicy
```

When Microsoft Exchange creates this group, it uses All Administrators for both the *Name* and *DisplayName* parameters.

## Use Exchange Online PowerShell to override the group naming policy when you rename a group

To override the group naming policy when you rename an existing group with Exchange Online PowerShell, run the following command.

```PowerShell
Set-DistributionGroup -Identity <Old Group Name> -Name <New Group Name> -DisplayName <New Group Name> -IgnoreNamingPolicy
```

For example, let's say you created a group naming policy late one night and the next morning you realized you misspelled the text string in the prefix. The next morning, you see that a new group has already been created with the misspelled prefix. You can fix the group naming policy in the EAC, but you have to use Exchange Online PowerShell to rename the group with the misspelled name. Run the following command.

```PowerShell
Set-DistributionGroup -Identity "Government_Contracts_NWRegion" -Name "Government_ContractEstimates_NWRegion" -DisplayName "Government_ContractEstimates_NWRegion" -IgnoreNamingPolicy
```

Important

Be sure to include the *DisplayName* parameter when you rename a group. If you don't, the old name is still displayed in the shared address book on the To:, Cc:, and From: lines in email messages.

## How do you know this worked?

To verify that you've successfully created or renamed a distribution group that ignores the group naming policy, run the following commands.

```PowerShell
Get-DistributionGroup <Name> | Format-List DisplayName
```

```PowerShell
Get-OrganizationConfig | Format-List DistributionGroupNamingPolicy
```

If the format of the display name for the group is different than the one enforced by your organization's group naming policy, it worked.