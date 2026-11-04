---
layout: Conceptual
title: Use mail flow rules to inspect message attachments in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/inspect-message-attachments
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
description: Admins can learn how to configure mail flow rules to inspect message attachments in Exchange Online.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 874d1c78-a8ec-4938-b388-d3208c2fa971
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2025-07-28T00:00:00.0000000Z
locale: en-us
document_id: 4dd230cd-1717-a932-a5c9-02db4f1b050c
document_version_independent_id: 24dcb706-d0d9-61d3-e99d-289db401ffaa
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/inspect-message-attachments.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/inspect-message-attachments
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/inspect-message-attachments.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 796e6392-7f7a-d808-8053-32a5af2c2ec9
---

# Use mail flow rules to inspect message attachments in Exchange Online | Microsoft Learn

In cloud-based organizations, you can inspect email attachments by setting up Exchange mail flow rules (also known as transport rules). Mail flow rules allow you to examine email attachments as a part of your messaging security and compliance needs. When you inspect attachments, you can then take action on the messages based on the content or characteristics of the attachments. Here are some attachment-related tasks you can do by using mail flow rules:

- Search for files with text that matches a pattern you specify, and add a disclaimer at the end of the message.
- Inspect content within attachments and, if there are any keywords you specify, redirect the message to a moderator for approval before it's delivered.
- Check for messages with attachments that can't be inspected and then block the entire message from being sent.
- Check for attachments that exceed a certain size and then notify the sender of the issue, if you choose to prevent the message from being delivered.
- Check whether the properties of an attached Office document match the values that you specify. With this condition, you can integrate the requirements of your mail flow rules and DLP policies with a non-Microsoft classification system, such as SharePoint or the Windows Server File Classification Infrastructure (FCI).
- Create notifications that alert users if they send a message that matches a mail flow rule.
- Block all messages containing attachments. For examples, see [Use mail flow rules for attachment blocking scenarios in Exchange Online](common-attachment-blocking-scenarios).

Note

All of these conditions scan compressed archive attachments.

Exchange Online administrators can create mail flow rules in the Exchange admin center (EAC) at **Mail flow** &gt; **Rules**. You need permissions to do this procedure. After you start to create a new rule, you can see the full list of attachment-related conditions by selecting **Any attachment** under **Apply this rule if**. The attachment-related options are shown in the following diagram.

![List of conditions for attachments.](../../exchangeonline/media/c8ab24df-dbb6-4760-bfb0-b62938bfb447.png)

For more information about mail flow rules, including the full range of conditions and actions that you can choose, see [Mail flow rules (transport rules) in Exchange Online](mail-flow-rules). Customers with the Built-in security add-on for on-premises mailboxes can benefit from the mail flow rules best practices provided in [Best practices for configuring the Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/best-practices-for-configuring-eop). If you're ready to start creating rules, see [Manage mail flow rules in Exchange Online](manage-mail-flow-rules).

Tip

If you suspect that your rule isn't working properly, first check which attachments the message contains.

To inspect which attachments the message contained during mail flow rule evaluation, see [Test-TextExtraction](/en-us/powershell/module/exchangepowershell/test-textextraction).

This method should work.

## Inspect the content within attachments

You can use the mail flow rule conditions in the following table to examine the content of message attachments. For these conditions, only the first 2 megabytes (MB) of text extracted from an attachment is inspected. The 2-MB limit refers to the extracted text, not the file size of the attachment. For example, a 4-MB file might contain less than 2 MB of text so that all of the text would be inspected.

To start using these conditions when inspecting messages, you need to add them to a mail flow rule. For more information about creating or changing rules, see [Manage mail flow rules in Exchange Online](manage-mail-flow-rules).

| Condition name in the EAC | Condition name in Exchange Online PowerShell | Description |
| --- | --- | --- |
| **Any attachment's content includes** **Any attachment** &gt; **content includes any of these words** | *AttachmentContainsWords* | This condition matches messages with supported file type attachments that contain a specified string or group of characters. |
| **Any attachment's content matches** **Any attachment** &gt; **content matches these text patterns** | *AttachmentMatchesPatterns* | This condition matches messages with supported file type attachments that contain a text pattern that matches a specified regular expression. |
| **Any attachment's content can't be inspected** **Any attachment** &gt; **content can't be inspected** | *AttachmentIsUnsupported* | Mail flow rules only can inspect the content of supported file types. If the mail flow rule finds an attachment that isn't supported, the *AttachmentIsUnsupported* condition is triggered. The supported file types are described in the next section. |

