---
layout: Conceptual
title: Deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/standalone-eop/configure-eop-spam-protection-hybrid
Manager: chrisda
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: chrisda
author: chrisda
ms.date: 2025-12-16T00:00:00.0000000Z
audience: ITPro
ms.topic: how-to
ms.localizationpriority: medium
search.appverid:
- MET150
ms.assetid: 0cbaccf8-4afc-47e3-a36d-a84598a55fb8
ms.collection:
- M365-security-compliance
description: Admins in on-premises Exchange organizations can learn how to configure their on-premises Exchange organization to correctly move cloud-detected spam messages to the Junk Email folder in on-premises mailboxes.
ms.custom: seo-marvel-apr2020
ms.service: exchange-online
locale: en-us
document_id: 2ebc5a87-7c60-84d9-0de1-fdc5b86bb36e
document_version_independent_id: cf3ee91b-8200-5438-053a-98aa15a6165b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/standalone-eop/configure-eop-spam-protection-hybrid.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standalone-eop/configure-eop-spam-protection-hybrid
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/standalone-eop/configure-eop-spam-protection-hybrid.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: 3bb9ad97-fac2-ab83-4077-768b4f57c650
---

# Deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes | Microsoft Learn

Note

This article doesn't apply to mailboxes in the cloud.

If your inbound internet mail flows through Microsoft 365 to on-premises Exchange recipients, you need to configure on-premises Exchange to recognize and translate the spam filtering verdicts from the cloud. This configuration allows the [junk email rule in on-premises mailboxes](/en-us/exchange/antispam-and-antimalware/antispam-protection/configure-antispam-settings) to correctly move spam from the Inbox to the Junk Email folder in the following environments:

- [Exchange Server hybrid deployments](../exchange-hybrid) with Exchange Online mailboxes and on-premises Exchange mailboxes.
- [The Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/standalone-eop) protecting on-premises Exchange mailboxes.

Specifically, you need to create Exchange mail flow rules (also known as transport rules) in your on-premises Exchange organization with the following settings:

