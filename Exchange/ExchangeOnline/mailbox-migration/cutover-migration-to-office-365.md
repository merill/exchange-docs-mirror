---
layout: Conceptual
title: Migrate email to Exchange Online using the Exchange cutover method in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/cutover-migration-to-office-365
Manager: jtremper
ms.subservice: exo-mailbox-migration
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
ms.topic: upgrade-and-migration-article
author: lkueter
ms.author: heidip
ms.assetid: 9496e93c-1e59-41a8-9bb3-6e8df0cd81b4
ms.reviewer: 
description: An article describing when and how to do a cutover migration from a source email system to Microsoft 365 or Office 365 Exchange.
ms.collection:
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- MBS150
- BCS160
audience: Admin
f1.keywords:
- CSH
ms.custom: Adm_O365
ms.service: exchange-online
ms.date: 2024-03-28T00:00:00.0000000Z
locale: en-us
document_id: 721f096d-23d4-0fed-4f5e-0e0964798e8f
document_version_independent_id: 3af25c86-f5e9-1b9c-ffb6-d0d1afa7210e
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/cutover-migration-to-office-365.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/cutover-migration-to-office-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/cutover-migration-to-office-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 8f85dbd2-ffe9-69d2-7642-3b86a14377cf
---

# Migrate email to Exchange Online using the Exchange cutover method in Exchange Online | Microsoft Learn

As part of a Microsoft 365 or Office 365 deployment, you can migrate the contents of user mailboxes from a source email system to Microsoft 365 or Office 365. When you do this all at one time, it's called a cutover migration. Choosing a cutover migration is suggested when:

- Your current on-premises Exchange organization is Microsoft Exchange Server 2003 or later.
- Your on-premises Exchange organization has fewer than 2,000 mailboxes.

    Note

    Even though cutover migration supports moving up to 2000 mailboxes, due to length of time it takes to create and migrate 2000 users, it is more reasonable to migrate 150 users or fewer.

## Plan for migration

Setting up an email cutover migration to Microsoft 365 or Office 365 requires careful planning. Before you begin, here are a few things to consider:

- You can move your entire email organization to Microsoft 365 or Office 365 over a few days and manage user accounts in Microsoft 365 or Office 365.
- A maximum of 2,000 mailboxes can be migrated to Microsoft 365 or Office 365 by using a cutover Exchange migration. However, we recommend that you only migrate 150 mailboxes.
- The primary domain name used for your on-premises Exchange organization must be an accepted as a domain owned by you in your Microsoft 365 or Office 365 organization.
- After the migration is complete, each user who has an on-premises Exchange mailbox also will be a new user in Microsoft 365 or Office 365, but you must still assign licenses to users whose mailboxes are migrated.

    Note

    When migrating from Exchange 2003, TCP port 6001, 6002 and 6004 need to be open on the Exchange 2003 side.

## Impact to users

After your on-premises and Microsoft 365 or Office 365 organizations are set up for a cutover migration, post-setup tasks could impact your users.

- **Administrators or users must configure desktop computers**: Make sure that desktop computers are updated and set up for use with Microsoft 365 or Office 365. These actions allow users to use local user credentials to sign in to Microsoft 365 or Office 365 from desktop applications. Users with permission to install applications can update and set up their own desktops. Or updates can be installed for them. After updates are made, users can send email from Outlook 2013, Outlook 2010, or Outlook 2007.
- **Potential delay in email routing**: Email sent to on-premises users whose mailboxes were migrated to Microsoft 365 or Office 365 are routed to their on-premises Exchange mailboxes until the MX record is changed.

## How does cutover migration work?

The main steps you perform for a cutover migration are shown in the following illustration.

![Process for performing a cutover email migration to Microsoft 365 or Office 365.](../exchangeonline/mailbox-migration/media/a607954b-1ab6-40e6-becc-d61ad5a35d69.png)

