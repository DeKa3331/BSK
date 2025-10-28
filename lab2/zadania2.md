zad1
generujemy wyraz:

curl -X 'GET' \
  'http://localhost:10001/hash' \
  -H 'accept: application/json'

mozemy zapisac go do pliku: 

echo -n "Hello" | md5sum

sprawdzanie czy jest poprawny:

curl -X 'POST' \
  'http://localhost:10001/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "f16f5740cbfb3364",
  "hash_hex": "4fb33aea6fb5d5dd3f7352eef75fd037"
}'
!!!!
{"result":"Correct MD5 hash!"}
!!!

zad2
curl -X 'GET' \
  'http://localhost:10002/hash' \
  -H 'accept: application/json'
  
echo -n "rayray87" | openssl dgst -sha256

sprawdzenie:
curl -X 'POST' \
  'http://localhost:10002/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "f5019e8dce21b6c4",
  "hash_hex": "b0d283f545ea9fd5fa25d3a70c6c83e13e900d844252cb79057bf2b586b0b0d6"
}'
{"result":"Correct SHA-256 hash!"}


zad3
curl -X 'GET' \
  'http://localhost:10003/hash' \
  -H 'accept: application/json'



echo -n "911002" | openssl dgst -sha512

curl -X 'POST' \
  'http://localhost:10003/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "6c69d99bd8433e1e",
  "hash_hex": "d990ba7ebeea9e261cc9ec44327d5ef56c1b6aa887342c736a9f076b7f2c43da366d6dff0ddeb8f0003525a9705f2f854cc404299869634a8745c96983dbf522"
}'

{"result":"Correct SHA-512 hash!"}

zad4

wyraz generujemy poza kontenerem

curl -X 'GET' \
  'http://localhost:10004/hash' \
  -H 'accept: application/json'

argona uzywamy w konterze
docker run -it mazurkatarzyna/openssl-332-ubuntu:latest

w miejscu pass wpisac wyraz!:
  openssl kdf -keylen 24 -kdfopt pass:raptowniejsza -kdfopt salt:NaCl2024 -kdfopt iter:1 -kdfopt memcost:8192 ARGON2D

przykladowy outcome:
AA:21:F8:6F:AE:6A:0E:F4:9F:71:E2:EA:2D:39:E2:C1:59:67:CB:F1:2F:B6:5E:16

ale aby przeszedl nam submit to muismy usunad : czyli, 


openssl kdf -keylen 24 -kdfopt pass:raptowniejsza -kdfopt salt:NaCl2024 -kdfopt iter:1 -kdfopt memcost:8192 ARGON2D |tr -d ':'

outcome:
AA21F86FAE6A0EF49F71E2EA2D39E2C15967CBF12FB65E16

test:
(poza kontenerem)
curl -X 'POST' \
  'http://localhost:10004/submit/argon2d' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "ea4125d6a48b1ab7",
  "hash_hex": "AA21F86FAE6A0EF49F71E2EA2D39E2C15967CBF12FB65E16"
}'

  "result": "Correct ARGON2D hash!"



  

