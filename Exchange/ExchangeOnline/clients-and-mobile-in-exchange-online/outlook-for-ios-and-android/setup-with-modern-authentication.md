---
layout: Conceptual
title: Account setup with modern authentication in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/setup-with-modern-authentication
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
description: 'Summary: How users with modern authentication-enabled accounts can quickly set up their Outlook for iOS and Android accounts in Exchange Online.'
ms.topic: install-set-up-deploy
author: AshaIyengar21
ms.author: serdars
ms.assetid: 1efe7737-b573-4f36-a0f2-27714d2ebdb0
ms.collection:
- exchange-online
- M365-email-calendar
ms.reviewer: smithre4
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2023-10-24T00:00:00.0000000Z
locale: en-us
document_id: aeec798c-00f4-df45-da44-47e5aac06ff9
document_version_independent_id: 4cdfab74-fce7-f298-c3df-51da100c2162
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/setup-with-modern-authentication.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/setup-with-modern-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/setup-with-modern-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 03d1d2aa-4cac-30b4-f530-aca0c574fd2e
---

# Account setup with modern authentication in Exchange Online | Microsoft Learn

**Summary**: How users with modern authentication-enabled accounts can quickly set up their Outlook for iOS and Android accounts in Exchange Online.

Users with modern authentication-enabled accounts (Microsoft 365 or Office 365 accounts or [on-premises accounts using hybrid modern authentication](../../clients/outlook-for-ios-and-android/use-hybrid-modern-auth)) have two ways to set up their own Outlook for iOS and Android accounts: Auto-Detect and single sign-on. In addition, Outlook for iOS and Android also offers IT administrators the ability to "push" account configurations to their Microsoft 365 and Office 365 users, and to control whether Outlook for iOS and Android supports personal accounts.

## Modern authentication

Modern authentication is an umbrella term for a combination of authentication and authorization methods that include:

- **Authentication methods**: Multifactor authentication; Client Certificate-based authentication.
- **Authorization methods**: Microsoft's implementation of Open Authorization (OAuth).

Modern authentication is enabled by using the Microsoft Authentication Library (MSAL). MSAL-based authentication is what Outlook for iOS and Android uses to access Exchange Online mailboxes in Microsoft 365 or Office 365. MSAL authentication, used by Office apps on both desktop and mobile devices, involves users signing in directly to Microsoft Entra ID, which is the identity provider for Microsoft 365 and Office 365, instead of providing credentials to Outlook.

