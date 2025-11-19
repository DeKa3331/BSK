WAZNA SPRAWA DO ZAPYTANIA  W ZADANIU 3.5 WYSYLAJAC ZAPYTANIE DO KONSOLI DOSTAJE KLUCZ ALE NIE PRIVATE KOD JA GO WZIALEM Z DOCSOW ZAPYTAC!

w 3.6 np wogole nie generuje sesion_id

zad3.1
-generuje dwa klucze publiczny i prywatny, aktualnie w pliku mamy tylko prywany:
openssl genpkey -algorithm RSA -out priv.pem -pkeyopt rsa_keygen_bits:1024



-wyswietlanie klucza prywatnego jako tekst:
 openssl pkey -noout -text -in priv.pem

-generacja publicznego na podstawie wczesniejszego prywatnego:
openssl pkey -in priv.pem -pubout -out pub.pem

deka@SKH-KUBUNTU:~$ cat pub.pem
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC877JWFlI2DTbqoeMy4S6zXu0H
1P0ZOwnBeZF3AxNC+SzyiFwUdfccjQJpdIrCU/DSt1ZdyqnP+MheuOCl+WVpfeyC
gTzhkLQWpHUUGznaPIr/ZVT1F+xxpnXS6aYr4TXbhYfaYsWYG6T78IPIciHrSaNf
7+HEL5TRPZTIEu4SPwIDAQAB
-----END PUBLIC KEY-----


wyswietlanie zakodowanego base64 kodu publicznego
openssl pkey -in priv.pem -text_pub -noout


klucz publiczny upload:

curl -X 'POST' \
  'http://127.0.0.1:3001/upload/public' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@pub.pem;type=application/x-x509-ca-cert'

curl -X 'POST' \
  'http://127.0.0.1:3001/upload/private' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@priv.pem;type=application/x-x509-ca-cert'

zad3.2

generacja za pomoca krzywej:
openssl genpkey -algorithm EC -pkeyopt ec_paramgen_curve:prime256v1 -out ecpriv.pem
  'http://127.0.0.1:3001/upload/private' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@priv.pem;type=application/x-x509-ca-cert'


  z prywatnego publiczny:
openssl ec -in ecpriv.pem -pubout -out ecpub.pem
upload publiczny;
curl -X 'POST' \
  'http://127.0.0.1:3002/upload/ec/public' \
  -H 'accept: */*' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@ecpub.pem;type=application/x-x509-ca-cert'

  upload prywatny:
curl -X 'POST' \
  'http://127.0.0.1:3002/upload/ec/private' \
  -H 'accept: */*' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@ecpriv.pem;type=application/x-x509-ca-cert'

  zad3.3 
  zrobione jako 1sze poprostu dlugosc losowa akurat sie trafila

  zad3.4

  generacja klucza za pomoca requesta get:
curl -X 'GET' \
  'http://127.0.0.1:3004/getprivkey' \
  -H 'accept: */*'


zajeciowa wersja (bez ostatniego):
curl -X GET http://127.0.0.1:3004/getprivkey

 zapis do pliku wygenerowanego klucza:
curl -X GET http://127.0.0.1:3004/getprivkey -o genpriv.pem


sprawdzenie dlugosc klucza:
deka@SKH-KUBUNTU:~$ openssl rsa -in genpriv.pem -text -noout | grep "Private-Key"
Private-Key: (2048 bit, 2 primes)

generacja publicznego:
openssl pkey -in genpriv.pem -pubout -out public_key.pem


curl -X 'POST' \
  'http://127.0.0.1:3004/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'session_id=c483f0e678457dd5' \
  -F 'public_key_file=@public_key.pem;type=application/x-x509-ca-cert'

  {
  "result": "Keys match!"
}

zad3.5

mozna to tak zrobic tym i skopiowac i zapis do pliku:
deka@SKH-KUBUNTU:~$ curl -X 'GET' \    
  'http://127.0.0.1:3005/getprivkey' \
  -H 'accept: application/octet-stream'
-----BEGIN PRIVATE KEY-----
MIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0wawIBAQQgpBvOBzeMuW6b5kXi
DUEDDCTYAsqgKAIDYsrDOd2XDFGhRANCAAR8GkL9FvzfJSwwfmYt7QXzLkjw71KI
30UlELrijBko+ZS7qRcoQzOg4iExELc4vSKH62gU3vx8ygP/u8qjAMQ8
-----END PRIVATE KEY-----deka@SKH-KUBUNTU:~$ 



a ja pobralem plik z docsow i nazywa sie private_key_test

zawartosc wyglada tak:
-----BEGIN PRIVATE KEY-----
MIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0wawIBAQQgLLnJuTO9PPF4Ik6E
2xK92XT0vfaxnFFxYlxH6yyx3wihRANCAAS6bMjaJOP13Ksp0a3HBQ+iMLBhOWJA
BkpY85oz3EqXQJzGOnGgiewu1mg/ApRGLf6FU4oCeIPDcdgWsfIR/P80
-----END PRIVATE KEY-----

generowanie klucza:
openssl ec -in private_key_test.pem -pubout -out ec_pub.pem


test:

curl -X 'POST' \
  'http://127.0.0.1:3005/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'session_id=ca9da28e7adc857b' \
  -F 'public_key_file=@ec_pub.pem;type=application/x-x509-ca-cert'


  {
  "result": "Keys match!"


  zad3.6
  deka@SKH-KUBUNTU:~$ curl -X 'GET' \
  'http://localhost:3006/encrypt' \
  -H 'accept: */*'
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA/u+ptBV/+cwYBfRDa5lw
GReDtT0pJsTcBqNWU5R/WiyivcY6cvcQKekj+vu8++/KrfA1yNVqK6osZ5QNFvOY
wrTFF+LIbKKZp6OaNbVUaUjWPhwyhYNrIvx6L9BxURMsCMt4nNjrx7Ab4S6eZMUM
GmyMeJ9GU/K6b/BfuVqs1GnjHYKEnQEb6J1c9nfb5vtxeJmzySi7KK3h72bpsVat
iaKU5O61lfgo+k3hbIfHROuOw7vJWjaZVx5HuYjBY9tTGyLwtj68nAlAm7GMJ79U
t3fiRorObrnyz+KyTiJjlgGiHFg/kq78csZbSS+Itv1MwhGsm8FMHcpaalwujFcg
TQIDAQAB
-----END PUBLIC KEY-----
}

dobra dostaje za malo danych zostawiam to



zad3.6
