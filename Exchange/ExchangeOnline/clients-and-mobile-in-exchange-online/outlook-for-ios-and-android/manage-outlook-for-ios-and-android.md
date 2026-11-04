---
layout: Conceptual
title: Managing Outlook for iOS and Android in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/manage-outlook-for-ios-and-android
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
description: 'Summary: This article describes best practices for managing mobile devices with Outlook for iOS and Android in Exchange Online.'
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 30e8c819-4d41-4458-a746-a9ba9a84a7c0
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
document_id: 8bff51b2-eb56-a0ba-f8fe-e4ce5683636b
document_version_independent_id: 241ff142-7a08-d291-948f-0a0d6219f11b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/manage-outlook-for-ios-and-android.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/manage-outlook-for-ios-and-android
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/manage-outlook-for-ios-and-android.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/b8932893-874f-48e4-b2d5-5521fe75a61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/e757ef92-a039-44aa-8ed6-705843b26fea
platformId: f0757aeb-57e0-b74d-19fb-b3cb3ad69d64
---

# Managing Outlook for iOS and Android in Exchange Online | Microsoft Learn

**Summary**: This article describes best practices for managing mobile devices with Outlook for iOS and Android in Exchange Online.

Outlook for iOS and Android give users the fast, intuitive email and calendar experience, while being the only app to provide support for the best features of Microsoft 365 and Office 365. In addition, Microsoft provides many utilities for managing and protecting company data on mobile devices in your Exchange Online organization.

## Options for managing devices and applications

Customers looking to manage Outlook for iOS and Android have the following options:

1. **Recommended**: The Enterprise Mobility + Security suite, which includes Microsoft Intune and Microsoft Entra Conditional Access.
2. Basic Mobility and Security for Microsoft 365.
3. Third-party Unified Endpoint Management solutions.
4. Mobile Device Access and Mobile Device Mailbox Policies.

Note

For implementation details on each of these three options, see [Securing Outlook for iOS and Android in Exchange Online](secure-outlook-for-ios-and-android).

Microsoft recommends that customers use the features of the Enterprise Mobility + Security suite to protect corporate data on mobile devices, due to the advanced capabilities provided by these services.

Important

When the user authenticates in Outlook for iOS and Android, Exchange Online mobile device access rules (allow, block, or quarantine) are skipped if there are any Microsoft Entra Conditional Access policies applied to the user that include:

