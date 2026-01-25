# Certyfikaty TLS i Infrastruktura PKI

Certyfikaty **TLS (Transport Layer Security)** są podstawowym mechanizmem zapewniającym **poufność, integralność i uwierzytelnienie** w komunikacji sieciowej, stanowiąc trzon protokołu **HTTPS**.

Ich działanie opiera się na hierarchicznym modelu zaufania **PKI (Public Key Infrastructure)**, w którym zaufane **Główne Urzędy Certyfikacji (Root CA)** podpisują certyfikaty **Pośrednich Urzędów Certyfikacji (Intermediate CA)**, a te z kolei certyfikaty końcowe (np. serwerów).

---

## 1. Fundamenty Infrastruktury Klucza Publicznego (PKI)

**Infrastruktura Klucza Publicznego (PKI)** to kompleksowy system, który stanowi podstawę dla bezpiecznego zarządzania cyfrowymi certyfikatami i kluczami publicznymi.

### 1.1. Definicja i Cele PKI
PKI jest zdefiniowane jako zestaw technologii, procedur oraz podmiotów, którego celem jest umożliwienie bezpiecznego zarządzania tożsamością cyfrową. Kluczowe funkcje to:

* **Wiarygodna identyfikacja:** Umożliwia weryfikację tożsamości podmiotów uczestniczących w komunikacji.
* **Podpisywanie i weryfikacja:** Dostarcza mechanizmów do cyfrowego podpisywania certyfikatów i późniejszej weryfikacji tych podpisów.
* **Hierarchia zaufania:** Tworzy strukturę, w której zaufanie jest delegowane od głównych urzędów do jednostek niższego rzędu.
* **Unieważnianie certyfikatów:** Zapewnia procedury (np. **listy CRL**) do unieważniania certyfikatów, które zostały skompromitowane.

### 1.2. Kluczowe Komponenty PKI
System PKI składa się z kilku fundamentalnych elementów utrzymujących łańcuch zaufania:

* **Root CA (Główny Urząd Certyfikacji):** Podmiot o **najwyższym poziomie zaufania**, którego certyfikaty są wbudowane w systemy operacyjne i przeglądarki.
* **Intermediate CA (Pośredni Urząd Certyfikacji):** Urzędy, których certyfikaty są podpisane przez Root CA. Służą do podpisywania certyfikatów końcowych.
* **RA (Urząd Rejestracji):** Instytucja odpowiedzialna za weryfikację tożsamości podmiotów ubiegających się o certyfikat.
* **Repozytoria Certyfikatów i CRL:** Bazy danych przechowujące ważne certyfikaty oraz listy certyfikatów unieważnionych (Certificate Revocation List).
* **Podmioty Końcowe:** Użytkownicy końcowi certyfikatów, tacy jak serwery HTTPS.

### 1.3. Hierarchia i Model Zaufania
Model zaufania w PKI jest ściśle hierarchiczny. Przeglądarka ufa certyfikatowi serwera tylko wtedy, gdy jest w stanie zweryfikować **cały łańcuch podpisów**, prowadzący od certyfikatu serwera, przez certyfikat pośredni, aż do certyfikatu głównego (Root CA).

1.  **Krok 1:** Root CA podpisuje certyfikat Intermediate CA.
2.  **Krok 2:** Intermediate CA podpisuje certyfikat serwera.
3.  **Krok 3:** Klient/przeglądarka weryfikuje podpisy w odwrotnej kolejności (**Bottom-Up**), aby potwierdzić autentyczność.

---

## 2. Certyfikaty TLS w Praktyce

Certyfikaty TLS są praktycznym zastosowaniem koncepcji PKI w celu zabezpieczenia komunikacji sieciowej.

### 2.1. Proces Generowania i Podpisywania
Proces uzyskania zaufanego certyfikatu przebiega następująco:

1.  **Generowanie Pary Kluczy:** Na serwerze tworzona jest para kluczy: **prywatny** (tajny) i **publiczny**.
2.  **Tworzenie CSR (Certificate Signing Request):** Generowane jest żądanie zawierające klucz publiczny oraz dane identyfikacyjne (np. domenę).
3.  **Wysyłka CSR do CA:** Żądanie jest przesyłane do wybranego Urzędu Certyfikacji.
4.  **Weryfikacja i Podpisanie:** CA weryfikuje tożsamość i podpisuje certyfikat swoim kluczem prywatnym.
5.  **Wydanie Certyfikatu:** Podpisany certyfikat TLS jest instalowany na serwerze.

