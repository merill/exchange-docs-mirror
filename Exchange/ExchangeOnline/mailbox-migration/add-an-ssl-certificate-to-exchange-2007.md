---
layout: Conceptual
title: Add an SSL certificate to Exchange 2007 for migration to Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/mailbox-migration/add-an-ssl-certificate-to-exchange-2007
Manager: serdars
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
author: AshaIyengar21
ms.author: serdars
ms.assetid: d4524743-a63f-413f-b290-5f0d2f070392
ms.reviewer: 
description: Steps to add an SSL certificate to Exchange 2007,
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
ms.date: 2018-08-16T00:00:00.0000000Z
locale: en-us
document_id: 58f2c42c-58e0-7224-de3c-fd6afeaca192
document_version_independent_id: 2c9d0620-3164-ef8a-3191-018b4fc480f1
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/mailbox-migration/add-an-ssl-certificate-to-exchange-2007.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mailbox-migration/add-an-ssl-certificate-to-exchange-2007
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/mailbox-migration/add-an-ssl-certificate-to-exchange-2007.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: 47b92a39-e319-a44a-1347-be7a94720d0b
---

# Add an SSL certificate to Exchange 2007 for migration to Exchange Online | Microsoft Learn

Some services, such as Outlook Anywhere, Cutover migration to Microsoft 365 or Office 365, and Exchange ActiveSync, require certificates to be configured on your Microsoft Exchange Server 2007 server. This article shows you how to configure an SSL certificate from a third-party certificate authority (CA).

## Tasks for adding an SSL certificate

Adding an SSL certificate to Microsoft Exchange Server 2007 is a three step process.

1. Create a certificate request
2. Submit the request to certificate authority
3. Import the certificate

## Create a certificate request

To create a certificate request in Microsoft Exchange Server 2007, use the [New-ExchangeCertificate](/en-us/previous-versions/office/exchange-server-2007/aa998327%28v=exchg.80%29) command. To run the **New-ExchangeCertificate** command, the account you use must be in the Exchange Server Administrator role and local Administrators group for the target server.

**To create a certificate request**

1. Open the Exchange Management Shell on the local server.
2. On the command line, type:

    ```PowerShell
    New-ExchangeCertificate -DomainName "owa.servername.contoso.com","mail.servername.contoso.com","autodiscover.servername.contoso.com","sts.servername,contoso.com","oos.servername.contoso.com","mail12.servername.contoso.com","edge.servername.contoso.com" -FriendlyName "Exchange 2007 Certificate" -GenerateRequest:$true -KeySize 2048 -Path "C:\certlocation" -PrivateKeyExportable $true -SubjectName "c=us, o=ContosoCorporation, cn=servername,contoso.com"
    ```

    In the command example above, *servername* is the name of your server, *contoso.com* is an example of a domain name, and *certlocation* is a file path to the location where you want to store the request once it is generated. Replace all these placeholders with the information that appropriate for yourMicrosoft Exchange Server 2007.

    In the *DomainName* parameter, add the domain names for the certificate request. For example, if you configured your internal and external URLs to be the same, the domain name for Outlook Web Access when accessed from the internet or intranet should look like owa.*servername*.contoso.com.

    Use the *SubjectName* parameter to specify the Subject Name on the resulting certificate. This field is used by DNS-aware services and binds a certificate to a particular domain name.

    You must specify the *GenerateRequest* parameter as `$true`. Otherwise, you will create a self-signed certificate.
3. After you run the above command, a certificate request is saved in the file location you specified by using the *Path* parameter.

    The **New-ExchangeCertificate** command also creates a *Thumbprint* output parameter that you use when you submit the request to a third-party certificate authority in the next step.

## Submit the request to certificate authority

After you've saved the certificate request, submit the request to your CA. This can be an internal CA or a third-party CA, depending on your organization. Clients that connect to the Client Access server must trust the CA that you use. You can search the CA website for the specific steps for submitting your request.

## Import the certificate

After you receive the certificate from the CA, use the [Import-ExchangeCertificate](/en-us/previous-versions/office/exchange-server-2007/bb124424%28v=exchg.80%29) command to import it.

**To import the certificate request**

1. Open the Exchange Management Shell on local server.
2. On the command line, type:

    ```PowerShell
    Import-ExchangeCertificate C:\filepath
    ```

    The *filepath* parameter above specifies the location where you saved the certificate file that was provided by the third-party CA.

    When you run this command, it creates a *Thumbprint* output parameter that you use to enable to certificate in the next step.

**To enable the certificate**

1. To enable the certificate, you use the [Enable-ExchangeCertificate](/en-us/previous-versions/office/exchange-server-2007/aa997231%28v=exchg.80%29) command. On the command line, type:

    ```PowerShell
    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services iis,smtp,pop,imap
    ```

    The *Thumbprint* parameter specifies the one you received as output when you ran the **Import-ExchangeCertificate** command.

    In the *Services* parameter, specify the services you want to assign to this certificate. At a minimum, you should specify SMTP and IIS.
2. If you receive the warning **Overwrite the existing default SMTP certificate?**, type in `A` (yes for all).