---
layout: Conceptual
title: Regular expressions in mail flow rules | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/regular-expressions-usage-transport-rules
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: high
description: How to use regular expressions (RegEx) in mail flow rules (also known as transport rules) in Exchange Online.
ms.topic: overview
author: v-smandalika
ms.author: serdars
ms.reviewer: 
ms.collection:
- Strat_EX_Admin
- exchange-server
f1.keywords:
- NOCSH
audience: ITPro
ms.service: exchange-server-it-pro
ms.date: 2023-08-23T00:00:00.0000000Z
locale: en-us
document_id: 1a511045-a311-16b8-2e16-846bde256b97
document_version_independent_id: c86503be-7eba-ed56-2f5f-fc3a4928f3df
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/regular-expressions-usage-transport-rules.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/regular-expressions-usage-transport-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/regular-expressions-usage-transport-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 4e59a795-c9d6-df54-2956-143d4a54b980
---

# Regular expressions in mail flow rules | Microsoft Learn

You can use regular expressions (RegEx) in conditions and exceptions in mail flow rules (also known as transport rules) to match text patterns in different parts of a message (for example, message headers, sender, recipients, subject, and the message body). Conditions and exceptions determine whether the action in the rule should be applied to an email message.

Note

Due to the variances in customer environments, Microsoft Customer Support Services (CSS) can't participate in the development or testing of custom regular expression scripts ("RegEx scripts"). For RegEX custom script development, testing, and debugging, Microsoft 365 customers will need to rely upon internal IT resources. Alternatively, Microsoft 365 customers may choose to use an external consulting resource such as Microsoft Consulting Services (MCS). Regardless of the script development resource, CSS support engineers aren't available to assist customers with custom RegEx script inquiries.

Looking for management tasks related to mail flow rules? See [Mail flow rules (transport rules) in Exchange Online](../security-and-compliance/mail-flow-rules/mail-flow-rules).

## Simple expressions vs regular expressions

A *simple expression* is a specific value that you want to match exactly in a message. Conditions and exceptions using simple expressions match specific words or text strings. For example, a mail flow rule condition that looks for documents named **Yearly Sales Forecast.docx**.

A *regular expression* is a concise and flexible notation for finding patterns of text in a message. The notation consists of two basic character types:

- **Literal characters**: Text that must exist in the target string. These characters are normal characters, as typed.
- **Metacharacters**: One or more special characters that indicate how the text can vary in the target string.

You can use regular expressions to quickly parse email messages to find specific text patterns. Regular expressions enable you to detect messages with specific types of content, such as social security numbers (SSNs), patent numbers, and phone numbers.

You can't reasonably match variable data with a simple expression because a simple expression requires every possible variation of the value to detect. Matching a large number of simple expressions in message content can be resource intensive. Using regular expressions is more efficient. Instead of specifying all possible variations, you can configure the mail flow rule condition to search for a text pattern.

## Regular expressions in Exchange Online

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), parameter names that end with `MatchesPatterns` use regular expressions. In the [Exchange admin center (EAC)](../exchange-admin-center), conditions and exception names that end with **...matches any of these text patterns** use regular expressions. For more information about mail flow rule conditions and exceptions in Exchange Online, see [Mail flow rule conditions and exceptions (predicates) in Exchange Online](../security-and-compliance/mail-flow-rules/conditions-and-exceptions).

Warning

Carefully test regular expressions. A misconfigured regular expression could yield unexpected matches and cause unwanted mail flow rule behavior, including:

- Undesirable actions on messages and message content.
- Potential data loss.

Complex regular expressions might also affect mail flow performance. Test your regular expressions in a test environment before you implement them in production.

The following table lists the pattern strings that you can use to create a pattern-matching regular expression in Exchange Online:

