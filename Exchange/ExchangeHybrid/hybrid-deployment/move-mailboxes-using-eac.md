---
layout: Conceptual
title: Use the EAC to move mailboxes | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/move-mailboxes-using-eac
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
audience: ITPro
ms.topic: upgrade-and-migration-article
f1.keywords:
- CSH
ms.custom:
- O365E_HRCMoveRequest_FL312271
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
- M365-email-calendar
ms.assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms.reviewer: 
description: This article describes how to move mailboxes using the Exchange Admin Center (EAC).
ms.date: 2024-10-03T00:00:00.0000000Z
locale: en-us
document_id: 33ef039d-1855-01a8-4f07-691c962c9a15
document_version_independent_id: 9ba7b6d1-4799-6a27-c693-b1a1cae64b1c
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/move-mailboxes-using-eac.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/move-mailboxes-using-eac
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/move-mailboxes-using-eac.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 9d5494f3-3005-6070-8fb2-29e3952f4195
---

# Use the EAC to move mailboxes | Microsoft Learn

Using the Exchange Admin Center (EAC), you can move mailboxes from an on-premises organization to an Exchange Online organization, and from an Exchange Online organization to an on-premises organization.

## Move on-premises mailboxes to Exchange Online organization

To move on-premises mailboxes to Exchange Online organizations, perform the following steps:

1. In the on-premises EAC, go to **Home** &gt; **Migration**.
2. Select **Add migration batch**.
3. On the **Add migration batch** page:

    1. In the **Give migration batch a unique name** text box, enter a name for the migration batch.
    2. From the **Select the mailbox migration path** drop-down list, select **Migration to Exchange Online**.
    3. Select **Next**.
4. From the **Select the migration type** drop-down list, select **Remote move migration**, and then select **Next**.
5. On the **Prerequisites for remote migration** page, select **Next**.

    Note

    If you've already created a migration endpoint, you'll receive an endpoint confirmation prompt for this step. If you've created two or more migration endpoints, you must choose an endpoint from the **Select migration endpoint** drop-down list.
6. From the **Select migration endpoint** drop-down list, select a migration endpoint, and then select **Next**.
7. On the **Add user mailboxes** page:

    1. Select **Manually add users to migrate**.

        Note

        The **Manually add users to migrate** option can be used to migrate a mailbox (or mailboxes) of a single user. If you want to migrate the mailboxes of users in bulk, use the **Migrate from CSV file** option. For more information on this option, see [CSV files for Mailbox migration in Exchange Online](/en-us/exchange/mailbox-migration/csv-files-for-migration).
    2. In the **Enter display names of mailboxes you want to migrate** text box, enter the name or email address of the user whose mailboxes you want to migrate.
    3. Select the mailboxes that you want to move to Exchange Online, and then Select **Next**.

    Note

    If shared mailbox accounts don't appear in the user selection list, you need to sync the shared mailbox on-premises AD accounts to Microsoft 365 or Office 365 by using cloud sync or Microsoft Entra Connect. The shared mailbox AD accounts appear as blocked accounts in the Microsoft 365 admin center and you can select them from the user list.
8. From the **Target delivery domain** drop-down list, select a domain, and then select **Next**.
9. On the **Schedule batch migration** page:

    1. In the search box under **After the batch is complete, a report will be sent to the following recipients. You must select at least one recipient to receive this report**, enter a name or email address, and from the list displayed, select a user.
    2. From the **Start the migration batch by** pane, select one of the following options:

        1. **Manually start the batch later (by selecting it in the migration dashboard and then clicking Start)**: When you choose this option, the batch is saved with a **Start** button in the dashboard (the **Migration batches** page) for you to select whenever you want the batch migration to start.
        2. **Automatically start the batch**: When you choose this option, the batch migration starts immediately.
        3. **Start the batch automatically after time**: When you choose this option and set the date and time at which you want the batch migration to start, the batch migration automatically starts on the specified date and time.
    3. From the **End the migration batch by** pane, select one of the following options:

        1. **Manually completing the batch later (by clicking "Complete this migration batch" link on the right pane, after the link becomes active)**: When you choose this option, the batch that's to be migrated and that's displayed on the dashboard displays a **Complete the migration** button for you to select whenever you want.
        2. **Automatically complete the migration batch**: When you choose this option, the batch migration is completed automatically.
        3. **Complete the batch automatically after time**: When you choose this option and set the date and time at which you want the batch migration to complete, the batch migration automatically completes at the specified time.

        Note

        If you select **Manually completing the batch later (by clicking "Complete this migration batch" link on the right pane, after the link becomes active)** in step **9(c)(i)**, Exchange Online only synchronizes 95% of each mailbox in that batch. Exchange Online periodically synchronizes the batch to keep each mailbox at 95% synchronization until the batch is manually completed by selecting the **Complete this migration batch**, at which point the remaining 5% is migrated.
