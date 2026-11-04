---
layout: Conceptual
title: Using Outlook for iOS and Android in the Government Community Cloud in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-in-the-government-cloud
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
description: 'Summary: How organizations in the Office 365 U.S. Government Community Cloud (GCC) can enable Outlook for iOS and Android for their users.'
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: 73b693d9-39bb-4689-a1ff-4be505a5945b
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
document_id: ba22add1-5185-c5b2-8520-c47855559a7a
document_version_independent_id: f79f12a8-fb77-5a0f-d152-441394373673
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-in-the-government-cloud.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-in-the-government-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-in-the-government-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 9fcd6a32-ff26-dc03-7a5a-665f7ec186d7
---

# Using Outlook for iOS and Android in the Government Community Cloud in Exchange Online | Microsoft Learn

**Summary**: How organizations in the Office 365 U.S. Government Community Cloud (GCC) can enable Outlook for iOS and Android for their Exchange Online users.

Outlook for iOS and Android is fully architected in the Microsoft Cloud and meets the security and compliance requirements of all United States Government customers when the mailboxes reside in Exchange Online.

For customers with Exchange Online mailboxes operating in the Government Community Cloud (GCC Moderate, GCC High or Department of Defense), Outlook for iOS and Android uses the [native Microsoft sync technology](outlook-for-ios-and-android). This architecture is FedRAMP-compliant (defined by NIST Special Publication 800-145) and approved, and meets GCC High and DoD requirements DISA SRG Level 4 (GCC-High) and Level 5 (DoD), Defense Federal Acquisition Regulations Supplement (DFARS), and International Traffic in Arms Regulations (ITAR), which were approved by a third-party assessment organization and are FISMA-compliant based on the NIST 800-53 rev 4.

For more information, please see the Office 365 FedRAMP System Security plan located in the FedRAMP Audit Reports section of the [Microsoft Service Trust Portal](https://servicetrust.microsoft.com/).

Important

Customers operating in the Government Community Cloud might have user mailboxes that also reside on-premises via an Exchange hybrid topology. Accessing on-premises mailboxes with Outlook for iOS and Android doesn't utilize an architecture that is FedRAMP-compliant. For more information on this architecture, see [Using Basic authentication with Outlook for iOS and Android](../../clients/outlook-for-ios-and-android/use-basic-auth).

This article covers how to:

- Enable Outlook for iOS and Android for Office 365 GCC customers.
- Unlock non-FedRAMP compliant features, if needed.

## Enabling Outlook for iOS and Android for Office 365 GCC customers

GCC (Moderate, High, and Department of Defense) customers can use Outlook for iOS and Android without any special configuration.

For Office 365 GCC customers who don't currently use Outlook for iOS and Android, enabling the app requires the following actions:

1. Unblocking Outlook for iOS and Android in the organization.
2. Downloading the app on user devices.
3. Having users add their account on their devices.

### 1. Unblock Outlook for iOS and Android

Remove any restrictions in your Exchange environment that might block Outlook for iOS and Android. Update your Exchange mobile device access rules or any relevant Microsoft Entra Conditional Access policies to unblock the app. For more information about making Outlook the only approved mobile messaging client, see [Securing Outlook for iOS and Android in Exchange Online](secure-outlook-for-ios-and-android).

### 2. Download and install Outlook for iOS and Android

End users need to install the app on their devices. How the installation happens depends on whether or not the devices are enrolled in a unified endpoint management (UEM) solution, such as Microsoft Intune. Users with enrolled devices can install the app through their UEM solution, like the Intune Company Portal. Users with devices that aren't enrolled in an UEM solution can search for "Microsoft Outlook" in the Apple App Store or Google Play Store and download it from one of those locations.

Note

To leverage app-based conditional access policies, the Microsoft Authenticator app must be installed on iOS devices. For Android devices, the Intune Company Portal app is leveraged. For more information, see [App-based conditional access with Intune](/en-us/MEM/intune/protect/app-based-conditional-access-intune?form=MG0AV3).

## Disabled services and features

By default, certain services and features of Outlook for iOS and Android are disabled automatically for the Office 365 U.S. Government Community Cloud (GCC) because they don't meet FedRAMP requirements:

- **In-app support**: Users aren't able to submit support tickets from within the app or upload diagnostic data using Collect Diagnostics. They should contact their internal help desk and provide logs (via the Share Diagnostics Logs option in Setting -&gt; Help). If necessary, the organization's IT department can then contact Microsoft Support directly.

    Important

    Setting *OutlookMobileGCCRestrictionsEnabled* to false allows submission of support, diagnostic, or crash data to be sent to Microsoft through in-app support or by using Collect Diagnostics. The data are uploaded to Microsoft systems that are outside of the Office 365 GCC compliance boundary, including the Office 365 FedRAMP boundary. Customers should update organizational training and policy materials to instruct users to avoid including any sensitive US government information as part of the in-app support submission.
- **In-app feature requests**: Users aren't able to submit in-app feature requests.
- **Multiple accounts**: Only the user's Office 365 GCC account and OneDrive account can be added to a single device. Personal accounts can't be added. Customers can use another device for personal accounts, or an Exchange ActiveSync client from another provider.
- **Calendar Apps**: Calendar apps (Facebook, Wunderlist, Evernote, Meetup) aren't available with GCC accounts.
- **Add-Ins**: Add-ins aren't available with GCC accounts.
- **Storage Providers**: Only the GCC account's OneDrive storage account can be added within Outlook for iOS and Android. Third-party storage accounts (for example, Dropbox, Box) can't be added.
- **Office Lens**: Office Lens technology (for example, scanning business cards and taking pictures) included in Outlook for iOS and Android isn't available with GCC accounts.
- **File picker**: The file picker used for adding attachments during email composition is limited to email attachments, iCloud & Device, OneDrive files, and SharePoint sites. The Recent Files list is limited to email attachments.
- **TestFlight**: GCC accounts aren't able to access prerelease features when using the TestFlight version of Outlook for iOS.

Executing the below Exchange Online cmdlet enables GCC users using Outlook for iOS and Android access to the above features and services that aren't FedRAMP compliant:

```PowerShell
Set-OrganizationConfig -OutlookMobileGCCRestrictionsEnabled $false
```

At any time, access to the above features can be revoked by resetting the parameter back to the default value:

```PowerShell
Set-OrganizationConfig -OutlookMobileGCCRestrictionsEnabled $true
```

Changing this setting typically takes effect within 48 hours. As this setting is a tenant-based change, all Outlook for iOS and Android users in the GCC organization are affected.

For more information on the cmdlet, see [Set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/set-organizationconfig).

## Services and features not available

Certain services and features of Outlook for iOS and Android aren't available for the Office 365 U.S. Government Community Cloud (GCC) because they don't meet FedRAMP requirements:

- **Location services**: Bing location services aren't available with GCC accounts. Features that rely on location services, like Cortana Time To Leave, are also unavailable.
- **Privacy settings**: Privacy settings can't be configured through the Office cloud policy service.
- **Play My Emails**: Play My Emails isn't available for GCC accounts.
- **To Do**: To Do is currently not available for GCC accounts.

For more information on the cmdlet, see [Set-OrganizationConfig](/en-us/powershell/module/exchangepowershell/set-organizationconfig).