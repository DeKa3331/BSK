# Gnu Privacy Guard (GPG): Analiza Kluczowych Koncepcji i Mechanizmów

## Streszczenie menedżerskie

Dokument stanowi syntezę kluczowych informacji dotyczących **Gnu Privacy Guard (GPG)**, otwartoźródłowej implementacji standardu **Pretty Good Privacy (PGP)**. GPG to fundamentalne narzędzie służące do zabezpieczania danych i komunikacji, które zapewnia poufność, integralność oraz autentyczność informacji.

Jego działanie opiera się na **kryptografii asymetrycznej**, wykorzystującej parę kluczy: **publiczny** (udostępniany) oraz **prywatny** (tajny). Kluczowym elementem systemu jest zdecentralizowany model zaufania, znany jako **"Web of Trust" (sieć zaufania)**.

---

## 1. Wprowadzenie do Gnu Privacy Guard (GPG)

**Gnu Privacy Guard (GPG)** jest otwartoźródłową implementacją standardu PGP. Jego głównym celem jest zabezpieczanie komunikacji i danych poprzez mechanizmy szyfrowania i podpisywania cyfrowego. Implementacja tych funkcji pozwala osiągnąć trzy kluczowe cele bezpieczeństwa:

* **Poufność:** Zapewnienie, że informacje są dostępne tylko dla uprawnionych osób.
* **Integralność:** Gwarancja, że przesyłane dane nie zostały zmodyfikowane w trakcie transmisji.
* **Autentyczność:** Potwierdzenie tożsamości nadawcy informacji.

---

## 2. Fundament Działania: Kryptografia Klucza Asymetrycznego

Podstawą działania GPG jest system **kryptografii asymetrycznej**, który opiera się na generowaniu unikalnej pary kluczy dla każdego użytkownika.



### Klucz publiczny
Jest **jawny** i przeznaczony do udostępniania innym osobom. Służy do dwóch celów:
1.  **Szyfrowanie wiadomości:** Każdy, kto posiada klucz publiczny odbiorcy, może zaszyfrować dla niego wiadomość.
2.  **Weryfikacja podpisów cyfrowych:** Umożliwia sprawdzenie, czy podpis został złożony przez właściciela odpowiadającego mu klucza prywatnego.

### Klucz prywatny
Jest **ściśle tajny** i musi być chroniony przez właściciela. Jego zastosowania są lustrzanym odbiciem klucza publicznego:
1.  **Deszyfrowanie wiadomości:** Tylko posiadacz klucza prywatnego może odszyfrować wiadomość zaszyfrowaną jego kluczem publicznym.
2.  **Tworzenie podpisów cyfrowych:** Służy do generowania unikalnego podpisu pod danymi, co potwierdza tożsamość nadawcy.

---

## 3. Proces Szyfrowania i Deszyfrowania Danych

Mechanizm szyfrowania w GPG ma na celu zapewnienie **poufności danych**. Proces ten przebiega w dwóch etapach.



### Proces Szyfrowania
1.  **Plik źródłowy (Raw File):** Użytkownik posiada oryginalny, niezaszyfrowany plik.
2.  **Szyfrowanie:** Plik jest szyfrowany przy użyciu **klucza publicznego** docelowego odbiorcy.
3.  **Plik zaszyfrowany (Encrypted File):** Wynikiem operacji jest plik, którego treść jest niemożliwa do odczytania bez odpowiedniego klucza.
4.  **Transmisja:** Zaszyfrowany plik może być bezpiecznie przesłany za pośrednictwem publicznych kanałów.

### Proces Deszyfrowania
1.  **Odbiór pliku:** Odbiorca otrzymuje zaszyfrowany plik.
2.  **Deszyfrowanie:** Odbiorca używa swojego **klucza prywatnego** (matematycznie powiązanego z użytym kluczem publicznym), aby odszyfrować plik.
3.  **Plik źródłowy:** Odbiorca odzyskuje oryginalną, czytelną treść.

---

## 4. Podpisy Cyfrowe: Weryfikacja Autentyczności i Integralności

**Podpis cyfrowy** służy do potwierdzenia, że wiadomość pochodzi od konkretnego nadawcy (**autentyczność**) i że jej treść nie została zmieniona (**integralność**).



### Proces Podpisywania (Nadawca)
1.  **Utworzenie skrótu (Hash):** Z oryginalnej wiadomości generowany jest unikalny skrót kryptograficzny.
2.  **Szyfrowanie skrótu:** Wygenerowany skrót jest szyfrowany przy użyciu **klucza prywatnego** nadawcy. Wynik to **podpis cyfrowy**.
3.  **Dołączenie podpisu:** Podpis jest dołączany do wiadomości.

### Proces Weryfikacji (Odbiorca)
1.  **Rozdzielenie danych:** Odbiorca oddziela wiadomość od podpisu.
2.  **Obliczenie nowego skrótu:** Odbiorca oblicza własny skrót z otrzymanej wiadomości (Wynik A).
3.  **Odszyfrowanie podpisu:** Odbiorca używa **klucza publicznego** nadawcy do odszyfrowania podpisu cyfrowego, odzyskując oryginalny skrót (Wynik B).
4.  **Porównanie:** Jeśli skróty (A i B) są identyczne, weryfikacja jest pomyślna.

---

## 5. Metody Podpisywania Plików w GPG

GPG oferuje trzy główne metody tworzenia podpisów cyfrowych:

| Metoda | Polecenie GPG | Opis | Plik wynikowy | Polecenie weryfikacji |
| :--- | :--- | :--- | :--- | :--- |
| **Podpis zintegrowany** (sign) | `gpg --sign plik.txt` | Podpis jest dołączany bezpośrednio do pliku (binarny). | `plik.txt.gpg` | `gpg --verify plik.txt.gpg` |
| **Podpis odłączony** (detach-sign) | `gpg --detach-sign plik.txt` | Podpis jest w osobnym pliku; oryginał pozostaje nienaruszony. | `plik.txt.sig` | `gpg --verify plik.txt.sig plik.txt` |
| **Podpis tekstowy** (clearsign) | `gpg --clearsign plik.txt` | Podpis dodawany w formie czytelnej (ASCII). Treść pozostaje widoczna. | `plik.txt.asc` | `gpg --verify plik.txt.asc` |

---

## 6. Zarządzanie Kluczami i Model Zaufania

### Keyring (Pierścień Kluczy)
Jest to **baza danych**, w której GPG przechowuje klucze publiczne i prywatne użytkownika oraz zaimportowane klucze innych osób.

### Web of Trust (Sieć Zaufania)
W odróżnieniu od centralnych urzędów (CA), GPG wykorzystuje **zdecentralizowany model zaufania**.



* Użytkownicy osobiście weryfikują tożsamość innych.
* Podpisują klucz publiczny innej osoby swoim kluczem prywatnym, wyrażając **zaufanie**.
* Tworzy się sieć powiązań, pozwalająca ufać kluczom poświadczonym przez zaufanych pośredników.

### Fingerprint (Odcisk Palca)
Unikalny identyfikator klucza publicznego (skrót kryptograficzny). Służy do **jednoznacznej i bezpiecznej identyfikacji klucza**. Porównanie odcisku palca (np. telefonicznie) jest zalecaną metodą weryfikacji tożsamości właściciela klucza.
