# Analiza Luki Bezpieczeństwa SQL Injection

## Podsumowanie Zarządcze

Dokument ten przedstawia kompleksową analizę podatności **SQL Injection (SQLi)**, jednej z najpowszechniejszych i najbardziej niebezpiecznych luk w aplikacjach internetowych.

**SQLi** polega na **wstrzykiwaniu złośliwego kodu SQL** do zapytań bazodanowych, co może prowadzić do kradzieży lub modyfikacji danych, a w skrajnych przypadkach do przejęcia pełnej kontroli nad serwerem.



### Kluczowe wnioski:
* **Identyfikacja:** Podatność występuje w polach wejściowych (formularze, URL). Testowanie polega na wprowadzaniu znaków specjalnych (np. `'`, `;`) i obserwowaniu błędów.
* **Typy Ataków:** Od klasycznego wstrzyknięcia, przez **SQL Union Injection** (kradzież danych), po zaawansowane techniki **Blind** oraz **Time-Based** (wnioskowanie o danych bez widocznych błędów).
* **Metody Ochrony:** Fundamentem są **Zapytania Przygotowane (Prepared Statements)**. Wspierane przez walidację danych, zasadę minimalnych uprawnień i zapory WAF.

---

## 1. Wprowadzenie do SQL Injection (SQLi)

**SQL Injection** to technika ataku polegająca na manipulacji zapytaniem do bazy danych poprzez nieodpowiednio zabezpieczone dane wejściowe aplikacji.

**Potencjalne Skutki Ataku:**
1.  **Kradzież wrażliwych danych** (hasła, dane osobowe).
2.  **Modyfikacja lub usunięcie danych** (niszczenie integralności bazy).
3.  **Przejęcie pełnej kontroli** nad serwerem bazy danych.

---

## 2. Identyfikacja Podatności SQL Injection

Proces opiera się na dwóch działaniach: **testowaniu wejść** i **obserwacji odpowiedzi**.

### 2.1. Testowanie Wejść Użytkownika
Podatność występuje tam, gdzie dane użytkownika trafiają bezpośrednio do zapytań SQL:
* Formularze (logowania, wyszukiwania).
* Parametry w URL.
* Nagłówki HTTP i pliki cookie.

**Metody testowania (Payloady):**
* Znaki specjalne: `'`, `"`, `;`, `--`
* Testy logiczne: `' OR '1'='1'; --`
* Testy UNION: `' UNION SELECT NULL , NULL , NULL; --`

### 2.2. Obserwowanie Odpowiedzi Serwera
Objawy istnienia luki:
* **Błędy bazy danych:** Np. `SQL syntax error`.
* **Zmiana zachowania:** Aplikacja zwraca więcej danych niż powinna lub loguje użytkownika bez hasła.

---

## 3. Typologia Ataków SQL Injection



### 3.1. Klasyczny SQL Injection
Bezpośrednie wstrzyknięcie kodu, wykorzystujące brak walidacji.
* **Przykład:** Ominięcie logowania.
    * *Zapytanie:* `SELECT * FROM users WHERE username = '$user'`
    * *Atak:* `' OR '1'='1`
    * *Skutek:* Warunek zawsze prawdziwy, zwraca wszystkich użytkowników.

### 3.2. SQL Union Injection
Wykorzystuje operator **UNION** do połączenia wyników legalnego zapytania z wynikami ataku.
* **Cel:** Wydobycie danych z innych tabel.
* *Przykład:* `1' UNION SELECT null, database();` – zwraca nazwę bazy danych.

### 3.3. Blind SQL Injection
Stosowany, gdy aplikacja **nie zwraca błędów ani wyników zapytania**. Atakujący wnioskuje o danych na podstawie zachowania aplikacji (np. True/False).
* *Metoda:* Zadawanie pytań "Czy pierwsza litera hasła to 'A'?".

### 3.4. Time-Based Blind SQL Injection
Odmiana Blind SQLi oparta na **opóźnieniach czasowych**.
* *Mechanizm:* Jeśli warunek jest prawdziwy, serwer "zasypia" (np. `SLEEP(5)`).
* *Przykład:* `' OR IF(SUBSTRING(database(),1,1)='t', SLEEP(5), 0); --`

---

## 4. Metody Ochrony i Dobre Praktyki

Skuteczna ochrona wymaga podejścia wielowarstwowego (Defense in Depth).



1.  **Używanie Przygotowanych Zapytań (Prepared Statements):**
    Najważniejsza metoda. Oddziela kod SQL od danych. Silnik bazy traktuje wejście użytkownika zawsze jako tekst, a nie jako komendę.
    * *Python:* `cursor.execute("SELECT * FROM users WHERE user = ?", (username,))`

2.  **Walidacja i Sanitacja:**
    * Ograniczenie formatu danych (np. tylko liczby).
    * Kodowanie znaków specjalnych.

3.  **Zarządzanie Uprawnieniami:**
    Zasada **najmniejszego przywileju**. Aplikacja powinna mieć dostęp tylko do niezbędnych tabel.

4.  **Zapory Aplikacyjne (WAF):**
    Automatyczne blokowanie żądań zawierających wzorce SQLi.