10. From the **Select timezone** drop-down list, select a timezone, and then select **Save**.

    Note

    The entries in the migration report are based on the **UTC** timezone by default. The admin can select another timezone (other than **UTC**) of choice from the **Select timezone** drop-down list. Then, the entries in the migration report will be based on the chosen timezone.
11. Select **Done**.
12. On the **Migration batches** page, select your migration batch, and then select **Resume migration**.
13. Select **Confirm**.
14. Close the page that displays the notification message **Operation successful**.
15. Check for your migration batch and verify whether its status is **Starting**.

If you encounter issues during the mailbox moves, or during the creation of a migration batch, see [Troubleshoot migration issues in Exchange Server hybrid environment](/en-us/exchange/troubleshoot/move-or-migrate-mailboxes/troubleshoot-migration-issues-in-exchange-hybrid).

## Move Exchange Online mailboxes to on-premises organization

You can use the remote move migration wizard in the EAC in Exchange Online to move existing cloud mailboxes to the on-premises Exchange organization:

1. In the Exchange Online EAC, go to **Home** &gt; **Migration**.
2. Select **Add migration batch**.
3. On the **Add migration batch** page:

    1. In the **Give migration batch a unique name** text box, enter a name for the migration batch.
    2. From the **Select the mailbox migration path** drop-down list, select **Migration from Exchange Online**.
    3. Select **Next**.
4. From the **Select migration endpoint** drop-down list, select a migration endpoint, and then select **Next**.
5. On the **Add user mailboxes** page:

    1. Select **Manually add users to migrate**.
    2. In the **Enter display names of mailboxes you want to migrate** text box, enter the name or email address.
    3. Select the mailboxes that you want to move to Exchange Online, and then Select **Next**.

        Note

        You must select a user mailbox, and not a shared mailbox. The user whose mailbox is being chosen for migration must be a mail-enabled user.
6. On the **Move configuration** page:

    1. From the **Target delivery domain** drop-down list, select a domain.
    2. From the **Move options** pane, select any one of the displayed options.
    3. Under **Target Database**, in the **Enter database name you'd like this mailbox to be moved to** text box, enter the destination database to which you want to move the mailbox.

        Note

        The destination database is the one at the on-premises organization.
    4. Select **Next**.
