---
layout: Conceptual
title: Troubleshoot issues with high volume email for Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/troubleshoot-high-volume-email-m365
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.author: serdars
ms.topic: troubleshooting-general
author: serdars
ms.service: exchange-online
ms.assetid: e1da5f2f-c732-4010-85c9-878b2cef3fb3
ms.collection:
- exchange-online
- M365-email-calendar
description: Learn how to troubleshoot issues with high volume email for Microsoft 365.
f1.keywords:
- NOCSH
ms.reviewer: simone.liebal
audience: ITPro
ms.date: 2026-04-17T00:00:00.0000000Z
locale: en-us
document_id: 77ef8d27-59d7-174d-2f26-4686748522f2
document_version_independent_id: 81e0863e-97f1-7911-b120-de3b756139fd
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/troubleshoot-high-volume-email-m365.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/troubleshoot-high-volume-email-m365
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/troubleshoot-high-volume-email-m365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 82894588-c16d-a547-0756-f68b01a97fa3
---

# Troubleshoot issues with high volume email for Microsoft 365 | Microsoft Learn

## Issue: I set up my printer or LOB app for HVE, but it still can't send email

1. Verify the settings that were entered directly into the printer are correct:

    | Printer setting | Value |
    | --- | --- |
    | Server/smart host | smtp.hve.mx.microsoft (recommended) or smtp-hve.office365.com (will be deprecated in the future) |
    | Port | Port 587 |
    | TLS/StartTLS | Enabled |
    | Authentication | HVE account credentials or OAuth token |
2. Depending on your chosen authentication, check if HVE account credentials are correct or OAuth token is valid.
3. Validate that your HVE account and service is working correctly. You can use SMTP component in the Power Automate platform: [SMTP - Connectors](/en-us/connectors/smtp/).

## Error: Authentication unsuccessful

If you receive one of the following errors:

- 535 5.7.3 Authentication unsuccessful
- 535 5.7.139 Authentication unsuccessful, the organization configuration doesn't allow this authentication request.

1. Disable the Azure Security Defaults by toggling the **Enable Security Defaults** to **No**:
    1. Sign in to the Azure portal as a Security administrator or Conditional Access administrator.
    2. Navigate to **Microsoft Entra ID** &gt; **Properties**.
    3. Select **Manage security defaults**.
    4. Set the **Enable security defaults** toggle to **No**.
    5. Select **Save**.
2. HVE accounts can operate even if [SMTPClientAuthenticationDisabled](/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission) is set to True within TransportConfig due to the use of a custom endpoint.
3. To avoid any impact from authentication policies, if these are being utilized, it's important for customers to ensure AllowBasicAuthSmtp is enabled in the policy that applies to the HVE account. Custom [authentication policies](/en-us/exchange/clients-and-mobile-in-exchange-online/disable-basic-authentication-in-exchange-online) can be applied to the HVE accounts as needed.

## Troubleshoot billing‑related issues

High Volume Email uses M365 pay‑as‑you‑go billing. If an HVE account doesn’t have a valid billing policy assigned, or if there’s an issue with the associated Azure subscription, the account cannot send email.

Note

**High Volume Email billing will begin June 1st, 2026**. Until then, usage will not be billed. Billing policies can be configured beforehand, but they will only become **required starting June 1, 2026**, when usage billing begins.

You can view billing status and errors for HVE accounts in the **Exchange admin center** on the **High Volume Email** page or by viewing the billing policy associated with a specified HVE account using the **Exchange Online PowerShell**.

- On the High Volume Email page in the Exchange admin center, billing policy information for each HVE account is shown in the **Billing policy** column.
- In Exchange Online PowerShell, the `BillingPolicyStatus` property returned by `Get-HVEAccountBillingPolicy` reflects the billing status of the HVE account. If an issue exists, the `FailureReason` property provides additional details about the billing policy or associated subscription.

The following table shows how billing policy states are represented in the Exchange admin center and Exchange Online PowerShell, along with their underlying causes:

| Exchange Admin Center (Billing policy column) | Exchange Online PowerShell (BillingPolicyStatus) | Description |
| --- | --- | --- |
| Name of the billing policy | `BillingPolicyValid` | A valid billing policy is assigned and the subscription is active. |
| "Connect a policy" link | `NoProperBillingPolicyStored` | No billing policy is assigned to the account. |
| Policy deleted | `BillingPolicyNotFound` | The assigned billing policy no longer exists. |
| N/A | `BillingPolicyMismatched` | The billing policy retrieved doesn’t match the expected tenant or policy identity. This is an uncommon scenario. |
| Policy disconnected from service | `NoConnectedBillingPolicyFound` | The billing policy isn’t connected to High Volume Email. |
| Subscription inactive or deleted | `SubscriptionIsNotActive` | The subscription linked to the billing policy isn’t active. |
| N/A | `NoSPOLicenseFound` | No SharePoint Online license is available for the tenant, preventing billing policy validation. |

