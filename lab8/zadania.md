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























