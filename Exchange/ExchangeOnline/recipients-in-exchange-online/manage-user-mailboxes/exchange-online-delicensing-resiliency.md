---
layout: Conceptual
title: Get Started with Delicensing Resiliency in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/exchange-online-delicensing-resiliency
Manager: serdars
ms.subservice: exo-manageability
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.custom:
- has-azure-ad-ps-ref
description: Admins can learn how to get started with Delicensing Resiliency in Exchange Online.
ms.topic: get-started
author: serdars
ms.author: serdars
ms.assetid: be7f59a5-bbc9-4b7a-a28b-f47b26dd33a7
ms.reviewer: YajvendraGupta
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2024-11-05T00:00:00.0000000Z
locale: en-us
document_id: bda3808d-7e73-a71f-fbc5-c83e070a2437
document_version_independent_id: f164d0af-67bf-f417-d6b8-345692895391
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/exchange-online-delicensing-resiliency.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: recipients-in-exchange-online/manage-user-mailboxes/exchange-online-delicensing-resiliency
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/recipients-in-exchange-online/manage-user-mailboxes/exchange-online-delicensing-resiliency.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: fb99500b-43b0-b4c0-9d79-f85e0f14a327
---

# Get Started with Delicensing Resiliency in Exchange Online | Microsoft Learn

## What is Exchange Online Delicensing Resiliency

