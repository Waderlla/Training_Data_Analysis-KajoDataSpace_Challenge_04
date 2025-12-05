# Opis procesu oczyszczania danych

## 1. Przegląd
Ten dokument opisuje pełny proces oczyszczania danych zastosowany do wszystkich zestawów danych treningowych użytych w dashboardzie. Celem było stworzenie spójnych, gotowych do analizy tabel we wszystkich źródłach, przy jednoczesnym zachowaniu szczegółowych informacji o treningach.

---

## 2. Pliki źródłowe
Do Power Query zostały zaimportowane następujące pliki:

- **male_cwiczenia.csv**  
- **waga_i_obwod.csv**  
- **sztanga.csv**  
- **orbitrek.csv**  
- **max_pull_up.csv**  
- **cwiczenia_ogolne.csv**  
- **mapping_cwiczenia_miesnie.csv** *(ręcznie stworzona tabela mapowania)*

Każdy plik wymagał nieco innego zakresu czyszczenia w zależności od struktury i jakości danych.

---

## 3. Ogólne zasady oczyszczania danych
We wszystkich zestawach danych zastosowano te same podstawowe kroki:

- usunięcie pustych wierszy,
- podniesienie pierwszego wiersza do nagłówków,
- ustawienie odpowiednich typów danych (data, tekst, liczby, czas),
- ujednolicenie nazw kolumn do formatu snake_case,
- usunięcie niepotrzebnych lub automatycznie wygenerowanych kolumn (np. `_1`, `_2`),
- usunięcie zbędnych spacji i korekta drobnych niespójności tekstowych.

Dzięki temu możliwe było późniejsze łączenie tabel zgodnie z jedną wspólną strukturą.

---

## 4. Czyszczenie poszczególnych plików

### 4.1 **sztanga.csv**
Najbardziej złożony plik ze względu na komentarze i dodatkowe ręczne pola.

**Kroki:**

1. Podniesienie pierwszego wiersza do nagłówków.  
2. Ustawienie typów danych dla wszystkich kolumn.  
3. Usunięcie pustych wierszy i automatycznie wygenerowanych kolumn.  
4. Ujednolicenie nazw kolumn, np.:  
   - `Dzień` → `dzien`  
   - `Ćwiczenie` → `cwiczenie`  
   - `Powtórzenia` → `powtorzenia`  
   - `Serie` → `serie`  
   - `Waga (kg)` → `waga_kg`  
5. Wyciągnięcie strukturalnych informacji z komentarzy:  
   - `ocena_ciezaru` – czy ciężar był odpowiedni,  
   - `blisko_upadku` – czy seria była blisko upadku mięśniowego,  
   - `odczucia_miesniowe` – czy pojawiły się odczucia mięśniowe.  
6. Konwersja powyższych pól na typ liczbowy (0/1).  
7. Dodanie kolumny `partia_glowna` poprzez mapowanie ćwiczenia do partii mięśniowej.

---

### 4.2 **orbitrek.csv**
Prosty plik z danymi cardio.

**Kroki:**

1. Podniesienie nagłówków.  
2. Ustawienie typów (data, liczby).  
3. Ujednolicenie kolumn: `dzien`, `minuty`, `kalorie`.  
4. Dodanie kolumny `czas` → przeliczenie minut na format czasu.  
5. Konwersja `czas` na typ *time*.

---

### 4.3 **max_pull_up.csv**

**Kroki:**

1. Podniesienie nagłówków.  
2. Ustawienie typów danych:  
   - `Dzień` jako data,  
   - `Max Pull Up` jako liczba.  
3. Zmiana nazw kolumn: `dzien`, `max_pull_up`.

---

### 4.4 **cwiczenia_ogolne.csv**
Ćwiczenia mieszane, siłowe i cardio.

**Kroki:**

1. Podniesienie nagłówków.  
2. Ustawienie typów danych.  
3. Ujednolicenie nazw kolumn: `dzien`, `cwiczenie`, `minuty`.  
4. Dodanie `czas` → konwersja minut na format czasu.  
5. Konwersja na typ *time*.

---

### 4.5 **waga_i_obwod.csv**

**Kroki:**

1. Import do Power Query.  
2. Po imporcie **ręcznie dodano w Excelu kolumnę `wzrost`**, potrzebną np. do liczenia BMI.

---

### 4.6 **mapping_cwiczenia_miesnie.csv**
Tabela ręczna, służąca do przypisania ćwiczeń do partii mięśniowych.

**Kroki:**

1. Podniesienie nagłówków.  
2. Ustawienie typu tekstowego dla obu kolumn.

---

## 5. Wynik końcowy
Po oczyszczeniu wszystkie pliki:

- mają spójne nazwy kolumn,
- poprawne typy danych,
- dodatkowe kolumny wyprowadzone z komentarzy,
- jednolite mapowanie ćwiczeń do głównych partii mięśniowych.

Dane są gotowe do dalszego modelowania, tworzenia KPI i budowy dashboardu.
