---
layout: Conceptual
title: How SMTP DNS-based Authentication of Named Entities (DANE) works | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/how-dane-secures-email
Manager: dcscontentpm
ms.subservice: exo-mail-flow
ms.devlang: powershell
ROBOTS: INDEX,FOLLOW
breadcrumb_path: /exchange/breadcrumb/toc.json
recommendations: true
uhfHeaderId: MSDocsHeader-Exchange
feedback_system: None
feedback_product_url: ''
ms.localizationpriority: medium
description: Learn how SMTP DNS-based Authentication of Named Entities (DANE) works to secure email communications between mail servers.
ms.topic: article
author: Cloud-Writer
ms.author: meerak
ms.assetid: 
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2026-07-21T00:00:00.0000000Z
locale: en-us
document_id: 0fe0c05f-239f-b4cb-f475-00d49c5b2e73
document_version_independent_id: 3071b1ec-3e04-23e9-fced-2d1e650c2a0a
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/how-dane-secures-email.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/how-dane-secures-email
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/how-dane-secures-email.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 4241796a-318d-9c77-14d7-a6e90a3f5e72
---

# How SMTP DNS-based Authentication of Named Entities (DANE) works | Microsoft Learn

The SMTP protocol is the main protocol used to transfer messages between mail servers. By default, it's not secure. The Transport Layer Security (TLS) protocol was introduced years ago to support encrypted transmission of messages over SMTP. It's commonly used opportunistically rather than as a requirement, leaving much email traffic in clear text and vulnerable to interception by bad actors. Furthermore, SMTP determines the IP addresses of destination servers through the public DNS infrastructure, which is susceptible to spoofing and man-in-the-middle (MITM) attacks. This vulnerability led to the creation of many new standards to increase security for sending and receiving email. One of those standards is DNS-based Authentication of Named Entities (DANE).

