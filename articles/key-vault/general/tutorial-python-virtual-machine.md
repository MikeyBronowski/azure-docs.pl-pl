---
title: Samouczek — używanie Azure Key Vault z maszyną wirtualną w języku Python | Microsoft Docs
description: W tym samouczku skonfigurujesz maszynę wirtualną aplikacji w języku Python w celu odczytu wpisu tajnego z magazynu kluczy.
services: key-vault
author: msmbaldwin
ms.service: key-vault
ms.subservice: general
ms.topic: tutorial
ms.date: 07/20/2020
ms.author: mbaldwin
ms.custom: mvc, devx-track-python, devx-track-azurecli
ms.openlocfilehash: ae62bf353f8a92c4408d4a38a91771ad60a13107
ms.sourcegitcommit: 7863fcea618b0342b7c91ae345aa099114205b03
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93285302"
---
# <a name="tutorial-use-azure-key-vault-with-a-virtual-machine-in-python"></a>Samouczek: używanie Azure Key Vault z maszyną wirtualną w języku Python

Azure Key Vault pomaga chronić klucze, wpisy tajne i certyfikaty, takie jak klucze interfejsu API i parametry połączenia bazy danych.

W tym samouczku skonfigurujesz aplikację w języku Python do odczytywania informacji z Azure Key Vault przy użyciu zarządzanych tożsamości dla zasobów platformy Azure. Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie magazynu kluczy
> * Przechowywanie wpisu tajnego w Key Vault
> * Tworzenie maszyny wirtualnej platformy Azure z systemem Linux
> * Włączanie [tożsamości zarządzanej](../../active-directory/managed-identities-azure-resources/overview.md) dla maszyny wirtualnej
> * Przyznaj uprawnienia wymagane do odczytania danych z Key Vault przez aplikację konsolową
> * Pobierz klucz tajny z Key Vault

Przed rozpoczęciem Przeczytaj [Key Vault podstawowe pojęcia](basic-concepts.md). 

Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="prerequisites"></a>Wymagania wstępne

Dla systemów Windows, Mac i Linux:
  * [Narzędzia](https://git-scm.com/downloads)
  * Ten samouczek wymaga uruchomienia interfejsu wiersza polecenia platformy Azure lokalnie. Musisz mieć zainstalowany interfejs wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja wiersza polecenia lub jego uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0](/cli/azure/install-azure-cli).

## <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure.

Aby zalogować się do platformy Azure przy użyciu interfejsu wiersza polecenia platformy Azure, wpisz:

```azurecli
az login
```

## <a name="create-a-resource-group-and-key-vault"></a>Tworzenie grupy zasobów i magazynu kluczy

[!INCLUDE [Create a resource group and key vault](../../../includes/key-vault-rg-kv-creation.md)]

## <a name="populate-your-key-vault-with-a-secret"></a>Wypełnij swój magazyn kluczy kluczem tajnym

[!INCLUDE [Create a secret](../../../includes/key-vault-create-secret.md)]

## <a name="create-a-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz maszynę wirtualną o nazwie **myVM** przy użyciu jednej z następujących metod:

| Linux | Windows |
|--|--|
| [Interfejs wiersza polecenia platformy Azure](../../virtual-machines/linux/quick-create-cli.md) | [Interfejs wiersza polecenia platformy Azure](../../virtual-machines/windows/quick-create-cli.md) |
| [PowerShell](../../virtual-machines/linux/quick-create-powershell.md) | [PowerShell](../../virtual-machines/windows/quick-create-powershell.md) |
| [Witryna Azure Portal](../../virtual-machines/linux/quick-create-portal.md) | [Witryna Azure Portal](../../virtual-machines/windows/quick-create-portal.md) |

Aby utworzyć maszynę wirtualną z systemem Linux przy użyciu interfejsu wiersza polecenia platformy Azure, użyj polecenie [AZ VM Create](/cli/azure/vm) .  Poniższy przykład dodaje konto użytkownika o nazwie *azureuser*. Parametr `--generate-ssh-keys` jest używany, aby automatycznie wygenerować klucz SSH i umieścić go w domyślnej lokalizacji klucza ( *~/.ssh* ). 

