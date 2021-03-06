---
title: Szybki Start — Dodawanie wywołania do aplikacji systemu iOS przy użyciu usług Azure Communications Services
description: W tym przewodniku szybki start dowiesz się, jak korzystać z biblioteki klienta wywołującego usługę Azure Communications Services dla systemu iOS.
author: matthewrobertson
ms.author: marobert
ms.date: 07/24/2020
ms.topic: quickstart
ms.service: azure-communication-services
ms.openlocfilehash: 36ec27f3a0e69126a91b52bed26dc645ec89e46e
ms.sourcegitcommit: b4647f06c0953435af3cb24baaf6d15a5a761a9c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2021
ms.locfileid: "101656651"
---
W tym przewodniku szybki start dowiesz się, jak rozpocząć wywoływanie przy użyciu biblioteki klienta wywołującej usługi Azure Communications Services dla systemu iOS.

> [!NOTE]
> Ten dokument używa wersji 1.0.0-beta. 8 z wywołującej biblioteki klienta.

## <a name="prerequisites"></a>Wymagania wstępne

Do ukończenia tego samouczka potrzebne są następujące wymagania wstępne:

- Konto platformy Azure z aktywną subskrypcją. [Utwórz konto bezpłatnie](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). 
- Na komputerze Mac z systemem [Xcode](https://go.microsoft.com/fwLink/p/?LinkID=266532), wraz z prawidłowym certyfikatem dewelopera zainstalowanym w łańcuchu kluczy.
- Wdrożony zasób usług komunikacyjnych. [Utwórz zasób usług komunikacyjnych](../../create-communication-resource.md).
- [Token dostępu użytkownika](../../access-tokens.md) dla usługi komunikacyjnej platformy Azure.

## <a name="setting-up"></a>Konfigurowanie

### <a name="creating-the-xcode-project"></a>Tworzenie projektu Xcode

W Xcode Utwórz nowy projekt dla systemu iOS i wybierz szablon **aplikacji pojedynczego widoku** . W tym samouczku jest stosowana [Struktura SwiftUI](https://developer.apple.com/xcode/swiftui/), więc należy ustawić **Język** **SWIFT** i **interfejs użytkownika** na **SwiftUI**. Nie zamierzasz tworzyć testów podczas tego przewodnika Szybki Start. Możesz usunąć zaznaczenie opcji **Dołącz testy**.

:::image type="content" source="../media/ios/xcode-new-ios-project.png" alt-text="Zrzut ekranu przedstawiający okno nowy projekt w Xcode.":::

### <a name="install-the-package-and-dependencies-with-cocoapods"></a>Instalowanie pakietu i zależności za pomocą CocoaPods

1. Utwórz plik podfile dla aplikacji, tak jak to:

   ```
   platform :ios, '13.0'
   use_frameworks!

   target 'AzureCommunicationCallingSample' do
     pod 'AzureCommunicationCalling', '~> 1.0.0-beta.8'
     pod 'AzureCommunication', '~> 1.0.0-beta.8'
     pod 'AzureCore', '~> 1.0.0-beta.8'
   end
   ```

2. Uruchom polecenie `pod install`.
3. Otwórz `.xcworkspace` program with Xcode.

### <a name="request-access-to-the-microphone"></a>Zażądaj dostępu do mikrofonu

Aby można było uzyskać dostęp do mikrofonu urządzenia, należy zaktualizować listę właściwości informacji aplikacji za pomocą `NSMicrophoneUsageDescription` . Należy ustawić skojarzoną wartość `string` , która zostanie uwzględniona w oknie dialogowym, którego system używa do żądania dostępu od użytkownika.

Kliknij prawym przyciskiem myszy `Info.plist` wpis drzewa projektu i wybierz polecenie **Otwórz jako**  >  **kod źródłowy**. Dodaj następujące wiersze w sekcji najwyższego poziomu `<dict>` , a następnie Zapisz plik.

```xml
<key>NSMicrophoneUsageDescription</key>
<string>Need microphone access for VOIP calling.</string>
```

### <a name="set-up-the-app-framework"></a>Konfigurowanie struktury aplikacji

Otwórz plik **contentView. Swift** projektu i Dodaj `import` deklarację na początku pliku w celu zaimportowania `AzureCommunicationCalling library` . Ponadto `AVFoundation` należy zaimportować ten kod do żądania uprawnień audio w kodzie.

```swift
import AzureCommunicationCalling
import AVFoundation
```

Zastąp implementację `ContentView` struktury niektórymi prostymi kontrolkami interfejsu użytkownika, które umożliwiają użytkownikowi zainicjowanie i zakończenie wywołania. W tym przewodniku szybki start dołączymy logikę biznesową do tych kontrolek.

```swift
struct ContentView: View {
    @State var callee: String = ""
    @State var callClient: CallClient?
    @State var callAgent: CallAgent?
    @State var call: Call?

    var body: some View {
        NavigationView {
            Form {
                Section {
                    TextField("Who would you like to call?", text: $callee)
                    Button(action: startCall) {
                        Text("Start Call")
                    }.disabled(callAgent == nil)
                    Button(action: endCall) {
                        Text("End Call")
                    }.disabled(call == nil)
                }
            }
            .navigationBarTitle("Calling Quickstart")
        }.onAppear {
            // Initialize call agent
        }
    }

    func startCall() {
        // Ask permissions
        AVAudioSession.sharedInstance().requestRecordPermission { (granted) in
            if granted {
                // Add start call logic
            }
        }
    }

    func endCall() {
        // Add end call logic
    }
}
```

## <a name="object-model"></a>Model obiektów

Następujące klasy i interfejsy obsługują niektóre główne funkcje biblioteki klienta wywołującego usługi Azure Communications Services:

| Nazwa                                  | Opis                                                  |
| ------------------------------------- | ------------------------------------------------------------ |
| CallClient | CallClient jest głównym punktem wejścia do biblioteki wywołującej klienta.|
| CallAgent | CallAgent jest używany do uruchamiania wywołań i zarządzania nimi. |
| CommunicationTokenCredential | CommunicationTokenCredential jest używany jako poświadczenia tokenu do tworzenia wystąpienia CallAgent.| 
| CommunicationUserIdentifier | CommunicationUserIdentifier jest używany do reprezentowania tożsamości użytkownika, który może być jedną z następujących: CommunicationUserIdentifier/PhoneNumberIdentifier/CallingApplication. |

## <a name="authenticate-the-client"></a>Uwierzytelnianie klienta

Zainicjuj `CallAgent` wystąpienie z tokenem dostępu użytkownika, które umożliwi nam nawiązywanie i odbieranie wywołań. Dodaj następujący kod do `onAppear` wywołania zwrotnego w **contentView. Swift**:

```swift
var userCredential: CommunicationTokenCredential?
do {
    userCredential = try CommunicationTokenCredential(token: "<USER ACCESS TOKEN>")
} catch {
    print("ERROR: It was not possible to create user credential.")
    return
}

self.callClient = CallClient()

// Creates the call agent
self.callClient?.createCallAgent(userCredential: userCredential) { (agent, error) in
    if error != nil {
        print("ERROR: It was not possible to create a call agent.")
        return
    }

    if let agent = agent {
        self.callAgent = agent
        print("Call agent successfully created.")
    }
}
```

Należy zastąpić `<USER ACCESS TOKEN>` prawidłowym tokenem dostępu użytkownika dla zasobu. Jeśli nie masz jeszcze dostępnego tokenu, zapoznaj się z dokumentacją [tokenu dostępu użytkownika](../../access-tokens.md) .

## <a name="start-a-call"></a>Rozpocznij wywołanie

`startCall`Metoda jest ustawiana jako akcja, która będzie wykonywana po naciśnięciu przycisku *Rozpocznij połączenie* . Zaktualizuj implementację, aby rozpocząć wywoływanie przy użyciu `ASACallAgent` :

```swift
func startCall()
{
    // Ask permissions
    AVAudioSession.sharedInstance().requestRecordPermission { (granted) in
        if granted {
            // start call logic
            let callees:[CommunicationIdentifier] = [CommunicationUserIdentifier(identifier: self.callee)]
            self.call = self.callAgent?.call(participants: callees, options: StartCallOptions())
        }
    }
}
```

Można również użyć właściwości w, `StartCallOptions` Aby ustawić początkowe opcje wywołania (tj. umożliwia uruchomienie wywołania z mikrofonu wyciszonego).

## <a name="end-a-call"></a>Zakończenie wywołania

Zaimplementuj `endCall` metodę, aby zakończyć bieżące wywołanie, gdy zostanie naciśnięty przycisk *Zakończ połączenie* .

```swift
func endCall()
{    
    self.call!.hangup(HangupOptions()) { (error) in
        if (error != nil) {
            print("ERROR: It was not possible to hangup the call.")
        }
    }
}
```

## <a name="run-the-code"></a>Uruchamianie kodu

Możesz skompilować i uruchomić aplikację w symulatorze systemu iOS, wybierając opcję  >  **Uruchom** produkt lub używając skrótu klawiaturowego (&#8984;-R).

:::image type="content" source="../media/ios/quick-start-make-call.png" alt-text="Końcowy wygląd i działanie aplikacji szybkiego startu":::

Wychodzące wywołanie VOIP można utworzyć, podając identyfikator użytkownika w polu tekstowym i naciskając przycisk **Rozpocznij połączenie** . Wywołanie `8:echo123` nawiązuje połączenie z botem ECHA. jest to doskonałe rozwiązanie do rozpoczęcia i sprawdzenia, czy urządzenia audio działają. 

> [!NOTE]
> Podczas pierwszego wywołania system wyświetli monit o uzyskanie dostępu do mikrofonu. W aplikacji produkcyjnej należy użyć `AVAudioSession` interfejsu API, aby [sprawdzić stan uprawnień](https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/requesting_access_to_protected_resources) i bezpiecznie aktualizować zachowanie aplikacji po udzieleniu uprawnienia.

## <a name="sample-code"></a>Przykładowy kod

Możesz pobrać przykładową aplikację z usługi [GitHub](https://github.com/Azure-Samples/communication-services-ios-quickstarts/tree/main/Add%20Voice%20Calling)
