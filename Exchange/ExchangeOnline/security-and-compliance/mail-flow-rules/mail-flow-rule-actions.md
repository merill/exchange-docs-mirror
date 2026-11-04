---
layout: Conceptual
title: Mail flow rule actions in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rule-actions
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
description: Learn about the actions that are available for mail flow rules in cloud-based organizations.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: a5dfe768-fe26-4290-a801-84b3499f1bc4
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.custom: msecd-doc-authoring-1015
ms.date: 2026-08-11T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: a8d245fb-eb4b-879d-4da8-7e7be414a179
document_version_independent_id: a05b031b-db9a-6f28-09a3-68640eb9c570
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/mail-flow-rule-actions.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/mail-flow-rule-actions
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/mail-flow-rule-actions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 2cbe031f-83be-b970-116a-2f6cc035c238
---

# Mail flow rule actions in Exchange Online | Microsoft Learn

In cloud-based organizations, actions in mail flow rules (also known as transport rules) specify what you want to do to messages that match conditions of the rule. For example, you can create a rule that forwards messages from specific senders to a moderator, or adds a disclaimer or personalized signature to all outbound messages.

Actions typically require additional properties. For example, when the rule redirects a message, you need to specify where to redirect the message. Some actions have multiple properties that are available or required. For example, when the rule adds a header field to the message header, you need to specify both the name and value of the header. When the rule adds a disclaimer to messages, you need to specify the disclaimer text, but you can also specify where to insert the text, or what to do if the disclaimer can't be added to the message. Typically, you can configure multiple actions in a rule, but some actions are exclusive. For example, one rule can't reject and redirect the same message.

For more information about mail flow rules, including how multiple actions are handled, see [Mail flow rules (transport rules) in Exchange Online](mail-flow-rules).

For more information about conditions and exceptions in mail flow rules, see [Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions).

For more information about actions in mail flow rules in Exchange Server, see [Mail flow rule actions in Exchange Server](../../policy-and-compliance/mail-flow-rules/actions).

## Actions for mail flow rules in Exchange Online

The actions that are available in mail flow rules in cloud-based organizations are described in the following table. Valid values for each property are described in the Property values section.

Note

- After you select an action in the Exchange admin center (EAC), the value that's ultimately shown in the **Do the following** field is often different from the click-path you selected. Also, when you create new rules, you can sometimes (depending on the selections you make) select a short action name from a template (a filtered list of actions) instead of following the complete click-path. The short names and full click-path values are shown in the EAC column in the table.
- The names of some of the actions that are returned by the **Get-TransportRuleAction** cmdlet are different than the corresponding parameter names, and multiple parameters might be required for an action.

