---
title: Korzystanie z narzędzia Purview Studio
description: W tym artykule opisano sposób korzystania z usługi Azure kontrolą Studio.
author: nayenama
ms.author: nayenama
ms.service: purview
ms.subservice: purview-data-catalog
ms.topic: conceptual
ms.date: 11/12/2020
ms.openlocfilehash: d8e6c4b2addf9745b2ddabe8f6fdad9d82dce59f
ms.sourcegitcommit: 2ba6303e1ac24287762caea9cd1603848331dd7a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97503954"
---
# <a name="use-purview-studio"></a>Korzystanie z narzędzia Purview Studio

Ten artykuł zawiera omówienie niektórych głównych funkcji usługi Azure kontrolą.

## <a name="prerequisites"></a>Wymagania wstępne

* Aktywne konto kontrolą zostało już utworzone w Azure Portal, a użytkownik ma uprawnienia dostępu do kontrolą Studio.

## <a name="launch-purview-account"></a>Uruchom konto kontrolą

* Aby uruchomić konto kontrolą, przejdź do konta kontrolą w Azure Portal, wybierz konto, które chcesz uruchomić, i uruchom konto.

   :::image type="content" source="./media/use-purview-studio/launch-from-portal.png" alt-text="Zrzut ekranu przedstawiający wybór w celu uruchomienia wykazu kont usługi Azure kontrolą.":::

* Innym sposobem uruchomienia konta kontrolą jest przejście do programu `https://web.purview.azure.com` , wybranie **Azure Active Directory** i nazwy konta w celu uruchomienia konta.

## <a name="home-page"></a>Strona główna

Strona **główna** jest stroną początkową dla klienta usługi Azure kontrolą.

 :::image type="content" source="./media/use-purview-studio/purview-homepage.png" alt-text="Zrzut ekranu strony głównej.":::

Poniższa lista zawiera podsumowanie najważniejszych funkcji **strony głównej**. Każda liczba na liście odpowiada wyróżnionej liczbie na poprzednim zrzucie ekranu.

1. Przyjazna nazwa katalogu. Nazwę katalogu można skonfigurować w **centrum zarządzania** > **Informacje o koncie*.

2. Analiza wykazu pokazuje liczbę:
    - Użytkownicy, grupy i aplikacje
    - Źródła danych
    - Elementy zawartości
    - Terminy słownika

3. Pole wyszukiwania umożliwia wyszukiwanie zasobów danych w ramach wykazu danych.

4. Przyciski szybki dostęp zapewniają dostęp do często używanych funkcji aplikacji. Wyświetlane przyciski są zależne od roli przypisanej do konta użytkownika.

    - W przypadku *Curator danych* przyciski to **centrum wiedzy**, **przeglądanie zasobów**, **Zarządzanie słownikiem** i **wgląd w szczegółowe** dane.
    - W *przypadku czytnika danych* polecanymi przyciskami **są centrum wiedzy**, **przeglądanie zasobów**, **Wyświetlanie słownika** i **wgląd w szczegółowe** dane.
    - W przypadku Curator danych *administratora źródła danych*  +  proponowane przyciski to **centrum wiedzy**, **Rejestrowanie źródeł danych**, **przeglądanie zasobów** i **Zarządzanie słownikiem**.
    - W przypadku czytnika danych *administratora źródła danych*  +  przyciski Polecane to **centrum wiedzy**, **Rejestrowanie źródeł danych**, **przeglądanie zasobów** i **słownik wyświetlania**.

5. Lewy pasek nawigacyjny ułatwia znalezienie najważniejszych stron aplikacji. Wyświetlane przyciski są zależne od roli przypisanej do konta użytkownika.

    - W przypadku *Curator danych* przyciski to **Home**, **Słowniczek**, **Insights** i **Management Center**.
    - W przypadku *czytnika danych* przyciski to **Strona główna**, **słownik**, **szczegółowe informacje** i **centrum zarządzania**.
    - W *przypadku*  +  *Curator/czytnika danych* administratora źródła danych przyciski to **Strona główna**, **źródła**, **słownik**, **szczegółowe informacje** i **centrum zarządzania**.
  
6. Karta **ostatnio używane** zawiera listę ostatnio używanych zasobów danych. Informacje o dostępie do zasobów znajdują się [w temacie wyszukiwanie Data Catalog](how-to-search-catalog.md) i [przeglądanie według typu zasobu](how-to-browse-catalog.md#browse-experience).  Karta **Moje elementy** jest listą zasobów danych należących do zalogowanego użytkownika.
7. **Przydatne linki** zawierają linki do stanu regionu, dokumentacji, cennika, przeglądu i stanu kontrolą
8. Górny pasek nawigacyjny zawiera informacje na temat informacji o wersji/aktualizacji, zmiany kontrolą konta, powiadomień, pomocy i informacji zwrotnych.

## <a name="knowledge-center"></a>Centrum wiedzy

Centrum wiedzy umożliwia znalezienie wszystkich filmów wideo i samouczków związanych z kontrolą.

## <a name="guided-tours"></a>Przewodniki

Każde środowisko użytkownika w usłudze Azure kontrolą Studio zawiera przewodniki, w których można zadawać Przegląd strony. Aby rozpocząć Przewodnik, wybierz pozycję **Pomoc** na górnym pasku i wybierz pozycję przewodniki z **przewodnikiem**.

:::image type="content" source="./media/use-purview-studio/guided-tour.png" alt-text="Zrzut ekranu przedstawiający Przewodnik po samouczku.":::

> [!Important]
   > Rola administratora źródła danych nie ma dostępu do programu kontrolą Studio.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dodawanie podmiotu zabezpieczeń](tutorial-scan-data.md)