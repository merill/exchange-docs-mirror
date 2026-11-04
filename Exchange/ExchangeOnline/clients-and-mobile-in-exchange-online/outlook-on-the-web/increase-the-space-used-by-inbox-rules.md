---
layout: Conceptual
title: Modify the space used by Inbox rules in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/increase-the-space-used-by-inbox-rules
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
ms.custom:
- has-azure-ad-ps-ref
description: Admins can learn how to increase or decrease the space that's available to store Inbox rules in mailboxes in an Exchange Online organization.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: 3f01edde-1cdc-4891-ad9d-7d01582664e9
ms.reviewer: 
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: outlook
f1.keywords:
- NOCSH
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 3d76e96a-b0a9-552b-e0cf-fa5a1caeee85
document_version_independent_id: 93a0041c-a6ea-0255-0127-a2ad8d4ba436
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/increase-the-space-used-by-inbox-rules.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: clients-and-mobile-in-exchange-online/outlook-on-the-web/increase-the-space-used-by-inbox-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/clients-and-mobile-in-exchange-online/outlook-on-the-web/increase-the-space-used-by-inbox-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 6a401b51-c957-678b-21d4-3f1b1b9095d0
---

# Modify the space used by Inbox rules in Exchange Online | Microsoft Learn

Inbox rules in Outlook on the web (formerly known as Outlook Web App) and the Outlook desktop apps are limited to 256 KB total for all rules. Each rule you create will take up space in your mailbox. The actual amount of space a rule uses depends on several factors, such as how long the name is and how many conditions you've applied. When you reach the 256 KB limit, you'll be warned that you can't create any more rules or that you can't update a rule. You can't increase the amount of space that's allocated to store Inbox rules in Exchange Online, but you can decrease it to suit your business needs.

**Notes**:

- The valid range for the Inbox rules quota is 32 KB to 256 KB.
- There isn't a maximum number of rules that users can create.
- The quota for Inbox rules applies only to *enabled* rules. There's no restriction on the number of *disabled* rules that a mailbox can have. However, the *total size* of rules that are enabled or active in the mailbox can't exceed the quota value

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes or less.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox settings" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- You can only use Exchange Online PowerShell to perform the procedure in this article. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Use Exchange Online PowerShell to increase the limit for Inbox rules

There are three basic methods you can use to modify the rules quota for a mailbox:

- **Individual mailboxes**: Use the following syntax:

    ```PowerShell
    Set-Mailbox -Identity <MailboxIdentity> -RulesQuota "<32 KB to 256 KB>"
    ```

    This example decreases the rules quota to 200 KB for the user douglas@contoso.com.

    ```PowerShell
    Set-Mailbox -Identity douglas@contoso.com -RulesQuota "200 KB"
    ```
- **Filter mailboxes by attributes**: This method requires that the mailboxes all share a unique filterable attribute. For example:

    - Title, Department, or address information for user accounts as seen by the **Get-User** cmdlet.
    - CustomAttribute1 through CustomAttribute15 for mailboxes by as seen the **Get-Mailbox** cmdlet.

    The syntax uses the following two commands (one to identify the mailboxes, and the other to apply the rules quota to the mailboxes):

    ```PowerShell
    $<VariableName> = <Get-User | Get-Mailbox> -ResultSize unlimited -Filter <Filter>
    ```

    ```PowerShell
    $<VariableName> | foreach {Set-Mailbox -Identity $_.MicrosoftOnlineServicesID -RulesQuota "<32 KB to 256 KB>"}
    ```

    This example decreases the rules quota to 32 KB to all mailboxes whose **Title** attribute contains "Vendor" or "Contractor".

    ```PowerShell
    $V = Get-User -ResultSize unlimited -Filter "(RecipientType -eq 'UserMailbox') -and (Title -like '*Vendor*' -or Title -like '*Contractor*')"
    ```

    ```PowerShell
    $V | foreach {Set-Mailbox -Identity $_.MicrosoftOnlineServicesID -RulesQuota "32 KB"}
    ```
- **Use a list of specific mailboxes**: This method requires a text file to identify the mailboxes. Values that don't contain spaces (for example, the user account) work best. The text file must contain one user account on each line like this:

> 
> akol@contoso.com  tjohnston@contoso.com  kakers@contoso.com

    The syntax uses the following two commands (one to identify the user accounts, and the other to apply the rules quota to those users):

    ```PowerShell
    $<VariableName> = Get-Content "<text file>"
    ```

    ```PowerShell
      $<VariableName> | foreach {Set-Mailbox -Identity $_ RulesQuota "<32 KB to 256 KB>"}
    ```

    This example decreases the rules quota to 150 KB to the mailboxes specified in the file C:\My Documents\Junior Managers.txt.

    ```PowerShell
    $Jr = Get-Content "C:\My Documents\Junior Managers.txt"
    ```

    ```PowerShell
    $Jr | foreach {Set-Mailbox -Identity $_ -RulesQuota "150 KB"}
    ```

## How do you know this worked?

To verify that you've modified the Inbox rules quota on a mailbox, use any of the following steps in Exchange Online PowerShell:

- Replace &lt;MailboxIdentity&gt; with the name, alias, email address, or account name of the mailbox, and run the following command to verify the value of the **RulesQuota** property:

    ```PowerShell
    Get-Mailbox -Identity "<MailboxIdentity>" | Format-List RulesQuota
    ```
- Run the following command to verify the value of the **RulesQuota** property for all mailboxes:

    ```PowerShell
    Get-Mailbox -ResultSize unlimited | Format-Table Name,RulesQuota -Auto
    ```

## What else do I need to know?

- Inbox rules are run from top to bottom in the order in which they appear in the **Rules** window. To change the order of rules, click the rule you want to move, and then click the up or down arrow to move the rule to the position you want in the list.
- When you create a forwarding rule, you can add more than one address to forward to. The number of addresses you can forward may be limited, depending on the settings for your account. If you add more addresses than are allowed, your forwarding rule won't work. If you create a forwarding rule with more than one address, test it to be sure it works.