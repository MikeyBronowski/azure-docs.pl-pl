---
title: Porównanie przykładów migracji Media Services V2 i V3
description: Zestaw przykładów ułatwiających porównanie różnic kodu między Azure Media Services V2 i v3.
services: media-services
author: IngridAtMicrosoft
manager: femila
ms.service: media-services
ms.topic: conceptual
ms.workload: media
ms.date: 1/14/2021
ms.author: inhenkel
ms.openlocfilehash: 640b9b40295ae9b9aea865f7b6159da6ff4a3251
ms.sourcegitcommit: 100390fefd8f1c48173c51b71650c8ca1b26f711
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/27/2021
ms.locfileid: "98898311"
---
# <a name="media-services-migration-code-sample-comparison"></a>Porównanie przykładów kodu migracji Media Services

![logo przewodnika migracji](./media/migration-guide/azure-media-services-logo-migration-guide.svg)

<hr color="#5ea0ef" size="10">

Możesz użyć niektórych przykładów kodu, aby porównać sposób wykonywania czynności między zestawami SDK.

## <a name="samples-for-comparison"></a>Przykłady do porównania

Poniższa tabela zawiera listę przykładów do porównania między wersjami 2 i V3 dla typowych scenariuszy.

|Scenariusz|Interfejs API v2|Interfejs API v3|
|---|---|---|
|Tworzenie elementu zawartości i przekazywanie pliku |[przykład v2 .NET](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L113)|[przykład .NET w wersji 3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L169)|
|Przesyłanie zadania|[przykład v2 .NET](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L146)|[przykład .NET w wersji 3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L298)<br/><br/>Pokazuje, jak najpierw utworzyć transformację, a następnie przesłać zadanie.|
|Publikowanie elementu zawartości przy użyciu szyfrowania AES |1. Utwórz `ContentKeyAuthorizationPolicyOption`<br/>2. Utwórz `ContentKeyAuthorizationPolicy`<br/>3. Utwórz `AssetDeliveryPolicy`<br/>4. Utwórz `Asset` i przekaż zawartość albo Prześlij `Job` i Użyj `OutputAsset`<br/>5. Skojarz `AssetDeliveryPolicy` z `Asset`<br/>6. Utwórz `ContentKey`<br/>7. Dołącz `ContentKey` do `Asset`<br/>8. Utwórz `AccessPolicy`<br/>9. Utwórz `Locator`<br/><br/>[przykład v2 .NET](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L64)|1. Utwórz `ContentKeyPolicy`<br/>2. Utwórz `Asset`<br/>3. Przekaż zawartość lub Użyj `Asset` jako `JobOutput`<br/>4. Utwórz `StreamingLocator`<br/><br/>[przykład .NET w wersji 3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/EncryptWithAES/Program.cs#L105)|
|Pobierz szczegóły zadania i Zarządzaj zadaniami |[Zarządzanie zadaniami za pomocą wersji 2](../previous/media-services-dotnet-manage-entities.md#get-a-job-reference) |[Zarządzanie zadaniami za pomocą wersji 3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L546)|

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [migration guide next steps](./includes/migration-guide-next-steps.md)]
