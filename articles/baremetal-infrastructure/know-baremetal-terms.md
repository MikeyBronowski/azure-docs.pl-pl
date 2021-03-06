---
title: Znajomość warunków infrastruktury Azure BareMetal
description: Poznaj warunki infrastruktury Azure BareMetal.
ms.topic: conceptual
ms.date: 1/4/2021
ms.openlocfilehash: fd7a39854c86f728ef152f8e7d858157e1ad26f4
ms.sourcegitcommit: aeba98c7b85ad435b631d40cbe1f9419727d5884
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2021
ms.locfileid: "97861916"
---
# <a name="know-the-terms-for-baremetal-infrastructure"></a>Poznaj warunki dotyczące infrastruktury BareMetal

W tym artykule omówiono niektóre ważne warunki BareMetal.

- **Poprawka**: istnieje Oryginalna poprawka sygnatury znana jako Poprawka 3 (rev 3) i dwie różne wersje stempla dla sygnatur wystąpień BareMetal. Każda sygnatura różni się w architekturze i sąsiedztwie na hostach maszyn wirtualnych platformy Azure:
    - **Poprawka 4** (rev 4): nowszy projekt, który zapewnia bliższe bliskość hostom maszyn wirtualnych platformy Azure i obniża opóźnienie między maszynami wirtualnymi platformy Azure i jednostkami wystąpienia BareMetal. 
    - **Poprawka 4,2** (rev 4,2): Najnowsza BareMetal infrastruktura z użyciem istniejącej architektury rev 4. Rev 4 zapewnia bliższą bliskość hostom maszyn wirtualnych platformy Azure. W przypadku opóźnień sieci między maszynami wirtualnymi platformy Azure i jednostkami wystąpienia BareMetal wdrożonymi w znacznikach lub wierszach z 4. Możesz uzyskać dostęp do wystąpień BareMetal i zarządzać nimi za pomocą Azure Portal.    

- **Sygnatura**: określa wewnętrzny rozmiar wdrożenia firmy Microsoft BareMetal Instances. Aby można było wdrożyć jednostki wystąpień, należy wdrożyć sygnaturę wystąpienia BareMetal składającą się z stojaków obliczeniowych, sieci i magazynu w lokalizacji centrum danych. Takie wdrożenie nosi nazwę sygnatury wystąpienia BareMetal lub z poprawki 4,2.

- **Dzierżawca**: klient wdrożony w sygnaturze wystąpienia BareMetal zostaje odizolowany do *dzierżawy.* Dzierżawa jest odizolowana od sieci, magazynu i warstwy obliczeniowej od innych dzierżawców. Jednostki magazynowe i obliczeniowe przypisane do różnych dzierżawców nie są ze sobą widoczne ani nie komunikują się ze sobą na poziomie sygnatury wystąpienia BareMetal. Klient może wybrać wdrożenie w różnych dzierżawach. Nawet nie ma żadnej komunikacji między dzierżawcami na poziomie sygnatury wystąpienia BareMetal.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [infrastrukturze BareMetal](workloads/sap/baremetal-overview-architecture.md) lub sposobach [identyfikowania i współpracy z jednostkami wystąpień BareMetal](workloads/sap/baremetal-infrastructure-portal.md). 