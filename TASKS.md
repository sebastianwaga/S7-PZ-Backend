# Zadania projektu — GitHub Issues

Każda sekcja jest osobnym Issue. Użyj jej nagłówka jako tytułu, a celu i kryteriów odbioru jako opisu. Przy tworzeniu Issue ustaw wskazane pola Assignee, Labels i Milestone; samo wklejenie metadanych do opisu ich nie ustawia.

Identyfikatory ORG-01, API-01 itd. są robocze. Po utworzeniu Issues zastąp zależności odnośnikami do rzeczywistych numerów, np. #23. Każde zadanie realizuj na wskazanym branchu, a PR powiąż przez Closes #numer. Po poprawnym CI i review pozostałych dwóch osób wykonaj squash merge. Pośrednie PR-y mogą używać Refs #numer.

Milestones: M1 — pierwszy przepływ z trasą samochodową; M2 — pełna edycja i pozostałe transporty; M3 — historia, kraje i statystyki; M4 — testy całości, wdrożenie i oddanie. Testy i dokumentacja powstają również na bieżąco przy implementacji.

Estymaty to orientacyjne przedziały godzin aktywnej pracy przy podstawowej znajomości wybranego stosu technologicznego i dostępnych zależnościach. Obejmują realizację zadania, własną weryfikację i przygotowanie PR; nie obejmują oczekiwania na review. Przenieś estymatę do Issue i po zakończeniu dopisz rzeczywisty czas. Jeśli zakres przekroczy około 1–2 dni pracy, podziel zadanie na mniejsze Issues.

Opis projektu: [README.md](README.md).

---

## [ORG-01] Utworzyć repozytorium i ustawić GitHub flow

- **Assignee:** sebastianwaga
- **Labels:** organizacja
- **Milestone:** M1
- **Estymata:** 1–3 h
- **Branch:** chore/org-01-repository
- **Zależności:** brak

### Cel

Przygotować publiczne repozytoria oraz uzgodniony sposób pracy całego zespołu.

### Kryteria odbioru

- [ ] Repozytoria S7-PZ-Backend (ze strukturą backendu, docs/ i infra/) oraz S7-PZ-Mobile mają pliki README oraz dostęp dla wszystkich członków zespołu.
- [ ] Zmiany na main przechodzą przez pull requesty i review pozostałych członków zespołu zgodnie z zasadami zajęć; konfiguracja ochrony gałęzi to egzekwuje w zakresie dostępnym w GitHub.
- [ ] Przyjęto squash merge, powiązanie PR z numerem Issue oraz krótkie branche tworzone z aktualnego main.
- [ ] Po uruchomieniu ORG-04 wymagane kontrole CI są podłączone do reguł scalania.

---

## [ORG-02] Przygotować lokalne środowisko backendu

- **Assignee:** SX2V
- **Labels:** infrastruktura, backend
- **Milestone:** M1
- **Estymata:** 3–6 h
- **Branch:** chore/org-02-backend-environment
- **Zależności:** ORG-01

### Cel

Zapewnić powtarzalne uruchomienie Django REST Framework i PostgreSQL.

### Kryteria odbioru

- [ ] Docker Compose uruchamia backend i PostgreSQL, a migracje można wykonać według README.
- [ ] Plik .env.example opisuje wymagane zmienne bez prawdziwych sekretów; baza korzysta z trwałego wolumenu.
- [ ] Endpoint kontrolny pozwala sprawdzić połączenie aplikacji mobilnej z działającym API.
- [ ] Nowa osoba może uruchomić środowisko na podstawie instrukcji w repozytorium.

---

## [ORG-03] Utworzyć szkielet aplikacji Flutter

- **Assignee:** sebastianwaga
- **Labels:** mobile
- **Milestone:** M1
- **Estymata:** 3–6 h
- **Branch:** chore/org-03-flutter-setup
- **Zależności:** ORG-01

### Cel

Rozpocząć mobilkę wcześnie i sprawdzić podstawową komunikację z backendem.

### Kryteria odbioru

- [ ] Projekt Flutter uruchamia się na wybranym emulatorze lub urządzeniu z Androidem.
- [ ] Istnieje nawigacja pomiędzy ekranami startowymi i konfiguracja adresu API dla środowiska deweloperskiego.
- [ ] Aplikacja potrafi wyświetlić odpowiedź endpointu kontrolnego; do czasu dostępności backendu dopuszczone są dane przykładowe.
- [ ] Instrukcja opisuje uruchomienie Fluttera oraz adres backendu używany na emulatorze i urządzeniu.

---

## [ORG-04] Uruchomić GitHub Actions

- **Assignee:** sebastianwaga
- **Labels:** infrastruktura, testy
- **Milestone:** M1
- **Estymata:** 3–5 h
- **Branch:** ci/org-04-workflows
- **Zależności:** ORG-02, ORG-03

### Cel

Automatycznie weryfikować zmiany przed scaleniem do main.

### Kryteria odbioru

- [ ] PR uruchamia Ruff i pytest dla backendu oraz flutter analyze i flutter test dla mobilki.
- [ ] Backendowe testy korzystające z bazy mają dostępną testową instancję PostgreSQL.
- [ ] Istnieją podstawowe testy uruchomienia aplikacji; celowo błędna zmiana powoduje niepowodzenie odpowiedniej kontroli.
- [ ] Wyniki są widoczne przy PR, a nazwy kontroli są wykorzystane w zasadach scalania.

