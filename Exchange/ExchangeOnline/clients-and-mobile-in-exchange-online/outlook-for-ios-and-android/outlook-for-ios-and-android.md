---
layout: Conceptual
title: Outlook for iOS and Android in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: 'Summary: This article contains architectural and security information for administrators about Outlook for iOS and Android.'
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: b5cf21f4-57d2-4bfc-abc6-1f0689826af8
ms.collection:
- exchange-online
- M365-email-calendar
ms.reviewer: smithre4
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: ca9af29f-c472-ebfd-e166-66a7d2b8bf0c
document_version_independent_id: 958cc7b8-3330-52a0-26fd-5717cba1df2f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 0f6a734b-764f-13c2-a9f0-d6063b5d66b5
---

# Outlook for iOS and Android in Exchange Online | Microsoft Learn

The Outlook app for iOS and Android is designed to bring together email, calendar, contacts, and other files, enabling users in your organization to do more from their mobile devices. This article provides an overview of the architecture, so that administrators can deploy and maintain Outlook for iOS and Android in their organizations.

Note

The [Outlook for iOS and Android Help Center](https://support.microsoft.com/office/cd84214e-a5ac-4e95-9ea3-e07f78d0cde6) is available for users, including help for using the app on specific devices and troubleshooting information.

## Outlook for iOS and Android architecture

The Outlook for iOS and Android app is fully powered by the Microsoft Cloud. All Office 365 Enterprise, Government, Business, and Education accounts are supported natively, which means there's no mailbox data cached outside of Microsoft 365 or Office 365. Data simply stays in its current Exchange Online mailbox, and it's secured with TLS version 1.2 over HTTPS connections end-to-end, between Microsoft 365 or Office 365 and the app. Outlook for iOS and Android is fully delivered through Microsoft services that provide a strong commitment to security, privacy, and compliance.

The Microsoft 365- or Office 365-based architecture provides the following benefits:

1. **Data locality**: User mailbox data stays in place, and therefore continues to respect the data locality and regionality promises of Microsoft 365 or Office 365 for data at rest. In other words, the user's mailbox data is stored within the region in which the tenant (or mailbox in the case of a [Multi-Geo](/en-us/microsoft-365/enterprise/multi-geo-capabilities-in-exchange-online) tenant) is located.
2. **Device ID**: Each Outlook for iOS and Android connection registers in the Microsoft 365 or Office 365 Admin console and is able to be managed as a unique connection.
3. **Modern Authentication (OAuth)**: Outlook for iOS and Android leverages Modern Authentication (OAuth) to protect user's credentials. Modern authentication provides Outlook for iOS and Android with a secure mechanism to access Microsoft 365 or Office 365 data without ever touching a user's credentials. At sign in, the user authenticates directly against an identity platform (either Microsoft Entra ID or an on-premises identity provider like ADFS) and receives an access token in return, which grants Outlook for iOS and Android access to the user's mailbox or files. At no time does the service have access to the user's password in any form.
4. **Enterprise Mobility + Security support**: Customers can take advantage of Microsoft Enterprise Mobility + Security (EMS) including Microsoft Intune and Microsoft Entra ID P1 or P2, to enable conditional access and Intune app protection policies, which control and secure corporate messaging data on the mobile device.

Within the Microsoft 365- or Office 365-based architecture, Outlook for iOS and Android uses the native Microsoft sync technology as the protocol for data synchronization.

![new synch image.](../../exchangeonline/media/newsync.png)

The native Microsoft sync technology offers several benefits:

1. **Eliminates middle tier services**: Data synchronization with the native Microsoft sync technology occurs between the app and Microsoft 365 or Office 365, eliminating the need for any middle tier services.
2. **Latency reduction**: By replacing the proprietary Outlook device API and Stateless Protocol Translator, there's a reduction in end-to-end latency between the app and Microsoft 365 or Office 365.
3. **Additional instance support**: Removing the intermediary Stateless Protocol Translator for data connections enables Microsoft to support other unique Microsoft 365 or Office 365 instances, like Office 365 Government Community Cloud High and Office 365 Department of Defense, that were previously blocked from using Outlook for iOS and Android.
4. **Protocol consolidation**: Today, each Outlook client platform utilizes a different data sync protocol, which hinders the ability to innovate and deploy new features quickly across all Outlook clients. The native Microsoft sync technology that Outlook for iOS and Android is adopting has been in use by the native Windows 10 mail client for many years, and Outlook for Mac will use this technology in the future.
5. **Unlocking new features**: The native Microsoft sync technology enables Outlook for iOS and Android to take advantage of native Microsoft 365 or Office 365 features it doesn't support today, such as S/MIME, sensitivity labels, and shared mailboxes. These and more Microsoft 365 or Office 365 features will roll out soon after the architecture update.