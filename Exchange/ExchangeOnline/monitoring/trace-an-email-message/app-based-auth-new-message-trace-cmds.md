---
layout: Conceptual
title: How to use app-based authentication for the new Message Trace cmdlets | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/exchange/monitoring/trace-an-email-message/app-based-auth-new-message-trace-cmds
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
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid: 
ms.custom: 
description: Learn how to use app-based authentication for the new Message Trace cmdlets.
ms.date: 2025-06-16T00:00:00.0000000Z
locale: en-us
document_id: 7861c55d-16e5-59b5-e471-c737063e18c0
document_version_independent_id: cc3db681-396c-6a81-88e2-8f997b302921
original_content_git_url: https://github.com/MicrosoftDocs/OfficeDocs-Exchange-pr/blob/live/Exchange/ExchangeOnline/monitoring/trace-an-email-message/app-based-auth-new-message-trace-cmds.md
site_name: Docs
depot_name: office.OfficeDocs-Exchange
page_type: conceptual
toc_rel: ../../onlinetoc/toc.json
pdf_url_template: https://learn.microsoft.com/pdfstore/en-us/office.OfficeDocs-Exchange/{branchName}{pdfName}
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitoring/trace-an-email-message/app-based-auth-new-message-trace-cmds
moniker_range_name: 
monikers: []
item_type: Content
source_path: Exchange/ExchangeOnline/monitoring/trace-an-email-message/app-based-auth-new-message-trace-cmds.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 407e42a7-ba0f-13fd-fa2f-44686f310030
---

# How to use app-based authentication for the new Message Trace cmdlets | Microsoft Learn

This document provides guidance on using C# code and app-based authentication to call `Get-MessageTraceV2`/`Get-MessageTraceDetailV2` via the Exchange Online PowerShell module.

## Prerequisites:

### Install the Exchange Online PowerShell module

See [About the Exchange Online PowerShell V3 module](/en-us/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps&amp;preserve-view=true).

Install the latest preview or public version to get the latest improvements.

### Configure the required authentication

Follow the standard documentation to connect to Exchange Online PowerShell.

See [App-only authentication in Exchange Online PowerShell and Security & Compliance PowerShell](/en-us/powershell/exchange/app-only-auth-powershell-v2?view=exchange-ps&amp;preserve-view=true).

It's advisable to follow the recommended sections at each step in the documentation provided.

### Write the C# code to call `Get-MessageTraceV2`/`Get-MessageTraceDetailV2`

