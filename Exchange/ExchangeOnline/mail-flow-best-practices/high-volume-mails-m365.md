---
layout: Conceptual
title: Manage High Volume Email for Microsoft 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/high-volume-mails-m365
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
ms.topic: how-to
author: serdars
ms.service: exchange-online
ms.assetid: e1da5f2f-c732-4010-85c9-878b2cef3fb3
ms.collection:
- exchange-online
- M365-email-calendar
description: Learn how to manage High Volume Email for Microsoft 365 in Exchange Online.
f1.keywords:
- NOCSH
ms.reviewer: mgolda
audience: ITPro
ms.date: 2026-04-17T00:00:00.0000000Z
locale: en-us
document_id: f0a13d7b-dda7-b6de-ce0e-c76a2efd70d4
document_version_independent_id: a6c1c797-72fd-a007-30d4-ea64f50b6d87
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mail-flow-best-practices/high-volume-mails-m365.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mail-flow-best-practices/high-volume-mails-m365
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mail-flow-best-practices/high-volume-mails-m365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: ab0bb841-c70f-4c18-1bc3-3e06ecc52247
---

# Manage High Volume Email for Microsoft 365 | Microsoft Learn

## What is High Volume Email?

High Volume Email (HVE) in Exchange Online enables applications and devices to send large volumes of internal email without affecting user mailboxes or overall service health. HVE is designed for automated, transactional and operational messaging. It uses dedicated HVE accounts instead of user or shared mailboxes, ensuring that application and device‑generated email is clearly separated from user mailboxes and can be managed independently.

**Common scenarios include:**

- Payroll and HR system notifications
- IT monitoring and service alerts
- Line‑of‑business application messaging
- Device‑generated email (for example, printers and scanners)
- Security and compliance notifications

The following table compares the available options for sending email from applications or devices using Microsoft 365 or Office 365:

| Features | SMTP client submission | SMTP relay | High Volume Email |
| --- | --- | --- | --- |
| Send to recipients in your domain(s) | Yes | Yes | Yes |
| Relay to internet via Microsoft 365 or Office 365 | Yes | Yes | No |
| Bypasses antispam | Yes, if the mail is destined for one of your Microsoft 365 or Office 365 mailboxes. | No. Suspicious emails might be filtered. We recommend a custom SPF record. | Yes, if the mail is destined for one of your Microsoft 365 or Office 365 mailboxes. |
| Supports mail sent from third‑party hosted applications | Yes | No | Yes |
| Saves to Sent Items folder | Yes | No | No |
| Service endpoint | smtp.office365.com | Tenant MX endpoint (for example, contoso-com.mail.protection.outlook.com) | smtp.hve.mx.microsoft (recommended) or smtp-hve.office365.com (will be deprecated in the future) |
| Network port | Port 587 or port 25 | Port 25 | Port 587 |
| TLS required | Required | Optional | Required |
| Authentication method | Microsoft 365 or Office 365 user credentials | Static IP address(es) | HVE account credentials or OAuth token |

For detailed comparison, see [How to set up a multifunction device or application to send email using Microsoft 365](how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365).

## Limitations and best practices

The following limits and recommendations apply to High Volume Email. Review them carefully when planning and configuring HVE.

### Service limits

| Limit | Value |
| --- | --- |
| **Recipient rate limit** | None |
| **Message rate limit** | None |
| **HVE accounts per tenant** | Up to 100 HVE accounts |
| **Recipients per message** | Up to 50 recipients |
| **Maximum message size** | 10 MB |
| **Recipient scope** | Internal recipients within the tenant only |
| **Connection limits** | Up to 100 concurrent connections per IP address, or up to 250 authenticated connections per tenant |

### Supported cloud environments

- High Volume Email is supported in **Microsoft 365 Worldwide (standard multi-tenant)** environments.
- Support for additional cloud environments is under evaluation and will be communicated as information becomes available.

### Unsupported scenarios