---

## [ORG-05] Zaprojektować podstawowe ekrany

- **Assignee:** adamrudziewicz
- **Labels:** projektowanie, mobile
- **Milestone:** M1
- **Estymata:** 4–8 h
- **Branch:** docs/org-05-mockups
- **Zależności:** ORG-01

### Cel

Uzgodnić prosty interfejs potrzebny do realizacji wymaganych funkcji.

### Kryteria odbioru

- [ ] Makiety obejmują konto, profil, listę podróży, edytor punktów i odcinków, mapę, statystyki i publiczne profile.
- [ ] Pokazano przejścia pomiędzy ekranami oraz warianty ładowania, pustej listy i błędu.
- [ ] Edytor umożliwia powrót do wcześniej odwiedzonego miejsca i ustawienie innego transportu na każdym odcinku.
- [ ] Makiety lub odnośnik do nich są dostępne w repozytorium i zostały omówione przez zespół.

---

## [ORG-06] Ustalić reguły podróży, krajów i statystyk

- **Assignee:** adamrudziewicz
- **Labels:** organizacja, dokumentacja
- **Milestone:** M1
- **Estymata:** 2–4 h
- **Branch:** docs/org-06-domain-rules
- **Zależności:** ORG-01

### Cel

Zapisać jednoznaczne definicje stosowane w modelu danych, API i mobilce. Adam zapisuje ustalenia podjęte przez cały zespół; definicje nie są podejmowane jednostronnie.

### Kryteria odbioru

- [ ] Ustalono, co jest podróżą odbytą, jakie daty są wymagane oraz jak obsługiwane są podróże bez pełnej listy punktów.
- [ ] Ustalono sposób przypisania podróży na przełomie lat do statystyk rocznych; reguła ma przykład z datami grudzień/styczeń.
- [ ] Ustalono definicję unikalnego miejsca i odwiedzonego kraju; propozycja startowa to kraje zapisanych postojów, bez krajów jedynie przelatywanych.
- [ ] Opisano metody liczenia dystansu dla transportów i zasady prywatności; decyzje zapisano w docs/.

---

## [API-01] Zaprojektować domenę oraz modele profilu i podróży

- **Assignee:** SX2V
- **Labels:** backend
- **Milestone:** M1
- **Estymata:** 5–8 h
- **Branch:** feat/api-01-domain-model
- **Zależności:** ORG-02, ORG-06

### Cel

Uzgodnić cały model domenowy i wdrożyć bazowe modele profilu oraz podróży.

### Kryteria odbioru

- [ ] Diagram opisuje profil, podróż, uporządkowane punkty i odcinki, w tym transport, geometrię, dystans i sposób jego obliczenia.
- [ ] Modele profilu i podróży wraz z migracjami obsługują właściciela, widoczność, nazwę, daty i opcjonalny opis.
- [ ] Implementacja modelu punktu należy do API-05a, a modelu odcinka do API-05b; nie powstają dwie konkurencyjne migracje tych samych pól.
- [ ] Projekt uwzględnia powrót do tego samego miejsca, identyfikację unikalnych miejsc oraz reguły ORG-06.

---

## [API-02] Zaimplementować rejestrację i sesję użytkownika

- **Assignee:** SX2V
- **Labels:** backend
- **Milestone:** M1
- **Estymata:** 6–10 h
- **Branch:** feat/api-02-authentication
- **Zależności:** API-01

### Cel

Udostępnić rejestrację, logowanie, odświeżanie sesji i wylogowanie.

### Kryteria odbioru

- [ ] Rejestracja waliduje wymagane dane i unikalność identyfikatora konta; hasła są haszowane przez mechanizmy Django.
- [ ] Poprawne logowanie wydaje tokeny, a niepoprawne dane zwracają uzgodniony błąd bez ujawniania danych konta.
- [ ] Odświeżanie sesji działa; wylogowanie unieważnia token odświeżający zgodnie z wybraną konfiguracją, a czas ważności tokenu dostępu jest opisany.
- [ ] Dodano testy poprawnej i błędnej rejestracji, logowania, odświeżania oraz wylogowania.

---

## [API-03] Zaimplementować profil i jego widoczność

- **Assignee:** adamrudziewicz
- **Labels:** backend
- **Milestone:** M2
- **Estymata:** 3–5 h
- **Branch:** feat/api-03-profile
- **Zależności:** API-02

### Cel

Pozwolić użytkownikowi pobierać i zmieniać własny profil.

### Kryteria odbioru

- [ ] Endpoint zwraca uzgodnione podstawowe dane i pozwala je edytować z walidacją pól.
- [ ] Można zmienić widoczność publiczny/prywatny, a zmiana jest trwale zapisana.
- [ ] Własny profil jest dostępny właścicielowi; dane wewnętrzne i sekrety nie trafiają do publicznej reprezentacji.

---

## [API-04] Zaimplementować CRUD własnych podróży

- **Assignee:** SX2V
- **Labels:** backend
- **Milestone:** M1
- **Estymata:** 4–7 h
- **Branch:** feat/api-04-trips-crud
- **Zależności:** API-02

### Cel

Udostępnić listę, tworzenie, szczegóły, edycję i usuwanie podróży.

### Kryteria odbioru

