---
layout: Conceptual
title: Create a cloud-based archive in an Exchange hybrid deployment | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/create-cloud-based-archive
Manager: serdars
ms.subservice: ''
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: install-set-up-deploy
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
ms.assetid: ecc0a687-6c05-47bd-a079-a43d83cba9ea
ms.reviewer: 
description: In an Exchange hybrid deployment, you can configure an on-premises primary mailbox or an online mailbox with a cloud-based archive mailbox in Exchange Online.
ms.date: 2025-05-14T00:00:00.0000000Z
locale: en-us
document_id: 56dfb49c-fbb1-4e58-a94b-060f31744d6e
document_version_independent_id: 2b2de3cb-3087-c82a-f6ad-f58990a85ae0
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/create-cloud-based-archive.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/create-cloud-based-archive
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/create-cloud-based-archive.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: c6121c09-1a7c-9add-5316-fc5683ed91ad
---

# Create a cloud-based archive in an Exchange hybrid deployment | Microsoft Learn

In an Exchange hybrid deployment, you can configure an on-premises primary mailbox or an online mailbox with a cloud-based archive mailbox in Exchange Online.

## Before you begin

- The user with the on-premises primary mailbox must have a user account in your Microsoft 365 or Office 365 organization.
- The user account must be assigned an Exchange Online Archiving license. For more information about the different options, see [Exchange Online Archiving service description](/en-us/office365/servicedescriptions/exchange-online-archiving-service-description/exchange-online-archiving-service-description). The steps for assigning a license are included in the procedures in Step 1.
- After you enable the cloud-based archive mailbox in Step 1, it might take up to 30 minutes for the cloud-based archive mailbox to be provisioned. This is because the cloud-base archive mailbox is created by the process of directory synchronization, where your on-premises Active Directory is synchronized with Microsoft Entra ID in Microsoft 365 or Office 365. By default, directory synchronization runs once every 30 minutes.

## Step 1: Enable a cloud-based archive mailbox for a primary on-premises mailbox or an online mailbox

Use one of the following procedures to enable a cloud-based archive mailbox for an on-premises primary mailbox or an online mailbox. Perform these steps in the Exchange admin center or Exchange Management Shell in your on-premises Exchange organization and in the Microsoft 365 admin center.

### Use the EAC to create a cloud-based archive mailbox for a new user

1. In the EAC in your on-premises organization, go to **Recipients** &gt; **Mailboxes**.
2. Click **New**![Add Icon.](../exchangehybrid/media/itpro_eac_addicon.gif) &gt; **User mailbox** or **Office 365 mailbox** depending on where you want to create the mailbox.
3. On the **New user mailbox** page, create a mailbox for a new or existing user. For more information about creating a user mailbox, see [Create User Mailboxes](../recipients/create-user-mailboxes).
4. If you want to create an **online mailbox**:

    1. Click the **Create an archive mailbox** check box.

    If you want to create an **on-premises mailbox**:

    1. Click **More options** to enable a cloud-based archive mailbox.
    2. Under **Archive**, click the **Create an in-place archive for this user** check box, and then click **Cloud-based archive**. The name of the domain that the archive mailbox will be provisioned in is displayed.

    ![Under Archive, click the checkbox and then click Cloud-based archive.](../exchangehybrid/media/43d0473e-30ad-4021-94bc-a9c5449f43ba.png)
5. Click **Save** to create the mailbox and the cloud-based archive.

    Note on the **Mailboxes** page, the value **User (Archive)** is displayed in the **Mailbox type** column for the selected mailbox.
6. Wait up to 30 minutes for directory synchronization to create a corresponding user account in Microsoft 365 or Office 365.

    Tip

    In the Microsoft 365 admin center, go to **Health** &gt; **Directory sync status** to see the last time that directory synchronization occurred.
7. After verifying that directory synchronization has occurred after you created the new mailbox, in the Microsoft 365 admin center, go to **Users** &gt; **Active users**, and then select the new user account that was created for the new on-premises mailbox.
8. On the user properties page that's displayed, click **Edit** in the **Product licenses** section.

    ![Click Edit in the details pane to assign a license to the selected user.](../exchangehybrid/media/383a9068-53cb-420a-a05e-823e8b5a2c25.png)
9. Under the **Location** drop-down menu, select a location for the user.
10. Expand the list of Microsoft 365 or Office 365 Enterprise licenses, and then assign an Exchange Online Archiving license, and then save the changes.

    In the **Status** column in the list of users, notice that a license is assigned to the user.
11. Once again, wait up to 30 minutes for directory synchronization to provision a cloud-based archive mailbox. Go to Step 2 to see how to verify that the cloud-based archive mailbox has been created. After the archive mailbox is created, the user can access it by using Outlook or Outlook on the web.

### Use the Exchange Management Shell to create a cloud-based archive mailbox for a new user

The following example creates a new primary **on-premises mailbox** and Active Directory user account for Pilar Pinilla with a cloud-based archive mailbox. You're prompted to enter the password:

