---
author: msmbaldwin
ms.service: key-vault
ms.topic: include
ms.date: 07/20/2020
ms.author: msmbaldwin
ms.openlocfilehash: 872164dfee9f35881fca97b0339bd95c64a2f5ff
ms.sourcegitcommit: dd24c3f35e286c5b7f6c3467a256ff85343826ad
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2021
ms.locfileid: "99070218"
---
Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. Użyj polecenia cmdlet Azure PowerShell [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) , aby utworzyć grupę zasobów o nazwie Moja *resourceName* w lokalizacji *Wschodnie* . 

```azurepowershell-interactive
New-AzResourceGroup -Name "myResourceGroup" -Location "EastUS"
```
