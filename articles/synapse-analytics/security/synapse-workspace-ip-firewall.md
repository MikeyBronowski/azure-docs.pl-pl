---
title: Konfigurowanie reguł zapory adresów IP
description: Artykuł, który uczy się skonfigurować reguły zapory IP w usłudze Azure Synapse Analytics
author: RonyMSFT
ms.service: synapse-analytics
ms.topic: overview
ms.subservice: security
ms.date: 04/15/2020
ms.author: ronytho
ms.reviewer: jrasnick
ms.openlocfilehash: b937dad6c3c8f5a5773ca7779493b41c905307b1
ms.sourcegitcommit: 2dd0932ba9925b6d8e3be34822cc389cade21b0d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/01/2021
ms.locfileid: "99226509"
---
# <a name="azure-synapse-analytics-ip-firewall-rules"></a>Reguły zapory adresów IP usługi Azure Synapse Analytics

W tym artykule opisano reguły zapory IP i naucz się, jak je skonfigurować w usłudze Azure Synapse Analytics.

## <a name="ip-firewall-rules"></a>Reguły zapory adresów IP

Reguły zapory bazującej na adresach IP umożliwiają udzielenie lub zablokowanie dostępu do obszaru roboczego usługi Synapse na podstawie źródłowego adresu IP każdego żądania. Reguły zapory bazującej na adresach IP można skonfigurować dla obszaru roboczego. Reguły zapory adresów IP skonfigurowane na poziomie obszaru roboczego mają zastosowanie do wszystkich publicznych punktów końcowych obszaru roboczego (dedykowane pule SQL, bezserwerowa Pula SQL i programowanie).

## <a name="create-and-manage-ip-firewall-rules"></a>Tworzenie reguł zapory bazujących na adresach IP i zarządzanie nimi

Istnieją dwa sposoby dodawania reguł zapory IP do obszaru roboczego Synapse. Aby dodać zaporę IP do obszaru roboczego, wybierz pozycję **zabezpieczenia i obsługa sieci** i zaznacz pole wyboru **Zezwalaj na połączenia ze wszystkich adresów IP** podczas tworzenia obszaru roboczego.

![Zrzut ekranu, który podświetla przycisk Zabezpieczenia i sieć.](./media/synpase-workspace-ip-firewall/ip-firewall-1.png)

![Azure Portal konfigurację adresu IP obszaru roboczego Synapse.](./media/synpase-workspace-ip-firewall/ip-firewall-2.png)

Możesz również dodać reguły zapory adresów IP do obszaru roboczego Synapse po utworzeniu obszaru roboczego. Wybierz pozycję **zapory** w obszarze **zabezpieczenia** z Azure Portal. Aby dodać nową regułę zapory adresów IP, nadaj jej nazwę, początkowy adres IP i końcowy adres IP. Po zakończeniu wybierz pozycję **Zapisz**.

![Konfiguracja adresu IP obszaru roboczego usługi Azure Synapse w Azure Portal.](./media/synpase-workspace-ip-firewall/ip-firewall-3.png)

## <a name="connect-to-synapse-from-your-own-network"></a>Nawiązywanie połączenia z usługą Synapse z własnej sieci

Możesz nawiązać połączenie z obszarem roboczym usługi Synapse za pomocą programu Synapse Studio. Możesz również użyć SQL Server Management Studio (SSMS), aby nawiązać połączenie z zasobami SQL (dedykowanymi pulami SQL i bezserwerową pulą SQL) w obszarze roboczym.

Upewnij się, że Zapora w sieci i komputer lokalny zezwalają na komunikację wychodzącą na portach TCP 80, 443 i 1443 dla Synapse Studio.

Ponadto należy zezwolić na komunikację wychodzącą na porcie UDP 53 dla Synapse Studio. Aby nawiązać połączenie przy użyciu narzędzi, takich jak program SSMS i Power BI, musisz zezwolić na komunikację wychodzącą na porcie TCP 1433.

Zasady połączenia SQL są ustawiane *Domyślnie* dla obszaru roboczego. Możesz dowiedzieć się więcej o adresach IP i portach [, które klienci](../../azure-sql/database/connectivity-architecture.md#connection-policy)powinni zezwalać na komunikację wychodzącą.




## <a name="next-steps"></a>Następne kroki

Tworzenie [obszaru roboczego usługi Azure Synapse](../quickstart-create-workspace.md)

Tworzenie obszaru roboczego usługi Azure Synapse z [zarządzanym obszarem roboczym Virtual Network](./synapse-workspace-managed-vnet.md)