1. The administrator communicates upcoming changes to users and verifies domain ownership with the domain registrar.
2. The administrator prepares the servers for a cutover migration and creates empty mail-enabled security groups in Microsoft 365 or Office 365.
3. The administrator connects Microsoft 365 or Office 365 to the on-premises email system (this is called creating a migration endpoint).
4. The administrator migrates the mailboxes and then verifies the migration.
5. Grant Microsoft 365 or Office 365 licenses to your users.
6. The administrator configures the domain to begin routing email directly to Microsoft 365 or Office 365.
7. The administrator verifies that routing has changed, and then deletes the cutover migration batch.
8. The administrator completes post-migration tasks in Microsoft 365 or Office 365 (assigns licenses to users and creates an Autodiscover Domain Name System (DNS) record), and optionally decommissions the on-premises Exchange servers.
9. The administrator sends a welcome letter to users to tell them about Microsoft 365 or Office 365 and to describe how to sign in to their new mailboxes. (See [Overview of Outlook e-mail profile](https://support.microsoft.com/office/overview-of-outlook-e-mail-profiles-9073a8ac-c3d6-421d-b5b9-fcedff7642fc) for information on creating new Outlook profiles).

## Ready to run a cutover migration?

Expand the sections below and follow the steps.

## Prepare for a cutover migration

Before you migrate mailboxes to Microsoft 365 or Office 365 by using a cutover migration, there are a few changes to your Exchange Server environment you must complete first.

Note

If you have turned on directory synchronization, you need to turn it off before you can perform a cutover migration. You can do this by using PowerShell. For instructions, see [Turn off directory synchronization](/en-us/office365/enterprise/turn-off-directory-synchronization).

1. **Configure Outlook Anywhere on your on-premises Exchange Server**: The email migration service uses Outlook Anywhere (also known as RPC over HTTP), to connect to your on-premises Exchange Server. Outlook Anywhere is automatically configured for Exchange 2013. For information about how to set up Outlook Anywhere for Exchange 2010, Exchange 2007, and Exchange 2003, see the following:

    - [Exchange 2010: Enable Outlook Anywhere](/en-us/previous-versions/office/exchange-server-2010/bb123542%28v=exchg.141%29)
    - [Exchange 2007: How to Enable Outlook Anywhere](/en-us/previous-versions/office/exchange-server-2007/bb123889%28v=exchg.80%29)
    - [How to configure Outlook Anywhere with Exchange 2003](/en-us/previous-versions/office/exchange-server-2007/aa996922%28v=exchg.80%29)
2. You must use a certificate issued by a trusted certification authority (CA) with your Outlook Anywhere configuration in order for Microsoft 365 or Office 365 to run a cutover migration. If you're doing a cutover migration, you need to add the Outlook Anywhere and Autodiscover services to your certificate. For instructions on how to set up certificates, see:

    - [Add an SSL certificate to Exchange 2013](add-an-ssl-certificate-to-exchange-2013)
    - [Add an SSL certificate to Exchange 2010](add-an-ssl-certificate-to-exchange-2010)
    - [Add an SSL certificate to Exchange 2007](add-an-ssl-certificate-to-exchange-2007)
3. **Optional: Verify that you can connect to your Exchange organization using Outlook Anywhere**: Try one of the following methods to test your connection settings.

    - Use Outlook from outside your corporate network to connect to your on-premises Exchange mailbox.
    - Use the [Microsoft Exchange Remote Connectivity Analyzer](/en-us/connectivity-analyzer/exchange-remote-connectivity-analyzer-tool) to test your connection settings. Use the Outlook Anywhere (RPC over HTTP) or Outlook Autodiscover tests.
    - Wait for the connection to automatically be tested when you connect Microsoft 365 or Office 365 to your email system later in this procedure.
4. **Enable MRSProxy on your on-premises Exchange Server**: For information on how to set up MRSProxy, see [Enable the MRS Proxy endpoint in Exchange Server](/en-us/exchange/architecture/mailbox-servers/mrs-proxy-endpoint).
5. **Set permissions**: The on-premises user account that you use to connect to your on-premises Exchange organization (also called the migration administrator) must have the necessary permissions to access the on-premises mailboxes that you want to migrate to Microsoft 365 or Office 365. This user account is used when you connect Microsoft 365 or Office 365 to your email system later in this procedure. To migrate the mailboxes, the admin must have one of the following permissions:

    - The migration administrator must be assigned the **FullAccess** permission for each on-premises mailbox.

    or

    - The migration administrator must be assigned the **Receive As** permission on the on-premises mailbox database that stores user mailboxes.

    For instructions about how to set these permissions, see [Assign Exchange permissions to migrate mailboxes to Microsoft 365 or Office 365](assign-permissions-for-migration).
6. Verify that the mailboxes to be migrated are **not hidden from the address lists**.
7. **Disable Unified Messaging (UM)**: If UM is turned on for the on-premises mailboxes you're migrating, turn off UM before migration. [Turn on Cloud Voicemail](/en-us/microsoftteams/set-up-phone-system-voicemail) for your users after the migration is complete.
8. **Create security groups and clean up delegates**: Because the email migration service can't detect whether on-premises Active Directory groups are security groups, it can't provision any migrated groups as security groups in Microsoft 365 or Office 365. If you want to have security groups in Microsoft 365 or Office 365, you must first provision an empty mail-enabled security group in Microsoft 365 or Office 365 before starting the cutover migration.

    Additionally, this migration method only moves mailboxes, mail users, mail contacts, and mail-enabled groups with their membership. If any other Active Directory object, such as user mailbox that isn't migrated to Microsoft 365 or Office 365 is assigned as a manager or delegate to an object being migrated, you must remove them from the object before migration.

## Step 1: Verify you own the domain

During the migration, the Simple Mail Transfer Protocol (SMTP) address of each on-premises mailbox is used to create the email address for a new Microsoft 365 or Office 365 mailbox. To run a cutover migration, the on-premises domain must be a verified domain in your Microsoft 365 or Office 365 organization.

1. Sign in to Microsoft 365 or Office 365 with your work or school account.
2. Choose **Setup** &gt; **Domains**.
3. On the **Domains-** page, select **Add domain** to start the domain wizard.

    ![Choose Add domain.](../exchangeonline/mailbox-migration/media/b0267b62-3f20-4c76-be75-40f9c2274433.png)
4. On the **Add a domain** page, type in the domain name (for example, Contoso.com) you use for your on-premises Exchange organization, and then choose **Next**.
5. On the **Verify domain** page, select either **Sign in to GoDaddy** (if your DNS records are managed by GoDaddy) or **Add a TXT record instead** for any other registrars &gt; **Next**.
6. Follow the instructions provided for your DNS hosting provider. The TXT record usually is chosen to verify ownership.

    You can also find the instructions in [Add DNS records to connect your domain](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).

    After you add your TXT or MX record, wait about 15 minutes before proceeding to the next step.
7. In the Office 365 domain wizard, choose **done, verify now**, and you see a verification page. Choose **Finish**.

    If the verification fails at first, wait awhile, and try again.

    Don't continue to the next step in the domain wizard. You now have verified that you own the on-premises Exchange organization domain and are ready to continue with an email migration.

## Step 2: Connect Microsoft 365 or Office 365 to your email system

A migration endpoint contains the settings and credentials needed to connect the on-premises server that hosts the mailboxes you're migrating with Microsoft 365 or Office 365. The migration endpoint also defines the number of mailboxes to migrate simultaneously. For a cutover migration, you create an Outlook Anywhere migration endpoint.

1. In the Exchange admin center, go to **Migration**.
2. Select **Endpoints** in the top right corner of the page.
3. On the **Endpoints** page, select **Add**![New icon.](../exchangeonline/mailbox-migration/media/457cd93f-22c2-4571-9f83-1b129bcfb58e.gif).
4. On the **Add Endpoint** page, choose **Outlook Anywhere** as the migration type, and select **Next**.
5. Enter the appropriate information in the following fields:

    - **Migration endpoint name**: Type a unique endpoint name, for example, Test5-endpoint
    - **Account with privileges**: Type the *username* (domain\username format or an email address) for an account that has the necessary administrative permissions in the on-premises organization. Microsoft 365 or Office 365 will use this account to detect the migration endpoint and to test the permissions assigned to this account by attempting to access the mailbox with the specified email address.
    - **Password of account with privileges**: Type the *password* for the account with privileges that is the administrator account
    - **Email address**: Type the *email address* of any user in the on-premises Exchange organization that will be migrated. Microsoft 365 or Office 365 will test the connectivity to this user's mailbox. Make sure that this mailbox isn't\_ hidden from the address lists.
    - **Exchange server**: Type the *fully qualified domain name* (FQDN) for the on-premises Exchange Server. This is the host name for your Mailbox server. For example, EXCH-SRV-01.corp.contoso.com.
    - **RPC proxy server**: Type the *FQDN* for the RPC proxy server for Outlook Anywhere. Typically, the proxy server is the same as your Outlook on the web (formerly known as Outlook Web App) URL. For example, mail.contoso.com, which is also the URL for the proxy server that Outlook uses to connect to an Exchange Server.

        Note

        Leave the default values unchanged in *Maximum concurrent migrations* and *Maximum concurrent incremental styles*.
6. Select **Create**.

You successfully created a new endpoint!

To validate whether your Exchange Online is connected to the on-premises server, you can run the command in Example 4 of [Test-MigrationServerAvailability](/en-us/powershell/module/exchangepowershell/Test-MigrationServerAvailability).

## Step 3: Create the cutover migration batch

In a cutover migration, on-premises mailboxes are migrated to Microsoft 365 or Office 365 in a single migration batch.

1. In the Exchange admin center, go to **Migration**, and select **Add migration batch**.

    ![add migration batch](../exchangeonline/mailbox-migration/media/cutover-migration1.png)
2. On the **Add migration batch** page,

    - **Give migration batch a unique name**: Type a migration name, for example, test\_batch5.
    - **Select the mailbox migration path**: Verify that **Migration to Exchange Online** is selected.

    ![select migration type](../exchangeonline/mailbox-migration/media/cutover-migration2.png)
3. On the **Select the migration type** page, choose **Cutover migration** as migration type, and select **Next**.

    ![prerequisites](../exchangeonline/mailbox-migration/media/cutover-migration3.png)
4. Go through the prerequisites for cutover migration, and select **Next** again.

    ![set an endpoint](../exchangeonline/mailbox-migration/media/cutover-migration5.png)
5. On the **Set a migration endpoint** page, select a migration end point from the dropdown.
6. On the **Schedule batch migration** page, select start and end time for the migration batch. Here,

    - **Manually start the batch later**: The migration batch is created but isn't started. The status of the batch is set to **Created**. To start a migration batch, select it from the list, and then choose **Start**.
    - **Automatically start the batch**: The migration batch is started as soon as you save the new migration batch with a status of **Syncing**.
    - **Start the batch automatically after time**: The migration batch starts on the selected later date and time, which must be within 30 days in the future (relatively).
    - **Manually completing the batch later**: The migration batch is synced but isn't completed. The status of the batch is set to **Synced**. To complete a migration batch, select the batch from the list, and select **Complete migration batch**.
    - **Automatically completing the migration batch**: The migration batch completes as soon as the status changes to **Synced**.
    - **Complete the batch automatically after time**: The migration batch ends on the selected later date and time, which must be within 120 days in the future (relatively).
7. Select **Save** to create the migration batch, and select **Done**.

## Step 4: Start the cutover migration batch

If you created a migration batch and configured it to be started manually, you can start it by using the Exchange admin center.

1. In the Exchange admin center, go to **Migration**.
2. Select the batch from the list and select **Resume migration**.
3. Select **Confirm** in the pop-up to begin migration.
4. If a migration batch starts successfully, its status on the migration dashboard changes to **Starting**.

### Verify the synchronization worked

You can follow the sync status on the migration dashboard. If there are errors, you can view a log file that gives you more information about them.

You can also verify that the users get created in the Microsoft 365 admin center as the migration proceeds.

After the migration is done, the status is displayed as **Synced**.

## Optional: Reduce email delays

Although this task is optional, doing it can help avoid delays in the receiving email in the new Microsoft 365 or Office 365 mailboxes.

When people outside of your organization send you email, their email systems don't double-check where to send that email every time. Instead, their systems save the location of your email system based on a setting in your DNS server known as a time-to-live (TTL). If you change the location of your email system before the TTL expires, the sender's email system tries to send email to the old location before figuring out that the location changed. This location change can result in a mail delivery delay. One way to avoid this is to lower the TTL that your DNS server gives to servers outside of your organization. This makes the other organizations refresh the location of your email system more often.

Most email systems ask for an update each hour if a short interval such as 3,600 seconds (one hour) is set. We recommended that you set the interval at least this low before you start the email migration. This setting allows all the systems that send you email enough time to process the change. Then, when you make the final switch over to Microsoft 365 or Office 365, you can change the TTL back to a longer interval.

The place to change the TTL setting is on your email system's MX record. This lives on your public-facing DNS system. If you have more than one MX record, you need to change the value on each record to 3,600 seconds or less.

If you need some help configuring your DNS settings, see [Add DNS records to connect your domain](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).

## Step 5: Route your email directly to Microsoft 365 or Office 365

Email systems use a DNS record called an MX record to figure out where to deliver emails. During the email migration process, your MX record was pointing to your source email system. Now that the email migration to Microsoft 365 or Office 365 is complete, it's time to point your MX record at Microsoft 365 or Office 365. This helps make sure that email is delivered to your Microsoft 365 or Office 365 mailboxes. Moving the MX record will also let you turn off your old email system when you're ready.

For many DNS providers, there are specific instructions to change your MX record. If your DNS provider isn't included, or if you want to get a sense of the general directions, [general MX record instructions](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider) are provided as well.

It can take up to 72 hours for the email systems of your customers and partners to recognize the changed MX record. Wait at least 72 hours before you proceed to the next task: Delete the cutover migration batch.

## Step 6: Delete the cutover migration batch

After you change the MX record and verify that all email is being routed to Microsoft 365 or Office 365 mailboxes, notify the users that their mail is going to Microsoft 365 or Office 365. After this, you can delete the cutover migration batch. Verify the following before you delete the migration batch.

- All users are using Microsoft 365 or Office 365 mailboxes. After the batch is deleted, mail sent to mailboxes on the on-premises Exchange Server isn't copied to the corresponding Microsoft 365 or Office 365 mailboxes.
- Microsoft 365 or Office 365 mailboxes were synchronized at least once after mail began being sent directly to them. To do this, make sure that the value in the **Last Synced Time** box for the migration batch is more recent than when mail started being routed directly to Microsoft 365 or Office 365 mailboxes.

When you delete a cutover migration batch, the migration service cleans up any records related to the migration batch and then deletes the migration batch. The batch is removed from the list of migration batches on the migration dashboard.

1. In the Exchange admin center, go to **Migration**.
2. Select the required batch, and then select **Delete**.

    Note

    It can take a few minutes or the batch to be removed.
3. Select **Confirm** in the pop-up to delete the migration batch.

The migration batch is no longer listed.

## Step 7: Assign licenses to Microsoft 365 and Office 365 users

**Activate user accounts for the migrated accounts by assigning licenses**: If you don't assign a license, the mailbox is disabled when the grace period ends (30 days). To assign a license in the Microsoft 365 admin center, see [Add users individually or in bulk](/en-us/microsoft-365/admin/add-users/add-users).

## Complete post migration tasks

After migrating mailboxes to Microsoft 365 or Office 365, there are post-migration tasks that must be completed.

1. **Create an Autodiscover DNS record so users can easily get to their mailboxes**: After all on-premises mailboxes are migrated to Microsoft 365 or Office 365, you can configure an Autodiscover DNS record for your Microsoft 365 or Office 365 organization to enable users to connect easily to their new Microsoft 365 or Office 365 mailboxes with Outlook and mobile clients. This new Autodiscover DNS record has to use the same namespace that you're using for your Microsoft 365 or Office 365 organization. For example, if your cloud-based namespace is cloud.contoso.com, the Autodiscover DNS record you need to create is autodiscover.cloud.contoso.com.

    If you keep your Exchange Server, you should also make sure that Autodiscover DNS CNAME record has to point to Microsoft 365 or Office 365 in both internal and external DNS after the migration so that the Outlook client connects to the correct mailbox. Replace &lt;ServerName&gt; with the name of the Client Access server and run the following command in the Exchange Management Shell to prevent client connections to the server. You need to run the command on every Client Access server.

    ```PowerShell
    Set-ClientAccessServer -Identity <ServerName> -AutoDiscoverServiceInternalUri $null
    ```

    Microsoft 365 or Office 365 uses a CNAME record to implement the Autodiscover service for Outlook and mobile clients. The Autodiscover CNAME record must contain the following information:

    - **Alias:** autodiscover
    - **Target:** autodiscover.outlook.com

    For more information, see [Add DNS records to connect your domain](/en-us/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).
2. **Decommission on-premises Exchange Servers**: After you verify that all email is being routed directly to the Microsoft 365 or Office 365 mailboxes, and no longer need to maintain your on-premises email organization or don't plan on implementing a single sign-on solution, you can uninstall Exchange from your servers and remove your on-premises Exchange organization.

    For more information, see the following articles:

    - [Modify or Remove Exchange 2010](/en-us/previous-versions/office/exchange-server-2010/ee332361%28v=exchg.141%29)
    - [How to Remove an Exchange 2007 Organization](/en-us/previous-versions/office/exchange-server-2007/aa998313%28v=exchg.80%29)
    - [How to Uninstall Exchange Server 2003](/en-us/previous-versions/tn-archive/bb125110%28v=exchg.65%29)

    Note

    Decommissioning Exchange can have unintended consequences. Before decommissioning your on-premises Exchange organization, we recommend that you contact Microsoft Support.