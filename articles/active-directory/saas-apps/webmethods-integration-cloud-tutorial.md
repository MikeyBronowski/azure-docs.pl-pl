---
title: 'Samouczek: integracja Azure Active Directory z usługą webMethods Integration Suite | Microsoft Docs'
description: Dowiedz się, jak skonfigurować Logowanie jednokrotne między Azure Active Directory i webMethods Suite integracji.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/15/2019
ms.author: jeedes
ms.openlocfilehash: 52ad0d0356f4d309db89db6527d7fd2d7dec253d
ms.sourcegitcommit: fb3c846de147cc2e3515cd8219d8c84790e3a442
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/27/2020
ms.locfileid: "92636820"
---
# <a name="tutorial-azure-active-directory-integration-with-webmethods-integration-suite"></a>Samouczek: integracja Azure Active Directory z usługą webMethods Integration Suite

W tym samouczku dowiesz się, jak zintegrować pakiet integracyjny webMethods z usługą Azure Active Directory (Azure AD).
Integracja pakietu integracyjnego webMethods z usługą Azure AD zapewnia następujące korzyści:

* Możesz kontrolować usługę Azure AD, która ma dostęp do pakietu integracyjnego webMethods.
* Możesz umożliwić użytkownikom automatyczne logowanie do usługi webMethods Integration Suite (Logowanie jednokrotne) za pomocą swoich kont w usłudze Azure AD.
* Możesz zarządzać swoimi kontami w jednej centralnej lokalizacji — witrynie Azure Portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).
Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z pakietem webMethods Integration Suite, potrzebne są następujące elementy:

* Subskrypcja usługi Azure AD. Jeśli nie masz środowiska usługi Azure AD, możesz w [tym miejscu](https://azure.microsoft.com/pricing/free-trial/)uzyskać miesięczną wersję próbną.
* subskrypcja z włączoną obsługą logowania jednokrotnego w usłudze webMethods

## <a name="scenario-description"></a>Opis scenariusza

W tym samouczku skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD w środowisku testowym.

* Pakiet integracyjny webMethods obsługuje usługę **SP** i **dostawcy tożsamości** zainicjowane przez usługę SSO

* Pakiet integracyjny webMethods obsługuje Inicjowanie obsługi użytkowników **just in Time**

## <a name="adding-webmethods-integration-suite-from-the-gallery"></a>Dodawanie pakietu integracyjnego webMethods z galerii

Aby skonfigurować integrację usługi webMethods Integration Suite z usługą Azure AD, należy dodać pakiet integracyjny webMethods z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać pakiet integracyjny webMethods z galerii, wykonaj następujące czynności:**

1. W witrynie **[Azure Portal](https://portal.azure.com)** w panelu nawigacyjnym po lewej stronie kliknij ikonę usługi **Azure Active Directory** .

    ![Przycisk Azure Active Directory](common/select-azuread.png)

2. Przejdź do grupy **Aplikacje dla przedsiębiorstw** i wybierz opcję **Wszystkie aplikacje** .

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

3. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Przycisk Nowa aplikacja](common/add-new-app.png)

4. W polu wyszukiwania wpisz **webMethods Integration Suite** , wybierz pozycję **webMethods Integration Suite** z panelu wyników, a następnie kliknij przycisk **Dodaj** , aby dodać aplikację.

     ![Pakiet integracyjny webMethods na liście wyników](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD

W tej sekcji należy skonfigurować i przetestować Logowanie jednokrotne usługi Azure AD za pomocą pakietu integracyjnego webMethods w oparciu o użytkownika testowego o nazwie **Britta Simon** .
Aby logowanie jednokrotne działało, należy ustanowić relację linku między użytkownikiem usługi Azure AD i powiązanym użytkownikiem w pakiecie integracyjnym webMethods.

Aby skonfigurować i przetestować Logowanie jednokrotne w usłudze Azure AD za pomocą pakietu integracyjnego webMethods, należy wykonać następujące bloki konstrukcyjne:

1. **[Konfigurowanie logowania jednokrotnego usługi Azure AD](#configure-azure-ad-single-sign-on)** — aby umożliwić użytkownikom korzystanie z tej funkcji.
2. Skonfiguruj Logowanie jednokrotne w usłudze **[webMethods dla pakietu Integration Suite](#configure-webmethods-integration-suite-single-sign-on)** , aby skonfigurować pojedyncze ustawienia Sign-On po stronie aplikacji.
3. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować logowanie jednokrotne usługi Azure AD z użytkownikiem Britta Simon.
4. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić użytkownikowi Britta Simon korzystanie z logowania jednokrotnego usługi Azure AD.
5. **[Utwórz użytkownika testowego usługi webMethods Integration Suite](#create-webmethods-integration-suite-test-user)** , aby uzyskać odpowiednik Britta Simon w pakiecie integracyjnym usługi webMethods, który jest połączony z reprezentacją użytkownika w usłudze Azure AD.
6. **[Testowanie logowania jednokrotnego](#test-single-sign-on)** — aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie logowania jednokrotnego usługi Azure AD

W tej sekcji włączysz logowanie jednokrotne usługi Azure AD w witrynie Azure Portal.

Aby skonfigurować Logowanie jednokrotne usługi Azure AD za pomocą pakietu integracji z usługą webMethods, wykonaj następujące czynności:

1. W [Azure Portal](https://portal.azure.com/)na stronie integracji aplikacji **webMethods pakietu Integration Suite** wybierz pozycję **Logowanie jednokrotne** .

    ![Link do konfigurowania logowania jednokrotnego](common/select-sso.png)

2. W oknie dialogowym **Wybieranie metody logowania jednokrotnego** wybierz tryb **SAML/WS-Fed** , aby włączyć logowanie jednokrotne.

    ![Wybieranie trybu logowania jednokrotnego](common/select-saml-option.png)

3. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** kliknij ikonę **Edytuj** , aby otworzyć okno dialogowe **Podstawowa konfiguracja protokołu SAML** .

    ![Edycja podstawowej konfiguracji protokołu SAML](common/edit-urls.png)

4. Aby skonfigurować **chmurę integracji usługi webMethods** , w sekcji **Podstawowa konfiguracja protokołu SAML** , jeśli chcesz skonfigurować aplikację w trybie inicjalizacji **dostawcy tożsamości** , wykonaj następujące czynności:

    ![Zrzut ekranu przedstawia podstawową konfigurację języka SAML, w której można wprowadzić identyfikator, odpowiedź U R L i wybrać pozycję Zapisz.](common/idp-intiated.png)

    a. W polu tekstowym **Identyfikator** wpisz adres URL, korzystając z następującego wzorca: 

    - `<SUBDOMAIN>.webmethodscloud.com`
    - `<SUBDOMAIN>.webmethodscloud.eu`
    - `<SUBDOMAIN>.webmethodscloud.de`

    b. W polu tekstowym **Adres URL odpowiedzi** wpisz adres URL, korzystając z następującego wzorca: 


    - `https://<SUBDOMAIN>.webmethodscloud.com/integration/live/saml/ssoResponse`
    - `https://<SUBDOMAIN>.webmethodscloud.eu/integration/live/saml/ssoResponse`
    - `https://<SUBDOMAIN>.webmethodscloud.de/integration/live/saml/ssoResponse`

    c. Kliknij pozycję **Ustaw dodatkowe adresy URL** i wykonaj następujące kroki, jeśli chcesz skonfigurować aplikację w trybie inicjowania programu **SP** :

    ![Zrzut ekranu przedstawia ustawienie dodatkowego U R LS, gdzie można wprowadzić znak U R L.](common/metadata-upload-additional-signon.png)

    d. W polu tekstowym **Adres URL logowania** wpisz adres URL, korzystając z następującego wzorca: 

    - `https://<SUBDOMAIN>.webmethodscloud.com/integration/live/saml/ssoRequest`
    - `https://<SUBDOMAIN>.webmethodscloud.eu/integration/live/saml/ssoRequest`
    - `https://<SUBDOMAIN>.webmethodscloud.de/integration/live/saml/ssoRequest`

    > [!NOTE]
    > Te wartości nie są prawdziwe. Należy je zastąpić rzeczywistymi wartościami identyfikatora, adresu URL odpowiedzi i adresu URL logowania. Skontaktuj się z [zespołem pomocy technicznej webMethods Integration Suite](https://empower.softwareag.com/) , aby uzyskać te wartości. Przydatne mogą się również okazać wzorce przedstawione w sekcji **Podstawowa konfiguracja protokołu SAML** w witrynie Azure Portal.

5. Aby skonfigurować **chmurę interfejsu API usługi webMethods** , w sekcji **Podstawowa konfiguracja protokołu SAML** , jeśli chcesz skonfigurować aplikację w trybie inicjowania **dostawcy tożsamości** , wykonaj następujące czynności:

    ![Zrzut ekranu przedstawia podstawową konfigurację języka SAML, w której można wprowadzić identyfikator, odpowiedź U R L i wybrać pozycję Zapisz.](common/idp-intiated.png)

    a. W polu tekstowym **Identyfikator** wpisz adres URL, korzystając z następującego wzorca: 

    - `<SUBDOMAIN>.webmethodscloud.com`
    - `<SUBDOMAIN>.webmethodscloud.eu`
    - `<SUBDOMAIN>.webmethodscloud.de`

    b. W polu tekstowym **Adres URL odpowiedzi** wpisz adres URL, korzystając z następującego wzorca: 

    - `https://<SUBDOMAIN>.webmethodscloud.com/umc/rest/saml/initsso`
    - `https://<SUBDOMAIN>.webmethodscloud.eu/umc/rest/saml/initsso`
    - `https://<SUBDOMAIN>.webmethodscloud.de/umc/rest/saml/initsso`

    c. Kliknij pozycję **Ustaw dodatkowe adresy URL** i wykonaj następujące kroki, jeśli chcesz skonfigurować aplikację w trybie inicjowania programu **SP** :

    ![Zrzut ekranu przedstawia ustawienie dodatkowego U R LS, gdzie można wprowadzić znak U R L.](common/metadata-upload-additional-signon.png)

    d. W polu tekstowym **Adres URL logowania** wpisz adres URL, korzystając z następującego wzorca: 

    - `https://api.webmethodscloud.com/umc/rest/saml/initsso/?tenant=<TENANTID>`
    - `https://api.webmethodscloud.eu/umc/rest/saml/initsso/?tenant=<TENANTID>`
    - `https://api.webmethodscloud.de/umc/rest/saml/initsso/?tenant=<TENANTID>`

    > [!NOTE]
    > Te wartości nie są prawdziwe. Należy je zastąpić rzeczywistymi wartościami identyfikatora, adresu URL odpowiedzi i adresu URL logowania. Skontaktuj się z [zespołem pomocy technicznej webMethods Integration Suite](https://empower.softwareag.com/) , aby uzyskać te wartości. Przydatne mogą się również okazać wzorce przedstawione w sekcji **Podstawowa konfiguracja protokołu SAML** w witrynie Azure Portal.

6. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** w sekcji **Certyfikat podpisywania SAML** kliknij link **Pobierz** , aby pobrać **kod XML metadanych federacji** na podstawie podanych opcji zgodnie z wymaganiami i zapisać go na komputerze.

    ![Link do pobierania certyfikatu](common/metadataxml.png)

7. W sekcji **Konfigurowanie zestawu webMethods Integration Suite** skopiuj odpowiednie adresy URL zgodnie z wymaganiami.

    ![Kopiowanie adresów URL konfiguracji](common/copy-configuration-urls.png)

    a. Adres URL logowania

    b. Identyfikator usługi Azure AD

    c. Adres URL wylogowywania

### <a name="configure-webmethods-integration-suite-single-sign-on"></a>Konfigurowanie jednego Sign-On w usłudze webMethods Integration Suite

Aby skonfigurować Logowanie jednokrotne na stronie **webMethods Integration Suite** , należy wysłać pobrany **kod XML metadanych Federacji** i odpowiednie skopiowane adresy URL z Azure Portal do [zespołu pomocy technicznej pakietu Integration Suite](https://empower.softwareag.com/). Ustawią oni to ustawienie tak, aby połączenie logowania jednokrotnego SAML było ustawione właściwie po obu stronach.

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

W tej sekcji w witrynie Azure Portal utworzysz użytkownika testowego o nazwie Britta Simon.

1. W witrynie Azure Portal w okienku po lewej stronie wybierz pozycję **Azure Active Directory** , wybierz opcję **Użytkownicy** , a następnie wybierz pozycję **Wszyscy użytkownicy** .

    ![Linki „Użytkownicy i grupy” i „Wszyscy użytkownicy”](common/users.png)

2. Wybierz pozycję **nowy użytkownik** w górnej części ekranu.

    ![Przycisk Nowy użytkownik](common/new-user.png)

3. We właściwościach użytkownika wykonaj następujące kroki.

    ![Okno dialogowe Użytkownik](common/user-properties.png)

    a. W polu **Nazwa** wprowadź **BrittaSimon** .
  
    b. W polu **Nazwa użytkownika** wpisz **brittasimon \@ yourcompanydomain. Extension**  
    Na przykład BrittaSimon@contoso.com

    c. Zaznacz pole wyboru **Pokaż hasło** i zanotuj wartość wyświetlaną w polu Hasło.

    d. Kliknij pozycję **Utwórz** .

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

Ta sekcja umożliwia włączenie usługi Britta Simon w celu korzystania z logowania jednokrotnego na platformie Azure przez przyznanie dostępu do pakietu integracyjnego webMethods.

1. W Azure Portal wybierz pozycję **aplikacje dla przedsiębiorstw** , wybierz pozycję **wszystkie aplikacje** , a następnie wybierz pozycję **webMethods Integration Suite** .

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

2. Na liście Aplikacje wybierz pozycję **webMethods Integration Suite** .

    ![Link webMethods Integration Suite na liście aplikacji](common/all-applications.png)

3. W menu po lewej stronie wybierz pozycję **Użytkownicy i grupy** .

    ![Link „Użytkownicy i grupy”](common/users-groups-blade.png)

4. Kliknij przycisk **Dodaj użytkownika** , a następnie wybierz pozycję **Użytkownicy i grupy** w oknie dialogowym **Dodawanie przypisania** .

    ![Okienko Dodawanie przypisania](common/add-assign-user.png)

5. W oknie dialogowym **Użytkownicy i grupy** wybierz pozycję **Britta Simon** na liście Użytkownicy, a następnie kliknij przycisk **Wybierz** w dolnej części ekranu.

6. Jeśli oczekujesz, że masz dowolną wartość roli w potwierdzeniu SAML, w oknie dialogowym **Wybierz rolę** wybierz odpowiednią rolę dla użytkownika z listy, a następnie kliknij przycisk **Wybierz** w dolnej części ekranu.

7. W oknie dialogowym **Dodawanie przypisania** kliknij przycisk **Przypisz** .

### <a name="create-webmethods-integration-suite-test-user"></a>Tworzenie użytkownika testowego dla pakietu Integration Suite

W tej sekcji użytkownik o nazwie Britta Simon jest tworzony w pakiecie webMethods Integration Suite. Pakiet integracyjny webMethods obsługuje funkcję aprowizacji użytkowników just in Time, która jest domyślnie włączona. W tej sekcji nie musisz niczego robić. Jeśli użytkownik nie istnieje jeszcze w pakiecie integracyjnym webMethods, zostanie utworzony nowy po uwierzytelnieniu.

### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego 

W tej sekcji przetestujesz konfigurację logowania jednokrotnego usługi Azure AD przy użyciu panelu dostępu.

Po kliknięciu kafelka pakiet integracyjny usługi webMethods w panelu dostępu należy automatycznie zalogować się do pakietu integracyjnego usługi webMethods, dla którego skonfigurowano Logowanie jednokrotne. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

- [Lista samouczków dotyczących sposobu integrowania aplikacji SaaS z usługą Azure Active Directory](./tutorial-list.md)

- [Czym jest dostęp do aplikacji i logowanie jednokrotne za pomocą usługi Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

- [Co to jest dostęp warunkowy w usłudze Azure Active Directory?](../conditional-access/overview.md)