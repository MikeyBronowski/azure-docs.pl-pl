---
title: 'Samouczek: udostępnianie kotwic z Azure Cosmos DB'
description: W tym samouczku dowiesz się, jak udostępnić identyfikatory kotwic usługi Azure przestrzenny na urządzeniach z systemem Android/iOS w środowisku Unity przy użyciu usługi zaplecza i Azure Cosmos DB.
author: msftradford
manager: MehranAzimi-msft
services: azure-spatial-anchors
ms.author: parkerra
ms.date: 11/20/2020
ms.topic: tutorial
ms.service: azure-spatial-anchors
ms.openlocfilehash: ff888cd98cc79f3e2d508b01f092102eaa038c86
ms.sourcegitcommit: b8eba4e733ace4eb6d33cc2c59456f550218b234
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/23/2020
ms.locfileid: "95494764"
---
# <a name="tutorial-sharing-azure-spatial-anchors-across-sessions-and-devices-with-an-azure-cosmos-db-back-end"></a>Samouczek: udostępnianie kotwic przestrzennych platformy Azure między sesjami i urządzeniami przy użyciu zaplecza Azure Cosmos DB

Ten samouczek to kontynuacja [udostępniania zakotwiczenia przestrzennego platformy Azure między sesjami i urządzeniami.](../../../articles/spatial-anchors/tutorials/tutorial-share-anchors-across-devices.md) Przeprowadzimy Cię przez proces dodawania kilku możliwości, aby Azure Cosmos DB działać jako magazyn zaplecza, jednocześnie udostępniając kotwice przestrzenne platformy Azure między sesjami i urządzeniami.

![Obraz przedstawiający trwałość obiektu GIF](./media/persistence.gif)

Warto zauważyć, że mimo że będziesz używać aparatu Unity i Azure Cosmos DB w tym samouczku, wystarczy udostępnić przykład sposobu udostępniania identyfikatorów kotwic przestrzennych między urządzeniami. Do osiągniecia tego celu można użyć innych języków i technologii zaplecza.

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

Dodaj bazę danych usługi Azure Cosmos do utworzonej wcześniej grupy zasobów.

[!INCLUDE [cosmos-db-create-dbaccount-table](../../../includes/cosmos-db-create-dbaccount-table.md)]

Skopiuj `Connection String` plik, ponieważ będzie on potrzebny.

## <a name="make-minor-changes-to-the-sharingservice-files"></a>Wprowadzanie drobnych zmian w plikach SharingService

W **Eksplorator rozwiązań** Otwórz program `SharingService\Startup.cs` .

Znajdź `#define INMEMORY_DEMO` w górnej części pliku i komentarz, który znajduje się w wierszu. Zapisz plik.

W **Eksplorator rozwiązań** Otwórz program `SharingService\appsettings.json` .

Znajdź `StorageConnectionString` Właściwość i ustaw wartość tak, aby była taka sama jak `Connection String` wartość skopiowana w [kroku Tworzenie konta bazy danych](#create-a-database-account). Zapisz plik.

Możesz ponownie opublikować usługę udostępniania i uruchomić przykładową aplikację.

## <a name="next-steps"></a>Następne kroki

W tym samouczku użyto usługi Azure Cosmos DB do udostępnienia identyfikatorów kotwic między urządzeniami. Aby dowiedzieć się więcej na temat korzystania z kotwic przestrzennych platformy Azure w nowej aplikacji HoloLens Unity, przejdź do następnego samouczka.

> [!div class="nextstepaction"]
> [Uruchamianie nowej aplikacji Unity HoloLens](./tutorial-new-unity-hololens-app.md)