```PowerShell
New-Mailbox -Name "Pilar Pinilla" -UserPrincipalName pilarp@contoso.com -Password (Read-Host "Enter password" -AsSecureString) -ArchiveDomain <tenant_domain>.mail.onmicrosoft.com -RemoteArchive -FirstName Pilar -LastName Pinilla
```

For detailed syntax and parameter information, see [New-Mailbox](/en-us/powershell/module/exchangepowershell/new-mailbox).

The following example creates a new primary **online mailbox** and Active Directory user account for Kim Akers with a cloud-based archive mailbox. You're prompted to enter the password:

```PowerShell
New-RemoteMailbox -Name "Kim Akers" -UserPrincipalName kima@contoso.com -Password (Read-Host "Enter password" -AsSecureString) -Archive -FirstName Kim -LastName Akers
```

For detailed syntax and parameter information, see [New-RemoteMailbox](/en-us/powershell/module/exchangepowershell/new-remotemailbox).

After you create the primary and cloud-based archive mailboxes, wait up to 30 minutes for directory synchronization to create a corresponding user account in Microsoft 365 or Office 365. Then assign the product license as we described in Steps 8 to 10 of Use the EAC to create a cloud-based archive mailbox for a new user. To use PowerShell to assign the license, see [Assign Microsoft 365 licenses to user accounts with PowerShell](/en-us/microsoft-365/enterprise/assign-licenses-to-user-accounts-with-microsoft-365-powershell). Once again, wait up to 30 minutes for directory synchronization to provision a cloud-based archive mailbox. Go to Step 2 to see how to verify that the cloud-based archive mailbox has been created. After the archive mailbox is created, the user can access it by using Outlook or Outlook on the web.

Tip

In the Microsoft 365 admin center, go to **Health** &gt; **Directory sync status** to see the last time that directory synchronization occurred.

### Use the EAC to create a cloud-based archive mailbox for an existing user

1. In the Microsoft 365 admin center, go to **Users** &gt; **Active users**, and then select the user account that you want to create a cloud-base archive mailbox for.
2. On the user properties page that's displayed, click **Edit** in the **Product licenses** section.

    ![Click Edit in the details pane to assign a license to the selected user.](../exchangehybrid/media/383a9068-53cb-420a-a05e-823e8b5a2c25.png)
3. Under the **Location** drop-down menu, select a location for the user.
4. Expand the list of Microsoft 365 or Office 365 Enterprise licenses, and then assign an Exchange Online Archiving license, and then save the changes.

    In the **Status** column in the list of users, notice that a license is now assigned to the user.
5. In the EAC in your on-premises organization, go to **Recipients** &gt; **Mailboxes**.
6. In the list of mailboxes, select the user that you assigned the license to.
7. In the details pane, under **In-Place Archive**, click **Enable**.

    ![Click Enable in the details pane to enable the archive mailbox for the selected user.](../exchangehybrid/media/17ce99f7-d154-4e21-bec1-c938af1d4a0a.png)
8. If it's an **online mailbox**:

    - Click **yes** to enable the In-Place Archive.

    If it's an **on-premises mailbox**:

    - On the **Create in-place archive** page, click **Cloud-based archive**, and then click **Ok**. The name of the domain that the archive mailbox will be provisioned in is displayed.

        ![On the Create in-place archive page, click Cloud-based archive.](../exchangehybrid/media/9ad047c9-ef47-47df-93cc-0fab872f1ae1.png)

        Note on the **Mailboxes** page, the value **User (Archive)** is displayed in the **Mailbox type** column for the selected mailbox.
9. Wait up to 30 minutes for directory synchronization to create the cloud-based archive mailbox. Go to Step 2 to see how to verify that the cloud-based archive mailbox has been created. After the archive mailbox is created, the user can access it by using Outlook or Outlook on the web.

    Tip

    In the admin center, go to **Health** &gt; **Directory sync status** to see the last time that directory synchronization occurred.

### Use the Exchange Management Shell to create a cloud-based archive mailbox for an existing user

Before you create the cloud-based archive mailbox, you need to assign the product license as we described in Steps 1 to 4 of Use the EAC to create a cloud-based archive mailbox for an existing user. To use PowerShell to assign the license, see [Assign Microsoft 365 licenses to user accounts with PowerShell](/en-us/microsoft-365/enterprise/assign-licenses-to-user-accounts-with-microsoft-365-powershell).

The following example creates a cloud-based archive mailbox for Ayla who has a primary **on-premises mailbox**:

```PowerShell
Enable-Mailbox -Identity ayla@contoso.com -RemoteArchive -ArchiveDomain "contoso.mail.onmicrosoft.com"
```

For detailed syntax and parameter information, see [Enable-Mailbox](/en-us/powershell/module/exchangepowershell/enable-mailbox).

The following example creates a cloud-based archive mailbox for Laura who has a primary **online mailbox**:

```PowerShell
Enable-RemoteMailbox -Identity laura@contoso.com -Archive
```

