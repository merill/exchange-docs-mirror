---
layout: Conceptual
title: Best practices for configuring the Built-in security add-on for on-premises mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/standalone-eop/best-practices-for-configuring-eop
Manager: deniseb
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
audience: ITPro
ms.topic: best-practice
ms.localizationpriority: medium
ms.assetid: faf1efd1-3b0c-411a-804d-17f37292eac0
description: Admins in on-premises organizations that use the Built-in security add-on for on-premises mailboxes can follow these best-practice configuration recommendations.
ms.service: exchange-online
ms.date: 2024-05-16T00:00:00.0000000Z
locale: en-us
document_id: ea3eadd3-87eb-c456-9f3d-94b04afdbf0a
document_version_independent_id: 574ef583-477b-7524-d4cc-c0d54b361ecb
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/standalone-eop/best-practices-for-configuring-eop.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standalone-eop/best-practices-for-configuring-eop
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/standalone-eop/best-practices-for-configuring-eop.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 434ae4bc-49d8-ef46-ddc5-b7288c48d0c2
---

# Best practices for configuring the Built-in security add-on for on-premises mailboxes | Microsoft Learn

Follow the best-practice recommendations in this article for configuring the Built-in security add-on for on-premises mailboxes. These recommendations set you up for success and avoid common configuration errors. This article assumes you already completed the setup process for the Built-in security add-on for on-premises mailboxes. If your setup isn't finished, see [Set up the Built-in security add-on for on-premises mailboxes](set-up-your-eop-service).

## Use a test domain

We recommend that you use a test domain, subdomain, or low volume domain for trying out service features before implementing them on your higher-volume, production domains.

## Synchronize recipients

If your organization has existing user accounts in an on-premises Active Directory environment, you can synchronize those accounts to Microsoft Entra ID in the cloud. Using directory synchronization is recommended. To learn more about the benefits of using directory synchronization, and the steps for setting it up, see [Manage mail users in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-mail-users).

## Recommended settings

We empower admins to customize their security settings to satisfy the needs of their organization. Although, as a general rule, there are two security levels we recommend: Standard and Strict. These settings are listed in the [Recommended email and collaboration threat policy settings for cloud organizations](/en-us/defender-office-365/recommended-settings-for-eop-and-office365).

Although the following article is focused on Microsoft Defender for Office 365, [Get started with Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-deployment-guide) contains actions that also apply to the Built-in security add-on for on-premises mailboxes:

- [Step 1: Configure email authentication for your Microsoft 365 domains](/en-us/defender-office-365/mdo-deployment-guide#step-1-configure-email-authentication-for-your-microsoft-365-domains)
- [Step 2: Configure protection policies](/en-us/defender-office-365/mdo-deployment-guide#step-2-configure-protection-policies)
- [Step 3: Assign permissions to admins](/en-us/defender-office-365/mdo-deployment-guide#step-3-assign-permissions-to-admins)

### Other settings

These settings cover a range of features that are outside of security policies.

| Security feature name | Standard | Strict | Comment |
| --- | --- | --- | --- |
| Deploy the [Report Message add-in](/en-us/defender-office-365/submissions-users-report-message-add-in-configure) or the [Report Phishing add-in](/en-us/defender-office-365/submissions-users-report-message-add-in-configure) to improve end-user reporting of suspicious email. | Yes | Yes |  |
| Schedule Malware and Spam Reports. | Yes | Yes |  |
| Disable or monitor [automatic email forwarding to external domains](/en-us/defender-office-365/outbound-spam-policies-external-email-forwarding). | Yes | Yes |  |
| Verify that [audit logging is enabled](/en-us/purview/audit-log-enable-disable). | Yes | Yes |  |
| [IMAP connectivity to mailbox](/en-us/Exchange/clients-and-mobile-in-exchange-online/pop3-and-imap4/enable-or-disable-pop3-or-imap4-access) | Disabled | Disabled |  |
| [POP connectivity to mailbox](/en-us/Exchange/clients-and-mobile-in-exchange-online/pop3-and-imap4/enable-or-disable-pop3-or-imap4-access) | Disabled | Disabled |  |
| Authenticated SMTP submission | Disabled | Disabled | Authenticated client SMTP submission (also known as client SMTP submission or SMTP AUTH) is required for POP3 and IMAP4 clients and applications and devices that generate and send email.  For instructions to enable and disable SMTP AUTH globally or selectively, see [Enable or disable authenticated client SMTP submission in Exchange Online](/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission). |
| EWS connectivity to mailbox | Disabled | Disabled | Outlook uses Exchange Web Services for free/busy, out-of-office settings, and calendar sharing. If you can't disable EWS globally, you have the following options: <br>- Use [Authentication policies](/en-us/exchange/clients-and-mobile-in-exchange-online/disable-basic-authentication-in-exchange-online) to prevent EWS from using Basic authentication if your clients support modern authentication (modern auth).<br>- Use [Client Access Rules](/en-us/exchange/clients-and-mobile-in-exchange-online/client-access-rules/client-access-rules) to limit EWS to specific users or source IP addresses.<br>- Control EWS access to specific applications globally or per user. For instructions, see [Control access to EWS in Exchange](/en-us/exchange/client-developer/exchange-web-services/how-to-control-access-to-ews-in-exchange).<br><br> The [Report message add-in](/en-us/defender-office-365/submissions-users-report-message-add-in-configure) and the [Report phishing add-in](/en-us/defender-office-365/submissions-users-report-message-add-in-configure) uses REST by default in supported environments, but will fall back to EWS if REST isn't available. The supported environments that use REST are:<br>- Exchange Online<br>- Exchange 2019 or Exchange 2016<br>- Current Outlook for Windows from a Microsoft 365 subscription or one-time purchase Outlook 2019.<br>- Current Outlook for Mac from a Microsoft 365 subscription or one-time purchase Outlook for Mac 2016 or later.<br>- Outlook for iOS and Android<br>- Outlook on the web |
| [PowerShell connectivity](/en-us/powershell/exchange/disable-access-to-exchange-online-powershell) | Disabled | Disabled | Available for mailbox users or mail users (user objects returned by the [Get-User](/en-us/powershell/module/exchangepowershell/get-user) cmdlet). |
| Use [spoof intelligence](/en-us/defender-office-365/anti-spoofing-spoof-intelligence) to add senders to your allow list | Yes | Yes |  |
| [Directory-Based Edge Blocking (DBEB)](/en-us/exchange/mail-flow-best-practices/use-directory-based-edge-blocking) | Enabled | Enabled | Domain Type = Authoritative |
| [Set up multifactor authentication for all admin accounts](/en-us/microsoft-365/admin/security-and-compliance/set-up-multi-factor-authentication) | Enabled | Enabled |  |

## Troubleshooting

Troubleshoot general issues and trends by using the reports in the admin centers. For more information, see [View email security reports in the Microsoft Defender portal](/en-us/defender-office-365/reports-email-security).

Find single point specific data about a message by using the message trace tool. For more information, see [Message trace in Exchange Online](/en-us/exchange/monitoring/trace-an-email-message/message-trace-modern-eac).

## Report false positives and false negatives to Microsoft

To help improve spam filtering in the service for everyone, you should report false positives (good email marked as bad) and false negatives (bad email allowed) to Microsoft for analysis. For more information, see [Report messages and files to Microsoft](/en-us/defender-office-365/submissions-report-messages-files-to-microsoft).

## Create mail flow rules

Create mail flow rules (also known as transport rules) or custom filters to meet your business needs.

When you deploy a new rule to production, select one of the test modes first to see the effect of the rule. Once you're satisfied that the rule is working in the manner intended, change the rule mode to **Enforce**.

When you deploy new rules, consider adding the **Generate Incident Report** action to monitor the rule in action.

In hybrid environments where your organization includes both on-premises Exchange and Exchange Online, consider the conditions that you use in mail flow rules. If you want the rules to apply to the entire organization, be sure to use conditions that are available in both on-premises Exchange and in Exchange Online. While most conditions are available in both environments, there are a few that are only available in one environment or the other. Learn more at [Mail flow rules (transport rules) in Exchange Online](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules).