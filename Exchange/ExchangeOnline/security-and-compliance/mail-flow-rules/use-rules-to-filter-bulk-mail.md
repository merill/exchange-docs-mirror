---
layout: Conceptual
title: Use mail flow rules to filter bulk email in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-filter-bulk-mail
Manager: serdars
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
f1.keywords:
- NOCSH
ms.author: serdars
author: serdars
audience: ITPro
ms.topic: how-to
ms.localizationpriority: medium
search.appverid:
- MET150
ms.assetid: 2889c82e-fab0-4e85-87b0-b001b2ccd4f7
ms.collection:
- M365-security-compliance
description: Learn how to use mail flow rules (transport rules) to identify bulk email and request spam filtering in Exchange Online.
ms.custom:
- seo-marvel-apr2020
- msecd-doc-authoring-1015
ms.service: exchange-online
ms.date: 2026-08-11T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7832b4a6-3080-e5cc-3a53-17455e754b5a
document_version_independent_id: 6976eee4-ccac-1fc3-f158-2b87223fd1f2
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-filter-bulk-mail.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/mail-flow-rules/use-rules-to-filter-bulk-mail
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-filter-bulk-mail.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 87af6b5f-1328-7bb4-5f7b-ebf9253a736c
---

# Use mail flow rules to filter bulk email in Exchange Online | Microsoft Learn

In cloud-based organizations, anti-spam policies (also known as spam filter policies or content filter policies) scan inbound messages for spam and bulk mail (also known as gray mail). For more information, see [Configure anti-spam policies](/en-us/defender-office-365/anti-spam-policies-configure).

If you want more options to filter bulk mail, you can create mail flow rules (also known as transport rules) to search for text patterns or phrases that are frequently found in bulk mail and request that spam filtering treat those messages as spam. The requested SCL value is an input to cloud filtering, not a final verdict. For more information about bulk mail, see [What's the difference between junk email and bulk email?](/en-us/defender-office-365/anti-spam-spam-vs-bulk-about) and [Bulk complaint level (BCL) in cloud organizations](/en-us/defender-office-365/anti-spam-bulk-complaint-level-bcl-about).

Use the procedures in this article to create the mail flow rules in the Exchange admin center (EAC) or Exchange Online PowerShell.

## What do you need to know before you begin?

- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Exchange Online permissions](../../permissions-exo/permissions-exo): You need the **Transport Rules** role, which is assigned to the **Compliance Management**, **Records Management**, and **Organization Management** role groups by default.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Exchange Administrator** or **Global Administrator**^\*^ roles.

        Important

        ^\*^ Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.
- To open the EAC in Exchange Online, see [Exchange admin center in Exchange Online](../../exchange-admin-center). To open the EAC in the Built-in security add-on for on-premises mailboxes, see [Exchange admin center in the Built-in security add-on for on-premises mailboxes](/en-us/exchange/standalone-eop/exchange-admin-center-eop).
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- For more information about mail flow rules in cloud-based organizations, see the following topics:

    - [Mail flow rules (transport rules) in Exchange Online](mail-flow-rules)
    - [Mail flow rule conditions and exceptions (predicates) in Exchange Online](conditions-and-exceptions)
    - [Mail flow rule actions in Exchange Online](mail-flow-rule-actions)
- The list of words and text patterns that are used to identify bulk mail in the examples isn't exhaustive; you can add and remove entries as necessary. However, they're a good starting point.
- The search for words or text patterns in the subject or other header fields in the message occurs *after* the message has been decoded from the MIME content transfer encoding method that was used to transmit the binary message between SMTP servers in ASCII text. You can't use conditions or exceptions to search for the raw (typically, Base 64) encoded values of the subject or other header fields in messages.
- The following procedures mark a bulk message as spam for your entire organization. However, you can add another condition to apply these rules only to specific recipients, so that you can use aggressive filtering on a few, highly targeted users, while the rest of your users (who mostly get the bulk email they signed up for) aren't impacted.

## Use the EAC to create mail flow rules that filter bulk email

