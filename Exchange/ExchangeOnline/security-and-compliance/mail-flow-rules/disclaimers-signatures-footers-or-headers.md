---
layout: Conceptual
title: Organization-wide message disclaimers, signatures, footers, or headers in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/disclaimers-signatures-footers-or-headers
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: 'Summary: Admins can learn how to apply text to the top or bottom of outbound messages in Exchange Online'
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 29ac61c2-77f1-4071-b14e-8cc64e3e76ba
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-06-17T00:00:00.0000000Z
locale: en-us
document_id: 14dbf1c4-0702-250e-2097-c5663dfad762
document_version_independent_id: 505fbbcd-2a0d-b7e7-6f5b-c88c2c66fdbc
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/disclaimers-signatures-footers-or-headers.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/disclaimers-signatures-footers-or-headers
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/disclaimers-signatures-footers-or-headers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: fb5a61af-589e-e330-a30d-5daebd3ea113
---

# Organization-wide message disclaimers, signatures, footers, or headers in Exchange Online | Microsoft Learn

In cloud-based organizations, you can add an HTML or plain text legal disclaimer, disclosure statement, signature, or other information to the top or bottom of email messages that enter or leave your organization. To do this, you create a mail flow rule (also known as a transport rule) that adds the required information to messages.

- Users can apply signatures to their own outgoing messages in Outlook or Outlook on the web (formerly known as Outlook Web App). For more information, see [Create and add an email signature in Outlook on the web](https://support.microsoft.com/office/0F230564-11B9-4239-83DE-F10CBE4DFDFC).
- To add the disclaimer only to outgoing messages, you need to add a corresponding condition (for example, recipients located outside the organization). By default, mail flow rules are applied to incoming and outgoing messages.
- To avoid multiple disclaimers in an email conversation, add an exception that looks for unique text in your disclaimer. This exception ensures that the disclaimer is only added to the original message.
- Test the disclaimer. When you create the mail flow rule, you have the option to start using it immediately (**Enforce**), or to test it first and log the results. We recommend testing all mail flow rules prior to setting them to **Enforce**.

## What do you need to know before you begin?

- Estimated time to complete each procedure: 7 minutes.
- For information about the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can perform these procedures. To see what permissions you need, see the "Mail flow" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

## Use the EAC to add a disclaimer or other email header or footer

1. In the EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. On the **Rules** page, select ![](../../exchangeonline/media/itpro-eac-addicon.png)**Add a rule**, and then select **Apply disclaimers**.

    ![On the Rules page in the Exchange admin center, click Add a rule and then select Apply disclaimers.](../../exchangeonline/media/ee818b31-f5a5-40cc-9fe5-6c04f4120716.png)
3. In the new rule wizard that opens, configure the following settings on the **Set rule conditions** page:

    - **Name**: Enter a unique name for the rule.
    - **Apply this rule if**: Select the conditions that identify which messages get the disclaimer. For example:

        - **The recipient** &gt; **is external/internal**
        - In the **select recipient location** flyout that opens, select **Outside the organization**, and then click **Save**.

        Or, if you want this rule to apply to every message that enters or leaves the organization, select **Apply to all messages** from the **Apply this rule if** drop-down list.
    - **Do the following**: Verify **Apply a disclaimer to the message** and **append a disclaimer** are selected. If you'd rather put the disclaimer text at the top of the message, select **prepend a disclaimer** instead.

        - Select the **Enter text** link to enter the text of the disclaimer and select **Save**.

            Disclaimer text can include HTML tags and inline cascading style sheet (CSS) tags. You can add images using the IMG tag. Disclaimer text also supports the following tokens that use values from the sender:

            - `%%City%%`
            - `%%Company%%`
            - `%%CountryOrRegion%%`
            - `%%Department%%`
            - `%%DisplayName%%`
            - `%%Fax%%`
            - `%%FirstName%%`
            - `%%HomePhone%%`
            - `%%Initials%%`
            - `%%LastName%%`
            - `%%Manager%%`
            - `%%MobilePhone%%`
            - `%%Notes%%`
            - `%%Office%%`
            - `%%Pager%%`
            - `%%Phone%%`
            - `%%PostalCode%%`
            - `%%PostOfficeBox%%`
            - `%%StateOrProvince%%`
            - `%%StreetAddress%%`
            - `%%Title%%`
            - `%%UserPrincipalName%%`
            - `%%WindowsEmailAddress%%`
        - Select the **Select one** link to enter the fallback action if the disclaimer can't be inserted in the message.
        - On the **specify fallback action** page, choose a value from the drop-down list, and then select **Save**.

            Tip

            See the Fallback options for disclaimer rules section in this article for explanations and important information about the fallback actions.
    - **Except if**: To add an exception that prevents multiple disclaimers from being added in an email conversation, configure the following settings:

        - Select **The subject or body** and **Subject or body matches these text patterns**.
        - In the **Specify words or phrases** flyout that opens, enter the words or phrases in the disclaimer, select **Add**, and then select **Save**.

    When you're finished, select **Next**.
4. On the **Set rule settings** page, configure the following settings:

    - **Rule mode**: Leave the default value **Enforce** selected to turn on the rule immediately, or select **Test without Policy Tips** to log the results without actually adding the disclaimer to the messages.
    - **Severity**: Assign the severity level that appears in the message log. Valid values are:
        - **Low**
        - **Medium**
        - **High**
        - **Not audit**
        - **Not specified**
    - **Activate this rule on** and **Deactivate this rule on**: Optionally, select a date-time range when the rule is active.
    - **Stop processing more rules**: Optionally, stop applying more rules to a message after the disclaimer rule processes the message.
    - **Defer the message if rule processing doesn't complete**: Optionally, defer the message if the rule isn't able to process the message.
    - **Match sender address in message**: Select one of the following values:
        - **Header**: Only the message headers are examined. This value is the default value.
        - **Envelope**: Only the SMTP message envelope is examined.
        - **Header or envelope**: Both the message headers and SMTP message envelope are examined.
    - **Comments**: Optionally, enter comments to help describe the rule.

    When you're finished, select **Next**.
5. On the **Review and finish** page, review the settings of the rule and then select **Finish**.

## Use Exchange Online PowerShell to add a disclaimer or other email header or footer

Use the [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule) cmdlet to create the disclaimer rule. For detailed parameter information, see [Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions).

The following example creates a new mail flow rule that adds a disclaimer with an image at the end of all email messages that are sent outside the organization:

```PowerShell
New-TransportRule -Name "External Disclaimer" -SentToScope NotInOrganization -ApplyHtmlDisclaimerText "<h3>Disclaimer Title</h3><p>This is the disclaimer text.</p><img alt='Contoso logo' src='http://www.contoso.com/images/logo.gif'>"
```

The following example creates a new mail flow rule that adds an advertisement for one month at the beginning of all outgoing messages:

```PowerShell
New-TransportRule -Name "March Special" -Enabled $true -SentToScope NotInOrganization -ApplyHtmlDisclaimerLocation Prepend -ActivationDate '03/1/2017' -ExpiryDate '03/31/2017'-ApplyHtmlDisclaimerText "<table align=center width=200 border=1 bordercolor=blue bgcolor=green cellpadding=10 cellspacing=0><tr><td nowrap><a href=http://www.contoso.com/marchspecials.htm>Click to see March specials</a></td></tr></table>"
```

## How do you know this worked?

To verify that you've successfully created a disclaimer, and that the disclaimer works as expected, do the following steps:

- Send yourself both a plain text email and an HTML email that match the conditions and exceptions you defined, and verify that the text appears as you intended.
- If you added an exception to avoid adding the disclaimer to successive messages in a conversation, forward your test messages to yourself to verify that you don't get an extra copy of the disclaimer.
- Send yourself some messages that shouldn't get the disclaimer and verify that the disclaimer isn't included.

## Fallback options for disclaimer rules

If a mail flow rule can't modify the message to add the disclaimer (for example, the message is encrypted), you need to specify what to do. This contingency is known as the *fallback option* for the rule. The available fallback options for disclaimer rules are:

- **Wrap**: A new message is created and the original message is added to it as an attachment. The disclaimer text is added to the new message, which is delivered to the recipients. This is the default value.

    - Subsequent mail flow rules that examine message properties (for example, the message subject or text in the message body) will examine the new message, not the original message (which is now an attachment in the new message). If you want other rules to examine and act on the original message, ensure that those rules are applied *before* the disclaimer rule by using a lower priority for the disclaimer rule and higher priority for other rules.
    - If the process of inserting the original message as an attachment in the new message fails, the original message isn't delivered. The original message is returned to the sender in a non-delivery report (also known as an NDR or a bounce message).

    Important

    Don't use the value **Wrap** in rules that affect incoming messages from external senders. Use the value **Reject** instead. The effects of the value **Wrap** interfere with [Safe Attachments scanning](/en-us/defender-office-365/safe-attachments-about) of messages from external senders. To find affected rules, run the following command in Exchange Online PowerShell:

    ```powershell
    Get-TransportRule | where {$_.ApplyHTMLDisclaimerFallbackAction -eq 'Wrap' -and $_.FromScope -eq 'NotInOrganization'}
    ```
- **Ignore**: The rule is ignored and the original message is delivered without the disclaimer.
- **Reject**: The original message is returned to the sender in an NDR.

In the EAC, you select the fallback option in the rule action. In Exchange Online PowerShell, you use the *ApplyHtmlDisclaimerFallbackAction* parameter.

## For more information

After you configure a disclaimer rule, see [Manage mail flow rules](manage-mail-flow-rules), for information about how to view, modify, enable, disable, or remove the rule.