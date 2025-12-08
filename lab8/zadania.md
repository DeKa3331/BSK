zad1
1.pobieranie certyfikatu:
echo | openssl s_client -servername github.com -connect github.com:443 2>/dev/null | openssl x509 -out github.crt
2.wyswietlanie:
cat github.crt 
-----BEGIN CERTIFICATE-----
MIIEoTCCBEigAwIBAgIRAKtmhrVie+gFloITMBKGSfUwCgYIKoZIzj0EAwIwgY8x
CzAJBgNVBAYTAkdCMRswGQYDVQQIExJHcmVhdGVyIE1hbmNoZXN0ZXIxEDAOBgNV
BAcTB1NhbGZvcmQxGDAWBgNVBAoTD1NlY3RpZ28gTGltaXRlZDE3MDUGA1UEAxMu
U2VjdGlnbyBFQ0MgRG9tYWluIFZhbGlkYXRpb24gU2VjdXJlIFNlcnZlciBDQTAe
Fw0yNTAyMDUwMDAwMDBaFw0yNjAyMDUyMzU5NTlaMBUxEzARBgNVBAMTCmdpdGh1
Yi5jb20wWTATBgcqhkjOPQIBBggqhkjOPQMBBwNCAAQgNFxG/yzL+CSarvC7L3ep
H5chNnG6wiYYxR5D/Z1J4MxGnIX8KbT5fCgLoyzHXL9v50bdBIq6y4AtN4gN7gbW
o4IC/DCCAvgwHwYDVR0jBBgwFoAU9oUKOxGG4QR9DqoLLNLuzGR7e64wHQYDVR0O
BBYEFFPIf96emE7HTda83quVPjA9PdHIMA4GA1UdDwEB/wQEAwIHgDAMBgNVHRMB
Af8EAjAAMB0GA1UdJQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjBJBgNVHSAEQjBA
MDQGCysGAQQBsjEBAgIHMCUwIwYIKwYBBQUHAgEWF2h0dHBzOi8vc2VjdGlnby5j
b20vQ1BTMAgGBmeBDAECATCBhAYIKwYBBQUHAQEEeDB2ME8GCCsGAQUFBzAChkNo
dHRwOi8vY3J0LnNlY3RpZ28uY29tL1NlY3RpZ29FQ0NEb21haW5WYWxpZGF0aW9u
U2VjdXJlU2VydmVyQ0EuY3J0MCMGCCsGAQUFBzABhhdodHRwOi8vb2NzcC5zZWN0
aWdvLmNvbTCCAX4GCisGAQQB1nkCBAIEggFuBIIBagFoAHUAlpdkv1VYl633Q4do
NwhCd+nwOtX2pPM2bkakPw/KqcYAAAGU02uUSwAABAMARjBEAiA7i6o+LpQjt6Ae
EjltHhs/TiECnHd0xTeer/3vD1xgsAIgYlGwRot+SqEBCs//frx/YHTPwox9QLdy
7GjTLWHfcMAAdwAZhtTHKKpv/roDb3gqTQGRqs4tcjEPrs5dcEEtJUzH1AAAAZTT
a5PtAAAEAwBIMEYCIQDlrInx7J+3MfqgxB2+Fvq3dMlk1qj4chOw/+HkYVfG0AIh
AMT+JKAQfUuIdBGxfryrGrwsOD3pRs1tyAyykdPGRgsTAHYAyzj3FYl8hKFEX1vB
3fvJbvKaWc1HCmkFhbDLFMMUWOcAAAGU02uUJQAABAMARzBFAiEA1GKW92agDFNJ
IYrMH3gaJdXsdIVpUcZOfxH1FksbuLECIFJCfslINhc53Q0TIMJHdcFOW2tgG4tB
A1dL881tXbMnMCUGA1UdEQQeMByCCmdpdGh1Yi5jb22CDnd3dy5naXRodWIuY29t
MAoGCCqGSM49BAMCA0cAMEQCIHGMp27BBBJ1356lCe2WYyzYIp/fAONQM3AkeE/f
ym0sAiBtVfN3YgIZ+neHEfwcRhhz4uDpc8F+tKmtceWJSicMkA==
-----END CERTIFICATE-----

