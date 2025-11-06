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

zad2.7---tutaj wspieralem cie gpt juz

generacja:
 curl -X 'GET' \
  'http://localhost:2007/decrypt' \
  -H 'accept: application/json'
  
{"encrypted_b64":"09BSb4MUW4qb/o7BEKobJ9mffdiBIVDsXKsffdhrtrU=","iv_hex":"d27b64ad5a219930ee6f5df498b88f0e","password":"roro2008","session_id":"c630dc6fce76d3b6"}

kodowanie do pliku:
najpierw musimy zamienic nasze base64 na zakodowany
echo -n '09BSb4MUW4qb/o7BEKobJ9mffdiBIVDsXKsffdhrtrU=' > zad27.b64
base64 -d zad27.b64 > zad27.enc
echo -n 'd27b64ad5a219930ee6f5df498b88f0e' > wektor27.IV
echo -n 'roro2008' > password

deszyfrowanie, (bez soli):
openssl enc -d -aes-256-cbc -in zad27.enc -out zad27.dec -pbkdf2 -nosalt -pass pass:$(cat password) -iv $(cat wektor27.IV)


test:
curl -X 'POST' \
  'http://localhost:2007/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "c630dc6fce76d3b6",
  "decrypted_word": "sourstraw"
}'

{
  "result": "Correct decryption!"
}

zad2.8

generacja:
curl -X 'GET' \
  'http://localhost:2008/decrypt' \
  -H 'accept: application/json'

  {"encrypted_b64":"53VGXquP0h8drpsum1c16m/bv477l/F/","iv_hex":"17e2a8e514d45fea","password":"tayboo12","session_id":"a64119f895011885"}

zapis do plikow:
echo -n '53VGXquP0h8drpsum1c16m/bv477l/F/' > zad28.b64
base64 -d zad27.b64 > zad28.enc
echo -n '17e2a8e514d45fea' > wektor28.IV
echo -n 'tayboo12' > password

deszyfrowanie:
openssl enc -d -des-ede3-cbc -in zad28.enc -out zad28.dec -pbkdf2 -nosalt -pass pass:$(cat password) -iv $(cat wektor28.IV)
test:
cat zad28.dec
sent848neat363

curl -X 'POST' \
  'http://localhost:2008/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "a64119f895011885",
  "decrypted_word": "sent848neat363"
}'

{
  "result": "Correct decryption!"
}

zad2.9---tego nie wiem jak zrobic nie dziala (moje domysly)

generacja:
curl -X 'GET' \
  'http://localhost:2009/decrypt' \
  -H 'accept: application/json'

{"encrypted_b64":"Ruufpb6GYJkta+jSHB01FeNyp7aB9LeAQW39NGeVwrc=","password":"maryjane9","session_id":"63fced7970d81ec2"}

zapis do plikow:
echo -n 'Ruufpb6GYJkta+jSHB01FeNyp7aB9LeAQW39NGeVwrc=' > zad29.b64
base64 -d zad29.b64 > zad29.enc
echo -n 'maryjane9' > password


openssl enc -d -aes-256-ecb -in zad29.enc -out zad29.dec -pbkdf2 -nosalt -iter 356 -pass pass:$(cat password)


zad2.10
curl -X 'GET' \
  'http://localhost:2010/decrypt' \
  -H 'accept: application/json'

(tutaj byl ciekawy case bo iv_hex sie wylosowal jako null i nie wiedzialem co wtedy)

takie dane:
{"encrypted_b64":"a4SXD8y0oshfd+K2LcuGE7KyjjiV9JOR","iv_hex":null,"key_hex":"b5cdd0aa4afc2eea1f9e35e67686a4f0","session_id":"d1da692cbb7b465d"}


{"encrypted_b64":"b0Hdgq+BJKto9mItTbRo/g==","iv_hex":"ae1a43af767da136f0709934161eb6bb","key_hex":"cf5efd0ab7bc00c4698501f3cba30a89cabc5fc551bcce14","session_id":"7b3b020177f2d1ac"}

echo -n 'b0Hdgq+BJKto9mItTbRo/g==' > zad210.b64
base64 -d zad210.b64 > zad210.enc
echo -n 'cf5efd0ab7bc00c4698501f3cba30a89cabc5fc551bcce14' > key
echo -n 'ae1a43af767da136f0709934161eb6bb' >wektor210.IV

szukamy czym zaszyfrowane?:
sudo docker run -it docker.io/mazurkatarzyna/hashid:latest b0Hdgq+BJKto9mItTbRo/g==

ale to zwraca unknown czyli nie wiem jak to zrobic? gpt mi podpowiedzial aes-192-cbc

deszyfrowanie:
openssl enc -d -aes-192-cbc -in zad210.enc -out zad210.dec -K $(cat key) -iv $(cat wektor210.IV)

nie dziala nie wiem jak znalezc co to za szyfr

zad2.11
curl -sS http://127.0.0.1:2011/encrypt -H "accept: application/json"
{
  "algorithm": "ARIA-128-CTR",
  "image_data_base64": "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",
  "iv": "15f3b16ebd3cd72b2f2bc75dbe04a061",
  "key": "1fbcf99a5131a6a0094c2a40a1a0b8dd",
  "key_size_bits": 128,
  "session_id": "4dc13670-6557-4752-98ef-6184d3f93d09"
}


zapis do pliku:
echo -n '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' > image.b64
base64 -d image.b64 > zad211.enc
echo -n '1fbcf99a5131a6a0094c2a40a1a0b8dd' > key
echo -n '15f3b16ebd3cd72b2f2bc75dbe04a061' > wektor211.IV


szyfrowanie:
openssl enc -aria-128-ctr -in zad211.enc -out image.enc -K "$(cat key)" -iv "$(cat wektor211.IV)"

test:
cat image.enc
ale jest tak duze ze tego nie wklejam tutaj :)


jak powinien wyglada submit tez nie wiem wsm???


curl -X 'POST' \
  'http://localhost:2011/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -F 'file=@image.enc;type=application/x-x509-ca-cert'
  -d '{
  "session_id": "4dc13670-6557-4752-98ef-6184d3f93d09",
}'

{
  "result": "Correct decryption!"
}

2.12
analogicznie do 2.11 nie wiem dokonca jak zrobic :(




 





