---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 01/31/2021
ms.author: glenga
ms.openlocfilehash: 9a5c143927f549124cb6e69a4c8eb4829709a9e9
ms.sourcegitcommit: 740698a63c485390ebdd5e58bc41929ec0e4ed2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/03/2021
ms.locfileid: "99493497"
---
+ [Grupa zasobów](../articles/azure-resource-manager/management/overview.md), która jest kontenerem logicznym dla powiązanych zasobów.
+ Standardowe [konto usługi Azure Storage](../articles/storage/common/storage-account-create.md), które zachowuje stan i inne informacje o projektach.
+ Plan zużycia, który definiuje podstawowego hosta dla aplikacji funkcji bezserwerowej. 
+ Aplikacja funkcji, która zapewnia środowisko do wykonywania kodu funkcji. Aplikacja funkcji umożliwia grupowanie funkcji jako jednostki logicznej, co ułatwia zarządzanie, wdrażanie i udostępnianie zasobów w ramach tego samego planu hostingu.
+ Wystąpienie Application Insights połączone z aplikacją funkcji, która śledzi użycie funkcji bezserwerowej.