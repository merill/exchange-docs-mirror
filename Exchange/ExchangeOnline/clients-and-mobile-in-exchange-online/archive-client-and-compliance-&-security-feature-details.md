---
layout: Conceptual
title: Archive, Client, and Compliance & Security feature details | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/archive-client-and-compliance-&-security-feature-details
Manager: gailw
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: office365servicedesc
author: pamelaar
audience: ITPro
ms.topic: reference
ms.service: o365-administration
ms.localizationpriority: medium
ms.custom:
- Adm_ServiceDesc
- Adm_ServiceDesc_top
ms.assetid: 38abfbd2-5aaa-444a-a431-5e71c566f3e4
description: Learn about the archive features available in Microsoft Exchange Online Archiving.
ms.date: 2022-10-27T00:00:00.0000000Z
locale: en-us
document_id: 9e59fb3d-02c2-04f0-0df6-b5c951c636a0
document_version_independent_id: 9b1b37ac-475e-0822-a635-1da99a5a3dc3
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/archive-client-and-compliance-&-security-feature-details.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/archive-client-and-compliance-&-security-feature-details
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/archive-client-and-compliance-&-security-feature-details.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: a29d8daa-c729-6c3c-c6fe-c58df31c0ba6
---

# [Archive features](#tab/Archive-features)
The following sections describe the archive features of Microsoft Exchange Online Archiving.

## Archive mailbox

Exchange Online Archiving offers users advanced archiving capabilities with the archive mailbox feature. An archive mailbox is a specialized mailbox that appears alongside the users' primary mailbox folders in Outlook or Outlook on the web. Users can access the archive in the same way that they access their primary mailboxes. In addition, they can search both their archives and primary mailboxes.

Administrators can use the Exchange admin center (EAC) or remote Windows PowerShell to enable the archive feature for specific users. For more information, see [Enable or disable archive mailboxes in Exchange Online](/en-us/office365/securitycompliance/enable-archive-mailboxes).

Important

Using journaling, transport rules, or auto-forwarding rules to copy messages to Exchange Online Archiving for the purposes of archiving is not permitted.

A user's archive mailbox is intended for just that user. Microsoft reserves the right to deny additional archive storage space in instances where a user's archive mailbox is used to store archive data for other users or in other cases of inappropriate use.

### Move messages to Exchange Online Archiving

Users can drag and drop messages from .pst files into the archive, for easy online access. Users can also move email items from the primary mailbox to the archive mailbox automatically, using Archive Polices, to reduce the size and improve the performance of the primary mailbox.

### Import data to the archive

Users can import data to the archive in the following ways:

- Import data from a .pst file using Outlook's Import and Export wizard.
- Drag email messages from .pst files into the archive.
- Drag email messages from the primary mailbox into the archive.
- Let archive policies automatically move email messages from the primary mailbox, based on the age of the messages. For more information, see [Retention Tags and Retention Policies](/en-us/Exchange/policy-and-compliance/mrm/retention-tags-and-retention-policies).

Note

Administrators can also use Office 365 Import service to import .pst files to users' cloud-based archive mailboxes. For more information, see [Use network upload to import PST files to Office 365](/en-us/office365/securitycompliance/use-network-upload-to-import-pst-files).

## Deleted item recovery

Users can restore items they have deleted from any email folder in their archive. When an item is deleted, it is kept in the archive's Deleted Items folder. It remains there until it is manually removed by the user, or automatically removed by retention policies.

After an item has been removed from the archive's Deleted Items folder, the item is kept in the archive's Recoverable Items folder for an additional 14 days before being permanently removed. Users can recover these items using the **Recover Deleted Items** feature in Microsoft Outlook or Outlook on the web.

If a user has manually purged an item from the Recoverable Items folder, an administrator can recover the item within the same 14 day window, through a feature called Single Item Recovery. This feature allows administrators to conduct a multi-mailbox search to find purged items and then use the `Search-Mailbox` Windows PowerShell cmdlet to move the items from the discovery mailbox to users' mailboxes. For more information, see [Enable or disable single item recovery for a mailbox](/en-us/office365/securitycompliance/use-network-upload-to-import-pst-files).

Note

The Single Item Recovery period is 14 days by default, but it can be customized in some circumstances.

If an administrator has placed a user's mailbox on In-Place Hold or Litigation Hold, purged items are retained indefinitely and the 14-day window does not apply.

## Deleted mailbox recovery

When administrators delete users from the on-premises Exchange Server, the users' archives are also deleted. If the deleted archive mailboxes need to be recovered, the Microsoft support team can perform this recovery. A recovered archive will contain all of the mail stored in it at the time it was deleted.

Important

