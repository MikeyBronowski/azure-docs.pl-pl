---
title: Włączanie Snapshot Debugger dla aplikacji .NET i .NET Core w Azure Functions | Microsoft Docs
description: Włączanie Snapshot Debugger dla aplikacji .NET i .NET Core w programie Azure Functions
ms.topic: conceptual
author: cweining
ms.author: cweining
ms.date: 12/18/2020
ms.openlocfilehash: d86455eae0834f29099c7d5c96f8326408daf519
ms.sourcegitcommit: b39cf769ce8e2eb7ea74cfdac6759a17a048b331
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2021
ms.locfileid: "98675533"
---
# <a name="enable-snapshot-debugger-for-net-and-net-core-apps-in-azure-functions"></a>Włączanie Snapshot Debugger dla aplikacji .NET i .NET Core w programie Azure Functions

Snapshot Debugger obecnie działa dla aplikacji ASP.NET i ASP.NET Core, które działają w Azure Functions planach usług systemu Windows.

Zalecamy uruchomienie aplikacji w warstwie Podstawowa usługi lub wyższej przy użyciu Snapshot Debugger.

W przypadku większości aplikacji warstwy Bezpłatna i współdzielona nie mają wystarczającej ilości pamięci lub miejsca na dysku do zapisania migawek.

## <a name="prerequisites"></a>Wymagania wstępne

* [Włącz monitorowanie Application Insights w aplikacja funkcji](../../azure-functions/configure-monitoring.md#add-to-an-existing-function-app)

## <a name="enable-snapshot-debugger"></a>Włącz Snapshot Debugger

Jeśli używasz innego typu usługi platformy Azure, poniżej przedstawiono instrukcje dotyczące włączania Snapshot Debugger na innych obsługiwanych platformach:
* [Azure App Service](snapshot-debugger-appservice.md?toc=/azure/azure-monitor/toc.json)
* [usług Azure Cloud Services](snapshot-debugger-vm.md?toc=/azure/azure-monitor/toc.json)
* [Usługi Service Fabric platformy Azure](snapshot-debugger-vm.md?toc=/azure/azure-monitor/toc.json)
* [Azure Virtual Machines i zestawy skalowania maszyn wirtualnych](snapshot-debugger-vm.md?toc=/azure/azure-monitor/toc.json)
* [Lokalne maszyny wirtualne lub fizyczne](snapshot-debugger-vm.md?toc=/azure/azure-monitor/toc.json)

Aby włączyć Snapshot Debugger w aplikacji funkcji, musisz zaktualizować `host.json` plik, dodając Właściwość `snapshotConfiguration` zgodnie z definicją poniżej i ponownie Wdróż funkcję.

```json
{
  "version": "2.0",
  "logging": {
    "applicationInsights": {
      "snapshotConfiguration": {
        "isEnabled": true
      }
    }
  }
}
```

Snapshot Debugger jest wstępnie zainstalowana jako część środowiska uruchomieniowego Azure Functions, która jest domyślnie wyłączona.

Ponieważ Snapshot Debugger są zawarte w środowisku uruchomieniowym Azure Functions, nie jest to konieczne do dodawania dodatkowych pakietów NuGet ani ustawień aplikacji.

Podobnie jak w przypadku prostej aplikacji funkcji (.NET Core), poniżej pokazano, jak będzie wyglądać `.csproj` , `{Your}Function.cs` i `host.json` po włączeniu Snapshot Debugger.

CSPROJ projektu

```xml
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
    <AzureFunctionsVersion>v2</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Microsoft.NET.Sdk.Functions" Version="1.0.31" />
</ItemGroup>
<ItemGroup>
    <None Update="host.json">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="local.settings.json">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    <CopyToPublishDirectory>Never</CopyToPublishDirectory>
    </None>
</ItemGroup>
</Project>
```

Function — Klasa

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;

namespace SnapshotCollectorAzureFunction
{
    public static class ExceptionFunction
    {
        [FunctionName("ExceptionFunction")]
        public static Task<IActionResult> Run(
            [HttpTrigger(AuthorizationLevel.Function, "get", Route = null)] HttpRequest req,
            ILogger log)
        {
            log.LogInformation("C# HTTP trigger function processed a request.");

            throw new NotImplementedException("Dummy");
        }
    }
}
```

Plik hosta

```json
{
  "version": "2.0",
  "logging": {
    "applicationInsights": {
      "samplingExcludedTypes": "Request",
      "samplingSettings": {
        "isEnabled": true
      },
      "snapshotConfiguration": {
        "isEnabled": true
      }
    }
  }
}
```

## <a name="disable-snapshot-debugger"></a>Wyłącz Snapshot Debugger

Aby wyłączyć Snapshot Debugger w aplikacji funkcji, wystarczy zaktualizować `host.json` plik przez ustawienie `false` właściwości `snapshotConfiguration.isEnabled` .

```json
{
  "version": "2.0",
  "logging": {
    "applicationInsights": {
      "snapshotConfiguration": {
        "isEnabled": false
      }
    }
  }
}
```

Zalecamy, aby na wszystkich aplikacjach została włączona Snapshot Debugger, co ułatwi diagnostykę wyjątków aplikacji.

## <a name="next-steps"></a>Następne kroki

- Generuj ruch do aplikacji, która może wyzwolić wyjątek. Następnie odczekaj od 10 do 15 minut na wysłanie migawek do wystąpienia Application Insights.
- [Wyświetl migawki](snapshot-debugger.md?toc=/azure/azure-monitor/toc.json#view-snapshots-in-the-portal) w Azure Portal.
- Dostosuj konfigurację Snapshot Debugger w oparciu o przypadek użycia w aplikacji funkcji. Aby uzyskać więcej informacji, zobacz [Konfiguracja migawek w host.js](../../azure-functions/functions-host-json.md#applicationinsightssnapshotconfiguration).
- Aby uzyskać pomoc dotyczącą rozwiązywania problemów Snapshot Debugger, zobacz [Snapshot Debugger Rozwiązywanie problemów](snapshot-debugger-troubleshoot.md?toc=/azure/azure-monitor/toc.json).