---
author: PatrickFarley
ms.service: cognitive-services
ms.subservice: custom-vision
ms.topic: include
ms.date: 07/17/2019
ms.author: pafarley
ms.openlocfilehash: 07e7cc991f127bf4bb4f466c0108962786e45bce
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "96018379"
---
Zwróć uwagę na suwak **próg prawdopodobieństwa** w lewym okienku na karcie **wydajność** . Jest to poziom pewności, że przewidywanie musi mieć być uznawane za prawidłowe (na potrzeby obliczenia precyzji i odwołania). 

Gdy interpretujesz wywołania prognoz z progiem wysokiego prawdopodobieństwa, mają one zwrócić wyniki z wysoką dokładnością kosztu odwołania &mdash; wykryte klasyfikacje są poprawne, ale wiele nie zostanie wykryte. Próg niskiego prawdopodobieństwa oznacza, że wszystkie &mdash; rzeczywiste klasyfikacje są wykrywane, ale w tym zestawie występuje więcej fałszywych wartości dodatnich. Pamiętając o tym, należy ustawić próg prawdopodobieństwa zgodnie z konkretnymi potrzebami projektu. Później, gdy otrzymujesz wyniki przewidywania po stronie klienta, należy użyć tej samej wartości progowej prawdopodobieństwa, która została użyta w tym miejscu.