Administrators have 30 days from the time a user's mailbox is deleted to request an archive mailbox recovery. After 30 days, the archive mailbox is not recoverable.

## Mailbox service redundancy

Archive mailboxes in Exchange Online Archiving are replicated to multiple database copies, in geographically dispersed Microsoft data centers, to provide data restoration capability in the event of a messaging infrastructure failure. For large-scale failures, business continuity management is initiated.

## Feature availability

To view feature availability across plans, standalone options, and on-premises solutions, see [Exchange Online Archiving service description](/en-us/office365/servicedescriptions/exchange-online-archiving-service-description/exchange-online-archiving-service-description).

# [Client features](#tab/Client-features)
Microsoft Exchange Online Archiving lets users connect to their archive mailboxes from a variety of devices and platforms. All network connectivity to the user's archive occurs over the internet, and virtual private network (VPN) connections are not required. Organizations can publish an on-premises Client Access server to allow users to access their primary mailbox using Outlook Anywhere, without requiring a VPN connection. If VPN access is required to access the user's primary mailbox located on an on-premises server, this requirement does not change.

Important

Microsoft reserves the right to block or throttle connections from any client software that negatively impacts the health of the Exchange Online Archiving service.

## Microsoft Outlook

Microsoft Outlook is a rich email program that includes support for calendaring, contacts, and tasks. Exchange Online Archiving supports Outlook 2013, Outlook 2010, and Outlook 2007. Key features include:

- **Outlook Anywhere** - Outlook Anywhere lets Outlook users connect to Exchange Server and Exchange Online Archiving over the internet with no need for a VPN connection. Communication between Outlook and Exchange Online Archiving occurs via an SSL-secured tunnel, using the RPC-over-HTTP Windows networking component.
- **Autodiscover** - The Exchange Autodiscover service automatically configures Outlook to work with Exchange Online Archiving. Autodiscover lets Outlook users receive their required profile settings directly from Exchange the first time (and at fixed intervals thereafter) that they sign in with their email address and password.

Outlook 2010 and later and Outlook on the web provide users with the full features of the archive, as well as related features like retention and archive policies.

Outlook 2007 provides basic support for the archive, but not all archiving and compliance features are available in Outlook 2007. For example, with Outlook 2007, users cannot apply retention or archive policies to items in their mailboxes. They must rely on administrator-provisioned policies instead. Outlook 2007 users require the Office 2007 Cumulative Update for February 2011 to access the archive.

Note

Outlook is not provided with Exchange Online Archiving. Microsoft 365 Apps for enterprise (which includes Microsoft Outlook) is included in some plans and can be purchased as a separate subscription. For more information, see [Microsoft 365 plan options](/en-us/office365/servicedescriptions/office-365-platform-service-description/office-365-plan-options). For more information about Microsoft 365 Apps for enterprise, see the [Office applications service description](/en-us/office365/servicedescriptions/office-applications-service-description/office-applications-service-description).

### Clients supported by Exchange Online Archiving

The table below lists the clients supported by Exchange Online Archiving:

| Client | EOA support |
| --- | --- |
| Outlook 2013 and later | Supports the latest features in Exchange Online Archiving.^1^ |
| Outlook 2010 | Supports the latest features in Exchange Online Archiving only until Oct. 13, 2020. |
| Outlook 2007 | Not supported |
| Outlook 2003 | Not supported |
| Outlook for Mac 2011 | Not supported |
| Outlook for Mac | Supported for use with Exchange Online Archiving.^3^ |
| Outlook for iOS | Supported for use with Exchange Online Archiving. |
| Outlook for Android | Supported for use with Exchange Online Archiving. |
| Microsoft Office Entourage 2008 Web Services Edition | Not supported |
| IMAP and POP | Not supported |
| Exchange ActiveSync (mobile devices) | Not supported |