ladna wersja:
openssl x509 -in github.crt -noout -text

Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            ab:66:86:b5:62:7b:e8:05:96:82:13:30:12:86:49:f5
        Signature Algorithm: ecdsa-with-SHA256
        Issuer: C = GB, ST = Greater Manchester, L = Salford, O = Sectigo Limited, CN = Sectigo ECC Domain Validation Secure Server CA
        Validity
            Not Before: Feb  5 00:00:00 2025 GMT
            Not After : Feb  5 23:59:59 2026 GMT
        Subject: CN = github.com
        Subject Public Key Info:
            Public Key Algorithm: id-ecPublicKey
                Public-Key: (256 bit)
                pub:
                    04:20:34:5c:46:ff:2c:cb:f8:24:9a:ae:f0:bb:2f:
                    77:a9:1f:97:21:36:71:ba:c2:26:18:c5:1e:43:fd:
                    9d:49:e0:cc:46:9c:85:fc:29:b4:f9:7c:28:0b:a3:
                    2c:c7:5c:bf:6f:e7:46:dd:04:8a:ba:cb:80:2d:37:
                    88:0d:ee:06:d6
                ASN1 OID: prime256v1
                NIST CURVE: P-256
        X509v3 extensions:
            X509v3 Authority Key Identifier: 
                F6:85:0A:3B:11:86:E1:04:7D:0E:AA:0B:2C:D2:EE:CC:64:7B:7B:AE
            X509v3 Subject Key Identifier: 
                53:C8:7F:DE:9E:98:4E:C7:4D:D6:BC:DE:AB:95:3E:30:3D:3D:D1:C8
            X509v3 Key Usage: critical
                Digital Signature
            X509v3 Basic Constraints: critical
                CA:FALSE
            X509v3 Extended Key Usage: 
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Certificate Policies: 
                Policy: 1.3.6.1.4.1.6449.1.2.2.7
                  CPS: https://sectigo.com/CPS
                Policy: 2.23.140.1.2.1
            Authority Information Access: 
                CA Issuers - URI:http://crt.sectigo.com/SectigoECCDomainValidationSecureServerCA.crt
                OCSP - URI:http://ocsp.sectigo.com
            CT Precertificate SCTs: 
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : 96:97:64:BF:55:58:97:AD:F7:43:87:68:37:08:42:77:
                                E9:F0:3A:D5:F6:A4:F3:36:6E:46:A4:3F:0F:CA:A9:C6
                    Timestamp : Feb  5 00:03:50.475 2025 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:44:02:20:3B:8B:AA:3E:2E:94:23:B7:A0:1E:12:39:
                                6D:1E:1B:3F:4E:21:02:9C:77:74:C5:37:9E:AF:FD:EF:
                                0F:5C:60:B0:02:20:62:51:B0:46:8B:7E:4A:A1:01:0A:
                                CF:FF:7E:BC:7F:60:74:CF:C2:8C:7D:40:B7:72:EC:68:
                                D3:2D:61:DF:70:C0
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : 19:86:D4:C7:28:AA:6F:FE:BA:03:6F:78:2A:4D:01:91:
                                AA:CE:2D:72:31:0F:AE:CE:5D:70:41:2D:25:4C:C7:D4
                    Timestamp : Feb  5 00:03:50.381 2025 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:46:02:21:00:E5:AC:89:F1:EC:9F:B7:31:FA:A0:C4:
                                1D:BE:16:FA:B7:74:C9:64:D6:A8:F8:72:13:B0:FF:E1:
                                E4:61:57:C6:D0:02:21:00:C4:FE:24:A0:10:7D:4B:88:
                                74:11:B1:7E:BC:AB:1A:BC:2C:38:3D:E9:46:CD:6D:C8:
                                0C:B2:91:D3:C6:46:0B:13
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : CB:38:F7:15:89:7C:84:A1:44:5F:5B:C1:DD:FB:C9:6E:
                                F2:9A:59:CD:47:0A:69:05:85:B0:CB:14:C3:14:58:E7
                    Timestamp : Feb  5 00:03:50.437 2025 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:45:02:21:00:D4:62:96:F7:66:A0:0C:53:49:21:8A:
                                CC:1F:78:1A:25:D5:EC:74:85:69:51:C6:4E:7F:11:F5:
                                16:4B:1B:B8:B1:02:20:52:42:7E:C9:48:36:17:39:DD:
                                0D:13:20:C2:47:75:C1:4E:5B:6B:60:1B:8B:41:03:57:
                                4B:F3:CD:6D:5D:B3:27
            X509v3 Subject Alternative Name: 
                DNS:github.com, DNS:www.github.com
    Signature Algorithm: ecdsa-with-SHA256
    Signature Value:
        30:44:02:20:71:8c:a7:6e:c1:04:12:75:df:9e:a5:09:ed:96:
        63:2c:d8:22:9f:df:00:e3:50:33:70:24:78:4f:df:ca:6d:2c:
        02:20:6d:55:f3:77:62:02:19:fa:77:87:11:fc:1c:46:18:73:
        e2:e0:e9:73:c1:7e:b4:a9:ad:71:e5:89:4a:27:0c:90