- [ ] Podróż można zapisać z nazwą, datą lub zakresem dat oraz opcjonalnym opisem; daty są walidowane.
- [ ] Właściciel może zmienić i usunąć swoją podróż; usunięcie obejmuje powiązane punkty i odcinki.
- [ ] Lista ma paginację i przewidywalne sortowanie, a użytkownik otrzymuje tylko dozwolone dane.
- [ ] Testy sprawdzają podstawowy CRUD oraz odrzucenie próby zmiany cudzej podróży.

---

## [API-05a] Modele i endpointy zapisu oraz odczytu listy punktów

- **Assignee:** SX2V
- **Labels:** backend
- **Milestone:** M1
- **Estymata:** 4–6 h
- **Branch:** feat/api-05a-trip-points
- **Zależności:** API-01, API-04

### Cel

Zaimplementować model punktu i podstawowe API jego listy zgodnie z projektem domeny.

### Kryteria odbioru

- [ ] Model punktu i migracja obejmują podróż, kolejność, nazwę, współrzędne oraz dostępne identyfikator miejsca i kod kraju.
- [ ] Działa odczyt i bazowy zapis listy punktów własnej podróży; odpowiedź zachowuje kolejność.
- [ ] API waliduje współrzędne i przynależność punktów oraz dopuszcza powrót do wcześniej odwiedzonego miejsca.
- [ ] Przebudowa odcinków i zmiana kolejności pełnej podróży pozostają w API-05b; udokumentowano granicę obu zadań.

---

## [API-05b] Zmiana kolejności i atomowe tworzenie odcinków

- **Assignee:** SX2V
- **Labels:** backend
- **Milestone:** M1
- **Estymata:** 6–10 h
- **Branch:** feat/api-05b-trip-segments
- **Zależności:** API-05a

### Cel

Zaimplementować finalny atomowy zapis punktów i transportów wraz z modelem kolejnych odcinków.

### Kryteria odbioru

- [ ] Dla N punktów, gdy N jest co najmniej 1, powstaje N−1 odcinków między kolejnymi punktami; każdy ma własny transport.
- [ ] Dodanie, usunięcie lub zmiana kolejności aktualizuje strukturę odcinków i stosuje uzgodnioną regułę zachowania transportu.
- [ ] Walidacja własności i transakcja chronią przed częściowym zapisem albo użyciem punktu z cudzej podróży.
- [ ] Nowy lub zmieniony odcinek jest oznaczony jako wymagający obliczenia; stara geometria nie jest prezentowana jako aktualna. Geometrie i dystanse obliczają API-07/API-08, a pełne przeliczenia po edycji domyka API-09.

---

## [API-06] Podłączyć wyszukiwanie miejsc i geokodowanie

- **Assignee:** SX2V
- **Labels:** backend, mapy
- **Milestone:** M1
- **Estymata:** 4–6 h
- **Branch:** feat/api-06-geocoding
- **Zależności:** API-01

### Cel

Udostępnić wyszukiwanie miejsc przez MapTiler i normalizację odpowiedzi dostawcy.

### Kryteria odbioru

- [ ] Zapytanie zwraca nazwę, współrzędne i rozpoznany kraj oraz identyfikator miejsca, jeżeli dostawca go zwraca.
- [ ] Do podróży można zapisać wynik wyszukiwania, a dla punktu wskazanego na mapie można rozpoznać kraj.
- [ ] Brak wyników, brak rozpoznanego kraju i błąd dostawcy są odrębnymi, poprawnie obsłużonymi stanami.
- [ ] Klucz serwerowy jest konfigurowany poza repozytorium; integracja uwzględnia limity i warunki użycia dostawcy.

---

## [API-07] Wyznaczać i zapisywać trasy samochodowe

- **Assignee:** SX2V
- **Labels:** backend, mapy
- **Milestone:** M1
- **Estymata:** 6–10 h
- **Branch:** feat/api-07-car-routing
- **Zależności:** API-05b

### Cel

Pobrać z openrouteservice wiarygodny przebieg drogi i jej długość.

### Kryteria odbioru

- [ ] Dla odcinka samochodowego zapisywane są geometria, dystans w metrach oraz źródło obliczenia.
- [ ] Odczyt zapisanej podróży korzysta z bazy i nie wyznacza tej samej trasy ponownie.
- [ ] Timeout, limit, brak drogi i błąd dostawcy zwracają czytelny stan z możliwością ponowienia; linia prosta nie jest oznaczana jako poprawna trasa samochodowa.
- [ ] Test integracji używa kontrolowanej odpowiedzi dostawcy; wykonano również ręczne sprawdzenie rzeczywistego odcinka, np. Legnica–Berlin.

---

## [API-08] Obsłużyć samolot, pociąg i transport inny

- **Assignee:** sebastianwaga
- **Labels:** backend, mapy
- **Milestone:** M2
- **Estymata:** 6–10 h
- **Branch:** feat/api-08-transport-geometries
- **Zależności:** API-05b

### Cel

Generować uproszczone geometrie i zapisane dystanse pozostałych odcinków.

### Kryteria odbioru

- [ ] Odcinek lotniczy ma geometrię pozwalającą pokazać łuk; dystans jest liczony geodezyjnie między punktami.
- [ ] Pociąg i transport inny mają uproszczone połączenia oraz uzgodnioną metodę przybliżenia dystansu.
- [ ] Sposób liczenia dystansu jest zapisany przy odcinku; wynik nie zależy od powiększenia ani dekoracyjnego wygięcia linii.
- [ ] Sprawdzono odcinek o zerowym dystansie i długi lot; renderowanie nie tworzy przypadkowych linii przez całą mapę przy przekroczeniu południka 180°.

