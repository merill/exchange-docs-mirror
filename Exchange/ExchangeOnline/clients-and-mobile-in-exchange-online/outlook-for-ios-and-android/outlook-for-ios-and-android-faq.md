---
layout: Conceptual
title: 'Outlook for iOS and Android in Exchange Online: FAQ | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-faq
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
description: Learn about the most common questions asked by customers and administrators about using Outlook for iOS and Android with Exchange Online and Microsoft 365 or Office 365.
ms.topic: faq
author: AshaIyengar21
ms.author: serdars
ms.assetid: 747d4875-4b81-4b10-a206-fc2cbab83314
ms.collection:
- exchange-online
- M365-email-calendar
ms.reviewer: akprakash
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.custom: seo-marvel-apr2020
ms.date: 2023-10-31T00:00:00.0000000Z
locale: en-us
document_id: 398ae9a4-c12a-bbac-80b5-570b653867a5
document_version_independent_id: ad0617f6-897a-2f94-b109-a5fb6e6f31c1
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-faq.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-faq.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: d8952b13-06a9-7ffb-1b59-25469030cef0
---

# Outlook for iOS and Android in Exchange Online: FAQ | Microsoft Learn

**Summary**: This article covers the most common questions asked by customers and administrators about using Outlook for iOS and Android with Exchange Online and Microsoft 365 or Office 365.

The Outlook for iOS and Android app is designed to enable users in your organization to do more from their mobile devices, by bringing together email, calendar, contacts, and other files. The following sections highlight the most common questions we receive, across three key areas:

- Outlook for iOS and Android architecture and security
- Managing and maintaining Outlook for iOS and Android in your Exchange organization after it has been deployed
- Common questions from end users who access information in your Exchange organization with the Outlook for iOS and Android app on their mobile devices

## Architecture and security

The following questions are about the overall architecture of Outlook for iOS and Android in Exchange Online, as well as user authentication and other security concerns.

### Q: What cloud architecture is utilized by Outlook for iOS and Android for Microsoft 365 or Office 365 accounts?

For more information on the architecture, see [Outlook for iOS and Android in Exchange Online](outlook-for-ios-and-android).

### Q: Can I add two different Microsoft 365 or Office 365 accounts from different regions to Outlook for iOS and Android?

Yes, provided both accounts don't have Intune App Protection Policies assigned. However, for Government Community Cloud customers, users might only add their own account and OneDrive for Business storage account to the app; adding personal or other commercial accounts is prevented to meet FedRAMP requirements. For more information on Government Community Cloud restrictions with Outlook for iOS and Android, see [Using Outlook for iOS and Android in the Government Community Cloud](outlook-for-ios-and-android-in-the-government-cloud).

### Q: What authentication mechanism is used for Outlook for iOS are Android? Are credentials stored in Microsoft 365 or Office 365?

See [Account setup with modern authentication in Exchange Online](setup-with-modern-authentication).

### Q: Do Outlook for iOS and Android and other Microsoft Office mobile apps support single sign-on?

See [Account setup with modern authentication in Exchange Online](setup-with-modern-authentication).

### Q: What is the lifetime of the tokens generated and used by the Active Directory Authentication Library (ADAL) in Outlook for iOS and Android?

See [Account setup with modern authentication in Exchange Online](setup-with-modern-authentication).

### Q: What happens to the access token when a user's password is changed?

See [Account setup with modern authentication in Exchange Online](setup-with-modern-authentication).

### Q: Does Outlook for iOS and Android support certificate-based authentication?

Yes, Outlook for iOS and Android supports certificate-based authentication for modern authentication-enabled accounts (Microsoft 365 or Office 365 accounts or [on-premises accounts using hybrid modern authentication](../../clients/outlook-for-ios-and-android/use-hybrid-modern-auth)). For more information, see:

- [Configuring Active Directory Federation Services (ADFS)](/en-us/archive/blogs/samueld/adfs-certauth-aad-o365)
- [Certificate-based authentication on iOS](/en-us/entra/identity/authentication/certificate-based-authentication-federation-ios)
- [Certificate-based authentication on Android](/en-us/entra/identity/authentication/certificate-based-authentication-federation-android)

### Q: What does background synchronization enable? I notice that when I launch the app with it enabled, I still have to wait for messages to download, even after I've received new mail notifications for them; and sometimes, I get reminders for appointments that had been canceled.

Background synchronization enables new message notifications, calendar reminders, badge count updates, and background synchronization of mailbox and calendar information for Outlook for iOS and Android.

If background synchronization is disabled by the user in the mobile operating system's settings, then the user must launch the app and keep it in the foreground in order to synchronize messages and have an up-to-date calendar.

Background synchronization in Outlook for iOS and Android can also be temporarily disabled by the following actions:

- Force quitting Outlook for iOS.
- Restarting the iOS device.
- Outlook for iOS crashes and isn't restarted by the user.
- Not opening the app for a given period of time. iOS [automatically freezes third-party apps](https://developer.apple.com/library/archive/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/BackgroundExecution/BackgroundExecution.html), like Outlook, based on usage patterns. Android [doze mode and app standby](https://developer.android.com/training/monitoring-device-state/doze-standby) features can also prevent background updates to the app while those features are active.
- On some Android devices, you can also restrict background processing or network access per-app. In these cases, Outlook for Android can't process updates in the background. Android device manufacturers can modify the way you can interact with settings, therefore it isn't possible to document every device scenario, but in general, the following steps can be followed to remove battery optimization:

    1. Open **Settings**.
    2. Tap **Battery**.
    3. Tap the ellipse and tap **Battery optimization**.
    4. Tap the down arrow and tap **All apps**.
    5. For the Microsoft Authenticator, Intune Company Portal, and Outlook apps, tap **Not optimized** to turn off battery optimization.

If the mobile operating system prevents background synchronization, users experience the following results:

- New mail notifications continue to be delivered. However, upon launching the app, the new messages need to be downloaded.
- Calendar reminders fire for appointments that have been canceled, because the app was unable to download and process the meeting cancellation.

Note

Apple allows its native Mail and Calendar apps to do background refreshes without any restrictions. Therefore, users might notice a difference in the background synchronization experience between the apps. However, this also results in improved battery life and less data consumption with Outlook for iOS.

### Q: Does each user's instance of Outlook for iOS and Android have a unique device ID in the Microsoft 365- or Office 365-based architecture? How is the device ID generated and is this same device ID used in Intune?

Upon initial account sign in, Outlook for iOS and Android establishes a connection to the Microsoft 365- or Office 365-based architecture. A unique device ID is generated, and this device ID is what appears in Active Directory device records (which can be retrieved with cmdlets such as `Get-MobileDevice` in Exchange Online PowerShell) and which appears in HTTP request headers.

Intune uses a different device ID. The basic workflow for how Intune assigns a device ID is described in [App-based conditional access with Intune](/en-us/mem/intune/protect/app-based-conditional-access-intune). In Intune, the device ID is assigned when the device workplace joins for all device-conditional access scenarios. This ID is a Microsoft Entra ID-generated unique ID for the device. Intune uses that unique ID when sending compliance information, and ADAL uses that unique ID when authenticating to services.

### Q: Does Outlook for iOS and Android support RMS?

Yes. Outlook for iOS and Android supports reading protected messages. Outlook for iOS and Android works differently than desktop versions of Outlook when it comes to RMS. For desktop versions of Outlook, once a protected message is received and access is attempted, and Outlook verifies that the user can read RM messages, Outlook connects to Exchange to request an encryption key. The Outlook desktop client uses that encryption key to decrypt the message in front of the user (client-side). Mobile clients operate differently. When Outlook for iOS and Android sets up its initial relationship with Exchange, it notifies Exchange that it supports RMS. Exchange decrypts any protected messages before passing them to the client. In other words, decryption is performed server-side. Outlook for iOS and Android doesn't perform any decryption itself.

In cases where Outlook for iOS and Android receives protected messages and prompts end users to use an RM client to open the file, it means that Exchange hasn't decrypted the message, which is due to an issue on the Exchange side.

Note

Outlook for iOS uses iOS's native preview technology to quickly expose attachments to end users. iOS's preview technology doesn't support rights management and reports the error "The operation couldn't be completed. (OfficeImportErrorDomain error 912)" when a user attempts to open a rights-protected attachment. Users need to tap the respective Word, Excel, or PowerPoint app icon to open the rights-protected attachment in the native app.

### Q: Does Outlook for iOS and Android support Teams meetings?

Yes, Outlook for iOS and Android supports both Skype for Business and Teams meetings. The Teams coexistence mode at the Microsoft 365 or Office 365 organization level and the user level (the user setting takes precedence over the tenant setting) determines the meeting creation experience in Outlook for iOS and Android:

| Coexistence Mode | Outlook for iOS and Android experience |
| --- | --- |
| Islands | Skype for Business |
| Skype for Business Only | Skype for Business |
| Skype for Business with Teams Collaboration | Skype for Business |
| Teams Only | Teams |
| Skype for Business with Teams Collaboration and Meetings | Teams |

In addition, for users using the native Microsoft sync technology, a Teams Join button is available in calendar events. This provision makes it easy to Join a Teams meeting and is available for all coexistence modes. Users who aren't using the native Microsoft sync technology can join Teams Meetings using the web link in the meeting description.

For more information on the Teams coexistence modes, see [Choose your upgrade journey from Skype from Business to Teams](/en-us/microsoftteams/upgrade-and-coexistence-of-skypeforbusiness-and-teams).

### Q: What ports and end points does Outlook for iOS and Android use?

Outlook for iOS and Android communicates via TCP port 443. The app accesses various end points, depending on the activities of the user. Complete information is available in [URLs and IP address ranges](/en-us/office365/enterprise/urls-and-ip-address-ranges).

### Q: Does Outlook for iOS and Android support proxy configurations?

Yes, Outlook for iOS and Android supports proxy configurations when the proxy infrastructure meets the following requirements:

- **Supports HTTP protocol without TLS decryption and inspection**.
- **Doesn't perform authentication**.

Outlook for iOS and Android consume the proxy configuration as defined by the platform operating system. Typically, this configuration information is deployed via a PAC file. The PAC file must be configured to use hostnames instead of protocol; no extra custom settings are supported. For a list of hostnames that Outlook for iOS and Android accesses, see [URLs and IP address ranges](/en-us/office365/enterprise/urls-and-ip-address-ranges).

For tenants that haven't been migrated to the native Microsoft sync technology, the following extra requirement applies:

- **Supports and has SOCKS proxy capability enabled**. The Outlook for iOS and Android client utilizes TCP connections to our Microsoft 365- or Office 365-based architecture. The IP ranges for the SOCKS connections aren't restricted to a subset of Azure IP ranges, which means that customers can't define an allowlist range. The PAC must be configured to use hostnames instead of protocol and return the SOCKS proxy information given the host URL; no extra custom settings are supported.

### Q: Does Outlook for iOS and Android support shared mailboxes?

Yes, Outlook for iOS and Android supports shared mailboxes when the user mailbox and shared mailbox are located in Exchange Online and using the native Microsoft sync technology.

A shared mailbox is a special mailbox type that is created using the -Shared parameter. Access to the shared mailbox by a user is obtained via permissions and not by using alternate credentials. For more information, see [Shared mailboxes in Exchange Online](../../collaboration-exo/shared-mailboxes).

### Q: Does Outlook for iOS and Android support delegate mailboxes?

Yes, Outlook for iOS and Android has extended the shared mailbox capability to now allow users to add another person's mailbox when the user has been granted FullAccess permissions to the other person's mailbox. Granting SendAs or Send on Behalf of permissions also allows the user to send messages as the other person's mailbox. For more information on permission assignment, see [Manage permissions for recipients in Exchange Online](../../recipients-in-exchange-online/manage-permissions-for-recipients).

### Q: How many accounts does Outlook for iOS and Android support?

Outlook for iOS and Android supports a maximum of 25 accounts.

### Q: Does Outlook for iOS and Android support contact management functionality? What about integration with the operating system features?

Yes, Outlook for iOS and Android supports contact management. Within the app, users can initiate phone calls, text messages, video chat (for example, FaceTime), etc. Integration with the operating system, and contact management functionality, depend on the client platform, where the mailbox resides, and the authentication type used:

| Functionality | Office 365 mailbox | On-premises mailbox using Hybrid Modern Authentication | On-premises mailbox using Basic Authentication |
| --- | --- | --- | --- |
| **Export Outlook contacts to native Contacts app** | iOS | iOS | iOS  Android |
| **Bi-directional sync of Outlook contacts with native Contacts app** | Android | Android | Not supported |
| **Add a new contact from Outlook** | iOS  Android | iOS  Android | Not supported |
| **Edit an existing contact from Outlook** | iOS  Android | iOS  Android | Not supported |
| **Delete an existing contact from Outlook** | iOS  Android | Not supported | Not supported |
| **Sync profile picture between Outlook contacts and the native Contacts app** | Android | Android | Not supported |

By enabling contact synchronization between Outlook and the native contacts app, users receive the rich experience that the native operating system provides (for example, inbound and outbound caller-ID, text messaging name resolution, and so on). Only Outlook for iOS should be used for managing contact data and not the native iOS Contacts app. With Outlook for Android, users can utilize either the native Contacts app or Outlook for managing contact data, as contact changes are synchronized bi-directionally.

Note

In order to manage contacts (add/edit/delete) in Outlook for Android, contact sync must be enabled. This is because Outlook for Android delegates CRUD operations to the native Contacts app.

Administrators have extra capabilities with respect to contact synchronization between Outlook and the native Contacts app:

- Administrators can disable contact synchronization via an Intune App Protection Policy. For more information, see [iOS app protection policy settings](/en-us/mem/intune/apps/app-protection-policy-settings-ios?form=MG0AV3) and [Android app protection policy settings in Microsoft Intune](/en-us/mem/intune/apps/app-protection-policy-settings-android?form=MG0AV3).
- Administrators can enable contact synchronization by default on enrolled devices. For more information, see [Deploying Outlook for iOS and Android app configuration settings](outlook-for-ios-and-android-configuration-with-microsoft-intune).
- Administrators can reduce the amount of data that is exported to the native Contacts app via an Intune App Protection Policy with contact field export controls. For more information, see [Deploying Outlook for iOS and Android app configuration settings](outlook-for-ios-and-android-configuration-with-microsoft-intune).

### Q: Is Outlook for iOS and Android available in China?

Yes, Outlook for iOS is available in Apple's App Store in China.

The Google Play Store isn't available in China. However, Microsoft has distributed the Outlook for Android app in the following third-party app stores that are available in China:

- [Baidu](http://shouji.baidu.com/software/11483186.html)
- [Xiaomi](http://app.mi.com/details?id=com.microsoft.office.outlook)
- [Tencent (QQ)](http://android.app.qq.com/myapp/detail.htm?apkName=com.microsoft.office.outlook)
- [OPPO](https://app.cdo.oppomobile.com/home/detail?app_id=2264914)
- [Vivo](https://h5coml.vivo.com.cn/h5coml/appdetail_h5/browser_v2/index.html?appId=87200)
- Huawei

As Google's notification service, Firebase Cloud Messaging, isn't available in China, new mail push notifications don't function. Instead, Outlook for Android relies on polling notifications. For the native Microsoft sync technology, background polling occurs every 15 minutes while the app is in the background (assuming background synchronization isn't disabled).

However, if you have installed Outlook for Android from the Xiaomi app store, Outlook for Android can use the Xiaomi push service for push notifications instead of polling.

## Native Microsoft sync technology migration

The following questions are about the migration from the REST API data sync protocol to the native Microsoft sync technology used by Outlook for iOS and Android for accessing mailbox data.

### Q: Is there a minimum version of Outlook for iOS and Android required to use the native Microsoft sync technology?

For Outlook for iOS, users should install 3.10.1 or later. For Outlook for Android, users should install 3.0.14 or later. As always, we recommend users keep the Outlook app up to date.

### Q: What do users experience when our tenant is migrated to the native Microsoft sync technology?

Assuming the user is running a supported version of Outlook for iOS and Android, after your tenant is migrated, your users might see a brief notice indicating that we're updating their email and calendar data. Otherwise, the user experience to migrate to the updated architecture is seamless.

### Q: As a tenant administrator, can I control which of my users are migrated to the native Microsoft sync technology?

No, the migration to the native Microsoft sync technology is on a tenant-by-tenant basis and not a per-user basis. While the tenant selection order for migration is random, we're being deliberate about migrating Microsoft 365 or Office 365 mailboxes first before we migrate on-premises mailbox accounts. If you're a customer operating in a hybrid configuration where a portion of your mailboxes remains on-premises, the on-premises users using [hybrid modern authentication](../../clients/outlook-for-ios-and-android/use-hybrid-modern-auth) are migrated to the native Microsoft sync technology at a later date. This system means that your Microsoft 365 and Office 365 users are migrated to the native Microsoft sync technology, while the on-premises users continue to use the REST API to connect to Exchange Online.

Once your tenant is migrated, a user doesn't switch to the native Microsoft sync technology until after they launch/resume Outlook for iOS and Android.

### Q: If my user doesn't upgrade to a supported build of Outlook for iOS and Android before the migration, does that mean the user loses access to email and calendar data while mobile?

No, the user can continue to connect using the existing REST-based data sync protocol.

### Q: Are my Intune App Protection Policies or Microsoft Entra Conditional Access policies affected by this migration?

No, both Intune App Protection Policies and Microsoft Entra Conditional Access policies continue to be applied to the targeted identity, regardless of the data sync protocol used by Outlook for iOS and Android.

### Q: Do I have to update my Exchange mobile device access policies (allow block quarantine (ABQ) rules)?

No, the user agent string that Outlook for iOS and Android uses doesn't change. For more information on what that user agent is, see [Securing Outlook for iOS and Android in Exchange Online](secure-outlook-for-ios-and-android).

### Q: As an Exchange administrator, is there a way for me to determine which data sync protocol Outlook for iOS and Android clients are utilizing in the Microsoft 365- or Office 365-based architecture?

Yes, execute the following command from Exchange Online PowerShell:

```PowerShell
Get-MobileDevice | where {$_.DeviceModel -eq "Outlook for iOS and Android"} | Format-List FriendlyName,DeviceID,DeviceOS,ClientType
```

The `ClientType` property indicates which data sync protocol is in use. If the value is REST, then the client is utilizing the REST API. If the value is Outlook, then the client is using the native Microsoft sync technology.

Alternatively, a user can sign in to Outlook on the web and, from within **Options**, select **Mobile Devices** to view the details of a mobile device. Like the cmdlet, the user can see the value for the `ClientType` property.

## Administrating and monitoring Outlook for iOS and Android in your organization

The following questions are about managing and monitoring the Outlook for iOS and Android app within your organization after the app has been deployed.

### Q: Is it necessary to file an in-app support ticket when I experience an issue with Outlook for iOS and Android?

Yes, if you want to troubleshoot and resolve the issue, or if you want to inform us of a product defect or limitation, you need to file an in-app support ticket. Only through filing an in-app support ticket are the Outlook app's logs collected and analyzed by our product engineers.

Customers with a Microsoft Premier agreement can open support cases with Customer Service & Support (CSS). Instead of having the user initiate an in-app support ticket, the user can use Collect Diagnostics to upload the logs and share the incident ID with CSS/Premier. Collect Diagnostics captures data from Outlook for iOS and Android, Authenticator, and the Company Portal and upload all the relevant logs to Microsoft. Microsoft Support Escalation Engineers can use the incident ID to access the diagnostic logs and troubleshoot the user's issue.

To gather the logs:

1. Within Outlook for iOS and Android's settings, tap Help & Feedback.
2. Tap Collect Diagnostics.
3. Tap Get Started.
4. Tap Upload Outlook Logs (iOS) or Collect Logs (Android).
5. Share the incident ID with CSS.

### Q: As an Exchange administrator, I would like to deploy Outlook for iOS and Android, but in my testing I can't sign in. What might be the issue?

Assuming authentication isn't the issue, there are two areas you can check:

1. Check whether you have an EWS application policy that restricts which client applications can connect.
2. Check whether you have EWS enabled for the account.

For more information, see [Securing Outlook for iOS and Android in Exchange Online](secure-outlook-for-ios-and-android). If one of the above checks doesn't resolve the issue, open an in-app support ticket.

### Q: Does Outlook for iOS and Android support third-party unified endpoint management (MDM, EMM, or UEM) solutions?

For more information, see [Managing Outlook for iOS and Android in Exchange Online](manage-outlook-for-ios-and-android).

### Q: Is a license required to use Outlook for iOS and Android?

Outlook for iOS and Android is free for consumer usage from the iOS App store and from Google Play. However, commercial users require an Office 365 or Microsoft 365 subscription that includes the Office desktop applications: Microsoft 365 Apps for Business, Microsoft 365 Business Standard, Microsoft 365 Apps for enterprise, Office 365 Enterprise E3, Office 365 Enterprise E5, or the corresponding versions of those plans for Government or Education. Commercial users with the following subscriptions are allowed to use the Outlook mobile app on devices with integrated screens 10.1" diagonally or less: Office 365 Enterprise E1, Office 365 F1, Office 365 A1, Microsoft 365 Business Basic, and if you only have an Exchange Online license (without Office). If you only have an Exchange on-premises (Exchange Server) license, you aren't licensed to use the app.

## Common questions from end users

The following questions concern end users in your organization who are using Outlook for iOS and Android on their devices to access their Exchange mailboxes.

### Q: My users enabled the "Save Contacts" advanced settings option. However, they are complaining that not all contacts have synchronized on their iOS devices. Are there limitations with synchronization?

The initial export of contacts can only begin when Outlook is in the foreground. A user can switch between apps and the export continues while Outlook is active in memory. There are iOS limitations when syncing with iCloud that might result in data inconsistency, but Outlook automatically triggers a reconciliation to ensure that the contacts are always consistently exported (for example, reconciliation removes duplicates if Outlook detects exported contacts from a previous export activity). Reasons for missing/duplicate contacts might include:

- Outlook for iOS being suspended during sync.
- Enabling "Save Contacts" simultaneously on multiple devices (such as an iPad and an iPhone).
- Accrued sync errors over time.

If you're seeing an inconsistency and it hasn't been resolved after a short period of time, wait for 24 hours and then restart the app to trigger the reconciliation process. If that doesn't work, perform the following steps:

1. Disable "Save Contacts" for the affected account.
2. Check that all instances of the contacts are removed from the native iOS contacts app. If duplicates remain, go to Settings &gt; Help & Feedback &gt; Delete All Saved Contacts in order to remove any lingering duplicates.
3. Re-enable "Save Contacts" for the affected account.
4. Follow the on-screen prompts, which might instruct you to keep the phone open and plugged in during initial sync.

### Q: Why are the Office mobile apps required to be installed on Android in order to render attachments in Outlook, while iOS devices provide a preview of the attachments within Outlook?

This requirement is due to the differences in the base operating systems. iOS provides native content rendering for known attachment types, which Outlook for iOS uses to provide basic attachment rendering. Android provides nothing similar. Android users have to install the Office apps and/or third-party apps in order to render attachment content.

### Q: A new message included an attachment, but while I was offline I couldn't open the attachment. Why is that?

Outlook (like other mobile clients) doesn't download attachments automatically. This behavior is by design, in order to conserve device space. Attachments are only downloaded at the request of the user.

### Q: A week ago I accessed an attachment in a message, but now that I'm offline I can no longer access that attachment on my iOS device. However, I can access it on my Android device. Why is that?

Outlook for iOS stores attachments in our own database. As a result, every attachment we download to the client takes up a considerable amount of space in our database. To ensure the client is able to provide fast performance and take a small amount of space, we purge data rather aggressively based on usage (attachments are cached for up to seven days).

Unlike iOS, Android uses an accessible file system, so when Outlook for Android downloads an attachment, it doesn't go into the database, rather it's stored as a temporary file.

### Q: Why does data within Outlook for iOS disappear and then reappear after I toggle the Focused Inbox or the Organize by Thread settings?

Whenever those options are changed, Outlook for iOS performs a soft reset. This operation wipes the existing data that has been downloaded to the app and requires a resynchronization.

### Q: Can I view organization chart information in Outlook for iOS?

Yes. Outlook for iOS provides your company's organization information as part of a person's contact card details. Your company's reporting structure and a list of colleagues is also provided, to help employees connect with the people and teams they need to work with.

The list of people displayed as part of the Other Colleagues list in the **Show Organization** is based on common email distribution lists, group memberships, and degrees of separation in the Organization structure defined in Microsoft Entra ID.

If you don't have organization chart data exposed in the app, consult with your directory administrator. There are two main scenarios to consider:

1. Your company has a hybrid topology where an on-premises directory is synchronized with Microsoft Entra ID. You need to update Active Directory with the organization chart information, either directly in the directory or via your Human Resources system. Data is synchronized into Microsoft Entra ID automatically and is accessible via the Global Address List in Exchange Online.
2. Your company only uses Microsoft Entra ID for directory management. You need to update Microsoft Entra ID with the organization chart information, either directly in the directory or via your Human Resources system. This data is accessible via the Global Address List in Exchange Online.

### Q: How much of my mailbox data is synchronized with Outlook for iOS and Android?

For initial folder synchronization, Outlook for iOS and Android synchronizes 500 items per folder, with up to 1,000 items per folder if the user taps **Load more conversations**. The app periodically trims the items per folder down to the default number, in order to ensure optimal app performance.

### Q: Why are tasks and notes not available with Outlook for iOS and Android?

Microsoft's strategic direction for task management and note taking on mobile devices is the To-Do and OneNote apps, respectively. OneNote provides access to notes stored in an Exchange Online mailbox with Sticky Notes. To-Do provides integration with the tasks stored in Exchange Online mailboxes; however, Outlook for iOS and Android provides users the ability to create tasks from messages and exposes top tasks in the Zero Query search pane.

### Q: Does Outlook for iOS and Android support moderator message approval or rejection scenarios?

No, Outlook for iOS and Android doesn't support moderated message requests for approving or rejecting email. Outlook for iOS and Android doesn't provide an **approve/reject** button, so a moderator can't approve or reject moderated messages when using Outlook for iOS and Android.