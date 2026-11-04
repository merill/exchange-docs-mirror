---
layout: Conceptual
title: Shared mailboxes in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/shared-mailboxes
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
description: 'Summary: About shared mailboxes in Exchange Online, and how to create them.'
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: fdce3587-ed95-4433-9931-4cf74b52e8e0
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2018-06-26T00:00:00.0000000Z
locale: en-us
document_id: 488ecf85-5f6d-3abd-4253-8527b5082340
document_version_independent_id: ec414c0f-4ee4-bbd1-3851-3e4db0c97593
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/shared-mailboxes.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/shared-mailboxes
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/shared-mailboxes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 42d3855c-adf3-4157-fd38-09f2ffe5ae82
---

# Shared mailboxes in Exchange Online | Microsoft Learn

Shared mailboxes make it easy for a group of people in your company to monitor and send email from a common account, such as `info@contoso.com` or `support@contoso.com`. When a person in the group replies to a message sent to the shared mailbox, the email looks like it was sent by the shared mailbox, not from the individual user.

**Notes**:

- You should create your shared mailbox in the Microsoft 365 admin center. For more information, see [Create a shared mailbox](/en-us/microsoft-365/admin/email/create-a-shared-mailbox).
- Creating a shared mailbox in Exchange Online also creates an active user account with a system-generated (unknown) password. To block sign-in for this account, see [Block sign-in for the shared mailbox account](/en-us/microsoft-365/admin/email/create-a-shared-mailbox#block-sign-in-for-the-shared-mailbox-account).
- If your organization uses a hybrid Exchange environment, you should use the Exchange admin center (EAC) in your on-premises Exchange organization to create and manage shared mailboxes. To learn more about shared mailboxes, see [Shared mailboxes](../collaboration/shared-mailboxes/shared-mailboxes).
- When users move items from one folder to another in a shared mailbox, a copy of the item is stored in the [Recoverable Items](../security-and-compliance/recoverable-items-folder/recoverable-items-folder) folder.

## Use the EAC to create a shared mailbox

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../permissions-exo/feature-permissions) topic.

1. Open the EAC [Exchange admin center](../exchange-admin-center).
2. Go to **Recipients** &gt; **Mailboxes** and then click **Add a shared mailbox**.
3. Fill in the required fields:

    - **Display Name**
    - **Email address**
    - **Alias**
4. Click **Create** to save your changes and create the shared mailbox.
5. Under the **Next steps** section, click the **Add users to this mailbox** link.
6. To grant Full Access or Send As permissions, click the **Add users** button, and then select or search the users you want to grant permissions to. Confused about which permission to use? See Which permissions should you use? later in this topic.

    Note

    The Full Access permission allows a user to open the mailbox as well as create and modify items in it. The Send As permission allows anyone other than the mailbox owner to send email from this shared mailbox. Both permissions are required for successful shared mailbox operation.
7. Click **Save** to save your changes and create the shared mailbox.

### Use the EAC to edit shared mailbox delegation

1. In the EAC, go to **Recipients** &gt; **Mailboxes**. Select the shared mailbox, and then click **Manage mailbox delegation**![Delegation icon.](../exchangeonline/media/new-eac-shared-mailbox-delegation.png).
2. To grant or remove Full Access (Read and manage) and Send As permissions, click **Edit** next to the permission type.
3. On the Manage mailbox delegation page, you can remove permissions already added by clicking on the users listed (if any) or grant the permission by clicking **Add permissions** and then select the users you want to grant permissions to.

    Note

    The Full Access permission allows a user to open the mailbox as well as create and modify items in it. The Send As permission allows anyone other than the mailbox owner to send email from this shared mailbox. Both permissions are required for successful shared mailbox operation.
4. Click **Save** to save your changes.
5. Click **Close** to close the Mailbox permissions added/removed page.

## Use a shared mailbox

To learn how users can access and use shared mailboxes, check out the following articles:

- [Open and use a shared mailbox in Outlook for Windows](https://support.microsoft.com/office/d94a8e9e-21f1-4240-808b-de9c9c088afd)
- [Open and use a shared mailbox in Outlook on the web](https://support.microsoft.com/office/98b5a90d-4e38-415d-a030-f09a4cd28207)
- [Open and use a shared mailbox in Outlook mobile](https://support.microsoft.com/office/f866242c-81b2-472e-8776-6c49c5473c9f)

## Use Exchange Online PowerShell to create a shared mailbox

To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

This example creates the shared mailbox Sales Department and grants Full Access and Send on Behalf permissions for the security group MarketingSG. Users who are members of the security group will be granted the permissions to the mailbox.

Note

This example assumes that you've already created the security group MarketingSG and that security group is mail-enabled. See [Manage mail-enabled security groups](../recipients-in-exchange-online/manage-mail-enabled-security-groups).

```PowerShell
New-Mailbox -Shared -Name "Sales Department" -DisplayName "Sales Department" -Alias Sales | Set-Mailbox -GrantSendOnBehalfTo MarketingSG | Add-MailboxPermission -User MarketingSG -AccessRights FullAccess -InheritanceType All
```

For detailed syntax and parameter information, see [New-Mailbox](/en-us/powershell/module/exchangepowershell/new-mailbox).

## Which permissions should you use?

You can use the following permissions with a shared mailbox.

- **Full Access**: The Full Access permission lets a user open the shared mailbox and act as the owner of that mailbox. After accessing the shared mailbox, a user can create calendar items; read, view, delete, and change email messages; create tasks and calendar contacts. However, a user with Full Access permission can't send email from the shared mailbox unless they also have Send As or Send on Behalf permission.
- **Send As**: The Send As permission lets a user impersonate the shared mailbox when sending mail. For example, if Kweku logs into the shared mailbox Marketing Department and sends an email, it will look like the Marketing Department sent the email.
- **Send on Behalf**: The Send on Behalf permission lets a user send email on behalf of the shared mailbox. For example, if John logs into the shared mailbox Reception Building 32 and sends an email, it look like the mail was sent by "John on behalf of Reception Building 32". You can't use the EAC to grant Send on Behalf permissions, you must use **Set-Mailbox** cmdlet with the *GrantSendonBehalf* parameter.

## More information

For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../accessibility/keyboard-shortcuts-in-admin-center).