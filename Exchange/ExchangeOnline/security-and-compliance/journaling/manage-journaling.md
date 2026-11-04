---
layout: Conceptual
title: Manage journaling in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/journaling/manage-journaling
Manager: laurawi
ms.subservice: exo-security-compliance
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
description: Admins can learn how to view, create, modify, enable, disable, and delete journal rules for Exchange Online.
ms.topic: how-to
author: k-reagle
ms.author: kreagle
ms.assetid: d517f27e-f80a-4a06-988c-cbbf981c701d
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2026-06-26T00:00:00.0000000Z
locale: en-us
document_id: 4d49df7f-4717-d51e-b1b9-5a5a4768a1d9
document_version_independent_id: af6d6557-eb97-6aba-4511-c64e951ab31f
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/journaling/manage-journaling.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/journaling/manage-journaling
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/journaling/manage-journaling.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: abde4ddb-09f1-43df-5072-872d673b7a22
---

# Manage journaling in Exchange Online | Microsoft Learn

This article shows you how to perform basic tasks related to managing the older compliance feature of [journaling in Exchange Online](journaling). They're necessary only if you have to store email outside Exchange Online. Make sure you're aware of the [limitations and considerations](journaling#considerations-for-journaling) of this older feature before you configure any new journaling rules.

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Journaling" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions) article.
- Currently, you can use either the [Microsoft Purview compliance portal](/en-us/purview/purview-compliance-portal) or the [Classic Exchange admin center (EAC)](/en-us/exchange/features-in-classic-eac) to manage journaling in Exchange Online.
- You need to have a journaling mailbox and an alternate journaling mailbox configured. For more information, see [Configure Journaling in Exchange Online](configure-journaling).
- In Exchange Online, there's a limit to the number of journal rules that you can create. For details, see [Journal, Transport, and Inbox rule limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#journal-transport-and-inbox-rule-limits).
- If you're having trouble with the **JournalingReportDNRTo** mailbox, see [Mail flow rules and Inbox rules in Exchange Online don't work as expected](https://support.microsoft.com/help/2829319).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Create a journal rule

Important

If your organization is set up in a [hybrid deployment](/en-us/exchange/exchange-hybrid), you must configure any journaling rules twice; once in on-premises Exchange Server and an identical rule in Exchange Online. If you don't, some messages might not be journaled.

### Use the Purview compliance portal to create a journal rule

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), navigate to **Solutions** &gt; **Data lifecycle management** &gt; **Exchange (legacy)** &gt; **Journal rules**, and then select **+ New rule**.
2. On the **Define journal rule settings** page, provide a name for the journal rule and then complete the following fields:

    - **Send journal reports to**: Type the address of the journaling mailbox that will receive all the journal reports.

        Note

        You can also type the display name or alias of a mail user or a mail contact as the journal mailbox. In this case, journal reports will be sent to the external email address of the mail user or mail contact. But as previously explained, the external email address of a mail user or mail contact can't be the address of an Exchange Online mailbox.
    - **Journal rule name**: Enter the name of this new journal rule.
    - **Journal messages sent or received from**: Specify the recipient that the rule will target. You can either apply the rule to all messages, or select a specific recipient.
    - **Type of message to journal**: Specify the scope of the journal rule. You can journal all messages regardless of origin or destination, internal messages only, or external messages only.
3. Select **Next**, review the settings, and then **Submit** to create the journal rule.

### Use the classic EAC to create a journal rule

1. In the Classic EAC, navigate to **Compliance management** &gt; **Journal rules**, and then click **Add**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif).
2. In **Journal rule**, provide a name for the journal rule and then complete the following fields:

    - **If the message is sent to or received from**: Specify the recipient that the rule will target. You can either select a specific recipient or apply the rule to all messages.
    - **Journal the following messages**: Specify the scope of the journal rule. You can journal only the internal messages, only the external messages, or all messages regardless of origin or destination.
    - **Send journal reports to**: Type the address of the journaling mailbox that will receive all the journal reports.

        Note

        You can also type the display name or alias of a mail user or a mail contact as the journal mailbox. In this case, journal reports will be sent to the external email address of the mail user or mail contact. But as previously explained, the external email address of a mail user or mail contact can't be the address of an Exchange Online mailbox.
3. Click **Save** to create the journal rule.

### Use Exchange Online PowerShell to create a journal rule

This example creates the journal rule Discovery Journal Recipients to journal all messages sent from and received by the recipient user1@contoso.com.

```PowerShell
New-JournalRule -Name "Discovery Journal Recipients" -Recipient user1@contoso.com -JournalEmailAddress "Journal Mailbox" -Scope Global -Enabled $True
```

### How do you know this worked?

To verify that you have successfully created the journal rule, do one of the following:

- From the admin portal you used to create the journaling rule, verify that the new journal rule you created is listed on the **Journal rules** tab.
- From Exchange Online PowerShell, verify that the new journal rule exists by running the following command (the example below verifies the rule created in Exchange Online PowerShell example above):

    ```PowerShell
    Get-JournalRule -Identity "Discovery Journal Recipients"
    ```

## View or modify a journal rule

### Use the Purview compliance portal to view or modify a journal rule

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), navigate to **Solutions** &gt; **Data lifecycle management** &gt; **Exchange (legacy)** &gt; **Journal rules**.
2. In the list view, you'll see all the journal rules in your organization.
3. Select the rule you want to view or modify, and select **Edit**.
4. On the **Define journal rule settings** page, modify the settings you want, select **Next**, and **Submit**. For more information about the settings, see the previous procedure to create a journal rule.