---

## [API-09] Aktualizować geometrie i dystanse po edycji

- **Assignee:** SX2V
- **Labels:** backend, mapy
- **Milestone:** M2
- **Estymata:** 8–12 h
- **Branch:** feat/api-09-route-recalculation
- **Zależności:** API-05b, API-07, API-08

### Cel

Zapewnić, że edycja podróży nie pozostawia danych poprzedniego przebiegu.

### Kryteria odbioru

- [ ] Przeniesienie, usunięcie, dodanie i przestawienie punktu aktualizuje właściwe odcinki.
- [ ] Zmiana transportu wybiera właściwą metodę geometrii i dystansu, a nieaktualne wyniki są unieważniane.
- [ ] Awaria przeliczenia jest widoczna i nie daje statystyk udających poprawnie obliczony nowy przebieg.
- [ ] Testy obejmują powrót do tego samego miejsca oraz zapis bez zmiany punktów, który nie odpytuje routingu ponownie.

---

## [API-10] Udostępnić mapę wszystkich podróży i kraje

- **Assignee:** sebastianwaga
- **Labels:** backend, mapy
- **Milestone:** M3
- **Estymata:** 4–7 h
- **Branch:** feat/api-10-travel-history-map
- **Zależności:** API-06, API-09

### Cel

Dostarczyć dane mapy zbiorczej i identyfikatory państw do wyróżnienia.

### Kryteria odbioru

- [ ] API zwraca dozwolone punkty i zapisane geometrie podróży dla całej historii oraz wybranego roku.
- [ ] Lista odwiedzonych państw jest unikalna i zgodna z regułami ORG-06; brak rozpoznanego kraju nie psuje odpowiedzi.
- [ ] Przygotowano źródło poligonów granic i mapowanie jego identyfikatorów na kody krajów, np. dane Natural Earth do wizualizacji.
- [ ] Brak podróży daje poprawną pustą odpowiedź; odczyt danych nie uruchamia routingu.

---

## [API-11] Obliczać statystyki całej historii i wybranego roku

- **Assignee:** SX2V
- **Labels:** backend
- **Milestone:** M3
- **Estymata:** 6–10 h
- **Branch:** feat/api-11-travel-statistics
- **Zależności:** ORG-06, API-06, API-09

### Cel

Udostępnić spójne zestawienie wszystkich statystyk wymaganych w projekcie.

### Kryteria odbioru

- [ ] Odpowiedź zawiera liczbę podróży, odwiedzonych państw i miejsc, listę państw, dystans łączny oraz dystans według transportu.
- [ ] Cała historia i wybrany rok stosują te same definicje; podróż przez koniec roku jest rozliczana zgodnie z ORG-06.
- [ ] Suma dystansów transportów odpowiada sumie całkowitej; wartości bazowe są w metrach, a zaokrąglenia służą prezentacji.
- [ ] Dodanie, edycja i usunięcie podróży aktualizuje wyniki; sprawdzono pustą historię, powtarzające się kraje i miejsca.

---

## [API-12] Udostępnić publiczne profile i ich podróże

- **Assignee:** SX2V
- **Labels:** backend
- **Milestone:** M3
- **Estymata:** 4–7 h
- **Branch:** feat/api-12-public-profiles
- **Zależności:** API-03, API-04

### Cel

Pozwolić przeglądać cudze podróże z zachowaniem prywatności i własności danych.

### Kryteria odbioru

- [ ] Można znaleźć lub otworzyć publiczny profil i przeglądać jego publicznie dostępne podróże.
- [ ] Cudze prywatne dane są blokowane w szczegółach, listach, mapach i statystykach; sprawdzenie obejmuje bezpośrednie żądania z podmienionym ID.
- [ ] Zmiana profilu na prywatny blokuje następne niedozwolone odczyty, również przy stosowaniu cache.
- [ ] Publiczny odczyt nie daje prawa edycji, usuwania ani zarządzania cudzymi punktami i odcinkami.

---

## [API-13] Skonfigurować Django Admin

- **Assignee:** SX2V
- **Labels:** backend
- **Milestone:** M2
- **Estymata:** 4–7 h
- **Branch:** feat/api-13-admin-panel
- **Zależności:** API-03, API-09

### Cel

Dostarczyć wymagany webowy panel administracyjny do zarządzania danymi.

### Kryteria odbioru

- [ ] Administrator zarządza profilami, podróżami, punktami i odcinkami w zakresie przyjętym dla projektu.
- [ ] Działają wyszukiwanie, filtry i czytelne powiązania użytkownik–podróż–punkty–odcinki.
- [ ] Pola wyliczane są tylko do odczytu albo ich edycja wywołuje tę samą walidację i przeliczenia co API.
- [ ] Zwykły użytkownik nie ma dostępu do panelu; instrukcja opisuje utworzenie konta administratora.

---

## [API-14] Udostępnić kontrakt OpenAPI i Swagger UI

- **Assignee:** SX2V
- **Labels:** backend, dokumentacja
- **Milestone:** M1
- **Estymata:** 3–6 h
- **Branch:** docs/api-14-openapi
- **Zależności:** API-01

### Cel

Uruchomić drf-spectacular wcześnie i utrzymywać dokumentację razem z API.

### Kryteria odbioru