For detailed syntax and parameter information, see [Enable-RemoteMailbox](/en-us/powershell/module/exchangepowershell/enable-remotemailbox).

Wait up to 30 minutes for directory synchronization to create the cloud-based archive mailbox. Go to Step 2 to see how to verify that the cloud-based archive mailbox has been created. After the archive mailbox is created, the user can access it by using Outlook or Outlook on the web.

Tip

In the admin center, go to **Health** &gt; **Directory sync status** to see the last time that directory synchronization occurred.

## Step 2: Verify that the cloud-based archive mailbox is created

As previously explained, there might be a delay between the time that you enable a cloud-based archive mailbox and when the cloud-based archive mailbox is created. This is because directory synchronization has to run to create the cloud-based archive mailbox. Here are some ways to verify that the cloud-based archive mailbox has been created.

In your Exchange Online organization, run the following PowerShell command to display properties related to an on-premises user's cloud-based archive mailbox. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

If it's an **on-premises mailbox**:

```PowerShell
Get-MailUser <cloud mail user> | FL *archive*
```

If it's an **online mailbox**:

```PowerShell
Get-Mailbox <cloud mailbox> | FL *archive*
```

The following screenshots show the properties that are returned when the provisioning of the cloud-based archive mailbox is pending and after the cloud-based archive mailbox has been created.

### Properties before the cloud-based archive mailbox is provisioned by directory synchronization

![Property of cloud-based mailuser before the cloud-based archive is provisioned.](../exchangehybrid/media/c6a42713-f061-4761-93c1-2b5478953e46.png)

Before directory synchronization provisions the cloud-based archive, the *ArchiveStatus* property is set to `None`. Also note that the *ArchiveGuid* and *ArchiveName* properties are empty.

### Properties after the cloud-based archive mailbox is provisioned by directory synchronization

![Cloud-based mail user properties after the cloud-based archive is provisioned.](../exchangehybrid/media/005fcc87-6253-4218-aafc-50f212de54fa.png)

After directory synchronization provisions the cloud-based archive, the *ArchiveStatus* property is set to `Active`, and the *ArchiveGuid* and *ArchiveName* properties are populated. At this point, the user is able to access their cloud-based archive mailbox in Outlook or Outlook on the web.

Caution

As outlined in the [Retirement of cloud archive mailbox access by using Exchange Server on-premises OWA](https://techcommunity.microsoft.com/blog/exchange/retirement-of-cloud-archive-mailbox-access-by-using-exchange-server-on-premises-/4405432) blog post, the feature that allowed users with a primary mailbox hosted on Exchange Server (on-premises) to access their archive mailbox in Exchange Online via Outlook on the Web (OWA) has been deprecated.

![User can access their cloud-based archive mailbox in Outlook or Outlook on the web.](../exchangehybrid/media/8777bc4d-05c3-4489-8d8c-ff5429a0b2c3.png)

You can also run the following PowerShell command in your on-premises Exchange organization to display properties related to the cloud-based archive mailbox of an on-premises user.

If it's an **on-premises mailbox**:

```PowerShell
Get-Mailbox <on-premises user mailbox> | FL *archive*
```

If it's an **online mailbox**:

```PowerShell
Get-MailUser <on-premises mail user> | FL *archive*
```

#### Properties before the cloud-based archive mailbox is provisioned by directory synchronization

![Mailbox property before the cloud-based archive is provisioned.](../exchangehybrid/media/d5625bc8-03de-439a-8a0a-051ff537a0bf.png)

Before directory synchronization provisions the cloud-based archive, the *ArchiveStatus* property is set to `None` and the *ArchiveState* property is set to `HostedPending`.

#### Properties after the cloud-based archive mailbox is provisioned by directory synchronization

![Mailbox properties after the cloud-based archive is provisioned.](../exchangehybrid/media/9b42d562-1b0a-4722-97aa-35d0ef6f9372.png)

After directory synchronization provisions the cloud-based archive, the *ArchiveStatus* property is set to `Active` and the *ArchiveState* property is set to `HostedProvisioned`. At this point, the user is able to access their cloud-based archive mailbox in Outlook or Outlook on the web.

## (Optional) Run directory synchronization

As previously explained, the cloud-base archive mailbox is created by the process of directory synchronization. By default, your on-premises Active Directory is synchronized with Microsoft Entra ID in Microsoft 365 or Office 365 once every 30 minutes. You can see when the last time directory synchronization occurred by going to **Health** &gt; **Directory sync status** in the Microsoft 365 admin center.

Sometimes you may want to start directory synchronization to provision the cloud-based archive mailbox before the next scheduled synchronization. You can do this by running the following PowerShell command on the server where cloud sync or Microsoft Entra Connect is installed.

```PowerShell
Start-ADSyncSyncCycle -PolicyType Delta
```

For more information, see [Microsoft Entra Connect Sync: Scheduler](/en-us/azure/active-directory/hybrid/how-to-connect-sync-feature-scheduler).