| Action in the EAC | Action parameter in PowerShell | Property | Description |
| --- | --- | --- | --- |
| **Forward the message for approval to**<br>**Forward the message for approval** &gt; **to these people** | *ModerateMessageByUser* | `Addresses` | Forwards the message to the specified moderators as an attachment wrapped in an approval request. For more information, see [Use mail flow rules for message approval scenarios in Exchange Online](common-message-approval-scenarios). You can't use a distribution group as a moderator. <br>**Note**: This action isn't available in the Built-in security add-on for on-premises mailboxes. |
| **Forward the message for approval to the sender's manager**<br>**Forward the message for approval** &gt; **to the sender's manager** | *ModerateMessageByManager* | n/a | Forwards the message to the sender's manager for approval. <br> This action only works if the sender's **Manager** attribute is defined. Otherwise, the message is delivered to the recipients without moderation. <br><br>**Note**: This action isn't available in the Built-in security add-on for on-premises mailboxes. |
| **Redirect the message to**<br>**Redirect the message to** &gt; **these recipients** | *RedirectMessageTo* | `Addresses` | Redirects the message to the specified recipients. The message isn't delivered to the original recipients, and no notification is sent to the sender or the original recipients. <br>**Note**: In Exchange Online, you can't add a distribution group as a recipient. |
| **Deliver the message to the hosted quarantine**<br>**Redirect the message to** &gt; **hosted quarantine** | *Quarantine* | n/a | Delivers the message to the quarantine. For more information, see [Quarantined email messages](/en-us/defender-office-365/quarantine-about).  If the action is executed for a rule that's not last in the rule collection, as soon as the action is executed, current rule evaluation is stopped. When the message is released from Quarantine, rest of the rules in the rule collection (that are not evaluated initially because message is sent to quarantine) aren't evaluated at all. |
| **Use the following connector**<br>**Redirect the message to** &gt; **the following connector** | *RouteMessageOutboundConnector* | `OutboundConnector` | Uses the specified outbound connector to deliver the message. For more information about connectors, see [Configure mail flow using connectors](../../mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow). |
| **Reject the message with the explanation**<br>**Block the message** &gt; **reject the message and include an explanation** | *RejectMessageReasonText* | `String` | Returns the message to the sender in a non-delivery report (also known as an NDR or bounce message) with the specified text as the rejection reason. The recipient doesn't receive the original message or notification. <br> The default enhanced status code that's used is `5.7.1`. <br><br> When you create or modify the rule in PowerShell, you can specify the DSN code by using the *RejectMessageEnhancedStatusCode* parameter. |
| **Reject the message with the enhanced status code**<br>**Block the message** &gt; **reject the message with the enhanced status code of** | *RejectMessageEnhancedStatusCode* | `DSNEnhancedStatusCode` | Returns the message to the sender in an NDR with the specified enhanced delivery status notification (DSN) code. The recipient doesn't receive the original message or notification. <br> Valid DSN codes are `5.7.1` or `5.7.900` through `5.7.999`. <br><br> The default reason text that's used is `Delivery not authorized, message refused`. <br><br> When you create or modify the rule in PowerShell, you can specify the rejection reason text by using the *RejectMessageReasonText* parameter. |
| **Delete the message without notifying anyone**<br>**Block the message** &gt; **delete the message without notifying anyone** | *DeleteMessage* | n/a | Silently drops the message without sending a notification to the recipient or the sender. |
| **Add recipients to the Bcc box**<br>**Add recipients** &gt; **to the Bcc box** | *BlindCopyTo* | `Addresses` | Adds one or more recipients to the **Bcc** field of the message. The original recipients aren't notified, and they can't see the additional addresses. <br>**Note**: In Exchange Online, you can't add a distribution group as a recipient. |
| **Add recipients to the To box**<br>**Add recipients** &gt; **to the To box** | *AddToRecipients* | `Addresses` | Adds one or more recipients to the **To** field of the message. The original recipients can see the additional addresses. <br>**Note**: In Exchange Online, you can't add a distribution group as a recipient. |
| **Add recipients to the Cc box**<br>**Add recipients** &gt; **to the Cc box** | *CopyTo* | `Addresses` | Adds one or more recipients to the **Cc** field of the message. The original recipients can see the additional address. <br>**Note**: In Exchange Online, you can't add a distribution group as a recipient. |
| **Add the sender's manager as a recipient**<br>**Add recipients** &gt; **add the sender's manager as a recipient** | *AddManagerAsRecipientType* | `AddedManagerAction` | Adds the sender's manager to the message as the specified recipient type (**To**, **Cc**, **Bcc**), or redirects the message to the sender's manager without notifying the sender or the recipient. <br> This action only works if the sender's **Manager** attribute is defined in Active Directory. |
| **Append the disclaimer**<br>**Apply a disclaimer to the message** &gt; **append a disclaimer** | *ApplyHtmlDisclaimerText* *ApplyHtmlDisclaimerFallbackAction* *ApplyHtmlDisclaimerLocation* | First property: `DisclaimerText` Second property: `DisclaimerFallbackAction` Third property (PowerShell only): `DisclaimerTextLocation` | Applies the specified HTML disclaimer to the end of the message.  When you create or modify the rule in PowerShell, use the *ApplyHtmlDisclaimerLocation* parameter with the value `Append`. |
| **Prepend the disclaimer**<br>**Apply a disclaimer to the message** &gt; **prepend a disclaimer** | *ApplyHtmlDisclaimerText* *ApplyHtmlDisclaimerFallbackAction* *ApplyHtmlDisclaimerLocation* | First property: `DisclaimerText` Second property: `DisclaimerFallbackAction` Third property (PowerShell only): `DisclaimerTextLocation` | Applies the specified HTML disclaimer to the beginning of the message.  When you create or modify the rule in PowerShell, use the *ApplyHtmlDisclaimerLocation* parameter with the value `Prepend`. |
| **Remove this header**<br>**Modify the message properties** &gt; **remove a message header** | *RemoveHeader* | `MessageHeaderField` | Removes the specified header field from the message header. |
| **Set the message header to this value**<br>**Modify the message properties** &gt; **set a message header** | *SetHeaderName* *SetHeaderValue* | First property: `MessageHeaderField` Second property: `String` | Adds or modifies the specified header field in the message header, and sets the header field to the specified value. |
| **Apply a message classification**<br>**Modify the message properties** &gt; **apply a message classification** | *ApplyClassification* | `MessageClassification` | Applies the specified message classification to the message. <br>**Note**: This action isn't available in the Built-in security add-on for on-premises mailboxes. |
| **Set the spam confidence level (SCL) to**<br>**Modify the message properties** &gt; **set the spam confidence level (SCL)** | *SetSCL* | `SCLValue` | Submits the specified SCL value as an input to spam filtering. In cloud filtering, the value doesn't determine the final verdict or action, and the SCL value stamped on the message might differ. SCL is used primarily in on-premises Exchange environments. This action doesn't apply to intra-organizational (intra-org) messages. For more information, see [Use mail flow rules to set the SCL](use-rules-to-set-scl). |
| **Apply Office 365 Message Encryption and rights protection**<br>**Apply Message Encryption and rights protection to the message with**<br><br>**Modify the message security** &gt; **Message Encryption and rights protection** | *ApplyRightsProtectionTemplate* | `RMSTemplate` | Applies the specified Azure Rights Management (Azure RMS) template to the message. Azure RMS is part of Azure Information Protection. For more information, see [Set up new Message Encryption capabilities](/en-us/purview/set-up-new-message-encryption-capabilities). |
| **Require TLS encryption**<br>**Modify the message security** &gt; **require TLS encryption** | *RouteMessageOutboundRequireTls* | n/a | Forces the outbound messages to be routed over a TLS encrypted connection. |
| **Encrypt the messages with the previous version of OME**<br>**Modify the message security** &gt; **Apply Office the previous version of OME** | *ApplyOME* | n/a | If you haven't moved your Microsoft 365 or Office 365 organization to Microsoft Purview Message Encryption that's built on Azure Information Protection, this action encrypts the message and attachments with the previous version of OME. <br>**Notes**: <br><br>- We recommend that you make a plan to move to OME on Azure Information Protection as soon as it's reasonable for your organization. For instructions, see [Set up new Message Encryption capabilities](/en-us/purview/set-up-new-message-encryption-capabilities).<br>- If you receive an error stating that IRM licensing isn't enabled, you can't set up the previous version of OME. If you set up OME now, you'll set up the OME capabilities that are built on Azure Information Protection. |
| **Remove the previous version of OME from the message**<br>**Modify the message security** &gt; **Remove the previous version of OME** | *RemoveOME* | n/a | Decrypt the message and attachments from the previous version of OME so that users don't need to sign in to the encryption portal to view them. This action is only available for messages that are sent within your organization. |
| **Remove Office 365 Message Encryption and rights protection**<br>**Modify the message security** &gt; **Message Encryption and rights protection** | *RemoveOMEv2* | n/a | Remove the Azure RMS template from the message. |
| **Prepend the subject of the message with** | *PrependSubject* | `String` | Adds the specified text to the beginning of the **Subject** field of the message. Consider using a space or a colon (:) as the last character of the specified text to differentiate it from the original subject text.  To prevent the same string from being added to messages that already contain the text in the subject (for example, replies), add the **The subject includes** (*ExceptIfSubjectContainsWords*) exception to the rule. |
| **Generate incident report and send it to** | *GenerateIncidentReport* *IncidentReportContent* | First property: `Addresses` Second property: `IncidentReportContent` | Sends an incident report that contains the specified content to the specified recipients. <br> If the rule with this action is matched, this action is going to be executed even if the rule is in Audit or AuditAndNotify mode.  Note that GenerateIncidentReport action will not be executed for the notifications or other incident reports generated by DLP or Mail flow rules. |
| **Notify the recipient with a message** | *GenerateNotification* | `NotificationMessageText` | Specifies the text, HTML tags, and message keywords to include in the notification message that's sent to the message's recipients that matched the Transport Rule. For example, you can notify recipients that the message was rejected by the rule, or marked as spam and delivered to their Junk Email folder. Each matched recipient receives separate notification.  If the rule with this action is matched, this action is going to be executed even if the rule is in AuditAndNotify mode, but it will not be executed if the rule is in the Audit mode. |
| **Properties of this rule** section &gt; **Audit this rule with severity level** | *SetAuditSeverity* | `AuditSeverityLevel` | Specifies whether to: <br>- Prevent the generation of an incident report and the corresponding entry in the message tracking log.<br>- Generate an incident report and the corresponding entry in the message tracking log with the specified severity level (low, medium, or high). |
| **Properties of this rule** section &gt; **Stop processing more rules**<br>**More options** &gt; **Properties of this rule** section &gt; **Stop processing more rules** | *StopRuleProcessing* | n/a | Specifies that after the message is affected by the rule, the message is exempt from processing by other rules. |

