---
layout: Conceptual
title: Mail flow rule conditions and exceptions (predicates) in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/conditions-and-exceptions
Manager: anaruxa
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
audience: ITPro
ms.localizationpriority: medium
description: Learn about the conditions and exceptions (predicates) that are available for mail flow rules in cloud-based organizations.
ms.author: lusassl
ms.topic: article
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: 7235e5ed-f7f4-41b1-b1a0-47bb96223a2f
ms.collection:
- exchange-online
- M365-email-calendar
ms.reviewer: 
f1.keywords:
- NOCSH
ms.custom: msecd-doc-authoring-1015
ms.date: 2026-08-11T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 4b18f30a-b22b-5f3b-8357-82690321bad0
document_version_independent_id: cf3ce6c5-bd43-380a-b162-d475032facb8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/conditions-and-exceptions.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/conditions-and-exceptions
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/conditions-and-exceptions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
platformId: 314ddab8-1b23-999d-4279-a91b2f7fe9a7
---

# Mail flow rule conditions and exceptions (predicates) in Exchange Online | Microsoft Learn

Conditions and exceptions in mail flow rules (also known as transport rules) identify the messages that the rule is applied to or not applied to. For example, if the rule adds a disclaimer to messages, you can configure the rule to only apply to messages that contain specific words, messages sent by specific users, or to all messages except those sent by the members of a specific distribution group. Collectively, the conditions and exceptions in mail flow rules are also known as *predicates*, because for every condition, there's a corresponding exception that uses the exact same settings and syntax. The only difference is that conditions specify messages to include, while exceptions specify messages to exclude.

Most conditions and exceptions have one property that requires one or more values. For example, the **The sender is** condition requires the sender of the message. Some conditions have two properties. For example, the **A message header includes any of these words** condition requires one property to specify the message header field, and a second property to specify the text to look for in the header field. Some conditions or exceptions don't have any properties. For example, the **Any attachment has executable content** condition simply looks for attachments in messages that have executable content.

For more information about mail flow rules in Exchange Online, including how multiple conditions/exceptions or multi-valued conditions/exceptions are handled, see [Mail flow rules (transport rules) in Exchange Online](mail-flow-rules).

## Conditions and exceptions for mail flow rules in Exchange Online

The tables in the following sections describe the conditions and exceptions that are available in mail flow rules in Exchange Online. The property types are described in the Property types section.

Senders

Recipients

Message subject or body

Attachments

Any recipients

Message sensitive information types, To and Cc values, size, and character sets

Sender and recipient

Message properties

Message headers

Note

- After you select a condition or exception in the Exchange admin center (EAC), the value that's ultimately shown in the **Apply this rule if** or **Except if** field is often different (shorter) than the "click path value" you selected. Also, when you create new rules based on a template (a filtered list of scenarios), you can often select a short condition name instead of following the complete click path. The short names and full click path values are shown in the EAC column in the tables.
- If you select **[Apply to all messages]** in the EAC, you can't specify any other conditions. The equivalent in PowerShell is to create a rule without specifying any condition parameters.
- The settings and properties are the same in conditions and exceptions; so, the output of the **Get-TransportRulePredicate** cmdlet doesn't list exceptions separately. Also, the names of some of the predicates that are returned by this cmdlet are different than the corresponding parameter names, and a predicate might require multiple parameters.

### Senders

For conditions and exceptions that examine the sender's address, you can specify where rule looks for the sender's address.

In the EAC, in the **Properties of this rule** section, select **Match sender address in message**. You might need to select **More options** to see this setting. In PowerShell, the parameter is *SenderAddressLocation*. The available values are:

- **Header**: Only examine senders in the message headers (**From** field). This value is the default value.
- **Envelope**: Only examine senders from the message envelope (the **MAIL FROM** value that was used in the SMTP transmission, which is typically stored in the **Return-Path** field). Message envelope searching is only available for the following conditions (and the corresponding exceptions):

    - **The sender is** (*From*)
    - **The sender is a member of** (*FromMemberOf*)
    - **The sender address includes** (*FromAddressContainsWords*)
    - **The sender address matches** (*FromAddressMatchesPatterns*)
    - **The sender's domain is** (*SenderDomainIs*)
- **Header or envelope** (`HeaderOrEnvelope`) Examine senders in the message header and the message envelope.

Note

