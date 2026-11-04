---
layout: Conceptual
title: S/MIME for Outlook for iOS and Android in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/smime-outlook-for-ios-and-android
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
description: Admins can learn how to configure the S/MIME infrastructure in Exchange Online for use with Outlook for iOS and Android.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.reviewer: smithre4
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2021-05-11T00:00:00.0000000Z
locale: en-us
document_id: 166f2cf0-69e9-2a39-1d2b-1f647fe17dbe
document_version_independent_id: a2fc4fc6-bcb7-d90b-1b53-0621a0258037
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/smime-outlook-for-ios-and-android.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/smime-outlook-for-ios-and-android
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/smime-outlook-for-ios-and-android.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: b1398ac3-279b-cb78-6209-53de514a39d2
---

# S/MIME for Outlook for iOS and Android in Exchange Online | Microsoft Learn

S/MIME (Secure/Multipurpose Internet Mail Extensions) is a widely accepted protocol for sending digitally signed and encrypted messages. For more information, see [S/MIME for message signing and encryption in Exchange Online](../../security-and-compliance/smime-exo/smime-exo).

To use S/MIME in Outlook for iOS and Android, you need to configure specific S/MIME prerequisite in Exchange Online. After you complete those steps, you can deploy S/MIME certificates to Outlook for iOS and Android using the following methods:

- Manual certificate delivery
- Automated certificate delivery

This article describes how to configure Exchange Online for S/MIME using Outlook for iOS and Android, and how to use S/MIME in Outlook for iOS and Android.

## S/MIME prerequisites

Ensure S/MIME is properly configured in Exchange Online by following the steps outlined in [Configure S/MIME in Exchange Online](../../security-and-compliance/smime-exo/configure-smime-exo). Specifically, this configuration includes:

