---
layout: Conceptual
title: Use mail flow rules to route email based on a list of words, phrases, or patterns in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-route-email
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: Learn how to use mail flow rules to route email messages based on their contents in Exchange Online.
ms.localizationpriority: medium
ms.author: serdars
ms.topic: how-to
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms.collection:
- exchange-online
- M365-email-calendar
ms.reviewer: 
audience: ITPro
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: b8cf11da-901c-8c9f-2aa3-887c05844e51
document_version_independent_id: 0a2b3d28-f0be-9317-6180-cca2bf89f879
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-route-email.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/use-rules-to-route-email
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-route-email.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: df4523e9-f4d2-312f-8d0a-0770ce778f3e
---

# Use mail flow rules to route email based on a list of words, phrases, or patterns in Exchange Online | Microsoft Learn

In cloud-based organizations, you can use mail flow rules (also known as transport rules) to find and act on messages that contains specific words. This action can help your users comply with your organization's email policies.

For a short list of words or phrases, you can use the Exchange admin center (EAC). For a longer list, you can use [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) to import the words from a text file.

If your Exchange Online organization uses Data loss prevention (DLP), see [Data loss prevention](../data-loss-prevention/data-loss-prevention) for additional options for identifying and routing email that contains sensitive information (DLP isn't available in the Built-in security add-on for on-premises mailboxes).

## Example 1: Use a short list of unacceptable words

If your list of words or phrases is short, you can create a rule using the Exchange admin center. For example, if you want to make sure no one sends email with bad words or with misspellings of your company name, internal acronyms or product names, you could create a rule to block the message and tell the sender. Note that words, phrases, and patterns are not case sensitive.

This example blocks messages with common typos.

![Rule showing blocking a message based on text patterns.](../../exchangeonline/media/a8489cbb-be59-4890-ae30-1431703eeb88.png)

## Example 2: Use a long list of unacceptable words

If your list of words, phrases, or patterns is long, you can put them in a text file with each word, phrase, or pattern on its own line. Use Exchange Online PowerShell to read in the list of keywords into a variable, create a mail flow rule, and assign the variable with the keywords to the mail flow rule condition. For example, the following script takes a list of misspellings from a file called C:\My Documents\misspelled\_companyname.txt.

```PowerShell
$Keywords=Get-Content "C:\My Documents\misspelled_companyname.txt"
New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $Keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."
```

### Using phrases and patterns in the text file

The text file can contain regular expressions for patterns. These expressions are not case-sensitive. Common regular expressions include:

| Expression | Matches |
| --- | --- |
| **.** | Any single character |
| **\*** | Any additional characters |
| **\d** | Any decimal digit |
| [*character\_group*] | Any single character in *character\_group*. |

For example, this text file contains common misspellings of Microsoft.

```text
[mn]sft
[mn]icrosft
[mn]icro soft
[mn].crosoft
```

To learn how to specify patterns using regular expressions, see [Regular Expression Reference](/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference).