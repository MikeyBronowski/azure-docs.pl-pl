---
title: TimestampToDateTime w języku zapytań Azure Cosmos DB
description: Dowiedz się więcej o funkcji TimestampToDateTime systemu SQL w Azure Cosmos DB.
author: timsander1
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.topic: conceptual
ms.date: 08/18/2020
ms.author: tisande
ms.custom: query-reference
ms.openlocfilehash: af5e0eeb808835fd4f36a0eda79618f831248ad9
ms.sourcegitcommit: fa90cd55e341c8201e3789df4cd8bd6fe7c809a3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2020
ms.locfileid: "93340774"
---
# <a name="timestamptodatetime-azure-cosmos-db"></a>TimestampToDateTime (Azure Cosmos DB)
[!INCLUDE[appliesto-sql-api](includes/appliesto-sql-api.md)]

Konwertuje określoną wartość sygnatury czasowej na datę i godzinę.
  
## <a name="syntax"></a>Składnia
  
```sql
TimestampToDateTime (<Timestamp>)
```

## <a name="arguments"></a>Argumenty

*Timestamp*  

Podpisana wartość liczbowa, czyli bieżąca liczba milisekund, które upłynęły od epoki systemu UNIX. Innymi słowy, liczba milisekund, które upłynęły od 00:00:00 czwartek, 1 stycznia 1970.

## <a name="return-types"></a>Typy zwracane

Zwraca wartość ciągu ISO 8601 daty i czasu UTC w formacie, `YYYY-MM-DDThh:mm:ss.fffffffZ` gdzie:
  
  |Format|Opis|
  |-|-|
  |YYYY|rok czterocyfrowy|
  |MM|dwucyfrowy miesiąc (01 = styczeń itd.)|
  |DD|dwucyfrowy dzień miesiąca (od 01 do 31)|
  |T|Oznaczanie na początku elementów czasu|
  |hh|godzina dwucyfrowy (od 00 do 23)|
  |mm|minuty dwucyfrowe (od 00 do 59)|
  |ss|dwa cyfry sekund (od 00 do 59)|
  |. fffffff|siedem cyfr sekund|
  |Z|Oznaczenie UTC (skoordynowany czas uniwersalny)||
  
  Aby uzyskać więcej informacji na temat formatu ISO 8601, zobacz [ISO_8601](https://en.wikipedia.org/wiki/ISO_8601)

## <a name="remarks"></a>Uwagi

TimestampToDateTime będzie zwracana `undefined` , jeśli określona wartość sygnatury czasowej jest nieprawidłowa.

## <a name="examples"></a>Przykłady
  
Poniższy przykład konwertuje sygnaturę czasową na datę i godzinę:

```sql
SELECT TimestampToDateTime(1594227912345) AS DateTime
```

```json
[
    {
        "DateTime": "2020-07-08T17:05:12.3450000Z"
    }
]
```  

## <a name="next-steps"></a>Następne kroki

- [Funkcje daty i godziny Azure Cosmos DB](sql-query-date-time-functions.md)
- [Azure Cosmos DB funkcje systemowe](sql-query-system-functions.md)
- [Wprowadzenie do usługi Azure Cosmos DB](introduction.md)
