---
layout: Conceptual
title: Troubleshoot dynamic distribution group membership issues | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/troubleshoot-ddg-membership-issues
Manager: serdars
ms.subservice: exo-groups
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn how to troubleshoot dynamic distribution groups membership issues.
ms.topic: troubleshooting-general
author: SerdarSoysal
f1.keywords:
- CSH
ms.custom:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDynamicGroupWizardForm.CreateDynamicGroupInformationWizardPage
ms.author: serdars
ms.assetid: 8ef85d0a-41df-4b5c-b8e7-ca8d09c048ca
ms.reviewer: AkshayaPrakash-PM
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-09-08T00:00:00.0000000Z
locale: en-us
document_id: fff0f079-f2d9-7903-5f23-a96b5f176827
document_version_independent_id: b3cd3389-12d6-bfdf-6802-2a8775c02cee
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-dynamic-distribution-groups/troubleshoot-ddg-membership-issues.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-dynamic-distribution-groups/troubleshoot-ddg-membership-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-dynamic-distribution-groups/troubleshoot-ddg-membership-issues.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: ec12e119-5f80-3f3a-2393-c420c8a1de91
---

# Troubleshoot dynamic distribution group membership issues | Microsoft Learn

This article describes the remedies that can be applied when troubleshooting issues related to the membership of a dynamic distribution group (DDG).

## There are no members in my dynamic distribution group

If you're not seeing any members in your DDG, it may be because of one of the following reasons:

1. **The initial membership list is still being calculated.** When a DDG is created, a background process calculates the membership list. The calculation can take up to 2 hours to complete for DDGs with more than 5,000 members. During this time, the DDG has no members. For DDGs with 5,000 members or fewer, the membership list is populated immediately.
2. **The membership list is being recalculated.** When the membership rules of an existing DDG are modified, a background process recalculates the membership list. The recalculation can take up to 2 hours (for DDGs with 5,000 or more members) to complete. During recalculation, the DDG continues to use the previous membership list.
3. **No recipients match the membership rules.** Check the membership rules again to see if you need to change them. For information on procedures that tell you how to do this, see [Create a dynamic distribution group](create-manage-dynamic-distribution-groups).

For details on the timing of membership population and recalculation, see [Dynamic distribution group membership lifecycle](create-manage-dynamic-distribution-groups#dynamic-distribution-group-membership-lifecycle).

## The members of my DDG don't match what I expect

If the members of your DDG don't match what you expect, you can verify what the membership rules currently return by previewing them. See [Preview dynamic distribution group membership](create-manage-dynamic-distribution-groups#preview-dynamic-distribution-group-membership).

If the preview returns the recipients you expect but the DDG members don't match, the membership list might be stale (the system refreshes members at least once every 24 hours), or a background process might still be recalculating membership after a recent change to the rules. For details on the timing, see [Dynamic distribution group membership lifecycle](create-manage-dynamic-distribution-groups#dynamic-distribution-group-membership-lifecycle).

If the preview also doesn't return the expected recipients, the membership rules likely need to be adjusted. See [Create a dynamic distribution group](create-manage-dynamic-distribution-groups) for information on managing membership rules.

## When was my dynamic distribution group last refreshed?

You can view the last time your DDG was refreshed by using Exchange admin center (EAC) or by using Exchange Online PowerShell.

- In the EAC, select **Recipients &gt; Groups &gt; Dynamic distribution list**. You can view when each DDG was last refreshed in the **Last refreshed** column.

[![Screenshot that shows the page on which you can view a DDG's last refreshed data.](../../exchangeonline/media/ddg-last-refreshed-data.png)](../../exchangeonline/media/ddg-last-refreshed-data.png#lightbox)

- With Exchange Online PowerShell, use the **Get-DynamicDistributionGroup** command to retrieve the **CalculatedMembershipUpdateTime** property, which indicates when the DDG was last refreshed. Replace `<DDGIdentity>` with the name, alias, or email address of the DDG, and run the following command:

```PowerShell
(Get-DynamicDistributionGroup -Identity <DDGIdentity>).CalculatedMembershipUpdateTime
```

## I want to force refresh the membership list of a dynamic distribution group

You might want to consider forcing a membership refresh on the DDG if:

1. The DDG membership list isn't populated more than 2 hours after the group was created.
2. The DDG membership list isn't recalculated more than 2 hours after you modified the membership rules of the group.
3. The DDG membership list isn't refreshed within the expected 24-hour refresh interval.

To perform a refresh, replace `<DDGIdentity>` with the name, alias, or email address of the DDG in the following command in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps&amp;preserve-view=true), and run it:

```PowerShell
Set-DynamicDistributionGroup -Identity <DDGIdentity> -ForceMembershipRefresh
```

Note

You can run the refresh command only after more than 1 hour has passed since the last membership refresh. You can only refresh DDGs using Exchange Online PowerShell. You can't refresh DDGs in EAC.

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).