MSAL-based authentication uses OAuth for modern authentication-enabled accounts (Microsoft 365 or Office 365 accounts or [on-premises accounts using hybrid modern authentication](../../clients/outlook-for-ios-and-android/use-hybrid-modern-auth)). It also provides a secure mechanism for Outlook for iOS and Android to access email, without requiring access to user credentials. At sign-in, the user authenticates directly with Microsoft Entra ID and receives an access/refresh token pair in return. The access token grants Outlook for iOS and Android access to the appropriate resources in Microsoft 365 or Office 365 (for example, the user's mailbox). A refresh token is used to obtain a new access or refresh token pair when the current access token expires. OAuth provides Outlook with a secure mechanism to access Microsoft 365 or Office 365, without needing or storing a user's credentials.

For information on token lifetimes, see [Configurable token lifetimes in Microsoft identity platform](/en-us/entra/identity-platform/configurable-token-lifetimes). Token lifetime values can be adjusted; for more information, see [Configure authentication session management with Conditional Access](/en-us/entra/identity/conditional-access/howto-conditional-access-session-lifetime). If you choose to reduce token lifetimes, you can also reduce the performance of Outlook for iOS and Android, because a smaller lifetime increases the number of times the application must acquire a fresh access token.

A previously granted access token is valid until it expires. The identity model being utilized for authentication has an impact on how password expiration is handled. There are three scenarios:

1. For a federated identity model, the on-premises identity provider needs to send password expiry claims to Microsoft Entra ID, otherwise, Microsoft Entra ID won't be able to act on the password expiration. For more information, see [Configure AD FS to Send Password Expiry Claims](/en-us/windows-server/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims).
2. Password Hash Synchronization doesn't support password expiration. This scenario means that the apps that had previously obtained an access and refresh token pair will continue to function until the lifetime of the token pair is exceeded or the user changes the password. For more information, see [Implement password synchronization with Microsoft Entra Connect Sync](/en-us/entra/identity/hybrid/connect/how-to-connect-password-hash-synchronization).
3. Pass-through Authentication requires that password writeback enabled in Microsoft Entra Connect. For more information, see [Microsoft Entra pass-through authentication: Frequently asked questions](/en-us/entra/identity/hybrid/connect/how-to-connect-pta-faq#what-happens-if-my-user-s-password-has-expired-and-they-try-to-sign-in-by-using-pass-through-authentication-).

Upon token expiration, the client attempts to use the refresh token to obtain a new access token, but because the user's password has changed, the refresh token is invalidated (assuming directory synchronization has occurred between on-premises and Microsoft Entra ID). The invalidated refresh token forces the user to reauthenticate in order to obtain a new access token and refresh token pair.

## AutoDetect

Outlook for iOS and Android offers a solution called AutoDetect that helps end-users quickly setup their accounts. AutoDetect will first determine which type of account a user has, based on the SMTP domain. Account types that are covered by this service include Microsoft 365, Office 365, Outlook.com, Google, Yahoo, and iCloud. Next, AutoDetect makes the appropriate configurations to the app on the user's device based on that account type. This solution saves time for users and eliminates the need for manual input of configuration settings like hostname and port number.

For modern authentication, which is used by all Microsoft 365 or Office 365 accounts and [on-premises accounts using hybrid modern authentication](../../clients/outlook-for-ios-and-android/use-hybrid-modern-auth), AutoDetect queries Exchange Online for a user's account information and then configures Outlook for iOS and Android on the user's device so that the app can connect to Exchange Online. During this process, the only information required from the user is their SMTP address and credentials.

The following images show an example of account configuration via AutoDetect:

![Outlook for iOS and Android onboarding.](../../exchangeonline/media/67c22e0d-ba01-4923-bdb9-375f26ec90fb.png)

If AutoDetect fails for a user, the following images show an alternative account configuration path using manual configuration:

![Manaul account setup for Outlook for iOS and Android.](../../exchangeonline/media/fdb9b8e8-499d-4702-b362-4fe9a2e9c978.png)

## Single sign-on

All Microsoft apps that use the Microsoft Authentication Library (MSAL) support single sign-on. In addition, single sign-on is also supported when the apps are used with either the Microsoft Authenticator or Microsoft Company Portal apps.

Tokens can be shared and reused by other Microsoft apps (such as Word mobile) under the following scenarios:

1. When the apps are signed by the same signing certificate, and use the same service endpoint or audience URL (such as the Microsoft 365 or Office 365 URL). In this case, the token is stored in app shared storage.
2. When the apps use or support single sign-on with a broker app, and the tokens are stored within the broker app. Microsoft Authenticator is an example of a broker app. In the broker app scenario, after you attempt to sign in to Outlook for iOS and Android, MSAL will launch the Microsoft Authenticator app, which will make a connection to Microsoft Entra ID to obtain the token. It will then hold on to the token and reuse it for authentication requests from other apps, for as long as the configured token lifetime allows.

For more information, see [Configure SSO on macOS and iOS](/en-us/entra/identity-platform/single-sign-on-macos-ios).

If a user is already signed in to another Microsoft app on their device, like Word or Company Portal, Outlook for iOS and Android will detect that token and use it for its own authentication. When such a token is detected, users adding an account in Outlook for iOS and Android will see the discovered account available as "Found" under **Accounts** on the **Settings** menu. New users see their account in the initial account setup screen.

The following images show an example of account configuration via single sign-on for a first-time user:

![Single sign-on in Outlook for iOS and Android.](../../exchangeonline/media/d11691ca-49e9-4282-80f0-c73547ccc98e.png)

If a user already has Outlook for iOS and Android, such as for a personal account, but a Microsoft 365 or Office 365 account is detected because they recently enrolled, the single-sign on path resembles the following image:

![Alternative single-sign on path for Outlook for iOS and Android.](../../exchangeonline/media/e24efc89-10e1-4a11-b80c-bbfc08033334.png)

## Account setup configuration via enterprise mobility management

Outlook for iOS and Android offers IT administrators the ability to "push" account configurations to Microsoft 365 or Office 365 accounts or on-premises accounts using hybrid modern authentication. This capability works with any Unified Endpoint Management (UEM) provider who uses the [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android.

For users enrolled in Microsoft Intune, you can deploy the account configuration settings using Intune in the Azure portal.

Once account setup configuration has been set up in the UEM provider and the user enrolls their device, Outlook for iOS and Android detects that an account is "Found" and then prompts the user to add the account. The only information the user needs to enter to complete the setup process is their password. Then, the user's mailbox content loads and the user can begin using the app.

For more information on the account setup configuration keys needed to enable this functionality, see the Account setup configuration section in [Deploying Outlook for iOS and Android App Configuration Settings](outlook-for-ios-and-android-configuration-with-microsoft-intune).

## Organization allowed accounts mode

Respecting the data security and compliance policies of our largest and highly regulated customers is a key pillar to the Microsoft 365 and Office 365 value. Some companies have a requirement to capture all communications information within their corporate environment, and, ensure the devices are only used for corporate communications. To support these requirements, Outlook for iOS and Android on corporate-managed devices can be configured to only allow a single, corporate account to be provisioned within Outlook for iOS and Android. Like with account setup configuration, this capability works with any UEM provider who uses the [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android. This capability is supported with Microsoft 365 and Office 365 accounts or on-premises accounts using hybrid modern authentication; however, only a single corporate account can be added to Outlook for iOS and Android.

For more information on the settings that need to be configured to deploy Organization Allowed Accounts mode, see the Organization allowed accounts mode section in [Deploying Outlook for iOS and Android App Configuration Settings](outlook-for-ios-and-android-configuration-with-microsoft-intune).

Note

Account setup configuration and Organization allowed accounts mode can be configured together to simplify account setup.

To ensure these users can only access corporate email on enrolled devices (whether it be iOS or Android Enterprise) with Intune, you will need to use a Microsoft Entra Conditional Access policy with the grant controls [Require devices to be marked as compliant](/en-us/entra/identity/conditional-access/concept-conditional-access-grant#require-device-to-be-marked-as-compliant) and [Require approved client app](/en-us/azure/active-directory/active-directory-conditional-access-technical-reference). Details on creating this type of policy can be found in [Microsoft Entra app-based conditional access](/en-us/entra/identity/conditional-access/howto-policy-approved-app-or-app-protection).

Important

[Require devices to be marked as compliant](/en-us/entra/identity/conditional-access/concept-conditional-access-grant#require-device-to-be-marked-as-compliant) grant control requires the device to be managed by Intune.

1. The first policy allows Outlook for iOS and Android, and it blocks OAuth capable Exchange ActiveSync clients from connecting to Exchange Online. See "Step 1 - Configure a Microsoft Entra Conditional Access policy for Exchange Online", but for the fifth step, select "Require device to be marked as compliant", "Require approved client app", and "Require all the selected controls".
2. The second policy prevents Exchange ActiveSync clients using basic authentication from connecting to Exchange Online. See "Step 2 - Configure a Microsoft Entra Conditional Access policy for Exchange Online with Active Sync (EAS)."

## Shared Device Mode in Outlook for iOS and Android

Outlook for Android and iOS supports **Shared Device Mode**, enabling secure and seamless sign-in experiences on devices used by multiple users—such as in frontline worker or kiosk scenarios. With Shared Device Mode, your organization can ensure that personal and organizational data stays protected, and that users can quickly and easily access only the resources they're authorized for.

### What is Shared Device Mode?

Shared Device Mode is a feature enabled by Microsoft Entra ID (formerly Azure AD) that configures the device for **single sign-on (SSO)** and **single sign-out**. When a user signs into a supported app like Outlook, that sign-in applies across all apps configured for Shared Device Mode. Likewise, when the user signs out, all supported apps are signed out and local data is cleared.

Shared Device Mode is ideal for:

- Frontline workers who pick up any available device at the beginning of their shift.
- Shared tablets or phones in retail, healthcare, or manufacturing environments.
- Secure access to email and calendar without risk of cross-user data leakage.

Important

Shared Device Mode must be enabled by your organization's IT admin using [Overview of shared device mode](/en-us/entra/identity-platform/msal-shared-devices) documentation and appropriate device configuration tools such as Microsoft Intune.

### How Outlook Works in Shared Device Mode

When configured for Shared Device Mode, Outlook behaves differently from the regular experience to support shared usage:

| Feature | Behavior |
| --- | --- |
| **Sign-in** | Users sign in using their Microsoft Entra ID account. |
| **SSO across apps** | Once signed in, the user is also signed into other apps that support Shared Device Mode. |
| **Sign-out** | Users can sign out from the Shared Device launcher or manually in Outlook. This signs out all apps and clears local data. |
| **Data management** | Cached email, calendar, and contact data are removed upon sign out. |
| **Multi-user support** | Only one user is supported at a time; concurrent multi-user sessions aren't allowed. |

Tip

To minimize login friction, Outlook uses device-wide authentication tokens provided by the Shared Device Mode configuration.

### Device and App Setup

To enable Shared Device Mode with Outlook Mobile:

1. **Provision the device** using Microsoft Intune or your preferred MDM solution with Shared Device Mode enabled.
2. **Install Outlook for Android or iOS** from the official app store.
3. Ensure the latest version of Outlook is installed.
4. Ensure all other shared apps on the device are compatible with Shared Device Mode.

You can find more guidance in [Overview of shared device mode.](/en-us/azure/active-directory/develop/msal-shared-devices).

### Limitations and Considerations

- Shared Device Mode **doesn't support personal accounts** in Outlook.
- **Only Microsoft Entra ID work accounts** are supported.
- Users must **sign out at the end of their session** to ensure data privacy.
- **Offline support is not available**: Since the global sign out signal can't be supported while the device is offline, Outlook for iOS and Android is unable to support use of the app while offline if Outlook is configured for Shared Device Mode. Also, data is purged at sign out to protect user information.
- Features requiring persistent state (like Drafts or local search history) **may not be retained across sessions**.

### Troubleshooting

If Outlook doesn't appear to respect Shared Device Mode:

- Verify that the device is properly configured for Shared Device Mode.
- Check for updates to Outlook Mobile and other apps you rely on for your Shared Device Mode configuration.
- Ensure that sign-in policies and Conditional Access policies aren't blocking access.

You can gather logs or use Microsoft Endpoint Manager reporting tools to identify setup issues.

### Set up shared device mode

If your organization is already using shared device mode, no special configuration is required for the Outlook iOS and Android apps. If shared device mode hasn't been set up, contact your organization's mobile device management team about getting it set up. Refer them to the following articles if they're unfamiliar with the feature:

- [Overview of shared device mode](/en-us/azure/active-directory/develop/msal-shared-devices)
- [Manage devices for frontline workers](/en-us/microsoft-365/frontline/flw-devices)