- Cloud app condition: Exchange Online or Office 365
- Device platform condition: iOS and/or Android
- Client apps condition: Mobile apps and desktop client
- One of the following Grant access controls: [Require device to be marked as compliant](/en-us/entra/identity/conditional-access/concept-conditional-access-grant#require-device-to-be-marked-as-compliant), [Require approved client app](/en-us/entra/identity/conditional-access/concept-conditional-access-grant#require-approved-client-app) or [Require app protection policy](/en-us/entra/identity/conditional-access/concept-conditional-access-grant#require-app-protection-policy).

Note

When using mobile device cmdlets such as `Get-MobileDevice` to check the status of a device, the timestamp for Outlook for iOS and Android synchronization, indicated by the `LastSyncTime` property, may be up to 15 minutes behind the actual time of synchronization. While device synchronization does occur in real time, the returned time stamp may lag behind.

### Using Enterprise Mobility + Security

The richest and broadest protection capabilities for Microsoft 365 and Office 365 data are available when you subscribe to the Enterprise Mobility + Security suite. This suite includes Microsoft Intune, Azure Information Protection, and Microsoft Entra ID P1 or P2 features, such as conditional access.

Note

While the Enterprise Mobility + Security suite subscription includes licenses for both Microsoft Intune and Microsoft Entra ID, customers can purchase Microsoft Intune licenses and Microsoft Entra ID P1 or P2 licenses separately. All users must be licensed to leverage the conditional access and Intune app protection policies discussed in this article.

Intune provides mobile application management (MAM) capabilities, and other conditional access and device management capabilities. With Intune app protection policies, you can restrict actions on corporate data between apps managed by Intune and unmanaged apps. For example, cut, copy, paste, and "save as." For more information, see [How to create and assign app protection policies](/en-us/mem/intune/apps/app-protection-policies?form=MG0AV3). Additionally, the Intune-managed Outlook apps include a new multi-identity management feature that enables users to access both their personal and work email accounts in the same Outlook app while only applying the Intune app protection policies to the user's work account. This feature provides a much more seamless user experience.

Conditional access is a capability of Microsoft Entra ID that enables you to centrally enforce app access controls based on specific conditions. By using conditional access policies, you can apply the right access controls under the required conditions. Microsoft Entra Conditional Access provides you with added security when such security is needed, and it stays out of your users' way when it isn't.

Key features of the Enterprise Mobility + Security suite with Outlook for iOS and Android:

- **Conditional access**. Microsoft Entra ID ensures that Exchange Online email can be accessed only when the conditional access requirements are met. For more information on device enrollment, see [What is Conditional Access?](/en-us/entra/identity/conditional-access/overview).
- **Intune app protection**. Outlook for iOS and Android allows you to protect your corporate data with Intune app protection policies. This method is a great option for "bring your own device" (BYOD) scenarios where you want to keep corporate data safe without managing a user's devices. For more information on Intune app protection policies, see [Protect app data using mobile app management policies with Microsoft Intune](/en-us/mem/intune/apps/app-protection-policy).
- **Device enrollment**. Intune lets you manage your workforce's devices and apps, and how they access your company data. Outlook for iOS and Android ensures that Exchange Online email is accessible only on managed and compliant phones and tablets. When users sign in to the Outlook app on an unmanaged mobile device, Outlook prompts users to enroll the device in Intune by using the Azure conditional access policy, and then validates that the device meets organizational standards of device compliance.
- **Device management and reporting**. The enrollment process allows organizations to set and manage security policies. For example, enforce device-level PIN lock, require data encryption, and block compromised devices to prevent untrusted devices from accessing corporate email and data. Each enrolled device appears in the Microsoft 365 admin center, and reporting is available to provide details on the devices that access your corporate data.
- **Selective wipe**. Microsoft Intune can remove email data from Outlook for iOS and Android, while leaving any personal email accounts intact (whether the device is enrolled or not). This feature is an increasingly important requirement as more businesses adopt a "bring your own device" approach to phones and tablets.

### Using Basic Mobility and Security for Microsoft 365

Basic Mobility and Security for Microsoft 365 provides device management capabilities at no extra cost. Microsoft Intune powers these basic capabilities, providing a core set of controls in the Microsoft 365 admin center for organizations that need the basics.

There's no native capability to control which apps can be used, even after a device is enrolled. If you want to limit access to Outlook for iOS and Android, you need Microsoft Entra ID P1 or P2 licenses to use conditional access policies.

Outlook for iOS and Android fully supports the capabilities provided by Basic Mobility and Security for Microsoft 365.

For detailed information, see the following resources:

- [Overview of Basic Mobility and Security for Microsoft 365](https://support.microsoft.com/office/faa7d8e5-645d-4d59-839c-c8d4c1869e4a).
- [Manage settings and features on your devices with Microsoft Intune policies](/en-us/mem/intune/configuration/device-profiles)
- Instructions for your end-users to enroll a device in Basic Mobility and Security: [Enroll your mobile device using Basic Mobility and Security](https://support.microsoft.com/office/c8ac722d-dcaf-4135-8345-3e6327f5d3c5)

### Using Third-Party Unified Endpoint Management Solutions

Third-party unified endpoint management providers can deploy the Outlook for iOS and Android the same way they would deploy any iOS or Android app, using their existing tools. They can also apply important, universal device management controls. For example, device PIN, device encryption, device wipe, and more.

Third-party providers can also deploy certain app configuration settings, like account setup, organization allowed accounts mode, and general app configuration settings, to Outlook for iOS and Android; for more information, please see [Deploying Outlook for iOS and Android app configuration settings](outlook-for-ios-and-android-configuration-with-microsoft-intune).

To manage and protect corporate data within the app (for example, restrict cut, copy, paste, and "save as" actions with corporate data), customers need to use Microsoft's Enterprise Mobility + Security suite.

### Using Mobile Device Access and Mobile Device Mailbox Policies

Microsoft recommends that customers use either the Enterprise Mobility + Security suite or the built-in Basic Mobility and Security for Microsoft 365 to manage company data on mobile devices, due to the advanced capabilities provided by those services. Outlook for iOS and Android does support mobile device access and mobile device mailbox policies (formerly known as Exchange Active Sync policies), which are available through the Exchange admin center.

Outlook for iOS and Android supports the following Exchange mobile device mailbox policy settings:

- Device encryption enabled
- Min password length (only on Android)
- Password enabled
- Allow Bluetooth (used to manage the Outlook for Android wearable app when Intune App Protection Policies aren't in use)

    - When this setting is enabled (it's enabled by default) or configured for HandsfreeOnly, Outlook synchronization between the Android device and the wearable device is allowed for the work or school account.
    - When this setting is disabled, Outlook synchronization between the Android device and the wearable device isn't allowed for the work or school account (and any previously synced data for the account is deleted). Disabling the synchronization is controlled entirely within Outlook itself. Bluetooth isn't disabled on the device or wearable nor is any other wearable app affected.

For information on how to create or modify an existing mobile device mailbox policy, see [Mobile device mailbox policies in Exchange Online](../exchange-activesync/mobile-device-mailbox-policies).

Exchange administrators can also initiate a remote device wipe against Outlook for iOS and Android using Exchange admin center. After receiving the remote wipe request, the app removes the Outlook profile and all data associated with it.

Note

Outlook for iOS and Android only supports the **Wipe Data** remote wipe command and does not support **Account Only Remote Wipe Device** as defined in the Exchange admin center. For more information on how to perform a remote wipe, see [Perform a remote wipe on a mobile phone](../../clients/exchange-activesync/remote-wipe).

For more information about Microsoft Intune, see [Documentation for Microsoft Intune](/en-us/mem/intune/).