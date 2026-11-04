---
layout: Conceptual
title: Create a distribution group naming policy in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy
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
description: A group naming policy lets you standardize and manage the names of distribution groups created by users in your organization. You can add specific prefix and suffix to the name of a distribution group when it's created. And you can also block specific words from being used. This helps you minimize the use of inappropriate words in group names.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: b2ffb654-345d-4be1-be8e-83d28901373e
ms.reviewer: akprakash
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2023-10-31T00:00:00.0000000Z
locale: en-us
document_id: 2cd97ce9-e627-e92b-d2a0-4bd11a4b4711
document_version_independent_id: fa4ddc52-7d71-2700-47c1-6fab83540cd4
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 86c74352-5f24-d710-259e-afb5ff875442
---

# Create a distribution group naming policy in Exchange Online | Microsoft Learn

A group naming policy lets you standardize and manage the names of distribution groups created by users in your organization. You can add specific prefix and suffix to the name of a distribution group when it's created. And you can also block specific words from being used. This helps you minimize the use of inappropriate words in group names.

A group naming policy:

- Enforces a consistent naming strategy for groups created by users.
- Identifies distribution groups in the shared address book.
- Suggests the function or membership of the group.
- Identifies the type of users who are likely members of the group.
- Identifies the geographic region the group is used in.
- Blocks inappropriate words in group names.

How does a group naming policy work? When a user creates a group, they specify a name in the Display Name field. After the group is created, Microsoft Exchange applies the group naming policy by adding any prefix or suffix that you've defined in the group naming policy. The full name is displayed in the distribution groups list in the Exchange admin center (EAC), the shared address book, and the To:, Cc:, and From: fields in email messages. If a user tries to use a word that you've blocked, they get an error message when they try to save the new group and are asked to remove the blocked word and save the group again.

Here are some examples of a group naming policy. In each, **&lt;Group Name&gt;** is a descriptive name provided by the person who creates the group. Exchange adds the prefixes and suffixes defined by the policy to the display name when the group is created.

- Text strings, with underscore characters, used for a single prefix (DG) and suffix (Users):

    DG\_&lt;Group Name&gt;\_Users
- Multiple prefixes (DG and Contoso) and one suffix (Users), using text strings:

    DG\_Contoso\_&lt;Group Name&gt;\_Users
- An attribute (Department) used for the prefix:

    Department\_&lt;Group Name&gt;

    For example, say that your school populates the Department attribute for faculty members. Here's an example of a group name created by a faculty member in the Psychology department:

    **Psychology\_Cognitive201**

    In this example, the underscore character (\_) is provided as the only text string in a second prefix to separate the department name from the group name.

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) topic.
- The maximum length for a group name is 64 characters. This includes the combined number of characters in the prefix, the group name provided by the user, and the suffix.
- The group naming policy is applied only to groups created by users. When you or other administrators use the EAC to create distribution groups, the group naming policy is ignored and not applied to the group name.
- Group names are created without spacing. We recommend that you use an underscore character (\_) or some other placeholder between text strings, attributes, and the group name.
- You can use Windows PowerShell to override the group naming policy when you create and edit a distribution group. For more information, see [Override the distribution group naming policy](override-group-naming-policy).
- For information about keyboard shortcuts that might apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to create a group naming policy

1. In the [Exchange admin center](https://admin.exchange.microsoft.com/#/) click **Recipients** &gt; **Groups**.
2. Click **Add naming policy** to add prefixes and suffixes to your group names.
3. On the **Edit group naming policy** details pane, in the **Policy** section, configure the prefix by selecting either **Attribute** or **Text** in the drop-down menu.
4. Click **Add prefix** to add more prefixes.
5. For the suffix, in the drop-down menu, select either **Attribute** or **Text**, and configure the suffix.
6. Click **Add suffix** to add more prefixes.

    After you add a prefix and suffix, notice that a preview of the group naming policy is displayed.
7. To delete a prefix or suffix from the policy, click **X**.
8. In the **Blocked words** section, add the specific words that you want to block from being used in group names and aliases.
9. When you are finished, click **Save**.

## How do you know this worked?

To verify that you've successfully created a group naming policy, do the following:

- In the EAC, click **Recipients** &gt; **Groups** &gt; **Add naming policy**.

    In the **Edit group naming policy** details pane, the group naming policy that you defined is displayed in the **Preview policy** section.
- In Windows PowerShell, run the following command to display the group naming policy.

    ```PowerShell
    Get-OrganizationConfig | Format-List DistributionGroupNamingPolicy
    ```