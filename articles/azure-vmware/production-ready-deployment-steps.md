---
title: Planowanie wdrożenia rozwiązań VMware na platformie Azure
description: W tym artykule opisano przepływ pracy wdrażania rozwiązań VMware platformy Azure.  Wynik końcowy to środowisko gotowe do tworzenia i migracji maszyn wirtualnych.
ms.topic: tutorial
ms.date: 02/22/2021
ms.openlocfilehash: f9d49d7ff8109364c9fc1eee4388b30ccc1a61b6
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/03/2021
ms.locfileid: "101733668"
---
# <a name="planning-the-azure-vmware-solution-deployment"></a>Planowanie wdrożenia rozwiązań VMware na platformie Azure

Ten artykuł zawiera informacje o procesie planowania w celu identyfikowania i zbierania danych używanych podczas wdrażania. Podczas planowania wdrożenia, pamiętaj o udokumentowaniu zbieranych informacji w celu łatwego odwoływania się podczas wdrażania.

Procesy tego szybkiego startu powodują tworzenie maszyn wirtualnych i migracji w środowisku gotowym do produkcji. 

>[!IMPORTANT]
>Przed utworzeniem zasobu rozwiązania VMware platformy Azure należy wykonać artykuł dotyczący [sposobu włączania zasobów rozwiązania VMware dla platformy Azure](enable-azure-vmware-solution.md) w celu przesłania biletu pomocy technicznej w celu przydzielenia hostów. Gdy zespół pomocy technicznej otrzyma Twoje żądanie, zajmie do pięciu dni roboczych, aby potwierdzić żądanie i przydzielić hosty. Jeśli masz istniejącą chmurę prywatną rozwiązania VMware platformy Azure i potrzebujesz większej liczby hostów, przejdziesz do tego samego procesu. 


## <a name="subscription"></a>Subskrypcja

Określ subskrypcję, która ma zostać użyta do wdrożenia rozwiązania VMware platformy Azure.  Można utworzyć nową subskrypcję lub ponownie użyć istniejącej.

>[!NOTE]
>Subskrypcja musi być skojarzona z programem Microsoft Enterprise Agreement lub planem platformy Azure dla dostawcy rozwiązań w chmurze. Aby uzyskać więcej informacji, zobacz [How to enable Azure VMware Solution Resource](enable-azure-vmware-solution.md).

## <a name="resource-group"></a>Grupa zasobów

Zidentyfikuj grupę zasobów, której chcesz użyć dla rozwiązania VMware platformy Azure.  Ogólnie rzecz biorąc, Grupa zasobów jest tworzona dla rozwiązań VMware platformy Azure, ale można użyć istniejącej grupy zasobów.

## <a name="region"></a>Region (Region)

Określ region, dla którego ma zostać wdrożone rozwiązanie Azure VMware.  Aby uzyskać więcej informacji, zapoznaj się z [przewodnikiem dotyczącym produktów platformy Azure dostępnych według regionów](https://azure.microsoft.com/en-us/global-infrastructure/services/?products=azure-vmware).

## <a name="resource-name"></a>Nazwa zasobu

Zdefiniuj nazwę zasobu, która będzie używana podczas wdrażania.  Nazwa zasobu jest przyjazną i opisową nazwą, w której jest określana Chmura prywatna rozwiązania Azure VMware.

>[!IMPORTANT]
>Długość nazwy nie może przekraczać 40 znaków. Jeśli nazwa przekroczy ten limit, nie będzie można tworzyć publicznych adresów IP do użycia z chmurą prywatną. 

## <a name="size-hosts"></a>Rozmiar hostów

Określ rozmiar hostów, które mają być używane podczas wdrażania rozwiązania Azure VMware.  Aby uzyskać pełną listę, zobacz dokumentację [chmur prywatnych i klastrów rozwiązań VMware platformy Azure](concepts-private-clouds-clusters.md#hosts) .

## <a name="number-of-hosts"></a>Liczba hostów

Zdefiniuj liczbę hostów, które chcesz wdrożyć w chmurze prywatnej rozwiązania Azure VMware.  Minimalna liczba hostów wynosi trzy, a maksymalna wynosi 16 na klaster.  Aby uzyskać więcej informacji, zapoznaj się z dokumentacją dotyczącą [chmury i klastrów prywatnych rozwiązania Azure VMware](concepts-private-clouds-clusters.md#clusters) .

Klaster można zawsze później zwiększyć, jeśli trzeba przekroczyć początkowy numer wdrożenia.

## <a name="ip-address-segment"></a>Segment adresów IP

Pierwszym krokiem w procesie planowania wdrożenia jest zaplanowanie segmentacji adresów IP.  Rozwiązanie Azure VMware pozyskuje podaną sieć/22. Następnie carves go do mniejszych segmentów, a następnie używa tych segmentów IP dla vCenter, VMware HCX, NSX-T i vMotion.

Rozwiązanie Azure VMware nawiązuje połączenie z Microsoft Azure Virtual Network za pomocą wewnętrznego obwodu usługi ExpressRoute. W większości przypadków nawiązuje połączenie z centrum danych za poorednictwem ExpressRoute Global Reach. 

Rozwiązanie Azure VMware, istniejące środowisko platformy Azure i środowisko lokalne wszystkie trasy wymiany (zazwyczaj). W takim przypadku blok adresów sieciowych CIDR/22 zdefiniowany w tym kroku nie powinien nakładać się na wszystkie elementy, które są już lokalnie lub na platformie Azure.

**Przykład:** 10.0.0.0/22

Aby uzyskać więcej informacji, zobacz [Lista kontrolna planowania sieci](tutorial-network-checklist.md#routing-and-subnet-considerations).

:::image type="content" source="media/pre-deployment/management-vmotion-vsan-network-ip-diagram.png" alt-text="Identyfikowanie — segment adresów IP" border="false":::  

## <a name="ip-address-segment-for-virtual-machine-workloads"></a>Segment adresów IP dla obciążeń maszyny wirtualnej

Zidentyfikuj segment IP, aby utworzyć pierwszą sieć (segment NSX) w chmurze prywatnej.  Innymi słowy, chcesz utworzyć segment sieci w rozwiązaniu VMware platformy Azure, aby można było wdrożyć maszyny wirtualne w rozwiązaniu VMware platformy Azure.   

Nawet jeśli planujesz tylko rozszerzanie sieci L2, Utwórz segment sieci, który będzie sprawdzać poprawność środowiska.

Należy pamiętać, że wszystkie tworzone segmenty IP muszą być unikatowe na platformie Azure i lokalnie.  

**Przykład:** 10.0.4.0/24

:::image type="content" source="media/pre-deployment/nsx-segment-diagram.png" alt-text="Identyfikowanie segmentu adresów IP dla obciążeń maszyny wirtualnej" border="false":::     

## <a name="optional-extend-networks"></a>Obowiązkowe Rozszerzone sieci

Segmenty sieci można rozszerać z rozwiązań lokalnych do platformy Azure VMware, a jeśli to zrobisz, należy zidentyfikować te sieci teraz.  

Należy pamiętać, że:

- Jeśli planujesz rozszerzoną sieć ze środowiska lokalnego, te sieci muszą łączyć się z [przełącznikiem rozproszonym vSphere (vDS)](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.networking.doc/GUID-B15C6A13-797E-4BCB-B9D9-5CBC5A60C3A6.html) w lokalnym środowisku VMware.  
- Jeśli sieci, które chcesz rozszerzyć na żywo na [przełączniku standardowym vSphere](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.networking.doc/GUID-350344DE-483A-42ED-B0E2-C811EE927D59.html), nie można ich rozszerzyć.

## <a name="attach-virtual-network-to-azure-vmware-solution"></a>Dołączanie sieci wirtualnej do rozwiązania VMware platformy Azure

W tym kroku określisz bramę sieci wirtualnej ExpressRoute i obsługujemy Virtual Network platformy Azure służącą do łączenia obwodu usługi Azure VMware ExpressRoute.  Obwód usługi ExpressRoute umożliwia nawiązywanie połączeń z chmurą prywatną rozwiązania Azure VMware i z niej do innych usług platformy Azure, zasobów platformy Azure i środowisk lokalnych.

Możesz użyć *istniejącej* lub *nowej* bramy sieci wirtualnej ExpressRoute.

:::image type="content" source="media/pre-deployment/azure-vmware-solution-expressroute-diagram.png" alt-text="Tożsamość — Virtual Network platformy Azure, aby dołączyć rozwiązanie VMware dla platformy Azure" border="false":::

### <a name="use-an-existing-expressroute-virtual-network-gateway"></a>Użyj istniejącej bramy sieci wirtualnej ExpressRoute

Jeśli używasz *istniejącej* bramy sieci wirtualnej ExpressRoute, obwód usługi Azure VMware ExpressRoute jest ustanawiany po wdrożeniu chmury prywatnej. W takim przypadku pozostaw pole **Virtual Network** puste.  

Zanotuj, której bramy sieci wirtualnej ExpressRoute będziesz używać, i przejdź do następnego kroku.

### <a name="create-a-new-expressroute-virtual-network-gateway"></a>Tworzenie nowej bramy sieci wirtualnej ExpressRoute

Podczas tworzenia *nowej* bramy sieci wirtualnej ExpressRoute można użyć istniejącej usługi Azure Virtual Network lub utworzyć nową.  

- W przypadku istniejącej sieci wirtualnej platformy Azure:
   1. Sprawdź, czy w sieci wirtualnej nie ma żadnych istniejących bram sieci wirtualnej ExpressRoute. 
   1. Wybierz z listy **Virtual Network** istniejące Virtual Network platformy Azure.

- Nowe Virtual Network platformy Azure można utworzyć z wyprzedzeniem lub podczas wdrażania. Wybierz pozycję **Utwórz nowy** link poniżej listy **Virtual Network** .

Na poniższej ilustracji przedstawiono ekran **Tworzenie wdrożenia chmury prywatnej** z wyróżnionym polem **Virtual Network** .

:::image type="content" source="media/pre-deployment/azure-vmware-solution-deployment-screen-vnet-circle.png" alt-text="Zrzut ekranu przedstawiający ekran wdrożenia rozwiązania VMware platformy Azure z wyróżnionym polem Virtual Network.":::

>[!NOTE]
>Każda sieć wirtualna, która ma być używana lub utworzona, może być widoczna w środowisku lokalnym i w rozwiązaniu Azure VMware, dlatego należy się upewnić, że jakikolwiek segment IP używany w tej sieci wirtualnej i podsieci nie nakładają się na siebie.

## <a name="vmware-hcx-network-segments"></a>Segmenty sieci VMware HCX

VMware HCX to technologia dostosowana do rozwiązań VMware platformy Azure. Podstawowym przypadkiem użycia programu VMware HCX są migracje obciążeń i odzyskiwanie po awarii. Jeśli planujesz wykonać te czynności, najlepiej zaplanuj sieć teraz.   W przeciwnym razie możesz pominąć i przejść do następnego kroku.

[!INCLUDE [hcx-network-segments](includes/hcx-network-segments.md)]

## <a name="next-steps"></a>Następne kroki
Teraz, po zebraniu i udokumentowaniu potrzebnych informacji, przejdź do następnej sekcji, aby utworzyć chmurę prywatną rozwiązania Azure VMware.

> [!div class="nextstepaction"]
> [Wdrażanie usługi Azure VMware Solution](deploy-azure-vmware-solution.md)