- [ ] Schemat OpenAPI i Swagger UI są dostępne lokalnie pod opisanymi adresami; uzgodniono format błędów i jednostki.
- [ ] Dokumentacja opisuje autoryzację, daty, parametry i filtry oraz przykładowe żądania i odpowiedzi.
- [ ] Każdy kolejny PR zmieniający API aktualizuje schemat i przykłady; schema może być walidowana w CI.
- [ ] Po wdrożeniu dokumentacja jest dostępna przy zdalnej aplikacji, co zostaje sprawdzone w FIN-04.

---

## [APP-01] Przygotować klienta API i obsługę sesji

- **Assignee:** sebastianwaga
- **Labels:** mobile
- **Milestone:** M1
- **Estymata:** 6–10 h
- **Branch:** feat/app-01-api-client
- **Zależności:** ORG-03, API-14

### Cel

Utworzyć wspólną warstwę komunikacji Dio i zarządzania stanem w Riverpod.

### Kryteria odbioru

- [ ] Adres API zależy od środowiska, żądania mają wspólną obsługę błędów i timeoutów.
- [ ] Tokeny są przechowywane w bezpiecznym magazynie urządzenia, a żądania dodają wymagane uwierzytelnienie.
- [ ] Działa odświeżenie sesji; jego niepowodzenie prowadzi do ponownego logowania bez zapętlenia żądań.
- [ ] Warstwę można sprawdzić na danych przykładowych zgodnych z kontraktem; integracja sesji jest weryfikowana po API-02.

---

## [APP-02] Zbudować ekrany rejestracji i logowania

- **Assignee:** adamrudziewicz
- **Labels:** mobile
- **Milestone:** M1
- **Estymata:** 5–8 h
- **Branch:** feat/app-02-auth-screens
- **Zależności:** APP-01, API-02

### Cel

Udostępnić pełny cykl konta z poziomu aplikacji.

### Kryteria odbioru

- [ ] Działają formularze rejestracji i logowania z czytelną walidacją oraz błędami API.
- [ ] Po poprawnym logowaniu użytkownik trafia do swoich podróży, a sesja jest przywracana po ponownym uruchomieniu.
- [ ] Wylogowanie usuwa lokalną sesję, wywołuje właściwą operację API i czyści stan danych poprzedniego konta.
- [ ] Ładowanie blokuje przypadkowe wielokrotne wysłanie formularza.

---

## [APP-03] Zbudować ekran edycji profilu

- **Assignee:** adamrudziewicz
- **Labels:** mobile
- **Milestone:** M2
- **Estymata:** 3–5 h
- **Branch:** feat/app-03-profile-screen
- **Zależności:** APP-02, API-03

### Cel

Pozwolić zmieniać dane profilu i jego widoczność.

### Kryteria odbioru

- [ ] Ekran pobiera bieżące dane, pozwala je edytować i pokazuje wynik zapisu.
- [ ] Przełącznik publiczny/prywatny zapisuje stan w API i prezentuje go po ponownym otwarciu aplikacji.
- [ ] Nieudany zapis nie jest prezentowany jako sukces; błędy pól można poprawić bez utraty całego formularza.

---

## [APP-04] Zbudować listę i formularz podróży

- **Assignee:** adamrudziewicz
- **Labels:** mobile
- **Milestone:** M1
- **Estymata:** 6–10 h
- **Branch:** feat/app-04-trip-screens
- **Zależności:** APP-02, API-04, ORG-05

### Cel

Udostępnić zarządzanie podstawowymi danymi własnych podróży.

### Kryteria odbioru

- [ ] Lista pokazuje nazwę i daty, obsługuje kolejne strony oraz otwarcie szczegółów.
- [ ] Można dodać i edytować nazwę, pojedynczą datę lub zakres dat oraz opcjonalny opis zgodnie z regułami API.
- [ ] Usunięcie wymaga świadomego potwierdzenia i odświeża listę po sukcesie.
- [ ] Pusta lista zachęca do utworzenia pierwszej podróży; nieudany zapis zachowuje wpisane dane.

---

## [APP-05] Dodać wyszukiwanie i wybór miejsca

- **Assignee:** sebastianwaga
- **Labels:** mobile, mapy
- **Milestone:** M1
- **Estymata:** 4–7 h
- **Branch:** feat/app-05-place-picker
- **Zależności:** APP-01, API-06

### Cel

Pozwolić wybrać punkt przez wyszukanie miejsca lub wskazanie go na mapie.

### Kryteria odbioru

- [ ] Wyniki wyszukiwania można rozróżnić po nazwie i położeniu, a wybór przekazuje współrzędne i identyfikator do edytora.
- [ ] Użytkownik może wskazać punkt na mapie i potwierdzić lokalizację; kraj jest rozpoznawany przez API, jeśli to możliwe.
- [ ] Zapytania nie są wysyłane bez ograniczeń przy każdym znaku; starszy wynik nie nadpisuje nowszego.
- [ ] Brak wyników, brak połączenia i błąd dostawcy mają czytelne komunikaty.

---

## [APP-06a] Lista punktów, dodawanie, usuwanie i transport

- **Assignee:** sebastianwaga
- **Labels:** mobile
- **Milestone:** M1
- **Estymata:** 6–10 h
- **Branch:** feat/app-06a-points-editor
- **Zależności:** APP-04, APP-05, API-05b, API-07

### Cel

Zbudować podstawowy edytor potrzebny do pierwszej podróży dodawanej w całości z Fluttera.

### Kryteria odbioru

