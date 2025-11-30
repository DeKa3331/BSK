

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
openssl pkeyutl -encrypt -pubin -in plaintext.txt -inkey pub.pem -pkeyopt rsa_padding_mode:oaep -out encrypted.bin


zakodowanie:
base64 encrypted.bin > ciphertext.txt

deka@SKH-KUBUNTU:~$ curl -X 'POST' \
  'http://127.0.0.1:3008/decrypt' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'private_key=@priv.pem;type=application/x-x509-ca-cert' \
  -F 'public_key=@pub.pem;type=application/x-x509-ca-cert' \
  -F 'plaintext=@plaintext.txt;type=text/plain' \
  -F 'ciphertext=@ciphertext.txt;type=text/plain'


{"decrypted":"mojeslowo","keys_match":true,"plaintext_match":true,"result":"ok"}


zad3.9

curl -i 'GET' \
  'http://localhost:3009/sign' \
  -H 'accept: application/x-pem-file'


  
Server: Werkzeug/3.1.3 Python/3.10.19
Date: Sun, 30 Nov 2025 17:34:29 GMT
Content-Disposition: attachment; filename=private_key.pem
X-Session-Id: LcXZcBoM29tnGQyme1od4w
X-Word: lindsey99
Content-Type: application/x-pem-file
Content-Length: 1674
Access-Control-Allow-Origin: *
Connection: close


echo -n 'lindsey99' > word.txt

openssl dgst -sha256 -binary -out word.sha256 word.txt





-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAsw3TuVYaMS7teYgKJqiLRo6UEBr/8RT3Yr4e5uMzPunhjx+7
fi9MXGHY4ymneaUvFWMkJLVpz+d+RRJZOlC46AQaqDB4UkPzBtEYH2+gHdUb9of1
bLyvymUIIwEdQi/QNm0YC/2Vn82wnzRIztmytW47CboMRSsxuwTZXyM8JJXRbEwX
WEzgpFts0Wn8wI0VCmxF8oG80lUtUfjjiZr9O4VDrgatDkEIVnTn/34OSrYvEFWR
VghptS/Gq80ARnEvP5kJB5bmL61ruO1w8guhurjygzynNtYTCT0v2v+ix3BtRerw
gIrEsEbE77bWjO7MfaGgu3leSAiycteSTsz8QQIDAQABAoIBAAJoYokh1E6GUc4g
OTj4q+4JDnqWltvNySd3PJaUrj6Trf9W/R4s3hY5UH2aRKLMGOFk9s5NsFZ556i/
jtKr9YcU8Ev0Aieyy0erh9NLJLJHAIIqxQ8TLNrcG8FO/18BoidbtWK6pFSYszX6
WbrqmnKiML38VgQ3eOLRtXe4E0vPgEl1kx9gBJrv+MKGudPoAlQZUqXnEqyRhC3O
nhXX4XXcKFM26biww6AfzwDbpeESIPqJnqr/e0frFKqYPJRwtyrTD+7aVCtA0x12
h/HDhIC7zcq7PEqYOkzkxuhBUBgICXkSdFRzVgllyaRruCrSIiT+HXFuMc2T7wbL
A++PdKECgYEAxXfmZoc7XHQWB3c2770jjkO86jd4fssYj/eWZjCZksRVfx13qCLY
DG4JjE5uGLB6uROl56ezYcl5249Ngy4cHt99U0C8txLmGRga8744VIOrVF23INhb
/dnHDmXO9PbLRy3CbW7fZ2LDuq/5wR2SZFnL7VfFV6u8+W+6Lz2TW2ECgYEA6CCg
rALRmNN3M86PuNV0MCcSxzC8n1hvljAGF4HiF2FSC8C4JEDA79AAWX3pNd9dmxpQ
fK9ZznX3vk6uMCWCTZxq1D0q4N26D+xn8aEF3l3z6VFZi8GN6WVJsI7qesoGmLkX
LMI6SZBECdD1VK06l+gQga0HdrRWXiRj+OG1LOECgYAChNkHjcoQD9sIFVk6Daua
cPrD8hkzZNvXWk0s2Inc+Wwtxu5z0p326qBsjcORxQ6Ltdhz8Au1v6AyUM2oUrpB
GpC6syS1ISSWRVxyp4aIbXWOCfQAE0J5JoIHiPzu2wcUzVyhkLyA0R22D/Cbqgjo
Bs03Jdt6ltI+TFKPr7VlgQKBgBEDCyNwFXJQ1SSb19ag9iHtSygD/17iOVNVc6zX
XP1/qWapGhW2FS2+HbhxTN0g4JhUZl+s7jT+Wki9NXDb3t/XPdEOJo1SUqeGGNwR
g/+W/SA1UQ24ArF/NdZVswOKuM8KiZNDLMhlZUce5EvvYiLt4//M8YYWk1nU6uq7
h+6hAoGAbQvKYZbYMYJ89E78v/4N2aX2Go/uHmP51Uoz6wrUrExItdZeVgkw+8k9
dp11cWR01c1j4z8D4gj77xU+zuuitgjU4pAYzn2EMhnKEikGkriVPUqhFzphsx4T
mPVrOIFq4vBT1mJi5wN6Rc2b9PERXQz7Y+mFB7urf+c6fLDE+6o=
-----END RSA PRIVATE KEY-----


