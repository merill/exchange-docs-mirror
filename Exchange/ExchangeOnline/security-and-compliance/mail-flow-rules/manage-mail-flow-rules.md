---
layout: Conceptual
title: Manage mail flow rules in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules
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
description: Admins can learn how to view, create, modify, remove enable or disable, and import or export mail flow rules in Exchange Online.
ms.topic: how-to
author: AshaIyengar21
ms.author: serdars
ms.assetid: e7a81372-b6d7-4d1f-bc9e-a845a7facac2
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
ms.date: 2023-08-28T00:00:00.0000000Z
locale: en-us
document_id: 736d8598-4bde-5f1c-5eef-2f9b648912f6
document_version_independent_id: eb74141c-161c-d1db-e95c-032f3dfdf8ec
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/manage-mail-flow-rules.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/manage-mail-flow-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/manage-mail-flow-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 1d58e732-3e9c-6fca-26cb-b25432b1401d
---

# Manage mail flow rules in Exchange Online | Microsoft Learn

In cloud-based organizations, you can use Exchange mail flow rules (also known as transport rules) to look for specific conditions on messages that pass through your organization and take action on them.

This article shows you how to create, copy, adjust the order, enable or disable, delete, import or export rules, and monitor rule usage.

Tip

To ensure that your rules work the way you expect, ensure that you thoroughly test each rule and interactions between rules.

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.
- For information about how to access the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can perform these procedures. To see what permissions you need, see the "Mail flow" entry in [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions).
- For information about keyboard shortcuts that may apply to the procedures in this article, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center).

Tip

Having problems? Ask for help in the Exchange Online forum at [Exchange Online](/en-us/answers/tags/11/office-exchange-online).

## Create a mail flow rule

You can create a mail flow rule in the EAC or in PowerShell. In the EAC, you can also create a mail flow rule by copying an existing rule.

Note

After you create or copy a mail flow rule, it might take 30 minutes or more for the new rule to be applied to emails.

### Use the EAC to create a mail flow rule

The EAC allows you to create mail flow rules by selecting a template or starting from scratch.

1. In the new EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. On the **Rules** page, create the rule by using one of the following options:

    - To create a rule from a template, select **Add a rule**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif) and select a template from the drop-down list.
    - To create a new rule from scratch, select **Add a rule**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif) &gt; **Create a new rule**.

    The new rule wizard opens.
3. On the **Set rule conditions** page, enter a unique name for the rule in the **Name** box, and then select the conditions, exceptions, and actions for the rule:

    - **Apply this rule if...**: Select a condition from the list.

        - Some conditions require other values. For example, if you select **The sender is...**, you also need to specify a sender address. If you're adding a word or phrase, trailing spaces aren't allowed.
        - To add more conditions, select **Add condition**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif) and then repeat this step.
        - Select **Delete condition**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.gif) to remove the condition.
        - To apply to all messages in the organization, select the **Apply to all messages** condition.
    - **Do the following...**: Select an action from the list.

        - Some actions require other values. For example, if you select **Forward the message for approval to...**, you need to select a recipient in your organization.
        - To add more actions, select **Add action**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif) and then repeat this step.
        - Select **Delete action**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.gif) to remove the action.
    - **Except if...**: Use this setting to specify any exceptions to the rule. The available exceptions are identical to the available conditions.

        - Some exceptions require other values. For example, if you select **The sender is...**, you also need to specify a sender address. If you're adding a word or phrase, trailing spaces aren't allowed.
        - To add more exceptions, select **Add exception**![Add Icon.](../../exchangeonline/media/itpro_eac_addicon.gif) and then repeat this step.
        - Select **Delete exception**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.gif) to remove the exception.

    When you're finished on the **Set rule conditions** page, select **Next**.