- [ ] Użytkownik widzi listę punktów, dodaje i usuwa miejsca oraz wybiera transport dla kolejnych odcinków.
- [ ] Działa zapis przez API-05b i ponowny odczyt kolejności oraz transportów; błędny zapis zachowuje lokalny formularz.
- [ ] W M1 można wskazać dwa punkty, wybrać samochód, wyznaczyć i zapisać trasę przez API-07 oraz otworzyć ją na mapie.
- [ ] Przeciąganie nie jest wymagane w tym zadaniu; inne transporty korzystają z obliczeń po API-08, bez blokowania pierwszego przepływu samochodowego.

---

## [APP-06b] Przeciąganie punktów i zapis nowej kolejności

- **Assignee:** sebastianwaga
- **Labels:** mobile
- **Milestone:** M2
- **Estymata:** 4–7 h
- **Branch:** feat/app-06b-points-reordering
- **Zależności:** APP-06a, API-05b, API-09

### Cel

Dodać ReorderableListView oraz zintegrować zmianę kolejności z przeliczaniem podróży.

### Kryteria odbioru

- [ ] Przeciągnięcie punktu zmienia listę i czytelnie pokazuje nowe sąsiedztwo odcinków.
- [ ] Po zapisaniu i ponownym otwarciu kolejność oraz transporty odpowiadają API i regule przyjętej w API-05b.
- [ ] Zmiana wyzwala aktualizację odpowiednich geometrii i dystansów; mapa oraz statystyki pobierają nowy stan.
- [ ] Błąd zapisu lub przeliczania nie gubi lokalnej edycji i nie jest prezentowany jako sukces.

---

## [APP-07a] Podstawowa mapa podróży z trasą samochodową

- **Assignee:** sebastianwaga
- **Labels:** mobile, mapy
- **Milestone:** M1
- **Estymata:** 4–8 h
- **Branch:** feat/app-07a-car-trip-map
- **Zależności:** APP-04, API-07

### Cel

Wyświetlić we Flutterze zapisaną podróż samochodową z punktami.

### Kryteria odbioru

- [ ] flutter_map z MapTiler pokazuje punkty i zapisaną drogową geometrię z API, bez samodzielnego wyznaczania drogi.
- [ ] Widok dopasowuje się do podróży, pozwala przybliżać oraz odczytać szczegóły punktu i odcinka, w tym dystans.
- [ ] Obsłużono brak geometrii i błąd pobrania; wymagane oznaczenia dostawców są widoczne.
- [ ] Razem z APP-06a możliwy jest przepływ: dodaj dwa punkty → samochód → zapisz → otwórz mapę.

---

## [APP-07b] Łuki lotnicze i style pozostałych transportów

- **Assignee:** sebastianwaga
- **Labels:** mobile, mapy
- **Milestone:** M2
- **Estymata:** 3–5 h
- **Branch:** feat/app-07b-transport-map-styles
- **Zależności:** APP-07a, API-08

### Cel

Rozbudować mapę o zapisane geometrie wszystkich transportów i legendę.

### Kryteria odbioru

- [ ] Lot jest przedstawiony łukiem na podstawie geometrii z API-08; pociąg i inne mają połączenia uproszczone.
- [ ] Kolory, ikony lub style linii rozróżniają środki transportu, a legenda wyjaśnia oznaczenia.
- [ ] Szczegóły i dopasowanie widoku działają również dla podróży mieszanej; sprawdzono trasę Legnica–Berlin–Majorka–Berlin–Legnica.
- [ ] Flutter renderuje geometrię i dystans z backendu, bez drugiego niezależnego algorytmu liczenia łuków i długości.

---

## [APP-08] Wyświetlić mapę wszystkich podróży

- **Assignee:** sebastianwaga
- **Labels:** mobile, mapy
- **Milestone:** M3
- **Estymata:** 4–7 h
- **Branch:** feat/app-08-history-map
- **Zależności:** APP-07b, API-10

### Cel

Udostępnić mapę historii użytkownika.

### Kryteria odbioru

- [ ] Mapa pokazuje punkty i trasy wszystkich dostępnych podróży, a widok obejmuje ich zasięg.
- [ ] Wybranie trasy lub punktu prowadzi do szczegółów właściwej podróży.
- [ ] Działa wariant dla całej historii i wybranego roku oraz poprawny stan bez podróży.

---

## [APP-09] Wyświetlić odwiedzone kraje i ich obszary

- **Assignee:** sebastianwaga
- **Labels:** mobile, mapy
- **Milestone:** M3
- **Estymata:** 5–8 h
- **Branch:** feat/app-09-visited-countries
- **Zależności:** APP-08, API-10

### Cel

Zaprezentować listę krajów oraz rzeczywiste wyróżnienie ich na mapie.

### Kryteria odbioru

- [ ] Lista krajów jest unikalna i zgodna z danymi API dla całej historii lub wybranego roku.
- [ ] Poligony odwiedzonych państw są wyróżnione na mapie; same znaczniki lub lista nazw nie zastępują tej warstwy.
- [ ] Mapowanie kodów krajów na geometrie jest sprawdzone na przykładowych danych, a brak dopasowania nie blokuje pozostałych obszarów.
- [ ] Warstwa państw i mapa podróży pozostają czytelne przy zmianie powiększenia.

---

## [APP-10] Zbudować ekran statystyk podróżniczych

