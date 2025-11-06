zad2.1
generacja: curl -X 'GET' \
  'http://127.0.0.1:2001/encrypt' \
  -H 'accept: application/json'

  {"key_hex":"19739c5e15ae557cb2c7c0945b5ad5bb13c54e5b7cb039d8745c0f6ca5008f6c","session_id":"41a2123ecbf953b1","word":"feb212"}

zapisujemy to do pliku mozna tez sobie wygenerowac jakiegos gotowego hexa w ten sposob:
openssl rand -hex 32 > key
albo wpisac go:
echo -n '19739c5e15ae557cb2c7c0945b5ad5bb13c54e5b7cb039d8745c0f6ca5008f6c' > key
wyraz:
echo -n 'feb212' > zad1.txt

szyfrowanie:
openssl enc -aes-256-ecb -in zad1.txt -K $(cat key) -out zad1.enc -base64

zawartosc wyglada tak:
cat zad1.enc
+r2rq8u5yrTvZuqLmCP5Jw==
deka@SKH-KUBUNTU:~$ 

testowanie:
curl -X 'POST' \
  'http://127.0.0.1:2001/submit' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "41a2123ecbf953b1",
  "encrypted_b64": "+r2rq8u5yrTvZuqLmCP5Jw=="
}'

"result":"Correct encryption!"}

zad2.2----tutaj zadac pytania:

curl -X 'GET' \
  'http://localhost:2002/decrypt' \
  -H 'accept: application/json'

{"encrypted_b64":"QS4ZtK6WZcjmuX46jqQPzg==","key_hex":"faa93a7bfab3a4be1b0a8135613aef714a5f8c2b66b86a60f78c93dc76bcf6e0","session_id":"8338a903b10ffa3f"}


ustawianei plikow:
echo -n 'faa93a7bfab3a4be1b0a8135613aef714a5f8c2b66b86a60f78c93dc76bcf6e0'  > key
echo -n 'QS4ZtK6WZcjmuX46jqQPzg==' >zad1.enc

deszyfrowanie wyglada tak ( z tego co rozumiem):

openssl enc -d -aes-256-ecb -in zad1.enc -out zad1.dec -K $(cat key) -base64

i co ciekawe to zadziala jesli uzyje danych z 1szego zadania natomiast jesli chce uzyc tych wygenerowanych to wersja gpt dopiero dziala czemu? nie wiem.



tak mi poprawil gpt, i nie dokonca to rozumiem czemu tak
base64 -d zad1.enc | openssl enc -d -aes-256-ecb -K $(cat key) -nosalt -nopad -out zad1.dec

test:
curl -X 'POST' \
  'http://localhost:2002/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "8338a903b10ffa3f",
  "decrypted_word": "mrsmia1"
}'

{
  "result": "Correct decryption!"
}

zad2.3
generacja:
curl -X 'GET' \
  'http://localhost:2003/encrypt' \
  -H 'accept: application/json'

  
{"key_hex":"429e015ad94bd1a2c8d7b43c74a3289d","session_id":"350842e2af848b27","word":"mindy7"}


echo -n '429e015ad94bd1a2c8d7b43c74a3289d' > key
echo -n 'mindy7' >wyraz.txt 

szyfrowanie:
openssl enc -camellia-128-ecb -in wyraz.txt -out zad23.enc -K $(cat key) -base64

zawartosc:
cat zad23.enc
Syj6tMZES+TQjK/owkPocQ==

test:
curl -X 'POST' \
  'http://localhost:2003/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "350842e2af848b27",
  "encrypted_b64": "Syj6tMZES+TQjK/owkPocQ=="
}'


{
  "result": "Correct encryption!"
}


zad2.4-nie dziala
generacja:
curl -X 'GET' \
  'http://localhost:2004/decrypt' \
  -H 'accept: application/json'

{"encrypted_b64":"R85zKZPZuYS3SurCIGYOfg==","key_hex":"0bdbd361c60ed0cc573711628a5c0483","session_id":"71453384a469410c"}


zapis do plikow:
echo -n 'R85zKZPZuYS3SurCIGYOfg==' > zad24.enc
echo -n '0bdbd361c60ed0cc573711628a5c0483' > key

openssl enc -d -camellia-128-ecb -in zad24.enc -out zad24.dec -K $(cat key) -base64


znowu ten blad:
bad decrypt
4077278113750000:error:1C80006B:Provider routines:ossl_cipher_generic_block_final:wrong final block length:../providers/implementations/ciphers/ciphercommon.c:429:


zad2.5
generacja:

curl -X 'GET' \
  'http://localhost:2005/encrypt' \
  -H 'accept: application/json'
{"session_id":"2acab34e0c970a27","word":"mmnarak"}

zapis do pliku:
echo -n 'mmnarak' >word.txt

generacja klucza 192:
openssl rand -hex 24 > key

szyfrowanie:
openssl enc -aria-192-ecb -in word.txt -out zad25.enc -K $(cat key) -base64
test:
cat zad25.enc
SfR4yKC5mU1Xw+TLa0oTEw==

deszyfrowanie tego samoe:
openssl enc -d -aria-192-ecb -in zad25.enc -out zad25.dec -K $(cat key) -base64

cat zad25.dec
mmnarak

zad2.6---tutaj pytanie czy tak powinna wygladac skladnia z tym iv?
generacja:
curl -X 'GET' \
  'http://localhost:2006/encrypt' \
  -H 'accept: application/json'

  
{"session_id":"3ceb89363fd76ba8","word":"evilperson"}


zapis do pliku:
echo -n 'evilperson' >word.txt

generacja klucza 128:
openssl rand -hex 16 > key
openssl rand -hex 16 >wektor.IV

szyfrowanie:
openssl enc -aes-128-cbc -in word.txt -K $(cat key) -iv $(cat wektor.IV) -out zad26.enc -base64

test:
cat zad26.enc
4I+mQZlKDPBmsI2N/i5D2g==


curl -X 'POST' \
  'http://localhost:2006/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "3ceb89363fd76ba8",
  "encrypted_b64": "4I+mQZlKDPBmsI2N/i5D2g==",
  "key_hex": "6d077f68715d0698e5b7fad1d1fbc6eb",
  "iv_hex": "6512e1823eb844180573cab8dee49889"
}'

{
  "result": "Correct encryption!"
}

zad2.7

generacja:
 curl -X 'GET' \
  'http://localhost:2007/decrypt' \
  -H 'accept: application/json'
  
{"encrypted_b64":"yejJag3Ss8jxXeKKMbiY7JFS0JA5MYGB5ReLwJsFSxA=","iv_hex":"aebd8d0726a10d01df343faa48fa1bdd","password":"115657","session_id":"b61bd51656e7fd44"}

echo -n 'yejJag3Ss8jxXeKKMbiY7JFS0JA5MYGB5ReLwJsFSxA' >zad27.enc







  




 