## Property values

The property values that are used for actions in mail flow rules are described in the following table:

| Property | Valid values | Description |
| --- | --- | --- |
| `AddedManagerAction` | One of the following values: <br>- **To**<br>- **Cc**<br>- **Bcc**<br>- **Redirect** | Specifies how to include the sender's manager in messages. <br> If you select **To**, **Cc**, or **Bcc**, the sender's manager is added as a recipient in the specified field. <br><br> If you select **Redirect**, the message is only delivered to the sender's manager without notifying the sender or the recipient. <br><br> This action only works if the sender's **Manager** is defined. |
| `Addresses` | Exchange recipients | Depending on the action, you might be able to specify any mail-enabled object in the organization, or you might be limited to a specific object type. Typically, you can select multiple recipients, but you can only send an incident report to one recipient. |
| `AuditSeverityLevel` | One of the following values: <br>- Uncheck **Audit this rule with severity level**, or select **Audit this rule with severity level** with the value **Not specified** (`DoNotAudit`)<br>- **Low**<br>- **Medium**<br>- **High** | The values **Low**, **Medium**, or **High** specify the severity level that's assigned to the incident report and to the corresponding entry in the message tracking log. <br> The other value prevents an incident report from being generated, and prevents the corresponding entry from being written to the message tracking log. |
| `DisclaimerFallbackAction` | One of the following values: <br>- **Wrap**<br>- **Ignore**<br>- **Reject** | Specifies what to do if the disclaimer can't be applied to a message (for example, encrypted or signed messages where the contents can't be altered). The available fallback actions are: <br>- **Wrap**: A new message is created and the original message is added to it as an attachment. The disclaimer text is added to the new message, which is delivered to the recipients. This value is the default value.<br>    - If you want other rules to examine and act on the original message (which is now an attachment in the new message), ensure that those rules are applied *before* the disclaimer rule by using a lower priority for the disclaimer rule and higher priority for other rules.<br>    - If the process of inserting the original message as an attachment in the new message fails, the original message isn't delivered. The original message is returned to the sender in an NDR.<br>- **Ignore**: The rule is ignored and the original message is delivered without the disclaimer.<br>- **Reject**: The original message is returned to the sender in an NDR. |
| `DisclaimerText` | HTML string | Specifies the disclaimer text, which can include HTML tags, inline cascading style sheet (CSS) tags, and images by using the IMG tag. The maximum length is 5000 characters, including tags. |
| `DisclaimerTextLocation` | Single value: `Append` or `Prepend` | In PowerShell, you use the *ApplyHtmlDisclaimerLocation* parameter to specify the location of the disclaimer text in the message: <br>- `Append`: Add the disclaimer to the end of the message body. This value is the default value.<br>- `Prepend`: Add the disclaimer to the beginning of the message body. |
| `DSNEnhancedStatusCode` | Single DSN code value: <br>- `5.7.1`<br>- `5.7.900` through `5.7.999` | Specifies the DSN code that's used. You can create custom DSNs by using the **New-SystemMessage** cmdlet. <br> If you don't specify the rejection reason text along with the DSN code, the default reason text that's used is `Delivery not authorized, message refused`. <br><br> When you create or modify the rule in PowerShell, you can specify the rejection reason text by using the *RejectMessageReasonText* parameter. |
| `IncidentReportContent` | One or more of the following values: <br>- **Sender**<br>- **Recipients**<br>- **Subject**<br>- **Cc'd recipients** (`Cc`)<br>- **Bcc'd recipients** (`Bcc`)<br>- **Severity**<br>- **Matching rules** (`RuleDetections`)<br>- **False positive reports** (`FalsePositive`)<br>- **Matching content** (`IdMatch`)<br>- **Original mail** (`AttachOriginalMail`) | Specifies the original message properties to include in the incident report. You can choose to include any combination of these properties. In addition to the properties you specify, the message ID is always included. The available properties are: <br>- **Sender**: The sender of the original message.<br>- **Recipients**, **Cc'd recipients**, and **Bcc'd recipients**: All recipients of the message, or only the recipients in the **Cc** or **Bcc** fields. For each property, only the first 10 recipients are included in the incident report.<br>- **Subject**: The **Subject** field of the original message.<br>- **Severity**: The audit severity of the rule that was triggered. Message tracking logs include all the audit severity levels, and can be filtered by audit severity. <br>     In the EAC, if you clear the **Audit this rule with severity level** check box (in PowerShell, the *SetAuditSeverity* parameter value `DoNotAudit`), rule matches won't appear in the rule reports. <br><br>     If a message is processed by more than one rule, the highest severity is included in any incident reports.<br>- **Matching rules**: The list of rules that the message triggered.<br>- **False positive reports**: The false positive if the sender marked the message as a false positive for a Policy Tip.<br>- **Matching content**: The sensitive information type detected, the exact matched content from the message, and the 150 characters before and after the matched sensitive information.<br>- **Original mail**: The entire message that triggered the rule is attached to the incident report. <br>     In PowerShell, you specify multiple values separated by commas. |
| `MessageClassification` | Single message classification object | In the EAC, you select from the list of available message classifications. <br> In PowerShell, use the **Get-MessageClassification** cmdlet to see the message classification objects that are available. |
| `MessageHeaderField` | Single string | Specifies the SMTP message header field to add, remove, or modify. <br> The message header is a collection of required and optional header fields in the message. Examples of header fields are **To**, **From**, **Received**, and **Content-Type**. Official header fields are defined in RFC 5322. Unofficial header fields start with **X-** and are known as X-headers. |
| `NotificationMessageText` | Any combination of plain text, HTML tags, and keywords | Specified the text to use in a recipient notification message. <br> In addition to plain text and HTML tags, you can specify the following keywords that use values from the original message: <br><br>- `%%From%%`<br>- `%%To%%`<br>- `%%Cc%%`<br>- `%%Subject%%`<br>- `%%Headers%%`<br>- `%%MessageDate%%` |
| `OutboundConnector` | Single outbound connector | Specifies the identity of outbound connector that's used to deliver messages. For more information about connectors, see [Configure mail flow using connectors](../../mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow). <br> In the EAC, you select the connector from a list. <br><br> In PowerShell, use the **Get-OutboundConnector** cmdlet to see the connectors that are available. |
| `RMSTemplate` | Single Azure RMS template object | Specifies the Azure Rights Management (Azure RMS) template that's applied to the message. <br> In the EAC, you select the RMS template from a list. <br><br> In PowerShell, use the **Get-RMSTemplate** cmdlet to see the RMS templates that are available. <br><br> For more information about RMS in Microsoft 365 or Office 365, see [What is Azure Information Protection?](/en-us/azure/information-protection/what-is-information-protection). |
| `SCLValue` | One of the following values: <br>- **Bypass spam filtering** (`-1`)<br>- Integers 0 through 9 | Specifies the SCL value submitted by the rule. The value is an input to cloud filtering, not a final verdict, and the SCL value stamped on the message might differ. |
| `String` | Single string | Specifies the text that's applied to the specified message header field, NDR, or event log entry. <br> In PowerShell, if the value contains spaces, enclose the value within quotation marks ("). |

## For more information

[Mail flow rules (transport rules) in Exchange Online](mail-flow-rules)

[Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions)

[Mail flow rules (transport rules) in Exchange Online](mail-flow-rules)