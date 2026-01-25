# Protokół HTTP: Kluczowe Informacje

**Protokół HTTP (Hypertext Transfer Protocol)** stanowi fundament komunikacji w sieci World Wide Web, pełniąc funkcję protokołu **warstwy aplikacji** do przesyłania zasobów, takich jak dokumenty HTML, pliki graficzne czy wyniki zapytań.

Działa w modelu **zapytanie-odpowiedź** (Client-Server), gdzie klient (np. przeglądarka internetowa) wysyła żądanie o zasób, a serwer zwraca odpowiedź. Do wersji 1.1 HTTP jest **protokołem tekstowym**, co oznacza, że jego komendy są czytelne dla człowieka.

---

## 1. Wprowadzenie i Podstawowe Cechy

HTTP jest zdefiniowany w dokumentach **RFC 2616** oraz **7230-7235**. Jest to protokół bezstanowy, standardowo wykorzystujący protokół TCP/IP.

### 1.1. Porty Komunikacyjne
Komunikacja odbywa się zazwyczaj przez gniazda TCP/IP na portach:
* **Port 80:** Dla połączeń niezabezpieczonych.
* **Port 443:** Dla połączeń zabezpieczonych (HTTPS).

### 1.2. Główne Cechy Protokołu
* **Przeznaczenie:** Służy do przesyłania różnorodnych zasobów (plików) w sieci WWW (pliki statyczne, dynamiczne odpowiedzi).
* **Charakter tekstowy:** W wersjach do 1.1 polecenia są sformułowane w postaci czytelnego tekstu (podobnie jak w SMTP czy POP3).
* **Model komunikacji:** Klient inicjuje komunikację wysyłając zapytanie; serwer przetwarza je i odsyła odpowiedź (treść lub błąd).

---

## 2. Struktura Wiadomości HTTP

Formaty żądań i odpowiedzi w protokole HTTP są do siebie bardzo podobne. Każda wiadomość składa się z czterech fundamentalnych części:

1.  **Linia początkowa:** Inna dla żądania (Request Line), inna dla odpowiedzi (Status Line).
2.  **Nagłówki:** Zero lub więcej linii w formacie `Nazwa: Wartość`. Sterują zachowaniem klienta i serwera.
3.  **Pusta linia:** Para znaków **CRLF** (`\r\n`), która jednoznacznie oddziela sekcję nagłówków od ciała wiadomości.
4.  **Ciało wiadomości (Body):** Opcjonalna zawartość (np. kod HTML w odpowiedzi, dane formularza w żądaniu).

> **Ważne:** Każda linia w sekcji początkowej i nagłówków musi być zakończona parą znaków **CRLF** (`\r\n`).

### 2.1. Określanie Końca Odpowiedzi
Aby klient wiedział, że odebrał kompletną wiadomość, analizuje nagłówki:
* **Content-Length:** Określa rozmiar ciała odpowiedzi w bajtach.
* **Transfer-Encoding:** Np. `chunked` – wskazuje na specyficzny mechanizm przesyłania danych fragmentami.
* *Brak nagłówków:* Klient odbiera dane do momentu, aż serwer zamknie połączenie.

---

## 3. Żądania HTTP (Requests)

Żądanie HTTP wysyłane przez klienta ma ściśle określoną strukturę.

### 3.1. Ogólny Format Żądania
```http
Method Request-URI HTTP-Version
HEADER1: VALUE1
HEADER2: VALUE2
...
HEADERX: VALUEX

BODY
```
* **Method:** Metoda HTTP określająca rodzaj operacji.
* **Request-URI:** Ścieżka do zasobu na serwerze (może zawierać parametry).
* **HTTP-Version:** Wersja protokołu (np. HTTP/1.1).

### 3.2. Metody HTTP
Tabela dostępnych metod i ich przeznaczenie:

| Metoda | Opis |
| :--- | :--- |
| **GET** | Pobranie zasobu wskazanego przez URI. |
| **HEAD** | Pobranie samych nagłówków (informacji o zasobie), bez jego treści. |
| **PUT** | Przesłanie danych w celu aktualizacji/nadpisania istniejącego zasobu. |
| **POST** | Przesłanie danych do przetworzenia (np. formularz, utworzenie nowego zasobu). |
| **DELETE** | Żądanie usunięcia zasobu wskazanego przez URI. |
| **OPTIONS** | Żądanie informacji o opcjach komunikacji dla danego zasobu. |
| **TRACE** | Diagnostyka kanału komunikacyjnego; serwer odsyła otrzymane żądanie. |
| **CONNECT** | Tworzenie tuneli przez serwery pośredniczące (proxy). |
| **PATCH** | Częściowa aktualizacja zasobu (np. zmiana jednego pola). |

---

## 4. Odpowiedzi HTTP (Responses)

Odpowiedź serwera na żądanie klienta również posiada standardowy format.

### 4.1. Ogólny Format Odpowiedzi
```http
HTTP-Version Status-Code Reason-Phrase
HEADER1: VALUE1
HEADER2: VALUE2
...
HEADERX: VALUEX

BODY
```
* **Status-Code:** Trzycyfrowy kod numeryczny wyniku.
* **Reason-Phrase:** Tekstowy opis powiązany z kodem statusu.

### 4.2. Kategorie Kodów Statusu
Pierwsza cyfra kodu statusu określa klasę odpowiedzi:

| Kategoria | Nazwa | Opis |
| :--- | :--- | :--- |
| **1xx** | Informacyjne | Żądanie odebrane, proces jest kontynuowany. |
| **2xx** | Powodzenia | Żądanie pomyślnie odebrane, zrozumiane i zaakceptowane. |
| **3xx** | Przekierowania | Klient musi podjąć dodatkowe działania (np. zmiana adresu). |
| **4xx** | Błędy Klienta | Błąd składni lub niemożność realizacji żądania (np. 404). |
| **5xx** | Błędy Serwera | Serwer nie zdołał zrealizować poprawnego żądania (błąd wewnętrzny). |

---

## 5. Kategorie Nagłówków HTTP

Nagłówki HTTP można podzielić na cztery główne kategorie:

1.  **General Header Fields:** Nagłówki ogólne (np. data), mogą występować w żądaniach i odpowiedziach, nie dotyczą treści (encji).
2.  **Entity Header Fields:** Opisują metadane ciała wiadomości (np. typ, długość) lub zasobu.
3.  **Request Header Fields:** Specyficzne dla żądań (informacje o kliencie, preferencje).
4.  **Response Header Fields:** Specyficzne dla odpowiedzi (informacje o serwerze, dostęp do zasobu).

---

## 6. Przykłady Komunikacji HTTP

### Przykład 1: Standardowe pobranie strony (GET 200 OK)
**Żądanie:**
```http
GET /index.html HTTP/1.1
HOST: 212.182.24.27
```
**Odpowiedź:**
```http
HTTP/1.1 200 OK
Date: Thu, 13 Apr 2017 14:25:38 GMT
Server: Apache/2.4.18 (Ubuntu)
Last-Modified: Thu, 13 Apr 2017 13:57:13 GMT
Content-Length: 11321
Content-Type: text/html

<!DOCTYPE html PUBLIC ...>
<html>...</html>
```

### Przykład 2: Metoda niedozwolona (TRACE 405)
**Żądanie:**
```http
TRACE / HTTP/1.1
HOST: 212.182.24.27
```
**Odpowiedź:**
```http
HTTP/1.1 405 Method Not Allowed
Allow: 
Content-Length: 302
Content-Type: text/html; charset=iso-8859-1

<h1>Method Not Allowed</h1>
<p>The requested method TRACE is not allowed for the URL /.</p>
```

### Przykład 3: Sprawdzenie opcji serwera (OPTIONS 200)
**Żądanie:**
```http
OPTIONS /index.html HTTP/1.1
HOST: 212.182.24.27
```
**Odpowiedź:**
```http
HTTP/1.1 200 OK
Allow: OPTIONS,GET,HEAD,POST
Content-Length: 0
Content-Type: text/html
```

### Przykład 4: Pobranie samych nagłówków (HEAD 200)
**Żądanie:**
```http
HEAD /index.html HTTP/1.1
HOST: 212.182.24.27
```
**Odpowiedź (brak ciała):**
```http
HTTP/1.1 200 OK
Date: Thu, 13 Apr 2017 14:53:06 GMT
Content-Length: 11321
Content-Type: text/html
```
