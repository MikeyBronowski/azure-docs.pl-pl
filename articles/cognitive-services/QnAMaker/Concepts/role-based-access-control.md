---
title: Współpracuj z innymi — QnA Maker
description: Dowiedz się, jak współpracować z innymi autorami i edytorami przy użyciu kontroli dostępu opartej na rolach na platformie Azure.
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 5d5a580e2b7be4699933b43687dcf164bf8f4a4a
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/03/2021
ms.locfileid: "101700086"
---
# <a name="collaborate-with-other-authors-and-editors"></a>Współpracuj z innymi autorami i edytorami

Współpracuj z innymi autorami i edytorami przy użyciu kontroli dostępu opartej na rolach (Azure RBAC) w ramach zasobu QnA Maker.

## <a name="access-is-provided-on-the-qna-maker-resource"></a>Dostęp jest dostępny dla QnA Maker zasobu

Wszystkie uprawnienia są kontrolowane przez uprawnienia umieszczane w zasobie QnA Maker. Te uprawnienia są wyrównane do odczytu, zapisu, publikowania i pełnego dostępu.

Ta funkcja RBAC platformy Azure obejmuje następujące funkcje:
* Azure Active Directory (AAD) to 100% wstecz zgodne z uwierzytelnianiem na podstawie klucza dla właścicieli i współautorów. Klienci mogą korzystać z uwierzytelniania opartego na kluczach lub uwierzytelniania opartego na rolach RBAC na platformie Azure w swoich żądaniach.
* Szybko dodawaj autorów i redaktorów do wszystkich baz wiedzy w zasobie, ponieważ kontrola znajduje się na poziomie zasobu, a nie na poziomie bazy wiedzy.

> [!NOTE]
> Upewnij się, że dla zasobu dodano niestandardową poddomenę. [Niestandardowa poddomena](../../cognitive-services-custom-subdomains.md) powinna być obecna domyślnie, ale jeśli nie, należy ją dodać

## <a name="access-is-provided-by-a-defined-role"></a>Dostęp jest udostępniany przez zdefiniowaną rolę

[!INCLUDE [Azure RBAC permissions table](../includes/role-based-access-control.md)]

## <a name="authentication-flow"></a>Przepływ uwierzytelniania

Na poniższym diagramie przedstawiono przepływ, od perspektywy autora do logowania się do portalu QnA Maker i używania interfejsów API tworzenia.

> [!div class="mx-imgBorder"]
> ![Na poniższym diagramie przedstawiono przepływ, od perspektywy autora do logowania się do portalu QnA Maker i używania interfejsów API tworzenia.](../media/qnamaker-how-to-collaborate-knowledge-base/rbac-flow-from-portal-to-service.png)

|Kroki|Opis|
|--|--|
|1|Portal uzyskuje token dla QnA Maker zasobu.|
|2|Portal wywołuje odpowiedni interfejs API tworzenia QnA Maker (APIM), przekazując token zamiast kluczy.|
|3|Interfejs API usługi QnA Maker sprawdza poprawność tokenu.|
|4 |Interfejs API usługi QnA Maker wywołuje usługę QnAMaker.|

Jeśli zamierzasz wywołać [interfejsy API tworzenia](../index.yml), Dowiedz się więcej na temat konfigurowania uwierzytelniania.

## <a name="authenticate-by-qna-maker-portal"></a>Uwierzytelnianie za pomocą portalu QnA Maker

W przypadku tworzenia i współpracy przy użyciu portalu QnA Maker po dodaniu odpowiedniej roli do zasobu dla współpracownika Portal QnA Maker zarządza wszystkimi uprawnieniami dostępu.

## <a name="authenticate-by-qna-maker-apis-and-sdks"></a>Uwierzytelnianie za pomocą QnA Maker interfejsów API i zestawów SDK

W przypadku tworzenia i współpracy z interfejsami API przy użyciu protokołu REST lub zestawów SDK należy [utworzyć nazwę główną usługi](../../authentication.md#assign-a-role-to-a-service-principal) , aby zarządzać uwierzytelnianiem.

## <a name="next-step"></a>Następny krok

* Projektowanie bazy wiedzy dla języków i aplikacji klienckich