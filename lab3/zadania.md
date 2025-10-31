zad2.1
curl -X 'GET' \
  'http://127.0.0.1:2001/encrypt' \
  -H 'accept: application/json'

zapisujemy to do pliku mozna tez sobie wygenerowac jakiegos gotowego hexa w ten sposob:
openssl rand -hex 32 > key
albo wpisac go:
echo -n '2cabe041cab4ff0d8018d77b1dda10795dc7a3eb077a33d8b095a7ab1dbd51b3' > key
wyraz:
echo -n 'Hello' > zad1.txt

openssl enc -aes-256-ecb -in zad1.txt -K $(cat key) -out zad1.enc -base64

deka@SKH-KUBUNTU:~$ cat zad1.enc
VRQ9o8hNIFUfBHzL7q5i5w==

test:
curl -X 'POST' \
  'http://127.0.0.1:2001/submit' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "session_id": "3437d2aeb87e348b",
  "encrypted_b64": "ewtkSWTU04ttF6so2DDkrw=="
}'
{"result":"Correct encryption!"}

zad2.2
curl -X 'GET' \
  'http://localhost:2002/decrypt' \
  -H 'accept: application/json'

  aby odszyfrowac uzywamy:
   openssl enc -d -aes-256-ecb -in zad1.enc -out zad1.dec -K $(cat key) -base64


zad1.enc-to wyraz zaszyfrowany 
a key to klucz np:
$ echo -n '0b0506b2e8ace255f499cc4c28fcd87f21a84c12adf6937cf1ade0195254d078' > keyhex

zad2.3
curl -X 'GET' \
  'http://localhost:2003/encrypt' \
  -H 'accept: application/json'
{"key_hex":"518c0283dda28d5f536af3acfc801de7","session_id":"967bd4dc462abb65","word":"suppergirl"}
klucz:
deka@SKH-KUBUNTU:~$ echo -n '518c0283dda28d5f536af3acfc801de7' >keyhex
 wyraz:
 deka@SKH-KUBUNTU:~$ echo -n 'suppergirl' > wyraz
 
deka@SKH-KUBUNTU:~$ openssl enc -camellia-128-ecb -in wyraz -out zad23.enc -K $(cat keyhex) -base64
deka@SKH-KUBUNTU:~$ cat zad23.enc
kICyqvUvprwWBC+SgXVq6A==


{"result":"Correct encryption!"}

zad2.4
decrytpuje to co wczesniej:
deka@SKH-KUBUNTU:~$ openssl enc -d -camellia-128-ecb -in zad23.enc -out zad24.dec -K $(cat keyhex) -base64
deka@SKH-KUBUNTU:~$ cat zad24.dec
suppergirldeka@SKH-KUBUNTU:~$ 

zad2.5
└──╼ $openssl enc -aria-192-ecb -in zad25.txt -out zad25.enc -K $(cat key25) -base64

└──╼ $openssl enc -d -aria-192-ecb -in zad25.enc -out zad25.dec -K $(cat key25) -base64

zad2.6
curl -X 'GET' \
  'http://localhost:2006/encrypt' \
  -H 'accept: application/json'
{"session_id":"793e0fdc4bd100ea","word":"tekieronene"}
deka@SKH-KUBUNTU:~$ openssl rand -hex 16 > key26
deka@SKH-KUBUNTU:~$ openssl rand -hex 16 >wektor.IV
deka@SKH-KUBUNTU:~$ echo -n 'tekieronene' > zad26.txt
deka@SKH-KUBUNTU:~$ openssl enc -aes-128-ecb -in zad26.txt -K $(cat key26) -K $(cat wektor.IV) -out zad26.enc -base64
deka@SKH-KUBUNTU:~$ cat 26.enc
cat: 26.enc: No such file or directory
deka@SKH-KUBUNTU:~$ cat zad26.enc
4tZz/XuaKrDsduTVC4qqcw==

zad2.7

openssl enc -d -aes-256-cbc -in zad27.enc -out zad27.dec -pbkdf2 -pass:$(cat pass27.txt) -base64



  




 




