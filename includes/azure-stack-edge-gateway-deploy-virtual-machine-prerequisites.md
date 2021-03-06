---
author: alkohli
ms.service: databox
ms.topic: include
ms.date: 01/15/2021
ms.author: alkohli
ms.openlocfilehash: 71d5a910e36762d096763c4f45a13cbdad47414d
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/03/2021
ms.locfileid: "101730629"
---
Przed wdrożeniem maszyn wirtualnych na urządzeniu z systemem Azure Stack Edge musisz skonfigurować klienta programu tak, aby łączył się z urządzeniem za pośrednictwem Azure Resource Manager przez Azure PowerShell. Aby uzyskać szczegółowe instrukcje, zobacz [nawiązywanie połączenia z Azure Resource Manager na urządzeniu brzegowym Azure Stack](../articles/databox-online/azure-stack-edge-j-series-connect-resource-manager.md).

Upewnij się, że w celu uzyskania dostępu do urządzenia z poziomu klienta można wykonać następujące czynności. Ta konfiguracja została już wykonana po nawiązaniu połączenia z usługą Azure Resource Manager i teraz sprawdzanie, czy konfiguracja zakończyła się pomyślnie. 

1. Sprawdź, czy Azure Resource Manager komunikacja działa, uruchamiając następujące polecenie:     

    ```powershell
    Add-AzureRmEnvironment -Name <Environment Name> -ARMEndpoint "https://management.<appliance name>.<DNSDomain>"
    ```

1. Aby wywołać interfejsy API urządzeń lokalnych w celu uwierzytelnienia, wprowadź: 

    `login-AzureRMAccount -EnvironmentName <Environment Name>`

    Aby nawiązać połączenie za pośrednictwem Azure Resource Manager, podaj nazwę użytkownika *EdgeARMuser* i hasło.

1. W przypadku skonfigurowania obliczeń dla Kubernetes można pominąć ten krok. W przeciwnym razie upewnij się, że interfejs sieciowy został włączony do obliczeń, wykonując następujące czynności: 

   a. W lokalnym interfejsie użytkownika przejdź do pozycji ustawienia **obliczeń** .  
   b. Wybierz interfejs sieciowy, który ma zostać użyty do utworzenia przełącznika wirtualnego. Utworzone maszyny wirtualne zostaną podłączone do przełącznika wirtualnego, który jest dołączony do tego portu i skojarzonej sieci. Upewnij się, że wybrano sieć zgodną z adresem IP, który będzie używany przez maszynę wirtualną.  

    ![Zrzut ekranu przedstawiający okienko ustawień sieciowych konfiguracji obliczeniowej.](../articles/databox-online/media/azure-stack-edge-gpu-deploy-virtual-machine-templates/enable-compute-setting.png)

   c. W obszarze **Włącz dla obliczeń** w interfejsie sieciowym wybierz opcję **tak**. Azure Stack Edge utworzy przełącznik wirtualny, który odpowiada temu interfejsowi sieciowemu i będzie nim zarządzać. W tej chwili nie wprowadzaj określonych adresów IP dla usługi Kubernetes. Włączenie obliczeń może potrwać kilka minut.

    > [!NOTE]
    > Jeśli tworzysz maszyny wirtualne GPU, wybierz interfejs sieciowy, który jest połączony z Internetem. Dzięki temu można zainstalować na urządzeniu rozszerzenie procesora GPU.