- Adding HVE accounts to **distribution lists** or **mail‑enabled security groups** is not supported.
- HVE accounts cannot be used for external email delivery.
- HVE account does not have a mailbox and cannot receive email. If recipients need to reply to messages sent by an HVE account, configure a **Reply-To address** for the account. Replies are then delivered to the specified mailbox instead of the HVE account. You can configure the **Reply‑To address** in the HVE account settings. For more information, see [PowerShell management for High Volume Email accounts](high-volume-mails-m365#powershell-management-for-high-volume-email-accounts).

### Best practices

- **Use HVE accounts for automated messaging from devices or applications.**
    - HVE accounts are mail‑enabled user objects intended specifically for application or device‑generated email.
- **Do not assign licenses to HVE accounts.**
    - HVE accounts do not require Microsoft 365 licenses and shouldn’t be treated as user mailboxes.
- **Separate workloads by HVE account.**
    - Create multiple HVE accounts to isolate applications, environments, or business workflows.
- **Use OAuth authentication when possible.**
    - OAuth provides stronger security and better alignment with modern authentication practices. For more information, see [OAuth authentication for High Volume Emails for Microsoft 365](oauth-high-volume-mails-m365).
- **Email sending best practices**
    - **You know your recipients and they’re relatively stable:** Use a **static (flat) distribution list** to manage recipients and send messages to a single recipient: the distribution list. Distribution lists can help you manage the **50 recipients per message** limit. However, for **billing purposes**, recipients are counted **after distribution list expansion**.
    - **You have many recipients and the membership changes frequently:** Use **Active Directory attributes** with a **dynamic distribution list** to manage recipients automatically. Send messages to a single recipient (the dynamic distribution list) to simplify recipient management while keeping distribution up to date. As with static distribution lists, recipients are **billed after expansion**.
    - **You can’t rely on distribution lists:** Send messages directly to a flat list of recipients, batching messages to stay within the **maximum of 50 recipients per email message**.

## Plan for Billing for High Volume Email

High Volume Email uses [M365 pay as you go (PAYG) billing](/en-us/microsoft-365/commerce/services/pay-as-you-go-overview). When you use a Microsoft pay-as-you-go service linked to an Azure subscription, the service gets billed using the Azure subscription that you specify when you set up billing. The following table describes the service, its pricing, and how it measures usage.

| **Service** | **What's counted?** | **What's billed? (USD)** |
| --- | --- | --- |
| High Volume Email | Number of expanded delivered email recipients | $0.000042 per one recipient (equivalent to $42 per one million recipients) |

## Set up Billing for High Volume Email

As High Volume Email uses **M365 pay as you go (PAYG) billing**, each HVE account must be associated with a **billing policy**, which links the account to an Azure subscription for usage based billing. Without an assigned billing policy, an HVE account **cannot send email**.

Note

Each High Volume Email account can have one billing policy assigned. A single billing policy can be shared by multiple High Volume Email accounts, allowing you to group accounts under the same Azure subscription.

### Prerequisites

Before you assign a billing policy to an HVE account, ensure that **Microsoft 365 pay as you go billing is set up for your tenant**:

- Learn more about [M365 pay as you go billing](/en-us/microsoft-365/commerce/services/pay-as-you-go-overview).
- Learn how to [set up M365 pay as you go billing](/en-us/microsoft-365/commerce/services/pay-as-you-go-setup-billing-node) and connect an Azure subscription.

Once M365 pay-as-you-go billing is configured and you created a billing policy, connect it to the **High Volume Email service** in the Microsoft 365 admin center.

[![Screenshot of connecting High Volume Email service in M365 Admin Center.](../exchangeonline/media/hve-m365/hve-main-11.png)](../exchangeonline/media/hve-m365/hve-main-11.png#lightbox)

### Assign a billing policy to an HVE account

You can assign a billing policy when creating a new HVE account or update an existing account later. Billing policy assignment can be done by using either the **Exchange admin center** or **Exchange Online PowerShell**:

- To create an HVE account by using the Exchange admin center, see Create an HVE account.
- The assign or update a billing policy for an existing HVE account in Exchange admin center, see Update an existing HVE account.
- To manage billing policies by using PowerShell, see PowerShell management for High Volume Email accounts.

### Billing related account states

On the **High Volume Email** page in the **Exchange admin center**, billing information for each HVE account is shown in the **Billing policy** and **Account status** columns.

**Billing policy column**

The Billing policy column shows the current billing policy information for each HVE account, which will be one of the below options:

| Billing policy column value | Description |
| --- | --- |
| **Connect a billing policy** | No billing policy is assigned. Select the link to start the assignment process. |
| **Billing policy name** | A billing policy is assigned and valid. |
| **❌ Error message** | There’s an issue with the assigned billing policy (for example, the policy is deleted, disconnected, or linked to an inactive subscription). |
| **Refresh** | Billing policy information could not be loaded. Select **Refresh** to reload the policy assignment for that specific account. |

**Account status column**

The Account status column reflects whether an HVE account can send email based on its billing configuration:

| Account status column value | Description |
| --- | --- |
| **Active** | A valid billing policy is assigned to the account. The HVE account is ready to send email. |
| **Not active** | No billing policy is assigned, or there’s an issue with the assigned policy. The HVE account will not be able to send email, until a valid policy is assigned. |

### Troubleshooting billing issues

If an HVE account shows an error related to billing policy assignment, see [Troubleshoot issues with High Volume Email for Microsoft 365](troubleshoot-high-volume-email-m365) for detailed guidance.

## Get started with High Volume Email service

### Create an HVE account

HVE accounts can be created by using the Exchange admin center or Exchange Online PowerShell. The following steps describe creation in the Exchange admin center. For PowerShell, see [PowerShell management for High Volume Email accounts](high-volume-mails-m365#powershell-management-for-high-volume-email-accounts).

1. Go to the **Exchange admin center** at https://admin.exchange.microsoft.com/.
2. In the left navigation, select **Mail flow**, and then select **High Volume Email**.
3. Select **Add an HVE account**.

    [![Screenshot of High Volume Email page.](../exchangeonline/media/hve-m365/hve-main-8.png)](../exchangeonline/media/hve-m365/hve-main-8.png#lightbox)
4. On the **Add HVE account** page, provide the following information:

    - **Display name** – A friendly name to help you identify the HVE account.
    - **Primary email address** – Must use a domain that’s accepted in your tenant (for example, hve-app@contoso.com).
    - **Alias** (optional)
    - **Password** – Used for SMTP authentication if you choose to use basic authentication. Verify that the password complies with the password length, complexity, and history requirements of your organization.

    [![Screenshot of adding a new HVE account](../exchangeonline/media/hve-m365/hve-main-7.png)](../exchangeonline/media/hve-m365/hve-main-7.png#lightbox)
5. Select **Next**, and on the **Pay-as-you-go billing policy** step select a **billing policy** from the drop-down menu. Please note, that this is an optional step in the account creation process. A billing policy can also be assigned later, after the account was created.

    [![Screenshot of Pay-as-you-go billing policy page for adding a new HVE account.](../exchangeonline/media/hve-m365/hve-main-5.png)](../exchangeonline/media/hve-m365/hve-main-5.png#lightbox)
6. Select **Next**, review the information, and then select **Create**.

    [![Screenshot of review page for adding a new HVE account.](../exchangeonline/media/hve-m365/hve-main-6.png)](../exchangeonline/media/hve-m365/hve-main-6.png#lightbox)

After the account is created, it appears in the list of HVE accounts. Once a valid billing policy is assigned, the HVE account becomes active and can send email.

### Edit an existing HVE account

You can edit an existing HVE account by using either the **Exchange admin center** or **Exchange Online PowerShell**. This section describes editing an HVE account by using the Exchange admin center. For PowerShell, see PowerShell management for High Volume Email accounts.

1. Go to the **Exchange admin center** at https://admin.exchange.microsoft.com/.
2. In the left navigation, select **Mail flow**, and then select **High Volume Email**.
3. Select an HVE account from the list to open the account details.

    When you open an account, two tabs are available – **General** and **Billing policies**. You can also delete the HVE account from the account details page.

    [![Screenshot of general tab in HVE account details.](../exchangeonline/media/hve-m365/hve-main-9.png)](../exchangeonline/media/hve-m365/hve-main-9.png#lightbox)

    [![Screenshot of billing policies tab in HVE account details.](../exchangeonline/media/hve-m365/hve-main-10.png)](../exchangeonline/media/hve-m365/hve-main-10.png#lightbox)

**General tab**

The General tab allows you to review basic information about the HVE account, including **Display name** and **Primary email address**. To edit the **display name**, select **Manage general information**, update the value, and save your changes.

Note

The primary SMTP address of an HVE account cannot be changed in the Exchange admin center. To update the primary SMTP address, use Exchange Online PowerShell. For details, see PowerShell management for High Volume Email accounts.

**Billing policies tab**

The Billing policies tab shows the current billing policy assignment for the HVE account. From this page, you can:

- Review which billing policy is currently assigned
- Update the billing policy by selecting a different policy from the drop‑down menu and confirm with “Update”.

### Authentication considerations for High Volume Email

High Volume Email supports both modern authentication (OAuth) and basic authentication for SMTP connections. Your organization’s identity and security settings can affect which authentication methods are available.

- If [Security Defaults](/en-us/entra/fundamentals/security-defaults) are enabled in Microsoft Entra ID, all basic authentication methods (including SMTP) are disabled. In this configuration, HVE can authenticate only by using OAuth. To use basic authentication with HVE, you must disable Security Defaults. For more information, see [Security defaults in Microsoft Entra ID](/en-us/entra/fundamentals/security-defaults#disabling-security-defaults).
- For OAuth‑based authentication, see [OAuth authentication for High Volume Email for Microsoft 365](oauth-high-volume-mails-m365).
- HVE accounts can authenticate even when [SMTPClientAuthenticationDisabled](/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission) is set to `True` in `TransportConfig`, because HVE uses a dedicated SMTP endpoint.

To prevent authentication policies from blocking HVE traffic, ensure that the authentication settings applied to the HVE account allow the selected authentication method (OAuth or basic authentication). You can apply custom authentication policies specifically to HVE accounts as needed.

## Configure your application or device to send email using HVE

After creating an HVE account, configure your application or device (for example, a printer or line‑of‑business app) to send email by using the High Volume Email SMTP endpoint.

**Required SMTP settings**

Use the following settings in your application or device configuration:

| Printer/Application setting | Value |
| --- | --- |
| SMTP server (smart host) | smtp.hve.mx.microsoft (recommended) or smtp-hve.office365.com (will be deprecated in the future) |
| Port | 587 |
| TLS/StartTLS | Enabled |
| Authentication | HVE account credentials or OAuth token |

## View HVE usage report

1. Go to the **Exchange admin center** at https://admin.exchange.microsoft.com/.
2. In the left navigation, select **Reports**, and then select **Mail flow**.
3. Under **Mail flow reports**, select **High Volume Email**.
4. Select a time period for the report from the drop down. The default time period is **7 days**, but **30 days**, **90 days** and **Custom start date** are available as well.
5. Next to the time period drop down, choose the volume type you want to view. You can choose between **Recipient volume** (default) or **Message volume**.
6. If no account is selected, the tenant’s total HVE volume is shown. Select a specific HVE account to view usage data for this account in addition to the tenant total.

    [![Screenshot of HVE report.](../exchangeonline/media/hve-m365/hve-main-4.png)](../exchangeonline/media/hve-m365/hve-main-4.png#lightbox)

## PowerShell management for High Volume Email accounts

You can manage High Volume Email accounts by using Exchange Online PowerShell. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell.](/en-us/powershell/exchange/connect-to-exchange-online-powershell)

### List all HVE accounts

To list all HVE accounts in your tenant, run the following command:

```powershell
Get-MailUser -HVEAccount
```

### Create an HVE account

You can create an HVE account and provide a password in one of the following ways:

- **Option 1: Managed domain (provide the password as a secure string)**:

    ```powershell
    $securePassword = Read-Host "Enter password" -AsSecureString
    
    New-MailUser -HVEAccount -Name "HVE account" -Password $securePassword -PrimarySmtpAddress "HVEAccount_01@contoso.com"
    ```
- **Option 2: Managed domain (enter the password when prompted)**:

    ```powershell
    New-MailUser -HVEAccount -Name "HVE account" -PrimarySmtpAddress "HVEAccount_01@contoso.com"
    ```
- **Option 3: Create an HVE account with a federated domain**:

    If your tenant uses a federated domain, you can create an HVE account by specifying an email address in that domain. In the following example, fabrikam.com represents a federated domain in the tenant. Any managed domain can be included in the Name field.

    ```powershell
    New-MailUser -HVEAccount -Name "HVEaccount_01@contoso.com" -PrimarySmtpAddress "HVEAccount_01@fabrikam.com”
    ```

### Remove an HVE account

To delete an HVE account, run the following command:

```powershell
Remove-MailUser -Identity "HVE account"
```

You’ll be prompted to confirm the removal.

### Update the display name

To update the display name of an HVE account, run the following command:

```powershell
Set-MailUser -HVEAccount -Identity "HVE account" -DisplayName "HVE account 2"
```

### Change the primary SMTP address to a federated domain

If your tenant uses a federated domain and you created an HVE account using an address in a managed domain, you can update the account to use an address in a federated domain by changing the primary SMTP address. In the following example, fabrikam.com represents a federated domain in the tenant:

```powershell
Set-MailUser -HVEAccount -Identity "HVEAccount_01@contoso.com" -PrimarySmtpAddress "HVEAccount_01@fabrikam.com”
```

### View HVE account settings

You can view the configuration settings of an HVE account, this allows you to review settings such as the **Reply‑To address** and the list of **allowed applications** for OAuth authentication. For more information on allowed applications, see [Restrict OAuth access to allowed applications](oauth-high-volume-mails-m365#restrict-oauth-access-to-allowed-applications). To view the settings for a specific HVE account, run the following command:

```powershell
Get-HVEAccountSettings -Identity "HVEAccount_01@contoso.com"
```

### Modify HVE account settings

To modify the settings for a specific HVE account, run the following command:

```powershell
Set-HVEAccountSettings -Identity "HVEAccount_01@contoso.com" -ReplyTo "marketing@contoso.com"
```

### View available billing policies

To list all billing policies available in the tenant, that can be used for High Volume Email, run the following command:

```powershell
Get-BillingPolicy -ResourceType HVE
```

### View the billing policy assigned to an HVE account

To view the billing policy currently associated with a specified HVE account, run the following command:

```powershell
Get-HVEAccountBillingPolicy -Identity HVEAccount_01@contoso.com
```

### Assign or change a billing policy

To modify the billing policy mapping for a specified HVE account, run the following command. The GUIDs of billing policies available for use with High Volume Email can be retrieved by using the Get-BillingPolicy cmdlet with the -ResourceType HVE parameter.

```powershell
Set-HVEAccountBillingPolicy -Identity HVEAccount_01@contoso.com -BillingPolicyId "11111111-1111-1111-1111-111111111111"
```

After the policy is assigned, the service validates it automatically. If the policy is valid and the subscription is active, the account becomes active.

### Remove an assigned billing policy

To remove the billing policy mapping for a specified HVE account, run the following command:

```powershell
Set-HVEAccountBillingPolicy -Identity HVEAccount_01@contoso.com -BillingPolicyId $null
```