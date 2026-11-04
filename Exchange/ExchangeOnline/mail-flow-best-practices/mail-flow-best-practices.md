---
layout: Conceptual
title: Mail flow best practices for Exchange Online, Microsoft 365, and Office 365 (overview) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/mail-flow-best-practices
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
ms.author: serdars
ms.topic: best-practice
author: AshaIyengar21
ms.service: exchange-online
ms.assetid: 0e6cd9d5-ad3e-418a-8ea9-3bf33332c491
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
- NOCSH
description: Use Microsoft Exchange Online and Microsoft 365 or Office 365 to manage mail flow. Find out how, and get tips and best practices for setting up and managing your email.
audience: ITPro
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 48c969ec-e02c-70b0-59ba-a4a868a522ce
document_version_independent_id: b01cc2c1-bb5b-b443-ecfb-77a45ae7a693
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/mail-flow-best-practices.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/mail-flow-best-practices
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/mail-flow-best-practices.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 9f606eff-c11c-e19e-884b-695266884a57
---

# Mail flow best practices for Exchange Online, Microsoft 365, and Office 365 (overview) | Microsoft Learn

Use Microsoft Exchange Online and Microsoft 365 or Office 365 to manage mail flow. Find out how, and get tips and best practices for setting up and managing your email.

**This article is intended for IT Pros. Want something else?**

**Try [Set up Microsoft 365 for business](/en-us/microsoft-365/admin/setup/setup) or [Deploy Office 365 Enterprise for your organization](/en-us/office365/enterprise/setup-overview-for-enterprises)**.

Microsoft 365 and Office 365 give you flexibility in determining the best arrangement for how email is delivered to your organization's mailboxes. The path email takes from the internet to a mailbox and vice versa is called mail flow. Most organizations want Microsoft 365 or Office 365 to manage all their mailboxes and filtering, and some organizations need more complex mail flow setups to make sure that they comply with specific regulatory or business needs. If you're part of a small business or simply an organization that wants Microsoft 365 or Office 365 to manage all your mailboxes and mail flow, we recommend following the steps in [Set up Microsoft 365 for business](/en-us/microsoft-365/admin/setup/setup). That article provides a complete checklist for setting up Microsoft 365 or Office 365 services and programs, including how to set up your mail flow and email clients.

For information about how your cloud email is protected, see [Built-in security features for all cloud mailboxes](/en-us/defender-office-365/eop-about).

Tip

Are you new to Microsoft 365 or Office 365 mail flow? Check out the [External Domain Name System records for Microsoft 365 or Office 365](/en-us/office365/enterprise/external-domain-name-system-records) topic. We especially recommend reading the part about SPF records because customers often list the wrong values in their SPF record, which can cause mail flow problems.

Microsoft 365 and Office 365 mail flow covers the following scenarios:

| Mail flow setup | Your organization's scenario | Complexity |
| --- | --- | --- |
| [Manage all mailboxes and mail flow using Microsoft 365 or Office 365](manage-mailboxes-using-microsoft-365-or-office-365) | **[Scenario 1](manage-mailboxes-using-microsoft-365-or-office-365#hosted-mail-flow-scenarios)** I'm a new Microsoft 365 or Office 365 customer, and all my users' mailboxes are in Microsoft 365 or Office 365. I want to use all filtering solutions offered by Microsoft 365 and Office 365. **[Scenario 2](manage-mailboxes-using-microsoft-365-or-office-365#hosted-mail-flow-scenarios)** I'm a new Microsoft 365 or Office 365 customer. I have an existing email service but plan to move all the existing users' mailboxes to the cloud at once. I want to use all filtering solutions offered by Microsoft 365 and Office 365. | Simple |
| [Manage mail flow using a third-party cloud service with Microsoft 365 or Office 365](manage-mail-flow-using-third-party-cloud) | **[Scenario 1](manage-mail-flow-using-third-party-cloud#scenario-1---mx-record-points-to-third-party-spam-filtering)** I plan to have Microsoft 365 or Office 365 host all of my organization's mailboxes. My organization uses (or plans to use) a third-party (mail services) cloud solution for filtering spam and malware. All email sent from the internet must be filtered by this third-party cloud service. **[Scenario 2](manage-mail-flow-using-third-party-cloud#scenario-2---mx-record-points-to-third-party-solution-without-spam-filtering)** I plan to have Microsoft 365 or Office 365 host all my organization's mailboxes. My organization needs to send all email to a third-party service, such as archiving or auditing. However, the third-party service doesn't provide a spam filtering solution. | Complex |
| [Manage mail flow with mailboxes in multiple locations (Microsoft 365 or Office 365 and on-prem)](manage-mail-flow-for-multiple-locations)**Important**: In the near future, Microsoft 365 and Office 365 will reject email from unknown senders that are relayed from on-premises servers. This means that if the sender or recipient domain of a message doesn't belong to your organization, Microsoft 365 or Office 365 will reject the message unless you have created a connector to allow this behavior. This change will help prevent unauthorized parties from using your organization to send spam or malware through Microsoft 365 or Office 365.  This change potentially affects your mail flow if you use any scenario in this section. Each scenario has best practices to ensure that your mail flow continues uninterrupted. | **[Scenario 1](manage-mail-flow-for-multiple-locations#scenario-1-mx-record-points-to-microsoft-365-or-office-365-and-microsoft-365-or-office-365-filters-all-messages)** I'm migrating my mailboxes to Microsoft 365 or Office 365, and I want to keep some mailboxes on my organization's mail server (on-premises server). I want to use Microsoft 365 or Office 365 as my spam filtering solution and would like to send my messages from my on-premises server to the internet via Microsoft 365 or Office 365. Microsoft 365 or Office 365 sends and receives all messages. **[Scenario 2](manage-mail-flow-for-multiple-locations#scenario-2-mx-record-points-to-microsoft-365-or-office-365-and-mail-is-filtered-on-premises)** I'm migrating my mailboxes to Microsoft 365 or Office 365, and I want to keep some mailboxes on my organization's mail server (on-premises server). I want to use the filtering and compliance solutions that are already in my on-premises environment. And all messages coming from the internet to my cloud mailboxes or messages sent to the internet from my cloud mailboxes need to route through my on-premises servers. **[Scenario 3](manage-mail-flow-for-multiple-locations#scenario-3-mx-record-points-to-my-on-premises-servers)** I'm migrating my mailboxes to Microsoft 365 or Office 365, and I want to keep some mailboxes on my organization's mail server (on-premises server). I want to use the filtering and compliance solutions that are already in my on-premises email environment. All messages coming from the internet to my cloud mailboxes or messages sent to the internet from cloud mailboxes must route through my on-premises servers. And I need to point my domain's MX record to my on-premises server. **[Scenario 4](manage-mail-flow-for-multiple-locations#scenario-4-mx-record-points-to-my-on-premises-server-which-filters-and-provides-compliance-solutions-for-your-messages-your-on-premises-server-needs-to-relay-messages-to-the-internet-through-microsoft-365-or-office-365)** I'm migrating my mailboxes to Microsoft 365 or Office 365, and I want to keep some mailboxes on my organization's mail server (on-premises server). I want to use the filtering and compliance solutions that are already in my on-premises email environment. All messages sent from my on-premises servers must relay through Microsoft 365 or Office 365 to the internet. And I need to point my domain's MX record to my on-premises server. | Very complex |
| [Manage mail flow using a third-party cloud service with mailboxes on Microsoft 365 or Office 365 and on-prem](manage-mail-flow-on-office-365-and-on-prem) | **Scenario** I'm migrating my mailboxes to Microsoft 365 or Office 365, and I want to keep some mailboxes on my organization's mail server (on-premises server). I want to use a third-party cloud service to filter spam from the internet. My messages to the internet need to route through Microsoft 365 or Office 365 to protect my on-premises servers' IP addresses from being added to external block lists. | Most complex |
| Send emails from a multifunction printer/scanner/fax/application through Microsoft 365 or Office 365  For details about this scenario, see [How to set up a multifunction device or application to send email using Microsoft 365 or Office 365](how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365). | **Scenario** All my organization's mailboxes are hosted in Microsoft 365 or Office 365, but I have a multifunction printer, scanner, fax machine, or an application that needs to send email. | Complex |
| Using the built-in security features for all cloud mailboxes to protect on-premises mailboxes  For details about this scenario, see [Mail flow in cloud organizations](/en-us/defender-office-365/mail-flow-about) and [How connectors work with my on-premises email servers](use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow#how-connectors-work-with-my-on-premises-email-servers) | **Scenario** I have my own email servers (on-premises email servers), and I have licenses for the Built-in security add-on for on-premises mailboxes. | Simple |

For information about migrating your email to Microsoft Exchange Online, see [Ways to migrate multiple email accounts to Microsoft 365 or Office 365](../mailbox-migration/mailbox-migration).

## Introduction to the basics of Microsoft 365 and Office 365 mail flow

Microsoft 365 and Office 365 use domains, like contoso.com, to route email messages. When you set up email in Microsoft 365 or Office 365, you typically switch from the default domain that you got when you first signed up for Microsoft 365 or Office 365 (the domain ending with .onmicrosoft.com) to your organization's domain. Domain names, like contoso.com, are managed by using a worldwide system of domain registrars (for example, GoDaddy, HostGator, or Moniker) and databases called the Domain Name System (DNS). DNS provides a mapping between human-readable computer hostnames and the IP addresses used by networking equipment. If you're new to DNS, we recommend that you read [DNS basics](/en-us/microsoft-365/admin/get-help-with-domains/dns-basics). The following video provides you with a quick overview of some of the most important concepts about what DNS is and how it works.

### Understanding how DNS records control mail flow

In Microsoft 365 and Office 365 mail flow, there are several components of DNS that are particularly important for email authentication and delivery: MX records, SPF, DKIM, and DMARC.

**MX (mail exchanger) records** provide an easy way for mail servers to know where to send email. You can think of the MX record as a type of postal address. If you want Microsoft 365 or Office 365 to receive all email addressed to anyone@contoso.com, the MX record for contoso.com should point to Microsoft 365 or Office 365, and it will look like the following example:

```
Hostname: contoso-com.mail.protection.outlook.com
Priority: 0
TTL: 1 hour
```

**SPF (sender policy framework)** is a specially formatted TXT record in DNS. SPF validates that only the organization that owns a domain is actually sending email from that domain. SPF is a security measure that helps makes sure someone doesn't impersonate another organization. This impersonation is often called spoofing. As a domain owner, you can use SPF to publish a list of IP addresses or subnets that are authorized to send email on your organization's behalf. This can be helpful if you want to send email from multiple servers or services with different IP addresses.

Important

You can only have one SPF record per domain. Having multiple SPF records will invalidate all SPF records and cause mail flow problems.

Because most modern email servers look up a domain's SPF record before they accept any email from it, it's important to set up a valid SPF record in DNS when you first set up mail flow. For a quick introduction to SPF and to get it configured quickly, see [Set up SPF to identify valid email sources for your Microsoft 365 domain](/en-us/defender-office-365/email-authentication-spf-configure). For a more in-depth understanding of how Microsoft 365 and Office 365 use SPF, or for troubleshooting or non-standard deployments such as hybrid deployments, start with [Set up SPF to identify valid email sources for your Microsoft 365 domain](/en-us/defender-office-365/email-authentication-spf-configure).

**DomainKeys Identified Mail (DKIM).** lets you attach a digital signature to email messages in the message header of emails you send. Email systems that receive email from your domain use this digital signature to determine if incoming email that they receive is legitimate. For information about DKIM and Microsoft 365 or Office 365, see [Use DKIM to validate outbound email sent from your domain in Microsoft 365 or Office 365](/en-us/defender-office-365/email-authentication-dkim-configure).

**Domain-based Message Authentication, Reporting, and Conformance (DMARC).** helps receiving mail systems determine what to do with messages that fail SPF or DKIM checks and provides another level of trust for your email partners. For information on setting up DMARC, see [Use DMARC to validate email in Microsoft 365 or Office 365](/en-us/defender-office-365/email-authentication-dmarc-configure).

Use SPF, DKIM, and DMARC together for the best experience.

### How MX records affect spam filtering

For the best mail flow experience (especially for spam filtering) we recommend pointing the MX record for your organization's domain to Microsoft 365 or Office 365. Spam scanning is the initial connection point to the Microsoft 365 or Office 365 service. Who is sending the message, the IP address of the server that originally sent the message, and the behavior of the connecting mail server, all help determine whether a message is legitimate or spam. If your domain's MX record doesn't point to Microsoft 365 or Office 365, the spam filters won't be as effective. If your MX record doesn't point to Microsoft 365 or Office 365, there will be some valid messages that the service misclassifies as spam and some spam messages that the service misclassifies as legitimate email.

With that said, there are legitimate business scenarios that require your domain's MX record to point to somewhere other than Microsoft 365 or Office 365. For example, email destined for your organization might need to initially arrive at another destination (such as a third-party archiving solution), then route through Microsoft 365 or Office 365, and then be delivered to mailboxes on your organization's mail server. This setup might provide the best solution to meet your business requirements.

Whatever your needs, this guide will help you understand how your MX records, SPF, and, potentially, connectors need to be set up.

## For more information

The following are additional topics related to mail flow in Exchange Online:

[Test mail flow by validating your Microsoft 365 or Office 365 connectors](test-mail-flow)

[Troubleshoot Microsoft 365 or Office 365 mail flow](troubleshoot-mail-flow)

[Use Directory Based Edge Blocking to reject messages sent to invalid recipients](use-directory-based-edge-blocking)

[Manage accepted domains in Exchange Online](manage-accepted-domains/manage-accepted-domains)

[Remote domains in Exchange Online](remote-domains/remote-domains)

[Message format and transmission in Exchange Online](message-format-and-transmission)

[Configure the external postmaster address in Exchange Online](configure-external-postmaster-address)

[How to set up a multifunction device or application to send email using Microsoft 365 or Office 365](how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365)