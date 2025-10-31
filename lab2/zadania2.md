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


zad5
generacja:
curl -X 'GET' \
  'http://localhost:10005/hash' \
  -H 'accept: application/json'

haszowanie

htpasswd -bnBC 10 user "nicedelo"

sprawdzenie:

przykladowy haxh_hex:
$2y$10$C1NRs5SGzftQMaxmvkq.lO52cXuLKdT6hcjYnoK0YChrfTboCznjS

curl -X 'POST' \
  'http://localhost:10005/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "22c3de9380257748",
  "hash_hex": "$2y$10$C1NRs5SGzftQMaxmvkq.lO52cXuLKdT6hcjYnoK0YChrfTboCznjS"
}'



  "result": "Correct bcrypt hash!"

zad6

```py
#!/usr/bin/env python3
import hashlib
import sys

def md5_hash_string(input_string: str) -> str:
    md5 = hashlib.md5()
    md5.update(input_string.encode('utf-8'))
    return md5.hexdigest()

if __name__ == "__main__":
    if len(sys.argv) > 1:
        text = " ".join(sys.argv[1:])
    else:
        text = "hello world"
    hash_value = md5_hash_string(text)
    print(f"MD5 hash of '{text}': {hash_value}")
```

zad7
``` py
#!/usr/bin/env python3
import hashlib
import sys

def sha1_hash_string(input_string: str) -> str:
    """
    Returns the SHA-1 hash of a given string in hexadecimal format.
    """
    sha1 = hashlib.sha1()
    sha1.update(input_string.encode('utf-8'))
    return sha1.hexdigest()

if __name__ == "__main__":
    # Pobranie tekstu z argumentów wywołania
    if len(sys.argv) > 1:
        text = " ".join(sys.argv[1:])
    else:
        text = "hello world"

    hash_value = sha1_hash_string(text)
    print(f"SHA-1 hash of '{text}': {hash_value}")



```

zad8
``` py

#!/usr/bin/env python3
import hashlib
import sys

def sha256_hash_string(input_string: str) -> str:
    """
    Returns the SHA-256 hash of a given string in hexadecimal format.
    """
    sha256 = hashlib.sha256()
    sha256.update(input_string.encode('utf-8'))
    return sha256.hexdigest()

if __name__ == "__main__":
    # Pobranie tekstu z argumentów wywołania
    if len(sys.argv) > 1:
        text = " ".join(sys.argv[1:])
    else:
        text = "hello world"

    hash_value = sha256_hash_string(text)
    print(f"SHA-256 hash of '{text}': {hash_value}")

```
zad9
#tego nie wiem jak zrobic


zad10
do odhashowania mamy:
sudo docker run -it mazurkatarzyna/hash-identifier:latest
sudo docker run -it docker.io/mazurkatarzyna/hashid:latest
i wklejamy hasloLeast Possible Hashs:
[+] Tiger-160
[+] Haval-160
[+] RipeMD-160
[+] SHA-1(HMAC)
[+] Tiger-160(HMAC)
[+] RipeMD-160(HMAC)
[+] Haval-160(HMAC)
[+] SHA-1(MaNGOS)
[+] SHA-1(MaNGOS2)
[+] sha1($pass.$salt)
[+] sha1($salt.$pass)
[+] sha1($salt.md5($pass))
[+] sha1($salt.md5($pass).$salt)
[+] sha1($salt.sha1($pass))
[+] sha1($salt.sha1($salt.sha1($pass)))
[+] sha1($username.$pass)
[+] sha1($username.$pass.$salt)
[+] sha1(md5($pass))
[+] sha1(md5($pass).$salt)
[+] sha1(md5(sha1($pass)))
[+] sha1(sha1($pass))
[+] sha1(sha1($pass).$salt)
[+] sha1(sha1($pass).substr($pass,0,3))
[+] sha1(sha1($salt.$pass))
[+] sha1(sha1(sha1($pass)))
[+] sha1(strtolower($username).$pass)


zad11
nie wiem
zad12
sudo docker run -it docker.io/mazurkatarzyna/hashid:latest
6adfb183a4a2c94a2f92dab5ade762a47889a5a1
zad13
nie wiem
zad14
nie wiem


  

