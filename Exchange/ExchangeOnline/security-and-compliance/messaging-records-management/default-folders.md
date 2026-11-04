---
layout: Conceptual
title: Default folders that support Retention Policy Tags in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/messaging-records-management/default-folders
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
description: You can use Retention tags and retention policies to manage email lifecycle. Retention Policies contain Retention Tags, which are settings you can use to specify when a message should be automatically moved to the archive or when it should be deleted.
ms.topic: overview
author: k-reagle
ms.author: kreagle
ms.assetid: d2e2064f-4102-4018-b688-504d09da6d39
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
document_id: bd067815-de9f-6c6f-a6f1-eceb78e50366
document_version_independent_id: 2ef7cd6f-bda3-58ba-c485-afc6102ee5d6
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/default-folders.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/messaging-records-management/default-folders
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/default-folders.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 403d5d40-37b4-a1b6-9db3-eb2461ab5539
---

# Default folders that support Retention Policy Tags in Exchange Online | Microsoft Learn

Note

To proactively retain or delete mailbox content for information governance in Microsoft 365, we recommend that you use [retention policies and retention labels](/en-us/purview/retention) from the [Microsoft Purview portal](https://purview.microsoft.com/), instead of messaging records management that's described on this page. However, you should continue using messaging records management to move messages to archive mailboxes.

If you currently use messaging records management, this older feature will continue to work side-by-side with retention policies and retention labels. However, we recommend that going forward, you use retention policies and retention labels instead. They provide you with a single mechanism to centrally manage both retention and deletion of content across Microsoft 365.

You can use [Retention tags and retention policies](retention-tags-and-policies) to manage email lifecycle. Retention Policies contain Retention Tags, which are settings you can use to specify when a message should be automatically moved to the archive or when it should be deleted.

A Retention Policy Tag (RPT) is a type of retention tag that you can apply to default folders in a mailbox, such as **Inbox** and **Deleted Items**.

![Create a Retention Policy Tag (RPT).](../../exchangeonline/media/exo_retention_defaultfolders_createrpt.png)

## Supported default folders

You can create RPTs for the default folders shown in the following table.

| Folder name | Details |
| --- | --- |
| Archive | This folder is the default destination for messages archived with the Archive button in Outlook. The Archive feature provides a fast way for users to remove messages from their Inbox without deleting them.  This RPT is available only in Exchange Online. |
| Calendar | This default folder is used to store meetings and appointments. |
| Clutter | This folder contains email messages that are low priority. Clutter looks at what you've done in the past to determine the messages you're most likely to ignore. It then moves those messages to the **Clutter** folder. |
| Conversation History | This folder is created by Microsoft Lync (previously Microsoft Office Communicator). Although not treated as a default folder by Outlook, it's treated as a special folder by Exchange and can have RPTs applied. |
| Deleted Items | This default folder is used to store items deleted from other folders in the mailbox. Outlook and Outlook on the web (formerly known as Outlook Web App) users can manually empty this folder. Users can also configure Outlook to empty the folder upon closing Outlook. |
| Drafts | This default folder is used to store draft messages that haven't been sent by the user. Outlook on the web also uses this folder to save messages that were sent by the user but not submitted to the Hub Transport server. |
| Inbox | This default folder is used to store messages delivered to a mailbox. |
| Journal | This default folder contains actions selected by the user. These actions are automatically recorded by Outlook and placed in a timeline view. |
| Junk E-mail | This default folder is used to save messages marked as junk e-mail by the content filter on an Exchange server or by the anti-spam filter in Outlook. |
| Notes | This folder contains notes created by users in Outlook. These notes are also visible in Outlook on the web. |
| Outbox | This default folder is used to temporarily store messages sent by the user until they're submitted to a Hub Transport server. A copy of sent messages is saved in the Sent Items default folder. Because messages usually remain in this folder for a brief period, it isn't necessary to create an RPT for this folder. |
| RSS Feeds | This default folder contains RSS feeds. |
| Recoverable Items | This is a hidden folder in the Non-IPM sub-tree. It contains the Deletions, Versions, Purges, DiscoveryHolds, and Audits sub-folders. Retention tags for this folder move items from the Recoverable Items folder in the user's primary mailbox to the Recoverable Items folder in the user's archive mailbox. You can assign only the **Move To Archive** retention action to tags for this folder. To learn more, see [Recoverable Items folder in Exchange Online](../recoverable-items-folder/recoverable-items-folder). |
| Sent Items | This default folder is used to store messages that have been submitted to a Hub Transport server. |
| Sync Issues | This folder contains synchronization logs. |
| Tasks | This default folder is used to store tasks. To create an RPT for the Tasks folder, you have to use Exchange Online PowerShell. For more information, see [New-RetentionPolicyTag](/en-us/powershell/module/exchangepowershell/new-retentionpolicytag). After the RPT for the Tasks folder is created, you can manage it by using the Exchange admin center. |

## More Info

- RPTs are retention tags for default folders. You can only select a delete action for RPTs - either **delete and allow recovery** or **permanently delete**.
- You can't create an RPT to move messages to the archive. To move old items to archive, you can create a Default Policy Tag (DPT), which applies to the entire mailbox, or Personal Tags, which are displayed in Outlook and Outlook on the web as Archive Policies. Your users can apply them to folders or individual messages.
- You can't apply RPTs to the Contacts folder.
- You can only add one RPT for a particular default folder to a Retention Policy. For example, if a retention policy has an Inbox tag, you can't add another RPT of type Inbox to that retention policy.
- To learn how to create RPTs or other types of retention tags and add them to a retention policy, see [Create a Retention Policy](create-a-retention-policy).
- In Exchange Server and Exchange Online, a DPT also applies to the **Calendar** and **Tasks** default folders. This may result in items being deleted or moved to the archive based on the DPT settings. To prevent the DPT settings from deleting items in these folders, create RPTs with retention disabled. To prevent the DPT settings from moving items in a default folder, you can create a disabled Personal Tag with the move to archive action, add it to the retention policy, and then have users apply it to the default folder. For details, see [Prevent archiving of items in a default folder in Exchange 2010](https://techcommunity.microsoft.com/t5/exchange-team-blog/prevent-archiving-of-items-in-a-default-folder-in-exchange-2010/ba-p/603444).
- While you can apply an RPT to the 'Deleted Items' default folder, the behavior of tagged items may not always inherit the parent RPT and will honor the [principles of retention](/en-us/purview/retention), for example, if a retention tag or label was originally applied or inherited to an item, or if a retention label was automatically applied. For more information, see [Behavior of retention tags and retention labels for items moved to the Deleted Items folder](/en-us/exchange/reference/retention-deleted-items).