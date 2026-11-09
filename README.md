# Dziennik podróży

Projekt aplikacji turystycznej na przedmioty **Projekt zespołowy**
oraz **Programowanie urządzeń mobilnych** w roku akademickim 2026/27.

System ma umożliwiać zapisywanie podróży, oglądanie ich na mapie
i analizowanie historii podróżowania. Obejmuje aplikację mobilną,
API oraz webowy panel administracyjny.

## Status

Projekt jest na etapie planowania. Poniższe funkcje, technologie
i procedury opisują docelowe rozwiązanie.

Backlog, kryteria odbioru, zależności, branche i przypisania 43 zadań
znajdują się w [TASKS.md](TASKS.md).

## Repozytoria projektu

- **Repozytorium główne (Backend API, Panel administracyjny, Backlog, Sprawozdanie):** [sebastianwaga/S7-PZ-Backend](https://github.com/sebastianwaga/S7-PZ-Backend)
- **Repozytorium aplikacji mobilnej (Flutter):** [sebastianwaga/S7-PZ-Mobile](https://github.com/sebastianwaga/S7-PZ-Mobile)
- **Tablica zadań (GitHub Issues):** [Issues w S7-PZ-Backend](https://github.com/sebastianwaga/S7-PZ-Backend/issues)

## Planowane funkcje

- Rejestracja, logowanie, odświeżanie sesji i wylogowanie.
- Edycja profilu i wybór widoczności publiczny/prywatny.
- Przeglądanie podróży użytkowników z publicznym profilem.
- Dodawanie, edycja i usuwanie podróży z nazwą, datą lub zakresem dat i opcjonalnym opisem.
- Uporządkowane punkty podróży i osobny środek transportu dla każdego odcinka.
- Trasy samochodowe po drogach, łuki lotnicze oraz uproszczone połączenia dla pociągu i transportu innego.
- Mapa jednej podróży i wszystkich podróży użytkownika, z wyróżnieniem odwiedzonych państw.
- Statystyki całej historii i wybranego roku: podróże, państwa, miejsca, dystans łączny i według transportu.
- Panel administratora do zarządzania danymi oraz dokumentacja OpenAPI przy wdrożonym API.

Reguły liczenia miejsc, państw, dystansów i podróży na przełomie lat
zostaną uzgodnione w ORG-06 i zapisane w dokumentacji.

Zapisane geometrie i dystanse mają być wykorzystywane przy odczycie
bez ponownego wyznaczania tras.

## Technologie

| Obszar | Wybrany zestaw |
| --- | --- |
| Aplikacja mobilna | Flutter, Dart, Riverpod, Dio |
| API | Python, Django, Django REST Framework |
| Panel administracyjny | Django Admin |
| Baza danych | PostgreSQL; PostGIS opcjonalnie |
| Mapa i wyszukiwanie miejsc | flutter_map, MapTiler |
| Trasy samochodowe | openrouteservice |
| Dokumentacja API | drf-spectacular, OpenAPI, Swagger UI |
| Środowisko i wdrożenie | Docker Compose, planowany VPS i HTTPS przez Caddy |
| Kontrole jakości | GitHub Actions, Ruff, pytest, flutter analyze, flutter test |
| Sprawozdanie | LaTeX i wynikowy PDF |

Konkretne wersje narzędzi i zależności zostaną ustalone przy tworzeniu
projektu oraz zapisane w jego konfiguracji.

## Zespół

| Osoba | Główne obszary odpowiedzialności |
| --- | --- |
| adamrudziewicz | Organizacja i makiety, profil API, ekrany konta, profilu, listy podróży i statystyk, koordynacja dokumentacji |
| SX2V | Modele i API, uwierzytelnianie, integracje usług, spójność danych, panel administracyjny, wdrożenie i koordynacja prezentacji |
| sebastianwaga | Podstawa aplikacji mobilnej, edytor podróży i mapy, powiązane dane przestrzenne API, CI, testy integracyjne i wydanie mobilne |

Dokładne przypisanie każdego zadania określa [TASKS.md](TASKS.md).
Cały zespół uczestniczy w review, przygotowaniu własnych części
sprawozdania oraz prezentacji.

## Wymagania środowiska i uruchomienie

Do przygotowania środowiska przewidziano:

- Git.
- Docker z Docker Compose.
- Flutter SDK.
- Narzędzia Androida i emulator lub urządzenie.
- Zgodny Python i zależności projektu przy uruchamianiu backendu poza kontenerem.

Integracje wymagają kont i kluczy MapTiler oraz openrouteservice.
Klucze i sekrety muszą być konfigurowane poza repozytorium.
Konfiguracja ma uwzględniać limity dostawców, warunki zapisu wyników
i wymagane oznaczenia autorstwa map.

Dokładna instrukcja zostanie uzupełniona i sprawdzona podczas
ORG-02, ORG-03 oraz FIN-06. Będzie obejmować:

1. Pobranie repozytorium oraz instalację zgodnych wersji narzędzi i zależności.
2. Konfigurację środowiska na podstawie pliku `.env.example`.
3. Uruchomienie bazy i backendu, migracje oraz utworzenie administratora.
4. Konfigurację adresu API dla emulatora lub urządzenia i uruchomienie Fluttera.
5. Uruchomienie testów, lintowania i walidacji OpenAPI.
6. Wdrożenie, adresy API/panelu/Swagger UI, kopię i odtworzenie bazy oraz instalację wydania mobilnego.

Komendy uruchomienia, wersje, rzeczywiste adresy i lokalizacja pliku
instalacyjnego zostaną podane po przygotowaniu oraz weryfikacji tych elementów.

## GitHub flow

1. Utwórz Issue na podstawie odpowiedniej sekcji w TASKS.md.
2. Ustaw Assignee, Labels i Milestone oraz uzupełnij estymatę.
3. Zastąp robocze identyfikatory zależności odnośnikami do utworzonych Issues.
4. Z aktualnego `main` utwórz branch wskazany w zadaniu.
5. Wprowadzaj zmiany, testy i aktualizacje dokumentacji.
6. Otwórz PR do `main` z opisem zmiany i sposobem jej sprawdzenia.
7. Dodaj `Closes #numer`, jeśli PR kończy Issue, albo `Refs #numer` dla części pracy.
8. Poproś pozostałych członków zespołu o review i uwzględnij uwagi.
9. Po akceptacji i przejściu wymaganych kontroli wykonaj squash merge.
10. Usuń scalony branch i uzupełnij rzeczywisty czas w Issue.

Samo wklejenie treści TASKS.md do repozytorium nie tworzy GitHub Issues
ani nie ustawia ich metadanych.

## Kontrola jakości

Planowane CI uruchamia:

- **Backend:** Ruff i pytest.
- **Aplikacja mobilna:** flutter analyze i flutter test.
- **Testy bazodanowe:** PostgreSQL jako baza testowa.

Każda zmiana API obejmuje aktualizację OpenAPI.
Testy funkcji powstają przy ich implementacji.
Końcowe testy integracyjne obejmują prywatność, trasy, statystyki
i pełny przepływ aplikacji mobilnej.

## Etapy

| Milestone | Zakres |
| --- | --- |
| M1 | Środowisko, CI, konto, podróże, punkty i pierwsza trasa samochodowa widoczna w aplikacji |
| M2 | Profil, pełna edycja punktów, pozostałe transporty, przeliczenia i panel administracyjny |
| M3 | Historia podróży, odwiedzone kraje, statystyki i publiczne profile |
| M4 | Testy całości, wdrożenie, wydanie mobilne, dokumentacja i prezentacja |

## Dokumentacja i oddanie

Skład zespołu i publiczne repozytorium należy zgłosić najpóźniej
do drugich zajęć, a szczegółowe i przypisane Issues przygotować
przed czwartymi.

Prace nad aplikacją mobilną muszą rozpocząć się najpóźniej
do 7–8 zajęć; plan zakłada ich rozpoczęcie w M1.

Dokumentacja ma zawierać:

- Opis zamówienia i wymagania.
- Wykorzystane technologie.
- Podział obowiązków i zadania.
- Estymowaną i rzeczywistą czasochłonność.
- Instrukcje lokalnego i zdalnego uruchomienia.
- Wnioski, zrealizowane funkcje i możliwe usprawnienia.

Źródła LaTeX i PDF mają trafić do repozytorium.
Sposób oddania dla obu przedmiotów zostanie uzgodniony.

Prezentacja obejmuje działające wdrożenie, instalowalną aplikację
mobilną, panel administracyjny i OpenAPI. Cały zespół uczestniczy
w próbie i końcowym demo, przygotowanym na przykładowych podróżach
obejmujących różne środki transportu i lata.
