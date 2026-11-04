---
layout: Conceptual
title: Deprecation of Basic authentication in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/deprecation-of-basic-authentication-exchange-online
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
ms.author: srvar
f1.keywords:
- NOCSH
ms.topic: article
author: AshaIyengar21
ms.service: exchange-online
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid: MET150
description: Learn about deprecation of Basic authentication in Exchange Online
audience: Admin
ms.date: 2026-07-10T00:00:00.0000000Z
locale: en-us
document_id: 19cf826a-aaf1-91ed-8a8f-637d869e47df
document_version_independent_id: 61d69fb6-184d-acf5-8b02-39b3d885d28b
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/deprecation-of-basic-authentication-exchange-online.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/deprecation-of-basic-authentication-exchange-online
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/deprecation-of-basic-authentication-exchange-online.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 5ce2ec32-729d-a67b-27d7-987d839ef4cc
---

# Deprecation of Basic authentication in Exchange Online | Microsoft Learn

Important

Basic authentication is now disabled in all tenants.

Before December 31, 2022, you could re-enable the affected protocols if users and apps in your tenant couldn't connect. Now no one (you or Microsoft support) can re-enable Basic authentication in your tenant.

Read the rest of this article to fully understand the changes we made and how these changes might affect you.

For many years, applications have used Basic authentication to connect to servers, services, and API endpoints. Basic authentication simply means the application sends a username and password with every request, and those credentials are also often stored or saved on the device. Traditionally, Basic authentication is enabled by default on most servers or services, and is simple to set up.

Simplicity isn't at all bad, but Basic authentication makes it easier for attackers to capture user credentials (particularly if the credentials aren't protected by TLS), which increases the risk of those stolen credentials being reused against other endpoints or services. Furthermore, the enforcement of multifactor authentication (MFA) isn't simple or, in some cases, possible when Basic authentication remains enabled.

