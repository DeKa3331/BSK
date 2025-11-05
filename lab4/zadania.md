w tej lekcji mialem duzo problemow bo z tymi kluczami to wiecej nie dziala niz dziala


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

  prywant klucz upload:
  curl -X 'POST' \


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

zeby sie nie bawic z enterami na koncu:
jq -r '.private_key_pem' genpriv.pem > priv.pem
generacja publicznego z tego:
openssl pkey -in testpriv.pem -pubout -out genpriv.pub
