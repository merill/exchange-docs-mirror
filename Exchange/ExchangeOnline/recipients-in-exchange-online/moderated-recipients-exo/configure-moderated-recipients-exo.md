---
layout: Conceptual
title: Configure moderated recipients in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/moderated-recipients-exo/configure-moderated-recipients-exo
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
description: Admin can learn how to configure the moderation settings on all recipient types in the Exchange admin center (EAC) and in PowerShell in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: f0c3db25-653f-4252-acb1-2b5ba940ab80
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-03-14T00:00:00.0000000Z
locale: en-us
document_id: 8d5de53e-fdae-32a7-acaa-aacb001f6869
document_version_independent_id: 7096b6d2-3e01-051b-c4e6-c3596bb75125
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/moderated-recipients-exo/configure-moderated-recipients-exo.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/moderated-recipients-exo/configure-moderated-recipients-exo
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/moderated-recipients-exo/configure-moderated-recipients-exo.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: becf3924-ef96-37c9-a713-9e488faa3a90
---

# Configure moderated recipients in Exchange Online | Microsoft Learn

In your Exchange Online organization, messages that are sent to moderated recipients require the approval of a moderator before they're actually delivered. For more information, see [Moderated recipients in Exchange Online](moderated-recipients-exo).

This article described how to configure moderated groups in the Exchange admin center (EAC) and all recipient types in Exchange Online Powershell.

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes
- For more granular control over messages that need approval, you can use mail flow rules (transport rules). For details, see [Use mail flow rules for message approval scenarios in Exchange Online](../../security-and-compliance/mail-flow-rules/common-message-approval-scenarios).
- The moderation parameters are available to modify the following types of recipients using the corresponding cmdlets:

    - [Set-DistributionGroup](/en-us/powershell/module/exchangepowershell/set-distributiongroup)
    - [Set-DynamicDistributionGroup](/en-us/powershell/module/exchangepowershell/set-dynamicdistributiongroup)
    - [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox)
    - [Set-MailContact](/en-us/powershell/module/exchangepowershell/set-mailcontact)
    - [Set-MailPublicFolder](/en-us/powershell/module/exchangepowershell/set-mailpublicfolder)
    - [Set-MailUser](/en-us/powershell/module/exchangepowershell/set-distributiongroup)
    - [Set-UnifiedGroup](/en-us/powershell/module/exchangepowershell/set-unifiedgroup)
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Moderated Transport" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- You can use the EAC or PowerShell to configure groups for moderation. All other recipient types can only be configured for moderation using PowerShell. To open the EAC, see [Exchange admin center in Exchange Online](../../exchange-admin-center). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to configure a moderated distribution group

Note

You can configure moderation for Microsoft 365 Groups using EAC and Exchange Online PowerShell using the **Set-UnifiedGroup** command.

Messages that the owner of the group sends to the distribution group do not need to be approved by a moderator

The following steps are basically the same for all other group types: distribution groups, dynamic distribution groups and mail-enabled security groups.

1. In the EAC, click **Recipients** &gt; **Groups** &gt; **Distribution list**.
2. In this example, we'll configure moderation for a distribution list called *All employees*. In the result pane, select **All employees** by clicking anywhere in the row other than the button option that appears in the blank area next to the **Group name** column.
3. On the **All Employees** details page, click **Settings** &gt; **Edit Message approval** and configure the following settings:

    - Click **Require moderator approval for messages sent to this group** check box. You need to do this to make the remaining settings available.
    - In the **Group moderators** list, search for users to add.
    - In the **Add senders who don't require message approval** list, search for users to add.
    - In the **Notify a sender if their messages isn't approved**, select as required.
4. When you're finished, click **Save changes**.

![Message approval settings for a distribution group.](../../exchangeonline/media/ta_mod_scenario1_allemployes.png)

## Use Exchange Online PowerShell to configure a moderated recipient

Run the following command:

```powershell
Set-<RecipientType> -Identity <Identity> -ModerationEnabled $true -ModeratedBy <recipient1,recipient2...> -ByPassModerationFromSendersOrMembers <recipient1,recipient2...> -SendModerationNotifications <Never | Always | Internal>
```

This example configures the following moderation settings for the distribution group named All Employees:

- Enable moderation for the distribution group.
- Designate David Hamilton and Yossi Ran as moderators.
- Allow the members of the distribution group named HR to bypass moderation.
- Notify internal senders if their message to the distribution group is rejected, but do not send any notifications to external senders.

To accomplish the tasks in this example scenario, run the following command:

```powershell
Set-DistributionGroup -Identity "All Employees" -ModerationEnabled $true -ModeratedBy "David Hamilton","Yossi Ran" -ByPassModerationFromSendersOrMembers HR -SendModerationNotifications Internal
```

To add or remove users from the list of moderators or recipients who bypass moderation without affecting other entries, use the following syntax:

```powershell
Set-<RecipientType> -Identity <Identity> -ModeratedBy @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -ByPassModerationFromSendersOrMembers @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}
```

This example configures the following moderation settings for the distribution group named All Employees:

- Add the user chris@contoso.com to the list of existing moderators.
- Remove the user michelle@contoso.com from the list of existing senders who bypass moderation.

```PowerShell
Set-DistributionGroup -Identity "All Employees" -ModeratedBy @{Add="chris@contoso.com"} -ByPassModerationFromSendersOrMembers @{Remove="michelle@contoso.com}"
```

## How do you know this worked?

To verify that you have successfully configured a recipient for moderation, do the following steps:

1. Send a test message to the moderated recipient.
2. Verify the designated moderators receive notification.
3. Verify the recipients who bypass moderation receive the message directly.