1. On the **Rules** page in the Exchange admin center at https://admin.exchange.microsoft.com/#/transportrules, select ![](../../exchangeonline/media/itpro_eac_addicon.png)**Add a rule**, and then select **Create a new rule** to start the new rule wizard.
2. On the **Set rule conditions** page, configure the following settings:

    - **Name**: Enter a unique, descriptive name for the rule.
    - **Apply this rule if**: Configure one of the following settings to look for content in messages using regular expressions (RegEx) or words or phrases:

        - **The subject or body** &gt; **subject or body matches these text patterns**: In the **Specify words or phrases** flyout that opens, enter one of the following values, select **Add**, and repeat until you enter all of the values:

            - `If you are unable to view the content of this email\, please`
            - `\>(safe )?unsubscribe( here)?\</a\>`
            - `If you do not wish to receive further communications like this\, please`
            - `<img height="?1"? width="?1"? src=.?http\://`
            - `To stop receiving these+emails\:http\://`
            - `To unsubscribe from \w+ (e\-?letter|e?-?mail|newsletter)`
            - `no longer (wish )?(to )?(be sent|receive) w+ email`
            - `If you are unable to view the content of this email\, please click here`
            - `To ensure you receive (your daily deals|our e-?mails)\, add`
            - `If you no longer wish to receive these emails`
            - `to change your (subscription preferences|preferences or unsubscribe)`
            - `click (here to|the) unsubscribe`

        To edit an entry, select it and then select **Edit**![Edit icon.](../../exchangeonline/media/itpro-eac-editicon.png). To remove an entry, select it and then select **Delete**![Remove icon](../../exchangeonline/media/itpro-eac-deleteicon.png).

        When you're finished in the flyout, select **Save**.

        - **The subject or body** &gt; **subject or body includes any of these words**: In the **Specify words or phrases** flyout that opens, enter one of the following values, select **Add**, and repeat until you enter all of the values:

            - `to change your preferences or unsubscribe`
            - `Modify email preferences or unsubscribe`
            - `This is a promotional email`
            - `You are receiving this email because you requested a subscription`
            - `click here to unsubscribe`
            - `You have received this email because you are subscribed`
            - `If you no longer wish to receive our email newsletter`
            - `to unsubscribe from this newsletter`
            - `If you have trouble viewing this email`
            - `This is an advertisement`
            - `you would like to unsubscribe or change your`
            - `view this email as a webpage`
            - `You are receiving this email because you are subscribed`

        To edit an entry, select it and then select **Edit**![Edit icon.](../../exchangeonline/media/itpro-eac-editicon.png). To remove an entry, select it and then select **Delete**![Remove icon](../../exchangeonline/media/itpro-eac-deleteicon.png).

        When you're finished in the flyout, select **Save**.
    - **Do the following**: Select **Modify the message properties** &gt; **set the spam confidence level (SCL)**. In the **Specify SCL** flyout that appears, configure one of the following settings:

        - To request that spam filtering treat messages as **Spam**, select **6**.
        - To request that spam filtering treat messages as **High confidence spam**, select **9**.

        The requested SCL value doesn't determine the final cloud filtering verdict or action. If filtering honors the request, the action in the applicable anti-spam policy determines what happens to the message. The SCL value stamped on the message might differ from the value configured in the rule. For more information, see [Spam confidence level (SCL) in Microsoft 365](/en-us/defender-office-365/anti-spam-spam-confidence-level-scl-about).

        When you're finished in the flyout, select **Save**.

    When you're finished on the **Set rule conditions** page, select **Next**.
3. On the **Set rule settings** page, review or configure the settings, and then select **Next**.
4. On the **Review and finish** page, review the settings, and then select **Finish**.

## Use PowerShell to create mail flow rules that filter bulk email

Use the following syntax to create one or both of the mail flow rules (regular expressions vs. words):

```powershell
New-TransportRule -Name "<UniqueName>" [-SubjectOrBodyMatchesPatterns "<RegEx1>","<RegEx2>"...] [-SubjectOrBodyContainsWords "<WordOrPhrase1>","<WordOrPhrase2>"...] -SetSCL <6 | 9>
```

The following example creates a new rule named "Bulk email filtering - RegEx" that uses the same list of regular expressions from earlier in the topic to set messages as **Spam**:

```powershell
New-TransportRule -Name "Bulk email filtering - RegEx" -SubjectOrBodyMatchesPatterns "If you are unable to view the content of this email\, please","\>(safe )?unsubscribe( here)?\</a\>","If you do not wish to receive further communications like this\, please","\<img height\="?1"? width\="?1"? src=.?http\://","To stop receiving these+emails\:http\://","To unsubscribe from \w+ (e\-?letter|e?-?mail|newsletter)","no longer (wish )?(to )?(be sent|receive) w+ email","If you are unable to view the content of this email\, please click here","To ensure you receive (your daily deals|our e-?mails)\, add","If you no longer wish to receive these emails","to change your (subscription preferences|preferences or unsubscribe)","click (here to|the) unsubscribe"... -SetSCL 6
```

The following example creates a new rule named "Bulk email filtering - Words" that uses the same list of words from earlier in the topic to set messages as **High confidence spam**:

```powershell
New-TransportRule -Name "Bulk email filtering - Words" -SubjectOrBodyContainsWords "to change your preferences or unsubscribe","Modify email preferences or unsubscribe","This is a promotional email","You are receiving this email because you requested a subscription","click here to unsubscribe","You have received this email because you are subscribed","If you no longer wish to receive our email newsletter","to unsubscribe from this newsletter","If you have trouble viewing this email","This is an advertisement","you would like to unsubscribe or change your","view this email as a webpage","You are receiving this email because you are subscribed" -SetSCL 9
```

For detailed syntax and parameter information, see [New-TransportRule](/en-us/powershell/module/exchangepowershell/new-transportrule).

## How do you know this procedure worked?

To verify that you've configured mail flow rules to filter bulk email, do any of the following steps:

- In the EAC, go to **Mail flow** &gt; **Rules** &gt; select the rule &gt; select **Edit**![Edit icon.](../../exchangeonline/media/itpro-eac-editicon.png), select the **Settings** tab, and verify the settings.
- In PowerShell, replace &lt;Rule Name&gt; with the name of the rule, and run the following command to verify the settings:

    ```powershell
    Get-TransportRule -Identity "<Rule Name>" | Format-List
    ```
- From an external account, send a test message to an affected recipient that contains one of the phrases or text patterns. Review the `SCL`, `SFV`, and `CAT` fields in the `X-Forefront-Antispam-Report` header, and verify the final filtering verdict and action. For more information, see [Anti-spam message headers](/en-us/defender-office-365/message-headers-eop-mdo).