Note

- The condition names in Exchange Online PowerShell are parameter names on the **New-TransportRule** and **Set-TransportRule** cmdlets. For more information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).
- For more information more about property types for these conditions, see [Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions).
- For information on how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

### Supported file types for mail flow rule content inspection

The following table lists the file types supported by mail flow rules. The system automatically detects file types by inspecting file properties rather than the actual file name extension, thus helping to prevent malicious hackers from being able to bypass mail flow rule filtering by renaming a file extension. A list of file types with executable code that can be checked within the context of mail flow rules is specified later in this article.

| Category | File extension | Notes |
| --- | --- | --- |
| Adobe PDF | .pdf | None |
| Compressed archive files | `.arj, .bz2, .cab, .chm, .gz, .gzip, .lha, .lzh, .lzma, .mhtml, .msp, .rar, .rar4, .tar, .xar, .xz, .zip, .7z` | None |
| HTML | `.ascx, .asp, .aspx, .css, .hta, .htm, .html, .htw, .htx, .jhtml` | None |
| JSON | `adaptivecard, .json, messagecard` | None |
| Mail | `.eml, .msg, .nws` | None |
| Microsoft Office | `.doc, .docb, .docm, .docx, .dot, .dotm, .dotx, .obd, .obt, .one, .pot, .potm, .potx, .ppa, .ppam, .pps, .ppsm, .ppsx, .ppt, .pptm, .pptx, .xlb, .xlc, .xlm, .xls, .xlsb, .xlsm, .xlsx, .xlt, .xltm, .xltx, .xlw` | The contents of any embedded parts contained within these file types are also inspected. However, any objects that aren't embedded (for example, linked documents) aren't inspected. Content within the custom properties is also scanned. *Note*: *Legacy 97-2003 (.doc, .xls, ppt) files are not recursively inspected for embedded files. To ensure embedded content is inspected, save attachments in modern Office formats (.docx, .xlsx, .pptx).* |
| Microsoft Office xml | `.excelml, .powerpointml, .wordml` | None |
| Microsoft Visio | `.vdw, .vdx, .vsd, .vsdm, .vsdx, .vss, .vssm, .vssx, .vst, .vstm, .vstx, .vsx, .vtx` | None |
| OpenDocument | `.odp, .ods, .odt` | No parts of `.odf` files are processed. For example, if the `.odf` file contains an embedded document, the contents of that embedded document aren't inspected. |
| Other | `.dfx, .dxf, .encoffmetro, .fluid, .mime, .pointpub, .pub, .rtf, .vtt, .xps` | None |
| Text | `.asm, .bat, .c, .class, .cmd, .cpp, .cs, .csv, .cxx, .def, .dic, .h, .hpp, .hxx, .ibq, .idl, .inc, .inf, .ini, .inx, .java, .js, .json, .lnk, .log, .m3u, .messagestorage, .mpx, .php, .pl, .pos, .tsv, .txt, .vcf, .vcs` | Other text based files are also scanned. This list is representative. |
| XML | `.infopathml, .jsp, .mspx, .xml` | None |
| Images | `.bmp, .gif, .jpeg, .jpg, .png, .tif, .tiff` | Text extracted from images using optical character recognition (OCR) is inspected. |

## Inspect the file properties of attachments

The following conditions can be used in mail flow rules to inspect different properties of files that are attached to messages. To start using these conditions when inspecting messages, you need to add them to a mail flow rule. For more information about creating or changing rules, see [Manage mail flow rules](manage-mail-flow-rules).

Note

The *AttachmentNameMatchesPatterns* or *AttachmentExtensionMatchesWords* conditions don't inspect file properties (for example, to detect `.exe` files renamed with `.txt` extensions). To block files based on file property detection, use the [common attachments filter in anti-malware policies](/en-us/defender-office-365/anti-malware-protection-about#true-type-matching-in-the-common-attachments-filter).

