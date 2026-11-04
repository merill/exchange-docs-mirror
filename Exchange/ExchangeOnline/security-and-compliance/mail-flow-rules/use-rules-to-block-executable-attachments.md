---
layout: Conceptual
title: Use mail flow rules to block messages with executable attachments in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-block-executable-attachments
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: serdars
author: serdars
ms.date: 2026-03-11T00:00:00.0000000Z
audience: ITPro
ms.topic: how-to
ms.localizationpriority: medium
ms.assetid: c4fb4a86-b772-49d0-8773-e8ee897e175d
ms.custom:
- seo-marvel-apr2020
description: Admins can learn how to create mail flow rules (transport rules) to block messages that contain executable attachments.
ms.service: exchange-online
locale: en-us
document_id: cdb0f87f-103c-e6ea-1ffb-ee929902010e
document_version_independent_id: 63b1ee98-a4a6-1485-1ebf-1978ad398f77
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-block-executable-attachments.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/use-rules-to-block-executable-attachments
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-block-executable-attachments.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: e2cd0994-74d0-3441-6378-6d4ce87b5889
---

# Use mail flow rules to block messages with executable attachments in Exchange Online | Microsoft Learn

In cloud-based organizations, anti-malware policies block messages with harmful attachments (including executable attachments). For more information, see [Anti-malware protection](/en-us/defender-office-365/anti-malware-protection-about).

To further enhance protection, you can use mail flow rules (also known as transport rules) to identify and block messages that contain executable attachments as described in this article.

For example, following a malware outbreak, a company could apply this rule with a time limit so that affected users can get back to sending attachments after a specified period of time.

## What do you need to know before you begin?

- You need to be assigned permissions before you can do the procedures in this article. Specifically, you need the **Transport Rules** role, which is assigned to the **Organization Management**, **Compliance Management**, and **Records Management** role groups by default.

    For more information, see the following articles:

    - [Permissions in Exchange Online](../../permissions-exo/permissions-exo)
    - [Manage role groups in Exchange Online](../../permissions-exo/role-groups)
- To open the Exchange admin center (EAC) in Exchange Online, see [Exchange admin center in Exchange Online](../../exchange-admin-center).
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For more information about mail flow rules in Exchange Online and the Built-in security add-on for on-premises mailboxes, see the following articles:

    - [Mail flow rules (transport rules) in Exchange Online](mail-flow-rules)
    - [Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions)
    - [Mail flow rule actions in Exchange Online](mail-flow-rule-actions)

## Use the EAC to create a rule that blocks messages with executable attachments

1. In the EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. On the **Rules** page, select **Add a rule**![Add icon.](../../exchangeonline/media/itpro-eac-addicon.png) &gt; **Create a new rule**.
3. The new rule wizard opens. On the **Set rule conditions** page, configure the following settings:

    - **Name**: Enter a unique, descriptive name for the rule.
    - **Apply this rule if**: Select **Any attachment** &gt; **has executable content**.
    - **Do the following**: Select **Block the message** and then choose one of the following actions:

        - **reject the message and include an explanation**: In the **Specify reject reason** flyout that opens, enter the text you want to appear in the non-delivery report (also known as an NDR or bounce message). The default enhanced status code is 5.7.1.
        - **reject the message with the enhanced status code of**: In the **Enter enhanced status code** flyout that opens, enter the enhanced status code that you want to appear in the NDR. Valid values are 5.7.1 or a value from 5.7.900 to 5.7.999. The default rejection text is: `Delivery not authorized, message refused`.
        - **delete the message without notifying anyone**
    - **Except if**: Configure any optional exceptions for the rule.

    When you're finished on the **Set rule conditions** page, select **Next**.
4. On the **Set rule settings** page, configure any other rule properties as required:

    - Verify the **Rule mode** value is **Enforce** (the default value).
    - To include the rule in the [Exchange transport rule report](../../monitoring/mail-flow-reports/mfr-exchange-transport-rule-report), change the **Severity** level from **Not specified** (the default value) to **Low**, **Medium**, or **High**.
    - Select a date/time in **Activate this rule on**. Otherwise, the rule is created in the **Disabled** state.

    When you're finished on the **Set rule settings** page, select **Next**.
5. On the **Review and finish** page, verify your settings. Use the **Back** button or the edit links to make changes.

    When you're finished on the **Review and finish** page, select **Finish**.
6. After the rule is finished saving, select **Done**.

The new rule is now listed on the **Rules** page.

## Use PowerShell to create a rule that blocks messages with executable attachments

[Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) and then use the following syntax to create a rule to block messages that contain executable attachments:

```powershell
New-TransportRule -Name "<UniqueName>" -AttachmentHasExecutableContent $true [-RejectMessageEnhancedStatusCode <5.7.1 | 5.7.900 to 5.7.999>] [-RejectMessageReasonText "<Text>"] [-DeleteMessage $true]
```

- If you use the *RejectMessageEnhancedStatusCode* parameter without the *RejectMessageReasonText* parameter, the default text is: `Delivery not authorized, message refused`.
- If you use the *RejectMessageReasonText* parameter without the *RejectMessageEnhancedStatusCode* parameter, the default code is 5.7.1.

The following example creates a new rule named **Block Executable Attachments** that silently deletes messages that contain executable attachments.

```powershell
New-TransportRule -Name "Block Executable Attachments" -AttachmentHasExecutableContent $true -DeleteMessage $true
```

For detailed syntax and parameter information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).

## How do you know this procedure worked?

To verify that you successfully created a mail flow rule to block messages that contain executable attachments, do any of the following steps:

- **EAC**:

    1. Go to the **Rules** page at https://admin.exchange.microsoft.com/#/transportrules.
    2. On the **Rules** page, select the rule by clicking anywhere in the row other than the round check box next to the first column.
    3. In the details flyout that opens, verify the settings.
- **Exchange Online PowerShell**: Replace &lt;Rule Name&gt; with the name of the rule, and then run the following command to verify the settings:

    ```powershell
    Get-TransportRule -Identity "<Rule Name>" | Format-List Name,AttachmentHasExecutableContent,RejectMessage*,DeleteMessage
    ```
- If you set the **Severity** level of the rule, check the [Exchange transport rule report](../../monitoring/mail-flow-reports/mfr-exchange-transport-rule-report) to see how the rule is being used.