### Use the classic EAC to view or modify a journal rule

1. Sign in to the Classic EAC and navigate to **Compliance management** &gt; **Journal rules**.
2. In the list view, you'll see all the journal rules in your organization.
3. Double-click the rule you want to view or modify.
4. In **Journal Rule**, modify the settings you want. For more information about the settings in this dialog box, see the previous procedure to create a journal rule.

### Use Exchange Online PowerShell to view or modify a journal rule

This example displays a summary list of all journal rules in the Exchange organization:

```PowerShell
Get-JournalRule
```

This example retrieves the journal rule Brokerage Journal Rule, and pipes the output to the **Format-List** command to display rule properties in a list format:

```PowerShell
Get-JournalRule -Identity "Brokerage Journal Rule" | Format-List
```

If you want to modify the properties of a specific rule, you need to use the [Set-JournalRule](/en-us/powershell/module/exchangepowershell/set-journalrule) cmdlet. This example changes the name of the journal rule `JR-Sales` to `TraderVault`. The following rule settings are also changed:

- Recipient
- JournalEmailAddress
- Scope

```PowerShell
Set-JournalRule -Identity "JR-Sales" -Name TraderVault -Recipient traders@woodgrovebank.com -JournalEmailAddress tradervault@woodgrovebank.com -Scope Internal
```

### How do you know this worked?

To verify that you have successfully modified a journal rule, do one of the following:

- From the admin portal where you modified the journal rule, on the **Journal rules** tab, double-click the rule you modified and verify your changes were saved.
- From Exchange Online PowerShell, verify that you modified the journal rule successfully by running the following command. This command will list the properties you modified along with the name of the rule (the example below verifies the rule modified in Exchange Online PowerShell example above):

    ```PowerShell
    Get-JournalRule -Identity "TraderVault" | Format-List Name,Recipient,JournalEmailAddress,Scope
    ```

## Enable or disable a journal rule

Important

When you disable a journal rule, the journaling agent will stop journaling messages targeted by that rule. While a journal rule is disabled, any messages that would have normally been journaled by the rule aren't journaled. Make sure that you don't compromise the regulatory or compliance requirements of your organization by disabling a journaling rule.

### Use the Microsoft Purview compliance portal to enable or disable a journal rule

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), navigate to **Solutions** &gt; **Data lifecycle management** &gt; **Exchange (legacy)** &gt; **Journal rules**.
2. In the list view, next to the rule's name, select the check box and then select **Disable** or **Enable** to enable the rule or disable the rule.

### Use the classic EAC to enable or disable a journal rule

1. In the Classic EAC, navigate to **Compliance management** &gt; **Journal rules**.
2. In the list view, in the **On** column next to the rule's name, select the check box to enable the rule or clear it to disable the rule.

### Use Exchange Online PowerShell to enable or disable a journal rule

This example enables the rule Contoso.

```PowerShell
Enable-JournalRule -Identity "Contoso Journal Rule"
```

This example disables the rule Contoso.

```PowerShell
Disable-JournalRule -Identity "Contoso Journal Rule"
```

### How do you know this worked?

To verify that you have successfully enabled or disabled a journal rule, do one of the following:

- From the Microsoft Purview compliance portal, view the list of journal rules and use the **Status** column to confirm whether the rule is enabled (**On**) or disabled (**Off**).
- From the Classic EAC, view the list of journal rules check the status of the check box in the **On** column.
- From Exchange Online PowerShell, run the following command to return a list of all journal rules in your organization along, including their status:

    ```PowerShell
    Get-JournalRule | Format-Table Name,Enabled
    ```

## Remove a journal rule

### Use the Microsoft Purview compliance center to remove a journal rule

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), navigate to **Solutions** &gt; **Data lifecycle management** &gt; **Exchange (legacy)** &gt; **Journal rules**.
2. In the list view, select the rule you want to remove, and then select **Delete**.

### Use the classic EAC to remove a journal rule

1. In the Classic EAC, navigate to **Compliance management** &gt; **Journal rules**.
2. In the list view, select the rule you want to remove, and then click **Delete**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.gif).

### Use Exchange Online PowerShell to remove a journal rule

This example removes the rule Brokerage Journal Rule.

```PowerShell
Remove-JournalRule -Identity "Brokerage Journal Rule"
```

### How do you know this worked?

To verify that you have successfully removed the journal rule, do one of the following:

- From the admin portal you used, verify that the rule you removed is no longer listed on the **Journal rules** tab after you've refreshed the page.
- From Exchange Online PowerShell, run the following command to verify that the rule you removed is no longer listed:

    ```PowerShell
    Get-JournalRule
    ```

## For more information

[New-JournalRule](/en-us/powershell/module/exchangepowershell/new-journalrule)

[Get-JournalRule](/en-us/powershell/module/exchangepowershell/get-journalrule)

[Set-JournalRule](/en-us/powershell/module/exchangepowershell/set-journalrule)

[Enable-JournalRule](/en-us/powershell/module/exchangepowershell/enable-journalrule)

[Disable-JournalRule](/en-us/powershell/module/exchangepowershell/disable-journalrule)

[Remove-JournalRule](/en-us/powershell/module/exchangepowershell/remove-journalrule)