| Condition name in the EAC | Condition name in Exchange Online PowerShell | Description |
| --- | --- | --- |
| **Any attachment's file name matches** &lt;br&gt;&lt;br&gt; **Any attachment** &gt; **file name matches these text patterns** | *AttachmentNameMatchesPatterns* | This condition matches messages with attachments whose file name contains the characters you specify. |
| **Any attachment's file extension matches** &lt;br&gt;&lt;br&gt; **Any attachment** &gt; **file extension includes these words** | *AttachmentExtensionMatchesWords* | This condition matches messages with attachments whose file name extension matches what you specify. |
| **Any attachment is greater than or equal to** &lt;br&gt;&lt;br&gt; **Any attachment** &gt; **size is greater than or equal to** | *AttachmentSizeOver* | This condition matches messages with attachments when those attachments are greater than or equal to the size you specify. &lt;br&gt;&lt;br&gt; This condition refers to the sizes of individual attachments, not the cumulative size. For example, you have a rule that rejects messages with any attachment larger than 10 MB. A message with a single 15-MB attachment is rejected, but a message with three 5-MB attachments is allowed. |
| **The message didn't complete scanning** &lt;br&gt;&lt;br&gt; **Any attachment** &gt; **didn't complete scanning** | *AttachmentProcessingLimitExceeded* | This condition matches messages when the mail flow rules agent doesn't inspect the message. |
| **Any attachment has executable content** &lt;br&gt;&lt;br&gt; **Any attachment** &gt; **has executable content** | *AttachmentHasExecutableContent* | This condition matches messages that contain executable files as attachments. The supported file types are listed here. |
| **Any attachment is password protected** &lt;br&gt;&lt;br&gt; **Any attachment** &gt; **is password protected** | *AttachmentIsPasswordProtected* | This condition matches messages with attachments that are protected by a password. Password detection works for Office documents, compressed files (.zip, .7z), and .pdf files. |
| **Any attachment has these properties, including any of these words** &lt;br&gt;&lt;br&gt; **Any attachment** &gt; **has these properties, including any of these words** | *AttachmentPropertyContainsWords* | This condition matches messages where the specified property of the attached Office document contains specified words. A property and its possible values are separated with a colon. Multiple values are separated with a comma. Multiple property-value pairs are also separated with a comma. |

Note

- The condition names in Exchange Online PowerShell are parameter names on the **New-TransportRule** and **Set-TransportRule** cmdlets. For more information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).
- For more information about property types for these conditions, see [Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions).
- For information on how to connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

### Supported executable file types for mail flow rule inspection

The mail flow rules use true type detection to inspect file properties rather than merely the file extensions. This approach helps to prevent malicious hackers from being able to bypass your rule by renaming a file extension. The following table lists the executable file types supported by these conditions. If a file that isn't listed here is found, the `AttachmentIsUnsupported` condition is triggered.

| Type of file | Native extension |
| --- | --- |
| 32-bit Windows executable file with a dynamic link library extension. | .dll |
| Self-extracting executable program file. | .exe |
| Uninstallation executable file. | .exe |
| Program shortcut file. | .exe |
| 32-bit Windows executable file. | .exe |
| Microsoft Visio XML drawing file. | .vxd |
| OS/2 operating system file. | .os2 |
| 16-bit Windows executable file. | .w16 |
| Disk-operating system file. | .dos |
| European Institute for Computer Antivirus Research standard antivirus test file. | .com |
| Windows program information file. | .pif |
| Windows executable program file. | .exe |

Important

**.rar** (self-extracting archive files created with the WinRAR archiver), **.jar** (Java archive files), and **.obj** (compiled source code, 3D object, or sequence files) files are **not** considered to be executable file types. To block these files, you can use either of the following methods:

- Use mail flow rules that look for files with these extensions as described earlier in this article.
- Configure an anti-malware policy that blocks these file types using the common attachments filter. For more information, see [Configure anti-malware policies](/en-us/defender-office-365/anti-malware-policies-configure).

## Data loss prevention policies and attachment mail flow rules

Note

This section doesn't apply to the Built-in security add-on for on-premises mailboxes.

To help you manage important business information in emails, you can include any of the attachment-related conditions along with the rules of a data loss prevention (DLP) policy.

DLP policies and attachment-related conditions can help you enforce your business needs by defining those needs as mail flow rule conditions, exceptions, and actions. When you include the sensitive information inspection in a DLP policy, any attachments to messages are scanned for that information only. However, attachment-related conditions such as size or file type aren't included until you add the conditions listed in this article. DLP isn't available with all versions of Exchange; for more information, see [Data loss prevention](../data-loss-prevention/data-loss-prevention).

## For more information

For information on broadly blocking email with attachments, regardless of malware status, see [Common attachment blocking scenarios for mail flow rules in Exchange Online](common-attachment-blocking-scenarios).