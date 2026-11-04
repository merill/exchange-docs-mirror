---
layout: Conceptual
title: Public attachment handling in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/public-attachment-handling
Manager: serdars
ms.subservice: ''
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
description: As an admin, you can set up both private and public attachment handling in Outlook on the web depending on how you configure your Outlook on the web mailbox policies. The settings for private (internal) and public (external) networks define how users can open, view, send, or receive attachments depending on whether a user is signed in to Outlook on the web on a computer that is part of a private or of a public network.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 2b5b8f6a-1bce-4872-8989-bac53ffafaa4
ms.reviewer: chrisda
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2023-11-17T00:00:00.0000000Z
locale: en-us
document_id: 6696de80-0bb5-cc58-cfb5-e1d8e37e50cc
document_version_independent_id: d968e24e-50b1-1071-06d7-ff000d8af60a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/public-attachment-handling.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-on-the-web/public-attachment-handling
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/public-attachment-handling.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 1f2185d1-8464-2eb4-17d2-c0a5b5c291df
---

# Public attachment handling in Exchange Online | Microsoft Learn

As an admin, you can set up both private and public attachment handling in Outlook on the web (formerly known as Outlook Web App) depending on how you configure your Outlook on the web mailbox policies. The settings for private (internal) and public (external) networks define how users can open, view, send, or receive attachments depending on whether a user is signed in to Outlook on the web on a computer that is part of a private or of a public network.

## How can I control public attachment handling?

Although there are both private (internal network) and public (external network) settings to control attachments using Outlook on the web mailbox policies, admins require more consistent and reliable attachment handling when a user signs in to Outlook on the web from a computer on a public network such as at a coffee shop or library. To set up the ability to enforce attachment handling from external networks for an entire organization in Exchange Online, first use the [Set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/set-organizationconfig) cmdlet, set the *PublicComputersDetectionEnabled* parameter to `$true`, configure the correct Outlook on the web mailbox policy either by using the Exchange admin center (EAC) or the [Set-OwaMailboxPolicy](/en-us/powershell/module/exchangepowershell/set-owamailboxpolicy) cmdlet and create claim rules in AD FS. Enabling this setting on the [Set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/set-organizationconfig) cmdlet and creating the claim rules enable Exchange Online to tell if a user is signing in to Outlook on the web from a private and public network or computer.

The Outlook on the web mailbox policy parameters in the following table should be set to `$true` to enable an admin to control attachment handling for public computers and networks.

| Parameter\* | Description |
| --- | --- |
| *DirectFileAccessOnPublicComputersEnabled* | Specifies left-click and other options available for attachments when the user has signed in to Outlook on the web from a computer outside of a private or corporate network. If this parameter is set to `$true`, **Open** and other options are available. If it's set to `$false`, the **Open** option is disabled. |
| *ForceWacViewingFirstOnPublicComputers* | Specifies whether a user who signed in to Outlook on the web from a computer outside of a private or corporate network can open an Office file directly without first viewing it as a webpage. |
| *WacViewingOnPublicComputersEnabled* | Specifies whether a user who has signed in to Outlook on the web from a computer outside of the corporate network can view supported Office files using Outlook on the web. |

## What do you need to know before you begin?

