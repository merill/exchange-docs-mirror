---
layout: Conceptual
title: Configure document collaboration with Microsoft OneDrive and Microsoft Exchange Server 2016 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/hybrid-deployment/set-up-document-collaboration
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
ms.topic: how-to
ms.service: exchange-server-it-pro
ms.localizationpriority: medium
ms.custom:
- has-azure-ad-ps-ref
ms.collection:
- Hybrid
- Ent_O365_Hybrid
- M365-email-calendar
ms.assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms.reviewer: 
description: Admins can learn how to configure document collaboration with Microsoft OneDrive and Microsoft Exchange Server 2016.
ms.date: 2018-06-25T00:00:00.0000000Z
locale: en-us
document_id: 5394ebb7-dc48-2e50-dddc-99bf551a1ad0
document_version_independent_id: 9eb60f34-6da2-958e-5009-123f03768383
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeHybrid/hybrid-deployment/set-up-document-collaboration.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../hybridtoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hybrid-deployment/set-up-document-collaboration
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeHybrid/hybrid-deployment/set-up-document-collaboration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7428317a-e6c2-4461-ad3e-8a8ad3608734
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e4f59707-f107-48f2-8d75-0afd91868cd7
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
platformId: ce049dc1-c1d7-363a-fff2-f859e5fef636
---

# Configure document collaboration with Microsoft OneDrive and Microsoft Exchange Server 2016 | Microsoft Learn

**Summary**: How to allow your on-premises Exchange 2016 users to take advantage of using document collaboration with Microsoft OneDrive and SharePoint Online while in a hybrid configuration.

A file attachment option named *document collaboration* is available in Microsoft 365 and Office 365. This option allows on-premises Outlook on the web clients (formerly known as Outlook Web App or OWA) to integrate attachments stored on OneDrive directly in email messages.

Traditionally, a user sends a file to others by attaching it to an email message. This method has the following issues:

- Changes by each individual recipient are unique to their copy of the attachment.
- The attached files take up storage space in each user's mailbox.

With document collaboration, users can insert a link to a file that's stored in a OneDrive account. Recipients can modify the file at the same source location with no extra storage required.

Before the Exchange 2016 environment is configured for document collaboration, the file attachment dialogs in Outlook on the web looks like this:

![Traditional file attachment dialog in Outlook on the web in Exchange 2016.](../exchangehybrid/media/f8c74d70-42f9-48c6-b263-ce6cef8591a8.png)

After the environment is configured as described in this article, the file attachment dialog in Outlook on the web looks like this:

![File attachment dialog in Outlook on the web in Exchange 2016 with modern attachments enabled.](../exchangehybrid/media/89eeae65-ce3a-4c47-b57e-db734a1de95b.png)

Users in your organization with on-premises mailboxes and OneDrive for work or school accounts in Microsoft 365 or Office 365 are eligible to use the modern attachment method. The location of the recipients (online versus on-premises) doesn't matter.

For more information about hybrid deployments, see [Exchange Server Hybrid Deployments](../exchange-hybrid).

## What do you need to know before you begin?

- Estimated time to complete: 15 minutes
- Review [Exchange Server Hybrid Deployments](../exchange-hybrid), and make sure you understand the areas that are affected by configuring a hybrid deployment.
- Review and complete all hybrid deployment requirements outlined in [Hybrid deployment prerequisites](../hybrid-deployment-prerequisites).
- To use PowerShell in Exchange 2016, see the following articles:

    - [Open the Exchange Management Shell](/en-us/powershell/exchange/open-the-exchange-management-shell)
    - [Connect to Exchange servers using remote PowerShell](/en-us/powershell/exchange/connect-to-exchange-servers-using-remote-powershell)

Tip

Having problems? Ask for help in the Exchange Hybrid forum at [Exchange | Hybrid management](/en-us/answers/tags/377/office-exchange-hybrid-management).

## Configure Exchange 2016 to enable document collaboration in a hybrid environment

Verify that the following prerequisite steps are complete, and then use the procedure that follows to enable document collaboration.

**Prerequisites**:

- Configure your Exchange hybrid environment using the [Hybrid Configuration wizard](../hybrid-configuration-wizard) (HCW).
- Exchange 2016 must be installed in your on-premises organization. Exchange 2016 can coexist with earlier versions of Exchange, but document collaboration only works for mailboxes on an Exchange 2016 server.
- The authenticating server must be installed with all users synchronized. You can use the [Get-AuthServer](/en-us/powershell/module/exchangepowershell/get-authserver) cmdlet to find your authenticating server. We recommend using the HCW from an Exchange 2016 server to make any necessary OAuth configurations.

    Important

    OAuth between Exchange 2016 and the cloud must be configured. For more information, see [Configure OAuth Authentication Between Exchange and Exchange Online Organizations](../configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help).
- Users need to be licensed for either SharePoint Online or OneDrive for work or school. You can verify a user's license by selecting the user in the Microsoft 365 admin center and selecting the **Edit** button. For more information, see [OneDrive](/en-us/onedrive/onedrive).

Do the following steps:

1. Configure the default Outlook on the web mailbox policy with the OneDrive host URL.

    Tip

    Use the SharePoint admin center in Microsoft 365 or Office 365 to retrieve the OneDrive host URL. For example, `https://contoso-my.sharepoint.com` is a My Site Host URL for Contoso.

    Although the built-in Outlook on the web mailbox policy in Exchange 2016 is named "Default," it isn't automatically applied to mailboxes unless do one of the upcoming procedures.

    - Make the policy the default policy by running the following command in the Exchange Management Shell: `Set-OWAMailboxPolicy -Identity Default -IsDefault $true`. To confirm the default policy, rune the following command: ``.
    - Assign the Outlook web app mailbox policy directly to mailboxes. For more information, see [Apply or remove an Outlook Web App mailbox policy on a mailbox](/en-us/exchange/apply-or-remove-outlook-web-app-mailbox-policy-exchange-2013-help).

    This example uses the Exchange Management Shell to configure the internal and external MySite URLs in the Default Outlook on the web mailbox policy:

    ```powershell
    Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com
    ```
2. Apply the default Outlook on the web mailbox policy to users by doing either of the following steps in the Exchange Management Shell:

    - **Make the policy named Default the default policy**: Run the following command:

        ```powershell
        Set-OwaMailboxPolicy -Identity Default -IsDefault
        ```

        To verify that the policy is the default policy, run the following command:

        ```powershell
        Get-OWAMailboxPolicy | Format-Table Name,IsDefault
        ```
    - **Assign the policy named Default to users**: To assign the policy to an individual mailbox, replace &lt;MailboxIdentity&gt; with the name, alias, email address or UPN of the user, and then run the following command:

        ```powershell
        Set-CASMailbox -Identity <MailboxIdentity> -OwaMailboxPolicy Default
        ```
3. (Optional) On each Exchange 2016 server, restart the web app pool named **OWAApplicationPool** by running the following command. This step allows the configuration to work immediately. If you don't run this command, it takes a few minutes for Exchange to apply the updated mailbox policy. In the Exchange Management Shell run:

    ```powershell
    Restart-WebAppPool MSExchangeOWAAppPool
    ```

Outlook on the web users are now offered a choice for the type of attachments to include in email messages: traditional or modern.

![Attachment options dialog, Share with OneDrive or Send as attachment.](../exchangehybrid/media/7d2f27c2-3638-479a-a577-029ac61e7d95.png)