3Przeanalizuj certyfikat i odczytaj z niego następujące informacje (używając narzędzia OpenSSL):
• Dla jakiej domeny wystawiony jest certyfikat?
 Subject: CN = github.com
• Kto wystawił certyfikat (CA)?

• Kiedy certyfikat został wystawiony i kiedy wygasa?
Validity:
Not Before: Feb 5 00:00:00 2025 GMT
Not After : Feb 5 23:59:59 2026 GMT

• Jakie dodatkowe domeny są obsługiwane?
Subject Alternative Name: 
                DNS:github.com, DNS:www.github.com

• Jaki algorytm i długość klucza?
Public Key Algorithm: id-ecPublicKey
Public-Key: (256 bit)
ASN1 OID: prime256v1
NIST CURVE: P-256
Signature Algorithm: ecdsa-with-SHA256

• Do czego może być użyty certyfikat?
Key Usage: Digital Signature
Extended Key Usage:
 - TLS Web Server Authentication
 - TLS Web Client Authentication

• Ile certyfikatów znajduje się w łańcuchu zaufania?

• Kto jest głównym CA (root CA) w łańcuchu?



Specjalne polecenia:

Dla jakiej domeny wystawiony jest certyfikat?
openssl x509 -in github.crt -noout -subject
subject=CN = github.com
• Kto wystawił certyfikat (CA)?
openssl x509 -in github.crt -noout -issuer
issuer=C = GB, ST = Greater Manchester, L = Salford, O = Sectigo Limited, CN = Sectigo ECC Domain Validation Secure Server CA

w tym wypadku
Sectigo ECC Domain Validation Secure Server CA


• Kiedy certyfikat został wystawiony i kiedy wygasa?
openssl x509 -in github.crt -noout -dates
notBefore=Feb  5 00:00:00 2025 GMT
notAfter=Feb  5 23:59:59 2026 GMT

• Jakie dodatkowe domeny są obsługiwane?
openssl x509 -in github.crt -ext subjectAltName -noout
X509v3 Subject Alternative Name: 
    DNS:github.com, DNS:www.github.com

• Jaki algorytm i długość klucza?
openssl x509 -in github.crt -text -noout | grep "Public-Key"


• Do czego może być użyty certyfikat?
openssl x509 -in github.crt -ext extendedKeyUsage -noout
X509v3 Extended Key Usage: 
    TLS Web Server Authentication, TLS Web Client Authentication


• Ile certyfikatów znajduje się w łańcuchu zaufania?



• Kto jest głównym CA (root CA) w łańcuchu?
openssl x509 -in github.crt -text -noout | grep "Public Key Algorithm"
            Public Key Algorithm: id-ecPublicKey


pytanie dodatkowe o fingerprint:
openssl x509 -in github.crt -noout -fingerprint -sha256
sha256 Fingerprint=B8:BB:81:87:68:33:87:39:42:04:5A:8D:F8:F0:62:19:E0:06:02:EB:CB:43:84:C7:AB:C2:4F:18:37:9C:87:F5


4) WYODREBNIANIE:
openssl x509 -in github.crt -noout -pubkey > github.pubkey