Refer to this common documentation for calling cmdlets in Exchange Online PowerShell: [Use C# to connect to Exchange Online PowerShell | Microsoft Learn](/en-us/powershell/exchange/connect-to-exo-powershell-c-sharp?view=exchange-ps&amp;preserve-view=true).

Below is a sample specifically for `Get-MessageTraceV2`. You can adjust it to meet your needs. The example code (csproj is included for package version reference) demonstrates the process of retrieving message traces from the past two days iteratively. Feel free to update the code according to your requirements.

```csharp
namespace CallEXOCmdletSample
{
    using System;
    using System.Collections.Generic;
    using System.Collections.ObjectModel;
    using System.Globalization;
    using System.Linq;
    using System.Management.Automation;
    using System.Management.Automation.Runspaces;
    using System.Security;
    using System.Threading;

    public class ExchangeOnlineHelper
    {
        private const string NextQueryHint = "There are more results";

        public static void SingleConnectionToExchangeOnline()
        {
            // Import the ExchangeOnlineManagement module.
            // Set the Execution Policy of the runspace.
            InitialSessionState iss = InitialSessionState.CreateDefault();
            iss.ImportPSModule(new string[] { "ExchangeOnlineManagement" });
            iss.ExecutionPolicy = Microsoft.PowerShell.ExecutionPolicy.RemoteSigned;
            iss.ThrowOnRunspaceOpenError = true;

            using (Runspace runspace = RunspaceFactory.CreateRunspace(iss))
            {
                runspace.Open();
                using (PowerShell ps = PowerShell.Create())
                {
                    ps.Runspace = runspace;

                    ps.AddCommand("Connect-ExchangeOnline");
                    ps.AddParameters(new Dictionary<string, object>
                    {
                        ["Organization"] = "<YourOrgDomain>", // Replace with your organization name
                        ["CertificateThumbprint"] = "<YourCertificateThumbprint>", // Replace with your certificate thumbprint
                        ["AppID"] = "<YourAppID>" // Replace with your App ID
                    });

                    Collection<PSObject> connectionResult = ps.Invoke();

                    // Clear the connection commands before running cmdlets.
                    ps.Commands.Clear();

                    // Create a new command to execute Get-MessageTraceV2.
                    // List parameters that you want to use with Get-MessageTraceV2.
                    // More parameter are recommended to improve performance.
                    DateTime startDate = DateTime.UtcNow.AddDays(-2);
                    DateTime endDate = DateTime.UtcNow;
                    int resultSize = 100;

                    // Parameters that remain constant throughout all requests
                    var commonParameters = new Dictionary<string, object>
                    {
                        ["StartDate"] = startDate.ToString("O", CultureInfo.InvariantCulture),
                        ["ResultSize"] = resultSize
                    };

                    // Variable to support subsequent queries.
                    DateTime? lastMessageDate = null;
                    string lastRecipientAddress = null;

                    do
                    {
                        // Clear previous state
                        ps.Commands.Clear();
                        ps.Streams.Warning.Clear(); // Clear the warning stream before invoking the command.
                        ps.Streams.Error.Clear(); // Clear the error stream before invoking the command.

                        // Add command and common parameters
                        ps.AddCommand("Get-MessageTraceV2");
                        foreach (var param in commonParameters)
                        {
                            ps.AddParameter(param.Key, param.Value);
                        }

                        // Add subsequent query parameters if we're not on the first query
                        if (lastMessageDate.HasValue && !string.IsNullOrEmpty(lastRecipientAddress))
                        {
                            ps.AddParameter("EndDate", lastMessageDate.Value.ToString("O", CultureInfo.InvariantCulture));
                            ps.AddParameter("StartingRecipientAddress", lastRecipientAddress);
                        }
                        else
                        {
                            ps.AddParameter("EndDate", endDate.ToString("O", CultureInfo.InvariantCulture));
                        }

                        Collection<PSObject> results = ps.Invoke();

                        // Check if there were any errors.
                        if (!ps.HadErrors)
                        {
                            // Write the results to console.
                            foreach (PSObject result in results)
                            {
                                Console.WriteLine($"MessageTraceId: {result.Properties["MessageTraceId"]?.Value}");
                                Console.WriteLine($"MessageId: {result.Properties["MessageId"]?.Value}");
                                Console.WriteLine($"Received: {result.Properties["Received"]?.Value}");
                                Console.WriteLine($"SenderAddress: {result.Properties["SenderAddress"]?.Value}");
                                Console.WriteLine($"RecipientAddress: {result.Properties["RecipientAddress"]?.Value}");
                                Console.WriteLine($"FromIP: {result.Properties["FromIP"]?.Value}");
                                Console.WriteLine($"ToIP: {result.Properties["ToIP"]?.Value}");
                                Console.WriteLine($"Subject: {result.Properties["Subject"]?.Value}");
                                Console.WriteLine($"Status: {result.Properties["Status"]?.Value}");
                                Console.WriteLine($"Size: {result.Properties["Size"]?.Value}");
                            }

                            // Update subsequent query parameters based on the last result.
                            if (results.Count == resultSize)
                            {
                                var lastResult = results.Last();
                                lastMessageDate = lastResult.Properties["Received"]?.Value as DateTime?;
                                lastRecipientAddress = lastResult.Properties["RecipientAddress"]?.Value?.ToString();
                            }
                        }
                        else
                        {
                            // Write the errors to console by accessing the error stream of the Powershell object.
                            foreach (ErrorRecord error in ps.Streams.Error)
                            {
                                Console.WriteLine(error.ToString());
                            }
                        }

                        // Sleep 10 seconds before sending the next query to avoid throttling.
                        Thread.Sleep(TimeSpan.FromSeconds(10));
                    }
                    while (ps.Streams.Warning.Count > 0 && ps.Streams.Warning[0].ToString().Contains(NextQueryHint, StringComparison.OrdinalIgnoreCase));
                }
            }
        }
    }

    class Program
    {
        static void Main()
        {
            ExchangeOnlineHelper.SingleConnectionToExchangeOnline();
        }
    }
}
```

The following is an example code for csproj file.

```csproj
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net9.0</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.PowerShell.SDK" Version="7.5.1" />
    <PackageReference Include="Microsoft.Management.Infrastructure" Version="3.0.0" />
    <PackageReference Include="System.Management.Automation" Version="7.5.1" />
    <PackageReference Include="System.Runtime" Version="4.3.1" />
  </ItemGroup>
</Project>
```