7. On the **Schedule batch migration** page:

    1. Under **After the batch is complete, a report will be sent to the following recipients. You must select at least one recipient to receive this report**, in the search box, enter a name or email address, and then from the list displayed, select a user from the search results.
    2. From the **Start the migration batch by** pane, select one of the following options:

        1. **Manually start the batch later (by selecting it in the migration dashboard and then clicking Start)**: When you choose this option, the batch is saved with a **Start** button in the dashboard (the **Migration batches** page) for you to select whenever you want the batch migration to start.
        2. **Automatically start the batch**: When you choose this option, the batch migration starts immediately.
        3. **Start the batch automatically after time**: When you choose this option and set the date and time at which you want the batch migration to start, the batch migration automatically starts on the specified date and time.
    3. From the **End the migration batch by** pane, select one of the following options:

        1. **Manually completing the batch later (by clicking "Complete this migration batch" link on the right pane, after the link becomes active)**: When you choose this option, the batch that's to be migrated and that's displayed on the dashboard displays a **Complete the migration** button for you to select whenever you want.
        2. **Automatically complete the migration batch**: When you choose this option, the batch migration is completed automatically.
        3. **Complete the batch automatically after time**: When you choose this option and set the date and time at which you want the batch migration to complete, the batch migration automatically completes at the specified date and time.

            Note

            If you select **Manually completing the batch later (by clicking "Complete this migration batch" link on the right pane, after the link becomes active)** in step \**7*(c)(i)\*\*, Exchange Online only synchronizes 95% of each mailbox in that batch. Exchange Online periodically synchronizes the batch to keep each mailbox at 95% synchronization until the batch is manually completed by selecting **Complete this migration batch**, at which point the remaining 5% is migrated.
    4. From the **Select timezone** drop-down list, select a timezone, and then select **Save**.
8. From the page that displays the message **Batch creation successful**, select **Done**.
9. Select your migration batch, and then select **Resume migration**.
10. Select **Confirm**.
11. Close the page that displays the notification message **Operation successful**.
12. Check for your migration batch and verify that its status is **Starting**.

## Known issues

1. **Inaccessibility to a network during mailbox onboarding**: You may encounter a scenario wherein your connectivity to a network might have got terminated temporarily. This scenario can occur during or after you've onboarded an Exchange mailbox to the Exchange Online organization. To continue the process of "Exchange mailbox onboarding" or to access the onboarded Exchange mailboxes despite no network connectivity, perform the following task:

    - **Ensure that the *Turn on offline access* option is always enabled**: Offline access in Outlook on the web (formerly called Outlook Web App) lets users access their mailboxes when they're not connected to a network. If you migrate Exchange mailboxes to Exchange Online, users have to reset the offline access setting in their browser to use Outlook on the web offline. For more information about offline access in Outlook on the web, the browsers that support it, and how to turn it on, see [Using Outlook Web App offline](https://support.microsoft.com/office/3214839c-0604-4162-8a97-6856b4c27b36).
2. **Blockage in mailbox offboarding process**: When you try to offboard an Exchange mailbox, you may receive a message that reads:**Error: MigrationPermanentException: Cannot find a recipient that has mailbox GUID &lt;GUID&gt;.**

    For information on how to troubleshoot on seeing this error message, see the following article:

    [(MigrationPermanentException Cannot find a recipient that has mailbox GUID) error when moving mailboxes](/en-us/exchange/troubleshoot/move-mailboxes/migrationpermanentexception-when-moving-mailboxes).

## How do you know this worked?

When you move existing user mailboxes between the on-premises and Exchange Online organizations, the successful completion of the remote move wizard is your first indication that the "move mailboxes" process has completed as expected.

Because the mailbox move process takes several minutes to complete, you can also verify that the move is working correctly by opening the EAC and navigating through **Office 365** &gt; **Recipients** &gt; **Migration** to display the move status for the mailboxes selected in the remote move wizard. The value of the **Status** is **Syncing** during the mailbox move, and it's **Completed** when the mailbox has successfully moved to either the on-premises or Exchange Online organization.

After the mailbox move has completed, you can check that the remote mailbox located on the on-premises or Exchange Online organization has been successfully moved by verifying the mailbox properties. To do this, go to **Recipients** &gt; **Mailboxes** in the EAC for either the on-premises organization or Exchange Online organization. The user mailbox should show a **Mailbox Type** of **Office 365** for Exchange Online mailboxes and **User** for on-premises mailboxes.

You can also run the following cmdlet in the Exchange Management Shell to verify the status of the migration batch:

```PowerShell
Get-MigrationBatch -Identity <batch name>
```

Having problems? Ask for help in the Exchange Hybrid forum at [Exchange | Hybrid management](/en-us/answers/tags/377/office-exchange-hybrid-management).

To implement the next step of removing the completed migrated batches, see [Remove completed migration batches](remove-completed-migration-batches#remove-completed-migration-batches).