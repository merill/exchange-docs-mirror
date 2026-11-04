---
layout: Conceptual
title: Mail-enable or mail-disable a public folder in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/collaboration-exo/public-folders/enable-or-disable-mail-for-public-folder
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
description: Public folders are designed for shared access and provide an easy and effective way to collect, organize, and share information with other people in your workgroup or organization. Mail-enabling a public folder allows users to post to the public folder by sending an email message to it. When a public folder is mail-enabled additional settings become available for the public folder in the Exchange admin center (EAC), such as email addresses and mail quotas. In Exchange Online PowerShell, before a public folder is mail-enabled, you use the Set-PublicFolder cmdlet to manage all of its settings. After the public folder is mail-enabled, you use the Set-PublicFolder and the Set-MailPublicFolder cmdlets to manage the settings.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-09-08T00:00:00.0000000Z
locale: en-us
document_id: 305d82b6-159b-bbb7-f2bf-d13a022bccd9
document_version_independent_id: 32030c1a-9e9a-81ad-487e-e5af659804eb
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/collaboration-exo/public-folders/enable-or-disable-mail-for-public-folder.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collaboration-exo/public-folders/enable-or-disable-mail-for-public-folder
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/collaboration-exo/public-folders/enable-or-disable-mail-for-public-folder.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 2fdcbd91-cd09-a0e4-9b1b-f9cccf11c612
---

# Mail-enable or mail-disable a public folder in Exchange Online | Microsoft Learn

Public folders are designed for shared access and provide an easy and effective way to collect, organize, and share information with other people in your workgroup or organization. Mail-enabling a public folder allows users to post to the public folder by sending an email message to it. When a public folder is mail-enabled, additional settings become available for the public folder in the Exchange admin center (EAC), such as email addresses and mail quotas. In Exchange Online PowerShell, before a public folder is mail-enabled, you use the **Set-PublicFolder** cmdlet to manage all of its settings. After the public folder is mail-enabled, you use the **Set-PublicFolder** and the **Set-MailPublicFolder** cmdlets to manage the settings.

If you want users on the internet to send mail to a mail-enabled public folder, you need to set additional permissions using the **Add-PublicFolderClientPermission** cmdlet.

For other management tasks related to public folders, see [Public folder procedures in Microsoft 365 or Office 365 and Exchange Online](public-folders).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes
- To ensure that users on the internet can send e-mail messages to a mail-enabled public folder, the public folder needs to have at least the *CreateItems* access right granted to the Anonymous account. If you want to learn how to do this, check out Allow anonymous users to send email to a mail-enabled public folder.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Public folders" entry in the topic.
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to mail-enable or mail-disable a public folder

1. Navigate to **Public folders** &gt; **Public folders**.
2. In the list view, select the public folder that you want to mail-enable or mail-disable.
3. In the details pane, under **General**, select or unselect the **Mail-enabled** checkbox.
4. Select **Save**.

If you want external users to send mail to this public folder, make sure you follow the steps in Allow anonymous users to send email to a mail-enabled public folder.

## Use Exchange Online PowerShell to mail-enable a public folder

This example mail-enables the public folder Help Desk.

```PowerShell
Enable-MailPublicFolder -Identity "\Help Desk"
```

This example mail-enables the public folder Reports under the Marketing public folder, but hides the folder from address lists.

```PowerShell
Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True
```

If you want external users to send mail to this public folder, make sure you follow the steps in Allow anonymous users to send email to a mail-enabled public folder.

For detailed syntax and parameter information, see [Enable-MailPublicFolder](/en-us/powershell/module/exchangepowershell/enable-mailpublicfolder).

## Use Exchange Online PowerShell to mail-disable a public folder

This example mail-disables the public folder Marketing\Reports.

```PowerShell
Disable-MailPublicFolder -Identity "\Marketing\Reports"
```

For detailed syntax and parameter information, see [Disable-MailPublicFolder](/en-us/powershell/module/exchangepowershell/disable-mailpublicfolder).

## Allow anonymous users to send email to a mail-enabled public folder

You can use either Outlook or Exchange Online PowerShell to set permissions on a public folder's Anonymous account. You can't use the EAC to set permissions on the Anonymous account.

**Use Outlook to set permissions for the Anonymous account**

1. Open Microsoft Outlook using an account that is granted Owner permissions on the mail-enabled public folder you want anonymous users to send mail to.
2. Go to **Public folders - &lt;user's name&gt;**.
3. Navigate to the public folder you want to change.
4. Right-click on the public folder, select **Properties**, and then select the **Permissions** tab.
5. Select the **Anonymous** account, select **Create items** under **Write**, and then select **OK**.

**Use Exchange Online PowerShell to set permissions for the Anonymous account**

This example sets the `CreateItems` permission for the Anonymous account on the "Customer Feedback" mail-enabled public folder.

```PowerShell
Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous
```

For detailed syntax and parameter information, see [Add-PublicFolderClientPermission](/en-us/powershell/module/exchangepowershell/add-publicfolderclientpermission).