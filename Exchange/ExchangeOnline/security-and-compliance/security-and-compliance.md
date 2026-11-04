---
layout: Conceptual
title: Security and compliance for Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/security-and-compliance
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
description: This article outlines an overview of the security and compliance features in Exchange Online.
ms.topic: concept-article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 510524c6-6d3e-416f-9e27-fa25446b099a
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
- essentials-security
- essentials-compliance
audience: ITPro
ms.service: exchange-online
ms.date: 2024-04-29T00:00:00.0000000Z
locale: en-us
document_id: 9ad9b8bf-d3d8-fe08-9c6f-04cd7643ac3e
document_version_independent_id: 516f4807-102e-aa11-9669-c379305045d1
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/security-and-compliance.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/security-and-compliance
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/security-and-compliance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 37c69775-f60a-25c0-e975-fa938c29e7eb
---

# Security and compliance for Exchange Online | Microsoft Learn

Email is a reliable and ubiquitous communication medium for information workers in organizations of all sizes. Messaging stores and mailboxes have become repositories of valuable data. It's important for organizations to formulate messaging policies that dictate the fair use of their messaging systems, provide user guidelines for how to act on the policies, and where required, provide details about the types of communication that may not be allowed.

Organizations must also create policies to manage email lifecycle, retain messages for the length of time based on business, legal, and regulatory requirements, preserve email records for litigation and investigation purposes, and be prepared to search and provide the required email records to fulfill eDiscovery requests.

Leakage of sensitive information such as intellectual property, trade secrets, business plans, and personally identifiable information (PII) collected or handled by your organization must also be protected.

## Security and compliance in Exchange Online

The following table provides an overview of the security and compliance features in Exchange Online and includes links to topics that will help you learn about and manage these features.

| Feature | Description |
| --- | --- |
| [Archive mailboxes in Exchange Online](/en-us/purview/enable-archive-mailboxes) | Archive mailboxes (called In-Place Archiving) let people in your Microsoft 365 or Office 365 organization take control of messaging data by providing additional email storage. People can use Outlook or Outlook on the web (formerly known as Outlook Web App) to view messages in their archive mailbox and move or copy messages between their primary and archive mailboxes. |
| [Litigation Hold](/en-us/purview/ediscovery-create-holds) | Litigation Hold allows you to preserve or archive mailbox content for compliance and eDiscovery. |
| [Inactive mailboxes in Exchange Online](/en-us/purview/inactive-mailboxes-in-office-365) | You can preserve the contents of deleted mailboxes indefinitely by using inactive mailboxes. You can make an inactive mailbox by placing an In-Place Hold or a Litigation Hold on the mailbox, and then deleting the corresponding user account. In addition to preserving mailbox contents, administrators or compliance officers can use Content Search in the Microsoft Purview portal to search the contents of an inactive mailbox. |
| [Data loss prevention](/en-us/purview/dlp-learn-about-dlp) | Data loss prevention (DLP) helps you identify and monitor sensitive information, such as private identification numbers, credit card numbers, or standard forms used in your organization. You can set up DLP policies to notify users that they are sending sensitive information or block the transmission of sensitive information. |
| [Auditing reports](/en-us/purview/audit-solutions-overview) | You can use auditing solutions in Microsoft Purview to track changes made to your Exchange Online configuration by Microsoft and by your organization's administrators, and to audit mailbox access by persons other than the mailbox owner. Audited actions are recorded and available to view in an online report or export to a file. |
| [Messaging records management](messaging-records-management/messaging-records-management) (MRM) | Messaging records management (MRM) helps your organization manage email lifecycle to meet business and regulatory requirements and reduce the legal risks associated with email. In Exchange Online, you can use In-Place Hold or Litigation Hold to preserve email and [Retention tags and retention policies](messaging-records-management/retention-tags-and-policies) to archive and delete email. |
| [Information Rights Management in Exchange Online](/en-us/purview/information-rights-management-in-exchange-online) | Information Rights Management (IRM) helps you and your users control who can access, forward, print, or copy sensitive data within an email. IRM can use your on-premises Active Directory Rights Management Services (AD RMS) server. |
| [Message Encryption FAQ](/en-us/purview/ome-faq) | Message Encryption allows you to send encrypted messages to people inside or outside your organization, regardless of the destination email service, whether it's Outlook.com, Yahoo, Gmail, or another service. Designated recipients can send encrypted replies. Message Encryption combines email encryption and rights management capabilities. Rights management capabilities are powered by Azure Information Protection. |
| [S/MIME for Message Signing and Encryption](smime-exo/smime-exo) | Secure/Multipurpose Internet Mail Extensions (S/MIME) allows email users to help protect sensitive information by sending signed and encrypted email within their organization. As an administrator, you can enable S/MIME-based security for your organization if you have mailboxes in either Exchange Server or Exchange Online. |
| [Journaling in Exchange Online](journaling/journaling) | Journaling can help you meet legal, regulatory, and organizational compliance requirements by recording inbound and outbound email communications. In Exchange Online, you can create journal rules to deliver journal reports to your on-premises mailbox or archiving system, or to an external archiving service. |
| [Mail flow rules (transport rules) in Exchange Online](mail-flow-rules/mail-flow-rules) | You can use mail flow rules (also known as transport rules) to inspect messages sent or received by your users and take actions such as blocking or bouncing a message, holding it for review by a manager or an administrator or delivering a copy to another recipient if the message matches specified conditions. |