To get some initial background, you can read the [blog post](https://techcommunity.microsoft.com/t5/exchange-team-blog/introducing-exchange-online-delicensing-resiliency-to-protect/ba-p/4082759) that announces the Exchange Online Delicensing Resiliency feature. Today when a user mailbox license is removed, Microsoft Entra ID triggers a license removal change. Exchange Online reacts to these delicensing events by removing the mailbox access instantly.

We have witnessed cases where a customer accidentally removes licenses for thousands of users. A mistake in license assignment or tenant subscription can cause Exchange Online service disruption for the customer. Service disruption also impacts mail flow, which results in nondelivery reports (NDRs) or misrouting of emails. Trying to recover these lost emails could be difficult.

To catch delicensing mistakes, we need to delay its impact on Exchange Online service to allow time for the customer to catch potential mistakes. Therefore, we're adding the capability for customers to delay the operation of Exchange Online license removal by 30 days. This is to have resiliency in the delicensing flow to protect Exchange Online customers from losing mailbox capability immediately after accidental/un-intended delicensing.

## Enable your tenant for Exchange Online Delicensing Resiliency feature!

You can enable the feature and its associated capabilities like 'Admin notification' and 'user email notification' by referring to the following steps:

### Step 1 – Enable Exchange Online Delicensing Resiliency feature:

To enable the feature, execute the following PowerShell cmdlet:

```PowerShell
Set-OrganizationConfig -DelayedDelicensingEnabled:$true
```

Note

Exchange Online Delicensing Resiliency feature is accessible to tenants with over 5000 non-trial licenses only. Enabling the feature can take up to 24 to 48 hours. If the feature is not enabled after 24 hours, contact [Microsoft Support](https://support.microsoft.com/contactus/).

You may verify status of the feature enabled by executing the following PowerShell cmdlet:

```PowerShell
Get-OrganizationConfig | fl *DelayedDelicensingEnabledState*
```

[![Screenshot of enabling delicensing resiliency.](../../exchangeonline/media/delicensing-resiliency/powershell-cmd-1.png)](../../exchangeonline/media/delicensing-resiliency/powershell-cmd-1.png#lightbox)

### Step 2 – Enable admin notification:

When the feature is turned on, the [Service Health](/en-us/microsoft-365/enterprise/view-service-health) advisory notification is activated by default for the tenant admins to proactively deal with possible accidental delicensing of users. Admins get a weekly advisory digest notification if there's any delicensing activity in tenant. If you choose the [email option](/en-us/microsoft-365/enterprise/view-service-health#how-to-check-service-health) in Service Health, then you also get the same advisory digest notification in email format. The Service Health post consists of a count of delicensed users in a tenant over a period of eight days, who are in 30-days grace period.

The following is a sample of Service Health advisory notification:

[![Screenshot of Service advisory notification.](../../exchangeonline/media/delicensing-resiliency/service-health-notification.png)](../../exchangeonline/media/delicensing-resiliency/service-health-notification.png#lightbox)

The engine triggers Service Heath advisory notification based on the following conditions:

- A user is delicensed in the last seven days.
- If Service Heath advisory notification was sent before, the next notification should be more than seven days since the last notification.

For example, if a user is delicensed in the last seven days, a Service Heath advisory notification is expected to be received in the next one or two days. The engine waits for seven days since the last notification. Thereafter, everyday the engine continues to check if a user is delicensed in the last seven days. Suppose a user is delicensed after 10 days from the last notification sent, then the engine will trigger Service Heath advisory notification in approximately next 1-2 days consisting of a count of delicensed users in the tenant over a period of approximately last eight days. The following snapshot of Service Health advisory notifications for different scenarios helps you to understand how the engine works:

[![Screenshot of Service health notification for diff scenarios.](../../exchangeonline/media/delicensing-resiliency/shd-post.png)](../../exchangeonline/media/delicensing-resiliency/shd-post.png#lightbox)

Once the feature is enabled, admin notification capability is enabled by default. If you disable the admin notification (Service Heath advisory) and later wish to re-enable it, execute the following PowerShell cmdlet:

```PowerShell
Set-OrganizationConfig -TenantAdminNotificationForDelayedDelicensingEnabled:$true
```

Note

Enabling the admin notification may take up to 24 to 48 hours. If the admin notification is not enabled after 24 hours, contact [Microsoft Support](https://support.microsoft.com/contactus/).

You can verify status of the admin notification enabled by executing the following PowerShell cmdlet:

```PowerShell
Get-OrganizationConfig | fl *TenantAdminNotificationForDelayedDelicensing*
```

[![Screenshot of command to verify status of notification.](../../exchangeonline/media/delicensing-resiliency/powershell-cmd-2.png)](../../exchangeonline/media/delicensing-resiliency/powershell-cmd-2.png#lightbox)

### Step 3 – Enable 'user email notification':

Admins might overlook the Service Health advisory notification, which could result in users losing access to their mailboxes, after their 30-days grace period ends. To make the feature more actionable, once the Exchange Delicensing Resiliency feature is enabled, the 'user email notification' capability is enabled by default. When both are activated, the user whose license is removed will get periodic reminder email notifications (1 to 3) after 18 days from delicensing of the user. The email reminders are only sent to users exhibiting mailbox activities like sending mails, accessing mailbox, etc. after 24 hours of delicensing. The following is a sample of user email notification:

[![Screenshot of email notification.](../../exchangeonline/media/delicensing-resiliency/end-user-e-noti-outlook.png)](../../exchangeonline/media/delicensing-resiliency/end-user-e-noti-outlook.png#lightbox)

The engine triggers user email notification based on the following conditions:

- A user is in a delicensed state for more than 18 days to get the first email notification.
- The user's mailbox is exhibiting activity one day after the delicensing time.
- If an email was sent before, the next email should be sent approximately five days after from the previous email for the users still in delicensed state.

For example, if a user is in delicensed state, however exhibiting mailbox activity for more than a day after delicensing time, then after approximately 18 days expect to receive the first email notification, followed by the second and third notification on or around 23rd/24th day and 28th/29th day respectively, provided the user remains in delicensed state.

Another example is when a user remains in a delicensed state and exhibits mailbox activity on the 26th day from the delicensing time, then expect to receive only one email notification approximately on the 27th day from the delicensing time.

If a user exhibits mailbox activity after approximately more than 29 days from the delicensing time, then the user may not receive any email notification due to system processing delays.

The following snapshots show user email notifications for different scenarios to help you understand how the engine works:

[![Screenshot of user email notification 1 to know how engine works.](../../exchangeonline/media/delicensing-resiliency/end-user-e-noti-f1.png)](../../exchangeonline/media/delicensing-resiliency/end-user-e-noti-f1.png#lightbox)

[![Screenshot of user e notification 2 to know how the scenarios work.](../../exchangeonline/media/delicensing-resiliency/end-user-e-noti-f2.png)](../../exchangeonline/media/delicensing-resiliency/end-user-e-noti-f2.png#lightbox)

Once the feature is enabled, the 'user email notification' capability is enabled by default. If you disable the 'user email notification' capability and later wish to re-enable it, execute the following PowerShell cmdlet:

```PowerShell
Set-OrganizationConfig -EndUserMailNotificationForDelayedDelicensingEnabled:$true
```

Note

Enabling the 'user notification' may take up to 24 to 48 hours. If the 'user notification' is not enabled after 24 hours, contact [Microsoft Support](https://support.microsoft.com/contactus/).

You can verify that the 'user email notification' is enabled by executing the following PowerShell cmdlet:

```PowerShell
Get-OrganizationConfig | fl *EndUserMailNotificationForDelayedDelicensing*
```

[![Screenshot of command to verify status of admin notification enabled.](../../exchangeonline/media/delicensing-resiliency/powershell-3a.png)](../../exchangeonline/media/delicensing-resiliency/powershell-3a.png#lightbox)

Note

When you set the value of the `DelayedDelicensingEnabled` parameter to `$true`, the `TenantAdminNotificationForDelayedDelicensingEnabled` and `EndUserMailNotificationForDelayedDelicensingEnabled` parameters are set to `$true` by default.

When you set the value of the `DelayedDelicensingEnabled` parameter to `$false`, the `TenantAdminNotificationForDelayedDelicensingEnabled` and `EndUserMailNotificationForDelayedDelicensingEnabled` parameters are set to `$false` by default.

Important

The 30-days grace period may extend up to 60-days during tenant re-location process. This can happen when a tenant either opted for a GoLocal region move or seamless capacity optimization in the backend across regions by Microsoft.

Currently, the Exchange Online delicensing feature and its associated capabilities are available for tenants in Commercial cloud only.

## You're all set!

Once the feature is enabled for your tenant, you can start exploring the solution and its capabilities.

## What all you could do

With this feature, users will no longer immediately lose their mailbox access after they're delicensed by the admin. Users will lose mailbox access after the Exchange Online Delicensing Resiliency feature's 30-days grace period expires. Upon activating the feature, tenant admins can perform the following actions:

1. Enumerate all the delicensed users in your tenant: To enumerate all the delicensed users in 30-days grace period in your tenant, execute the following PowerShell cmdlet:

    ```PowerShell
    Get-PendingDelicenseUser
    ```

    [![Screenshot of command for enumerating all delicensed users.](../../exchangeonline/media/delicensing-resiliency/powershell4.png)](../../exchangeonline/media/delicensing-resiliency/powershell4.png#lightbox)

    Note

    Users who have been re-licensed will not appear in the Get-PendingDelicenseUser cmdlet output.

    Note

    Due to [provisioning delays](/en-us/exchange/troubleshoot/user-and-shared-mailboxes/delays-provision-mailbox-sync-changes), `Get-PendingDelicenseUser` and `Expedite-Delicensing<EDOID>` cmdlets may not work immediately when a user is delicensed in Microsoft Entra ID (either via MAC portal or Microsoft Entra ID cmdlets), as these events have not yet synced to Exchange Online from Microsoft Entra ID. Typically, this takes less than 30 minutes to sync changes for a user. However, it could take up to 24 hours for changes to sync. If the issue persists after 24 hours, submit a support service request.

    When the feature is enabled, you can also see Exchange Online users who lost their license recently in **Microsoft 365 admin center** under **Active Users** &gt; **License removed recently** as shown in the following screenshots:

    [![Screenshot of license removed recently option.](../../exchangeonline/media/delicensing-resiliency/lic-rem-rec-10.png)](../../exchangeonline/media/delicensing-resiliency/lic-rem-rec-10.png#lightbox)

    [![Screenshot of users license removed recently.](../../exchangeonline/media/delicensing-resiliency/lic-rem-rec-1.png)](../../exchangeonline/media/delicensing-resiliency/lic-rem-rec-1.png#lightbox)

    Note

    Microsoft 365 Admin Center doesn't support Enabling or Disabling Exchange Online Delicensing Resiliency feature and associated capabilities (admin notification and user notification). These need to be performed using Exchange cmdlets.

    To see the status of a specific delicensed user in 30-days grace period in your tenant, execute the following PowerShell cmdlet:

    ```PowerShell
    Get-PendingDelicenseUser <EDOID>
    ```

    You can use any identity of the user as Identity parameter in the above cmdlet like, UPN.

    [![Screenshot of command to view status.](../../exchangeonline/media/delicensing-resiliency/powershell-5.png)](../../exchangeonline/media/delicensing-resiliency/powershell-5.png#lightbox)

    Note

    `Get-PendingDelicenseUser` cmdlet output may contain non-actionable entries pertaining to mailbox which are on hold, objects removed/deleted in Microsoft Entra ID/Exchange Online, Exchange Online license free mailbox (like shared mailbox) etc., which eventually get cleared in approximately 60 days from the date of creation.

    You can view the status of a specific delicensed user in 30-days grace period in **Microsoft 365 admin center** under **Active Users**, as shown in the following screenshot:

    [![Screenshot of user delicensed in 30 days grace period.](../../exchangeonline/media/delicensing-resiliency/user-delicensed-30days.png)](../../exchangeonline/media/delicensing-resiliency/user-delicensed-30days.png#lightbox)

    To see users that are in a delicensing state for &gt;=30 days and are due for delicensing in your tenant anytime, execute the following PowerShell cmdlet:

    ```PowerShell
    Get-PendingDelicenseUser - -ShowDueObjectsOnly
    ```

    [![Screenshot of command to view users due for delicensing.](../../exchangeonline/media/delicensing-resiliency/powershell-6.png)](../../exchangeonline/media/delicensing-resiliency/powershell-6.png#lightbox)

    As the 30-days grace period for Exchange Online license removal is enabled in Exchange, you can see the status of users in delicensed state as 'Unlicensed' in MAC/EAC portal and 'IsLicensed' state as 'False' in Microsoft Entra ID cmdlet output, whereas in Exchange Online the users would be active. For example, the user 'Yaj1' status in MAC portal reflects as 'Unlicensed' and 'IsLicensed' state as 'False' in Microsoft Entra ID cmdlet output. However, mailbox connectivity continues to work for this user during the 30-days grace period in Exchange. The mailbox during 30-days grace period retains the same exchange capabilities as before delicensing action.

    [![Screenshot of status of users unlicensed.](../../exchangeonline/media/delicensing-resiliency/status-user.png)](../../exchangeonline/media/delicensing-resiliency/status-user.png#lightbox)

    [![Screenshot of command.](../../exchangeonline/media/delicensing-resiliency/powershell-7a.png)](../../exchangeonline/media/delicensing-resiliency/powershell-7a.png#lightbox)

    [![Screenshot of test success.](../../exchangeonline/media/delicensing-resiliency/powershell-8.png)](../../exchangeonline/media/delicensing-resiliency/powershell-8.png#lightbox)
2. Expedite delicensing: If delicensing of a user is expected, you can either allow the license to expire at the end of the grace period that is, 30-days from the delicensing operation, or you can expedite the delicense operation using the following cmdlet:

    ```PowerShell
    Expedite-Delicensing <EDOID>
    ```

    You can use any identity of the user as Identity parameter in the above cmdlet like, UPN.

    [![Screenshot of expedite delicensing command.](../../exchangeonline/media/delicensing-resiliency/powershell-9a.png)](../../exchangeonline/media/delicensing-resiliency/powershell-9a.png#lightbox)

    Another way to perform Expedite Delicensing for a user is to go to **Microsoft 365 admin center** and select **Active Users** &gt; **License removed recently**, as shown in the following screenshot:

    [![Screenshot of expedite delicensing for a user.](../../exchangeonline/media/delicensing-resiliency/expedite-delicense-user.png)](../../exchangeonline/media/delicensing-resiliency/expedite-delicense-user.png#lightbox)

    Note

    Once `Expedite-Delicensing<EDOID>` is performed, the service typically takes less than 30 minutes to delicense a user. However, at times it can take up to 24 hours for delicense provisioning to occur. If the user is still not delicensed after 24 hours, submit a support service request.

    Note

    You must always perform `Expedite-Delicensing<EDOID>` whenever you expect user to be completely delicensed from your environment. This is a mandatory step to be followed when you want to delicense a user after enabling the 'Exchange Online Delicensing Resiliency' feature. For example, if you are following this [blog](https://techcommunity.microsoft.com/t5/exchange-team-blog/permanently-clear-previous-mailbox-info/ba-p/607619) then after removing license from the user, you must execute `Expedite-Delicensing<EDOID>` and then execute `Set-User -PermanentlyClearPreviousMailboxInfo`.

    Once the user is successfully delicensed, you can see the following error message for the user:

    [![Screenshot of error message.](../../exchangeonline/media/delicensing-resiliency/powershell-10.png)](../../exchangeonline/media/delicensing-resiliency/powershell-10.png#lightbox)
3. Restore license: If the delicensing of a user is done by mistake and you'd like users to maintain access to their mailbox, then you can restore their license by referring to the guidance documented [here](/en-us/microsoft-365/admin/manage/assign-licenses-to-users).

## Key callouts: Behavior change

1. For scenarios where you want to utilize any mailbox attribute of any existing mailbox, admins were likely to perform delicensing followed by removal of the object. After enabling the 'Exchange Online Delicensing Resiliency' feature, admins must perform `Expedite-Delicensing<EDOID>` before removing the object to reuse its mailbox attributes. So, the recommended method henceforth is:  delicense &gt; expediate delicense &gt; remove (post mailbox converted to MEU/User).
2. For customer inflected migration or related scenarios (like conversion of Exchange Online object to Mail Enabled User), even though users are enabled with 30-days grace period, customers must complete the off-boarding process that is, conversion of Exchange Online object to Mail Enabled User before removing the license. Failing to do so may result in stale entries and unexpected behavior.
3. This feature isn't applicable for mailbox on [hold](/en-us/purview/ediscovery-identify-a-hold-on-an-exchange-online-mailbox), hence mailboxes on hold remain as it is.
4. The feature is not applicable for trial license mailboxes and shared mailboxes. For instance, when a user mailbox is converted to a shared mailbox, subsequent license removal from the user's account is not entitled for the feature.
5. Upon enabling the feature, mailboxes have additional 30-days grace period in addition to the [default 30-days grace period](../delete-or-restore-mailboxes#license-removal). Once the Exchange Online Delicensing Resiliency feature's 30-days grace period expires, Exchange Online license is removed, the user mailbox now serves default 30-days grace period, during which mail access is cut off. After approximately 60 days (Exchange Online Delicensing Resiliency feature's 30-days grace period + default 30-days grace period), the mailbox data is deleted and can't be recovered even after reapplying license.
6. [Disable-RemoteMailbox](/en-us/powershell/module/exchangepowershell/disable-remotemailbox): After enabling the feature, if you plan to remove user mailboxes from the cloud-based service but keep the associated user objects in the on-premises Active Directory, follow the steps:
    1. Delicense the cloud mailbox.
    2. Execute cmdlet `Get-PendingDelicenseUser` to confirm that the user is delicensed and is in the 30-days grace period.
    3. Execute `Expedite-Delicensing<EDOID>` for the user in Exchange Online.
    4. Wait to confirm that the object is converted to a vanilla user.
    5. Execute `Disable-RemoteMailbox` from on-premises shell for the user.

## How can I revert the feature?

If you wish to revert the feature completely, then you can disable the Exchange Online Delicensing Resiliency feature (step 1 below), that disables the feature along with associated capabilities that is, Admin notification and user notification capabilities. If you wish to only disable Admin notification or/and user notification capabilities, then you can do it independently. Once the feature is disabled, users that are already in 30-days grace period state will continue and complete the cycle of 30-days grace period. If you wish to terminate the cycle of 30-days grace period for the users, you can expedite the delicensing by executing `Expedite-Delicensing<EDOID>` cmdlet or perform Expedite Delicensing for a user in **Microsoft 365 admin center** under **Active Users** &gt; **License removed recently**.

### Step 1 – Disable Exchange Online Delicensing Resiliency feature:

To disable the feature, execute the following PowerShell cmdlet:

```PowerShell
Set-OrganizationConfig -DelayedDelicensingEnabled:$false
```

When you set the value of the `DelayedDelicensingEnabled` parameter to `$false`, the `TenantAdminNotificationForDelayedDelicensingEnabled` and `EndUserMailNotificationForDelayedDelicensingEnabled` parameters are set to `$false` by default.

### Step 2 – Disable admin notification:

To disable the admin notification (Service Heath advisory), execute the following PowerShell cmdlet:

```PowerShell
Set-OrganizationConfig -TenantAdminNotificationForDelayedDelicensingEnabled:$flase
```

### Step 3 – Disable user email notification:

To disable 'user email notification', execute the following PowerShell cmdlet:

```PowerShell
Set-OrganizationConfig -EndUserMailNotificationForDelayedDelicensingEnabled:$false
```

You can verify status of the Exchange Online Delicensing Resiliency feature and associated capabilities (Admin notification and user notification) by executing the following PowerShell cmdlet:

```PowerShell
Get-OrganizationConfig | fl *delayed*
```

[![Screenshot of command to verify feature.](../../exchangeonline/media/delicensing-resiliency/powershell-11a.png)](../../exchangeonline/media/delicensing-resiliency/powershell-11a.png#lightbox)

The setting `DelayedDelicensingBlockedExplicitlyState` is an internal configuration for the feature and is not intended for use by administrators.

Note

Disabling or enabling Exchange Online Delicensing Resiliency feature and associated capabilities (Admin notification and user notification) may take up to 24 to 48 hours. If the disable is not completed after 24 hours, contact [Microsoft Support](https://support.microsoft.com/contactus/).