### 2.2. Główne Zastosowanie
Certyfikaty TLS realizują dwa kluczowe zadania:
* **Uwierzytelnienie serwera:** Zapewnienie użytkownika, że łączy się z autentycznym serwerem.
* **Szyfrowanie komunikacji:** Ochrona przesyłanych danych przed podsłuchem i modyfikacją.

> **Ważne:** Mechanizm ten chroni przed atakami typu **man-in-the-middle**, w których atakujący podszywa się pod prawdziwy serwer.

### 2.3. Zawartość i Algorytmy
Certyfikat TLS zawiera **klucz publiczny serwera** oraz informacje identyfikacyjne. Do operacji kryptograficznych wykorzystywane są algorytmy takie jak **RSA**, **ECDSA** oraz **Ed25519**.

---

## 3. Protokół Uzgadniania TLS (TLS Handshake)

Proces nawiązywania bezpiecznego połączenia, zwany **TLS Handshake**, to sekwencja kroków, której celem jest uwierzytelnienie serwera, uzgodnienie parametrów szyfrowania i wygenerowanie kluczy sesyjnych.

| Krok | Źródło | Komunikat | Opis Działania |
| :--- | :--- | :--- | :--- |
| **1** | Klient | **Client Hello** | Klient wysyła listę obsługiwanych szyfrów, losową liczbę, Session ID oraz nazwę serwera (**SNI**). |
| **2** | Serwer | **Server Hello** | Serwer wybiera szyfr, wysyła własną losową liczbę oraz Session ID. |
| **3** | Serwer | **Server Certificates** | Serwer przesyła swój **certyfikat cyfrowy** (lub łańcuch) do weryfikacji. |
| **4** | Serwer | **Server Hello Done** | Serwer informuje o zakończeniu wysyłania komunikatów początkowych. |
| **5** | Klient | **Client Key Exchange** | Klient generuje tzw. **"pre-master secret"**, szyfruje go kluczem publicznym serwera i wysyła. |
| **6** | Obie strony | **Key Generation** | Strony niezależnie używają losowych liczb i "pre-master secret" do wygenerowania **identycznych kluczy sesyjnych**. |
| **7** | Obie strony | **Cipher Spec. Exchange** | Komunikat informujący, że od tej pory komunikacja będzie szyfrowana kluczami sesyjnymi. |
| **8** | Klient | **Finished** | Klient wysyła zaszyfrowaną wiadomość kontrolną (weryfikacja sukcesu). |
| **9** | Serwer | **Finished** | Serwer wysyła własną zaszyfrowaną wiadomość kontrolną. |

Po pomyślnym zakończeniu następuje faza **Record Protocol** (przesyłanie zaszyfrowanych danych aplikacji).

---

## 4. Certyfikaty Samopodpisane (Self-Signed)

Certyfikaty samopodpisane stanowią szczególną kategorię, która jest technicznie poprawna, ale celowo funkcjonuje **poza globalnym systemem zaufania PKI**.

### 4.1. Definicja i Charakterystyka
**Certyfikat samopodpisany (self-signed)** to certyfikat, który został podpisany **własnym kluczem prywatnym** jego twórcy, a nie kluczem zaufanego CA. W takim certyfikacie **wystawca (issuer) i podmiot (subject) są tym samym bytem**. Nie należy on do globalnej hierarchii zaufania.

### 4.2. Scenariusze Użycia
* **Środowiska testowe i deweloperskie:** Testowanie TLS bez ponoszenia kosztów.
* **Systemy wewnętrzne:** Zamknięte sieci korporacyjne (wymaga ręcznego dodania do zaufanych na urządzeniach).
* **Prywatne PKI:** Służą jako certyfikat główny dla wewnętrznej infrastruktury.

### 4.3. Powody Ostrzeżeń w Przeglądarkach
Przeglądarki wyświetlają ostrzeżenia bezpieczeństwa, ponieważ **nie są w stanie zweryfikować autentyczności** certyfikatu samopodpisanego:
1.  Certyfikat nie jest podpisany przez żaden z urzędów **Root CA** wbudowanych w przeglądarkę.
2.  Nie można zbudować **łańcucha zaufania**.
3.  Traktowane jest to jako potencjalne ryzyko podsłuchu lub podszywania się.
