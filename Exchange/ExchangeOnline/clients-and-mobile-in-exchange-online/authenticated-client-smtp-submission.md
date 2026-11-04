---
layout: Conceptual
title: Enable or disable SMTP AUTH in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission
Manager: tmechelke
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: 'Summary: An overview of SMTP AUTH in Exchange Online.'
ms.topic: how-to
author: srvar
ms.author: srvar
ms.assetid: 
ms.reviewer: akprakash
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: 4f463d2b-dfa3-1061-4e34-01fdfd8b5032
document_version_independent_id: a1d6d284-1c4c-438d-caaa-b06f7a7fb8a8
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 4327484b-3daa-be3c-c706-4f8722f47cdf
---

# Enable or disable SMTP AUTH in Exchange Online | Microsoft Learn

SMTP client email submissions (also known as *authenticated SMTP submissions* or *SMTP AUTH*) are used in the following scenarios in Office 365 and Microsoft 365:

- POP3 and IMAP4 clients. These protocols only allow clients to *receive* email messages, so they need to use authenticated SMTP to *send* email messages.
- Applications, reporting servers, and multifunction devices that generate and send email messages.

The SMTP AUTH protocol is used for SMTP client email submissions, typically on TCP port 587. SMTP AUTH supports modern authentication (Modern Auth) through OAuth in addition to basic authentication. For more information, see [Authenticate an IMAP, POP or SMTP connection using OAuth](/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth).

Virtually all modern email clients that connect to Exchange Online mailboxes in Office 365 or Microsoft 365 (for example, Outlook, Outlook on the web, iOS Mail, Outlook for iOS and Android, etc.) don't use SMTP AUTH to send email messages.

Therefore, we highly recommend that you disable SMTP AUTH in your Exchange Online organization, and enable it only for the accounts (mailboxes) that still require it. There are two settings that can help you do this:

- An organization-wide setting to disable (or enable) SMTP AUTH.
- A per-mailbox setting that overrides the tenant-wide setting.

These settings only apply to mailboxes that are hosted in Exchange Online (Office 365 or Microsoft 365).

Note

- If *security defaults* is enabled in your organization, SMTP AUTH is already disabled in Exchange Online. To use SMTP AUTH, you need to disable *security defaults*. For more information, see [Security defaults in Microsoft Entra ID](/en-us/entra/fundamentals/security-defaults)
- If your authentication policy disables basic authentication for SMTP, clients cannot use the SMTP AUTH protocol even if you enable the settings outlined in this article. For more information, see [Disable Basic authentication in Exchange Online](/en-us/exchange/clients-and-mobile-in-exchange-online/disable-basic-authentication-in-exchange-online).

## Disable SMTP AUTH in your organization