1. Setting up the [virtual certificate collection](../../security-and-compliance/smime-exo/configure-smime-exo#step-2-set-up-a-virtual-certificate-collection-in-exchange-online).
2. Publishing the certificate revocation list to the internet.

In manual and automated certificate delivery solutions, the certificate's trusted root chain must be available and discoverable within your virtual certificate collection in Exchange Online. Trust verification is performed on all digital certificates. Exchange Online validates the certificate by validating each certificate in the certificate chain until it reaches a trusted root certificate. This verification is done by obtaining the intermediate certificates through the authority information access attribute in the certificate until a trusted root certificate is located. Intermediate certificates can also be included with digitally signed email messages. If Exchange Online locates a trusted root certificate and can query the certificate revocation list for the certificate authority, the digital certificate's chain for that digital certificate is considered valid and trusted and can be used. If Exchange Online fails to locate a trusted root certificate or fails to contact the certificate revocation list for the certificate authority, that certificate is considered invalid and isn't trusted.

Outlook for iOS and Android uses the user's primary SMTP address for mail flow activities, which is configured during account profile setup. The S/MIME certificate used by Outlook for iOS and Android is calculated by comparing the user's primary SMTP address as defined in the account profile with the certificate's subject value or the subject alternative name value. If these values don't match, Outlook for iOS and Android reports a certificate isn't available (see Figure 7) and doesn't allow the user to sign and/or encrypt messages.

## Manual certificate delivery

Outlook for iOS and Outlook for Android both support manual certificate delivery, which is when the certificate is emailed to the user and the user taps on the certificate attachment within the app to initiate the certificate's installation. The following image shows how manual certificate delivery works in iOS.

![Screenshots showing manual certificate installation on iOS.](../../exchangeonline/media/sensitive-manual-certificate.png)

A user can export their own certificate and mail it to themselves using Outlook. For more information, see [Exporting a digital certificate](https://support.microsoft.com/office/f3574266-2f9e-4f15-ab21-5989f4cf0c9b).

Important

When exporting the certificate, ensure that the exported certificate is password-protected with a strong password.

## Automated certificate delivery

Important

- Outlook for iOS and Android only supports automated certificate delivery when Microsoft Endpoint Manager is the enrollment provider.
- For Outlook for iOS, this limitation is due to the iOS keychain architecture. iOS offers a system keychain and publisher keychains. iOS prevents non-Microsoft apps from accessing the system keychain (only first-party apps and the Safari webview controller can access the system keychain). To deliver accessible certificates for Outlook for iOS, the certificates must reside in the Microsoft publisher keychain to which Outlook for iOS has access. Only Microsoft published apps, like the Company Portal, can place certificates into the Microsoft publisher keychain.
- Outlook for Android relies on Endpoint Manager to deliver and approve the S/MIME certificates. Automatic certificate delivery is supported with Android enrollment scenarios: device administrator, Android Enterprise work profile, and Android Enterprise fully managed.

With Endpoint Manager, organizations can import encryption certificate histories from any Certification Authority. Endpoint Manager automatically delivers those certificates to any device that the user enrolls. Generally, Simple Certificate Enrollment Protocol (SCEP) is used for signing certificates. With SCEP, the private key is generated and stored on the enrolled device and a unique certificate is delivered to each device that a user enrolls, which can be used for non-repudiation. Lastly, Endpoint Manager supports derived credentials for customers who need support for the NIST 800-157 standard. The Company Portal is used to retrieve signing and encryption certificates from Intune.

In order to deliver certificates to Outlook for iOS and Android, you must complete the following prerequisites:

- Deploy trusted root certificates via Endpoint Manager. For more information, see [Create trusted certificate profiles](/en-us/mem/intune/protect/certificates-trusted-root?form=MG0AV3).
- Encryption certificates must be imported into Endpoint Manager. For more information, see [Configure and use imported PKCS certificates with Intune](/en-us/mem/intune/protect/certificates-pfx-configure?form=MG0AV3).
- Install and Configure the PFX Connector for Microsoft Intune. For more information, see [Download, install, and configure the PFX Certificate Connector for Microsoft Intune](/en-us/mem/intune/protect/certificate-connector-install?form=MG0AV3).
- Devices must be enrolled to receive trusted root and S/MIME certificates automatically from Endpoint Manager.

### Outlook for iOS automated certificate delivery

Use the following steps to create and configure the Outlook for iOS S/MIME policy in Endpoint Manager. These settings provide automated delivery of the signing and encryption certificates.

1. Sign into [Microsoft Endpoint Manager](https://endpoint.microsoft.com).
2. Select **Apps** and then select **App configuration policies**.
3. On the **App Configuration policies** blade, choose **Add** and select **Managed devices** to start the app configuration policy creation flow.
4. On the **Basics** section, enter a **Name**, and optional **Description** for the app configuration settings.
5. For **Platform**, choose **iOS/iPadOS**.
6. For **Targeted app**, choose **Select app**, and then, on the **Associated app** blade, choose **Microsoft Outlook**. Select **OK**.

    Note

    If Outlook isn't listed as an available app, then you must add it by following the instructions in [Assign apps to Android work profile devices with Intune](/en-us/mem/intune/apps/apps-add-android-for-work?form=MG0AV3) and [Add iOS store apps to Microsoft Intune](/en-us/mem/intune/apps/store-apps-ios?form=MG0AV3).
7. Select **Configuration settings** to add configuration settings.

    Select **Use configuration designer** next to **Configuration settings format** and accept or modify the default settings. For more information, see [Deploying Outlook for iOS and Android app configuration settings](outlook-for-ios-and-android-configuration-with-microsoft-intune).
8. Select **S/MIME** to display the **Outlook S/MIME settings**. ![Screenshot showing Outlook S/MIME settings.](../../exchangeonline/media/outlook-mobile-smime-settings-v3.png)
9. Set **Enable S/MIME** to **Yes**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or choose **No** if you want to prevent the user from changing the setting's value.
10. Choose whether to **Encrypt all emails** by selecting **Yes** or **No**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or choose **No** if you want to prevent the user from changing the setting's value.
11. Choose whether to **Sign all emails** by selecting **Yes** or **No**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or choose **No** if you want to prevent the user from changing the setting's value.
12. If needed, deploy a **LDAP URL** for recipient certificate lookup. For more information on the URL format, see LDAP support for certificate lookup.
13. Set **Deploy S/MIME certificates from Intune** to **Yes**.
14. Under **Signing certificates** next to **Certificate profile type**, choose one of the following options:

    - **SCEP**: Creates a unique certificate for the device and user that Microsoft Outlook can use for signing. For information on what is required to use SCEP certificate profiles, see [Configure infrastructure to support SCEP with Intune](/en-us/mem/intune/protect/certificates-scep-configure?form=MG0AV3).
    - **PKCS imported certificates**: Uses a certificate that's unique to the user, but might be shared across devices and has been imported to Endpoint Manager by the administrator on behalf of the user. The certificate is delivered to any device that a user enrolls. Endpoint Manager automatically picks the imported certificate that supports signing to deliver to the device that corresponds to the enrolled user. For information on what is required to use PKCS imported certificates, see [Configure and use PKCS certificates with Intune](/en-us/mem/intune/protect/certficates-pfx-configure).
    - **Derived credentials**: Uses a certificate that is already on the device that can be used for signing. The certificate must be retrieved on the device using the derived credentials flows in Intune.
15. Under **Encryption certificates** next to **Certificate profile type**, choose one of the following options:

    - **PKCS imported certificates**: Delivers any encryption certificates that have been imported to Endpoint Manager by the administrator across any device a user enrolls. Endpoint Manager automatically picks the imported certificate or certificates that support encryption and deliver to the enrolled user's devices.
    - **Derived credentials**: Uses a certificate that is already on the device that can be used for signing. The certificate must be retrieved on the device using the derived credentials flows in Intune.
16. Next to **End-user notifications**, choose how to notify end users to retrieve the certificates by selecting **Company Portal** or **Email**.

    On iOS, users must use the Company Portal app to retrieve their S/MIME certificates. Endpoint Manager informs the user that they need to launch the Company Portal to retrieve their S/MIME certificates via the Notifications section of Company Portal, a push notification, and/or an email. Clicking one of the notifications takes the user to a landing page that informs them of progress retrieving the certificates. Once the certificates are retrieved, the user can use S/MIME from within Microsoft Outlook for iOS to sign and encrypt email.

    The end-user notifications include the following options:

    - **Company Portal**: If selected, users receive a push notification on their device, which takes them to the landing page in Company Portal where S/MIME certificates are retrieved.
    - **Email**: Sends an email to the end user informing them that they need to launch Company Portal to retrieve their S/MIME certificates. If the user is on their enrolled iOS device when they select the link in the email, they're redirected to the Company Portal to retrieve their certificates.

    End-users see an experience similar to the following for automated certificate delivery: ![Screenshot showing automated certificate delivery.](../../exchangeonline/media/all-in-one-certificate-delivery.png)
17. Select **Assignments** to assign the app configuration policy to the Microsoft Entra groups. For more information, see [Assign apps to groups with Microsoft Intune](/en-us/mem/intune/apps/apps-deploy?form=MG0AV3).

### Outlook for Android automated certificate delivery

Use the following steps to create and configure the Outlook for iOS and Android S/MIME policy in Endpoint Manager. These settings provide automated delivery of the signing and encryption certificates.

1. Sign into [Microsoft Endpoint Manager](https://endpoint.microsoft.com).
2. Create a [SCEP certificate profile](/en-us/mem/intune/protect/certificates-profile-scep) or [PKCS certificate profile](/en-us/mem/intune/protect/certificates-imported-pfx-configure#create-a-pkcs-imported-certificate-profile) and assign it to your mobile users.
3. Select **Apps** and then select **App configuration policies**.
4. On the **App Configuration policies** blade, choose **Add** and select **Managed devices** to start the app configuration policy creation flow.
5. On the **Basics** section, enter a **Name**, and optional **Description** for the app configuration settings.
6. For **Platform**, choose **Android Enterprise** and for **Profile Type**, choose **All Profile Types**.
7. For **Targeted app**, choose **Select app**, and then, on the **Associated app** blade, choose **Microsoft Outlook**. Select **OK**.

    Note

    If Outlook isn't listed as an available app, then you must add it by following the instructions in [Assign apps to Android work profile devices with Intune](/en-us/mem/intune/apps/apps-add-android-for-work) and [Add iOS store apps to Microsoft Intune](/en-us/mem/intune/apps/store-apps-ios).
8. Select **Configuration settings** to add configuration settings.

    Select **Use configuration designer** next to **Configuration settings format** and accept or modify the default settings. For more information, see [Deploying Outlook for iOS and Android app configuration settings](outlook-for-ios-and-android-configuration-with-microsoft-intune).
9. Select **S/MIME** to display the **Outlook S/MIME settings**.
10. Set **Enable S/MIME** to **Yes**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or choose **No** if you want to prevent the user from changing the setting's value.
11. Choose whether to **Encrypt all emails** by selecting **Yes** or **No**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or choose **No** if you want to prevent the user from changing the setting's value.
12. Choose whether to **Sign all emails** by selecting **Yes** or **No**. When selecting **Yes** or **No**, administrators can choose to allow the user to change the app setting's value. Select **Yes** (app default) to allow the user to change the setting or choose **No** if you want to prevent the user from changing the setting's value.
13. Select **Assignments** to assign the app configuration policy to the Microsoft Entra groups. For more information, see [Assign apps to groups with Microsoft Intune](/en-us/mem/intune/apps/apps-deploy).

## Enabling S/MIME in the client

S/MIME must be enabled for Outlook for iOS and Android to view or create S/MIME-related content.

End users need to enable S/MIME functionality manually by accessing their account settings, tapping Security, and tapping the S/MIME control, which is off by default. The Outlook for iOS S/MIME security setting looks like the following example:

![Screenshots showing Outlook for iOS S/MIME security settings.](../../exchangeonline/media/sensitive-s-mime-setting.png)

Once S/MIME is enabled and the S/MIME certificates are installed, users can view the installed certificates by accessing their account settings and tapping Security. Furthermore, users can tap on each individual S/MIME certificate and view the certificate's details, including information like key usage and the validity period.

![Screenshot showing the Outlook for iOS certificate details screen.](../../exchangeonline/media/certdetails.png)

Users can configure Outlook to automatically sign or encrypt messages. This allows users to save time sending email while being confident that their emails are being signed/encrypted.

### LDAP support for certificate lookup

Outlook for iOS and Android supports accessing public user certificate keys from secure LDAP directory endpoints during recipient resolution. In order to utilize an LDAP endpoint, the following requirements must be met:

- The LDAP endpoint doesn't require authentication.
- The LDAP endpoint configuration is delivered to Outlook for iOS and ANdroid through an app configuration policy. For more information, see [S/MIME settings](outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings).
- The LDAP endpoint configuration is supported using the following formats:
    - `ldaps://contoso.com`
    - `ldap://contoso.com`
    - `ldap://contoso.com:389`
    - `ldaps://contoso.com:636`
    - `contoso.com`
    - `contoso.com:389`
    - `contoso.com:636`

When Outlook for iOS and Android performs a certificate lookup for a recipient, the app searches the local device first, then query Microsoft Entra ID, and then evaluate any LDAP directory endpoint. When Outlook for iOS and Android connects to the LDAP directory endpoint to search for a recipient's public certificate, certificate validation is performed to ensure that the certificate isn't revoked. The certificate is only considered valid by the app if certificate validation completes successfully.

## Using S/MIME in Outlook for iOS and Android

After the certificates have been deployed and S/MIME is enabled in the app, users can consume S/MIME related content and compose content using S/MIME certificates. If the S/MIME setting isn't enabled, users can't consume S/MIME content.

### View S/MIME messages

In the message view, users can view messages that are S/MIME signed or encrypted. In addition, users can tap the S/MIME status bar to view more information about the message's S/MIME status. The following screenshots show examples of how S/MIME messages are consumed in Android.

Important

In order to read an encrypted message, the recipient's private certificate key must be available on the device.

![Screenshots of S/MIME usage in iOS.](../../exchangeonline/media/sensitive-ios-s-mime.png)

Users can install a sender's public certificate key by tapping the S/MIME status bar. The certificate is installed on the user's device, specifically in the Microsoft publisher [keychain in iOS](https://support.apple.com/guide/security/welcome/web) or the system [KeyStore in Android](https://source.android.com/security/reports/Google_Android_Enterprise_Security_Whitepaper_2018.pdf). The Android version appears similar to the following example:

![Screenshots of Outlook for Android public key installation.](../../exchangeonline/media/sensitive-android-key-install.png)

If there are certificate errors, Outlook for iOS and Android warns the user. The user can tap the S/MIME status bar notification to view more information about the certificate error, such as in the following example.

![Screenshot of Outlook for iOS cert error on received message.](../../exchangeonline/media/sensitive-cert-error-message.png)

### Create S/MIME messages

Before a user can send a signed and/or encrypted message, Outlook for iOS and Android performs a validity check on the certificate to ensure it's valid for signing or encryption operations. If the certificate is near expiration, Outlook for iOS and Android alerts the user to obtain a new certificate when the user attempts to sign or encrypt a message, beginning 30 days before expiration.

![Screenshots showing warnings about certificate expiration.](../../exchangeonline/media/sensitive-android-cert-warning.png)

When composing an email in Outlook for iOS and Android, the sender can choose to encrypt and/or sign the message. By tapping on the **ellipses** and then **Sign and Encrypt**, the various S/MIME options are presented. Selecting an S/MIME option enables the respective encoding on the email as soon as the message is saved or sent, assuming the sender has a valid certificate.

Outlook for iOS and Android can send S/MIME signed and encrypted messages to distribution groups. Outlook for iOS and Android enumerates the certificates for the users defined in the distribution group, including users in nested distribution groups, though care should be taken on limiting the number of nested distribution groups to minimize the processing load.

Important

- Outlook for iOS and Android only supports sending clear-signed messages.
- In order to compose an encrypted message, the target recipient's public certificate key must be available either in the Global Address List or stored on the local device. In order to compose a signed message, the sender's private certificate key must be available on the device.

Here's how S/MIME options appear in Outlook for Android:

![Screenshots of Outlook for Android S/MIME options.](../../exchangeonline/media/sensitive-android-smime-options.png)

Outlook for iOS and Android evaluates all recipients before sending an encrypted message and confirm that a valid public certificate key exists for each recipient. The Global Address List (GAL) is checked first; if a certificate for the recipient doesn't exist in the GAL, Outlook queries the Microsoft publisher keychain in iOS or the system KeyStore in Android to locate the recipient's public certificate key. For recipients without a public certificate key (or an invalid key), Outlook prompts for their removal. The message is sent encrypted to any recipient unless the sender disables the encryption option during composition.

![Screenshot of Outlook for iOS warning about recipient certificates.](../../exchangeonline/media/sensitive-ios-no-cert-warning.png)