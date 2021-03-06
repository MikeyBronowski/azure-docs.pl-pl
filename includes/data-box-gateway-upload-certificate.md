---
author: alkohli
ms.service: databox
ms.topic: include
ms.date: 10/15/2020
ms.author: alkohli
ms.openlocfilehash: 27a4d775b8d88e02be69655e5adfc6155f867ef6
ms.sourcegitcommit: 16c7fd8fe944ece07b6cf42a9c0e82b057900662
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/03/2020
ms.locfileid: "96582743"
---
Odpowiedni certyfikat SSL zapewnia, że dane zaszyfrowane są wysyłane do właściwego serwera. Oprócz szyfrowania certyfikat umożliwia również uwierzytelnianie. Można przekazać własny zaufany certyfikat SSL za pośrednictwem interfejsu programu PowerShell urządzenia.

1. [Nawiąż połączenie z interfejsem programu PowerShell](#connect-to-the-powershell-interface).
2. Użyj `Set-HcsCertificate` polecenia cmdlet, aby przekazać certyfikat. Po wyświetleniu monitu podaj następujące parametry:

   - `CertificateFilePath` -Ścieżka do udziału zawierającego plik certyfikatu w formacie *PFX* .
   - `CertificatePassword` — Hasło używane do ochrony certyfikatu.
   - `Credentials` -Username, aby uzyskać dostęp do udziału, który zawiera certyfikat. Po wyświetleniu monitu podaj hasło do udziału sieciowego.

     W poniższym przykładzie pokazano użycie tego polecenia cmdlet:

     ```
     Set-HcsCertificate -Scope LocalWebUI -CertificateFilePath "\\myfileshare\certificates\mycert.pfx" -CertificatePassword "mypassword" -Credential "Username"
     ```
