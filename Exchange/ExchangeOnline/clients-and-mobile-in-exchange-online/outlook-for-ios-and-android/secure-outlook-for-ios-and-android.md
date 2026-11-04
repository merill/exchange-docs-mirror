---
layout: Conceptual
title: Securing Outlook for iOS and Android in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/secure-outlook-for-ios-and-android
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
description: 'Summary: How to enable Outlook for iOS and Android in your Exchange Online environment in a secure manner.'
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.assetid: dd886cdc-bfc1-42a4-8e67-66ae1d08af0f
ms.collection:
- exchange-online
- M365-email-calendar
ms.reviewer: smithre4
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.custom: seo-marvel-apr2020
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 247b0890-a1fe-6243-5ed5-09caa093e942
document_version_independent_id: 5abcab3a-5288-d497-e56b-b0cc1d5eb2b8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/secure-outlook-for-ios-and-android.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/secure-outlook-for-ios-and-android
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/secure-outlook-for-ios-and-android.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: f7f60bf3-8362-ae27-1bab-11dfc61137ff
---

# Securing Outlook for iOS and Android in Exchange Online | Microsoft Learn

Outlook for iOS and Android provides users the fast, intuitive email and calendar experience that users expect from a modern mobile app, while being the only app to provide support for the best features of Microsoft 365 or Office 365.

Protecting company or organizational data on users' mobile devices is extremely important. Begin by reviewing Setting up Outlook for iOS and Android, to ensure your users have all the required apps installed. After that, choose one of the following options to secure your devices and your organization's data:

1. **Recommended**: If your organization has an Enterprise Mobility + Security subscription, or separately has licensing for Microsoft Intune and Microsoft Entra ID P1 or P2, follow the steps in Using Enterprise Mobility + Security suite to protect corporate data with Outlook for iOS and Android to protect corporate data with Outlook for iOS and Android.
2. If your organization doesn't have an Enterprise Mobility + Security subscription or licensing for Microsoft Intune and Microsoft Entra ID P1 or P2, follow the steps in Using Basic Mobility and Security for Microsoft 365, and use the Basic Mobility and Security capabilities that are included in your Office 365 or Microsoft 365 subscription.
3. Follow the steps in Using Exchange Online mobile device policies to implement basic Exchange mobile device mailbox and device access policies.

If, on the other hand, you don't want to use Outlook for iOS and Android in your organization, see Blocking Outlook for iOS and Android.

Note

See Exchange Web Services (EWS) application policies later in this article if you'd rather implement an EWS application policy to manage mobile device access in your organization.

## Setting up Outlook for iOS and Android

For devices enrolled in a unified endpoint management (UEM) solution, users use the UEM solution, like the Intune Company Portal, to install the required apps: Outlook for iOS and Android and Microsoft Authenticator.

For devices that aren't enrolled in an UEM solution, users need to install:

- Outlook for iOS and Android via the Apple App Store or Google Play Store
- Microsoft Authenticator app via the Apple App Store or Google Play Store
- Intune Company Portal app via Apple App Store or Google Play Store

Once the app is installed, users can follow these steps to add their corporate email account and configure basic app settings:

- [Set up email account in Outlook for iOS mobile app](https://support.microsoft.com/office/b2de2161-cc1d-49ef-9ef9-81acd1c8e234)
- [Set up email in the Outlook for Android app](https://support.microsoft.com/office/886db551-8dfa-4fd5-b835-f8e532091872)
- [Optimizing the Outlook mobile app for your iOS or Android phone](https://support.microsoft.com/office/de075b19-b73c-4d8a-841b-459982c7e890)

Important

To use app-based conditional access policies, the Microsoft Authenticator app must be installed on iOS devices. For Android devices, the Intune Company Portal app is required. For more information, see [App-based Conditional Access with Intune](/en-us/mem/intune/protect/app-based-conditional-access-intune?form=MG0AV3).

## Using Enterprise Mobility + Security suite to protect corporate data with Outlook for iOS and Android

Important

The Allow/Block/Quarantine (ABQ) list provides no security guarantees (if a client spoofs the DeviceType header, it might be possible to bypass blocking for a particular device type). To securely restrict access to specific device types, we recommend that you configure conditional access policies. For more information, see [App-based conditional access with Intune](/en-us/mem/intune/protect/app-based-conditional-access-intune?form=MG0AV3).

The richest and broadest protection capabilities for Microsoft 365 and Office 365 data are available when you subscribe to the Enterprise Mobility + Security suite, which includes Microsoft Intune and Microsoft Entra ID P1 or P2 features, such as conditional access. At a minimum, you want to deploy a conditional access policy that only allows connectivity to Outlook for iOS and Android from mobile devices and an Intune app protection policy that ensures the corporate data is protected.

Note

While the Enterprise Mobility + Security suite subscription includes both Microsoft Intune and Microsoft Entra ID P1 or P2, customers can purchase Microsoft Intune licenses and Microsoft Entra ID P1 or P2 licenses separately. All users must be licensed in order to use the conditional access and Intune app protection policies that are discussed in this article.

### Block all email apps except Outlook for iOS and Android using conditional access

When an organization decides to standardize how users access Exchange data, using Outlook for iOS and Android as the only email app for end users, they can configure a conditional access policy that blocks other mobile access methods. You need several conditional access policies, with each policy targeting all potential users. These policies are described in [Conditional Access: Require approved client apps or app protection policy](/en-us/entra/identity/conditional-access/howto-policy-approved-app-or-app-protection).

1. Follow the steps in [Require approved client apps or app protection policy with mobile devices](/en-us/entra/identity/conditional-access/howto-policy-approved-app-or-app-protection#require-approved-client-apps-or-app-protection-policy-with-mobile-devices). This policy allows Outlook for iOS and Android, but blocks OAuth and basic authentication capable Exchange ActiveSync mobile clients from connecting to Exchange Online.

    Note

    This policy ensures mobile users can access all Microsoft 365 endpoints using the applicable apps.
2. Follow the steps in [Block Exchange ActiveSync on all devices](/en-us/entra/identity/conditional-access/howto-policy-approved-app-or-app-protection#block-exchange-activesync-on-all-devices), which prevents Exchange ActiveSync clients using basic authentication on non-mobile devices from connecting to Exchange Online.

    The previous policies use the grant access control [Require app protection policy](/en-us/azure/active-directory/active-directory-conditional-access-technical-reference), which ensures that an Intune App Protection Policy is applied to the associated account within Outlook for iOS and Android before granting access. If the user isn't assigned to an Intune App Protection Policy, isn't licensed for Intune, or the app isn't included in the Intune App Protection Policy, then the policy prevents the user from obtaining an access token and gaining access to messaging data.
3. Follow the steps in [Block legacy authentication with Microsoft Entra Conditional Access](/en-us/entra/identity/conditional-access/block-legacy-authentication) to block legacy authentication for other Exchange protocols on iOS and Android devices; this policy should target only Office 365 Exchange Online cloud app and iOS and Android device platforms. This ensures mobile apps using Exchange Web Services, IMAP4, or POP3 protocols with basic authentication can't connect to Exchange Online.

Note

After the conditional access policies are enabled, it might take up to 6 hours for any previously connected mobile device to become blocked.

When the user authenticates in Outlook for iOS and Android, Exchange Online mobile device access rules (allow, block, or quarantine) are skipped if there are any Microsoft Entra Conditional Access policies applied to the user that include:

- Cloud app condition: Exchange Online or Office 365
- Device platform condition: iOS and/or Android
- Client apps condition: Mobile apps and desktop client
- One of the following Grant access controls: [Require device to be marked as compliant](/en-us/entra/identity/conditional-access/concept-conditional-access-grant#require-device-to-be-marked-as-compliant), [Require approved client app](/en-us/entra/identity/conditional-access/concept-conditional-access-grant#require-approved-client-app) or [Require app protection policy](/en-us/entra/identity/conditional-access/concept-conditional-access-grant#require-app-protection-policy).

To use app-based conditional access policies, the Microsoft Authenticator app must be installed on iOS devices. For Android devices, the Intune Company Portal app is required. For more information, see [App-based Conditional Access with Intune](/en-us/mem/intune/protect/app-based-conditional-access-intune?form=MG0AV3).

### Protect corporate data in Outlook for iOS and Android using Intune app protection policies

App Protection Policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it might not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, with each level building off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. For Android devices, this level validates Android device attestation. This is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies and introduces IT and the user population to APP.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that's applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](/en-us/mem/intune/apps/app-protection-framework).

Regardless of whether the device is enrolled in an UEM solution, an Intune app protection policy needs to be created for both iOS and Android apps, using the steps in [How to create and assign app protection policies](/en-us/mem/intune/apps/app-protection-policies). These policies, at a minimum, must meet the following conditions:

1. They include all Microsoft mobile applications, such as Microsoft Edge, OneDrive, Office, or Teams, as this condition ensures that users can access and manipulate work or school data within any Microsoft app in a secure fashion.
2. They're assigned to all users. This ensures that all users are protected, regardless of whether they use Outlook for iOS or Android.
3. Determine which framework level meets your requirements. Most organizations should implement the settings defined in **Enterprise enhanced data protection** (Level 2) as that enables data protection and access requirements controls.

For more information on the available settings, see [Android app protection policy settings in Microsoft Intune](/en-us/mem/intune/apps/app-protection-policy-settings-android?form=MG0AV3) and [iOS app protection policy settings](/en-us/mem/intune/apps/app-protection-policy-settings-ios?form=MG0AV3).

Important

To apply Intune app protection policies against apps on Android devices that aren't enrolled in Intune, the user must also install the Intune Company Portal. For more information, see [What to expect when your Android app is managed by app protection policies](/en-us/mem/intune/fundamentals/end-user-mam-apps-android).

## Using Basic Mobility and Security for Microsoft 365

If you don't plan to use the Enterprise Mobility + Security suite, you can use Basic Mobility and Security for Microsoft 365. This solution requires that mobile devices be enrolled. When a user attempts to access Exchange Online with a device that isn't enrolled, the user is blocked from accessing the resource until they enroll the device.

Because this is a device management solution, there's no native capability to control which apps can be used even after a device is enrolled. If you want to limit access to Outlook for iOS and Android, you need to obtain Microsoft Entra ID P1 or P2 licenses and use the conditional access policies discussed in Block all email apps except Outlook for iOS and Android using conditional access.

An admin assigned the [Directory writers](/en-us/entra/identity/role-based-access-control/permissions-reference) role must complete the following steps to activate and set up enrollment. See [Set up Basic Mobility and Security](https://support.microsoft.com/office/set-up-basic-mobility-and-security-dd892318-bc44-4eb1-af00-9db5430be3cd) for complete steps. In summary, these steps include:

1. Activating Basic Mobility and Security by following the steps in the Microsoft 365 Security Center.
2. Setting up unified endpoint management by, for example, creating an APNs certificate to manage iOS devices.
3. Creating device policies and apply them to groups of users. When you do this, your users get an enrollment message on their device. And when they complete enrollment, their devices are restricted by the policies you set up for them.

Note

Policies and access rules created in Basic Mobility and Security override both Exchange mobile device mailbox policies and device access rules created in the Exchange admin center. After a device is enrolled in Basic Mobility and Security, any Exchange mobile device mailbox policy or device access rule applied to that device are ignored.

## Using Exchange Online mobile device policies

If you don't plan on using either the Enterprise Mobility + Security suite or the Basic Mobility and Security functionality, you can implement an Exchange mobile device mailbox policy to secure the device, and device access rules to limit device connectivity.

### Mobile device mailbox policy

Outlook for iOS and Android supports the following mobile device mailbox policy settings in Exchange Online:

- Device encryption enabled
- Min password length (only on Android)
- Password enabled
- Allow Bluetooth (used to manage the Outlook for Android wearable app)

    - When AllowBluetooth is enabled (default behavior) or configured for HandsfreeOnly, wearable synchronization between Outlook on the Android device and Outlook on the wearable is allowed for the work or school account.
    - When AllowBluetooth is disabled, Outlook for Android disables synchronization between Outlook on the Android device and Outlook on the wearable for the specified work or school account (and delete any data previously synced for the account). Disabling the synchronization is controlled entirely within Outlook itself; Bluetooth isn't disabled on the device or wearable nor is any other wearable app affected.

For information on how to create or modify an existing mobile device mailbox policy, see [Mobile device mailbox policies in Exchange Online](../exchange-activesync/mobile-device-mailbox-policies).

In addition, Outlook for iOS and Android supports Exchange Online's device-wipe capability. With Outlook, a remote wipe only wipes data within the Outlook app itself and doesn't trigger a full device wipe. For more information on how to perform a remote wipe, see [Perform a remote wipe on a mobile phone in Exchange Online](../exchange-activesync/remote-wipe-on-mobile-phone).

### Device access policy

Outlook for iOS and Android should be enabled by default, but in some existing Exchange Online environments the app might be blocked for a variety of reasons. Once an organization decides to standardize how users access Exchange data and use Outlook for iOS and Android as the only email app for end users, you can configure blocks for other email apps running on users' iOS and Android devices. You have two options for instituting these blocks within Exchange Online: the first option blocks all devices and only allows usage of Outlook for iOS and Android; the second option allows you to block individual devices from using the native Exchange ActiveSync apps.

Note

Because device IDs aren't governed by any *physical device* ID, they can change without notice. When this happens, it can cause unintended consequences when device IDs are used for managing user devices, as existing 'allowed' devices might be unexpectedly blocked or quarantined by Exchange. Therefore, we recommend administrators only set mobile device access policies that allow/block devices based on device type or device model.

#### Option 1: Block all email apps except Outlook for iOS and Android

You can define a default block rule and then configure an allow rule for Outlook for iOS and Android, and for Windows devices, using the following Exchange Online PowerShell commands. This configuration prevents any Exchange ActiveSync native app from connecting, and only allows Outlook for iOS and Android.

1. Create the default block rule:

    ```PowerShell
    Set-ActiveSyncOrganizationSettings -DefaultAccessLevel Block
    ```
2. Create an allow rule for Outlook for iOS and Android

    ```PowerShell
    New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Allow
    ```

#### Option 2: Block native Exchange ActiveSync apps on Android and iOS devices

Alternatively, you can block native Exchange ActiveSync apps on specific Android and iOS devices or other types of devices.

1. Confirm that there are no Exchange ActiveSync device access rules in place that block Outlook for iOS and Android:

    ```PowerShell
    Get-ActiveSyncDeviceAccessRule | Where-Object { $_.AccessLevel -eq "Block" -and $_.QueryString -like "Outlook*" } | Format-Table Name, AccessLevel, QueryString -AutoSize
    ```

    If any device access rules that block Outlook for iOS and Android are found, type the following to remove them:

    ```PowerShell
    Get-ActiveSyncDeviceAccessRule | Where-Object { $_.AccessLevel -eq "Block" -and $_.QueryString -like "Outlook*" } | Remove-ActiveSyncDeviceAccessRule
    ```
2. You can block most Android and iOS devices with the following commands:

    ```PowerShell
    New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "Android" -AccessLevel Block
    New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "iPad" -AccessLevel Block
    New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "iPhone" -AccessLevel Block
    New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "iPod" -AccessLevel Block
    ```
3. Not all Android device manufacturers specify "Android" as the DeviceType. Manufacturers might specify a unique value with each release. In order to find other Android devices that are accessing your environment, execute the following command to generate a report of all devices that have an active Exchange ActiveSync partnership:

    ```PowerShell
    Get-MobileDevice | Select-Object DeviceOS,DeviceModel,DeviceType | Export-CSV c:\temp\easdevices.csv
    ```
4. Create extra block rules, depending on your results from Step 3. For example, if you find your environment has a high usage of HTCOne Android devices, you can create an Exchange ActiveSync device access rule that blocks that particular device, forcing the users to use Outlook for iOS and Android. In this example, you would type:

    ```PowerShell
    New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "HTCOne" -AccessLevel Block
    ```

    Note

    The **-QueryString** parameter doesn't accept wildcards or partial matches.

**Additional resources**:

- [New-ActiveSyncDeviceAccessRule](/en-us/powershell/module/exchangepowershell/New-ActiveSyncDeviceAccessRule)
- [Get-MobileDevice](/en-us/powershell/module/exchangepowershell/Get-MobileDevice)
- [Set-ActiveSyncOrganizationSettings](/en-us/powershell/module/exchangepowershell/Set-ActiveSyncOrganizationSettings)

## Blocking Outlook for iOS and Android

If you don't want users in your organization to access Exchange data with Outlook for iOS and Android, the approach you take depends on whether you're using Microsoft Entra Conditional Access policies or Exchange Online's device access policies.

### Option 1: Block mobile device access using a conditional access policy

Microsoft Entra Conditional Access doesn't provide a mechanism whereby you can specifically block Outlook for iOS and Android while allowing other Exchange ActiveSync clients. With that said, conditional access policies can be used to block mobile device access in two ways:

- Option A: Block mobile device access on both the iOS and Android platforms
- Option B: Block mobile device access on a specific mobile device platform

#### Option A: Block mobile device access on both the iOS and Android platforms

If you want to prevent mobile device access for all users, or a subset of users, using conditional access, follow these steps.

Create conditional access policies, with each policy either targeting all users or a subset of users via a security group. Details are in [Common Conditional Access policy: Require approved client apps or app protection policy](/en-us/entra/identity/conditional-access/howto-policy-approved-app-or-app-protection).

1. The first policy blocks Outlook for iOS and Android and other OAuth capable Exchange ActiveSync clients from connecting to Exchange Online. See "Step 1 - Configure a Microsoft Entra Conditional Access policy for Exchange Online," but for the fifth step, choose **Block access**.
2. The second policy prevents Exchange ActiveSync clients using basic authentication from connecting to Exchange Online. See "Step 2 - Configure a Microsoft Entra Conditional Access policy for Exchange Online with ActiveSync (EAS)."

#### Option B: Block mobile device access on a specific mobile device platform

If you want to prevent a specific mobile device platform from connecting to Exchange Online, while allowing Outlook for iOS and Android to connect using that platform, create the following conditional access policies, with each policy targeting all users. Details are in [Common Conditional Access policy: Require approved client apps or app protection policy](/en-us/entra/identity/conditional-access/howto-policy-approved-app-or-app-protection).

1. The first policy allows Outlook for iOS and Android on the specific mobile device platform and blocks other OAuth capable Exchange ActiveSync clients from connecting to Exchange Online. See "Step 1 - Configure a Microsoft Entra Conditional Access policy for Exchange Online," but for step 4a, select only the desired mobile device platform (such as iOS) to which you want to allow access.
2. The second policy blocks the app on the specific mobile device platform and other OAuth capable Exchange ActiveSync clients from connecting to Exchange Online. See "Step 1 - Configure a Microsoft Entra Conditional Access policy for Exchange Online," but for step 4a, select only the desired mobile device platform (such as Android) to which you want to block access, and for step 5, choose **Block access**.
3. The third policy prevents Exchange ActiveSync clients using basic authentication from connecting to Exchange Online. See "Step 2 - Configure a Microsoft Entra Conditional Access policy for Exchange Online with ActiveSync (EAS)."

### Option 2: Block Outlook for iOS and Android using Exchange mobile device access rules

If you're managing your mobile device access via Exchange Online's device access rules, you have two options:

- Option A: Block Outlook for iOS and Android on both the iOS and Android platforms
- Option B: Block Outlook for iOS and Android on a specific mobile device platform

Every Exchange organization has different policies regarding security and device management. If an organization decides that Outlook for iOS and Android doesn't meet their needs or isn't the best solution for them, administrators have the ability to block the app. Once the app is blocked, mobile Exchange users in your organization can continue accessing their mailboxes by using the built-in mail applications on iOS and Android.

The `New-ActiveSyncDeviceAccessRule` cmdlet has a `Characteristic` parameter, and there are three `Characteristic` options that administrators can use to block the Outlook for iOS and Android app. The options are UserAgent, DeviceModel, and DeviceType. In the two blocking options described in the following sections, you use one or more of these characteristic values to restrict the access that Outlook for iOS and Android has to the mailboxes in your organization.

The values for each characteristic are displayed in the following table:

| Characteristic | String for iOS | String for Android |
| --- | --- | --- |
| DeviceModel | Outlook for iOS and Android | Outlook for iOS and Android |
| DeviceType | Outlook | Outlook |
| UserAgent | Outlook-iOS/2.0 | Outlook-Android/2.0 |

#### Option A: Block Outlook for iOS and Android on both the iOS and Android platforms

With the `New-ActiveSyncDeviceAccessRule` cmdlet, you can define a device access rule, using either the `DeviceModel` or `DeviceType` characteristic. In both cases, the access rule blocks Outlook for iOS and Android across all platforms, and prevents any device, on both the iOS platform and Android platform, from accessing an Exchange mailbox via the app.

The following are two examples of a device access rule. The first example uses the `DeviceModel` characteristic; the second example uses the `DeviceType` characteristic.

```PowerShell
New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "Outlook" -AccessLevel Block
```

```PowerShell
New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Block
```

#### Option B: Block Outlook for iOS and Android on a specific mobile device platform

With the `UserAgent` characteristic, you can define a device access rule that blocks Outlook for iOS and Android across a specific platform. This rule prevents a device from using Outlook for iOS and Android to connect on the platform you specify. The following examples show how to use the device-specific value for the `UserAgent` characteristic.

To block Android and allow iOS:

```PowerShell
New-ActiveSyncDeviceAccessRule -Characteristic UserAgent -QueryString "Outlook-Android/2.0" -AccessLevel Block
New-ActiveSyncDeviceAccessRule -Characteristic UserAgent -QueryString "Outlook-iOS/2.0" -AccessLevel Allow
```

To block iOS and allow Android:

```PowerShell
New-ActiveSyncDeviceAccessRule -Characteristic UserAgent -QueryString "Outlook-Android/2.0" -AccessLevel Allow
New-ActiveSyncDeviceAccessRule -Characteristic UserAgent -QueryString "Outlook-iOS/2.0" -AccessLevel Block
```

## Exchange Online controls

Beyond Microsoft Endpoint Manager, Basic Mobility and Security for Microsoft 365, and Exchange mobile device policies, you can manage the access that mobile devices have to information in your organization through various Exchange Online controls, as well as, whether to allow users access to add-ins within Outlook for iOS and Android.

### Exchange Web Services (EWS) application policies

An EWS application policy can control whether or not applications are allowed to use the REST API. When you configure an EWS application policy that only allows specific applications access to your messaging environment, you must add the user-agent string for Outlook for iOS and Android to the EWS allow list.

The following example shows how to add the user-agent strings to the EWS allow list:

```PowerShell
Set-OrganizationConfig -EwsAllowList @{Add="Outlook-iOS/*","Outlook-Android/*"}
```

### Exchange User controls

With the native Microsoft sync technology, administrators can control usage of Outlook for iOS and Android at the mailbox level. By default, users are allowed to access mailbox data using Outlook for iOS and Android. The following example shows how to disable a user's mailbox access with Outlook for iOS and Android:

```PowerShell
Set-CASMailbox jane@contoso.com -OutlookMobileEnabled $false
```

### Managing add-ins

Outlook for iOS and Android lets users integrate popular apps and services with the email client. Add-ins for Outlook are available on the web, Windows, Mac, and mobile. Since add-ins are managed via Microsoft 365 or Office 365, users are able to share data and messages between Outlook for iOS and Android and the unmanaged add-in (even when the account is managed by an Intune App Protection policy), unless add-ins are turned off for the user within the Microsoft 365 admin center.

If you want to stop your end users from accessing and installing Outlook add-ins (which affects all Outlook clients), execute the following changes to roles in the Microsoft 365 admin center:

- To prevent users from installing Office Store add-ins, remove the My Marketplace role from them.
- To prevent users from side loading add-ins, remove the My Custom Apps role from them.
- To prevent users from installing all add-ins, remove both, My Custom Apps and My Marketplace roles from them.

For more information, please see [Add-ins for Outlook](../add-ins-for-outlook/add-ins-for-outlook) and how to [Manage deployment of add-ins in the Microsoft 365 admin center](/en-us/microsoft-365/admin/manage/manage-deployment-of-add-ins).