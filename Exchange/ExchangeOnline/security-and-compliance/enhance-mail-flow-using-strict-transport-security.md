---
layout: Conceptual
title: Enhance mail flow with MTA-STS | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/security-and-compliance/enhance-mail-flow-using-strict-transport-security
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
description: Learn how Exchange Online uses MTA-STS to enforce TLS, validate receiving server certificates, and protect inbound and outbound mail flow against man-in-the-middle attacks.
ms.topic: article
author: Cloud-Writer
ms.author: meerak
ms.assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms.reviewer: 
f1.keywords:
- NOCSH
ms.collection:
- exchange-online
audience: ITPro
ms.service: exchange-online
ms.date: 2026-07-21T00:00:00.0000000Z
locale: en-us
document_id: ccc7d9a4-7376-5915-776e-2ae80f394158
document_version_independent_id: 83d0f294-c32f-92e6-6e27-040432f72b24
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/security-and-compliance/enhance-mail-flow-using-strict-transport-security.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-and-compliance/enhance-mail-flow-using-strict-transport-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/security-and-compliance/enhance-mail-flow-using-strict-transport-security.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 4a736125-3524-d736-cc15-3a1b2dcf777b
---

# Enhance mail flow with MTA-STS | Microsoft Learn

Support for the [SMTP MTA Strict Transport Security](https://datatracker.ietf.org/doc/html/rfc8461) (MTA-STS) standard is added to Exchange Online. The standard was developed to ensure that TLS is always used for connections between email servers. It also provides a way for sending servers to validate that the receiving server has a trusted certificate. If either TLS isn't offered or the certificate isn't valid, the sender refuses to deliver messages. These TLS and certificate-validity checks improve the overall security of SMTP and protect against man-in-the-middle attacks.

MTA-STS can be broken down into two scenarios: Inbound and Outbound Protection. Inbound protection covers the protection of domains hosted in Exchange Online with MTA-STS. Outbound protection covers the MTA-STS validations performed by Exchange Online when sending emails to MTA-STS-protected domains.

## How MTA-STS protects outbound mail

All messages sent outbound from Exchange Online to MTA-STS-protected recipients are validated with the TLS enforcement and certificate-validity checks defined by the MTA-STS standard. There's nothing administrators need to do to apply it. Our outbound implementation respects the wishes of the recipient domain owners via their MTA-STS policy. MTA-STS forms part of the security infrastructure of Exchange Online, and it's therefore always turned on (like other core SMTP features).

Note

For Outbound connectors using smart hosts, we're performing the MTA-STS validation against the smart host domain, not the final destination domain for the recipient.

Outbound MTA-STS may prevent emails from being delivered depending on the results of the MTA-STS validation against the destination domain. If the domain isn't secure and the MTA-STS policy is set to **Enforce**, an NDR may be returned to the sender with one of the following error codes:

| Error code | Description | Possible cause | Additional information |
| --- | --- | --- | --- |
| 5.4.8 | MX hosts of '{domain}' failed MTA-STS validation | The destination MX host wasn't the host expected per the domain's STS policy. | This error usually indicates an issue with the destination domain's MTA-STS policy not containing the MX host. For more information about MTA-STS, see https://datatracker.ietf.org/doc/html/rfc8461. |
| 5.7.5 | Remote certificate failed MTA-STS validation. Reason: {validityStatus} | The destination mail server's certificate must chain to a trusted root Certificate Authority, and the Common Name or Subject Alternative Name must contain an entry for the host name in the STS policy. | This error usually indicates an issue with the destination mail server's certificate. For more information about MTA-STS, see https://datatracker.ietf.org/doc/html/rfc8461. |

## How MTA-STS protects inbound mail

Domain owners can take action to protect emails sent to their domains with MTA-STS, if their MX record points to Exchange Online. If your MX record points to an intermediary third-party service, you'll need to verify whether MTA-STS requirements are met by that service provider, and then follow their instructions.

Once MTA-STS is set up for your domain, any messages sent from senders who support MTA-STS will perform the validations laid out by the standard to ensure a secure connection. If you're receiving an email from a sender who doesn't support MTA-STS, the email will still be delivered without the extra protection. Likewise, there's no disruption to messages if you aren't using MTA-STS yet but the sender supports it. The only scenario where messages aren't delivered is when both sides are using MTA-STS and MTA-STS validation fails.

## Adopt MTA-STS for your domain

MTA-STS allows a domain to declare support for TLS and communicate the MX record and destination certificate to expect. It also indicates what a sending server must do if there's a problem. This communication is done through a combination of a DNS TXT record and a policy file that's published as an HTTPS webpage. The HTTPS-protected policy introduces another security protection that attackers must overcome.

A domain's MTA-STS TXT record indicates MTA-STS support to a sender, after which the domain's HTTPS-based MTA-STS policy is retrieved by the sender. The TXT record should contain v=STSv1; until STSv2 is supported, and the id for the policy. The id MUST be unique for the domain owner and policy, as a change in the id signals to senders that they need to re-fetch the policy. The id doesn't need to be globally unique, don't worry about other domain owner's policy id's. After any MTA-STS policy updates, you need to update the id, or senders will keep using cached policies for your domain until the max\_age of the cached policy expires.

A repeatable pattern for setting a unique id is to use UTC time as such:`id=<yyyymmddhh0000>Z;`

The following TXT record is an example that declares support for MTA-STS, the id was set at 8 am January 1, 2022 UTC time:

`_mta-sts.contoso.com. 3600 IN TXT v=STSv1; id=20220101080000Z;`

A domain's MTA-STS policy needs to be located at a predefined URL that's hosted by the domain's web infrastructure. The URL syntax is `https://mta-sts.<domain name>/.well-known/mta-sts.txt`. For example, Microsoft.com's policy is found at: https://mta-sts.microsoft.com/.well-known/mta-sts.txt.

The following example shows the contents of an MTA-STS policy file (`mta-sts.txt`). The `version` field declares the protocol version, `mode` specifies whether the policy is enforced or in testing, `mx` identifies the authorized mail server, and `max_age` defines how long (in seconds) senders should cache the policy:

```console
version: STSv1
mode: enforce
mx: *.mail.protection.outlook.com
max_age: 604800
```

Any customer whose MX records point directly to Exchange Online can specify in their own policy the same `version`, `mode`, `mx` (`*.mail.protection.outlook.com`), and `max_age` values that are shown in https://mta-sts.microsoft.com/.well-known/mta-sts.txt. The unique required information in the policy is the MX record that points to Exchange Online (`*`.mail.protection.outlook.com) and the same certificate is shared by all Exchange Online customers. Exchange Online only allows one organization to receive emails for a given domain so that using a wildcard doesn't weaken security; however, that may not be the case for other email services. It's possible to publish your policy in *testing* mode to ensure it's valid before changing it to *enforce* mode. There are third-party validation tools out there that can check your configuration.

MTA-STS policy files aren't something that Exchange Online can host on behalf of customers; so, customers must configure their domain's STS policy using the services they prefer. Azure services can be easily used for policy hosting. For a step-by-step configuration guide, see Configuring Inbound MTA-STS with Azure Services. The policy needs to be protected by HTTPS with a certificate for the subdomain `mta-sts.<domain name>`.

Once the DNS TXT record is created and the policy file is available at the required HTTPS URL, the domain will be protected by MTA-STS. Details about MTA-STS are available in [RFC 8461](https://datatracker.ietf.org/doc/html/rfc8461).

### Configuring Inbound MTA-STS with Azure Services

Note

These configuration flows were developed to help Microsoft Exchange Online customers host their MTA-STS policy using Azure resources. This configuration flow assumes that you're an Exchange Online customer who is aware of how MTA-STS works and of its requirements. For more information about the protocol beyond this topic, see [RFC8461](https://www.rfc-editor.org/rfc/rfc8461.html).

There are two Azure resources that can be used to host the MTA-STS policy: [Azure Static Web App](https://azure.microsoft.com/services/app-service/static/) and [Azure Functions](/en-us/azure/azure-functions/functions-overview). Although this article describes how to deploy the policy using both Azure Static Web App and Azure Functions, the recommended method is [Azure Static Web App](https://azure.microsoft.com/services/app-service/static/) as it's designed for hosting static pages such as the STS policy, and Azure simplifies the configuration by providing a TLS certificate for the MTA-STS webpage out of the box, without requiring more configuration. If you aren't able to use [Azure Static Web App](https://azure.microsoft.com/services/app-service/static/), you can also host your policy as serverless code using [Azure Functions](/en-us/azure/azure-functions/functions-overview). This approach isn't the preferred method because Azure Functions is a feature designed for other scenarios and it doesn't issue a TLS certificate automatically, unlike Azure Static Web Apps. So using [Azure Functions](/en-us/azure/azure-functions/functions-overview) for MTA-STS requires that you issue your own "mta-sts.[your domain]" certificate and bind it to the function.

Regardless of which approach you've taken, we encourage you to validate whether your policy has been properly configured and whether the response time is acceptable – timeout per RFC guidance is 60 seconds.

These configuration flows are intended to provide only technical information about Azure features that can be used to host the MTA-STS policy and doesn't provide any information about Azure features' charging or costs. If you want to know Azure features' costs, use the Azure [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).

#### Option 1 (RECOMMENDED): Azure Static Web App

Perform the following steps to host your MTA-STS policy by using Azure Static Web App with Azure DevOps for deployment.

1. Create an Azure DevOps organization or use an organization that already exists. In this Azure Static Web App procedure, an organization called "ContosoCorporation" is used to host the MTA-STS policy.

    [![The screenshot that shows the projects tab.](../exchangeonline/media/projects-tab.png)](../exchangeonline/media/projects-tab.png#lightbox)
2. In **Repos &gt; Files**, clone your repository in any IDE that you prefer. In this Azure DevOps walkthrough, the repo is cloned in Visual Studio.

    [![The screenshot that shows an example of cloning to visual studio code.](../exchangeonline/media/clone-to-vs-code.png)](../exchangeonline/media/clone-to-vs-code.png#lightbox)
3. Once the repo is cloned, create the folder path `home\.well-known\`. Then, create the following files:

    - File 1: home.well-known\mta-sts.txt

        Note

        This configuration allows only Exchange Online to receive messages on behalf of your domain. If you're using multiple email providers, you need to reference MX hosts for those other providers' domains as well. Wildcards or '\*' must not be used as the MX prefix in all MTA-STS scenarios; the settings below are specific to Exchange Online only and must NOT be used as general guidance for configuring MTA-STS.

        1. Input the following text into the `mta-sts.txt` file:

            ```console
            version: STSv1
            mode: testing
            mx: *.mail.protection.outlook.com
            max_age: 604800
            ```

            Note

            It's recommended that the policy mode be initially set as **testing**. Then, at the end of the configuration and after validating that the policy is working as expected, update the `mta-sts.txt` file such that the mode is **enforce**.

            The file must only contain the content as shown in the following screenshot:

        [![The screenshot that displays the contents of File1.](../exchangeonline/media/contents-of-file1.png)](../exchangeonline/media/contents-of-file1.png#lightbox)
    - File 2: home\index.html

        1. Create an `index.html` file and input the following code into it:

            ```html
            <!DOCTYPE html>
            <html lang="en">
            
            <head>
            <meta charset="UTF-8">
            <title>MTA-STS</title>
            </head>
            
            <body>
            <h1>MTA-STS Static Website index</h1>
            </body>
            
            </html>
            ```

            The file must only contain the content as shown in the following screenshot:

        [![The screenshot that displays the contents of File2.](../exchangeonline/media/contents-of-file2.png)](../exchangeonline/media/contents-of-file2.png#lightbox)

        Once the folder path and files are created, don't forget to commit the changes and push them into your main branch.
4. Create a new Azure Static Web App with the following configuration:

    - **Name**: MTA-STS-StaticWebApp
    - **Plan type**: Standard
    - **Deployment Details**: Azure DevOps
    - **Organization**: ContosoCorporation
    - **Project**: MTA-STS\_Project
    - **Repository**: MTA-STS\_Project
    - **Branch**: master
    - **Build Presets**: Angular
    - **App Location**: /home

    [![The screenshot that shows a newly created Azure Static Web App with its information.](../exchangeonline/media/new-app-with-details.png)](../exchangeonline/media/new-app-with-details.png#lightbox)
5. Once the Static Web App creation is done and the resource is provisioned, go to **Overview &gt; Manage deployment token**; then copy the token, because you will paste it as a pipeline variable when creating the deployment pipeline.
6. Go to **Pipelines &gt; Create Pipeline &gt; Azure Repos Git &gt; MTA-STS\_Project**, and perform the following subtasks:

    1. Go to **Variables &gt; New Variable** and type the following:

        1. **Name**: token
        2. **Value**: (paste the token that you previously copied, in Step 5)
    2. Once the variable is saved, return to **Review your pipeline YAML** and paste the following yml, save and run it:

        ```yaml
        trigger:
        - main
        
        pool:
        vmImage: ubuntu-latest
        
        steps:
        - checkout: self
        submodules: true
        - task: AzureStaticWebApp@0
        inputs:
         app_location: '/home'
         azure_static_web_apps_api_token: $(token)
        ```

        In Azure DevOps, during deployment, if you experience the error **No hosted parallelism has been purchased or granted**, either request through this [free parallelism grant request form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR63mUWPlq7NEsFZhkyH8jChUMlM3QzdDMFZOMkVBWU5BWFM3SDI2QlRBSC4u) or implement a configuration through **Organization Settings &gt; Parallel jobs &gt; Microsoft Hosted &gt; Change &gt; Paid Parallel jobs** such that "Paid parallel jobs" are allowed.
7. Once the job finishes successfully, you can validate the deployment through the Azure portal by going to **Azure Static Web App &gt; Environment &gt; Browser**. You must see the `index.html` file's content.
8. Add your vanity domain in **Azure Static Web App &gt; Custom domains &gt; Add**. You'll be required to create a **CNAME** record through your DNS provider (for example, GoDaddy) to validate whether the zone belongs to you. Once the validation is finished, Azure will issue a certificate and bind it to your Static Web App automatically.
9. Validate whether your MTA-STS policy is published through: https://mta-sts.[your domain]/.well-known/mta-sts.txt.
10. Create the MTA-STS TXT DNS record through your DNS provider. The format is:

    ```console
    Hostname: _mta-sts.<domain name>
    TTL: 3600 (recommended)
    Type: TXT
    Text: v=STSv1; id=<ID unique for your domain's STS policy>Z;
    ```

    Note

    An example MTA-STS TXT record: `_mta-sts.contoso.com. 3600 IN TXT v=STSv1; id=20220101080000Z;`
11. Once the TXT record is available in DNS, validate your MTA-STS configuration. Once the configuration has been successfully validated, update the `mta-sts.txt` file so that the policy mode is **enforce**; then update your policy ID in the TXT record.

#### Option 2: Azure Function

Perform the following steps to host your MTA-STS policy as serverless code by using Azure Functions. This approach requires you to issue your own TLS certificate for the `mta-sts` subdomain.

1. Create a new Azure Function App with the following configuration:

    - **Function App name**: [As your choice]
    - **Publish**: Code
    - **Runtime stack**: .NET
    - **Version**: 6
    - **Operating System**: Windows
    - **Plan Type**: [As your choice]

    [![The screenshot that shows the configurations of a new Azure Function app.](../exchangeonline/media/new-azure-function-app.png)](../exchangeonline/media/new-azure-function-app.png#lightbox)
2. Add your custom domain to the Function App. You'll be required to create a **CNAME** record to validate whether the domain belongs to you.

    [![The screenshot that shows the custom domain to be added to the Function App.](../exchangeonline/media/custom-domain-to-add.png)](../exchangeonline/media/custom-domain-to-add.png#lightbox)
3. Bind your "mta-sts.[your domain]" to the Function App.

    [![The screenshot that shows the process of binding the domain to the Function App.](../exchangeonline/media/binding-to-function-app.png)](../exchangeonline/media/binding-to-function-app.png#lightbox)
4. In **App File**, add the following extension to the host.json of your Function App to eliminate the routePrefix. This addition is necessary to remove the /api from the function URL.

    ```json
    "extensions": {
      "http": {
        "routePrefix": ""
      }
    }
    ```

    [![The screenshot that shows the extension being added to the app file.](../exchangeonline/media/extension-added-to-app-file.png)](../exchangeonline/media/extension-added-to-app-file.png#lightbox)
5. In your Function App, go to **Functions &gt; Create** and configure the following parameters:

    Note

    Although this example describes the function development through the portal, you're free to use VS Code, or any other tool that you prefer.

    - **Development environment**: [As your choice; this example will use "Develop in Portal"]
    - **Select a template**: HTTP trigger
    - **New Function**: [As your choice]
    - **Authorization level**: Anonymous

    [![The screenshot that shows the Create function page.](../exchangeonline/media/create-function-screen.png)](../exchangeonline/media/create-function-screen.png#lightbox)
6. Once the function is created, open **Code + Test** and develop in C# a simple async HTTP response that will be your MTA-STS policy. The following example indicates that Exchange Online is expected to receive emails:

    Note

    It's recommended that the policy mode be initially set as **testing**. Then, at the end of the configuration and after validating that the policy is working as expected, update the `mta-sts.txt` file such that the mode is **enforce**.

    [![The screenshot that shows the mta-sts policy that's developed.](../exchangeonline/media/mta-sts-policy.png)](../exchangeonline/media/mta-sts-policy.png#lightbox)
7. In **Integration &gt; HTTP (req)**, edit the trigger to the following values:

    - **Route Template**: .well-known/mta-sts.txt
    - **Selected HTTP methods**: GET

    [![The screenshot that shows the Edit trigger page.](../exchangeonline/media/edit-trigger-screen.png)](../exchangeonline/media/edit-trigger-screen.png#lightbox)
8. Validate that your MTA-STS policy is published through: https://mta-sts.[your domain]/.well-known/mta-sts.txt.
9. Create the MTA-STS TXT DNS record through your DNS provider in the following format:

    ```console
    Hostname: _mta-sts.<domain name>
    TTL: 3600 (recommended)
    Type: TXT
    Text: v=STSv1; id=<ID unique for your domain's STS policy>Z;
    ```

    Note

    An example MTA-STS TXT record: `_mta-sts.contoso.com. 3600 IN TXT v=STSv1; id=20220101080000Z;`
10. Once the TXT record is available in DNS, validate your MTA-STS configuration. Once the configuration has been successfully validated, update the `mta-sts.txt` file such that the policy mode is **enforce**; then update your policy ID in the TXT record.

### Mitigating Issues with Inbound MTA-STS by Switching to "testing" Mode

Switching the MTA-STS policy mode to **testing** allows you to keep your MTA-STS infrastructure intact while signaling to senders that enforcement should be paused. It's useful during incidents where strict enforcement may cause delivery failures.

#### Step 1: Update Your Policy File

Change the policy mode value to **testing**.

Setting the policy mode to `testing` tells senders to fetch the policy but not enforce it, while still sending TLS reports.

#### Step 2: Upload the Updated Policy File

Upload the updated file to your domain's HTTPS server at:

`https://mta-sts.<your-domain>/.well-known/mta-sts.txt`

#### Step 3: Update the DNS TXT Record

Update the `_mta-sts.<your-domain> DNS TXT` record by changing the id value to a new unique string (e.g., UTC timestamp).

A repeatable pattern for setting a unique id is to use the current UTC time of a policy update, as such: `id=<yyyymmddhh0000>Z;`

The following TXT record is an example of an updated MTA-STS txt record, the update occurring at 8 am January 1, 2022 UTC time:

`_mta-sts.contoso.com. 3600 IN TXT v=STSv1; id=20220101080000Z;`

#### Step 4: Debug and Validate

After making the changes:

- Verify:

    - The policy file is reachable and has correctly formatted fields with accurate MX value(s) for your domain.
    - The DNS TXT record is updated and visible.
    - The policy's HTTPS certificate is valid.
- Check TLS-RPT reports (if configured) for signs of delivery issues or misconfigurations.