- **Assignee:** adamrudziewicz
- **Labels:** mobile
- **Milestone:** M3
- **Estymata:** 5–8 h
- **Branch:** feat/app-10-statistics-screen
- **Zależności:** APP-01, API-11, ORG-05

### Cel

Czytelnie przedstawić statystyki całej historii i wybranego roku.

### Kryteria odbioru

- [ ] Widoczne są liczby podróży, państw i miejsc, lista państw, kilometry łącznie oraz według transportu.
- [ ] Przełącznik całej historii i roku pobiera właściwe dane, a jednostki i zaokrąglenia są jednoznaczne.
- [ ] Ekran korzysta z obliczeń API i odświeża się po zmianie lub usunięciu podróży.
- [ ] Pusta historia i rok bez podróży pokazują poprawne wartości, bez błędów lub pozostałości poprzedniego wyboru.

---

## [APP-11] Dodać przeglądanie publicznych profili

- **Assignee:** sebastianwaga
- **Labels:** mobile
- **Milestone:** M3
- **Estymata:** 5–8 h
- **Branch:** feat/app-11-public-profiles
- **Zależności:** APP-03, APP-07b, API-12

### Cel

Pozwolić oglądać podróże użytkowników z publicznym profilem.

### Kryteria odbioru

- [ ] Można znaleźć lub otworzyć publiczny profil i jego listę podróży.
- [ ] Wybrana cudza podróż otwiera się na mapie w trybie odczytu, bez możliwości edycji.
- [ ] Zmiana widoczności, odmowa dostępu i usunięcie zasobu są obsługiwane bez pokazywania nieaktualnych prywatnych danych.

---

## [APP-12] Ujednolicić ładowanie, puste stany i błędy

- **Assignee:** sebastianwaga
- **Labels:** mobile
- **Milestone:** M4
- **Estymata:** 4–7 h
- **Branch:** fix/app-12-screen-states
- **Zależności:** APP-06b, APP-09, APP-10, APP-11

### Cel

Dopracować spójne zachowanie wszystkich wymaganych ekranów.

### Kryteria odbioru

- [ ] Każdy ekran obsługuje ładowanie, brak danych, błąd i ponowienie właściwej operacji.
- [ ] Brak połączenia i błędy usług mapowych nie powodują utraty zapisanych danych ani fałszywego potwierdzenia sukcesu.
- [ ] Teksty błędów są zrozumiałe i nie pokazują stosów wywołań ani sekretów; formularze zachowują dane po błędzie.
- [ ] Sprawdzono mały ekran, długie nazwy i czytelność legendy; wymagane oznaczenia map są widoczne w każdym widoku mapowym.

---

## [FIN-01] Przetestować uprawnienia i prywatność API

- **Assignee:** SX2V
- **Labels:** backend, testy
- **Milestone:** M4
- **Estymata:** 5–8 h
- **Branch:** test/fin-01-api-permissions
- **Zależności:** API-10, API-11, API-12, API-13

### Cel

Potwierdzić ochronę wszystkich zasobów i działanie publicznego odczytu.

### Kryteria odbioru

- [ ] Testy obejmują właściciela, innego użytkownika, anonimowego odbiorcę i administratora w przewidzianym zakresie.
- [ ] Podmiana ID nie pozwala zmieniać cudzych podróży, punktów ani odcinków.
- [ ] Prywatne dane nie pojawiają się w listach, szczegółach, mapach i statystykach; przestawienie profilu na prywatny blokuje kolejne odczyty.
- [ ] Testy działają w CI i obejmują pełny cykl sesji. Testy własnych endpointów są dodawane również na bieżąco w zadaniach API.

---

## [FIN-02] Sprawdzić spójność tras i statystyk

- **Assignee:** sebastianwaga
- **Labels:** backend, testy
- **Milestone:** M4
- **Estymata:** 5–8 h
- **Branch:** test/fin-02-routes-statistics
- **Zależności:** API-09, API-10, API-11

### Cel

Zebrać regresje najważniejszych reguł danych w testy integracyjne.

### Kryteria odbioru

- [ ] Sprawdzono dodawanie, przenoszenie, usuwanie i przestawianie punktów oraz zmianę transportu.
- [ ] Testy obejmują powtarzające się kraje i miejsca, pustą historię, zerowy dystans oraz podróż na przełomie lat.
- [ ] Edycja i usunięcie podróży zmieniają mapę krajów i wszystkie właściwe statystyki; suma transportów zgadza się z sumą łączną.
- [ ] Błąd geokodowania lub routingu ma przewidziany rezultat, a zapisane dane nie są ponownie wyznaczane przy samym odczycie.

---

## [FIN-03] Przetestować pełny przepływ w aplikacji mobilnej

- **Assignee:** sebastianwaga
- **Labels:** mobile, testy
- **Milestone:** M4
- **Estymata:** 8–12 h
- **Branch:** test/fin-03-mobile-flow
- **Zależności:** APP-12, FIN-01, FIN-02

### Cel

Potwierdzić współpracę wymaganych ekranów z rzeczywistym API.

### Kryteria odbioru

- [ ] Wykonano rejestrację, logowanie, dodanie podróży, wybór punktów i transportów, zapis oraz ponowne otwarcie mapy.
- [ ] Edycja i usunięcie podróży odświeżają listę, mapę wszystkich podróży, kraje oraz statystyki.
- [ ] Sprawdzono profil publiczny i prywatny z drugiego konta, restart aplikacji oraz wylogowanie.
- [ ] Najważniejszy stabilny przepływ ma test integracyjny, a scenariusze ręczne i wynik próby na urządzeniu są zapisane w repozytorium.