- **Conditions**: Find messages with the following cloud anti-spam headers and values:

    - `X-Forefront-Antispam-Report: SFV:SPM` (message marked as spam by spam filtering)
    - `X-Forefront-Antispam-Report: SFV:SKS` (message marked as spam by mail flow rules in the cloud before spam filtering)
    - `X-Forefront-Antispam-Report: SFV:SKB` (message marked as spam by spam filtering due to the sender's email address or email domain being in the blocked sender list or the blocked domain list in cloud anti-spam policies.)

    For more information about these header values, see [Anti-spam message headers in cloud organizations](/en-us/defender-office-365/message-headers-eop-mdo).
- **Action**: Set the spam confidence level (SCL) of these messages to 6 (spam).

This article describes how to create the required mail flow rules the Exchange admin center (EAC) and in the Exchange Management Shell (Exchange PowerShell) in the on-premises Exchange organization.

Tip

Instead of delivering the messages to the on-premises user's Junk Email folder, you can configure cloud anti-spam policies to quarantine spam messages. For more information, see [Configure anti-spam policies in cloud organizations](/en-us/defender-office-365/anti-spam-policies-configure).

## What do you need to know before you begin?

- You need to be assigned permissions in the on-premises Exchange environment before you can do these procedures. Specifically, you need to be assigned the **Transport Rules** role, which is assigned to the **Organization Management**, **Compliance Management**, and **Records Management** roles by default. For more information, see [Add members to a role group](/en-us/Exchange/permissions/role-group-members#add-members-to-a-role-group).
- A combination of the following settings control whether a message is delivered to the Junk Email folder in an on-premises Exchange mailbox:

    - The *SCLJunkThreshold* parameter value on the [Set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/set-organizationconfig) cmdlet in the Exchange Management Shell. The default value is 4, which means an SCL of 5 or higher should deliver the message to the user's Junk email folder.
    - The *SCLJunkThreshold* parameter value on the [Set-Mailbox](/en-us/powershell/module/exchangepowershell/set-mailbox) cmdlet in the Exchange Management Shell. The default value is blank ($null), which means the organization setting is used. For details, see [Exchange spam confidence level (SCL) thresholds](/en-us/Exchange/antispam-and-antimalware/antispam-protection/scl).
    - Whether the junk email rule is enabled on the mailbox (the *Enabled* parameter value is $true on the [Set-MailboxJunkEmailConfiguration](/en-us/powershell/module/exchangepowershell/set-mailboxjunkemailconfiguration) cmdlet in the Exchange Management Shell). It's the junk email rule that actually moves the message to the Junk Email folder after delivery. By default, the junk email rule is enabled on mailboxes. For more information, see [Configure Exchange antispam settings on mailboxes](/en-us/Exchange/antispam-and-antimalware/antispam-protection/configure-antispam-settings).
- To open the EAC on an Exchange Server, see [Exchange admin center in Exchange Server](/en-us/Exchange/architecture/client-access/exchange-admin-center). To open the Exchange Management Shell, see [Open the Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell) or [Connect to Exchange servers using remote PowerShell](/en-us/powershell/exchange/connect-to-exchange-servers-using-remote-powershell).
- For more information about mail flow rules in on-premises Exchange, see the following articles:

    - [Mail flow rules in Exchange Server](/en-us/Exchange/policy-and-compliance/mail-flow-rules/mail-flow-rules)
    - [Mail flow rule conditions and exceptions (predicates) in Exchange Server](/en-us/Exchange/policy-and-compliance/mail-flow-rules/conditions-and-exceptions)
    - [Mail flow rule actions in Exchange Server](/en-us/Exchange/policy-and-compliance/mail-flow-rules/actions)

## Use the EAC to create mail flow rules that set the SCL of cloud-detected spam messages

1. In the EAC in the on-premises Exchange organization, go to **Mail flow** &gt; **Rules**.
2. On the **Rules** page, select ![](../exchangehybrid/media/modern-eac-create-icon.png)**Add** &gt; **Create a new rule** in the dropdown list.
3. In the **New rule** page that opens, configure the following settings:

    - **Name**: Enter a unique, descriptive name for the rule. For example:

        - Cloud SFV:SPM to SCL 6
        - Cloud SFV:SKS to SCL 6
        - CloudCloud SFV:SKB to SCL 6
    - Select **More Options**.
    - **Apply this rule if**: Select **A message header** &gt; **includes any of these words**.

        In the **Enter text header includes Enter words** sentence that appears, do the following steps:

        - Select the **Enter text** link. In the **Specify header name** dialog that opens, enter **X-Forefront-Antispam-Report** and then select **OK**.
        - Select the **Enter words** link. In the **Specify words or phrases** dialog that opens, enter one of the cloud spam header values (**SFV:SPM**, **SFV:SKS**, or **SFV:SKB**), select **Add**![Add icon.](../exchangehybrid/media/itpro-eac-addicon.png), and then select **OK**.
    - **Do the following**: Select **Modify the message properties** &gt; **Set the spam confidence level (SCL)**.

        In the **Specify SCL** dialog that opens, select **6** (the default value is **5**).

    When you're finished on the **New rule** page, select **Save**.

Repeat these steps for the remaining cloud spam verdict values (**SFV:SPM**, **SFV:SKS**, or **SFV:SKB**).

### Use the Exchange Management Shell to create mail flow rules that set the SCL of cloud-protected spam messages

If you would rather use the Exchange Management Shell to create the three mail flow rules, use the following syntax:

```powershell
New-TransportRule -Name "<RuleName>" -HeaderContainsMessageHeader "X-Forefront-Antispam-Report" -HeaderContainsWords "<CloudSpamFilteringVerdict>" -SetSCL 6
```

For example:

```powershell
New-TransportRule -Name "Cloud SFV:SPM to SCL 6" -HeaderContainsMessageHeader "X-Forefront-Antispam-Report" -HeaderContainsWords "SFV:SPM" -SetSCL 6
```

```powershell
New-TransportRule -Name "Cloud SFV:SKS to SCL 6" -HeaderContainsMessageHeader "X-Forefront-Antispam-Report" -HeaderContainsWords "SFV:SKS" -SetSCL 6
```

```powershell
New-TransportRule -Name "Cloud SFV:SKB to SCL 6" -HeaderContainsMessageHeader "X-Forefront-Antispam-Report" -HeaderContainsWords "SFV:SKB" -SetSCL 6
```

For detailed syntax and parameter information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).

## How do you know this procedure worked?

To verify you successfully configured on-premises Exchange to deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes, do any of the following steps:

- In the EAC in the on-premises Exchange organization, go to **Mail flow** &gt; **Rules**, select the rule, and then select **Edit**![Edit icon.](../exchangehybrid/media/itpro-eac-editicon.png) to verify the settings.
- In the Exchange Management Shell, replace &lt;RuleName&gt; with the name of the mail flow rule, and run the following command to verify the settings:

    ```powershell
    Get-TransportRule -Identity "<RuleName>" | Format-List
    ```
- In an external email system **that doesn't scan outbound messages for spam**, send a Generic Test for Unsolicited Bulk Email (GTUBE) message to an affected on-premises recipient, and confirm that the message is delivered to the Junk Email folder. A GTUBE message is similar to the European Institute for Computer Antivirus Research (EICAR) text file for testing malware settings.

    To send a GTUBE message, include the following text in the body of an email message on a single line, without any spaces or line breaks:

    ```text
    XJS*C4JDBQADN1.NSBN3*2IDNEN*GTUBE-STANDARD-ANTI-UBE-TEST-EMAIL*C.34X
    ```