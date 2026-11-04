---
layout: Conceptual
title: Deploying Outlook for iOS and Android app configuration settings in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune
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
description: How to customize the behavior of Outlook for iOS and Android in your Exchange organization.
ms.topic: install-set-up-deploy
author: AshaIyengar21
ms.author: serdars
ms.assetid: e8a034f6-39b8-4dea-a3bc-9421aaa75d1d
ms.collection:
- exchange-online
- M365-email-calendar
ms.reviewer: smithre4
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2026-05-27T00:00:00.0000000Z
locale: en-us
document_id: 76073a9f-750e-fe8d-cc6b-e74a76e82f5b
document_version_independent_id: 5857e1e1-0d71-b005-98c2-ab99d4609200
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/80beb97b-18aa-44f8-9420-8f2a4cd448eb
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/8c09e0ef-0fde-4b6d-bf1b-b517e4db7f80
platformId: 69d6c355-30ff-e76a-f620-29b868641d6c
---

# Deploying Outlook for iOS and Android app configuration settings in Exchange Online | Microsoft Learn

**Summary**: How to customize the behavior of Outlook for iOS and Android in your Exchange organization.

Outlook for iOS and Android supports app settings that allow unified endpoint management (UEM) administrators (using tools such as Microsoft Intune) and Microsoft 365 or Office 365 administrators to customize the behavior of the app.

App configuration can be delivered either through the mobile device management OS channel on enrolled devices [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android or through the Intune App Protection Policy (APP) channel. Outlook for iOS and Android supports the following configuration scenarios:

- Account setup configuration
- Organization allowed accounts mode
- General app configuration settings
- S/MIME settings
- Data protection settings

Important

For configuration scenarios that require device enrollment on Android, the devices must be enrolled in Android Enterprise, and Outlook for Android must be deployed via the managed Google Play store. For more information, see [Set up enrollment of Android work profile devices](/en-us/mem/intune/enrollment/android-work-profile-enroll?form=MG0AV3) and [Add app configuration policies for managed Android devices](/en-us/mem/intune/apps/app-configuration-policies-use-android?form=MG0AV3).

Each configuration scenario highlights its specific requirements for example, whether the configuration scenario requires device enrollment, and thus works with any UEM provider, or requires Intune App Protection Policies. The following flowchart outlines which channel needs to be used for the above configuration scenarios:

Note

With Microsoft Intune, app configuration delivered through the mobile device management OS channel is referred to as a **Managed Devices** App Configuration Policy (ACP); app configuration delivered through the App Protection Policy (APP) channel is referred to as a **Managed Apps** App Configuration Policy.

![Flowchart of the process.](../../exchangeonline/media/acp-flowchart-v2.png)

## Account configuration scenarios

Outlook for iOS and Android offers administrators the following app configuration scenarios with enrolled devices:

- Account setup configuration
- Organization allowed accounts mode

These configuration scenarios only work with enrolled devices. However, any UEM provider is supported. If you aren't using Microsoft Intune, you need to refer your UEM documentation on how to deploy these settings. For more information on the configuration keys, see Configuration keys.

### Account setup configuration scenario

Outlook for iOS and Android offers administrators the ability to "push" account configurations to their Office 365 and on-premises users leveraging hybrid Modern Authentication users. For more information on account setup configuration, see [Account setup with modern authentication in Exchange Online](setup-with-modern-authentication#account-setup-configuration-via-enterprise-mobility-management).

### Organization allowed accounts mode scenario

Outlook for iOS and Android offers administrators the ability to restrict email and storage provider accounts to only corporate accounts. For more information on organization allowed accounts mode, see [Account setup with modern authentication in Exchange Online](setup-with-modern-authentication#organization-allowed-accounts-mode).

## General app configuration scenarios

Outlook for iOS and Android offers administrators the ability to customize the default configuration for several in-app settings. This capability is offered for both enrolled devices via any UEM provider and for devices that aren't enrolled when Outlook for iOS and Android has an Intune App Protection Policy applied.

Note

If an App Protection Policy is targeted to the users, the recommendation is to deploy the general app configuration settings in a **Managed Apps** device enrollment model. This deployment ensures the App Configuration Policy is deployed to both enrolled devices and unenrolled devices.

Outlook supports the following settings for configuration:

| Setting | Default app behavior | Notes | Recommended configuration |
| --- | --- | --- | --- |
| Open Links in Edge | On | Users will be prompted to open links in Edge. Admins now have the option to disable this feature for their company. | App Default |
| Focused Inbox | On | Focused Inbox separates your inbox into two tabs, **Focused** and **Other**. Your most important emails are on the **Focused** tab while the rest remains easily accessible (but out of the way) on the **Other** tab. | App default |
| Require Biometrics to access the app | Off | Biometrics, such as TouchID or FaceID, can be required for users to access the app on their device. When required, biometrics is used in addition to the authentication method selected in this profile. <br> This setting is only available for Outlook for iOS. <br><br> If using App Protection Policies, Microsoft recommends disabling this setting to prevent dual access prompts. | Disable |
| Save (or Sync) Contacts | Off | Saving contacts to the mobile device's native address book allows new calls and text messages to be linked with the user's existing Outlook contacts. <br> The user must grant access to the native Contacts app for contact synchronization to occur. | Enable |
| Sync Calendars | Off | Outlook for Android provides users the ability to synchronize Outlook calendar data with the native Calendar app. <br> The user must grant access to the native Calendar app for calendar synchronization to occur. <br><br> This feature is only supported with Outlook for Android. | App default |
| External Recipients MailTip | On | If the sender adds a recipient that's external or adds a distribution group that contains external recipients, the External Recipients MailTip is displayed. This MailTip informs senders if a message they're composing will leave the organization, helping them make the correct decisions about wording, tone, and content. <br> Exchange Online MailTipsExternalRecipientsTipsEnabled parameter must be set to $true for Outlook for iOS and Android to see the External Recipients MailTip. For more information, see [MailTips](/en-us/exchange/clients-and-mobile-in-exchange-online/mailtips/mailtips). <br><br> In Outlook for iOS and Android, to set all the internal domains for use when the MailTip service for external recipients is unavailable (as user is offline or due to low connectivity), see External recipients MailTip offline domain configuration. | App default |
| Block external images | Load for Safe Senders only (value 1) | When **Block external images** (BlockExternalImagesSetting) is set to 1(default), the app prevents the download of images hosted on the Internet unless the sender is internal or has been added to the user's Safe Senders list. (The user can still choose to download the images from within each message). | Enable Only for Safe Senders (value 1) |
| Default app signature | On | Indicates whether the app uses its default signature, "Get Outlook for [OS]", during message composition, if a custom signature isn't defined. Users can add their own signatures even when the default signature is disabled. | App default |
| Suggested replies | On | By default, Outlook for iOS and Android suggests replies in the **quick reply compose** window. If you select a suggested reply, you can edit the reply before sending it. | App default |
| Organize mail by thread | On | By default, Outlook for iOS and Android collates related emails into a single threaded conversation view. | App default |
| Play My Emails | On | By default, Play My Emails is promoted to eligible users via a banner in the inbox. | App default |
| Text Predictions | On | By default, Outlook for iOS and Android can suggest words and phrases as you compose messages. | App default |
| Themes | On | By default, Outlook for iOS and Android supports visual themes that can be enabled for certain beliefs or events. | App default |
| Louder Mandatory labeling | Off | Organizations have mandatory labeling enabled without default labeling, and would like to have the label selection first before going to compose the email. Then when the users select **Send**, the email could just be sent without any forgotten labeling pop ups. Outlook mobile will introduce a new MDM setting (com.microsoft.outlook.Mail.LouderMandatoryLabelEnabled) to allow admins to enable this louder mandatory configuration for Outlook mobile clients (iOS and Android) specifically. | App default |
| Default Font | Off | Default font ensures that users have the default font and size that is standard for your organization. When configured, this updates the default font for both the reading pane and for composing. Users can still change the font from the default while composing. | App default |

Settings that are security-related in nature have an additional option, **Allow user to change setting**. For these settings (*Save Contacts*, *Block external images*, and *Require Biometrics to access the app*), organizations can prevent the user from changing the app's configuration. The organization's configuration can't be overridden.

**Allow user to change setting** doesn't change the app's behavior. For example, if the admin enables *Block external images* and prevents a user change, then by default, external images aren't downloaded in messages; however, the user can manually download the images for that message body.

The following conditions describe Outlook's behavior when implementing various app configurations:

- If the admin configures a setting with its default value, and the app is configured with the default value, then the admin's configuration doesn't have any effect. For example, if the admin sets *External recipients MailTip*=on, the default value is also **on**, so Outlook's configuration doesn't change.
- If the admin configures a setting with the non-default value and the app is configured with the default value, then the admin's configuration is applied. For example, the admin sets *Focused Inbox*=off, but app default value is **on**, so Outlook's configuration for Focused Inbox is **off**.
- If the user has configured a non-default value, but the admin has configured a default value and allows user choice, then Outlook retains the user's configured value. For example, the user has enabled contact synchronization, but the admin sets *Save Contacts*=off and allows user choice, so Outlook keeps contact synchronization on and doesn't break caller-ID for user.
- If the admin disables user choice, Outlook always enforces the admin-defined configuration, regardless of the user's configuration or default app configuration. For example, the user has enabled contact synchronization, but the admin sets *Save Contacts*=off and disables user choice, so contact synchronization gets disabled and the user is prevented from enabling it.
- After the app configuration is applied, if the user changes the setting value to not match the admin desired value (and user choice is allowed), then the user's configuration is retained. For example, **Block external images** is **off** by default, admin set *Block external images*=on, but afterwards, user changes **Block external images** back to **off**. In this scenario, **Block external images** remains **off** the next time the policy is applied.

Users are alerted to configuration changes via a notification toast in the app:

![Notification toast in the app.](../../exchangeonline/media/outlook_mobile_intune_1.png)

This notification toast will automatically dismiss after 10 seconds. There are two scenarios where this notification toast won't appear:

- If the app has previously shown the notification in the last hour.
- If the app has been installed in less than 24 hours.

### External recipients MailTip offline domain configuration

In Outlook for iOS and Android, when the MailTip service is unavailable for external recipients as the user is offline or due to low connectivity, use the following MDM app configuration to set all the internal domains of the tenant:

- Key: `com.microsoft.outlook.Mail.InternalDomains`.
- Value:
    1. A list of domains split by a comma (`,`) in string type.
    2. You only need to add all your root domains. For example, if you have `microsoft.com` domain in your config, `service.microsoft.com`, `exchange.microsoft.com`, and `hr.service.microsoft.com` are all considered as internal recipients.
    3. All domains aren't case sensitive.
- Config example: `microsoft.com, contoso.onmicrosoft.com, hcdhc.net`

Note

1. For **UOPCC accounts**, the external recipient MailTips are enabled only when the internal domains MDM configuration is set (even if the value is empty).
2. If empty string is set in the app configuration, the recipient is still considered as an internal recipient when its domain is same as the sender's domain, or it's a sub-domain of the sender's domain.

### Save Contacts

The *Save Contacts* setting is a special case scenario because unlike the other settings, this setting requires user interaction: the user needs to grant Outlook permissions to access the native Contacts app and the data stored within. If the user doesn't grant access, then contact synchronization can't be enabled.

Note

With Android Enterprise, administrators can configure the default permissions assigned to the managed app. Within the policy, you can define that Outlook for Android is granted READ\_CONTACTS and WRITE\_CONTACTS within the work profile; for more information on how to assign permissions, see [Add app configuration policies for managed Android devices](/en-us/mem/intune/apps/app-configuration-policies-use-android?form=MG0AV3). When assigning default permissions, it's important to understand which [Android Enterprise deployment models](/en-us/mem/intune/fundamentals/deployment-guide-platform-android?form=MG0AV3) are in use, as the permissions may grant access to personal data.

When enabling Outlook for Android's Save Contacts within Android Enterprise's work profile, Outlook for Android is limited in only being able to access the native Contacts app within the work profile context; this limitation in accessibility provides a clear separation between work and personal profile data. However, Android Enterprise allows for the dialer and messaging apps within the personal profile to access the local contacts within the work profile. This behavior is enabled by default, but can be controlled via device restrictions; for more information, see [Android Enterprise device settings to allow or restrict features using Intune](/en-us/mem/intune/configuration/device-restrictions-android-for-work). It's possible that some dialer or messaging apps, whether pre-installed by the device manufacturer or installed from the Play Store, don't properly support this capability.

The workflow for enabling Save Contacts is the same for new accounts and existing accounts.

1. The user is notified that the administrator has enabled contact synchronization. In Outlook for iOS, the notification occurs within the app, whereas in Outlook for Android, a persistent notification is delivered via the Android notification center.

![Contact sync notification.](../../exchangeonline/media/outlook_mobile_intune_2.png)
2. If the user taps on the notification, the user is prompted to grant access:

![User is prompted for access to contacts.](../../exchangeonline/media/outlook_mobile_intune_3.png)
3. If the user allows Outlook to access the native Contacts app, access is granted, and contact synchronization is enabled. If the user denies Outlook access to the native Contacts app, then the user is prompted to go into the OS settings and enable contact synchronization:

![User is prompted to allow Outlook to access the native Contacts app.](../../exchangeonline/media/outlook_mobile_intune_4.png)
4. In the event the user denies Outlook access to the native Contacts app and dismisses the previous prompt, the user may later enable access by navigating to the account configuration within Outlook and tapping **Open Settings**:

![Outlook account settings.](../../exchangeonline/media/outlook_mobile_intune_5.png)

### Calendar Sync

Note

Calendar sync support will begin rolling out in October 2020.

Calendar sync enables users to synchronize their Outlook for Android calendar data with the native Android Calendar app. Calendar sync is **off** by default and requires user participation.

Like *Save Contacts*, the *Sync Calendars* setting is another special case scenario because this setting requires user interaction: the user needs to grant Outlook permissions to access the native Calendar app and the data stored within. If the user doesn't grant access, then calendar synchronization can't be enabled.

Note

With Android Enterprise, administrators can configure the default permissions assigned to the managed app. Within the policy, you can define that Outlook for Android is granted READ\_CALENDAR and WRITE\_CALENDAR within the work profile; for more information on how to assign permissions, see [Add app configuration policies for managed Android devices](/en-us/mem/intune/apps/app-configuration-policies-use-android?form=MG0AV3). When assigning default permissions, it's important to understand which [Android Enterprise deployment models](https://developers.google.com/android/work/overview) are in use, as the permissions may grant access to personal data. 

 When enabling Outlook for Android's Sync Calendar within Android Enterprise's work profile, Outlook for Android is limited in only being able to access the native Calendar app within the work profile context; this limitation in accessibility provides a clear separation between work and personal profile data.

## S/MIME scenarios

On enrolled devices, Outlook for iOS and Android supports automated certificate delivery. Outlook for iOS and Android also supports app configuration settings that enable or disable S/MIME in the app, as well as the user's ability to change the setting. For more information on how to deploy these settings via Microsoft Intune, see [Understanding S/MIME](sensitive-labeling-and-protection-outlook-for-ios-android#understanding-smime). For more information on the configuration keys, see Configuration keys.

## Data protection scenarios

Outlook for iOS and Android supports app configuration policies for the following data protection settings when the app is managed by Microsoft Intune with an Intune App Protection Policy applied:

- Managing the use of wearable technology
- Managing sensitive data in mail and calendar reminder notifications
- Managing the contact fields synchronized to the native contacts app
- Managing calendar sync availability
- Managing add-ins availability

These settings can be deployed to the app regardless of device enrollment status. For more information on the configuration keys, see Configuration keys.

### Configure Wearables for Outlook for iOS and Android

By default, Outlook for iOS and Android supports wearable technology, allowing the user to receive message notifications and event reminders, and the ability to interact with messages and view daily calendars. Organizations that want to disable the ability to access corporate data on wearables can block wearables with an App Configuration Policy.

### Configure Notifications for Outlook for iOS and Android

Mobile app notifications are critical in alerting users of new content or reminding them to act. Users interact with these notifications via the lock screen and in the operating system's notification center. Notifications often include detailed information, which can be sensitive in nature. This information, unfortunately, can inadvertently be leaked to casual observers.

Outlook for iOS and Android has designed its notifications to enable users to triage email and alert users to upcoming meetings, including incorporating Time to Leave suggestions. Mail notifications include the sender's address, the subject of the message, and a short message preview of the message body. Calendar reminders include the subject, location, and start time of the meeting.

Recognizing that these notifications may include sensitive data, organizations can use an Intune App Protection Policy setting, **Org Data Notifications** to remove the sensitive data. As this is an App Protection Policy setting, it applies on all devices (phones, tablets, and wearables) of the user for the apps that support the setting. For more information on the setting, see [iOS App Protection Policy settings](/en-us/mem/intune/apps/app-protection-policy-settings-ios?form=MG0AV3) and [Android App Protection Policy settings](/en-us/mem/intune/apps/app-protection-policy-settings-android?form=MG0AV3).

In addition to the App Protection Policy setting, Outlook for iOS and Android has a data protection App Configuration Policy setting, **Calendar Notifications** that provides additional flexibility with calendar notifications – organizations can block sensitive information in mail notifications, while allowing sensitive information in calendar notifications. After all, users might just need to know where they're going and when they should leave, at a glance.

The following table outlines the notification experience in Outlook for iOS and Android based on the combination of the App Protection and App Configuration policy settings:

| Org Data Notifications value | Calendar Notifications value | Notification behavior |
| --- | --- | --- |
| Allow (default) | Not Configured (default) | Default client behavior where sensitive data is exposed in mail and calendar notifications |
| Block | Not Configured | Sensitive data is exposed in mail and calendar notifications as Outlook ignores the block setting |
| Block Org Data | Not Configured | Sensitive data isn't available in mail or calendar notifications |
| Block Org Data | Allowed | Sensitive data isn't available in mail notifications <br> Calendar notifications expose sensitive data |

### Configure Contact Field Sync to native Contacts for Outlook for iOS and Android

The settings allow organizations to control the contact fields that synchronize between Outlook on iOS and Android and the native Contacts apps.

Note

Outlook for Android supports bi-directional contact synchronization. However, if a user edits a field in the native contacts app that is restricted (such as the **Notes** field), then that data won't synchronize back into Outlook for Android.

### Configure Calendar Sync availability with Outlook for Android

Calendar sync enables users to synchronize their Outlook for Android calendar data with the native Android Calendar app. Organizations can control whether calendar sync is available to the work or school account with the following methods:

- With Intune App Protection Policies, the setting **Sync policy managed app data with native apps or add-ins** defines whether *Save Contacts*, *Sync Calendars*, and *Add-ins* are available for use within the work or school account. By default, this setting is set to **Allow**. If this setting is set to **Block**, *Save Contacts*, *Sync Calendars*, and *Add-ins* are disabled for the work or school account and their associated App Configuration Policy settings are ignored.
- When the Intune App Protection Policy setting **Sync policy managed app data with native apps or add-ins** is set to **Allow**, organizations can also choose to define the availability of *Sync Calendars* through a managed apps App Configuration Policy. This flexibility allows for feature granularity control from a data protection perspective; for example, organizations can enable *Save Contacts* (by setting **Sync policy managed app data with native apps or add-ins** to **Allow**) but disable *Sync Calendars* (by setting the **Allow Calendar Sync** setting within a managed apps App Configuration Policy to **Off**).
- Finally, if organizations allow the availability of *Sync Calendars*, through an App Configuration Policy setting **Sync Calendars**, organizations can define the default sync state of calendar sync. This setting removes the need for the user to enable calendar synchronization manually.

### Configure Add-ins availability with Outlook for iOS and Android

Users can synchronize work or school account data into other services using add-ins. The availability of add-ins within the work or school account can be controlled with the following methods:

- With Intune App Protection Policies, the setting **Sync policy managed app data with native apps or add-ins** defines whether *Save Contacts*, *Sync Calendars*, and *Add-ins* are available for use within the work or school account. By default, this setting is set to **Allow**. If this setting is set to **Block**, *Save Contacts*, *Sync Calendars*, and *Add-ins* are disabled for the work or school account and their associated App Configuration Policy settings are ignored.
- When the Intune App Protection Policy setting **Sync policy managed app data with native apps or add-ins** is set to **Allow**, organizations can also choose to define the availability of *Add-ins* through a managed apps App Configuration Policy. This flexibility allows for feature granularity control from a data protection perspective; for example, organizations can enable *Save Contacts* (by setting **Sync policy managed app data with native apps** to **Allow**) but disable *Add-ins* (by setting the **Allow Add-ins** setting within a managed apps App Configuration Policy to **Off**).

Important

When configuring add-ins for your users, issues can occur when add-in policies are set in both Microsoft Intune and the Microsoft 365 Admin Center. We recommend choosing between add-in policy in Microsoft Intune or the Microsoft 365 Admin Center but not both at the same time. For granular add-in control, the Microsoft 365 Admin Center provides more specific configurations than Microsoft Intune, so you can choose which solution best fits your organization needs.

## Deploying configuration scenarios with Microsoft Intune for enrolled devices

Microsoft Intune enables administrators to easily deploy these settings to Outlook for iOS and Android via App Configuration Policies.

The following steps allow you to create an app configuration policy. After the configuration policy is created, you can assign its settings to groups of users.

Note

Intune notifies the enrolled device to check in with the Intune service for policy changes. The notification times vary, including immediately up to a few hours. For more information, see [Common questions, issues, and resolutions with device policies and profiles in Microsoft Intune](/en-us/mem/intune/configuration/device-profile-troubleshoot?form=MG0AV3).

Important

When deploying app configuration policies to managed devices, issues can occur when multiple policies have different values for the same configuration key and are targeted for the same app and user. These issues are due to the lack of a conflict resolution mechanism for resolving the differing values. You can prevent these issues by ensuring that only a single app configuration policy for managed devices is defined and targeted for the same app and user.

### Create a managed devices app configuration policy for Outlook for iOS and Android

1. Log in to [Microsoft Intune admin center](https://endpoint.microsoft.com).
2. Select **Apps** and then select **App configuration policies**.
3. On the **App Configuration policies** blade, choose **Add** and select **Managed devices** to start the app configuration policy creation flow.
4. On the **Basics** section, enter a **Name**, and optional **Description**, for the app configuration settings.
5. For **Platform**, choose either **iOS/iPadOS** or **Android Enterprise**.
6. If Android Enterprise is selected as the platform, for **Profile Type**, choose **All Profile Types**.
7. For **Targeted app**, choose **Select app**, and then, on the **Associated app** blade, choose **Microsoft Outlook**. Select **OK**.

    Note

    If Outlook isn't listed as an available app, then you must add it by following the instructions in [Assign apps to Android work profile devices with Intune](/en-us/mem/intune/apps/apps-add-android-for-work?form=MG0AV3) and [Add iOS store apps to Microsoft Intune](/en-us/mem/intune/apps/store-apps-ios?form=MG0AV3).
8. Select **Next** to complete the basic settings of the app configuration policy.
9. On the **Settings** section, select **Use configuration designer** for the **Configuration settings format**.
10. If you want to deploy account setup configuration, select **Yes** for **Configure email account** **settings** and configure appropriately:

    Note

    If an App Protection Policy is targeted to the users, the recommendation is to deploy the general app configuration settings in a **Managed Apps** device enrollment model instead of using **Managed devices**. This method ensures the App Configuration Policy is deployed to both enrolled devices and unenrolled devices.

    - For **Authentication type**, select **Modern authentication**. This setting is required for Microsoft 365 or Office 365 accounts or on-premises accounts using hybrid modern authentication.
    - For **Username attribute from Microsoft Entra ID**, select **User Principal Name**.
    - For **Email address attribute from Microsoft Entra ID**, select **Primary SMTP Address**.
    - If you want to configure Outlook for iOS and Android such that only the work or school account can be used, select **Require** for **Allow only work or** **school** **accounts**. This configuration will only allow a single corporate account to be added to Outlook for iOS and Android.
11. If you want to deploy general app configuration settings, configure the desired settings accordingly:

    - For **Focused Inbox**, choose from the available options: **Not configured** (default), **On** (app default), and **Off**.
    - For **Require Biometrics to access the app**, choose from the available options: **Not configured** (default), **On**, and **Off** (app default). When selecting **On** or **Off**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value. This setting is only available in Outlook for iOS.

        Important

        If the account is protected by an Intune App Protection Policy that requires a PIN to access the protected account, then the **Require Biometrics to access the app** setting should be disabled, otherwise the user is prompted with multiple authentication prompts when accessing the app.
    - For **Save Contacts**, choose from the available options: **Not configured** (default), **On**, and **Off** (app default). When selecting **On** or **Off**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value.
    - For **Suggested Replies**, choose from the available options: **Not configured** (default), **On** (app default), and **Off**. When selecting **On** or **Off**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value.
    - For **External recipients MailTip**, choose from the available options: **Not configured** (default), **On** (app default), and **Off**.
    - For **Default app signature**, choose from the available options: **Not configured** (default), **On** (app default), and **Off**.
    - For the **Block external images setting**, choose from the available three options: **Not configured** (default), **0** for Always Block, **1** for Load for Safe Senders (app default), and **2** for Always Load. When selecting any value, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value. Note that the legacy boolean setting BlockExternalImages is still supported when configured. See the table below for key value details.
    - For **Organize mail by thread**, choose from the available options: **Not configured** (default), **On** (app default), and **Off**.
    - For **Play My Emails**, choose from the available options: **Not configured** (default), **On** (app default), and **Off**.
    - For **Themes**, choose from the available options: **Not configured** (default), **On** (app default), and **Off**.
    - For **Sync Calendars**, choose from the available options: **Not configured** (default), **On** (app default), and **Off**. When selecting **On** or **Off**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value. This feature is only available in Outlook for Android.
    - For **Text Predictions**, choose from the available options: **Not configured** (default), **On** (app default), and **Off**. When selecting **On** or **Off**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value.
12. If you want to configure S/MIME settings, see [Outlook for iOS automated certificate delivery](smime-outlook-for-ios-and-android#outlook-for-ios-automated-certificate-delivery) or [Outlook for Android automated certificate delivery](smime-outlook-for-ios-and-android#outlook-for-android-automated-certificate-delivery).
13. When you're finished selecting settings, select **Next**.
14. On the **Assignments** section, select **Select groups to include**. Select the Microsoft Entra group to which you want to assign the app configuration policy, and then select **Select**.
15. When you're finished with assignments, select **Next**.
16. On the **Review + Create** section, review the settings configured and select **Create**.

The newly created configuration policy is displayed on the **App configuration** blade.

Note

For **Managed devices**, you'll need to create a separate app configuration policy for each platform. Also, Outlook will need to be installed from the Company Portal for the configuration settings to take effect.

## Deploying configuration scenarios with Microsoft Intune for unenrolled devices

If you're using Microsoft Intune as your mobile app management provider, the following steps allow you to create a managed apps app configuration policy. After the configuration is created, you can assign its settings to groups of users.

Note

Microsoft Intune managed apps will check-in with an interval of 30 minutes for Intune App Configuration Policy status, when deployed in conjunction with an Intune App Protection Policy. If an Intune App Protection Policy isn't assigned to the user, then the Intune App Configuration Policy check-in interval is set to 720 minutes.

### Create a managed apps app configuration policy for Outlook for iOS and Android

1. Log in to [Microsoft Intune admin center](https://endpoint.microsoft.com).
2. Select **Apps** and then select **App configuration policies**.
3. On the **App Configuration policies** blade, choose **Add** and select **Managed apps**.
4. On the **Basics** section, enter a **Name**, and optional **Description**, for the app configuration settings.
5. For **Public apps**, choose **Select public apps**, and then, on the **Targeted apps** blade, choose **Outlook** by selecting both the iOS and Android platform apps. Click **Select** to save the selected public apps.
6. Click **Next** to complete the basic settings of the app configuration policy.
7. On the **Settings** section, expand the **Outlook configuration settings**.
8. If you want to deploy general app configuration settings, configure the desired settings accordingly:

    - For **Focused Inbox**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**.
    - For **Require Biometrics to access the app**, choose from the available options: **Not configured** (default), **Yes**, and **No** (app default). When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value. This setting is only available in Outlook for iOS.

        Important

        If the account is protected by an Intune App Protection Policy that requires a PIN to access the protected account, then the **Require Biometrics to access the app** setting should be disabled, otherwise the user is prompted with multiple authentication prompts when accessing the app.
    - For **Save Contacts**, choose from the available options: **Not configured** (default), **Yes**, and **No** (app default). When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value.
    - For **External recipients MailTip**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**.
    - For the **Block external images setting**, choose from the available three options: **Not configured** (default), **0** for Always Block, **1** for Load for Safe Senders (app default), and **2** for Always Load. When selecting any value, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value. Note that the legacy boolean setting BlockExternalImages is still supported when configured. See the table below for key value details.
    - For **Default app signature**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**.
    - For **Suggested Replies**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value.
    - For **Organize mail by thread**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**.
    - For **Play My Emails**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**.
    - For **Sync Calendars**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value. This feature is available only in Outlook for Android.
    - For **Text Predictions**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value.
9. If you want to manage the data protection settings, configure the desired settings accordingly:

    - For **Org data on wearables**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**.
    - For **Calendar Notifications**, choose from the available options: **Not configured** (default) and **Allowed**. By default, calendar notifications are allowed within the app and display sensitive information. **Allowed** only takes effect when the App Protection Policy setting **Org Data Notifications** is set to **Block org data**.
    - For **Allow Add-ins**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**. For more information on the setting choices, see Add-ins.
    - For **Allow Calendar Sync**, choose from the available options: **Not configured** (default), **Yes** (app default), and **No**. For more information on the setting choices, see Calendar Sync.
    - If you want to manage which contact fields sync with the native contacts apps, configure the desired **Sync contact fields to native contacts app configuration** settings accordingly. For each contact field setting, choose from the available options: **Not configured** (default), **Yes** (app default), **No**.
10. If you want to manage the app's S/MIME configuration, configure the desired settings accordingly:

    - For **Enable S/MIME**, choose from the available options: **Not configured** (default), **Yes**, and **No** (app default). When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value.

    Important

    S/MIME certificates must be available within Outlook for iOS and Android for the user sign or encrypt messages. For more information, see [S/MIME for Outlook for iOS and Android](smime-outlook-for-ios-and-android).

    - Choose whether to **Encrypt all emails** by selecting **Yes** or **No**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value.
    - Choose whether to **Sign all emails** by selecting **Yes** or **No**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or select **No** if you want to prevent the user from changing the setting's value.
    - If needed, deploy a **LDAP URL** for recipient certificate lookup. For more information on the URL format, see [LDAP support for certificate lookup](smime-outlook-for-ios-and-android#ldap-support-for-certificate-lookup).
11. When you're finished configuring the settings, select **Next**.
12. On the **Assignments** section, choose **Select groups to include**. Select the Microsoft Entra group to which you want to assign the app configuration policy, and then select **Select**.
13. When you're finished with the assignments, select **Next**.
14. On the **Create app configuration policy Review + Create** blade, review the settings configured and select **Create**.

The newly created configuration policy is displayed on the **App configuration** blade.

## Configuration keys

The following sections outline the app configuration keys and their supported values. Configuration keys identified with the **Managed apps** device enrollment type are delivered through the App Protection Policy channel. Configuration keys identified with the **Managed devices** device enrollment type are delivered through the mobile device management OS channel. If a configuration key is listed with both device enrollment types, the key can be delivered through either channel; for more information, see General app configuration scenarios.

Important

App configuration keys are case sensitive. Use the proper casing to ensure the configuration takes effect.

### iOS devices and third-party unified endpoint management solutions

If the **Managed devices** device enrollment type configuration keys are deployed with a third-party UEM provider, then the following additional key must also be delivered for iOS devices:

**key** = IntuneMAMUPN, **value** = username@company.com

The exact syntax of the key/value pair may differ based on the third-party UEM provider used. The following table shows examples of some third-party UEM providers and the exact values for the key/value pair:

| Third-party UEM provider | Configuration Key | Value Type | Configuration Value |
| --- | --- | --- | --- |
| Microsoft Intune | IntuneMAMUPN | String | {{UserPrincipalName}} |
| Workspace ONE | IntuneMAMUPN | String | {UserPrincipalName} |
| MobileIron | IntuneMAMUPN | String | ${userUPN} **or** ${userEmailAddress} |
| Citrix Endpoint Management | IntuneMAMUPN | String | ${user.userprincipalname} |
| ManageEngine Mobile Device Manager | IntuneMAMUPN | String | %upn% |

### Account setup configuration

Outlook for iOS and Android offers administrators the ability to "push" account configurations to their Microsoft 365 and Office 365 users. For more information on account setup configuration, see [Account setup with modern authentication in Exchange Online](setup-with-modern-authentication#account-setup-configuration-via-enterprise-mobility-management).

| Key | Value | Device Enrollment Type |
| --- | --- | --- |
| com.microsoft.outlook.Settings.OpenLinks.UseSystemDefaultBrowser | This new app config policy disables Open Links feature and always uses system default browser. | Managed devices |
| com.microsoft.outlook.Settings.OpenLinks.UserChangeAllowed | This new app config policy hides settings page for Open Links. | Managed devices |
| com.microsoft.outlook.EmailProfile.EmailAddress | This key specifies the email address to be used for sending and receiving mail. <br>**Value type**: String <br><br>**Accepted values**: Email address <br><br>**Default if not specified**: &lt;blank&gt; <br><br>**Required**: Yes <br><br>**Example**: user@companyname.com | Managed devices |
| com.microsoft.outlook.EmailProfile.EmailUPN | This key specifies the User Principal Name or username for the email profile that is used to authenticate the account. <br>**Value type**: String <br><br>**Accepted values**: UPN Address or username <br><br>**Default if not specified**: &lt;blank&gt; <br><br>**Required**: Yes <br><br>**Example**: userupn@companyname.com | Managed devices |
| com.microsoft.outlook.EmailProfile.AccountType | This key specifies the account type being configured based on the authentication model. <br>**Value type**: String <br><br>**Accepted values**: ModernAuth <br><br>**Required**: Yes <br><br>**Example**: ModernAuth | Managed devices |

### Organization allowed accounts mode settings

Outlook for iOS and Android offers administrators the ability to restrict email and storage provider accounts to only corporate accounts. For more information on organization allowed accounts mode, see [Account setup with modern authentication in Exchange Online](setup-with-modern-authentication#organization-allowed-accounts-mode).

| Key | Value | Platform | Device Enrollment Type |
| --- | --- | --- | --- |
| IntuneMAMAllowedAccountsOnly | This key specifies whether organization allowed account mode is active. <br>**Value type**: String <br><br>**Accepted values**: Enabled, Disabled <br><br>**Required**: Yes <br><br>**Value**: Enabled | iOS | Managed devices |
| IntuneMAMUPN | This key specifies the User Principal Name for the account. <br>**Value type**: String <br><br>**Accepted values**: UPN Address <br><br>**Required**: Yes <br><br>**Example**: userupn@companyname.com | iOS | Managed devices |
| com.microsoft.intune.mam.AllowedAccountUPNs | This key specifies the UPNs allowed for organization allowed account mode. <br>**Accepted values**: UPN Address <br><br>**Required**: Yes <br><br>**Example**: userupn@companyname.com | Android | Managed devices |

### General app configuration settings

Outlook for iOS and Android offers administrators the ability to customize the default configuration for several in-app settings.

| Key | Value | Device Enrollment Type |
| --- | --- | --- |
| com.microsoft.outlook.Mail.FocusedInbox | This key specifies whether **Focused Inbox** is enabled. Setting the value to *false* will disable **Focused Inbox**. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Auth.Biometric | This key specifies whether FaceID or TouchID is required to access the app. Setting the value to *true* will enable biometric access. This key is only supported with Outlook for iOS.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Auth.Biometric.UserChangeAllowed | This key specifies whether the biometric setting can be changed by the end user. This key is only supported with Outlook for iOS. <br>**Value type**: Boolean <br><br>**Accepted values**: <br><br> true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Contacts.LocalSyncEnabled | By default, Outlook doesn't sync contact data with the native Contacts app. This key defines the default sync state behavior. Setting the value to *true* will enable contact sync. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Contacts.LocalSyncEnabled.UserChangeAllowed | This key specifies whether the contact sync state can be changed by the end user. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.ExternalRecipientsToolTipEnabled | This key specifies whether the **External Recipients MailTip** is enabled. Setting the value to *false* will disable the MailTip. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.BlockExternalImagesEnabled | (Legacy) This key specifies whether external images are blocked by default. Setting the value to *true* will enable blocking external images. **Note**: This key is now considered a legacy key which can be better expressed using the BlockExternalImagesSetting key which allows for more policy options and loading for safe senders only.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.BlockExternalImagesSetting | This key specifies the setting for whether external images are downloaded, according to the values below.<br>**Note**: When set, this key will override the value in the legacy key above, if that is also set. This is the newer version, which allows for a "Load for Safe Senders" setting. <br><br>**Value Type**: Int <br><br>**Accepted values**: <br><br>**Always Block**: 0 <br><br>**Load only for Safe Senders**: 1 <br><br>**Always Load**: 2 <br><br>**Default if not specified**: 1 (Load for Safe Senders only) | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.BlockExternalImagesEnabled.UserChangeAllowed | (Legacy) This key specifies whether the **Block External Images** setting can be changed by the end user. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.BlockExternalImagesSetting.UserChangeAllowed | This key specifies whether the Block External Images setting can be updated by user settings on their device. It behaves in the same way as the legacy key above. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.DefaultSignatureEnabled | This key specifies whether the app uses its default signature. Setting the value to *false* will disable the app's default signature. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SuggestedRepliesEnabled | This key specifies whether the app enables **Suggested Replies**. Setting the value to *false* will disable the app's ability to suggest replies.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SuggestedRepliesEnabled.UserChangeAllowed | This key specifies whether the Suggested Replies setting can be changed by the end user.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.OrganizeByThreadEnabled | This key specifies whether the app enables **Organize by thread** view. Setting the value to *false* will disable mail threaded conversation view.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.PlayMyEmailsEnabled | This key specifies whether the Play My Emails feature is promoted to eligible users via a banner in the inbox. When set to *Off*, this feature won't be promoted to eligible users in the app. Users can choose to manually enable Play My Emails from within the app, even when this feature is set to *Off*. When set as not configured, the default app setting is *On* and the feature will be promoted to eligible users.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Calendar.NativeSyncEnabled | By default, Outlook doesn't sync calendar data to the native Calendar app. This key defines the default sync state behavior. Setting the value to *true* will enable calendar sync. This key is only supported with Outlook for Android. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Calendar.NativeSyncEnabled.UserChangeAllowed | This key specifies whether the calendar sync state can be changed by the end user. This key is only supported with Outlook for Android. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.TextPredictionsEnabled | Outlook can suggest words and phrases as you compose messages. When set as not configured, the default app setting is set to *On*. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.TextPredictionsEnabled.UserChangeAllowed | This key specifies whether **Smart Compose** can be changed by the end user. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Settings.ThemesEnabled | Outlook supports custom visual themes. When set as not configured, the default app setting is set to *On*. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.BlockSharing | This key specifies whether the app enables the block sharing experience. Setting the value to *true* will block sharing of the inbox in the app. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified:** false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Calendar.BlockSharing | This key specifies whether the app enables the block sharing experience. Setting the value to *true* will block sharing of the calendar in the app. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified:** false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Settings.defaultFontName | This key configures the default font name. Users will not be able to change their default font name if this key is configured. See below to allow for user configuration.<br>**Value**:  1. String  2. The font name must be included in the list of fonts supported by Office. This list may have some minor changes across versions. For a more accurate list, refer to the link: [Cloud fonts in Office](https://support.microsoft.com/en-us/office/cloud-fonts-in-office-f7b009fe-037f-45ed-a556-b5fe6ede6adb). **Note:** Avoid selecting bold and italic font variations.  3. The font names aren't case sensitive. <br><br>**Config example**: Arial | Managed Devices, Managed Apps |
| com.microsoft.outlook.Settings.defaultFontSize | This key configures the default font size. Users will not be able to change their default font size if this key is configured. See below to allow for user configuration.<br>**Value**: 1. Int  2. The font size must be one of the allowed values: 8, 9, 10, 11, 12, 14, 16, 18, 20, 22, 24, 26, 28, 36, 48, 72. <br><br>**Config example**: 12 | Managed Devices, Managed Apps |
| com.microsoft.outlook.Settings.defaultFontName.UserChangeAllowed | This key allows a user to change their default font name when the Intune setting for com.microsoft.outlook.Settings.defaultFontName is configured. The font name configured in com.microsoft.outlook.Settings.defaultFontName is used by default until the user changes the font name.**Value type**: Boolean <br>**Accepted values**: true, false <br><br>**Default if not specified:** false <br><br>**Required**: No <br><br>**Example**: true | Managed Devices, Managed Apps |
| com.microsoft.outlook.Settings.defaultFontSize.UserChangeAllowed | This key allows a user to change their default font size when the Intune setting for com.microsoft.outlook.Settings.defaultFontSize is configured. The font name configured in com.microsoft.outlook.Settings.defaultFontSize is used by default until the user changes the font size.**Value type**: Boolean <br>**Accepted values**: true, false <br><br>**Default if not specified:** false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |

### S/MIME settings

Outlook for iOS offers administrators the ability to customize the default S/MIME configuration in Outlook for iOS and Android.

| Key | Value | Device Enrollment Type |
| --- | --- | --- |
| com.microsoft.outlook.Mail.SMIMEEnabled | This key specifies whether the app enables S/MIME. Use of S/MIME requires certificates available to Outlook for iOS and Android. Setting the value to *true* will enable S/MIME support in the app.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SMIMEEnabled.UserChangeAllowed | This key specifies whether the S/MIME setting can be changed by the end user.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SMIMEEnabled.EncryptAllMail | This key specifies whether S/MIME encryption is required to send messages. Use of S/MIME requires certificates available to Outlook for iOS and Android. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SMIMEEnabled.EncryptAllMail.UserChangeAllowed | This key specifies whether the S/MIME setting can be changed by the end user.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SMIMEEnabled.SignAllMail | This key specifies whether S/MIME signing is required to send messages. Use of S/MIME requires certificates available to Outlook for iOS and Android. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: false <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SMIMEEnabled.SignAllMail.UserChangeAllowed | This key specifies whether the S/MIME setting can be changed by the end user.<br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Required**: No <br><br>**Example**: false | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SMIMEEnabled.LDAPHostName | This key specifies the LDAP directory endpoint to query for certificates.<br>**Value type**: String <br><br>**Accepted values**: ldap://domainname:protocol, ldaps://domainname:protocol, domainname:protocol <br><br>**Default if not specified**: N/A <br><br>**Required**: No <br><br>**Example**: ldap://contoso.com <br><br> ldaps://contoso.com <br><br> contoso.com <br><br> ldaps://contoso.com:636 <br><br> contoso.com:636 | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SMIMEEnabled.CertificatesLookupOrder | This key specifies the order in which certificates are used to decrypt and encrypt S/MIME messages. <br>**Value type**: String <br><br>**Accepted values**: Write as "X, X, X, X", "X, X, X", "X, X", or "X" <br>- 0 (Contacts)<br>- 1 (GAL)<br>- 2 (Device)<br>- 3 (LDAP) <br>**Default if not specified**: "0, 1, 2, 3" <br><br>**Required**: No <br><br>**Example**: "3, 2, 0, 1", "3" | Managed Devices, Managed Apps |
| com.microsoft.outlook.Mail.SMIMEEnabled.ManualCertSelect | This key specifies whether users can manually select certificates to use for S/MIME signing and encryption. When enabled, users can choose from the available certificates instead of having Outlook automatically select certificates for signing and encryption. <br>**Value type**: Boolean <br><br>**Accepted values**: true, false <br><br>**Default if not specified**: false <br><br>**Required**: No <br><br>**Example**: true | Managed Devices, Managed Apps |

### Data protection settings

Outlook for iOS and Android offers administrators additional data protection capabilities when Outlook is managed by Microsoft Intune and has an Intune App Protection Policy.

| Key | Value | Device Enrollment Type |
| --- | --- | --- |
| com.microsoft.outlook.Calendar.NativeSyncAvailable.IntuneMAMOnly | By default, an App Protection Policy allows for calendar synchronization with the native Calendar app but can be used to block calendar sync availability with the **Sync policy managed app data with native apps or add-ins** setting. Configuring this setting to *false* will block calendar synchronization when the App Protection Policy setting is set to **Allowed**. This key is only supported with Outlook for Android. <br>**Accepted values**: true, false <br><br>**Default if not specified**: No value specified <br><br>**Example**: false | Managed apps |
| com.microsoft.outlook.AddinsAvailable.IntuneMAMOnly | By default, an App Protection Policy allows users to utilize third-party add-ins but can be used to block add-ins with the **Sync policy managed app data with native apps or add-ins** setting. Configuring this setting to *false* will block add-ins when the App Protection Policy setting is set to **Allowed**. <br>**Accepted values**: true, false <br><br>**Default if not specified**: No value specified <br><br>**Example**: false | Managed apps |
| com.microsoft.outlook.Calendar.Notifications.IntuneMAMOnly | **(1)** If APP NotificationRestrictions is set to **BlockOrgData**, only then check for com.microsoft.outlook.Calendar.Notifications.IntuneMAMOnly: <br>If the app config value is set to **null** (doesn't exist), all sensitive data properties are removed. <br><br> If the app config value is set to **0**, all sensitive data are exposed.<br><br> If the app config value is set to **1**, only the subject (and meeting time) is exposed.<br><br>**(2)** If APP NotificationRestrictions is set to **Allow** or NotificationRestrictions is set to **Block**, then all sensitive data properties are exposed in calendar reminder notifications. <br><br>**Important**: To set the com.microsoft.outlook.Calendar.Notifications.IntuneMAMOnly value to **1**, admins must create a policy using Intune scripts to inject a value of **1** until the MEM portal is able to be updated. | Managed apps |
| com.microsoft.intune.mam.areWearablesAllowed | This key specifies if Outlook data can be synchronized to a wearable device. Setting the value to *false* disables wearable synchronization. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: false | Managed apps |
| com.microsoft.outlook.ContactSync.AddressAllowed | This key specifies if the contact's address should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.BirthdayAllowed | This value specifies if the contact's birthday should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.CompanyAllowed | This key specifies if the contact's company name should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.DepartmentAllowed | This key specifies if the contact's department should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.EmailAllowed | This key specifies if the contact's email address should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.InstantMessageAllowed | This key specifies if the contact's instant messaging address should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.JobTitleAllowed | This key specifies if the contact's job title should be synchronized to native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.NicknameAllowed | This key specifies if the contact's nickname should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.NotesAllowed | This key specifies if the contact's notes should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.PhoneHomeAllowed | This key specifies if the contact's home phone number should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.PhoneHomeFaxAllowed | This key specifies if the contact's home fax number should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.PhoneMobileAllowed | This key specifies if the contact's mobile phone number should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.PhoneOtherAllowed | This key specifies if the contact's other phone number should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.PhonePagerAllowed | This key specifies if the contact's pager phone number should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.PhoneWorkAllowed | This key specifies if the work phone number should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.PhoneWorkFaxAllowed | This key specifies if the contact's work fax number should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.PrefixAllowed | This key specifies if the contact's name prefix should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.ContactSync.SuffixAllowed | This key specifies if the contact's name suffix should be synchronized with native contacts. <br>**Accepted values**: true, false <br><br>**Default if not specified**: true <br><br>**Example**: true | Managed apps |
| com.microsoft.outlook.WidgetsAvailable.IntuneMAMOnly | By default, an App Protection Policy allows for the widget to sync with the Outlook app but can be used to block widget sync availability with the **Sync policy managed app data with native apps or add-ins** setting. Configuring this setting to *false* blocks the widget synchronization when the **App Protection Policy** setting is set to **Allowed**. <br>**Accepted values**: true, false <br><br>**Default if not specified**: No value specified <br><br>**Example**: Here's an example that allows calendar sync but disallows widget sync: <br><br>*Sync policy managed app data with native apps or add-ins* == allow *com.microsoft.outlook.WidgetsAvailable.IntuneMAMOnly* = false <br><br> Here's another example to block widget sync, calendar sync, and add-ins: <br><br>*Sync policy managed app data with native apps or add-ins* == block <br><br> And another example that blocks calendar sync but allows widget sync: <br><br>*Sync policy managed app data with native apps or add-ins* == allow *com.microsoft.outlook.WidgetsAvailable.IntuneMAMOnly* = true *com.microsoft.outlook.Calendar.NativeSyncAvailable.IntuneMAMOnly* = false | Managed apps |
| Louder Mandatory labeling | Off <br> Organizations have mandatory labeling enabled without default labeling, and would like to have the label selection first before going to compose the email. Then when the users click **Send**, the email could just be sent without any forgotten labeling pop ups. Outlook mobile will introduce a new MDM setting (com.microsoft.outlook.Mail.LouderMandatoryLabelEnabled) to allow admins to enable this louder mandatory configuration for Outlook mobile clients (iOS and Android) specifically. | App default |
| com.microsoft.outlook.Mail.Notifications.IntuneMAMOnly | **(1)** If Intune App Protection Policy (APP) NotificationRestrictions = BlockOrgData, only then check for com.microsoft.outlook.Mail.Notifications.IntuneMAMOnly: <br> If app config value is **null** (doesn't exist): All sensitive data properties are removed. <br><br> If app config value is **0**: Only subject and sender are exposed. <br><br> If app config value is **1**: Only sender is exposed. <br><br>**(2)** Else, if APP NotificationRestrictions = Allow or NotificationRestrictions = Block, then: <br><br> All sensitive data properties are exposed in mail notifications. | Managed apps |
| com.microsoft.outlook.Mail.VideoMessages.VideoCaptureAndUploadEnabled | If app config value = **null** (doesn't exist): Video capture is enabled. <br><br> If app config value = **true**: Video capture is enabled. <br><br> If app config value = **false**: Video capture is disabled. You can still capture photos. <br><br> Video capture will enable the user to capture a video within Microsoft Outlook Mobile and upload the captured video to an email via OneDrive for Business. | Managed devices, Managed apps |

## Download emails and work offline using days-based sync window setting

Using the days-based sync window setting, you can decide how many days' worth of emails and attachments you want to download to your iOS or Android device and thus always access them even when offline.

### Available Microsoft Intune controls

Using Microsoft Intune, admins can specify a default sync window for their users. Admins can also allow or disallow changes to the default sync window. The keys for these settings are:

| Key | Input type (Value) |
| --- | --- |
| `com.microsoft.outlook.Settings.DaysToSync` | Integer (1-90) |
| `com.microsoft.outlook.Settings.DaysToSync.UserChangeAllowed` | Boolean (true/false) |

Admin needs to set a valid value (number of days), from `1` to `90`.