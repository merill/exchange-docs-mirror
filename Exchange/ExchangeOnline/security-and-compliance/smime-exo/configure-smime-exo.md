---
layout: Conceptual
title: Configure S/MIME in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/smime-exo/configure-smime-exo
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: serdars
author: serdars
ms.date: 2021-05-07T00:00:00.0000000Z
audience: ITPro
ms.topic: how-to
ms.localizationpriority: medium
search.appverid:
- MET150
ms.assetid: 887c710b-0ec6-4ff0-8065-5f05f74afef3
description: Admins can learn about the basic steps for configuring S/MIME in Exchange Online for message encryption and digitally signed messages.
ms.custom: seo-marvel-apr2020
ms.service: exchange-online
locale: en-us
document_id: 0db0df87-55f0-94ec-70a9-1448fecf0643
document_version_independent_id: e3e3f11b-ca34-e57c-e7b7-6d7bf0848028
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/smime-exo/configure-smime-exo.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/smime-exo/configure-smime-exo
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/smime-exo/configure-smime-exo.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 9e73aa0d-a283-33e2-14dd-ea51c0c40227
---

# Configure S/MIME in Exchange Online | Microsoft Learn

S/MIME (Secure/Multipurpose Internet Mail Extensions) is a widely accepted protocol for sending digitally signed and encrypted messages. For more information, see [S/MIME for message signing and encryption in Exchange Online](smime-exo).

S/MIME is available in Exchange Online with the following types of email clients:

- [Supported versions of Outlook](/en-us/deployoffice/endofsupport/office-365-services-connectivity).
- Outlook on the web (formerly known as Outlook Web App) **on Windows clients**. For more information, see [Encrypt messages by using S/MIME in Outlook on the web](https://support.microsoft.com/office/878c79fc-7088-4b39-966f-14512658f480).

    Note

    Sensitive policy actions are applied on the server backend, while S/MIME signing and/or encryption is done in the Outlook on the web client. Because of this architectural constraint, S/MIME is disabled in Outlook on the web in messages where there are sensitivity labels with protection actions.
- Mobile devices (for example, Outlook for iOS and Android, Exchange ActiveSync apps or native email apps).

As an Exchange Online admin, you can enable S/MIME-based security for the mailboxes in your organization. The high-level steps are described in the following list and are expanded upon in this article:

1. Set up and publish S/MIME certificates.
2. Set up a virtual certificate collection in Exchange Online.
3. Sync user certificates for S/MIME into Microsoft 365.
4. Configure policies to install S/MIME extensions in web browsers for Outlook on the web.
5. Configure email clients to use S/MIME.

For end-to-end S/MIME configuration instructions for Outlook for iOS and Android, see [S/MIME for Outlook for iOS and Android](../../clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/smime-outlook-for-ios-and-android).

## Step 1: Set up and publish S/MIME certificates

Each user in your organization requires their own certificate that's issued for the purposes of signing and encryption. You publish these certificates to your on-premises Active Directory for distribution. Your Active Directory must be located on computers at a physical location that you control and not at a remote facility or cloud-based service on the internet.

For more information about Active Directory, see [Active Directory Domain Services Overview](/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview).

1. Install a Windows-based Certification Authority (CA) and set up a public key infrastructure to issue S/MIME certificates. Certificates issued by third-party certificate providers are also supported. For details, see [Active Directory Certificate Services Overview](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740%28v=ws.11%29).

    **Notes**:

    - Certificates issued by a third-party CA have the advantage of being automatically trusted by all clients and devices. Certificates that are issued by an internal, private CA aren't automatically trusted by clients and devices, and not all devices (for example, phones) can be configured to trust private certificates.
    - Consider using an intermediate certificate instead of the root certificate to issue certificates to users. That way, if you ever need to revoke and reissue certificates, the root certificate is still intact.
    - The certificate must have a private key and the X509 extension "Subject Key Identifier" must be populated.
2. Publish the user's certificate in their on-premises Active Directory account in the **UserSMIMECertificate** and/or **UserCertificate** attributes.

### Step 2: Set up a virtual certificate collection in Exchange Online

The virtual certificate collection is responsible for validating S/MIME certificates. Set up the virtual certificate collection by using the following steps:

1. Export the root and intermediate certificates that are required to validate user S/MIME certificates from a trusted machine to a serialized certificate store (SST) file in Windows PowerShell. For example:

    ```powershell
    Get-ChildItem -Path cert:\<StoreCertPath> | Export-Certificate -FilePath "C:\My Documents\Exported Certificate Store.sst" -Type SST
    ```

    For detailed syntax and parameter information, see [Export-Certificate](/en-us/powershell/module/pki/export-certificate).
2. Import the certificates from the SST file into Exchange Online by running the following command in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell):

    ```PowerShell
    Set-SmimeConfig -SMIMECertificateIssuingCA ([System.IO.File]::ReadAllBytes('C:\My Documents\Exported Certificate Store.sst'))
    ```

    For detailed syntax and parameter information, see [Set-SmimeConfig](/en-us/powershell/module/exchangepowershell/set-smimeconfig).