cat:
-----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEIDRcRv8sy/gkmq7wuy93qR+XITZx
usImGMUeQ/2dSeDMRpyF/Cm0+XwoC6Msx1y/b+dG3QSKusuALTeIDe4G1g==
-----END PUBLIC KEY-----


6.2
pobieranie z przekierowaniem do pliku:

openssl s_client -connect github.com:443 -showcerts </dev/null > gh.txt 2>/dev/null > github.txt

6.3
sudo docker run -p 8443:443 --name tls3 docker.io/mazurkatarzyna/tls-ex3:latest

echo | openssl s_client -servername 127.0.0.1 -connect 127.0.0.1:8443 2>/dev/null | openssl x509 -out strona.crt
deka@SKH-KUBUNTU:~$ cat strona.crt
-----BEGIN CERTIFICATE-----
MIIDpzCCAo+gAwIBAgIUH9b0yv1zMuQeN+fqOhJyqjZzJ5gwDQYJKoZIhvcNAQEL
BQAwYzELMAkGA1UEBhMCUEwxEjAQBgNVBAgMCUx1YmVsc2tpZTEPMA0GA1UEBwwG
THVibGluMQ0wCwYDVQQKDARVTUNTMQwwCgYDVQQLDANNRkkxEjAQBgNVBAMMCWxv
Y2FsaG9zdDAeFw0yNTEyMDQxNzI5MThaFw0yNjEyMDQxNzI5MThaMGMxCzAJBgNV
BAYTAlBMMRIwEAYDVQQIDAlMdWJlbHNraWUxDzANBgNVBAcMBkx1YmxpbjENMAsG
A1UECgwEVU1DUzEMMAoGA1UECwwDTUZJMRIwEAYDVQQDDAlsb2NhbGhvc3QwggEi
MA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDXWuFKJP3hfruNdPk+D0grIa9j
I3PVnGi/IE/IRJSFpQg9K+4juPRkBfqWDBlNaAC+40IVYfX8vvpGiml38DAjPgTW
akEegSR7Ct21TCJ3p6DWgqNu2MWnfClbA/PP6XAfCGRfgrQ5tT68vK5GOfuzqjY7
doQD0Tuzypv7MTlmINruRwSSaW7Hn4uciK5WAroAdiBJyVS/DprhALpvwbQK4reB
2Kuw196sUPOwWJfeOUFxpmnsuMgMJRT/uaLk20TGQnNZ7mS7hkVV6qnVpep+7TrQ
bkYYl7mxD/X3XuiOKOyNmCogLyiqH/yuIRTKmsIz8K7wp48weXkKPJ1XMv55AgMB
AAGjUzBRMB0GA1UdDgQWBBQreQ4JY/vGWi+Ebzvxa2pdHq7JxjAfBgNVHSMEGDAW
gBQreQ4JY/vGWi+Ebzvxa2pdHq7JxjAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4IBAQDPKK2Dz9aMMJWnjUdvhI7QW0W/pHsqvWe2ge0i5cx4MF+v7/0Z
u7M7yPS2kBeLBLbJzu4nbMyguewubnhdL4zGz/ZZqbavMBQkmhZVqEQEjzXoCqSt
p9AOcyQF+ksh4ax8ebFQmc3gpPPTuA58bMcdLLInSprWFZ5DdbxW02AtpNsBD8io
2BF8FEAKUmbvZKPYjCiNHdkRdmOkX8KD8H4ZB4RhPOfymrVrNCzgDle0NTRdBtWs
2XNhaU37IIQVxMcRknRXT0UEyybb3XyU0N1yaRLXB75oKj41hI8XDSlZx7PDzlhE
xh5yZKcXHNxRXMOdKbxZpYELu/BKCDC3/Q3L
-----END CERTIFICATE-----