You can disable (or enable) SMTP AUTH globally for your organization in the EAC or by using [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

To disable SMTP AUTH globally in your organization in the EAC, go to the **Mail Flow** settings page in the [Settings](https://admin.exchange.microsoft.com/#/settings) and toggle the setting labeled **Turn off SMTP AUTH protocol for your organization**.

To disable SMTP AUTH globally in your organization with PowerShell, run the following command:

```PowerShell
Set-TransportConfig -SmtpClientAuthenticationDisabled $true
```

Note

To enable SMTP AUTH if it's already disabled, use the value `$false`.

### How do you know this procedure worked?

To verify that you've globally disabled SMTP AUTH in your organization, run the following command and verify that the value of the **SmtpClientAuthenticationDisabled** property is `True`:

```PowerShell
Get-TransportConfig | Format-List SmtpClientAuthenticationDisabled
```

## Enable SMTP AUTH for specific mailboxes

The per-mailbox setting to enable (or disable) SMTP AUTH is available in the Microsoft 365 admin center or [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

### Use the Microsoft 365 admin center to enable or disable SMTP AUTH on specific mailboxes

1. Open the [Microsoft 365 admin center](https://admin.microsoft.com) and go to **Users** &gt; **Active users**.
2. Select the user, and in the flyout that appears, select **Mail**.
3. In the **Email apps** section, select **Manage email apps**.
4. Verify the **Authenticated SMTP** setting: unchecked = disabled, checked = enabled.
5. When you're finished, select **Save changes**.

### Use Exchange Online PowerShell to enable or disable SMTP AUTH on specific mailboxes

Use the following syntax:

```PowerShell
Set-CASMailbox -Identity <MailboxIdentity> -SmtpClientAuthenticationDisabled <$true | $false | $null>
```

The value `$null` indicates the setting for the mailbox is controlled by the global setting on the organization. You use the values `$true` (disabled) or `$false` (enabled) to *override* the organization setting. The mailbox setting takes precedence over the organization setting.

This example enables SMTP AUTH for mailbox `sean@contoso.com`.

```PowerShell
Set-CASMailbox -Identity sean@contoso.com -SmtpClientAuthenticationDisabled $false
```

This example disables SMTP AUTH for mailbox `chris@contoso.com`.

```PowerShell
Set-CASMailbox -Identity chris@contoso.com -SmtpClientAuthenticationDisabled $true
```

### Use Exchange Online PowerShell to enable or disable SMTP AUTH on multiple mailboxes

Use a text file to identify the mailboxes. Values that don't contain spaces (for example, alias, email address, or account name) work best. The text file must contain one mailbox on each line like this:

> 
> `akol@contoso.com``tjohnston@contoso.com``kakers@contoso.com`

The syntax uses the following two commands (one to identify the mailboxes, and the other to enable SMTP AUTH for those mailboxes):

```PowerShell
$<VariableName> = Get-Content "<text file>"
$<VariableName> | foreach {Set-CASMailbox -Identity $_ -SmtpClientAuthenticationDisabled <$true | $false | $null>}
```

This example enables SMTP AUTH for the mailboxes specified in the file C:\My Documents\Allow SMTP AUTH.txt.

```PowerShell
$Allow = Get-Content "C:\My Documents\Allow SMTP AUTH.txt"
$Allow | foreach {Set-CASMailbox -Identity $_ -SmtpClientAuthenticationDisabled $false}
```

Note

To disable SMTP AUTH for the mailboxes, use the value `$true`. To return control to the organization setting, use the value `$null`.

### How do you know this worked?

To verify that you've enabled or disabled SMTP AUTH for a specific mailbox, do any of the following steps:

- **Individual mailboxes in the Microsoft 365 admin center**: Go to **Users** &gt; **Active users** &gt; select the user &gt; select **Mail** &gt; select **Manage email apps** and verify the value of **Authenticated SMTP** (checked = enabled, unchecked = disabled).
- **Individual mailboxes in Exchange Online PowerShell**: Replace `<MailboxIdentity>` with the name; alias; email address or account name of the mailbox; run the following command; and verify the value of the **SmtpClientAuthenticationDisabled** property (`False` = enabled, `True` = disabled, blank = use organization setting).

    ```PowerShell
    Get-CASMailbox -Identity <MailboxIdentity>  | Format-List SmtpClientAuthenticationDisabled
    ```
- **All mailboxes where SMTP AUTH is disabled**: Run the following command:

    ```PowerShell
    $Users = Get-CASMailbox -ResultSize unlimited
    $Users | where {$_.SmtpClientAuthenticationDisabled -eq $true}
    ```
- **All mailboxes where SMTP AUTH is enabled**: Run the following command:

    ```PowerShell
    $Users = Get-CASMailbox -ResultSize unlimited
    $Users | where {$_.SmtpClientAuthenticationDisabled -eq $false}
    ```
- **All mailboxes where SMTP AUTH is controlled by the organization setting**: Run the following command:

    ```PowerShell
    $Users = Get-CASMailbox -ResultSize unlimited
    $Users | where {$_.SmtpClientAuthenticationDisabled -eq $null}
    ```