- Procedures in this topic require specific permissions. See each procedure for information related to each procedure's permissions.
- [Create one or more mailboxes for users](../../recipients-in-exchange-online/create-user-mailboxes).
- [Enable Outlook on the web on a user's mailbox](../../recipients-in-exchange-online/manage-user-mailboxes/enable-or-disable-outlook-web-app) if it has been disabled.
- Verify that cookies have been enabled in the Web browser for all the users in your organization.
- Set up and configure single sign-on (SSO) using AD FS:

    - [Checklist: Use AD FS to implement and manage single sign-on](/en-us/windows-server/identity/ad-fs/deployment/checklist--implementing-a-federated-web-sso-design)
    - [Set up ADFS for Single Sign-On](/en-us/office365/troubleshoot/active-directory/set-up-adfs-for-single-sign-on)
    - [Configure single sign on](/en-us/azure/active-directory/hybrid/how-to-connect-sso)
- For information about how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Task 1 - Enable public attachment handling for your organization

Run the following command:

```PowerShell
Set-OrganizationConfig -PublicComputersDetectionEnabled $true
```

Note

Setting this parameter to `$true` won't affect the settings for the following parameters:

- *ForceWacViewingFirstOnPublicComputers*
- *WSSAccessOnPublicComputersEnabled*
- *UNCAccessOnPublicComputersEnabled*

## Task 2 - Add and create claim rules in AD FS 2.0

You must create a custom claim rule because an AD FS server relies on the presence of the `x-ms-proxy` claim to detect whether user is coming from an internal or external network. When an AD FS proxy is deployed for external or public access, and if the user is coming from outside a private network, there's a `x-ms-proxy` claim sent from AD FS proxy to an AD FS server. For more information about claim rules in AD FS, see [Create a Rule to Send Claims Using a Custom Rule](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807049%28v=ws.11%29).

1. On the **Start Screen**, type **AD FS Management**, and then press **Enter**.
2. In AD FS console tree, go to **AD FS\Trust Relationships** &gt; **Relying Party Trusts** and select **O365 Identity Platform**.
3. In **O365 Identity Platform**, select **Edit Claim Rules** &gt; **Add Rule** &gt; **Issuance Transform Rules**.
4. On the **Select Rule Template** page, under **Claim rule template**, select **Send Claims Using a Custom Rule** from the list, and then select **Next**.
5. On the **Configure Rule** page under **Claim rule name**, type the display name for this rule.
6. Under **Custom rule**, input the following text:

    ```text
    exists ([Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) => issue(Type = "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value = "false");
    ```
7. Next, input the following text:

    ```text
    NOT exists ([Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) => issue(Type = "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value = "true");
    ```
8. Select **Finish**.
9. In the **Edit Claim Rules** dialog box, select **OK** to save the rule.

## Task 3 - Enable public attachment handling on an Outlook on the web mailbox policy

### Use EAC to enable public attachment handling settings

1. In the [EAC](https://admin.exchange.microsoft.com), select **Roles** &gt; **Outlook web app policies**. Or, use [**Outlook web app policies**](https://admin.exchange.microsoft.com/#/owapolicies).
2. Select the mailbox policy by clicking anywhere in the row other than the button option that appears in the blank area next to the **Name** column.
3. In the **Details** flyout that opens, select **Manage access**.
4. Under **File access**, select how users can view and access attachments from public or private computers:

    - Public or shared computer: If set to **Enabled**, users can open attachments by selecting them and then selecting **Open**.
    - Private computer: If set to **Enabled**, users can open attachments by selecting them and then selecting **Open**.
5. Select **Save changes** to update the policy.

### Use Exchange Online PowerShell to enable public attachment handling settings

Run the following command:

```PowerShell
Set-OwaMailboxPolicy -Identity MyOWAPublicPolicy -DirectFileAccessOnPublicComputersEnabled $true -ForceWacViewingFirstOnPublicComputers $true -WacViewingOnPublicComputersEnabled $true
```

## What you need to know about attachments?

An attachment can be a file that's created in any program, for example, a Word document, an Excel spreadsheet, a .wav file, or a bitmap file. Users can attach or include one or more files on any item that they create in their mailbox, for example, an email message, calendar item, or contact. Outlook on the web allows you to send and receive many common files types continuously.

Some attachments might be removed or blocked by an antivirus software used by your organization, by the organization of the recipients of your email, or you might be required to save them on your computer before you can open them. By default, Outlook on the web allows you to open attached Word, Excel, PowerPoint, text files and many media files directly. The files you can open from Outlook on the web vary depending on your account settings. The following list describes the default file name extensions that you can open in Outlook on the web.

**File name extensions allowed by default**:

- .avi
- .bmp
- .doc
- .doc
- .docm
- .docx
- .gif
- .jpeg
- .mp3
- .one
- .pdf
- .png
- .ppsm
- .ppsx
- .ppt
- .pptm
- .pptx
- .pub
- .rpmsg
- .rtf
- .tif
- .txt
- .vsd
- .wav
- .wma
- .wmv
- .xls
- .xls
- .xlsb
- .xlsm
- .xlsx