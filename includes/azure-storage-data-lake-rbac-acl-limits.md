---
services: storage
author: normesta
ms.service: storage
ms.topic: include
ms.date: 09/29/2020
ms.author: normesta
ms.custom: include file
ms.openlocfilehash: 97b47b48a183951002d04cd58b08d5e2b9051eda
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "96017688"
---
| Mechanism (Mechanizm) | Zakres |Limity | Obsługiwany poziom uprawnień |
|---|---|---|---|
| Kontrola dostępu na podstawie ról platformy Azure | Konta magazynu, kontenery. <br>Międzyzasobówowe przypisania ról platformy Azure na poziomie subskrypcji lub grupy zasobów. | 2000 przypisań ról platformy Azure w ramach subskrypcji | Role platformy Azure (wbudowane lub niestandardowe) |
| STARSZ| Katalog, plik |32 wpisy listy ACL (efektywne 28 wpisów listy ACL) dla każdego pliku i dla katalogu. Dostęp i domyślne listy ACL mają własne limity wpisów listy kontroli dostępu 32. |Uprawnienie listy ACL|