## Troubleshoot OAuth authentication issues for High Volume Email

With the support of OAuth authentication for High Volume Email, clients can now significantly enhance the security of their email operations. This article can help you troubleshoot authentication failures during the authentication stage.

As a first step to fixing any problems, check your configuration. See [OAuth authentication for high volume emails for Microsoft 365](oauth-high-volume-mails-m365) for the configuration options.

### I received an authentication error when trying to authenticate with OAuth2

This error can be caused by different factors:

- Expired Tokens: The token used for authentication or authorization may have expired.
- Invalid Token: The format of the token doesn't match the OAuth2 format.
- Incorrect API permissions: The API permission type mismatch causing OAuth2 failure occurs when the scopes or permissions requested by the client application don't align with the permissions configured or allowed on the authorization server.

## OAuth SMTP Error Codes and Resolutions

This section provides explanation for common OAuth SMTP error codes and offers guidance on how to resolve them. If you encounter any of the following error codes, follow the recommended steps to address the issue.

| Error Code | Description | Resolution |
| --- | --- | --- |
| **501 5.5.121** | Invalid XOAUTH2 argument. | Ensure that the authentication data after XOAUTH2 is encoded correctly in base64 format. |
| **501 5.5.122** | Invalid XOAUTH2 auth data. For example: the following format for auth data is incorrect: `auth=Bearer^Auser=EmailAddress OauthToken^A^A` | Ensure that the auth data encoded into base64 follows the format (angled brackets are used as placeholders):`user=EmailAddress^Aauth=Bearer OauthToken^A^A` |
| **501 5.5.123** | Invalid XOAUTH2 auth data - No user address provided. For example: User email address is absent: `user=^Aauth=Bearer OauthToken^A^A` | Ensure that the auth data encoded into base64 follows the format (angled brackets are used as placeholders):`user=EmailAddress^Aauth=Bearer OauthToken^A^A` |
| **501 5.5.124** | Invalid XOAUTH2 auth data - User address provided isn't valid. For example: User email address is invalid `user=InvalidEmailAddress^Aauth=Bearer OauthToken^A^A` | Ensure that the auth data encoded into base64 follows the format (angled brackets are used as placeholders):`user=EmailAddress^Aauth=Bearer OauthToken^A^A` |
| **501 5.5.125** | Invalid XOAUTH2 auth data - Auth type data absent. For example: `Bearer` keyword is absent from the auth data `user=EmailAddress^Aauth= OauthToken^A^A` | Ensure that the auth data encoded into base64 follows the format (angled brackets are used as placeholders):`user=EmailAddress^Aauth=Bearer OauthToken^A^A` |
| **501 5.5.126** | Invalid XOAUTH2 auth data - Auth token absent. For example: `OauthToken` string is absent from the auth data `user=EmailAddress^Aauth=Bearer ^A^A` | Ensure the auth data encoded into base64 follows the format (angled brackets are used as placeholders):`user=EmailAddress^Aauth=Bearer OauthToken^A^A` |
| **535 5.7.127** | Authentication unsuccessful | This is a generic authentication failure scenario. Refer to the document [OAuth authentication for high volume emails for Microsoft 365](oauth-high-volume-mails-m365) for the recommended setup. |
| **535 5.7.142** | XOAUTH2 authentication failed. Token will expire soon. | Ensure that the session time doesn't exceed the token expiry time. Obtain a new OAuth token if possible. |
| **535 5.7.143** | XOAUTH2 authentication failed. Expired token. | Check if the token is still valid, regenerate the user token to ensure the token is valid. |
| **535 5.7.144** | XOAUTH2 authentication failed. Invalid API permissions. | Follow the document [OAuth authentication for high volume emails for Microsoft 365](oauth-high-volume-mails-m365) to check the configured permissions under API Permission section. |
| **550 5.7.240** | The application is not allowed for use with this High Volume Email account. | Ensure the application is on the allowed applications list for this High Volume Email account. For more information on allowed applications, see [OAuth authentication for high volume emails for Microsoft 365](oauth-high-volume-mails-m365). |

For more information on SMTP error codes, see [Email non-delivery reports and SMTP errors in Exchange Online](/en-us/troubleshoot/exchange/email-delivery/ndr/non-delivery-reports-in-exchange-online).