^1^ Outlook included with Microsoft Office Standard is not supported. To learn more, see [License requirements for Personal Archive and retention policies](https://support.office.com/article/Outlook-license-requirements-for-Exchange-features-46B6B7C5-C3CA-43E5-8424-1E2807917C99). ^2^ Requires update to enable archiving support. Outlook 2007 users cannot view or apply retention or archive policies to items in their archive mailboxes; they must rely on administrator-provisioned policies. Additionally, Outlook 2007 users cannot search the on-premises mailbox and the archive at the same time. ^3^ You can't use Outlook 2016 for Mac or Outlook for Mac to move or copy folders, calendar items, contacts, tasks, or notes to your archive, or view them in the archive mailbox, if the items were previously moved there by using any other version of Outlook (such as Outlook 2016 for Windows). For more information, see [Use your online archive with Outlook 2016 for Mac](https://support.office.com/article/Use-your-online-archive-with-Outlook-2016-for-Mac-45b8439c-2982-4b6b-9097-eed71dbfe238).

## Outlook on the web

Outlook on the web is a web-based version of the Outlook email program that is used with Exchange Online. Wherever users are connected to the internet—at home, at the office, or on the road—they can access their email through Outlook on the web.

Users can access their archive by signing in to Outlook on the web on-premises (using the same URL). The archive appears alongside their primary mailbox in Outlook on the web. There is no explicit way to access the archive directly from Outlook on the web.

## Feature availability

To view feature availability across plans, standalone options, and on-premises solutions, see [Exchange Online Archiving service description](/en-us/office365/servicedescriptions/exchange-online-archiving-service-description/exchange-online-archiving-service-description).

# [Compliance and security features](#tab/Compliance-and-security-features)
## Compliance features in Exchange Online Archiving

This article describes the compliance features of Microsoft Exchange Online Archiving.

### Retention policies

Exchange Online Archiving offers retention policies to help organizations reduce the liabilities associated with email and other communications. With these policies, administrators can apply retention settings to specific folders in users' inboxes. Administrators can also give users a menu of retention policies and let them apply the policies to specific items, conversations, or folders using Outlook 2010 or later or Outlook on the web. In Exchange Online Archiving, administrators manage retention policies from the on-premises infrastructure.

Exchange Online Archiving offers two types of policies: archive and delete. Both types can be applied to the same item or folder. For example, a user can tag an email message so that it is automatically moved to the personal archive in a specified number of days and deleted after another span of days.

With Outlook 2010 and later and Outlook on the web, users can apply retention policies to folders, conversations, or individual messages and can also view the applied retention policies and expected deletion dates on messages. Users of other email clients can have email deleted or archived based on server-side retention policies provisioned by the administrator, but they do not have the same level of visibility and control.

The retention policy capabilities offered in Exchange Online Archiving are the same as those offered in Exchange Server 2010 Service Pack 2 (SP2) and later. Administrators can manage retention policies from on-premises Exchange Server 2010 and later environments. Managed Folders, an older approach to messaging records management that was introduced in Exchange 2007, are not available in and not compatible with Exchange Online Archiving. For more information, see [Retention Tags and Retention Policies](/en-us/Exchange/policy-and-compliance/mrm/retention-tags-and-retention-policies).

### In-Place Hold and Litigation Hold

When a reasonable expectation of litigation exists, organizations are required to preserve electronically stored information (ESI), including email that's relevant to the case. This expectation can occur before the specifics of the case are known, and preservation is often broad. Organizations may preserve all email related to a specific topic, or all email for certain individuals.

In Exchange Online, you can use In-Place Hold or Litigation Hold to accomplish the following goals:

- Enable users to be placed on hold and preserve mailbox items immutably
- Preserve mailbox items deleted by users or automatic deletion processes such as MRM
- Protect mailbox items from tampering, changes by a user, or automatic processes by saving a copy of the original item
- Preserve items indefinitely or for a specific duration
- Keep holds transparent from the user by not having to suspend MRM
- Use In-Place eDiscovery to search mailbox items, including items placed on hold

Additionally, you can use In-Place Hold to:

- Search and hold items matching specified criteria
- Place a user on multiple In-Place Holds for different cases or investigations

Note

When you put a mailbox on In-Place Hold or Litigation Hold, the hold is placed on both the primary and the archive mailbox.

For more information, see [In-Place Hold and Litigation Hold](/en-us/exchange/security-and-compliance/in-place-and-litigation-holds).

Note

The default quota for the Recoverable Items Folder is 100 GB for Exchange Online Archiving users.

### In-Place eDiscovery

Exchange Online Archiving supports In-Place eDiscovery for searching the contents of mailboxes in an organization. Using the Exchange admin center or remote Windows PowerShell from an on-premises Exchange 2013 server, administrators or authorized Discovery managers can search a variety of mailbox items - including email messages, attachments, calendar appointments, tasks, and contacts. In-Place eDiscovery can search simultaneously across primary mailboxes and archives. Rich filtering capabilities include sender, receiver, message types, sent date, received date, carbon copy, and blind carbon copy, along with Keyword Query Language (KQL) syntax. For more information, see [In-Place eDiscovery](/en-us/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery).

The Exchange admin center and remote Windows PowerShell can be used to search up to 5,000 mailboxes at a time in an In-Place eDiscovery search. For details about using remote Windows PowerShell to run In-Place eDiscovery searches, see [New-MailboxSearch](/en-us/powershell/module/exchangepowershell/new-mailboxsearch).

Note

In remote Windows PowerShell, the `Search-Mailbox` cmdlet can be used to search more than 5,000 mailboxes. For details about searching large numbers of mailboxes using remote Windows PowerShell, see [Search-Mailbox](/en-us/powershell/module/exchangepowershell/search-mailbox).

Results of an In-Place eDiscovery search can be previewed in the Exchange admin center, exported to a .pst file, or copied to a special type of mailbox, called a discovery mailbox. Administrators or compliance officers can connect to the discovery mailbox to review messages. For details, see [Create an In-Place eDiscovery Search](/en-us/purview/ediscovery-content-search).

Note

When copying search results for an In-Place eDiscovery search performed across on-premises and cloud-based mailboxes or archives, you must select an on-premises discovery mailbox. Messages from the on-premises primary mailbox and the cloud-based archive are copied to the on-premises discovery mailbox.

Administrators can also search for and delete inappropriate email messages sent to multiple mailboxes across their organizations. For example, if confidential salary information was accidentally sent to all employees, an administrator can delete the email from the users' mailboxes. This type of search is not available in the Exchange admin center. It must be performed using Remote PowerShell. For details on how to delete messages from users' mailboxes, see [Search and Delete Messages](/en-us/Exchange/policy-and-compliance/ediscovery/delete-messages).

## Security features in Exchange Online Archiving

The following sections describe the security features of Microsoft Exchange Online Archiving.

### Encryption between on-premises servers and Exchange Online Archiving

TLS is used to encrypt the connection between email servers to help prevent spoofing and provide confidentiality for messages in transit. TLS is also used for securing on-premises mail server traffic to Microsoft datacenters for Exchange Online Archiving.

### Encrypting between clients and Exchange Online Archiving

Client connections to Exchange Online Archiving use the following encryption methods to enhance security:

- SSL is used for securing Outlook, Outlook on the web, and Exchange Web Services traffic, using TCP port 443.
- Client connections to on-premises servers do not change with the introduction of Exchange Online Archiving.

### Encryption: S/MIME and PGP

Exchange Online Archiving will store Secure/Multipurpose Internet Mail Extensions (S/MIME) messages. However, Exchange Online Archiving does not host S/MIME functions or host the public keys, nor does it provide key repository, key management, or key directory services because all of these services attach to the on-premises Exchange infrastructure.

Similarly, Exchange Online Archiving will store messages that are encrypted using client-side, third-party encryption solutions such as Pretty Good Privacy (PGP).

### Information Rights Management

Exchange Online Archiving does not provide hosted Information Rights Management (IRM) services, but administrators can use on-premises Active Directory Rights Management Services (AD RMS). If an AD RMS server is deployed, Outlook can communicate directly with that server, enabling users to compose and read IRM-protected messages. If interoperability between the AD RMS server and the on-premises Exchange environment is configured, users will be able to compose and read IRM-protected messages.

#### Support for IRM in Outlook on the web

Users can read and create IRM-protected messages natively in Outlook on the web, just as they can in Outlook. IRM-protected messages in Outlook on the web can be accessed through Internet Explorer, Firefox, Safari, and Chrome (with no plug-in required). The messages include full-text search, conversation view, and the preview pane. Interoperability between the Active Directory Rights Management Services server and the on-premises Exchange environment must be configured to enable this.

#### IRM search

IRM-protected messages are indexed and searchable, including headers, subject, body, and attachments. Users can search IRM-protected items in Outlook and Outlook on the web, and administrators can search IRM-protected items by using In-Place eDiscovery or the **Search-Mailbox** cmdlet.

### Auditing

Exchange Online Archiving provides two types of built-in auditing capabilities:

- **Administrator audit logging** - Administrator audit logging allows customers to track changes made by their administrators in the Exchange Online Archiving environment, including changes to RBAC roles or Exchange policies and settings.
- **Mailbox audit logging** - Mailbox audit logging allows customers to track access to mailboxes by users other than the mailbox owner.

Several predefined audit reports are available in the Exchange admin center, including Administrator Role Changes, Litigation Hold, and Non-Owner Mailbox Access. Administrators can filter reports by date and role, and they can export all audit events for specified mailboxes in XML format for long-term retention or custom reporting.

Administrator audit logging is on by default, and mailbox audit logging is off by default. Administrators can use remote Windows PowerShell to enable mailbox audit logging for some or all mailboxes in their organization. For more information, see [Auditing Reports](/en-us/exchange/security-and-compliance/exchange-auditing-reports/exchange-auditing-reports).

## Feature availability

To view feature availability across plans, standalone options, and on-premise solutions, see [Exchange Online Archiving service description](/en-us/office365/servicedescriptions/exchange-online-archiving-service-description/exchange-online-archiving-service-description).

---