echo -n '-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAsw3TuVYaMS7teYgKJqiLRo6UEBr/8RT3Yr4e5uMzPunhjx+7
fi9MXGHY4ymneaUvFWMkJLVpz+d+RRJZOlC46AQaqDB4UkPzBtEYH2+gHdUb9of1
bLyvymUIIwEdQi/QNm0YC/2Vn82wnzRIztmytW47CboMRSsxuwTZXyM8JJXRbEwX
WEzgpFts0Wn8wI0VCmxF8oG80lUtUfjjiZr9O4VDrgatDkEIVnTn/34OSrYvEFWR
VghptS/Gq80ARnEvP5kJB5bmL61ruO1w8guhurjygzynNtYTCT0v2v+ix3BtRerw
gIrEsEbE77bWjO7MfaGgu3leSAiycteSTsz8QQIDAQABAoIBAAJoYokh1E6GUc4g
OTj4q+4JDnqWltvNySd3PJaUrj6Trf9W/R4s3hY5UH2aRKLMGOFk9s5NsFZ556i/
jtKr9YcU8Ev0Aieyy0erh9NLJLJHAIIqxQ8TLNrcG8FO/18BoidbtWK6pFSYszX6
WbrqmnKiML38VgQ3eOLRtXe4E0vPgEl1kx9gBJrv+MKGudPoAlQZUqXnEqyRhC3O
nhXX4XXcKFM26biww6AfzwDbpeESIPqJnqr/e0frFKqYPJRwtyrTD+7aVCtA0x12
h/HDhIC7zcq7PEqYOkzkxuhBUBgICXkSdFRzVgllyaRruCrSIiT+HXFuMc2T7wbL
A++PdKECgYEAxXfmZoc7XHQWB3c2770jjkO86jd4fssYj/eWZjCZksRVfx13qCLY
DG4JjE5uGLB6uROl56ezYcl5249Ngy4cHt99U0C8txLmGRga8744VIOrVF23INhb
/dnHDmXO9PbLRy3CbW7fZ2LDuq/5wR2SZFnL7VfFV6u8+W+6Lz2TW2ECgYEA6CCg
rALRmNN3M86PuNV0MCcSxzC8n1hvljAGF4HiF2FSC8C4JEDA79AAWX3pNd9dmxpQ
fK9ZznX3vk6uMCWCTZxq1D0q4N26D+xn8aEF3l3z6VFZi8GN6WVJsI7qesoGmLkX
LMI6SZBECdD1VK06l+gQga0HdrRWXiRj+OG1LOECgYAChNkHjcoQD9sIFVk6Daua
cPrD8hkzZNvXWk0s2Inc+Wwtxu5z0p326qBsjcORxQ6Ltdhz8Au1v6AyUM2oUrpB
GpC6syS1ISSWRVxyp4aIbXWOCfQAE0J5JoIHiPzu2wcUzVyhkLyA0R22D/Cbqgjo
Bs03Jdt6ltI+TFKPr7VlgQKBgBEDCyNwFXJQ1SSb19ag9iHtSygD/17iOVNVc6zX
XP1/qWapGhW2FS2+HbhxTN0g4JhUZl+s7jT+Wki9NXDb3t/XPdEOJo1SUqeGGNwR
g/+W/SA1UQ24ArF/NdZVswOKuM8KiZNDLMhlZUce5EvvYiLt4//M8YYWk1nU6uq7
h+6hAoGAbQvKYZbYMYJ89E78v/4N2aX2Go/uHmP51Uoz6wrUrExItdZeVgkw+8k9
dp11cWR01c1j4z8D4gj77xU+zuuitgjU4pAYzn2EMhnKEikGkriVPUqhFzphsx4T
mPVrOIFq4vBT1mJi5wN6Rc2b9PERXQz7Y+mFB7urf+c6fLDE+6o=
-----END RSA PRIVATE KEY-----' > priv.pem




podpisywanie:

openssl pkeyutl -sign -in word.sha256 -inkey priv.pem \
    -pkeyopt digest:sha256 \
    -pkeyopt rsa_padding_mode:pss \
    -pkeyopt rsa_pss_saltlen:32 \
    -out signature.bin

zamiana na base64:
    base64 signature.bin > signature.b64

wysylanie:
    curl -X 'POST' \
  'http://localhost:3009/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'session_id=LcXZcBoM29tnGQyme1od4w' \
  -F 'signature_b64=@signature.b64'

{
  "result": "Correct signature!"
}

zad3.10

curl -i 'GET' \
  'http://localhost:3010/verify' \
  -H 'accept: application/zip' -o zadania.zip

  unzip zadania.zip

  echo -n 'pineapple' >word.txt

  base64 -d signature.b64 > signature.bin

  

nie dziala mi ten verify:

openssl dgst -sha256 -verify public_key.pem -sigopt rsa_padding_mode:pss -sigopt rsa_pss_saltlen:32 -signature signature.bin word.txt


ale tak by wygladal submit:
  curl -X 'POST' \
  'http://localhost:3010/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'session_id=gAnDrSfVteCJYLtRNlYglg' \
  -F 'word=cherry' \
  -F 'public_key_pem=@public_key.pem;type=application/x-x509-ca-cert' \
  -F 'signature_b64=@signature.b64' \
  -F 'user_verified=false'

  ale moze to nie mialo przejsc? bo wtedy user_verified=false i dziala?


  

  








