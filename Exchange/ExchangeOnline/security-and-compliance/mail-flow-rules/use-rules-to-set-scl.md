---
layout: Conceptual
title: Use mail flow rules to set the SCL in messages in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl
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
ms.date: 2026-08-11T00:00:00.0000000Z
audience: ITPro
ms.topic: how-to
ms.localizationpriority: medium
search.appverid:
- MET150
ms.assetid: 4ccab17a-6d49-4786-aa28-92fb28893e99
ms.collection:
- M365-security-compliance
description: Learn how to use Exchange mail flow rules (transport rules) and spam confidence level (SCL) values to submit filtering requests for messages.
ms.custom:
- seo-marvel-apr2020
- msecd-doc-authoring-1015
ms.service: exchange-online
ai-usage: ai-assisted
locale: en-us
document_id: 1d2d2006-3af2-366e-50f8-c42a007a1e66
document_version_independent_id: 8d4ec857-121f-163f-9691-93668cd6f9a2
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-set-scl.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/use-rules-to-set-scl
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-set-scl.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: a5b0ed81-0ab7-a385-1619-ed1dd2fc77e4
---

# Use mail flow rules to set the SCL in messages in Exchange Online | Microsoft Learn

In cloud-based organizations, anti-spam policies (also known as spam filter policies or content filter policies) scan inbound messages for spam. For more information, see [Configure anti-spam policies](/en-us/defender-office-365/anti-spam-policies-configure).

The spam confidence level (SCL) value doesn't determine whether cloud spam filtering identifies a message as **Spam** or **High confidence spam**, and it doesn't determine the action taken on the message. Spam filtering makes these decisions using message categorization and other signals. SCL is used primarily in on-premises Exchange, including hybrid environments where cloud-filtered messages are delivered to on-premises mailboxes.

In Exchange Online, you can use mail flow rules (also known as transport rules) to submit the following requests to spam filtering:

- Bypass most spam filtering by setting SCL to `-1`.
- Treat messages as spam by setting SCL to `5` or `6`.
- Treat messages as high confidence spam by setting SCL to `9`.

These SCL values are inputs to filtering, not final decisions. Secure by default and other filtering signals evaluate the request and might not honor it. The SCL value stamped on the message might also differ from the value configured in the rule. For more information, see [Spam confidence level (SCL) in Microsoft 365](/en-us/defender-office-365/anti-spam-spam-confidence-level-scl-about).

## What do you need to know before you begin?

- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Exchange Online permissions](../../permissions-exo/permissions-exo): You need the **Transport Rules** role, which is assigned to the **Compliance Management**, **Records Management**, and **Organization Management** role groups by default.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Exchange Administrator** or **Global Administrator**^\*^ roles.

        Important

        ^\*^ Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.
- To open the EAC in Exchange Online, see [Exchange admin center in Exchange Online](../../exchange-admin-center). To open the EAC in the Built-in security add-on for on-premises mailboxes, see [Exchange admin center in the Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/exchange-admin-center-eop).
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For more information about mail flow rules in cloud-based organizations, see the following articles:

    - [Mail flow rules (transport rules) in Exchange Online](mail-flow-rules)
    - [Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions)
    - [Mail flow rule actions in Exchange Online](mail-flow-rule-actions)

## Use the EAC to create a mail flow rule that sets the SCL of a message

1. On the **Rules** page in the Exchange admin center at https://admin.exchange.microsoft.com/#/transportrules, select **Add a rule**![Add icon.](../../exchangeonline/media/itpro-eac-addicon.png), and then select **Create a new rule** to start the new rule wizard.
2. On the **Set rule conditions** page, configure the following settings:

    - **Name**: Enter a unique, descriptive name for the rule.
    - **Apply this rule if**: Select one or more conditions to identify messages. For more information, see [Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions).
    - **Do the following**: Select **Modify the message properties** &gt; **set the spam confidence level (SCL)**. In the **Specify SCL**flyout that opens, select one of the following values:
        - **Bypass spam filtering**: Requests that messages that meet the rule conditions bypass most spam filtering. Other Microsoft 365 email protection features aren't affected. For example, messages are always scanned for malware. The SCL value stamped on a message might be `0` or `1` instead of `-1` to indicate that the message was evaluated and found not to be spam.

            A mail flow rule that requests **Bypass spam filtering** doesn't allow the delivery of high confidence phishing messages (HPHISH) or messages that contain malware. You can use the [Tenant Allow/Block List](/en-us/defender-office-365/tenant-allow-block-list-about) to temporarily override an HPHISH false positive after you [report the message to Microsoft](/en-us/defender-office-365/submissions-admin#report-good-email-to-microsoft). If the MX record for the recipient domain doesn't point to Microsoft 365 because mail is routed through a non-Microsoft service or device first, a rule with **Bypass spam filtering** allows messages detected as high confidence phishing by Microsoft 365 anti-spam filtering to be delivered to the Inbox.

            Important

            Don't use mail flow rules to bypass spam filtering for SecOps mailboxes or phishing simulation messages. Instead, use the advanced delivery policy. For more information, see [Configure the delivery of third-party phishing simulations to users and unfiltered messages to SecOps mailboxes](/en-us/defender-office-365/advanced-delivery-policy-configure).

            Be very careful about allowing messages to skip spam filtering. The mail flow rule should use more conditions than just the sender's email address or domain. For more information, see [Create sender allowlists for cloud mailboxes](/en-us/defender-office-365/create-safe-sender-lists-in-office-365#use-mail-flow-rules).
        - **0 to 4**: Submits the selected SCL value to spam filtering. These values don't determine the verdict or action in cloud filtering.
        - **5 or 6**: Requests that the message be treated as **Spam**.
        - **7 or 8**: Valid SCL values, but these values don't determine the verdict or action in cloud filtering.
        - **9**: Requests that the message be treated as **High confidence spam**.

            If filtering honors a request for **Spam** or **High confidence spam**, the action in the anti-spam policy that detected the message determines what happens to it. For example, the message might be moved to the Junk Email folder or quarantine.
    - **Except if**: Configure any exceptions to the rule as required.

    When you're finished on the **Set rule conditions** page, select **Next**.
3. On the **Set rule settings** page, review or configure the settings, and then select **Next**.
4. On the **Review and finish** page, review the settings, and then select **Finish**.

## How do you know this procedure worked?

To verify the rule:

1. Send a test message from an external account that matches the rule conditions.
2. In the message header, find the `X-Forefront-Antispam-Report` header.
3. Review the following fields:
    - `SCL`: The actual SCL value stamped on the message. This value might differ from the value configured in the rule.
    - `SFV`: Indicates whether the filtering request from the mail flow rule was honored.
    - `CAT`: Identifies the filtering category applied to the message.
4. Confirm that the final message location and action match the filtering verdict and applicable anti-spam policy.

For more information about these fields, see [Anti-spam message headers](/en-us/defender-office-365/message-headers-eop-mdo).