Basic authentication is an outdated industry standard. Threats posed by it have only increased since we originally announced that we were going to turn it off (see [Improving Security - Together](https://techcommunity.microsoft.com/t5/exchange-team-blog/improving-security-together/ba-p/805892)). There are better and more effective user authentication alternatives.

We actively recommend that customers adopt security strategies such as [Zero Trust](/en-us/security/zero-trust/) (Never Trust, Always Verify) or apply real-time assessment policies when users and devices access corporate information. These alternatives allow for intelligent decisions about who is trying to access what from where on which device rather than simply trusting an authentication credential that could be a bad actor impersonating a user.

With these threats and risks in mind, we took steps to improve data security in Exchange Online.

Note

The deprecation of basic authentication also prevents the use of app passwords with apps that don't support two-step verification.

## What we are changing

We removed the ability to use Basic authentication in Exchange Online for Exchange ActiveSync (EAS), POP, IMAP, Remote PowerShell (RPS), Exchange Web Services (EWS), Offline Address Book (OAB), Autodiscover, Outlook for Windows, and Outlook for Mac.

We also disabled SMTP AUTH in all tenants where it wasn't being used.

This decision requires customers to move from apps that use basic authentication to apps that use Modern authentication. Modern authentication (OAuth 2.0 token-based authorization) has many benefits and improvements that help mitigate the issues in basic authentication. For example, OAuth access tokens have a limited usable lifetime and are specific to the applications and resources for which they're issued; so they can't be reused. Enabling and enforcing MFA is also simple with Modern authentication.

## When did this change take place?

Beginning in early 2021, we started to disable Basic authentication for existing tenants with no reported usage.

Beginning in early 2023, we disabled Basic authentication for all tenants who had any type of extension. You can read more about the timing [here](https://techcommunity.microsoft.com/t5/exchange-team-blog/basic-authentication-deprecation-in-exchange-online-time-s-up/ba-p/3695312).

Note

In Office 365 Operated by 21Vianet, we began disabling Basic authentication on March 31, 2023. All other cloud environments were subject to the October 1, 2022, date.

## Impact to messaging protocols and existing applications

This change affects the applications and scripts you might use in different ways.

### POP, IMAP, and SMTP AUTH

In 2020, we released OAuth 2.0 support for POP, IMAP, and SMTP AUTH. Updates to some client apps have been implemented to support these authentication types (Thunderbird for example, though not yet for customers using Office 365 Operated by 21Vianet); so users with up-to-date versions can change their configuration to use OAuth. There's no plan for Outlook clients to support OAuth for POP and IMAP, but Outlook can connect using MAPI/HTTP (Windows clients) and EWS (Outlook for Mac).

Application developers who have built apps that send, read, or otherwise process email using these protocols will be able to keep the same protocol; however, they need to implement secure, Modern authentication experiences for their users. This functionality is built on top of [Microsoft identity platform v2.0](/en-us/entra/identity-platform/v2-overview) and supports access to Microsoft 365 email accounts.

If your in-house application needs to access IMAP, POP and SMTP AUTH protocols in Exchange Online, follow these step-by-step instructions to implement OAuth 2.0 authentication: [Authenticate an IMAP, POP, or SMTP connection using OAuth](/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth). Additionally, use the PowerShell script [Get-IMAPAccesstoken.ps1](https://github.com/DanijelkMSFT/ThisandThat/blob/main/Get-IMAPAccessToken.ps1) to test IMAP access after your OAuth enablement on your own in a simple way including the shared mailbox use case.

Although SMTP AUTH is currently available, Microsoft has announced plans to retire Basic authentication for SMTP AUTH in Exchange Online. As the retirement timeline has been updated, we recommend referring to the latest official announcement for current milestones and guidance:

https://techcommunity.microsoft.com/blog/exchange/updated-exchange-online-smtp-auth-basic-authentication-deprecation-timeline/4489835

Other options for sending authenticated mail include using alternative protocols, such as the [Microsoft Graph API](/en-us/graph/api/user-sendmail).

### Exchange ActiveSync (EAS)

Many users have mobile devices that are set up to use EAS. If they were using Basic authentication, they're affected by this change.

We recommend using [Outlook for iOS and Android](https://products.office.com/outlook-mobile-for-android-and-ios) when connecting to Exchange Online. Outlook for iOS and Android fully integrates Microsoft Enterprise Mobility + Security (EMS), which enables conditional access and app protection (MAM) capabilities. Outlook for iOS and Android helps you secure your users and your corporate data, and it natively supports Modern authentication.

There are other mobile device email apps that support Modern authentication. The built-in email apps for all popular platforms typically support Modern authentication, so sometimes the solution is to verify that your device is running the latest version of the app. If the email app is current, but is still using Basic authentication, you might need to remove the account from the device and then add it back.

If you're using [Microsoft Intune](/en-us/mem/intune/), you might be able to change the authentication type using the email profile you push or deploy to your devices. If you're using iOS devices (iPhones and iPads), you should take a look at [Add e-mail settings for iOS and iPadOS devices in Microsoft Intune](/en-us/mem/intune/configuration/email-settings-ios).

Any iOS device that's managed with Basic Mobility and Security won't be able to access email if the following conditions are true:

- You've configured a device security policy to require a managed email profile for access.
- You haven't modified the policy since November 9, 2021 (which means the policy is still using Basic authentication).

Policies created or modified after this date have already been updated to use Modern authentication.

To update policies that haven't been modified since November 9, 2021, to use Modern authentication, make a temporary change to the policy's access requirements. We recommend changing and saving the **Require Encrypted backups** cloud setting, which will upgrade the policy to use Modern authentication. Once the altered policy has the status value **Turned on**, the email profile has been upgraded. You may then revert the temporary change to the policy.

Note

During the upgrade process, the email profile will be updated on the iOS device and the user will be prompted to enter their username and password.

If your devices are using certificate-based authentication, they will be unaffected when Basic authentication is turned off in Exchange Online later this year. Only devices authenticating directly using Basic authentication will be affected.

Certificate-based authentication is still legacy authentication and as such will be blocked by Microsoft Entra Conditional Access policies that block legacy authentication. For more information, see [Block legacy authentication with Microsoft Entra Conditional Access](/en-us/entra/identity/conditional-access/block-legacy-authentication).

### Exchange Online PowerShell

Since the release of the Exchange Online PowerShell module, it's been easy to manage your Exchange Online settings and protection settings from the command line using Modern authentication. The module uses Modern authentication and works with MFA for connecting to all Exchange-related PowerShell environments in Microsoft 365: Exchange Online PowerShell and Security & Compliance PowerShell.

The Exchange Online PowerShell module can also be used non-interactively, which enables running unattended scripts. Certificate-based authentication provides admins the ability to run scripts without the need to create service-accounts or store credentials locally. To learn more, see [App-only authentication for unattended scripts in the Exchange Online PowerShell module](/en-us/powershell/exchange/app-only-auth-powershell-v2).

Important

Don't confuse the fact that PowerShell requires Basic authentication enabled for WinRM (on the local machine where the session is run from). The username/password isn't sent to the service using Basic, but the Basic Auth header is required to send the session's OAuth token because the WinRM client doesn't support OAuth. We're working on this problem and will have more to announce in the future. Just know that enabling Basic on WinRM *is not* using Basic to authenticate to the service. For more information, see [Exchange Online PowerShell: Turn on Basic authentication in WinRM](/en-us/powershell/exchange/exchange-online-powershell-v2#turn-on-basic-authentication-in-winrm).

Read more about this situation here: [Understanding the Different Versions of Exchange Online PowerShell Modules and Basic Auth](https://techcommunity.microsoft.com/t5/exchange-team-blog/understanding-the-different-versions-of-exchange-online/ba-p/3394487).

For details on moving from the V1 version of the module to the current version, see [this blog post](https://techcommunity.microsoft.com/t5/exchange-team-blog/moving-from-the-exchange-powershell-v1-module-to-the-v2-preview/ba-p/3450679).

Version 3.0.0 of the Exchange Online PowerShell V3 module (Preview versions 2.0.6-PreviewX) contains REST API-backed versions of all Exchange Online cmdlets that don't require Basic authentication in WinRM. For more information, see [Updates for version 3.0.0](/en-us/powershell/exchange/exchange-online-powershell-v2#updates-for-version-300-the-exo-v3-module).

### Exchange Web Services (EWS)

Many applications have been created using EWS for access to mailbox and calendar data.

In 2018, we announced that EWS would no longer receive feature updates and we recommended that application developers switch to using Microsoft Graph. See [Upcoming changes to Exchange Web Services (EWS) API for Office 365](https://techcommunity.microsoft.com/t5/exchange-team-blog/upcoming-changes-to-exchange-web-services-ews-api-for-office-365/ba-p/608055).

Many applications have successfully moved to Graph, but for those applications that haven't, it's noteworthy that EWS already fully supports Modern authentication. So if you can't migrate to Graph yet, you can switch to using Modern authentication with EWS, knowing that EWS will eventually be deprecated.

To learn more, see:

- [Upcoming API Deprecations in Exchange Web Services for Exchange Online - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/exchange-team-blog/upcoming-api-deprecations-in-exchange-web-services-for-exchange/ba-p/2813925)
- [Authenticate an EWS application by using OAuth](/en-us/exchange/client-developer/exchange-web-services/how-to-authenticate-an-ews-application-by-using-oauth)
- [What to do with EWS Managed API PowerShell scripts that use Basic Authentication](https://github.com/gscales/EWS-BasicToOAuth-Info/blob/main/What%20to%20do%20with%20EWS%20Managed%20API%20PowerShell%20scripts%20that%20use%20Basic%20Authentication.md)

### Outlook, MAPI, RPC, and Offline Address Book (OAB)

All versions of Outlook for Windows since 2016 have Modern authentication enabled by default; so it's likely that you're already using Modern authentication. Outlook Anywhere (formerly known as RPC over HTTP) has been deprecated in Exchange Online in favor of MAPI over HTTP. Outlook for Windows uses MAPI over HTTP, EWS, and OAB to access mail, set free/busy and out of office, and download the OAB. All of these protocols support Modern authentication.

Outlook 2007 or Outlook 2010 can't use Modern authentication and will eventually be unable to connect. Outlook 2013 requires a setting to enable Modern authentication, but once you configure the setting, Outlook 2013 can use Modern authentication with no issues. As announced earlier here, Outlook 2013 requires a minimum update level to connect to Exchange Online. See [New minimum Outlook for Windows version requirements for Microsoft 365](https://techcommunity.microsoft.com/t5/microsoft-365-blog/new-minimum-outlook-for-windows-version-requirements-for/ba-p/2684142).

Outlook for Mac supports Modern Authentication.

For more information about Modern authentication support in Office, see [How modern authentication works for Office client apps](/en-us/office365/enterprise/modern-auth-for-office-2013-and-2016).

If you need to migrate Public Folders to Exchange online, see [Public Folder Migration Scripts with Modern Authentication Support](https://techcommunity.microsoft.com/t5/exchange-team-blog/announcing-public-folder-migration-scripts-with-modern/ba-p/3382800).

### Autodiscover

In November 2022, we [announced](https://techcommunity.microsoft.com/t5/exchange-team-blog/basic-authentication-deprecation-in-exchange-online-what-s-next/ba-p/3678143) we would disable Basic authentication for the Autodiscover protocol once EAS and EWS are disabled in a tenant.

## Client options

Some of the options available for each of the impacted protocols are listed below.

### Protocol recommendation

For EWS, Remote PowerShell, POP and IMAP, and EAS:

- **If you have written your own code using these protocols**, update your code to use **OAuth 2.0** instead of Basic authentication, or migrate to a newer protocol (Graph API).
- **If you or your users are using a third-party application which uses these protocols**, reach out to the third-party app developer who supplied this application to update it to support OAuth 2.0 authentication or assist your users to switch to an application that's built using OAuth 2.0.

| Key Protocol Service | Impacted Clients | Client Specific Recommendation | Special Recommendation for Office 365 Operated by 21Vianet (Gallatin) | Other Protocol Info / Notes |
| --- | --- | --- | --- | --- |
| Outlook | All versions of Outlook for Windows and Mac | - Upgrade to Outlook 2013 or later for Windows and to Outlook 2016 or later for Mac<br>- If you're using Outlook 2013 for Windows, turn on modern auth through the [registry key](/en-us/office365/admin/security-and-compliance/enable-modern-authentication) |  | [Enabling Modern Auth for Outlook – How Hard Can It Be?](https://techcommunity.microsoft.com/t5/exchange-team-blog/enabling-modern-auth-for-outlook-how-hard-can-it-be/ba-p/2278411) |
| Exchange Web Services (EWS) | Third-party applications not supporting OAuth | - Modify app to use Modern authentication.<br>- Migrate app to use Graph API and Modern authentication.<br><br><br> Popular Apps: <br><br>- Microsoft Teams Rooms: Enable Modern authentication by following the steps in [Authentication in Microsoft Teams Rooms](/en-us/MicrosoftTeams/rooms/rooms-authentication#prerequisites-specific-to-microsoft-teams-rooms)<br>- Dynamics 365 / PowerApps: [Use of Basic authentication with Exchange Online](/en-us/power-platform/admin/use-basic-authentication-exchange-online)<br>- Cisco Unity: [Cisco Unity Connection Service Bulletin for Unified Messaging with Microsoft Office 365 Product Bulletin](https://www.cisco.com/c/en/us/products/collateral/unified-communications/unified-communications-manager-callmanager/bulletin-c25-743410.html) | [Follow this article to migrate your customized Gallatin application to use EWS with OAuth](https://mp.weixin.qq.com/s/sfQs0NTCxray6b81j8Xt4Q)Microsoft Teams and Cisco Unity not currently available in Gallatin | [What to do with EWS Managed API PowerShell scripts that use Basic Authentication](https://github.com/gscales/EWS-BasicToOAuth-Info/blob/main/What%20to%20do%20with%20EWS%20Managed%20API%20PowerShell%20scripts%20that%20use%20Basic%20Authentication.md)- No EWS feature updates starting July 2018 |
| Remote PowerShell (RPS) | - Exchange administrators<br>- [Delegated Admin Privileges](/en-us/partner-center/customers-revoke-admin-privileges)<br>- Automated management tools | Use either: <br>- [Exchange Online PowerShell module](/en-us/powershell/exchange/exchange-online-powershell-v2).<br>- [PowerShell within Azure Cloud Shell](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/Azure-Cloud-Shell-Now-Supports-Exchange-Online/ba-p/652269). | Azure Cloud Shell isn't available in Gallatin | Learn more about [Automation and certificate-based authentication support for the Exchange Online PowerShell module](/en-us/powershell/exchange/app-only-auth-powershell-v2) and [Understanding the Different Versions of Exchange Online PowerShell Modules and Basic Auth](https://techcommunity.microsoft.com/t5/exchange-team-blog/understanding-the-different-versions-of-exchange-online/ba-p/3394487). |
| POP and IMAP | Third-party mobile clients such as Thunderbird first-party clients configured to use POP or IMAP | Recommendations: <br>- Move away from these protocols as they don't enable full features.<br>- Move to OAuth 2.0 for POP/IMAP when your client app supports it. | [Follow this article to configure POP and IMAP with OAuth in Gallatin with sample code](https://mp.weixin.qq.com/s/Uwd6AkL1_KPoJ8XoXBMU-Q) | IMAP is popular for Linux and education customers. OAuth 2.0 support started rolling out in April 2020. [Authenticate an IMAP, POP, or SMTP connection using OAuth](/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth) |
| Exchange ActiveSync (EAS) | Mobile email clients from Apple, Samsung and so on | - Move to Outlook for iOS and Android or another mobile email app that supports Modern authentication<br>- Update the app settings if it can do OAuth but the device is still using Basic<br>- Switch to Outlook on the web or another mobile browser app that supports Modern authentication<br><br><br> Popular Apps: <br><br>- Apple iPhone/iPad/macOS: All up-to-date iOS/macOS devices are capable of using Modern authentication; just remove and add back the account.<br>- Microsoft Windows 10 Mail client: Remove and add back the account, choosing Office 365 as the account type | - Apple's native mail app on iOS doesn't currently work in Gallatin; we recommend you use Outlook mobile<br>- Windows 10/11 Mail app isn't supported with Gallatin<br>- [Follow this article to configure EAS with OAuth and sample code](https://mp.weixin.qq.com/s/-SAezFkdmYO5dnPHBUFH-A) | Mobile devices that use a native app to connect to Exchange Online generally use this protocol |
| Autodiscover | EWS and EAS apps using Autodiscover to find service endpoints | - Upgrade code/app to one supporting OAuth |  | [Autodiscover web service reference for Exchange](/en-us/exchange/client-developer/web-service-reference/autodiscover-web-service-reference-for-exchange) |

### Resources

To learn more, check out the following articles:

**Security Defaults**:

- [Security defaults in Microsoft Entra ID](/en-us/entra/fundamentals/security-defaults)
- [Enabling Security Defaults](/en-us/entra/fundamentals/security-defaults#enabling-security-defaults)

**Exchange Online Authentication Policies**:

- [Manage Basic Authentication in the Microsoft 365 Admin Center (Simple)](/en-us/exchange/clients-and-mobile-in-exchange-online/disable-basic-authentication-in-exchange-online#manage-basic-authentication-in-the-microsoft-365-admin-center)
- [Authentication Policy Procedures in Exchange Online (Advanced)](/en-us/exchange/clients-and-mobile-in-exchange-online/disable-basic-authentication-in-exchange-online#authentication-policy-procedures-in-exchange-online)

**Microsoft Entra Conditional Access**:

- [Common Conditional Access policy: Block legacy authentication (Simple)](/en-us/entra/identity/conditional-access/howto-conditional-access-policy-block-legacy)
- [Block legacy authentication with Microsoft Entra Conditional Access (Detailed)](/en-us/entra/identity/conditional-access/block-legacy-authentication)