4. On the **Set rule settings** page, configure the following settings:

    - **Rule mode**: Select one of the following values:

        - **Enforce**: Turn on the rule and start processing messages immediately. All actions on the rule are taken.
        - **Test with Policy Tips**: Turn on the rule, and any Policy Tip actions ( **Notify the sender with a Policy Tip**) are sent, but no actions related to message delivery are taken.
        - **Test without Policy Tips**: Only the **Generate incident report** action is enforced. No actions related to message delivery are taken.
    - **Severity**: Select a severity level for this rule. Rule matches are grouped by severity level in activity reports. Severity level is just a filter to make the reports easier to use. The severity level has no impact on the priority that the rule is processed in.

        - **Not specified**
        - **Low**
        - **Medium**
        - **High**
        - **Not audit**: Rule matches don't appear in rule reports.
    - **Activate this rule on** and **Deactivate this rule on**: Use these settings to turn the rule on and off for a specific time period. If you create the rule before **Activate this rule on** date, the rule is enabled but it isn't processed. After the **Deactivate this rule on** date, the rule remains enabled but it isn't processed.
    - **Stop processing more rules**: Use this setting to prevent additional rules from being applied to the message after this rule. If a message is processed by this rule, no subsequent rules are processed for that message.
    - **Defer the message if rule processing doesn't complete**: Specify how the message should be handled if rule processing can't finish. By default, the rule is ignored and processing of the message by other rules continues. If you select this option, the message is resubmitted for processing.
    - **Match sender address in message**: Specify which email address is evaluated by conditions or exceptions that inspect the sender's email address:

        - **Header**: Only the message headers are examined.
        - **Envelope**: Only the SMTP message envelope is examined.
        - **Header or envelope**: Both the message headers and SMTP message envelope are examined.
    - **Comments**: Add an optional comment to the rule.

    When you're finished on the **Set rule settings** page, select **Next**.
5. On the **Review and finish** page, verify the settings. Select **Back** or use the **Edit rule conditions** or **Edit rule settings** links to modify the settings.

    When you're finished on the **Review and finish** page, select **Finish**.
6. On the confirmation page, select **Done**.

### Use Exchange Online PowerShell to create a mail flow rule

The following example creates a new mail flow rule that prepends the text `External message to Sales DG:` to the Subject line of external messages that are sent to the Sales Department distribution group:

```PowerShell
New-TransportRule -Name "Mark messages from the Internet to Sales DG" -FromScope NotInOrganization -SentTo "Sales Department" -PrependSubject "External message to Sales DG:"
```

For detailed syntax and parameter information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).

Note

The parameters and action used in the previous example are for illustration only. Review all the available mail flow rule conditions and actions to determine which ones meet your requirements.

### Use the EAC to copy a mail flow rule

1. In the new EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. On the **Rules** page, select the rule by selecting the radio button that appears next to the **Status** value, and then select the **Duplicate**![Copy Icon.](../../exchangeonline/media/itpro_eac_copyicon.gif) action that appears.
3. In the **Make a copy of "&lt;Rule Name&gt;"** flyout that opens, the values on the **Conditions** and **Settings** tabs are filled in with the settings of the copied rule. The default name is **Copy of &lt;Rule Name&gt;**. You can change any of the rule settings. The available settings are identical to creating a new rule as explained in the Use the EAC to create a mail flow rule section.
4. When you finished editing the settings of the rule, select **Make copy** at the bottom of the flyout.
5. In the confirmation flyout that opens, select **Duplicate**.
6. In the success flyout that opens, select **Close X**.

### How do you know that you've successfully created a mail flow rule?

To verify that you've successfully created a mail flow rule, do either of the following steps:

- On the **Rules** page in the EAC at https://admin.exchange.microsoft.com/#/transportrules, verify that the mail flow rule you created or copied is listed.
- In Exchange Online PowerShell, replace &lt;New Rule Name&gt; with the name of the rule that you created or copied and run the following command:

    ```PowerShell
    Get-TransportRule -Identity "<New Rule Name>""
    ```

## View or modify a mail flow rule

Note

After you modify a mail flow rule, it might take 30 minutes or more for the updated rule to be applied to emails.

### Use the EAC to view or modify a mail flow rule

1. In the new EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. On the **Rules** page, select a rule from the list by clicking anywhere in the row other than the round checkbox next to the name.
3. In the details flyout that opens you can see the existing settings and make changes by selecting **Edit rule conditions** and **Edit rule settings** at the top of the flyout. The available settings are identical to creating a new rule as explained in the Use the EAC to create a mail flow rule section.

### Use Exchange Online PowerShell to view or modify a mail flow rule

The following example returns a summary list of all mail flow rules in the organization:

```PowerShell
Get-TransportRule
```

To view the detailed information about a specific mail flow rule, provide the unique identifier for the rule (for example, Name, DistinguishedName, or GUID). It's helpful to send the output to the **Format-List** cmdlet to format the properties.

The following example returns all the properties of the specified mail flow rule:

```PowerShell
Get-TransportRule -Identity "Sender is a member of marketing" | Format-List
```

The following example adds an exception to the existing rule named "Sender is a member of marketing" so that it doesn't apply to messages sent by the user Kelly Rollin:

```PowerShell
Set-TransportRule -Identity "Sender is a member of marketing" -ExceptIfFrom "Kelly Rollin"
```

For detailed syntax and parameter information, see [Set-TransportRule](/en-us/powershell/module/exchangepowershell/set-transportrule).

### How do you know that you've successfully modified a mail flow rule?

To verify that you've successfully modified a mail flow rule, do either of the following steps:

- On the **Rules** page in the EAC at https://admin.exchange.microsoft.com/#/transportrules, select the rule that you modified by clicking anywhere in the row other than the radio button next to the **Status** value. In the details flyout that opens, confirm the settings.
- In Exchange Online PowerShell, replace &lt;Rule Name&gt; with the name of the rule that you modified and run the following command:

    ```PowerShell
    Get-TransportRule -Identity "<Rule Name>" | Format-List Name,ExceptIfFrom
    ```

## Set the priority of a mail flow rule

On the **Rules** page in the EAC, mail flow rules are shown in the order that they're processed. The rule at the top of the list has the **Priority** value 0 and is processed first.

### Use the EAC to set the priority of a rule

1. In the EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. On the **Rules** page, select a rule by selecting the radio button next to the **Status** value, and then select the **Move up** or **Move down** actions to move the rule up or down the list.

### Use Exchange Online PowerShell to set the priority of a rule

The following example sets the priority of the specified mail flow rule to 2:

```PowerShell
Set-TransportRule -Identity "Sender is a member of Marketing" -Priority "2"
```

For detailed syntax and parameter information, see [Set-TransportRule](/en-us/powershell/module/exchangepowershell/set-transportrule).

### How do you know that you've successfully set the priority of a mail flow rule

To verify that you've successfully set the priority of a mail flow rule, do either of the following steps:

- On the **Rules** page in the EAC at https://admin.exchange.microsoft.com/#/transportrules, verify the order of the rules.
- In Exchange Online PowerShell, run the following command:

    ```PowerShell
    Get-TransportRule | Format-List Name,Priority
    ```

## Enable or disable a mail flow rule

By default, the status of mail flow rule is disabled when you create them using EAC. This is done so that you can review the rule one more time before finally enabling it. You can enable the rule after the rule creation is complete.

### Use the EAC to enable or disable a mail flow rule

1. In the EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. On the **Rules** page, select the rule by clicking anywhere in the row other than the radio button next to the name. The **Status** value of the rule is **Enabled** or **Disabled**.
3. In the details flyout that opens, use the toggle in the **Enable or disable rule** section near the top of the flyout to enable or disable the rule.

### Use Exchange Online PowerShell to enable or disable a mail flow rule

The following example disables the specified mail flow rule:

```PowerShell
Disable-TransportRule -Identity "Sender is a member of marketing"
```

The following example enables the specified mail flow rule:

```PowerShell
Enable-TransportRule -Identity "Sender is a member of marketing"
```

For detailed syntax and parameter information, see [Disable-TransportRule](/en-us/powershell/module/exchangepowershell/disable-transportrule) and [Enable-TransportRule](/en-us/powershell/module/exchangepowershell/enable-transportrule).

### How do you know you've successfully enabled or disabled a mail flow rule?

To verify that you've successfully enabled or disabled a mail flow rule, do either of the following steps:

- On the **Rules** page in the EAC at https://admin.exchange.microsoft.com/#/transportrules, verify the value in the **Status** column.
- In Exchange Online PowerShell, run the following command to return a list of all rules in your organization along with their status values:

    ```PowerShell
    Get-TransportRule | Format-Table Name,State
    ```

## Remove a mail flow rule

### Use the EAC to remove a mail flow rule

1. In the EAC at https://admin.exchange.microsoft.com, go to **Mail flow** &gt; **Rules**. Or, to go directly to the **Rules** page, use https://admin.exchange.microsoft.com/#/transportrules.
2. On the **Rules** page, select the rule by selecting the radio button next to the **Status** value, and then select the **Delete**![Delete icon.](../../exchangeonline/media/itpro_eac_deleteicon.gif) action that appears.
3. In the confirmation flyout that opens, select **Confirm**.

### Use Exchange Online PowerShell to remove a mail flow rule