5.  **Regularne Testy:**
    Audyty kodu i testy penetracyjne.

---

## 5. Przykłady Ataków SQL Injection (SQLi)

> **Ważne:** Poniższe przykłady służą wyłącznie celom edukacyjnym. Testowanie ich na systemach, do których nie masz uprawnień, jest nielegalne.

---

### 1. Omijanie Uwierzytelniania (Authentication Bypass)
To klasyczny przykład, w którym atakujący loguje się na konto administratora **bez znajomości hasła**.

**Scenariusz:** Formularz logowania na stronie.

**Podatny kod (PHP):**
```php
$username = $_POST['username'];
$password = $_POST['password'];

// Niebezpieczne łączenie ciągów znaków
$sql = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";
```

**Atak (Payload):**
W polu nazwy użytkownika wpisujemy:
```sql
admin' OR '1'='1
```
W polu hasła wpisujemy cokolwiek (jest ignorowane).

**Co widzi baza danych?**
```sql
SELECT * FROM users WHERE username = 'admin' OR '1'='1' AND password = '...'
```


**Wynik:**
Warunek `OR '1'='1'` jest zawsze prawdziwy (**TRUE**). Baza danych zwraca pierwszy rekord z tabeli (zazwyczaj jest to administrator), ignorując sprawdzanie hasła.

---

### 2. Kradzież Danych (UNION-Based SQLi)
Wykorzystuje operator **UNION**, aby dołączyć wyniki z innej tabeli do wyników, które aplikacja legalnie wyświetla.

**Scenariusz:** Wyszukiwarka produktów (np. `search.php?id=10`).

**Podatny kod:**
```sql
SELECT title, description, price FROM products WHERE id = $id
```

**Atak (Payload):**
W parametrze URL podajemy:
```sql
1 UNION SELECT username, password, email FROM users
```

**Co widzi baza danych?**
```sql
SELECT title, description, price FROM products WHERE id = 1
UNION
SELECT username, password, email FROM users
```

**Wynik:**
Aplikacja wyświetli produkt o ID 1, a pod nim – zamiast kolejnych produktów – wyświetli **listę loginów, haseł i emaili** z tabeli `users`.
*Warunek:* Liczba kolumn w obu zapytaniach musi się zgadzać.

---

### 3. Niszczenie Danych (Stacked Queries)
Jeśli baza danych i sterownik pozwalają na wykonywanie **wielu zapytań rozdzielonych średnikiem** (np. Microsoft SQL Server, PostgreSQL), atakujący może modyfikować dane.

**Scenariusz:** Usuwanie produktu z koszyka.

**Podatny kod:**
```sql
SELECT * FROM products WHERE id = $product_id
```

**Atak (Payload):**
```sql
10'; DROP TABLE users; --
```

**Co widzi baza danych?**
```sql
SELECT * FROM products WHERE id = 10';
DROP TABLE users;
--
```

**Wynik:**
Baza wykonuje pierwsze zapytanie (wyświetla produkt), a zaraz potem wykonuje drugie – **całkowicie usuwając tabelę użytkowników**. Znak `--` (lub `#` w MySQL) komentarza sprawia, że reszta oryginalnego zapytania jest ignorowana.

---

### 4. Blind SQL Injection (Ślepe wstrzyknięcie)
Sytuacja, w której aplikacja **nie zwraca danych z bazy ani komunikatów błędów**, ale reaguje różnie (np. inną treścią strony lub czasem odpowiedzi) w zależności od tego, czy zapytanie jest prawdziwe, czy fałszywe.

**Scenariusz:** Sprawdzanie dostępności loginu.
**Cel:** Atakujący chce odgadnąć hasło administratora literka po literce.

**Atak (Payload - pytanie logiczne):**
```sql
' AND (SELECT SUBSTRING(password, 1, 1) FROM users WHERE username = 'admin') = 'a' --
```

**Mechanizm:**
1.  Jeśli hasło zaczyna się na literę 'a', strona załaduje się normalnie (**TRUE**).
2.  Jeśli nie, strona załaduje się inaczej lub zwróci pusty wynik (**FALSE**).
3.  Atakujący automatycznie (np. narzędziem SQLMap) sprawdza każdą literę alfabetu dla każdego znaku hasła.

---

### Jak się bronić? (Prepared Statements)

Jedyną skuteczną metodą obrony jest stosowanie **Zapytań Przygotowanych (Prepared Statements)**.

**Bezpieczny kod (PHP/PDO):**
```php
$stmt = $pdo->prepare('SELECT * FROM users WHERE username = :username AND password = :password');

// Dane są wysyłane oddzielnie od zapytania
$stmt->execute(['username' => $user_input, 'password' => $pass_input]);
$user = $stmt->fetch();
```



**Dlaczego to działa?**
Baza danych traktuje dane wejściowe (`:username`) wyłącznie jako **ciąg tekstowy**, a nie jako wykonywalny kod SQL. Nawet jeśli użytkownik wpisze `' OR '1'='1`, baza poszuka użytkownika o dokładnie takiej dziwnej nazwie, zamiast modyfikować logikę zapytania.