ladnie:
openssl x509 -in strona.crt -noout -text

Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            1f:d6:f4:ca:fd:73:32:e4:1e:37:e7:ea:3a:12:72:aa:36:73:27:98
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = PL, ST = Lubelskie, L = Lublin, O = UMCS, OU = MFI, CN = localhost
        Validity
            Not Before: Dec  4 17:29:18 2025 GMT
            Not After : Dec  4 17:29:18 2026 GMT
        Subject: C = PL, ST = Lubelskie, L = Lublin, O = UMCS, OU = MFI, CN = localhost
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (2048 bit)
                Modulus:
                    00:d7:5a:e1:4a:24:fd:e1:7e:bb:8d:74:f9:3e:0f:
                    48:2b:21:af:63:23:73:d5:9c:68:bf:20:4f:c8:44:
                    94:85:a5:08:3d:2b:ee:23:b8:f4:64:05:fa:96:0c:
                    19:4d:68:00:be:e3:42:15:61:f5:fc:be:fa:46:8a:
                    69:77:f0:30:23:3e:04:d6:6a:41:1e:81:24:7b:0a:
                    dd:b5:4c:22:77:a7:a0:d6:82:a3:6e:d8:c5:a7:7c:
                    29:5b:03:f3:cf:e9:70:1f:08:64:5f:82:b4:39:b5:
                    3e:bc:bc:ae:46:39:fb:b3:aa:36:3b:76:84:03:d1:
                    3b:b3:ca:9b:fb:31:39:66:20:da:ee:47:04:92:69:
                    6e:c7:9f:8b:9c:88:ae:56:02:ba:00:76:20:49:c9:
                    54:bf:0e:9a:e1:00:ba:6f:c1:b4:0a:e2:b7:81:d8:
                    ab:b0:d7:de:ac:50:f3:b0:58:97:de:39:41:71:a6:
                    69:ec:b8:c8:0c:25:14:ff:b9:a2:e4:db:44:c6:42:
                    73:59:ee:64:bb:86:45:55:ea:a9:d5:a5:ea:7e:ed:
                    3a:d0:6e:46:18:97:b9:b1:0f:f5:f7:5e:e8:8e:28:
                    ec:8d:98:2a:20:2f:28:aa:1f:fc:ae:21:14:ca:9a:
                    c2:33:f0:ae:f0:a7:8f:30:79:79:0a:3c:9d:57:32:
                    fe:79
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Subject Key Identifier: 
                2B:79:0E:09:63:FB:C6:5A:2F:84:6F:3B:F1:6B:6A:5D:1E:AE:C9:C6
            X509v3 Authority Key Identifier: 
                2B:79:0E:09:63:FB:C6:5A:2F:84:6F:3B:F1:6B:6A:5D:1E:AE:C9:C6
            X509v3 Basic Constraints: critical
                CA:TRUE
    Signature Algorithm: sha256WithRSAEncryption
    Signature Value:
        cf:28:ad:83:cf:d6:8c:30:95:a7:8d:47:6f:84:8e:d0:5b:45:
        bf:a4:7b:2a:bd:67:b6:81:ed:22:e5:cc:78:30:5f:af:ef:fd:
        19:bb:b3:3b:c8:f4:b6:90:17:8b:04:b6:c9:ce:ee:27:6c:cc:
        a0:b9:ec:2e:6e:78:5d:2f:8c:c6:cf:f6:59:a9:b6:af:30:14:
        24:9a:16:55:a8:44:04:8f:35:e8:0a:a4:ad:a7:d0:0e:73:24:
        05:fa:4b:21:e1:ac:7c:79:b1:50:99:cd:e0:a4:f3:d3:b8:0e:
        7c:6c:c7:1d:2c:b2:27:4a:9a:d6:15:9e:43:75:bc:56:d3:60:
        2d:a4:db:01:0f:c8:a8:d8:11:7c:14:40:0a:52:66:ef:64:a3:
        d8:8c:28:8d:1d:d9:11:76:63:a4:5f:c2:83:f0:7e:19:07:84:
        61:3c:e7:f2:9a:b5:6b:34:2c:e0:0e:57:b4:35:34:5d:06:d5:
        ac:d9:73:61:69:4d:fb:20:84:15:c4:c7:11:92:74:57:4f:45:
        04:cb:26:db:dd:7c:94:d0:dd:72:69:12:d7:07:be:68:2a:3e:
        35:84:8f:17:0d:29:59:c7:b3:c3:ce:58:44:c6:1e:72:64:a7:
        17:1c:dc:51:5c:c3:9d:29:bc:59:a5:81:0b:bb:f0:4a:08:30:
        b7:fd:0d:cb


