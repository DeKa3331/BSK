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





