---
layout: Conceptual
title: S/MIME in Exchange Online | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/smime-exo/smime-exo
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
description: Admins can learn about how S/MIME works in Exchange Online for message encryption and digitally signed messages.
ms.topic: article
author: AshaIyengar21
ms.author: serdars
ms.reviewer: smithre4
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
ms.date: 2021-05-11T00:00:00.0000000Z
locale: en-us
document_id: 146e1dad-3eff-cf6b-19aa-a859c92ac178
document_version_independent_id: 01f13ce8-3d11-9a09-5c3c-a01d9a51f887
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/smime-exo/smime-exo.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/smime-exo/smime-exo
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/smime-exo/smime-exo.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: a0e0eee8-72ea-99dc-6dc2-160de58aeb32
---

# S/MIME in Exchange Online | Microsoft Learn

S/MIME (Secure/Multipurpose internet Mail Extensions) is a widely accepted protocol for sending digitally signed and encrypted messages. S/MIME in Exchange Online provides the following services for email messages:

- **Encryption**: Protects the content of email messages.
- **Digital signatures**: Verifies the identity of the sender of an email message.

The rest of this article generally describes S/MIME and how these services work.

To configure S/MIME in Exchange Online, see the following topics:

[Configure S/MIME in Exchange Online](configure-smime-exo)

[S/MIME for Outlook for iOS and Android](../../clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/smime-outlook-for-ios-and-android)

## S/MIME digital signatures

Digital signatures are the more commonly used service of S/MIME. As the name suggests, digital signatures are the digital counterpart to the traditional, legal signature on a paper document. As with a legal signature, digital signatures provide the following security capabilities:

- **Authentication**: A signature serves to validate an identity. It verifies the answer to "who are you" by providing a means of differentiating that entity from all others and proving its uniqueness. Because there's no authentication in SMTP email, there's no way to know who sent a message. Authentication in a digital signature solves this problem by allowing a recipient to know that a message was sent by the person or organization who claims to have sent the message.
- **Nonrepudiation**: The uniqueness of a signature prevents the owner of the signature from disowning the signature. This capability is called nonrepudiation. Thus, the authentication that a signature provides gives the means to enforce nonrepudiation. The concept of nonrepudiation is most familiar in the context of paper contracts: a signed contract is a legally binding document, and it's impossible to disown an authenticated signature. Digital signatures provide the same function and, increasingly in some areas, are recognized as legally binding, similar to a signature on paper. Because SMTP email doesn't provide a means of authentication, it can't provide nonrepudiation. It's easy for a sender to disavow ownership of an SMTP email message.
- **Data integrity**: An additional security service that digital signatures provide is data integrity. Data integrity is a result of the specific operations that make digital signatures possible. With data integrity services, when the recipient of a digitally signed email message validates the digital signature, the recipient is assured that the email message that is received is, in fact, the same message that was signed and sent, and hasn't been altered while in transit. Any alteration of the message while in transit after it has been signed invalidates the signature. In this way, digital signatures provide an assurance that signatures on paper can't, because it's possible for a paper document to be altered after it has been signed.

Important

Although digital signatures provide data integrity, they don't provide confidentiality. Messages with only a digital signature are sent in clear text, like SMTP messages and can be read by others. In the case where the message is opaque-signed, a level of obfuscation is achieved because the message is base64-encoded, but it is still clear text. To protect the contents of email messages, encryption must be used.

## S/MIME encryption

Message encryption provides a solution to information disclosure. SMTP-based internet email doesn't secure messages. An SMTP internet email message can be read by anyone who sees it as it travels or views it where it's stored. These problems are addressed by S/MIME using encryption. Encryption is a way to change information so that it can't be read or understood until it's changed back into a readable and understandable form. Message encryption provides two specific security services:

- **Confidentiality**: Message encryption serves to protect the contents of an email message. Only the intended recipient can view the contents, and the contents remain confidential and can't be known by anyone else who might receive or view the message. Encryption provides confidentiality while the message is in transit and in storage.
- **Data integrity**: As with digital signatures, message encryption provides data integrity services as a result of the specific operations that make encryption possible.

Important

Although message encryption provides confidentiality, it doesn't authenticate the message sender in any way. An unsigned, encrypted message is as susceptible to sender impersonation as a message that isn't encrypted. Because nonrepudiation is a direct result of authentication, message encryption also doesn't provide nonrepudiation. Although encryption does provide data integrity, an encrypted message can show only that the message hasn't been altered since it was sent. No information about who sent the message is provided. To prove the identity of the sender, the message must use a digital signature.

## Related message encryption technologies

Other encryption technologies work together to provide protection for messages at rest and in-transit. S/MIME can work simultaneously with the technologies in the following list, but isn't dependent on them:

- **Transport Layer Security (TLS) which replaces Secure Sockets Layer (SSL)**:
    - Encrypts the tunnel or the route between email servers in order to help prevent snooping and eavesdropping.
    - Encrypts the connection between email clients and email servers.
- **BitLocker**: Encrypts data on hard drives in client computers and servers. If an unauthorized party somehow gains access, they can't read the data on the drives.

[Microsoft Purview Message Encryption](/en-us/purview/email-encryption) is a direct competitor to S/MIME, and has the following advantages over S/MIME:

- It's a policy-based encryption service that's configured by an admin to encrypt messages that are sent to anyone inside or outside of the organization. In contrast, users are required to decide whether to apply or not apply S/MIME to messages that they send.
- It's an online service that's built on Azure Rights Management (Azure RMS) and doesn't rely on a public key infrastructure. In contrast, S/MIME requires a certificate and certificate publishing infrastructure.
- Microsoft Purview Message Encryption provides additional capabilities. For example, you can customize messages with your organization's brand.