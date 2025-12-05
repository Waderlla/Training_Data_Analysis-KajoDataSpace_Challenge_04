# Proces przygotowania i oczyszczania danych

Poniżej znajduje się kompletny opis procesu oczyszczania danych zastosowanego we wszystkich tabelach użytych w projekcie fitness‑dashboard.

---

## 1. Ogólny cel przygotowania danych

Celem procesu było:
- ujednolicenie nazewnictwa kolumn i wartości,
- konwersja typów danych do prawidłowych formatów (daty, liczby, czas),
- dodanie pól pomocniczych niezbędnych do wizualizacji (np. `czas` jako typ *time*),
- stworzenie słownika mapującego każde ćwiczenie na główną partię mięśniową,
- przygotowanie jednolitego schematu danych umożliwiającego dalsze łączenie w Tableau.

---

## 2. Tabela **Sztanga**

### Wykonane kroki:
1. Załadowanie danych oraz nadanie nagłówków.
2. Konwersja typów:
   - `Dzień` → *date*  
   - wartości liczbowe (`powtorzenia`, `serie`, `waga_kg`) → *whole number*
3. Usunięcie pustych wierszy i zbędnych kolumn.
4. Ujednolicenie nazw kolumn (`cwiczenie`, `waga_kg`, `czas_miedzy_seriami`).
5. Dodanie obliczonej kolumny `partia_glowna` — reguły przypisujące każdą nazwę ćwiczenia do partii mięśniowej.
6. Ostateczne uporządkowanie typów danych.

---

## 3. Tabela **Orbitrek**

### Wykonane kroki:
1. Załadowanie danych oraz nadanie nagłówków.
2. Zmiana nazw kolumn (`dzien`, `minuty`, `kalorie`).
3. Konwersja typów:  
   - `dzien` → *date*,  
   - `minuty`, `kalorie` → *whole number*.
4. Dodanie kolumny pomocniczej:  
   - `czas = minuty/1440` jako liczba dni (wymóg Power Query).
5. Konwersja `czas` do typu *time* dla prawidłowego eksportu do Tableau.

---

## 4. Tabela **Max Pull Up**

### Wykonane kroki:
1. Załadowanie danych oraz nadanie nagłówków.
2. Konwersja typów:  
   - `Dzień` → *date*,  
   - `Max Pull Up` → *whole number*.
3. Zmiana nazw kolumn na `dzien` oraz `max_pull_up` dla spójności.

---

## 5. Tabela **Ćwiczenia ogólne**

### Wykonane kroki:
1. Załadowanie danych, nadanie nagłówków.
2. Konwersja typów:  
   - `Dzień` → *date*,  
   - `Minuty` → *whole number*,  
   - `Rodzaj ćwiczenia` → *text*.
3. Ujednolicenie nazw kolumn (`dzien`, `cwiczenie`, `minuty`).
4. Dodanie kolumny `czas = minuty / 1440`.
5. Konwersja `czas` do typu *time*.

---

## 6. Tabela **Małe ćwiczenia**

*(Jeśli stosowana analogicznie — zapis uwzględnia standardowy proces)*  
1. Nadanie nagłówków, konwersja typów.  
2. Wyczyszczenie wartości tekstowych.  

---

## 7. Tabela **Waga i obwód**

1. Uporządkowanie nagłówków.
2. Konwersja daty oraz wszystkich obwodów do typów liczbowych.
3. Usunięcie pustych rekordów.

---

## 8. Tabela **mapping_cwiczenia_miesnie**

(Słownik stworzony ręcznie)

- Zawiera dwie kolumny: `cwiczenie` oraz `miesien`.
- Każde ćwiczenie przypisane do konkretnej partii głównej.
- Wczytane i użyte bez modyfikacji (jedynie nagłówki + typy).

---

## 9. Spójność schematu danych

Wszystkie tabele końcowe mają:
- kolumny o spójnych nazwach (`dzien`, `cwiczenie`, `minuty`, `czas`, `waga_kg`, `serie`, `powtorzenia`, `kalorie`, `max_pull_up`),
- prawidłowe typy danych,
- przygotowane pola niezbędne do obliczeń i KPI w Tableau.

Plik jest gotowy do połączenia na poziomie daty lub ćwiczenia oraz do użycia w dashboardzie.

---

## 10. Rezultat końcowy

Proces oczyszczania umożliwia:
- bezbłędne łączenie danych z różnych źródeł,
- poprawne działanie filtrów i obliczeń w Tableau,
- pełną automatyzację odświeżania danych,
- czytelność i jednoznaczność w raportowaniu.

