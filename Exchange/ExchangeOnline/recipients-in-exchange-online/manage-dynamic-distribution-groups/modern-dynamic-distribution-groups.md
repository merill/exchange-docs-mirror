---
layout: Conceptual
title: Modern dynamic distribution groups in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/modern-dynamic-distribution-groups
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: Low
description: Learn about the changes to Modern Dynamic distribution groups in Exchange Online.
ms.topic: article
author: AshaIyengar21
f1.keywords:
- CSH
ms.author: serdars
ms.reviewer: 
audience: ITPro
ms.service: exchange-online
ms.date: 2024-06-28T00:00:00.0000000Z
locale: en-us
document_id: 4b225d9c-90c7-4b93-b66c-47b435c83e90
document_version_independent_id: 3f6ad047-c00c-df59-4886-9d827f7a147a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-dynamic-distribution-groups/modern-dynamic-distribution-groups.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-dynamic-distribution-groups/modern-dynamic-distribution-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-dynamic-distribution-groups/modern-dynamic-distribution-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 3bb5ba4a-192c-625f-5a8a-46dbaa3c265a
---

# Modern dynamic distribution groups in Exchange Online | Microsoft Learn

Dynamic distribution groups (DDGs) in Exchange Online are modernized to bring a more reliable, predictable, and better performing experience. This change reduces mail delivery latency, improve service reliability, and allow you to see the members of a DDG before sending a message.

The membership list is now stored for each DDG and is updated once every 24 hours. You know exactly to whom the message is being sent, and it also addresses potential compliance issues. Storing the calculated list of members on the DDG object allows messages to be delivered more quickly and gives our service has greater reliability.

## DDG behavior changes

The changes in behavior for dynamic distribution groups in Exchange Online are described in the following table:

| Area | Old behavior | New behavior |
| --- | --- | --- |
| Mail delivery latency | Unpredictable. The time it takes to deliver mail to a DDG depends on how complex the filters are on that DDG. | Faster and more predictable overall. You should see delivery times more in line with regular distribution groups. |
| Creation | DDGs could be used immediately after being created. | It takes 2 hours for the initial membership list to be calculated and be available for use. |
| Modification | DDGs could be used immediately after any changes were made | Users have to wait up to 2 hours for the membership list to be recalculated and links updated. |
| Membership list "freshness" | The list of members was up to date in real time. | The list of members for each DDG is refreshed every 24 hours. |

Important

The list of DDG members might become stale. For example, a user leaves a department used as a filter for the DDG. They might continue to receive mail sent to the DDG for the next 24 hours util the membership list is refreshed.

Mail flow rules (also known as transport rules) are also affected, rules use the membership list that's also refreshed once every 24 hours.

## View DDG members

To view the members of a DDG, replace &lt;DDGIdentity&gt; with the name, alias, or email address of the DDG and run the following command in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell). The command returns the calculated list of members stored on the dynamic distribution group object.

```PowerShell
Get-DynamicDistributionGroupMember -Identity <DDGIdentity>
```

For detailed parameter and syntax information, see [Get-DynamicDistributionGroupMember](/en-us/powershell/module/exchangepowershell/get-dynamicdistributiongroupmember).

Note

Don't use the old procedure for viewing members of a DDG as described in [View members of a dynamic distribution group in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/view-group-members). The old procedure returns all users that satisfy the DDG filters at the time you run the command. The old procedure doesn't return the calculated list of members that are stored on the DDG object.

## Refresh the membership of a DDG

If your DDG membership list isn't updated after the next 24-hour refresh interval, you can force a membership refresh in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell). Replace &lt;DDGIdentity&gt; with the name, alias, or email address of the DDG and run the following command:

```PowerShell
Set-DynamicDistributionGroup -Identity <DDGIdentity> -ForceMembershipRefresh
```

For detailed syntax and parameter information, see [Set-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/set-dynamicdistributiongroup)

Note

You can run the refresh command only one hour after the last membership refresh.