## Step 3: Sync user certificates for S/MIME into Microsoft 365

Before anyone can send S/MIME-protected messages in Exchange Online, you need to set up and configure the appropriate certificates for each user **and** publish their public X.509 certificates to Microsoft 365. The sender's email client uses the recipient's public certificate to encrypt the message.

1. Issue certificates and publish them in your local Active Directory. For more information, see [Active Directory Certificate Services Overview](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740%28v=ws.11%29).
2. After your certificates are published, use Microsoft Entra Connect to synchronize user data from your on-premises Exchange environment to Microsoft 365. For more information on this process, see [Microsoft Entra Connect Sync: Understand and customize synchronization](/en-us/azure/active-directory/hybrid/how-to-connect-sync-whatis).

Along with synchronizing other directory data, Microsoft Entra Connect synchronizes the **userCertificate** and **userSMIMECertificate** attributes for each user object for S/MIME signing and encryption of email messages. For more information about Microsoft Entra Connect, see [What is Microsoft Entra Connect?](/en-us/azure/active-directory/hybrid/whatis-azure-ad-connect).

## Step 4: Configure policies to install the S/MIME extensions in web browsers

Note

This step is required only for Outlook on the web clients.

S/MIME in Outlook on the web in the Chromium-based [Microsoft Edge](https://www.microsoft.com/windows/microsoft-edge) or in Google Chrome requires specific policy settings that are configured by an admin.

Specifically, you need to set and configure the policy named **ExtensionInstallForcelist** to install the S/MIME extension in the browser. The policy value is `maafgiompdekodanheihhgilkjchcakm;https://outlook.office.com/owa/SmimeCrxUpdate.ashx`. Applying this policy requires domain-joined or Microsoft Entra joined devices, so using S/MIME in Edge or Chrome effectively requires domain-joined or Microsoft Entra joined devices.

To elaborate, `maafgiompdekodanheihhgilkjchcakm` is the extension id for S/MIME managed extension.

To ensure that the correct S/MIME extention is fetched for update, it's important to also add below defined policy - `override_update_url = 1 (DWORD)`. This should be added under the defined path in - `ExtensionSettings\maafgiompdekodanheihhgilkjchcakm`.

For details about the policies, see the following topics:

- [ExtensionInstallForcelist - Edge](/en-us/deployedge/microsoft-edge-policies#extensioninstallforcelist)
- [ExtensionInstallForcelist - Chrome](https://chromeenterprise.google/policies/?policy=ExtensionInstallForcelist)
- [ExtensionSettings - Edge](/en-us/deployedge/microsoft-edge-manage-extensions-ref-guide)
- [ExtensionSettings - Chrome](https://chromeenterprise.google/policies/?policy=ExtensionSettings)

The policy is a prerequisite for using S/MIME in Outlook on the web. It **does not replace** the S/MIME control that's installed by users. Users are prompted to download and install the S/MIME control in Outlook on the web during their first use of S/MIME. Or, users can proactively go to **S/MIME** in their Outlook on the web settings to get the download link for the control.

## Step 5: Configure email clients to use S/MIME

If an email client supports S/MIME, the next consideration is access to the user's S/MIME certificate by that email client. The S/MIME certificate needs to be installed on the user's computer or device. You can distribute S/MIME certificates automatically (for example, using [Microsoft Endpoint Manager](/en-us/mem/endpoint-manager-overview)) or manually (for example, the user can export the certificate from their computer and import it on their mobile device). After the certificate is available locally, you can enable and configure S/MIME in the settings of the email client.

For more information about S/MIME in email clients, see the following topics:

- **Outlook**: See the "Encrypting with S/MIME" section in [Encrypt email messages](https://support.microsoft.com/office/373339cb-bf1a-4509-b296-802a39d801dc).
- **Outlook for iOS and Android**: [Enabling S/MIME in the client](../../clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/smime-outlook-for-ios-and-android#enabling-smime-in-the-client)
- **Mail in iOS**: [Use S/MIME to send encrypted messages in an Exchange environment in iOS](https://support.apple.com/HT202345)

You can also use the following parameters on the [New-MobileDeviceMailboxPolicy](/en-us/powershell/module/exchangepowershell/new-mobiledevicemailboxpolicy) and [Set-MobileDeviceMailboxPolicy](/en-us/powershell/module/exchangepowershell/set-mobiledevicemailboxpolicy) cmdlets in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) to configure S/MIME settings for mobile devices:

- *AllowSMIMEEncryptionAlgorithmNegotiation*
- *AllowSMIMESoftCerts*
- *RequireEncryptedSMIMEMessages*
- *RequireEncryptionSMIMEAlgorithm*
- *RequireSignedSMIMEAlgorithm*
- *RequireSignedSMIMEMessages*