```azurecli-interactive
az vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

Zwróć uwagę na wartość `publicIpAddress` w danych wyjściowych.

## <a name="assign-an-identity-to-the-vm"></a>Przypisywanie tożsamości do maszyny wirtualnej

Utwórz tożsamość przypisaną do systemu dla maszyny wirtualnej za pomocą polecenia [AZ VM Identity Assign](/cli/azure/vm/identity?view=azure-cli-latest#az-vm-identity-assign) , aby utworzyć identyfikator w systemie Azure:

```azurecli
az vm identity assign --name "myVM" --resource-group "myResourceGroup"
```

Zanotuj tożsamość przypisaną przez system, która jest wyświetlana w poniższym kodzie. Dane wyjściowe poprzedniego polecenia byłyby następujące: 

```output
{
  "systemAssignedIdentity": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "userAssignedIdentities": {}
}
```

## <a name="assign-permissions-to-the-vm-identity"></a>Przypisywanie uprawnień do tożsamości maszyny wirtualnej

Teraz można przypisać wcześniej utworzone uprawnienia tożsamości do magazynu kluczy, uruchamiając następujące polecenie:

```azurecli
az keyvault set-policy --name "<your-unique-keyvault-name>" --object-id "<systemAssignedIdentity>" --secret-permissions get list
```

## <a name="log-in-to-the-vm"></a>Logowanie się do maszyny wirtualnej

Aby zalogować się do maszyny wirtualnej, postępuj zgodnie z instrukcjami podanymi w temacie [łączenie i logowanie do maszyny wirtualnej platformy Azure z systemem Linux](../../virtual-machines/linux/login-using-aad.md) lub łączenie się z [maszyną wirtualną platformy Azure z systemem Windows i logowanie się do](../../virtual-machines/windows/connect-logon.md)niej.


Aby zalogować się do maszyny wirtualnej z systemem Linux, można użyć polecenia SSH z " <publicIpAddress> " podanym w kroku [Tworzenie maszyny wirtualnej](#create-a-virtual-machine) :

```terminal
ssh azureuser@<PublicIpAddress>
```

## <a name="install-python-libraries-on-the-vm"></a>Instalowanie bibliotek języka Python na maszynie wirtualnej

Na maszynie wirtualnej Zainstaluj dwie biblioteki języka Python, które będą używane w naszym skrypcie języka Python: `azure-keyvault-secrets` i `azure.identity` .  

Na maszynie wirtualnej z systemem Linux można na przykład zainstalować następujące polecenia `pip3` :

```bash
pip3 install azure-keyvault-secrets

pip3 install azure.identity
```

## <a name="create-and-edit-the-sample-python-script"></a>Tworzenie i edytowanie przykładowego skryptu w języku Python

Na maszynie wirtualnej Utwórz plik w języku Python o nazwie **Sample.py**. Edytuj plik, aby zawierał następujący kod, zastępując ciąg "<nazwą magazynu kluczy unikatowych>" nazwą magazynu:

```python
from azure.keyvault.secrets import SecretClient
from azure.identity import DefaultAzureCredential

keyVaultName = "<your-unique-keyvault-name>"
KVUri = f"https://{keyVaultName}.vault.azure.net"
secretName = "mySecret"

credential = DefaultAzureCredential()
client = SecretClient(vault_url=KVUri, credential=credential)
retrieved_secret = client.get_secret(secretName)

print(f"The value of secret '{secretName}' in '{keyVaultName}' is: '{retrieved_secret.value}'")
```

## <a name="run-the-sample-python-app"></a>Uruchamianie przykładowej aplikacji w języku Python

Na koniec Uruchom **Sample.py**. Jeśli wszystko zostało utracone, należy zwrócić wartość klucza tajnego:

```bash
python3 sample.py

The value of secret 'mySecret' in '<your-unique-keyvault-name>' is: 'Success!'
```

## <a name="clean-up-resources"></a>Czyszczenie zasobów

Gdy nie są już potrzebne, Usuń maszynę wirtualną i Magazyn kluczy.  Możesz to zrobić szybko, usuwając grupę zasobów, do której należą:

```azurecli
az group delete -g myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

[Interfejsy API REST usługi Azure Key Vault](/rest/api/keyvault/)