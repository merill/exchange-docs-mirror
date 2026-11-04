---
layout: Conceptual
title: Create a Retention Policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy
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
description: Learn how to create and manage retention policies in Exchange Online to control the email lifecycle for your organization. Follow step-by-step instructions and best practices to ensure compliance and effective data management. - msecd-doc-authoring-1012
ms.topic: how-to
author: k-reagle
ms.author: kreagle
ms.assetid: d8806c98-fea5-492f-906d-f514e25361b2
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ai-usage: ai-assisted
ms.date: 2026-05-29T00:00:00.0000000Z
locale: en-us
document_id: 2031dafe-5b8b-0edb-0fb5-0d05f2671954
document_version_independent_id: e8d75883-dc6c-9359-db15-7bd763ced4de
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/create-a-retention-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/messaging-records-management/create-a-retention-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/messaging-records-management/create-a-retention-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: eaba074d-028c-03a7-85eb-26c9fae90153
---

# Create a Retention Policy in Exchange Online | Microsoft Learn

Note

To proactively retain or delete mailbox content for data lifecycle management in Microsoft 365, we recommend that you use [Microsoft 365 retention policies and retention labels](/en-us/purview/retention) from the [Microsoft Purview portal](https://purview.microsoft.com/), instead of messaging records management that's described on this page. However, you should continue using messaging records management to move messages to archive mailboxes.

If you currently use messaging records management (MRM), this older feature will continue to work side-by-side with Microsoft 365 retention policies and retention labels. However, we recommend that going forward, you use Microsoft 365 retention policies and retention labels instead. They provide you with a single mechanism to centrally manage both retention and deletion of content across Microsoft 365.

In Exchange Online, you can use messaging records management (MRM) retention policies to manage email lifecycle. Retention policies are applied by creating retention tags, adding them to a retention policy, and applying the policy to mailbox users.

For additional management tasks related to retention policies, see the article [Messaging Records Management Procedures](/en-us/purview/inactive-mailboxes-in-office-365).

## What do you need to know before you begin?

- Estimated time to complete this task: 30 minutes.
- Procedures in this topic require specific permissions. See each procedure for its permissions information.
- Configuration for the MRM retention policies and tags is in the [Microsoft Purview portal](/en-us/purview/purview-portal).
- Mailboxes to which you apply these retention policies must reside in Microsoft 365.

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Step 1: Create a retention tag

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Messaging records management" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.

### Use the Microsoft Purview portal to create a retention tag

1. Sign in to the [Microsoft Purview portal](https://purview.microsoft.com) and navigate to **Solutions** &gt; **Data lifecycle management** &gt; **Exchange (legacy)** &gt; **MRM Retention tags**, and then select **+ New tag**.
2. On the **Define how the tag will be applied** page, select one of the following options, and then select **Next**:

    - **Automatically to entire mailbox (default)**: Select this option to create a default policy tag (DPT). You can use DPTs to create a default deletion policy and a default archive policy, which applies to all items in the mailbox.

        You can't use this configuration to create a DPT to delete voice mail items. For details about how to create a DPT to delete voice mail items, see the Exchange Online PowerShell example on this page.
    - **Automatically to default folder**: Select this option to create a retention policy tag (RPT) for a default folder such as **Inbox** or **Deleted Items**, and then select the folder.

        You can create RPTs only with the **Delete and allow recovery** or **Permanently delete** retention actions.
    - **By users to items and folders (personal)**: Select this option to create personal tags. These tags allow Outlook and Outlook on the web (formerly known as Outlook Web App. or OWA) users to apply archive or deletion settings to a message or folders that are different from the settings applied to the parent folder or the entire mailbox.
3. On the **Define retention settings** page title and options will vary depending on the type of tag you selected. Complete the following fields, and then select **Next**:

    - **Retention Period**: Select one of the following options:

        - **When the item reaches the following age (in days)**: Select this option and specify the number of days to retain items before they're moved or deleted. The retention age for all supported items except Calendar and Tasks is calculated from the date an item is received or created. Retention age for Calendar and Tasks items is calculated from the end date.
        - **Never**: Select this option to specify that items should never be deleted or moved to the archive.
    - **Retention Action**: Select one of the following actions to be taken after the item reaches its retention period:

        - **Delete and allow recovery**: Select this action to delete items but allow users to recover them using the **Recover Deleted Items** option in Outlook or Outlook on the web. Items are retained until the deleted item retention period configured for the mailbox database or the mailbox user is reached.
        - **Permanently delete**: Select this option to permanently delete the item from the mailbox database.

            Important

            While mailboxes or items are subject to holds such as Microsoft 365 retention policies or retention labels, or litigation hold, they won't be permanently deleted and will continue to be returned in eDiscovery searches.
        - **Move item to archive**: This action is available only if you're creating a DPT or a personal tag. Select this action to move items to the user's archive mailbox.
4. On the **Name your tag** page, enter a name and optional description, and then select **Next**:

    - **Name**: Enter a name for the retention tag. The tag name is for display purposes and doesn't have any impact on the folder or item a tag is applied to. Consider that the personal tags you provision for users are available in Outlook and Outlook on the web.
    - **Description**: User this optional field to enter any administrative notes or comments. The field isn't displayed to users.
5. Review and submit to create the tag with your chosen configuration.

### Use Exchange Online PowerShell to create a retention tag

Use the [New-RetentionPolicyTag](/en-us/powershell/module/exchangepowershell/new-retentionpolicytag) cmdlet to create a retention tag. Different options available in the cmdlet allow you to create different types of retention tags. Use the *Type* parameter to create a DPT (value of **All**), RPT (specify a default folder type, such as **Inbox**) or a personal tag (value of **Personal**).

The following example creates a DPT to delete all messages in the mailbox after 7 years (2,556 days):

```PowerShell
New-RetentionPolicyTag -Name "DPT-Corp-Delete" -Type All -AgeLimitForRetention 2556 -RetentionAction DeleteAndAllowRecovery
```

The following example creates a DPT to move all messages to the In-Place Archive in 2 years (730 days):

```PowerShell
New-RetentionPolicyTag -Name "DPT-Corp-Move" -Type All -AgeLimitForRetention 730 -RetentionAction MoveToArchive
```

The following example creates a DPT to delete voice mail messages after 20 days:

```PowerShell
New-RetentionPolicyTag -Name "DPT-Corp-Voicemail" -Type All -MessageClass Voicemail -AgeLimitForRetention 20 -RetentionAction DeleteAndAllowRecovery
```

The following example creates an RPT to permanently delete messages in the Junk EMail folder after 30 days:

```PowerShell
New-RetentionPolicyTag -Name "RPT-Corp-JunkMail" -Type JunkEmail -AgeLimitForRetention 30 -RetentionAction PermanentlyDelete
```

The following example creates a personal tag to never delete a message:

```PowerShell
New-RetentionPolicyTag -Name "Never Delete" -Type Personal -RetentionAction DeleteAndAllowRecovery -RetentionEnabled $false
```

## Step 2: Create a retention policy

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Messaging records management" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.

### Use the Microsoft Purview portal to create a retention policy

1. Sign in to the [Microsoft Purview portal](https://purview.microsoft.com) and navigate to **Solutions** &gt; **Data lifecycle management** &gt; **Exchange (legacy)** &gt; **MRM Retention policies**, and then select **New policy**.
2. On the **Configure your policy** page, enter a name for the retention policy, and then select **+ Add tag** to select the tags you want to add to this retention policy.

    You can create a retention policy without adding any retention tags to it, but items in the mailbox to which the policy is applied won't be moved or deleted. You can also add and remove retention tags from a retention policy after it's created.
3. On the **Choose retention tags** page, select the tags you want, and then select **Add**.

    A retention policy can contain the following tags:

    - One DPT with the **Move item to archive** action.
    - One DPT with the **Delete and allow recovery** or **Permanently delete** actions.
    - One DPT for voice mail messages with the **Delete and allow recovery** or **Permanently delete** actions.
    - One RPT per default folder such as **Inbox** to delete items.
    - Any number of personal tags.

    Note

    Although you can add any number of personal tags to a retention policy, having many personal tags with different retention settings can confuse users. We recommend linking no more than ten personal tags to a retention policy.
4. Review and submit to create your retention policy with your configurations.

You can create a retention policy without adding any retention tags to it, but items in the mailbox to which the policy is applied won't be moved or deleted. You can also add and remove retention tags from a retention policy after it's created.

### Use Exchange Online PowerShell to create a retention policy

The following example creates the retention policy RetentionPolicy-Corp and uses the *RetentionPolicyTagLinks* parameter to associate five retention tags to the policy:

```PowerShell
New-RetentionPolicy "RetentionPolicy-Corp"  -RetentionPolicyTagLinks "DPT-Corp-Delete","DPT-Corp-Move","DPT-Corp-Voicemail","RPT-Corp-JunkMail","Never Delete"
```

For detailed syntax and parameter information, see [New-RetentionPolicy](/en-us/powershell/module/exchangepowershell/new-retentionpolicy).

## Step 3: Apply a retention policy to mailbox users

After you create a retention policy, you must apply it to mailbox users. You can apply different retention policies to different set of users. For detailed instructions, see [Apply a retention policy to mailboxes](apply-retention-policy).

## How do you know this worked?

After you create retention tags, add them to a retention policy, and apply the policy to a mailbox user, the next time the MRM mailbox assistant processes the mailbox, messages are moved or deleted based on settings you configured in the retention tags.

To verify that you have applied the retention policy, do the following:

1. Replace &lt;Mailbox Identity&gt; with the name, email address, or alias of the mailbox, and run the following command in Exchange Online PowerShell command to run the MRM assistant manually against a single mailbox:

    ```PowerShell
    Start-ManagedFolderAssistant -Identity "<Mailbox Identity>"
    ```
2. Log on to the mailbox using Outlook or Outlook on the web and verify that messages are deleted or moved to an archive in accordance with the policy configuration.