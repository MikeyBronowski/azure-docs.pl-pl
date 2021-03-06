---
title: Samouczek dotyczący nawiązywania połączenia z Azure Stack Edge mini R in Azure Portal
description: Dowiedz się, jak nawiązać połączenie z urządzeniem Azure Stack Edge mini R przy użyciu lokalnego interfejsu użytkownika sieci Web.
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: tutorial
ms.date: 10/20/2020
ms.author: alkohli
Customer intent: As an IT admin, I need to understand how to connect and activate Azure Stack Edge Mini R so I can use it to transfer data to Azure.
ms.openlocfilehash: fe76391a5cfce8d7d39e47131db108ab87e5aed5
ms.sourcegitcommit: 6a350f39e2f04500ecb7235f5d88682eb4910ae8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96468529"
---
# <a name="tutorial-connect-to-azure-stack-edge-mini-r"></a>Samouczek: łączenie z Azure Stack krawędzi mini R

W tym samouczku opisano sposób nawiązywania połączenia z urządzeniem Azure Stack Edge mini R przy użyciu lokalnego interfejsu użytkownika sieci Web.

Proces połączenia może potrwać około 5 minut.

Ten samouczek zawiera informacje dotyczące:

> [!div class="checklist"]
>
> * Wymagania wstępne
> * Nawiązywanie połączenia z urządzeniem fizycznym



## <a name="prerequisites"></a>Wymagania wstępne

Przed skonfigurowaniem i skonfigurowaniem urządzenia Azure Stack Edge upewnij się, że:

* Urządzenie fizyczne zostało zainstalowane zgodnie z opisem w temacie [Install Azure Stack Edge](azure-stack-edge-mini-r-deploy-install.md).


## <a name="connect-to-the-local-web-ui-setup"></a>Nawiązywanie połączenia z konfiguracją lokalnego interfejsu użytkownika sieci Web

1. Skonfiguruj kartę Ethernet na komputerze, aby nawiązać połączenie z urządzeniem Azure Stack EDGE Pro ze statycznym adresem IP 192.168.100.5 i podsiecią 255.255.255.0.

2. Podłącz komputer do portu 1 na urządzeniu. Jeśli komputer jest połączony bezpośrednio z urządzeniem (bez przełącznika), użyj kabla skrzyżowanego lub karty Ethernet USB. Użyj poniższej ilustracji, aby zidentyfikować PORT 1 na urządzeniu.

    ![Okablowanie dla Wi-Fi](./media/azure-stack-edge-mini-r-deploy-install/wireless-cabled.png)

[!INCLUDE [azure-stack-edge-gateway-delpoy-connect](../../includes/azure-stack-edge-gateway-deploy-connect.md)]


## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono następujące informacje:

> [!div class="checklist"]
> * Wymagania wstępne
> * Nawiązywanie połączenia z urządzeniem fizycznym


Aby dowiedzieć się, jak skonfigurować ustawienia sieciowe na urządzeniu, zobacz:

> [!div class="nextstepaction"]
> [Konfigurowanie sieci](./azure-stack-edge-mini-r-deploy-configure-network-compute-web-proxy.md)