| Pattern String | Description |
| --- | --- |
| \S | The \S pattern string matches any single character that's not a space. |
| \s | The \s pattern string matches any single white-space character. |
| \D | The \D pattern string matches any non-numeric digit. |
| \d | The \d pattern string matches any single numeric digit. |
| \w | The \w pattern string matches any single Unicode character categorized as a letter or a decimal digit. |
| \W | The \W pattern string matches any single Unicode character not categorized as a letter or a decimal digit. |
| \* | The asterisk ( `*` ) character matches zero or more instances of the previous character. For example, `ab*c` matches the following strings: `ac`, `abc`, and `abbbbc`. |
| | | The Pipe ( | ) character acts as an OR operator. For example, 'contoso|fabrikam' matches any instances of `contoso` or `fabrikam`. |
| ( ) | Parentheses act as grouping delimiters. For example, `\a(bc)*\` matches the following strings: `a`, `abc`, `abcbc`, `abcbcbc`, and so on. |
| `\` | A backslash is used as an escape character before a special character. Special characters are characters used in pattern strings: <br>- Backslash `\`<br>- Pipe |<br>- Asterisk `*`<br>- Opening parenthesis `(`<br>- Closing parenthesis `)`<br>- Caret `^`<br>- Dollar sign `$`<br><br><br> For example, if you want to match a string that contains `(525)`, use `\(525\)`. |
| ^ | The caret ( `^` ) character indicates that the pattern string that follows the caret must exist at the start of the text string being matched. For example, `^fred@contoso` matches `fred@contoso.com` and `fred@contoso.co.uk` but not `alfred@contoso.com`. |
| $ | The dollar-sign ( `$` ) character indicates that the preceding pattern string must exist at the end of the text string being matched. For example, `contoso.com$` matches `adam@contoso.com` and `kim@research.contoso.com` but doesn't match `kim@contoso.com.au`. |

### Constructing regular expressions

By using the preceding table, you can construct a regular expression that matches the pattern of the data that you want to match:

- Working from left to right, examine each character or group of characters in the data that you want to match.
- Read the description of each pattern string to determine how it's applied to the data that you're matching.
- Determine which pattern string in the table represents that character or group of characters, and add that pattern string to the regular expression.

Note

Regular expressions used in Transport Rules are **NOT** case sensitive.

The following example matches North American telephone numbers in the formats 425 555-0100 and 425.555.0100:

```text
425(\s|.)\d\d\d(-|.)\d\d\d\d
```

You can expand on this example by adding the telephone format (425) 555-0100, which uses parentheses around the area code.

The following example matches all three telephone number formats.

```text
\d\d\d((\s|.|-|\)|\)\s)\d\d\d(\s|.|-)\d\d\d\d
```

You can analyze the previous example as follows:

- `\d\d\d`: Requires that exactly three numeric digits appear first.
- `((\s|.|-|\)|\)\s)`: Requires that a space, a period, or a hyphen exists after the three-digit number. Each character-matching string is contained in the grouping delimiters and is separated by the pipe character. This separation means that only one of the specified characters inside the grouping delimiters can exist in this location in the string being matched. For the separation between area code and the next three digits, it also looks for a closed parenthesis, or closed parenthesis and space.
- `\d\d\d`: Requires that exactly three numeric digits appear next.
- `(\s|.|-)`: Requires that a space, a period, or a hyphen exists after the three-digit number.
- `\d\d\d\d`: Requires that exactly four numeric digits appear next.

The previous example matches the following values:

- (425)555.0100
- 425 555 0100
- 425 555 0100
- (425) 555-0100
- 425-555-0100
- (425) 555-0100

## Creating a mail flow that uses a regular expression

The following example creates a mail flow rule in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) that uses regular expressions to match SSNs in the subject of an email message:

```powershell
New-TransportRule -Name "Social Security Number Block Rule" -SubjectOrBodyMatchesPatterns '\d\d\d-\d\d-\d\d\d\d' -RejectMessageEnhancedStatusCode "5.7.1" -RejectMessageReasonText "This message has been rejected because of content restrictions"
```

For detailed syntax and parameter information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).

The following example shows the new mail flow rule:

```PowerShell
Get-TransportRule "Social Security Number Block Rule" | Format-List
```

For detailed syntax and parameter information, see [Get-TransportRule](/en-us/powershell/module/exchangepowershell/get-transportrule).