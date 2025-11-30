

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
 curl -i 'GET'   'http://localhost:3006/encrypt'   -H 'accept: */*'
curl: (6) Could not resolve host: GET
HTTP/1.1 200 OK
Server: Werkzeug/3.1.3 Python/3.10.19
Date: Sun, 30 Nov 2025 14:52:01 GMT
Content-Disposition: attachment; filename=public_key_V8ZMYTjZRF4.pem
Content-Type: application/octet-stream
Content-Length: 450
Cache-Control: no-cache
Date: Sun, 30 Nov 2025 14:52:01 GMT
X-Session-ID: V8ZMYTjZRF4
X-Word: rocking
Access-Control-Allow-Origin: *
Connection: close

-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA+zxUsCtxUZ0IaxBQj595
HEFcrRduzgExRnQoYIRYjiY7qIeMGFi1dHnzXrB4x0fJKiXS+cKSfplfkCLzfyhy
Po/tahAbB1X+aRaYzs7kkQjzMvx8Z3u6+AnVAdPh3hoIESpcSXTtviR+6CvRpuA/
t3X4LfnPRAlTAvvsIzJGpoX8bb5reIYOBCn52IpA5YJfCk2Zh/iS4B+qo/bRm/YB
cEtvJljrVv+/pMezXK96HflTIBEV9s7/Lq1WEcS8F9JQAEkHqS3gSK6PP6Z5navD
pMK4GbBbB4Y+6VhuKepy/fy2h9osxCDN4u5A8+BrVf5zZNn+3VA+gqKgd2IuHMVB
bwIDAQAB
-----END PUBLIC KEY-----

zapisuje klucz do pliku

echo -n '-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA+zxUsCtxUZ0IaxBQj595
HEFcrRduzgExRnQoYIRYjiY7qIeMGFi1dHnzXrB4x0fJKiXS+cKSfplfkCLzfyhy
Po/tahAbB1X+aRaYzs7kkQjzMvx8Z3u6+AnVAdPh3hoIESpcSXTtviR+6CvRpuA/
t3X4LfnPRAlTAvvsIzJGpoX8bb5reIYOBCn52IpA5YJfCk2Zh/iS4B+qo/bRm/YB
cEtvJljrVv+/pMezXK96HflTIBEV9s7/Lq1WEcS8F9JQAEkHqS3gSK6PP6Z5navD
pMK4GbBbB4Y+6VhuKepy/fy2h9osxCDN4u5A8+BrVf5zZNn+3VA+gqKgd2IuHMVB
bwIDAQAB
-----END PUBLIC KEY-----' >public.pem


jakby byl problem na kolokwium to gpt mowi zeby zwrocic to tak:

```
cat > public.pem << EOF
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA+zxUsCtxUZ0IaxBQj595
HEFcrRduzgExRnQoYIRYjiY7qIeMGFi1dHnzXrB4x0fJKiXS+cKSfplfkCLzfyhy
Po/tahAbB1X+aRaYzs7kkQjzMvx8Z3u6+AnVAdPh3hoIESpcSXTtviR+6CvRpuA/
t3X4LfnPRAlTAvvsIzJGpoX8bb5reIYOBCn52IpA5YJfCk2Zh/iS4B+qo/bRm/YB
cEtvJljrVv+/pMezXK96HflTIBEV9s7/Lq1WEcS8F9JQAEkHqS3gSK6PP6Z5navD
pMK4GbBbB4Y+6VhuKepy/fy2h9osxCDN4u5A8+BrVf5zZNn+3VA+gqKgd2IuHMVB
bwIDAQAB
-----END PUBLIC KEY-----
EOF
```

zapis wyrazu z naglowka:
echo -n "rocking" > word.txt



szyfrowanie:

echo -n "rocking" | openssl pkeyutl -encrypt -pubin -inkey public.pem -pkeyopt rsa_padding_mode:oaep -out encrypted.bin



deka@SKH-KUBUNTU:~$ cat encrypted.bin
�x�▒��@2#��#T����^Q*+_�-��8��ǽB.N���������X���%��
                                                 ��
����gmɿM��M#�1�ۙ����^��}#L7A���{��ū�`����C��        ��Ւ|��=m�E�
                                 �k�(̉
                                     ��H�EO����1��lI�^�B��▒2��y):��e���\6�X��@�~�*      X�0�T5y���!�E▒v
^�-���


a tak naprawde na kolosa wystarczy:
curl -X 'POST' \
  'http://localhost:3006/submit' \
  -H 'accept: application/json' \
  -F 'session_id=V8ZMYTjZRF4' \
  -F 'encrypted_file=@encrypted.bin'
{"result":"Correct encryption!"}

zad3.7

pobieranie danych:

  curl -i 'GET' \
  'http://127.0.0.1:3007/decrypt' \
  -H 'accept: */*'

  curl: (6) Could not resolve host: GET
HTTP/1.1 200 OK
Server: Werkzeug/3.1.3 Python/3.10.19
Date: Sun, 30 Nov 2025 15:18:57 GMT
Content-Disposition: attachment; filename=encrypted_and_key.zip
Content-Type: application/zip
Content-Length: 4156
Cache-Control: no-cache
Date: Sun, 30 Nov 2025 15:18:57 GMT
X-Session-Id: fedf2c6c4044db66
Access-Control-Allow-Origin: *
Connection: close

Warning: Binary output can mess up your terminal. Use "--output -" to tell 
Warning: curl to output it to your terminal anyway, or consider "--output 
Warning: <FILE>" to save to a file.


jak widac tutaj jest problem ale to dlatego ze dostaje zipa 

wiec moge sobie to zapisac odrazu do zipa o tak:

  curl http://127.0.0.1:3007/decrypt -o dane.zip

WAZNE
**  unzip dane.zip**

openssl pkeyutl -decrypt -inkey private_key.pem -in <(base64 -d encrypted.txt) -pkeyopt rsa_padding_mode:oaep -out decrypted.txt

deka@SKH-KUBUNTU:~$ openssl pkeyutl -decrypt -inkey private_key.pem -in <(base64 -d encrypted.txt) -pkeyopt rsa_padding_mode:oaep -out decrypted.txt
deka@SKH-KUBUNTU:~$ cat decrypted.txt
bonita4

i wysylanie do serwera:

curl -X 'POST' \
  'http://127.0.0.1:3007/submit' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "fedf2c6c4044db66",
  "decrypted_word": "bonita4"
}'

zad3.8

generacja klucza:
openssl genpkey -algorithm RSA -out priv.pem -pkeyopt rsa_keygen_bits:1024

generacja publicznego na podstawie wczesniejszego prywatnego:
openssl pkey -in priv.pem -pubout -out pub.pem

losowe slowo:

echo -n 'mojeslowo' > plaintext.txt

zaszyfrowanie:
openssl pkeyutl -encrypt -pubin -in plaintext.txt -inkey public.pem -pkeyopt rsa_padding_mode:oaep -out encrypted.bin


zakodowanie:
base64 encrypted.bin > ciphertext.txt

base64 -w 0 encrypted.bin > ciphertext.txt


deka@SKH-KUBUNTU:~$ curl -X 'POST' \
  'http://127.0.0.1:3008/decrypt' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'private_key=@priv.pem;type=application/x-x509-ca-cert' \
  -F 'public_key=@pub.pem;type=application/x-x509-ca-cert' \
  -F 'plaintext=@plaintext.txt;type=text/plain' \
  -F 'ciphertext=@ciphertext.txt;type=text/plain'
{"error":"Ciphertext with incorrect length.","keys_match":true,"result":"decryption_failed"}