3.skipuje bo komendy mamy wyzej w wiekszosci


zad6.4







zad6.5
uruchomienie:
sudo docker run -p 8447:443 --name tls6 docker.io/mazurkatarzyna/tls-ex6:latest

pobiereanie pliku:
curl http://127.0.0.1:8447/cert -o cert.pem


wyodrebnienie klucza:
openssl x509 -in cert.pem -pubkey -noout > publicziny_key.pem



curl -X POST -F "public_key=@publicziny_key.pem" http://127.0.0.1:8447/public


kiedy wygasa:
openssl x509 -in cert.pem -noout -enddate
notAfter=Jul 29 10:02:41 2026 GMT

wystawiony:
openssl x509 -in cert.pem -noout -startdate
notBefore=Dec  8 10:02:41 2025 GMT

albo w skrocie
openssl x509 -in cert.pem -noout -dates
i samodizelnie rozdzelic

wydawca:
openssl x509 -in cert.pem -noout -issuer
issuer=CN = IdenTrust Authority, O = IdenTrust, C = PL
deka@SKH-KUBUNTU:~$ 

algorytm i rozmiar:
openssl x509 -in cert.pem -text -noout | grep "Public Key Algorithm"
Public Key Algorithm: rsaEncryption
               

rozmiar:
openssl x509 -in cert.pem -text -noout | grep "Public-Key"
Public-Key: (4096 bit)

glowna domena:
openssl x509 -in cert.pem -noout -subject
subject=CN = api233.pl, O = Org 740, C = PL

alternatywne:
openssl x509 -in cert.pem -ext subjectAltName -noout
X509v3 Subject Alternative Name: 
    DNS:api233.pl, DNS:secure672.pl, DNS:secure929.io, DNS:secure796.net

uzycie:
openssl x509 -in cert.pem -ext keyUsage -noout
X509v3 Key Usage: critical
    Digital Signature, Key Encipherment

alternatywne uzycie:
openssl x509 -in cert.pem -ext extendedKeyUsage -noout
X509v3 Extended Key Usage: critical
    TLS Web Server Authentication



curl -X POST "http://127.0.0.1:8447/validate" \
-H "accept: application/json" \
-H "Content-Type: application/json" \
-d '{
  "expiry_date": "Jul 29 10:02:41 2026 GMT",
  "issued_date": "Dec  8 10:02:41 2025 GMT",
  "issuer": "CN = IdenTrust Authority, O = IdenTrust, C = PL",
  "key_algorithm": "rsa",
  "key_size": 4096,
  "key_usage": [
    "Digital Signature",
    "key encipherment"
  ],
  "primary_domain": "api233.pl",
  "san_domains": [
    "api233.pl",
    "secure672.pl",
    "secure929.io",
    "secure796.net"
  ]
}'


WYNIK 100%:

{
  "percentage": "100%",
  "results": {
    "dates": {
      "correct": true,
      "your_expiry": "Jul 29 10:02:41 2026 GMT",
      "your_issued": "Dec  8 10:02:41 2025 GMT"
    },
    "issuer": {
      "correct": true,
      "expected": "IdenTrust Authority",
      "your_answer": "CN = IdenTrust Authority, O = IdenTrust, C = PL"
    },
    "key_info": {
      "correct": true,
      "your_algorithm": "RSA",
      "your_key_size": "4096"
    },
    "key_usage": {
      "correct": true,
      "expected": [
        "digital signature",
        "key encipherment"
      ],
      "your_answer": [
        "digital signature",
        "key encipherment"
      ]
    },
    "primary_domain": {
      "correct": true,
      "expected": "api233.pl",
      "your_answer": "api233.pl"
    },
    "san_domains": {
      "correct": true,
      "expected": [
        "secure796.net",
        "secure929.io",
        "secure672.pl",
        "api233.pl"
      ],
      "your_answer": [
        "secure796.net",
        "secure929.io",
        "secure672.pl",
        "api233.pl"
      ]
    }
  },
  "score": "6/6"
}




zad6.6
zamiast bawic sie wiresharkiem to pobralem z kampusa ex66.zip

unzip ex66.zip

tym sie bede musial pobawic bo ogarnialem wiresharka na linuxe



