---

## [FIN-04] Wdrożyć API, bazę, panel i dokumentację

- **Assignee:** SX2V
- **Labels:** infrastruktura, backend
- **Milestone:** M4
- **Estymata:** 8–14 h
- **Branch:** ops/fin-04-deployment
- **Zależności:** ORG-02, API-13, API-14

### Cel

Udostępnić działające środowisko zdalne potrzebne do prezentacji.

### Kryteria odbioru

- [ ] Django API, Django Admin i Swagger UI działają zdalnie przez HTTPS, a baza przechowuje dane po restarcie usług.
- [ ] Zmienne i klucze są konfigurowane dla wdrożenia; DEBUG jest wyłączony, a migracje i pliki statyczne panelu są obsłużone.
- [ ] Opisano wykonanie kopii bazy i sprawdzono możliwość jej odtworzenia; dostępny jest podstawowy podgląd logów.
- [ ] Po wdrożeniu wykonano próbę logowania, zapisu podróży i otwarcia dokumentacji; pierwsze środowisko testowe warto uruchomić już w M1.

---

## [FIN-05] Przygotować instalowalne wydanie mobilne

- **Assignee:** sebastianwaga
- **Labels:** mobile
- **Milestone:** M4
- **Estymata:** 3–5 h
- **Branch:** release/fin-05-mobile-build
- **Zależności:** FIN-03, FIN-04

### Cel

Zbudować aplikację, którą można zainstalować i pokazać na urządzeniu.

### Kryteria odbioru

- [ ] Przygotowano oznaczony wersją instalowalny build, np. APK na Androida, z właściwym adresem zdalnego API.
- [ ] Wydanie działa na urządzeniu, w tym mapy, wymagane klucze dostawców i podstawowy przepływ podróży.
- [ ] Instrukcja opisuje instalację i lokalizację artefaktu; publikacja w sklepie nie jest zakładana jako dodatkowy wymóg.

---

## [FIN-06] Napisać instrukcję uruchomienia i wdrożenia

- **Assignee:** adamrudziewicz
- **Labels:** dokumentacja
- **Milestone:** M4
- **Estymata:** 3–5 h
- **Branch:** docs/fin-06-running-instructions
- **Zależności:** FIN-04, FIN-05

### Cel

Umożliwić uruchomienie i ocenę systemu na podstawie dokumentacji. SX2V dostarcza komendy backendu i wdrożenia, a sebastianwaga instalacji i budowania mobilki.

### Kryteria odbioru

- [ ] Instrukcja lokalna obejmuje wymagane narzędzia, konfigurację, backend, bazę, migracje, administratora i Fluttera.
- [ ] Instrukcja zdalna opisuje wdrożenie, adresy API/panelu/OpenAPI, aktualizację oraz konfigurację usług mapowych.
- [ ] Opisano instalację mobilki i uruchomienie testów; druga osoba sprawdziła instrukcję na świeżym środowisku lub czystym checkoutcie.

---

## [FIN-07] Opracować sprawozdanie w LaTeX i PDF

- **Assignee:** adamrudziewicz
- **Labels:** dokumentacja
- **Milestone:** M4
- **Estymata:** 8–14 h
- **Branch:** docs/fin-07-project-report
- **Zależności:** FIN-06

### Cel

Przygotować dokumenty obejmujące wymagania obu przedmiotów. Adam koordynuje skład dokumentu; każdy autor dostarcza opis własnej implementacji i czasochłonności.

### Kryteria odbioru

- [ ] W repozytorium są źródła LaTeX i wynikowy PDF; ustalono sposób oddania dokumentów dla obu przedmiotów.
- [ ] Sprawozdanie zawiera opis zamówienia, technologie, podział obowiązków, zadania z estymatami i rzeczywistą czasochłonnością.
- [ ] Zawiera instrukcje lokalnego i zdalnego uruchomienia oraz wnioski: co zrealizowano, czego nie i co można poprawić.
- [ ] Treść odpowiada wdrożonemu systemowi i jest gotowa najpóźniej w dniu oddania; rozdziały powstają na bieżąco, zanim zakończy się FIN-06.

---

## [FIN-08] Przygotować dane i przećwiczyć prezentację

- **Assignee:** SX2V
- **Labels:** organizacja
- **Milestone:** M4
- **Estymata:** 4–7 h
- **Branch:** docs/fin-08-presentation
- **Zależności:** FIN-05, FIN-07

### Cel

Przygotować scenariusz i skoordynować wspólną próbę demonstracji działającego, wdrożonego systemu. Każdy członek zespołu prezentuje swoją część.

### Kryteria odbioru

- [ ] Dane demonstracyjne obejmują co najmniej dwa konta o różnej prywatności i podróże w co najmniej dwóch latach.
- [ ] Scenariusz obejmuje Legnica–Berlin samochodem, Berlin–Majorka samolotem, kilka punktów samochodem na Majorce i podróż powrotną oraz przykłady pozostałych transportów.
- [ ] Demo pokazuje edycję, mapę jednej i wszystkich podróży, wyróżnione kraje, statystyki historyczne i roczne, publiczny profil, panel oraz OpenAPI.
- [ ] Cały zespół uczestniczy w próbie, zna swoje części prezentacji i sprawdził działanie wdrożenia oraz instalowalnej aplikacji.

---