The following example removes the specified mail flow rule:

```PowerShell
Remove-TransportRule -Identity "Sender is a member of marketing"
```

For detailed syntax and parameter information, see [Remove-TransportRule](/en-us/powershell/module/exchangepowershell/remove-transportrule).

### How do you know that you've successfully removed a mail flow rule?

To verify that you've successfully removed the mail flow rule, do either of the following steps:

- On the **Rules** page of the EAC at https://admin.exchange.microsoft.com/#/transportrules, verify that the rule you removed is no longer listed.
- In Exchange Online PowerShell, run the following command and verify that the rule you removed is no longer listed:

    ```PowerShell
    Get-TransportRule
    ```

## Monitor rule usage

You can check the number of times each rule is matched by using **Exchange Transport Rule report** in the EAC. For a rule to be included in the report, a rule can't have the **Severity** value **Not audit** (all other values are OK). You can view the report online, or download report data to a .csv file.

Note

While most data is in the report within 24 hours, some data may take as long as 5 days to appear.

1. In the EAC at https://admin.exchange.microsoft.com, go to **Reports** &gt; **Mail flow**. Or, to go directly to the **Mail flow reports** page, use https://admin.exchange.microsoft.com/#/reports/mailflowreportsmain.
2. On the **Mail flow reports** page, find and select **Exchange Transport Rule report**.

For details about the report, see [Exchange transport rule report in the new Exchange admin center in Exchange Online](../../monitoring/mail-flow-reports/mfr-exchange-transport-rule-report).

## Import or export a mail flow rule collection in Exchange Online

Use the **Export-TransportRuleCollection** cmdlet in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) to export all of the mail flow rules in the organization to an XML file. For more information, see [Export-TransportRuleCollection](/en-us/powershell/module/exchangepowershell/export-transportrulecollection).

The **Import-TransportRuleCollection** cmdlet will be deprecated from Exchange Online PowerShell. To manually import a mail flow rules collection XML file in Exchange Online PowerShell, do the following steps:

1. Back up all existing mail flow rules using the **Export-TransportRuleCollection** cmdlet (the next step removes all existing mail flow rules, just like the **Import-TransportRuleCollection** cmdlet did). For example:

    ```powershell
    $file = Export-TransportRuleCollection
    
    [System.IO.File]::WriteAllBytes('C:\MailFlowRuleCollections\BackupRuleCollection.xml', $file.FileData)
    ```
2. Remove all existing mail flow rules in the organization by running the following command:

    ```powershell
    Get-TransportRule | foreach {Remove-TransportRule $_.Guid -Confirm:$false}
    ```
3. Copy the following text into Notepad:

    ```powershell
    if ((Get-TransportRule).Count -ne 0)
    
    {
       Write-Host "Please remove your current mail flow rules first."
    
        return
    }
    
    [xml]$xml = Get-Content "C:\MailFlowRuleCollections\RuleCollectionToImport.xml"
    
    $rulesToImport = $xml.SelectNodes("//rules/rule")
    
    if ($rulesToImport.Count -eq 0)
    
    {
        Write-Host "There are no mail flow rules to be imported."
    
        return
    }
    
    Write-Host "Importing $($rulesToImport.Count) mail flow rules."
    
    $index = 0
    
    foreach ($rule in $rulesToImport)
    
    {
        $index++
    
        Write-Host "Importing rule '$($rule.Name)' $index/$($rulesToImport.Count)."
    
        Invoke-Expression $($rule.version.commandBlock.InnerText) | Out-Null
    }
    ```
4. Update the following line with the path and filename of the mail flow rule XML collection that you want to import:

    ```powershell
    [xml]$xml = Get-Content "C:\MailFlowRuleCollections\RuleCollectionToImport.xml"
    ```
5. Save the file as .ps1 in a location that's easy for you to find (for example, `C:\Data\Import-Rules.ps1`).
6. In PowerShell, use the following syntax to run the script:

    ```powershell
    & "<Path to script file>\<FileName>.ps1"
    ```

    For example:

    ```powershell
    & "C:\Data\Import-Rules.ps1"
    ```

## Need more help?

[Mail flow rules (transport rules) in Exchange Online](mail-flow-rules)

[Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions)

[Mail flow rule actions in Exchange Online](mail-flow-rule-actions)

[Journal, transport, and inbox rule limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#journal-transport-and-inbox-rule-limits)