DANE for SMTP [RFC 7672](https://tools.ietf.org/html/rfc7672) uses the presence of a Transport Layer Security Authentication (TLSA) record in a domain's DNS record set to signal that a domain and its mail servers support DANE. If there's no TLSA record present, DNS resolution for mail flow works as usual without any DANE checks. The TLSA record securely signals TLS support and publishes the DANE policy for the domain. So, sending mail servers can successfully authenticate legitimate receiving mail servers using SMTP DANE. This authentication makes it resistant to downgrade and MITM attacks. DANE has direct dependencies on DNSSEC, which works by digitally signing records for DNS lookups using public key cryptography. DNSSEC checks occur on recursive DNS resolvers, the DNS servers that make DNS queries for clients. DNSSEC ensures that DNS records aren't tampered with and are authentic.

Once the MX, A/AAAA, and DNSSEC-related resource records for a domain are returned to the DNS recursive resolver as DNSSEC authentic, the sending mail server asks for the TLSA record corresponding to the MX host entries. If the TLSA record is present and proven authentic using another DNSSEC check, the DNS recursive resolver returns the TLSA record to the sending mail server.

After the authentic TLSA record is received, the sending mail server establishes an SMTP connection to the MX host associated with the authentic TLSA record. The sending mail server tries to set up TLS and compare the server's TLS certificate with the data in the TLSA record to validate that the destination mail server connected to the sender is the legitimate receiving mail server. The message is transmitted (using TLS) if authentication succeeds. When authentication fails or if TLS isn't supported by the destination server, Exchange Online retries the entire validation process. It starts with a DNS query for the same destination domain again after 15 minutes, then 15 minutes after that, then every hour for the next 24 hours. If authentication continues to fail after 24 hours of retrying, the message expires, and an NDR with error details is generated and sent to the sender.

## What are the components of DANE?

### TLSA resource record

Use the TLS Authentication (TLSA) record to associate a server's X.509 certificate or public key value with the domain name that contains the record. You can only trust TLSA records if you enable DNSSEC on your domain. If you use a DNS provider to host your domain, they might offer DNSSEC as a setting when you configure your domain. For more information about DNSSEC zone signing, see [Overview of DNSSEC](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj200221%28v=ws.11%29).

Example TLSA record:

[![Screenshot that shows an example of a TLSA record.](../exchangeonline/media/example-of-tlsa-record.png)](../exchangeonline/media/example-of-tlsa-record.png#lightbox)

The TLSA record type has four configurable fields:

**Certificate Usage Field**: Specifies how the sending email server should verify the destination email server's certificate.

| Value | Acronym | Description |
| --- | --- | --- |
| 0^1^ | PKIX-TA | Certificate used is the trust-anchor Public CA from the X.509 trust-chain. |
| 1^1^ | PKIX-EE | Certificate checked is the destination server; DNSSEC checks must verify its authenticity. |
| 2 | DANE-TA | Use server's private key from the X.509 tree that must be validated by a trust anchor in the chain of trust. The TLSA record specifies the trust anchor to be used for validating the TLS certificates for the domain. |
| 3 | DANE-EE | Only match against the destination server's certificate. |

^1^ Exchange Online follows RFC implementation guidance that Certificate Usage Field values of 0 or 1 shouldn't be used when DANE is implemented with SMTP. When a TLSA record that has a Certificate Usage field value of 0 or 1 is returned to Exchange Online, Exchange Online treats it as not usable. If all TLSA records are found unusable, Exchange Online doesn't perform the DANE validation steps for 0 or 1 when sending the email. Instead, because of the presence of a TLSA record, Exchange Online enforces the use of TLS for sending the email, sending the email if the destination email server supports TLS or dropping the email and generating an NDR if the destination email server doesn't support TLS.

In the example TLSA record, the Certificate Usage Field is set to '3', so the Certificate Association Data ('abc123...xyz789') matches only the destination server's certificate.

**Selector field**: Indicates which parts of the destination server's certificate should be checked.

| Value | Acronym | Description |
| --- | --- | --- |
| 0 | Cert | Use full certificate. |
| 1 | SPKI (Subject Public Key Info) | Use certificate's public key and the algorithm with which the public key is identified to use. |

In the example TLSA record, the Selector Field is set to '1' so the Certificate Association Data matches by using the destination server certificate's public key and the algorithm with which the public key is identified.

**Matching Type Field**: Indicates the format the certificate is represented in the TLSA record.

| Value | Acronym | Description |
| --- | --- | --- |
| 0 | Full | The data in the TLSA record is the full certificate or SPKI. |
| 1 | SHA-256 | The data in the TLSA record is an SHA-256 hash of either the certificate or the SPKI. |
| 2 | SHA-512 | The data in the TLSA record is an SHA-512 hash of either the certificate or the SPKI. |

In the example TLSA record, the Matching Type Field is set to '1' so the Certificate Association Data is an SHA-256 hash of the Subject Public Key Info from the destination server certificate.

**Certificate Association Data**: Specifies the certificate data that is used for matching against the destination server certificate. This data depends on the Selector Field value and the Matching Type Value.

In the example TLSA record, the Certificate Association data is set to 'abc123..xyz789'. Since the Selector Field value in the example is set to '1', it references the destination server certificate's public key and the algorithm that's identified to be used with it. And since the Matching Type field value in the example is set to '1', it references the SHA-256 hash of the Subject Public Key Info from the destination server certificate.

## What is the recommended TLSA record configuration?

Per RFC implementation guidance for SMTP DANE, use a TLSA record with the Certificate Usage field set to 3, the Selector field set to 1, and the Matching Type field set to 1.

## Exchange Online Mail Flow with SMTP DANE

The mail flow process for Exchange Online with SMTP DANE, shown in the following flow chart, validates domain and resource record security through DNSSEC, TLS support on the destination mail server, and that the destination mail server's certificate matches what is expected based on its associated TLSA record.

There are only two scenarios where an SMTP DANE failure results in the email being blocked:

- The destination domain signals DNSSEC support but one or more records are returned as inauthentic.
- All MX records for the destination domain have TLSA records and none of the destination server's certificates match what was expected per the TLSA record data, or a TLS connection isn't supported by the destination server.

    ![Screenshot that shows Exchange online mail flow with SMTP DANE.](../exchangeonline/media/mail-flow-smtp-dane-1.png)

## Related Technologies

| Technology | Additional Information |
| --- | --- |
| **Mail Transfer Agent - Strict Transport Security (MTA-STS)** helps thwart downgrade and Man-in-the-Middle attacks by providing a mechanism for setting domain policies that specify whether the destination email server supports TLS and what to do when TLS can't be negotiated, for example stop the transmission. | More information about Exchange Online's upcoming support for inbound and outbound MTA-STS will be published later this year. [Exchange Online Transport News from Microsoft Ignite 2020 - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/exchange-team-blog/exchange-online-transport-news-from-microsoft-ignite-2020/ba-p/1687699)[rfc8461 (ietf.org)](https://datatracker.ietf.org/doc/html/rfc8461) |
| **Sender Policy Framework (SPF)** uses IP information to ensure that destination email systems trust messages sent from your custom domain. | [How Sender Policy Framework (SPF) prevents spoofing](/en-us/microsoft-365/security/office-365-security/email-authentication-anti-spoofing) |
| **DomainKeys Identified Mail (DKIM)** uses X.509 certificate information to ensure that destination email systems trust messages sent outbound from your custom domain. | [How to use DKIM for email in your custom domain](/en-us/microsoft-365/security/office-365-security/email-authentication-dkim-configure) |
| **Domain-based Message Authentication, Reporting, and Conformance (DMARC)** works with Sender Policy Framework and DomainKeys Identified Mail to authenticate mail senders and ensure that destination email systems trust messages sent from your domain. | [Use DMARC to validate email, setup steps](/en-us/microsoft-365/security/office-365-security/email-authentication-dmarc-configure) |

## Inbound SMTP DANE with DNSSEC

### Prerequisites

Before you start, ensure you meet the following prerequisites:

1. Add the domain as an **Accepted Domain** and ensure the domain status is **Healthy** in the Microsoft 365 Admin Center. This documentation assumes the domain’s MX record is set to priority 0 or 10 and that there's no "fallback" or secondary MX record. If you have a fallback MX record, work closely with your Exchange Online Administrator to ensure changes are carried out correctly.
2. To receive the full security benefits of the feature, enable DNSSEC for your domain.
3. Access to [Exchange Online PowerShell](/en-us/powershell/exchange/exchange-online-powershell?view=exchange-ps&amp;preserve-view=true) and the permissions to run the cmdlets described in [Exchange Online PowerShell](/en-us/powershell/exchange/exchange-online-powershell?view=exchange-ps&amp;preserve-view=true).

Note

To enable DNSSEC for a domain that uses a third-party gateway, follow steps 1 through 3, following the note at the end of step 3 on third-party gateways.

### Set up inbound SMTP DANE with DNSSEC

To set up inbound SMTP DANE with DNSSEC, complete the following sections:

- Enable DNSSEC
- Enable SMTP DANE

Note

DNS record provisioning and updates can take some time to complete. DNS changes can take longer than expected to become visible due to multiple layers of caching.

#### Enable DNSSEC

1. Update the TTL of your existing MX record to the lowest TTL possible (but not lower than 30 seconds). Then, wait for the previous TTL to expire before proceeding. For example, if the TTL of your existing MX record was 3,600 seconds (1 hour) before you changed it, you need to wait 1 hour before proceeding to step 2.
2. Connect to Exchange Online PowerShell.

    Warning

    If you're using MTA-STS, you need to set your policy mode to "testing" and update the ID in the MTA-STS txt record. (You can use the current time in UTC as the new policy ID.) Then, wait for the "max\_age" of the policy to expire before proceeding. For example, if the "max\_age" of your existing STS policy was 3,600 seconds (1 hour) before you changed it, you need to wait 1 hour before proceeding.
3. For the domain that you want to enable SMTP DANE with DNSSEC, enable DNSSEC on the domain by running the following command (replace "domain" with the name of your chosen domain, for example, contosotest.com):

    ```powershell
    Enable-DnssecForVerifiedDomain -DomainName <DomainName>
    ```

    Note

    This command can take a few minutes to execute.

    **Example output of successful execution**

    | Result | DnssecMxValue | ErrorData |
    | --- | --- | --- |
    | Success | contosotest-com.o-v1.mx.microsoft |  |

    The success response provides the MX value for the domain. This value is the name that the new MX record points to for the domain you're enabling with DNSSEC. For example, `contosotest-com.o-v1.mx.microsoft`.
4. Take the "DnssecMxValue" value, go to the DNS registrar hosting the domain, add a new MX record using the value returned in step 3, set the TTL to the lowest possible value (but not lower than 30 seconds), and set the priority of the new MX record to **20**.

> 
> If you're using a third-party email gateway and want to use this value as the new Exchange Online target host to which the third-party email gateway sends your inbound mail, go to the third party’s admin portal, update the target smart host, then validate mail flow using the DNSSEC test (select “DNSSEC Validation”, not “DANE Validation [including DNSSEC]”) in the [Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/O365DaneValidation/input). If mail is flowing as expected, you don't need to continue with the remaining DNSSEC steps. If you still want to enable SMTP DANE for this domain, continue to Enable SMTP DANE and start at the step where you run `Enable-SmtpDaneInbound`.

    Warning

    If you're using MTA-STS, ensure that the policy mode is set to "testing". Then, delete the current mx row containing the legacy MX record information and add the new FQDN to your MTA-STS policy file as a new mx row. Then, update the policy ID in the policy and the MTA-STS TXT record (you can use the current time in UTC as the new policy ID).
5. Verify that the new MX is working via the [Inbound SMTP Email test](https://testconnectivity.microsoft.com/tests/O365InboundSmtp/input) by expanding the Test Steps and verifying the Mail Exchanger ending in mx.microsoft was tested successfully. You might have to retry this test, depending on DNS caching.

    **Example success output**

    [![Screenshot that shows the example of an output that notifies a success of the process implemented.](../exchangeonline/media/success-output-example.png)](../exchangeonline/media/success-output-example.png#lightbox)
6. Change the priority of the legacy MX pointing to mail.protection.outlook.com from current priority to **30**; change the priority of the MX record created in step 3 so that it's set to priority **0** (highest priority).
7. Delete the legacy MX record ending with "mail.protection.outlook.com", "mail.eo.outlook.com", or "mail.protection.outlook.de". Then, update the TTL for the MX record ending in mx.microsoft to **3,600 seconds**. Optionally, you can confirm everything is working as expected using the DNSSEC test (ensure that you select “DNSSEC Validation” during test input, not “DANE Validation [including DNSSEC]”) in the [Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/O365DaneValidation/input). You might have to retry this test, depending on DNS caching and TTLs.

#### Enable SMTP DANE

1. Update the TTL of your existing MX record to the lowest TTL possible (but not lower than 30 seconds). Then, wait for the previous TTL to expire before proceeding. For example, if the TTL of your existing MX record was 3,600 seconds (1 hour) before you changed it, you need to wait 1 hour before proceeding to step 2.
2. Connect to Exchange Online PowerShell.

    Warning

    If you're using MTA-STS, you need to set your policy mode to "testing" and update the ID in the MTA-STS txt record. (You can use the current time in UTC as the new policy ID.) Then, wait for the "max\_age" of the policy to expire before proceeding. For example, if the "max\_age" of your existing STS policy was 3,600 seconds (1 hour) before you changed it, you need to wait 1 hour before proceeding.
3. For the domain that you want to enable SMTP DANE with DNSSEC, enable DNSSEC on the domain by running the following command (replace "domain" with the name of your chosen domain, for example, contosotest.com):

    ```powershell
    Enable-DnssecForVerifiedDomain -DomainName <DomainName>
    ```

    Note

    This command can take a few minutes to execute.

    **Example output of successful execution**

    | Result | DnssecMxValue | ErrorData |
    | --- | --- | --- |
    | Success | contosotest-com.o-v1.mx.microsoft |  |

    The success response provides the MX value for the domain. This value is the name that the new MX record points to for the domain you're enabling with DNSSEC. For example, `contosotest-com.o-v1.mx.microsoft`.
4. Take the "DnssecMxValue" value, go to the DNS registrar hosting the domain, add a new MX record using the value returned in step 3, set the TTL to the lowest possible value (but not lower than 30 seconds), and set the priority of the new MX record to **20**.

    Note

    If you're using a third-party email gateway and want to use this value as the new Exchange Online target host to which the third-party email gateway sends your inbound mail, go to the third party’s admin portal, update the target smart host that the third party uses to send to Exchange Online, then validate that "mail flow working via the DNSSEC test (**ensure that you select “DNSSEC Validation” during test input**, not “DANE Validation [including DNSSEC])” in the [Microsoft Remote Connectivity Analyzer: Test Input](https://testconnectivity.microsoft.com/tests/O365DaneValidation/input)". If mail is flowing as expected, you don't need to continue following the below steps. If you want to enable SMTP DANE for this domain, skip to step 7.

    Warning

    If you're using MTA-STS, ensure that the policy mode is set to "testing". Then, delete the current mx row containing the legacy MX record information and add the new FQDN to your MTA-STS policy file as a new mx row. Then, update the policy ID in the policy and the MTA-STS TXT record (you can use the current time in UTC as the new policy ID).
5. Verify that the new MX is working via the Inbound SMTP Email test (https://testconnectivity.microsoft.com/tests/O365InboundSmtp/input) by expanding the Test Steps and verifying the Mail Exchanger ending in mx.microsoft was tested successfully. You might have to retry this test, depending on DNS caching.

    **Example success output**

    [![Screenshot that shows the example of an output that notifies a success of the process implemented.](../exchangeonline/media/success-output-example.png)](../exchangeonline/media/success-output-example.png#lightbox)
6. Change the priority of the legacy MX pointing to mail.protection.outlook.com from current priority to **30**; change the priority of the MX record created in step 3 so that it's set to priority **0** (highest priority).
7. Delete the legacy MX record ending with "mail.protection.outlook.com", "mail.eo.outlook.com", or "mail.protection.outlook.de". Then, update the TTL for the MX record ending in mx.microsoft to **3,600 seconds**. Optionally, you can confirm everything is working as expected using the DNSSEC test (ensure that you select “DNSSEC Validation” during test input, not “DANE Validation [including DNSSEC])” in the [Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/O365DaneValidation/input). You might have to retry this test, depending on DNS caching and TTLs.

    Once TTLs on the legacy MX record expire, a successful output looks like:

    [![Screenshot that shows the example of an output that notifies that domains have successfully passed the DNSSEC validation test.](../exchangeonline/media/domains-passed-dnssec-validation-test.png)](../exchangeonline/media/domains-passed-dnssec-validation-test.png#lightbox)
8. Run the following command [replace (DomainName) with the name of your chosen domain, for example, contosotest.com] if you want to enable SMTP DANE for that same domain once the DNSSEC enablement is complete:

    ```powershell
    Enable-SmtpDaneInbound -DomainName <DomainName>
    ```

    | Result | ErrorData |
    | --- | --- |
    | Success |  |
9. Verify that the TLSA record has been propagated (which can take 15-30 minutes) by using an online tool of your choice and the [Microsoft Remote Connectivity Analyzer: Test Input](https://testconnectivity.microsoft.com/tests/O365DaneValidation/input).

    Once you complete DNSSEC enablement and the SMTP DANE record (TLSA) is provisioned by Exchange Online, a successful output is displayed as shown in the following screenshot:

    [![Screenshot that shows the example of an output that notifies that domains have successfully passed the Dane validation test.](../exchangeonline/media/domains-passed-dane-validation-test.png)](../exchangeonline/media/domains-passed-dane-validation-test.png#lightbox)

    Exchange Online hosts multiple TLSA records to increase the reliability of a success of SMTP DANE validations. It's expected that some of the TLSA records fail validation. As long as one TLSA record passes validation, SMTP DANE is configured correctly, and the email is secured with SMTP DANE.

    Warning

    If you're using MTA-STS, after validating that the policy works and that the mail flows as expected, set the policy mode back to "enforce" and update the ID in the MTA-STS txt record. (You can use the current time in UTC as the new policy ID.)

#### Limitations

1. **Viral or self-service sign-up domains**: Domains that you set up as "self service" aren't currently supported with Inbound SMTP DANE with DNSSEC.
2. **onmicrosoft.com domains**: The ‘onmicrosoft.com’ domain for the tenant isn't currently supported with Inbound SMTP DANE with DNSSEC. We're investigating the support for Inbound SMTP DANE with DNSSEC for the onmicrosoft.com domains; however, the ETA is unknown.
3. **Third-party gateways**: If you use a third-party email gateway on the inbound path that accepts mail for the tenant, does some processing, then relays it to Exchange Online, you can only use this feature to secure emails relayed from the third-party gateway to Exchange Online if the third-party gateway supports SMTP DANE with DNSSEC validation. If you're in this configuration, you need to set up Inbound SMTP DANE with DNSSEC by using Exchange PowerShell.
4. **Other third-party integration with mail flow**: Some customers use third-party gateways on the outbound path, where the email is sent to the third party via a connector, the third party does some processing and then resubmits to Exchange Online, then Exchange Online finally sends the email. These customers might need to work with their third-party provider when enabling the feature so that there are no disruptions. The third-party relay needs to use a DNS lookup when submitting the email back to Exchange Online, and use the new MX record hostname -&gt; contoso-com.(subdomain).mx.microsoft created during feature enablement.
5. **Fully Delegated domains**: Domains that Microsoft hosts and use NS delegation so that Microsoft’s name servers are authoritative for the domain are supported with Inbound SMTP DANE with DNSSEC. We intend to support Inbound SMTP DANE with DNSSEC for these domains; however, the ETA is unknown.

#### Debugging issues that come up while enabling Inbound SMTP DANE with DNSSEC

##### Issues with Enable/Disable-DnssecForVerifiedDomain and Enable/Disable-SmtpDane Inbound

1. `DomainNotFound`

    **Message (DNSSEC)**: ‘DNSSEC enabling/disabling failed due to domain contoso.com not existing in AAD.‘**Messages (SMTP DANE)**:

    - ‘SMTP DANE enabling/disabling failed due to domain contoso.com not existing in AAD.’
    - ‘SMTP DANE enabling/disabling failed due to domain contoso.com not found in the list of accepted domains.’**Cause**: The provided domain wasn't found in the list of accepted domains.**Action(s) To Take**: Go to the Microsoft 365 Admin Center and ensure the domain is verified with the tenant. If the domain is healthy in the Microsoft 365 Admin Center, go to the Exchange Admin Center and ensure the domain is added as an "Accepted Domain".

    **DNSSEC**

    | Result | DnssecMxValue | ErrorData |
    | --- | --- | --- |
    | Error |  | ErrorCode: ‘DomainNotFound’ ErrorDetails ’DNSSEC enabling failed... |

    **SMTP DANE**

    | Result | ErrorData |
    | --- | --- |
    | Error | ErrorCode: ‘DomainNotFound’ ErrorDetails ’SMTP DANE enabling... |
2. `DnsSecOperationFailed`

    **Message (DNSSEC)**: ‘DNSSEC enabling/disabling failed due to AdditionalErrorDetails. Retry the operation at a later time.‘**Messages (SMTP DANE)**: SMTP DANE enabling/disabling failed due to AdditionalErrorDetails. Retry the operation at a later time.**Cause**: An attempt to create the proper DNS zone and/or records failed.**Action(s) To Take**: Try rerunning the cmdlet.

    **DNSSEC**

    | Result | DnssecMxValue | ErrorData |
    | --- | --- | --- |
    | Error |  | ErrorCode: ‘DnssecOperationFailed’ ErrorDetails ’DNSSEC enabling failed... |

    **SMTP DANE**

    | Result | ErrorData |
    | --- | --- |
    | Error | ErrorCode: ‘DnssecOperationFailed’ ErrorDetails ’SMTP DANE enabling ... |
3. `PartitionNotFound`

    **Messages (SMTP DANE)**: ‘SMTP DANE enabling/disabling failed due to domain contoso.com not having a partition.’**Cause**: DNSSEC isn't enabled for the domain.**Action(s) To Take**: Ensure that you use a DNSSEC-enabled domain.

    | Result | ErrorData |
    | --- | --- |
    | Error | ErrorCode: ‘PartitionNotFound’ ErrorDetails ’SMTP DANE enabling |
4. `DomainNotSupported`

    **Message (DNSSEC)**: ‘The specified domain is an onmicrosoft domain: contoso-com.onmicrosoft.com.’'**Messages (SMTP DANE)**: ‘The specified domain is an onmicrosoft domain: contoso-com.onmicrosoft.com.’'**Cause**: The domain is an initial or MOERA domain. Those domains aren't currently supported.**Action(s) To Take**: Ensure that you use a domain that doesn't end with ‘onmicrosoft.com.'

    **DNSSEC**

    | Result | DnssecMxValue | ErrorData |
    | --- | --- | --- |
    | Error |  | ErrorCode: ‘DomainNotSupported’ ErrorDetails ’The specified domain ... |

    **SMTP DANE**

    | Result | ErrorData |
    | --- | --- |
    | Error | ErrorCode: ‘DomainNotSupported’ ErrorDetails ’The specified domain ... |

##### Issues with Get-DnssecStatusForVerifiedDomain

1. **Message**: ‘EG001: Cannot retrieve DNSSEC feature status for domain [{domain}].’**Cause**: While validating the domain’s configuration in Exchange Online, the domain wasn't added to Exchange Online. If you think you already added this domain to Exchange Online, retry running the cmdlet as this issue might be temporary.**Action(s) To Take**: Retry the cmdlet. If it continues to fail, go to the Microsoft 365 Admin Center and complete the setup process for this domain.
2. **Message**: ‘EG002: Domain [{domain}] isn't verified domain of the organization.’**Cause**: While validating the domain’s configuration in Exchange Online, the domain was added to Exchange Online but not verified.**Action(s) To Take**: Go to the Microsoft 365 Admin Center and complete the setup and verification process for this domain.
3. **Message**: ‘DNS query error occurs while getting MX records for [{domain}] domain.’**Cause**: During DNS validation, a generic DNS failure occurred when querying the domain.**Action(s) To Take**: Retry running the cmdlet. You might need to review your configuration for the domain you're trying to enable with SMTP DANE with DNSSEC.
4. **Message**: ‘Domain [{domain}] not found.’**Cause**: During DNS validation, an NXDOMAIN failure occurred when querying the domain.**Action(s) To Take**: Retry running the cmdlet after verifying the MX record configuration for the domain. DNS propagation can take up to 48 hours for some DNS providers.
5. **Message**: ‘ED003: Domain [{domain}] found. No authentic MX records found.’**Cause**: During DNSSEC validation, an MX record that resolved to a DNSSEC-secured A record (the A record for the 'hostname' value of the MX record) wasn't found.**Action(s) To Take**: Retry running the cmdlet after verifying the MX record configuration for the domain. DNS propagation can take up to 48 hours for some DNS providers.
6. **Message**: ‘EX002: Value of MX record didn't match the expected one.’**Cause**: During MX validation, an MX record that matches the expected one wasn't found.**Action(s) To Take**: Review your MX records in your domain. Ensure that one MX record matches the expected record that is outputted after running `Enable-DnssecForVerifiedDomain` or `Get-DnssecStatusForVerifiedDomain`.
7. **Message**: ‘EX003: Priority of MX record did not match the expected one.’**Cause**: During MX validation, the expected MX record was found but its priority wasn't set to 0.**Action(s) To Take**: Set your MX record (containing the value returned when running `Enable-DnssecForVerifiedDomain`or `Get-DnssecStatusForVerifiedDomain`) to be priority **0**.
8. **Message**: ‘EX004: There is a different MX record with same preference as the expected one.’**Cause**: During MX validation, the highest-priority MX record wasn't the expected MX record.**Action(s) To Take**: If you completed steps 1 through 4 of Set up inbound SMTP DANE with DNSSEC, complete steps 5 and 6 by switching the priorities of your MX records so that the expected MX is 0 (highest priority), validating the configuration, and then deleting the legacy MX record.
9. **Message**: ‘EX005: There is a different MX record with lower preference than the expected one.’**Cause**: During MX validation, an MX record for the domain didn't match the expected MX record.**Action(s) To Take**: If you completed steps 1 through 5 of Set up inbound SMTP DANE with DNSSEC, complete step 6 by deleting the legacy MX record.
10. **Message**: ‘EX006: There is a different MX record with higher preference than the expected one.’**Cause**: During MX validation, a different MX record had higher preference than the expected one.**Action(s) To Take**: Set your legacy MX record (ending in **mail.protection.outlook.com**, **mail.eo.outlook.com**, or **mail.protection.outlook.de**) to priority **20**.
11. **Message**: ‘EX007: MX record was not found.’**Cause**: During MX validation, an MX record that matches the expected one wasn't found.**Action(s) To Take**: Review your MX records in your domain. Ensure that one MX record matches the expected record which is outputted after running `Enable-DnssecForVerifiedDomain` or `Get-DnssecStatusForVerifiedDomain`.
12. **Message**: ‘EX008: The correct MX record found, but with lower preference than expected.’**Cause**: During MX validation, the expected MX record had the wrong priority.**Action(s) To Take**: Set your MX record (containing the value returned when running `Enable-DnssecForVerifiedDomain` or `Get-DnssecStatusForVerifiedDomain`) to priority **0**.
13. **Message**: ‘EX009: The correct MX record found, but with higher preference than expected.’**Cause**: During MX validation, the expected MX record had the wrong priority.**Action(s) To Take**: Set your MX record (containing the value returned when running `Enable-DnssecForVerifiedDomain` or `Get-DnssecStatusForVerifiedDomain`) to priority **0**.
14. **Message**: ‘EX010: Unknown error while searching MX records for domain [{domain}].’**Cause**: During MX validation, a generic DNS error occurred.**Action(s) To Take**: Retry running the cmdlet after verifying the MX record configuration for the domain. DNS propagation can take up to 48 hours for some DNS providers.
15. **Message**: ‘EX012: MX records not found for domain [{domain}].’**Cause**: During MX validation, an MX record that matches the expected one wasn't found.**Action(s) To Take**: Review your MX records in your domain. Ensure that one MX record matches the expected record which is outputted after running `Enable-DnssecForVerifiedDomain` or `Get-DnssecStatusForVerifiedDomain`.
16. **Message**: ‘EX013: Unknown expected MX record for domain [{domain}].’**Cause**: During MX validation, an MX record that matches the expected one wasn't found.**Action(s) To Take**: Review your MX records in your domain. Ensure that one MX record matches the expected record which is outputted after running `Enable-DnssecForVerifiedDomain` or `Get-DnssecStatusForVerifiedDomain`.
17. **Message**: ‘ES001: Expected MX record missing in policy while mode is ‘‘enforced’’.’**Cause**: During MTA-STS validation, the mx value matching your expected record wasn't found.**Action(s) To Take**: Set the mode of your MTA-STS policy to **test**; then, add the mxhostname value (returned when running `Enable-DnssecForVerifiedDomain` or `Get-DnssecStatusForVerifiedDomain`) as a row in the MTA-STS policy.
18. **Message**: 'ES002: No expected MX record found to compare policy with. Enable DNSSEC feature for domain [{domain}] first.'**Cause**: MTA-STS was found but DNSSEC status of the domain was unretrievable.**Action(s) To Take**: Complete the steps in Set up inbound SMTP DANE with DNSSEC.

#### Mitigating mail flow issues with Inbound SMTP DANE with DNSSEC

There are three key scenarios for mail flow issues once Inbound SMTP DANE with DNSSEC is enabled:

1. **Issue with SMTP DANE validations failing**: For information on how to mitigate this issue, see Mitigating SMTP DANE validations failing.
2. **Issue with DNSSEC validations failing**: For information on how to mitigate this issue, see Mitigating DNSSEC validations failing.
3. **Issue with MX value**: For information on how to mitigate this issue, see Mitigating issues with MX value.

##### Mitigating SMTP DANE validations failing

To mitigate impact from SMTP DANE validations, run the following command:

```powershell
Disable-SmtpDaneInbound -DomainName <DomainName>
```

##### Mitigating DNSSEC validations failing

1. To mitigate any impact from DNSSEC validations failing, you need to disable DNSSEC on your domain (contoso.com) through your DNS provider.

    Note

    If disabling DNSSEC doesn't resolve the issue, the problem might be with your MX value.
2. Disable DNSSEC on your domain through your DNS provider. Then, open a support ticket with your DNS provider to find out how to safely re-enable DNSSEC for your domain.

##### Mitigating issues with MX value

1. Make sure your MX value matches the value in the **Microsoft 365 Admin Center -&gt; Settings -&gt; Domains**.
2. Select the domain, select **DNS records**, then run **Check health**.
3. Make sure the MX record shows as **OK**; if it doesn't, update the value to what is provided in the admin center.
4. Go to your DNS registrar and find the MX record for your domain. The hostname value is:

    `<MX token>.<subdomain>.mx.microsoft`
5. Create a second MX record with the following hostname value and set the priority to **20**:

    `<MX token>.mail.protection.outlook.com`

    Note

    Replace the "MX Token" value with the MX token from the current MX Record for your domain found in step 4. For example, the MX token for contosotest.com is contosotest-com.
6. Make sure the MX record you created in step 5 is working.

    Important

    One way to ensure the second MX record is working is to use the [Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/O365InboundSmtp/input).

    1. Input the domain (for example, contoso.com) into the test; then select **Perform Test**.
    2. Open **Test Steps**.
    3. Open **Test Steps** for **Testing inbound SMTP mail flow for domain “admin@(domain)”**.
    4. Open Additional Details under **Attempting to retrieve DNS MX records for domain ‘(domain)’**.
    5. Confirm that the **(MX token).mail.protection.outlook.com** MX record is healthy.
7. If mail flow works with the **MX token.mail.protection.outlook.com** MX record, run the following command:

    `Disable-DnssecForVerifiedDomain -DomainName <DomainName>`
8. Delete the DNSSEC MX record that matches the values below:

    `<MX token>.<subdomain>.mx.microsoft`
9. Make sure the MX record you created in step 5 is the only MX record, and that it's set to priority **0** (highest priority).

## How can Exchange Online customers use Outbound SMTP DANE with DNSSEC?

As an Exchange Online customer, you don't need to do anything to configure this enhanced email security for your outbound email. We built this enhanced email security for you, and it's ON by default for all Exchange Online customers. Exchange Online uses this security when the destination domain advertises support for DANE. To reap the benefits of sending email with DNSSEC and DANE checks, communicate to your business partners with whom you exchange email that they need to implement DNSSEC and DANE so they can receive email using these standards.

## Troubleshooting sending emails with SMTP DANE

Currently, there are four error codes for DANE when sending emails with Exchange Online. Microsoft is actively updating this error code list. You can see the errors in:

1. The Exchange Admin Center portal through the Message Trace Details view.
2. NDRs generated when a message isn't sent due to a DANE or DNSSEC failure.
3. Remote Connectivity Analyzer tool [Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/o365).

    | NDR Code | Description |
    | --- | --- |
    | 4/5.7.321 | starttls-not-supported: Destination mail server must support TLS to receive mail. |
    | 4/5.7.322 | certificate-expired: Destination mail server's certificate is expired. |
    | 4/5.7.323 | tlsa-invalid: The domain failed DANE validation. |
    | 4/5.7.324 | dnssec-invalid: Destination domain returned invalid DNSSEC records. |

    Note

    Currently, when a domain signals that it supports DNSSEC but fails DNSSEC checks, Exchange Online doesn't generate the 4/5.7.324 dnssec-invalid error. It generates a generic DNS error:

    `4/5.4.312 DNS query failed`

    We're actively working to remedy this known limitation. If you receive this error statement, navigate to the Microsoft Remote Connectivity Analyzer and perform the DANE validation test against the domain that generated the 4/5.4.312 error. The results show if it's a DNSSEC issue or a different DNS issue.

### Troubleshooting 4/5.7.321 starttls-not-supported

This error usually indicates an issue with the destination mail server. After receiving the message:

1. Check that you entered the destination email address correctly.
2. Alert the destination email administrator that you received this error code so they can determine if the destination server is configured correctly to receive messages using TLS.
3. Retry sending the email and review the Message Trace Details for the message in the Exchange Admin Center portal.

### Troubleshooting 4/5.7.322 certificate-expired

The sending email server must present a valid X.509 certificate that isn't expired. X.509 certificates must be renewed after their expiration, commonly annually. After receiving the message:

1. Alert the destination email administrator that you received this error code and provide the error code string.
2. Allow time for the destination server certificate to be renewed and the TLSA record to be updated to reference the new certificate. Then, retry sending the email and review the Message Trace Details for the message in the Exchange Admin Center portal.

### Troubleshooting 4/5.7.323 tlsa-invalid

This error code relates to a TLSA record misconfiguration and can only be generated after a DNSSEC-authentic TLSA record is returned. Many scenarios during the DANE validation occur after the record is returned that can result in the code being generated. Microsoft is actively working on the scenarios that this error code covers, so that each scenario has a specific code. Currently, one or more of these scenarios could cause the generation of the error code:

1. The destination mail server's certificate doesn't match with what the authentic TLSA record expects.
2. The authentic TLSA record is misconfigured.
3. The destination domain is under attack.
4. Any other DANE failure.

After receiving the message:

1. Alert the destination email administrator that you received this error code and provide them with the error code string.
2. Allow time for the destination email admin to review their DANE configuration and email server certificate validity. Then, retry sending the email and review the Message Trace Details for the message in the Exchange Admin Center portal.

### Troubleshooting 4/5.7.324 dnssec-invalid

Exchange Online generates this error code when the destination domain indicates it's DNSSEC-authentic but Exchange Online can't verify it as DNSSEC-authentic.

After receiving the message:

1. Alert the destination email administrator that you received this error code and provide them with the error code string.
2. Allow time for the destination email admin to review their domain's DNSSEC configuration. Then, retry sending the email and review the Message Trace Details for the message in the Exchange Admin Center portal.

## Troubleshooting receiving emails with SMTP DANE

Currently, admins of receiving domains can use two methods to validate and troubleshoot their DNSSEC and DANE configuration to receive email from Exchange Online by using the following standards:

1. Adopt SMTP TLS-RPT (Transport Layer Security Reporting) introduced in [RFC8460](https://datatracker.ietf.org/doc/html/rfc8460)
2. Use the Remote Connectivity Analyzer tool [Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/o365)

TLS-RPT https://datatracker.ietf.org/doc/html/rfc8460 is a reporting mechanism for senders to provide details to destination domain administrators about DANE and MTA-STS successes and failures with those respective destination domains. To receive TLS-RPT reports, you only need to add a TXT record in your domain's DNS records that includes the email address or URI you want the reports to be sent to. Exchange Online sends TLS-RPT reports in JSON format.

The following table shows an example of a record:

| Type | Domain Name | TTL | Record |
| --- | --- | --- | --- |
| TXT | \_smtp.\_tls.microsoft.com | 3600 | v=TLSRPTv1;rua=https://tlsrpt.azurewebsites.net/report |

The second method is to use the Remote Connectivity Analyzer [Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/tests/o365), which can do the same DNSSEC and DANE checks against your DNS configuration that Exchange Online does when sending email outside the service. This method is the most direct way of troubleshooting errors in your configuration to receive email from Exchange Online by using these standards.

When troubleshooting errors, the following error codes might be generated:

| NDR Code | Description |
| --- | --- |
| 4/5.7.321 | starttls-not-supported: Destination mail server must support TLS to receive mail. |
| 4/5.7.322 | certificate-expired: Destination mail server's certificate has expired. |
| 4/5.7.323 | tlsa-invalid: The domain failed DANE validation. |
| 4/5.7.324 | dnssec-invalid: Destination domain returned invalid DNSSEC records. |

Note

Currently, when a domain signals that it supports DNSSEC but fails DNSSEC checks, Exchange Online doesn't generate the 4/5.7.324 dnssec-invalid error. It generates a generic DNS error:

`4/5.4.312 DNS query failed`

We're actively working to remedy this known limitation. If you receive this error statement, navigate to the Microsoft Remote Connectivity Analyzer and perform the DANE validation test against the domain that generated the 4/5.4.312 error. The results show if it's a DNSSEC issue or a different DNS issue.

### Troubleshooting 4/5.7.321 starttls-not-supported

Note

These steps are for email administrators troubleshooting receiving email from Exchange Online by using SMTP DANE.

This error usually indicates an issue with the destination mail server. The Remote Connectivity Analyzer tests connecting with the mail server. Two scenarios generally generate this code:

1. The destination mail server doesn't support secure communication at all, and plain, non-encrypted communication must be used.
2. The destination server is configured improperly and ignores the STARTTLS command.

After receiving the message:

1. Check the email address.
2. Locate the IP address that's associated with the error statement so you can identify the mail server the statement is associated with.
3. Check your mail server's setting to make sure it's configured to listen for SMTP traffic (commonly ports 25 and 587).
4. Wait a few minutes, then retry the test with the Remote Connectivity Analyzer tool.
5. If it still fails, try removing the TLSA record and run the test with the Remote Connectivity Analyzer tool again.
6. If there are no failures, this message might indicate the mail server you're using to receive mail doesn't support STARTTLS. You might need to upgrade to one that supports STARTTLS to use DANE.

### Troubleshooting 4/5.7.322 certificate-expired

Note

These steps are for email administrators troubleshooting receiving email from Exchange Online by using SMTP DANE.

The sending email server must present a valid X.509 certificate that isn't expired. X.509 certificates must be renewed after their expiration, commonly annually. After receiving the message:

1. Check the IP address that's associated with the error statement, so you can identify the mail server it's associated with. Locate the expired certificate on the email server you identified.
2. Sign in to your certificate provider's website.
3. Select the expired certificate and follow the instructions to renew and pay for the renewal.
4. After your provider verifies the purchase, download a new certificate.
5. Install the renewed certificate into its associated mail server.
6. Update the mail server's associated TLSA record with the new certificate's data.
7. After waiting an appropriate amount of time, retry the test with the Remote Connectivity Analyzer tool.

### Troubleshooting 4/5.7.323 tlsa-invalid

Note

These steps are for email administrators troubleshooting receiving email from Exchange Online by using SMTP DANE.

This error code relates to a TLSA record misconfiguration. The error code can only be generated after a DNSSEC-authentic TLSA record is returned. However, many scenarios during the DANE validation occur after the record is returned that can result in the code being generated. Microsoft is actively working on the scenarios that this error code covers, so that each scenario has a specific code. Currently, one or more of these scenarios can cause the generation of the error code:

1. Authentic TLSA record is misconfigured.
2. The certificate isn't yet time valid or is configured for a future time window.
3. Destination domain is under attack.
4. Any other DANE failure.

After receiving the message:

1. Check the IP address that's associated with the error statement to identify the mail server.
2. Identify the TLSA record that's associated with the mail server.
3. Verify the configuration of the TLSA record to ensure that it signals the sender to perform the preferred DANE checks and that the correct certificate data is included in the TLSA record.
    1. If you need to update the record for discrepancies, wait a few minutes, then rerun the test with the Remote Connectivity Analyzer tool.
4. Locate the certificate on the mail server.
5. Check the time window for which the certificate is valid. If it's set to start validity at a future date, it needs to be renewed for the current date.
    1. Sign in to your certificate provider's website.
    2. Select the expired certificate and follow the instructions to renew and pay for the renewal.
    3. After your provider verifies the purchase, you can download a new certificate.
    4. Install the renewed certificate into its associated mail server.

### Troubleshooting 4/5.7.324 dnssec-invalid

Note

These steps are for email administrators troubleshooting receiving email from Exchange Online by using SMTP DANE.

Exchange Online generates this error code when the destination domain indicates its DNSSEC-authentic but Exchange Online can't verify it as DNSSEC-authentic. This section isn't comprehensive for troubleshooting DNSSEC issues and focuses on scenarios where domains previously passed DNSSEC authentication but don't now.

Note

Exchange Online also generates this error code if it receives a SERVFAIL response from a DNS server on a TLSA query for the destination domain.

After receiving the message:

1. If you're using a DNS provider, such as GoDaddy, alert your DNS provider of the error so they can work on the troubleshooting and configuration change.
2. If you're managing your own DNSSEC infrastructure, many DNSSEC misconfigurations can generate this error message. Check for these common problems if your zone previously passed DNSSEC authentication:
    1. Broken trust chain, when the parent zone holds a set of DS records that point to something that doesn't exist in the child zone. Such pointers by DS records can result in the child zone being marked as bogus by validating resolvers.
        - Resolve by reviewing the child domain's RRSIG key IDs and ensuring that they match with the key IDs in the DS records published in the parent zone.
    2. RRSIG resource record for the domain isn't time valid, it has either expired or its validity period hasn't begun.
        - Resolve by generating new signatures for the domain by using valid timespans.

When you send an outbound email, if the receiving domain has DNSSEC enabled, Exchange Online queries for TLSA records associated with MX entries in the domain. If no TLSA record is published, the response to the TLSA lookup must be NOERROR (no records of requested type for this domain) or NXDOMAIN (there's no such domain). DNSSEC requires this response if no TLSA record is published; otherwise, Exchange Online interprets the lack of response as a SERVFAIL error. As per [RFC 7672](https://tools.ietf.org/html/rfc7672), a SERVFAIL response is untrustworthy; so, the destination domain fails DNSSEC validation. Exchange Online defers this email with the following error:

`450 4.7.324 dnssec-invalid: Destination domain returned invalid DNSSEC records`

### If the email sender reports receipt of the message

If you're using a DNS provider, such as GoDaddy, alert your DNS provider of the error so that they can troubleshoot the DNS response. If you're managing your own DNSSEC infrastructure, the issue could be with the DNS server itself or with the network.

## Frequently Asked Questions

### As an Exchange Online customer, can I opt out of using DNSSEC and DANE?

We strongly believe DNSSEC and DANE significantly increase the security of our service and benefit all of our customers. Over the last year, we worked diligently to reduce the risk and severity of the potential impact this deployment might have for Microsoft 365 customers. We actively monitor and track the deployment to ensure negative impact is minimized as it rolls out. Because of this, tenant-level exceptions or opt-out isn't available. If you experience any issues related to the enablement of DNSSEC and DANE, the different methods for investigating failures noted in this document help you identify the source of the error. In most cases, the issue is with the external destination party and you need to communicate to these business partners that they need to correctly configure DNSSEC and DANE in order to receive email from Exchange Online using these standards.

### How does DNSSEC relate to DANE?

DNSSEC adds a layer of trust into DNS resolution by applying the public key infrastructure to ensure the records returned in response to a DNS query are authentic. DANE ensures that the receiving mail server is the legitimate and expected mail server for the authentic MX record.

### What is the difference between MTA-STS and DANE for SMTP?

DANE and MTA-STS serve the same purpose, but DANE requires DNSSEC for DNS authentication while MTA-STS relies on certificate authorities.

### Why isn't Opportunistic TLS sufficient?

Opportunistic TLS encrypts communication between two endpoints if both agree to support it. However, even if TLS encrypts the transmission, a domain can be spoofed during DNS resolution such that it points to a malicious actor's endpoint instead of the real endpoint for the domain. This spoof is a gap in email security that MTA-STS and SMTP DANE with DNSSEC address.

### Why isn't DNSSEC sufficient?

DNSSEC isn't fully resistant to man-in-the-middle attacks and downgrade (from TLS to clear text) attacks for mail flow scenarios. The addition of MTA-STS and DANE along with DNSSEC provides a comprehensive security method to thwart both MITM and downgrade attacks.