In the **automatic-forwarding** scenario, the sender address for forwarded mail is the address of the original sender and not the forwarder. For more information, see [A transport rule doesn't match if user mailbox rules automatically forward messages](/en-us/exchange/troubleshoot/email-delivery/autoforward-mail-exclusions-not-honored-transport-rule).

In the **Auto-Reply** scenario, sender is determined by checking *SenderAddressLocation*.

- If you set -Headers, the sender will be a user-generated Auto-Reply message.
- If you set -Envelope, the sender will be a user who sent original message.

| Condition or exception in the EAC | Condition and exception parameters in Exchange Online PowerShell | Property type | Description |
| --- | --- | --- | --- |
| **The sender is**<br>**The sender** &gt; **is this person** | *From* *ExceptIfFrom* | `Addresses` | Messages that are sent by the specified mailboxes, mail users, mail contacts, or Microsoft 365 groups in the organization. <br> For more information about using Microsoft 365 groups with this condition, see the Addresses entry in the Property types section. |
| **The sender is located**<br>**The sender** &gt; **is external/internal** | *FromScope* *ExceptIfFromScope* | `UserScopeFrom` | Messages that are sent by either internal senders or external senders. |
| **The sender is a member of**<br>**The sender** &gt; **is a member of this group** | *FromMemberOf* *ExceptIfFromMemberOf* | `Addresses` | Messages that are sent by a member of the specified distribution group, mail-enabled security group, or Microsoft 365 group. <br> For more information about using Microsoft 365 groups with this condition, see the Addresses entry in the Property types section. |
| **The sender address includes**<br>**The sender** &gt; **address includes any of these words** | *FromAddressContainsWords* *ExceptIfFromAddressContainsWords* | `Words` | Messages that contain the specified words in the sender's email address. |
| **The sender address matches**<br>**The sender** &gt; **address matches any of these text patterns** | *FromAddressMatchesPatterns* *ExceptIfFromAddressMatchesPatterns* | `Patterns` | Messages where the sender's email address contains text patterns that match the specified regular expressions. <br> For more information about regular expressions, see [Regular expressions to be used in transport rules](../../mail-flow-best-practices/regular-expressions-usage-transport-rules). |
| **The sender is on a recipient's list**<br>**The sender** &gt; **is on a recipient's supervision list** | *SenderInRecipientList* *ExceptIfSenderInRecipientList* | `SupervisionList` | Messages where the sender is on the recipient's Allowlist or Blocklist. |
| **The sender's specified properties include any of these words**<br>**The sender** &gt; **has specific properties including any of these words** | *SenderADAttributeContainsWords* *ExceptIfSenderADAttributeContainsWords* | First property: `ADAttribute`<br> Second property: `Words` | Messages where the specified Active Directory attribute of the sender contains any of the specified words. <br> The **Country** attribute requires the two-letter country code value (for example, DE for Germany). |
| **The sender's specified properties match these text patterns**<br>**The sender** &gt; **has specific properties matching these text patterns** | *SenderADAttributeMatchesPatterns* *ExceptIfSenderADAttributeMatchesPatterns* | First property: `ADAttribute`<br> Second property: `Patterns` | Messages where the specified Active Directory attribute of the sender contains text patterns that match the specified regular expressions. |
| **Sender's IP address is in the range**<br>**The sender** &gt; **IP address is in any of these ranges or exactly matches** | *SenderIPRanges* *ExceptIfSenderIPRanges* | `IPAddressRanges` | Messages where the sender's IP address matches the specified IP address, or falls within the specified IP address range.  The IP address that's used during evaluation of this condition is the address of the last hop before reaching the service. **This IP address is not guaranteed to be the original sender's IP address**, especially if third-party software is used during message transport. |
| **The sender's domain is**<br>**The sender** &gt; **domain is** | *SenderDomainIs* *ExceptIfSenderDomainIs* | `DomainName` | Messages where the domain of the sender's email address matches the specified value. <br> This predicate will match domains and subdomains with domain provided. For example: <br><br> For the value "domain.com", both domain "domain.com" and subdomain "subdomain.domain.com" will be matched. |

### Recipients

For conditions and exceptions that examine the recipient's address, you can specify where the rule looks for the recipient's address by using the *RecipientAddressType* parameter in Exchange Online PowerShell. Valid values are:

- **Original**: Checks the address that the message was originally addressed to, before the service resolved it.
- **Resolved**: Checks the recipient's resolved address. For mailboxes, the address resolves to the primary SMTP address. For mail users and mail contacts, the address resolves to the external email address. Proxy addresses aren't checked. This value is the default value.

For example, if a message is sent to a mail user's email address in your organization, **Original** checks that address, but **Resolved** checks the mail user's external email address.

Note

If the Mail flow rule is configured to check for the recipient where the recipient is a distribution group, the rule won't be matched. When the message is sent to a distribution group, the group will be resolved to distinct users of that group before reaching Mail flow rules and instead, will check every member of a group.

If you want the rule to work when a distribution group is the recipient, under **Apply this rule if** select **The message** and **To or CC box contains this person** and select the name of the group from the list (this won't work if the group is mentioned as BCC recipient).

| Condition or exception in the EAC | Condition and exception parameters in Exchange Online PowerShell | Property type | Description |
| --- | --- | --- | --- |
| **The recipient is**<br>**The recipient** &gt; **is this person** | *SentTo* *ExceptIfSentTo* | `Addresses` | Messages where one of the recipients is the specified mailbox, mail user, or mail contact in the organization. The recipients can be in the **To**, **Cc**, or **Bcc** fields of the message. <br>**Note**: You can't specify distribution groups, mail-enabled security groups, or Microsoft 365 groups. If you need to take action on messages that are sent to a group, use the **To box contains**(*AnyOfToHeader*) or **Cc box contains** or **To or Cc box contains** condition instead. |
| **The recipient is located**<br>**The recipient** &gt; **is external/external** | *SentToScope* *ExceptIfSentToScope* | `UserScopeTo` | Messages that are sent to internal or external recipients. |
| **The recipient is a member of**<br>**The recipient** &gt; **is a member of this group** | *SentToMemberOf* *ExceptIfSentToMemberOf* | `Addresses` | Messages that contain recipients who are members of the specified distribution group, mail-enabled security group, or Microsoft 365 group. The group can be in the **To**, **Cc**, or **Bcc** fields of the message. <br> For more information about using Microsoft 365 groups with this condition, see the Addresses entry in the Property types section. |
| **The recipient address includes**<br>**The recipient** &gt; **address includes any of these words** | *RecipientAddressContainsWords* *ExceptIfRecipientAddressContainsWords* | `Words` | Messages that contain the specified words in the recipient's email address. <br>**Note**: This condition doesn't consider messages that are sent to recipient proxy addresses. It only matches messages that are sent to the recipient's primary email address. |
| **The recipient address matches**<br>**The recipient** &gt; **address matches any of these text patterns** | *RecipientAddressMatchesPatterns* *ExceptIfRecipientAddressMatchesPatterns* | `Patterns` | Messages where a recipient's email address contains text patterns that match the specified regular expressions. <br>**Note**: This condition doesn't consider messages that are sent to recipient proxy addresses. It only matches messages that are sent to the recipient's primary email address. |
| **The recipient is on the sender's list**<br>**The recipient** &gt; **is on the sender's supervision list** | *RecipientInSenderList* *ExceptIfRecipientInSenderList* | `SupervisionList` | Messages where the recipient is on the sender's Allowlist or Blocklist. |
| **The recipient's specified properties include any of these words**<br>**The recipient** &gt; **has specific properties including any of these words** | *RecipientADAttributeContainsWords* *ExceptIfRecipientADAttributeContainsWords* | First property: `ADAttribute`<br> Second property: `Words` | Messages where the specified Active Directory attribute of a recipient contains any of the specified words. <br> The **Country** attribute requires the two-letter country code value (for example, DE for Germany). |
| **The recipient's specified properties match these text patterns**<br>**The recipient** &gt; **has specific properties matching these text patterns** | *RecipientADAttributeMatchesPatterns* *ExceptIfRecipientADAttributeMatchesPatterns* | First property: `ADAttribute`<br> Second property: `Patterns` | Messages where the specified Active Directory attribute of a recipient contains text patterns that match the specified regular expressions. |
| **A recipient's domain is**<br>**The recipient** &gt; **domain is** | *RecipientDomainIs* *ExceptIfRecipientDomainIs* | `DomainName` | Messages where the domain of a recipient's email address matches the specified value. <br> This predicate will match domains and subdomains with domain provided. For example: <br><br> For the value "domain.com", both domain "domain.com" and subdomain "subdomain.domain.com" will be matched. |

Note

**MemberOf predicate issues:** If `MemberOf` predicates (for example, `FromMemberOf` or `SentToMemberOf`) are not evaluated correctly despite a user being a valid group member, note that Transport Rules cache group membership. Cache refreshes occur approximately every 3 hours, but not all groups are refreshed in each cycle, so there is no SLA for when changes take effect.

Besides, [Dynamic Distribution Group (DDG) membership is updated every 24 hours](/en-us/Exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/modern-dynamic-distribution-groups#refresh-the-membership-of-a-ddg). As a result, membership changes for DDGs can take up to 24 hours, plus up to 3 additional hours for membership of newly added\removed user to be present in Transport Rule evaluation properly.

### Message subject or body

Note

The search for words or text patterns in the subject or other header fields in the message occurs *after* the message has been decoded from the MIME content transfer encoding method that was used to transmit the binary message between SMTP servers in ASCII text. You can't use conditions or exceptions to search for the raw (typically, Base64) encoded values of the subject or other header fields in messages.

| Condition or exception in the EAC | Condition and exception parameters in Exchange Online PowerShell | Property type | Description |
| --- | --- | --- | --- |
| **The subject or body includes**<br>**The subject or body** &gt; **subject or body includes any of these words** | *SubjectOrBodyContainsWords* *ExceptIfSubjectOrBodyContainsWords* | `Words` | Messages that have the specified words in the **Subject** field or message body. |
| **The subject or body matches**<br>**The subject or body** &gt; **subject or body matches these text patterns** | *SubjectOrBodyMatchesPatterns* *ExceptIfSubjectOrBodyMatchesPatterns* | `Patterns` | Messages where the **Subject** field or message body contains text patterns that match the specified regular expressions. |
| **The subject includes**<br>**The subject or body** &gt; **subject includes any of these words** | *SubjectContainsWords* *ExceptIfSubjectContainsWords* | `Words` | Messages that have the specified words in the **Subject** field. |
| **The subject matches**<br>**The subject or body** &gt; **subject matches these text patterns** | *SubjectMatchesPatterns* *ExceptIfSubjectMatchesPatterns* | `Patterns` | Messages where the **Subject** field contains text patterns that match the specified regular expressions. |

### Attachments

For more information about how mail flow rules inspect message attachments, see [Use mail flow rules to inspect message attachments in Exchange Online](inspect-message-attachments).

Tip

If you suspect that your rule isn't working properly, first check which attachments the message contains. To inspect which attachment/s the message contained during Mail flow rule evaluation, see [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction).

| Condition or exception in the EAC | Condition and exception parameters in Exchange Online PowerShell | Property type | Description |
| --- | --- | --- | --- |
| **Any attachment's content includes**<br>**Any attachment** &gt; **content includes any of these words** | *AttachmentContainsWords* *ExceptIfAttachmentContainsWords* | `Words` | Messages where an attachment contains the specified words. |
| **Any attachments content matches**<br>**Any attachment** &gt; **content matches these text patterns** | *AttachmentMatchesPatterns* *ExceptIfAttachmentMatchesPatterns* | `Patterns` | Messages where an attachment contains text patterns that match the specified regular expressions. <br>**Note**: Only the first 150 kilobytes (KB) of the attachments are scanned. |
| **Any attachment's content can't be inspected**<br>**Any attachment** &gt; **content can't be inspected** | *AttachmentIsUnsupported* *ExceptIfAttachmentIsUnsupported* | n/a | Mail flow rules only can inspect the content of supported file types. If the mail flow rule finds an attachment file type that isn't supported, the *AttachmentIsUnsupported* condition is triggered. Supported file types for an attachment are listed here [Use mail flow rules to inspect message attachments in Exchange Online](/en-us/exchange/security-and-compliance/mail-flow-rules/inspect-message-attachments). |
| **Any attachment's file name matches**<br>**Any attachment** &gt; **file name matches these text patterns** | *AttachmentNameMatchesPatterns* *ExceptIfAttachmentNameMatchesPatterns* | `Patterns` | Messages where an attachment's file name contains text patterns that match the specified regular expressions. |
| **Any attachment's file extension matches**<br>**Any attachment** &gt; **file extension includes these words** | *AttachmentExtensionMatchesWords* *ExceptIfAttachmentExtensionMatchesWords* | `Words` | Messages where an attachment's file extension matches any of the specified words. **Note:** Nested attachments (files inside original attachments) extensions and original attachment extensions are inspected. If you want to see all attachment extensions evaluated by a mail flow rule for a specific message, see [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction). |
| **Any attachment is greater than or equal to**<br>**Any attachment** &gt; **size is greater than or equal to** | *AttachmentSizeOver* *ExceptIfAttachmentSizeOver* | `Size` | Messages where any attachment is greater than or equal to the specified value. <br> In the EAC, you can only specify the size in kilobytes (KB). |
| **The message didn't complete scanning**<br>**Any attachment** &gt; **didn't complete scanning** | *AttachmentProcessingLimitExceeded* *ExceptIfAttachmentProcessingLimitExceeded* | n/a | Messages where the Exchange mailflow rules engine couldn't complete the scanning of the attachments. You can use this condition to create rules that work together to identify and process messages where the content couldn't be fully scanned. **Note:** This condition applies only to limitations in the rules engine scanning process and is not related to Microsoft Defender for Office 365 Safe Attachments scanning |
| **Any attachment has executable content**<br>**Any attachment** &gt; **has executable content** | *AttachmentHasExecutableContent* *ExceptIfAttachmentHasExecutableContent* | n/a | Messages where an attachment is an executable file. The system inspects the file's properties rather than relying on the file's extension. To understand better this condition/exception, see [Use mail flow rules to inspect message attachments in Exchange Online](/en-us/exchange/security-and-compliance/mail-flow-rules/inspect-message-attachments) |
| **Any attachment is password protected**<br>**Any attachment** &gt; **is password protected** | *AttachmentIsPasswordProtected* *ExceptIfAttachmentIsPasswordProtected* | n/a | Messages where an attachment is password protected (and therefore can't be scanned). Password detection works for Office documents, archive documents (.zip, .7z), and .pdf files. |
| **has these properties, including any of these words**<br>**Any attachment** &gt; **has these properties, including any of these words** | *AttachmentPropertyContainsWords* *ExceptIfAttachmentPropertyContainsWords* | First property: `DocumentProperties`<br> Second property: `Words` | Messages where the specified property of an attached Office document contains the specified words. <br> This condition helps you integrate mail flow rules with SharePoint, File Classification Infrastructure (FCI) in Windows Server 2012 R2 or later, or a third-party classification system. <br><br> You can select from a list of built-in properties, or specify a custom property. |

### Any recipients

The conditions and exceptions in this section provide a unique capability that affects *all* recipients when the message contains at least one of the specified recipients. For example, let's say you have a rule that rejects messages. If you use a recipient condition from the Recipients section, the message is only rejected for those specified recipients. For example, if the rule finds the specified recipient in a message, but the message contains five other recipients, then the message is rejected for that one recipient, and is delivered to the five other recipients.

If you add a recipient condition from this section, that same message is rejected for the detected recipient and the five other recipients.

Conversely, a recipient exception from this section *prevents* the rule action from being applied to *all* recipients of the message, not just for the detected recipients.

Note

These conditions don't consider messages that are sent to recipient proxy addresses. They only match messages that are sent to the recipient's primary email address.

These conditions are applied to all recipients in the current fork of the message only. If the message was bifurcated by any other action (for example, anti-malware or an earlier mail flow rule), the action will be applied on the matching fork only.

| Condition or exception in the EAC | Condition and exception parameters in Exchange Online PowerShell | Property type | Description |
| --- | --- | --- | --- |
| **Any recipient address includes**<br>**Any recipient** &gt; **address includes any of these words** | *AnyOfRecipientAddressContainsWords* *ExceptIfAnyOfRecipientAddressContainsWords* | `Words` | Messages that contain the specified words in the **To**, **Cc**, or **Bcc** fields of the message. |
| **Any recipient address matches**<br>**Any recipient** &gt; **address matches any of these text patterns** | *AnyOfRecipientAddressMatchesPatterns* *ExceptIfAnyOfRecipientAddressMatchesPatterns* | `Patterns` | Messages where the **To**, **Cc**, or **Bcc** fields contain text patterns that match the specified regular expressions. |

### Message sensitive information types, To and Cc values, size, and character sets

The conditions in this section that look for values in the **To** and **Cc** fields behave like the conditions in the Any recipients section (*all* recipients of the message are affected by the rule, not just the detected recipients).

Note

- The recipient conditions in this section don't consider messages that are sent to recipient proxy addresses. They only match messages that are sent to the recipient's primary email address.
- For more information about using Microsoft 365 groups with the recipient conditions in this section, see the Addresses entry in the Property types section.

| Condition or exception in the EAC | Condition and exception parameters in Exchange Online PowerShell | Property type | Description |
| --- | --- | --- | --- |
| **The To box contains**<br>**The message** &gt; **To box contains this person** | *AnyOfToHeader* *ExceptIfAnyOfToHeader* | `Addresses` | Messages where the **To** field includes any of the specified recipients. |
| **The To box contains a member of**<br>**The message** &gt; **To box contains a member of this group** | *AnyOfToHeaderMemberOf* *ExceptIfAnyOfToHeaderMemberOf* | `Addresses` | Messages where the **To** field contains a recipient who is a member of the specified distribution group, mail-enabled security group, or Microsoft 365 group. |
| **The Cc box contains**<br>**The message** &gt; **Cc box contains this person** | *AnyOfCcHeader* *ExceptIfAnyOfCcHeader* | `Addresses` | Messages where the **Cc** field includes any of the specified recipients. |
| **The Cc box contains a member of**<br>**The message** &gt; **contains a member of this group** | *AnyOfCcHeaderMemberOf* *ExceptIfAnyOfCcHeaderMemberOf* | `Addresses` | Messages where the **Cc** field contains a recipient who is a member of the specified distribution group or mail-enabled security group. |
| **The To or Cc box contains**<br>**The message** &gt; **To or Cc box contains this person** | *AnyOfToCcHeader* *ExceptIfAnyOfToCcHeader* | `Addresses` | Messages where the **To** or **Cc** fields contains any of the specified recipients. |
| **The To or Cc box contains a member of**<br>**The message** &gt; **To or Cc box contains a member of this group** | *AnyOfToCcHeaderMemberOf* *ExceptIfAnyOfToCcHeaderMemberOf* | `Addresses` | Messages where the **To** or **Cc** fields contains a recipient who is a member of the specified distribution group or mail-enabled security group. |
| **The message size is greater than or equal to**<br>**The message** &gt; **size is greater than or equal to** | *MessageSizeOver* *ExceptIfMessageSizeOver* | `Size` | Messages where the total size (message plus attachments) is greater than or equal to the specified value. <br> In the EAC, you can only specify the size in kilobytes (KB). <br><br>**Note**: Message size limits on mailboxes are evaluated before mail flow rules' action. A message that's too large for a mailbox will be rejected before a rule with this condition is able to act on the message. |
| **The message character set name includes any of these words**<br>**The message** &gt; **character set name includes any of these words** | *ContentCharacterSetContainsWords* *ExceptIfContentCharacterSetContainsWords* | `CharacterSets` | Messages that have any of the specified character set names. |

### Sender and recipient

| Condition or exception in the EAC | Condition and exception parameters in Exchange Online PowerShell | Property type | Description |
| --- | --- | --- | --- |
| **The sender is one of the recipient's**<br>**The sender and the recipient** &gt; **the sender's relationship to a recipient is** | *SenderManagementRelationship* *ExceptIfSenderManagementRelationship* | `ManagementRelationship` | Messages where the sender is either the manager of a recipient or is managed by a recipient. |
| **The message is between members of these groups**<br>**The sender and the recipient** &gt; **the message is between members of these groups** | *BetweenMemberOf1* and *BetweenMemberOf2* *ExceptIfBetweenMemberOf1* and *ExceptIfBetweenMemberOf2* | `Addresses` | Messages that are sent between members of the specified distribution groups or mail-enabled security groups. <br> For more information about using Microsoft 365 groups with this condition, see the Addresses entry in the Property types section. |
| **The manager of the sender or recipient is**<br>**The sender and the recipient** &gt; **the manager of the sender or recipient is this person** | *ManagerForEvaluatedUser* and *ManagerAddress* *ExceptIfManagerForEvaluatedUser* and *ExceptIfManagerAddress* | First property: `EvaluatedUser`<br> Second property: `Addresses` | Messages where a specified user is either the manager of the sender or of a recipient. |
| **The sender's and any recipient's property compares as**<br>**The sender and the recipient** &gt; **the sender and recipient property compares as** | *ADComparisonAttribute* and *ADComparisonOperator* *ExceptIfADComparisonAttribute* and *ExceptIfADComparisonOperator* | First property: `ADAttribute`<br> Second property: `Evaluation` | Messages where the specified Active Directory attributes for the sender and recipient either match or don't match. |

### Message properties

| Condition or exception in the EAC | Condition and exception parameters in Exchange Online PowerShell | Property type | Description |
| --- | --- | --- | --- |
| **The message type is**<br>**The message properties** &gt; **include the message type** | *MessageTypeMatches* *ExceptIfMessageTypeMatches* | `MessageType` | Messages of the specified type. **Note**: When Outlook or Outlook on the web (formerly known as Outlook Web App) is configured to forward a message, the **ForwardingSmtpAddress** property is added to the message. In thin clients like Outlook on the web, encryption as a message type is currently not supported.  If the message has been forwarded using [mailbox forwarding](../../recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding) (also known as SMTP Forwarding), this condition/exception **will not** match during mail flow rule evaluation. |
| **The message is classified as**<br>**The message properties** &gt; **include this classification** | *HasClassification* *ExceptIfHasClassification* | `MessageClassification` | Messages that have the specified message classification. This classification is a custom message classification that you can create in your organization by using the **New-MessageClassification** cmdlet. <br>**Note**: This condition/exception isn't available in the Built-in security add-on for on-premises mailboxes. |
| **The message isn't marked with any classifications**<br>**The message properties** &gt; **don't include any classification** | *HasNoClassification* *ExceptIfHasNoClassification* | n/a | Messages that don't have a message classification. <br>**Note**: This condition/exception isn't available in the Built-in security add-on for on-premises mailboxes. |
| **The message importance is set to**<br>**The message properties** &gt; **include the importance level** | *WithImportance* *ExceptIfWithImportance* | `Importance` | Messages that are marked with the specified "Importance" level. |

### Message headers

Note

The search for words or text patterns in the subject or other header fields in the message occurs *after* the message has been decoded from the MIME content transfer encoding method that was used to transmit the binary message between SMTP servers in ASCII text. You can't use conditions or exceptions to search for the raw (typically, Base64) encoded values of the subject or other header fields in messages.

| Condition or exception in the EAC | Condition and exception parameters in Exchange Online PowerShell | Property type | Description |
| --- | --- | --- | --- |
| **A message header includes**<br>**A message header** &gt; **includes any of these words** | *HeaderContainsMessageHeader* and *HeaderContainsWords* *ExceptIfHeaderContainsMessageHeader* and *ExceptIfHeaderContainsWords* | First property: `MessageHeaderField`<br> Second property: `Words` | Messages that contain the specified header field, and the value of that header field contains the specified words. <br> The name of the header field and the value of the header field are always used together. |
| **A message header matches**<br>**A message header** &gt; **matches these text patterns** | *HeaderMatchesMessageHeader* and *HeaderMatchesPatterns* *ExceptIfHeaderMatchesMessageHeader* and *ExceptIfHeaderMatchesPatterns* | First property: `MessageHeaderField`<br> Second property: `Patterns` | Messages that contain the specified header field, and the value of that header field contains the specified regular expressions. <br> The name of the header field and the value of the header field are always used together. |

## Property types

The property types that are used in conditions and exceptions are described in the following table:

Note

If the property is a string, trailing spaces aren't allowed.

| Property type | Valid values | Description |
| --- | --- | --- |
| `ADAttribute` | Select from a predefined list of Active Directory attributes | You can check against any of the following Active Directory attributes: <br>- **City**<br>- **Company**<br>- **Country**<br>- **CustomAttribute1 - CustomAttribute15**<br>- **Department**<br>- **DisplayName**<br>- **Email**<br>- **FaxNumber**<br>- **FirstName**<br>- **HomePhoneNumber**<br>- **Initials**<br>- **LastName**<br>- **Manager**<br>- **MobileNumber**<br>- **Notes**<br>- **Office**<br>- **OtherFaxNumber**<br>- **OtherHomePhoneNumber**<br>- **OtherPhoneNumber**<br>- **PagerNumber**<br>- **PhoneNumber**<br>- **POBox**<br>- **State**<br>- **Street**<br>- **Title**<br>- **UserLogonName**<br>- **ZipCode**<br><br><br> In the EAC, to specify multiple words or text patterns for the same attribute, separate the values with commas. For example, the value `San Francisco,Palo Alto` for the **City** attribute looks for "City equals San Francisco" or "City equals Palo Alto". <br><br> In Exchange Online PowerShell, use the syntax `"AttributeName1:Value1,Value 2 with spaces,Value3...","AttributeName2:Word4,Value 5 with spaces,Value6..."`, where `Value` is the word or text pattern that you want to match, for example, `"City:San Francisco,Palo Alto"` or `"City:San Francisco,Palo Alto"`, `"Department:Sales,Finance"`. <br><br> When you specify multiple attributes, or multiple values for the same attribute, the **or** operator is used. Don't use values with leading or trailing spaces. <br><br> The **Country** attribute requires the two-letter ISO 3166-1 country code value (for example, DE for Germany). For more information, see [Country Codes - ISO 3166](https://www.iso.org/iso-3166-country-codes.html). |
| `Addresses` | Exchange Online recipients | Depending on the nature of the condition or exception, you might be able to specify any mail-enabled object in the organization (for example, recipient-related conditions), or you might be limited to a specific object type (for example, groups for group membership conditions). And, the condition or exception might require one value, or allow multiple values. <br> In Exchange Online PowerShell, separate the multiple values by commas. <br><br> This condition doesn't consider messages that are sent to recipient proxy addresses. It only matches messages that are sent to the recipient's primary email address. <br><br> The recipient picker in the EAC doesn't allow you to select Microsoft 365 groups from the list of recipients. But, you can enter the email address of a Microsoft 365 group in the box next to **Check names**, and then validate the email address by selecting **Check names**, which will add the group to the **add** box. |
| `CharacterSets` | Array of character set names | One or more content character sets that exist in a message. For example:<br>- `Arabic/iso-8859-6`<br>- `Chinese/big5`<br>- `Chinese/euc-cn`<br>- `Chinese/euc-tw`<br>- `Chinese/gb2312`<br>- `Chinese/iso-2022-cn`<br>- `Cyrillic/iso-8859-5`<br>- `Cyrillic/koi8-r`<br>- `Cyrillic/windows-1251`<br>- `Greek/iso-8859-7`<br>- `Hebrew/iso-8859-8`<br>- `Japanese/euc-jp`<br>- `Japanese/iso-022-jp`<br>- `Japanese/shift-jis`<br>- `Korean/euc-kr`<br>- `Korean/johab`<br>- `Korean/ks_c_5601-1987`<br>- `Turkish/windows-1254`<br>- `Turkish/iso-8859-9`<br>- `Vietnamese/tcvn` |
| `DomainName` | Array of SMTP domains | For example, `contoso.com` or `eu.contoso.com`. <br> In Exchange Online PowerShell, you can specify multiple domains separated by commas. |
| `EvaluatedUser` | Single value of **Sender** or **Recipient** | Specifies whether the rule is looking for the manager of the sender or of the recipient. |
| `Evaluation` | Single value of **Equal** or **Not equal** (`NotEqual`) | When comparing the Active Directory attribute of the sender and recipients, this property specifies whether the values should match, or not match. |
| `Importance` | Single value of **Low**, **Normal**, or **High** | The "Importance" level that was assigned to the message by the sender in Outlook or Outlook on the web. |
| `IPAddressRanges` | Array of IP addresses or address ranges | You enter the IPv4 addresses using the following syntax: <br>- **Single IP address**: For example, `192.168.1.1`.<br>- **IP address range**: For example, `192.168.0.1-192.168.0.254`.<br>- **Classless InterDomain Routing (CIDR) IP address range**: For example, `192.168.0.1/25`.<br><br><br> In Exchange Online PowerShell, you can specify multiple IP addresses or ranges separated by commas. |
| `ManagementRelationship` | Single value of **Manager** or **Direct report** (`DirectReport`) | Specifies the relationship between the sender and any of the recipients. The rule checks the **Manager** attribute in Active Directory to see if the sender is the manager of a recipient or is managed by a recipient. |
| `MessageClassification` | Single message classification | In the EAC, you select from the list of message classifications that you've created. <br> In Exchange Online PowerShell, you use the **Get-MessageClassification** cmdlet to identify the message classification. <br><br> For example, use the following command to search for messages with the `Company Internal` classification and prepend the message subject with the value `CompanyInternal`: `New-TransportRule "Rule Name" -HasClassification @(Get-MessageClassification "Company Internal").Identity -PrependSubject "CompanyInternal"` |
| `MessageHeaderField` | Single string | Specifies the name of the header field. The name of the header field is always paired with the value in the header field (word or text pattern match). The message header is a collection of required and optional header fields in the message. Examples of header fields are **To**, **From**, **Received**, and **Content-Type**. Official header fields are defined in RFC 5322. Unofficial header fields start with **X-** and are known as X-headers. |
| `MessageType` | Single message type value | Specifies one of the following message types: <br>- **Automatic reply** (`OOF`)<br>- **Auto-forward** (`AutoForward`)<br>- **Encrypted**<br>- **Calendaring**<br>- **Permission controlled** (`PermissionControlled`)<br>- **Voicemail**<br>- **Signed**<br>- **Approval request** (`ApprovalRequest`)<br>- **Read receipt** (`ReadReceipt`)<br><br><br>**Note**: When Outlook or Outlook on the web is configured to forward a message, the **ForwardingSmtpAddress** property is added to the message. |
| `Patterns` | Array of regular expressions | Specifies one or more regular expressions that are used to identify text patterns in values. For more information, see [Regular Expression Syntax](/en-us/visualstudio/ide/using-regular-expressions-in-visual-studio). <br> In Exchange Online PowerShell, you specify multiple regular expressions separated by commas, and you enclose each regular expression within quotation marks (").  Regular Expressions used in Transport Rules are **NOT** case sensitive. |
| `SCLValue` | One of the following values: <br>- **Bypass spam filtering** (`-1`)<br>- Integers 0 through 9 | Specifies the spam confidence level (SCL) value submitted by a rule. The value is an input to cloud filtering, not a final verdict, and the SCL value stamped on the message might differ. For more information, see [Use mail flow rules to set the SCL](use-rules-to-set-scl). |
| `Size` | Single size value | Specifies the size of an attachment or the whole message. <br> In the EAC, you can only specify the size in kilobytes (KB). <br><br> In Exchange Online PowerShell, when you enter a value, qualify the value with one of the following units: <br><br>- `B` (bytes)<br>- `KB` (kilobytes)<br>- `MB` (megabytes)<br>- `GB` (gigabytes)<br><br><br> For example, `20 MB`. Unqualified values are typically treated as bytes, but small values may be rounded up to the nearest kilobyte. |
| `SupervisionList` | Single value of **Allow** or **Block** | Supervision policies were a feature in Live@edu that allowed you to control who could send mail to and receive mail from users in your organization (for example, the closed campus and anti-bullying policies). In Microsoft 365 and Office 365, you can't configure supervision list entries on mailboxes. |
| `UserScopeFrom` | Single value of **Inside the organization** (`InOrganization`) or **Outside the organization** (`NotInOrganization`) | A sender is considered to be inside the organization if either of the following conditions is true: <br>- The message was sent or received over an authenticated connection AND the sender meets at least one of the following criteria: The sender is a mailbox or a mail user or a group, or a mail-enabled public folder in the organization.<br>- The sender's email address is in an accepted domain that's configured as an authoritative domain or in an internal relay domain, **and** the message was sent or received over an authenticated connection. For more information about accepted domains, see [Manage accepted domains in Exchange Online](../../mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains).<br><br><br> A sender is considered to be outside the organization if either of the following conditions is true: <br><br>- The sender's email address isn't in an accepted domain.<br>- The sender's email address is in an accepted domain that's configured as an external relay domain.<br><br><br>**Note**: To determine whether mail contacts are considered to be inside or outside the organization, the sender's address is compared with the organization's accepted domains. |
| `UserScopeTo` | One of the following values: <br>- **Inside the organization** (`InOrganization`)<br>- **Outside the organization** (`NotInOrganization`) | A recipient is considered to be inside the organization if any of the following conditions are true: <br>- The recipient is a mailbox, mail user, group, or mail-enabled public folder that exists inside the organization.<br>- The recipient's email address is in an accepted domain that's configured as an authoritative domain or in an internal relay domain, **and** the message was sent or received over an authenticated connection.<br>- The recipient's domain is in a remote domain with the *IsInternal* parameter being set to the value `$true`.<br><br><br> A recipient is considered to be outside the organization if either of the following conditions is true: <br><br>- The recipient's email address isn't in an accepted domain.<br>- The recipient's email address is in an accepted domain that's configured as an external relay domain. |
| `Words` | Array of strings | Specifies one or more words to look for. The words aren't case-sensitive, and can be surrounded by spaces and punctuation marks. Wildcards and partial matches aren't supported. For example, "contoso" matches " Contoso". <br> However, if the text is surrounded by other characters, it isn't considered a match. For example, "contoso" doesn't match the following values: <br><br>- Acontoso<br>- Contosoa<br>- Acontosob<br><br><br> The asterisk (\*) is treated as a literal character, and isn't used as a wildcard character. <br><br> The "at" sign (@) is also treated as a literal character. Therefore, if it's used when searching Recipient Addresses, it won't match. For example: <br><br>- @contoso.com won't match user@contoso.com<br>- contoso.com will match user@contoso.com<br><br><br> In this scenario, the correct way to set up matching patterns is to use either **ExceptIfRecipientDomainIs** or **ExceptIfRecipientAddressMatchesPatterns** |

## For more information

[Mail flow rules (transport rules) in Exchange Online](mail-flow-rules)

[Mail flow rule actions in Exchange Online](mail-flow-rule-actions)

[Mail flow rules (transport rules) in Exchange Online](mail-flow-rules)

[New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule)