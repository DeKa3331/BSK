tworzenie klucza:

deka@SKH-KUBUNTU:~$ gpg --full-generate-key
gpg (GnuPG) 2.2.40; Copyright (C) 2022 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 1024
Requested keysize is 1024 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: jakub
Email address: jakub@test.pl
Comment: none
You selected this USER-ID:
    "jakub (none) <jakub@test.pl>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: /home/deka/.gnupg/trustdb.gpg: trustdb created
gpg: directory '/home/deka/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/deka/.gnupg/openpgp-revocs.d/C1993C8FFA793A91B21B5B36067FBC2603B2D56B.rev'
public and secret key created and signed.

pub   rsa1024 2025-11-17 [SC]
      C1993C8FFA793A91B21B5B36067FBC2603B2D56B
uid                      jakub (none) <jakub@test.pl>
sub   rsa1024 2025-11-17 [E]


hasla mozna nie wpisywac zadziala

zeby wyswietlic:
deka@SKH-KUBUNTU:~$ gpg --list-keys
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
/home/deka/.gnupg/pubring.kbx
-----------------------------
pub   rsa1024 2025-11-17 [SC]
      C1993C8FFA793A91B21B5B36067FBC2603B2D56B
uid           [ultimate] jakub (none) <jakub@test.pl>
sub   rsa1024 2025-11-17 [E]



gpg --armor --export jakub@test.pl >pub key



deka@SKH-KUBUNTU:~$ gpg --armor --export-secret-key jakub@test.pl >pub key
deka@SKH-KUBUNTU:~$ cat key
1fbcf99a5131a6a0094c2a40a1a0b8dddeka@SKH-KUBUNTU:~$ cat pub key
-----BEGIN PGP PRIVATE KEY BLOCK-----

lQHYBGka6zkBBADIyhgF45BZVPwyrN2SkEEHArxJsMzCB2u8jJRKaxme9XW6EDX5
ahq0tXaO2dVMD1GRhNCMwFNEAxCV0aduRnRqPyzwWMl1gOiTe5iyUDF3MDmlHptq
BEEwpVbRqKHvHu4NVE1tF/sJEFYt8mDB0zuCfvBIaXvP9AyjOhpQw1D2TwARAQAB
AAP/Y+sVu1B8E8hT3E/jzzyT744v7qfZrTCOL3zxinrzfAQAOsA4a86eTZED16CV
IU16NOUX9wL6LJ0t0rBLFnhfE2JUcOs4B1KLd4EK8vUF5oOAYy5JYZ8RPRW0DGe1
V+X+L+/04Ux1PAKlKT7sVhUw+esgS/0d2t5FXchpgWq6o+kCANlBJUSNiEqgqSja
4e2CguCIKt9EozqTI+RFCechIIjclWGYwdpge5aM9GA7RjJlwIfvOLVyxKUzpmeP
lRPMEiUCAOyZOpn192l8V7YvU9ftNqEyXvbz/1tIpahXkgz0ra+OKRTqdd5ME4JV
O1QbMSeY0/aYImndiqjPdSy5XH3GimMCAJOIHfkciCJZCxzhaHkMermGe4kKaMTv
lb2v90sqd7XXr/VS33qeGG4HPdUAfbM5sYB2se0lX9ctaONfM4+246ugybQcamFr
dWIgKG5vbmUpIDxqYWt1YkB0ZXN0LnBsPojOBBMBCgA4FiEEwZk8j/p5OpGyG1s2
Bn+8JgOy1WsFAmka6zkCGwMFCwkIBwIGFQoJCAsCBBYCAwECHgECF4AACgkQBn+8
JgOy1WvnPgQAsiB9iqnqD1jBW/A86LrGpMLhL34iLWma+9e8julL1cEOC3JZGihG
9R4rYNGuDZ7/+5riicUH0upO4RE/H3mXQGuUUGR1Mu430WcRwvEOmZtCqRxvM2o2
Js0UX8XE957EM2yDBzhqGYO7x5BrP9ulZaC3drMuigX1eaHu6ra1RgqdAdgEaRrr
OQEEAMN/+Ogqls1eKKi7paHZkfFR/440pDavcKesBqV/SU/FJX+GelggS3GaTwij
OJLJkUeNS22DgojiPpD1o5U9qhYckW31CSfSXW11WWOq1LwtGLONHHPwfeTn2iPX
wnXgchfZBcQcMhTtQkIZHlEOqNNY1Y/gzmtLoRwCZ6kAxemPABEBAAEAA/9c8bru
+cx/L5xJ+AhbZbpWTgMe4xUNMKRw+r6gMN80TwiwU8lXm2byyAd6FktfsffhWiH5
m1PUayeOuFHAsrPpAUHZ+f88pAenCPR63vhB14dQBfp9HA9RuR//INLcIyI8S0EL
FzuoGpKkBCHV+rQv+4/UocdYjPnSXfm/dUa/6QIA1EScvQX3Wfh1IYsF975SoIZ5
/Y2CRx00l7Ai8UGFfjpf1HDsim/moXXrDYLYAp8PGBoo+hqghHSx6Bo1cwaRqQIA
68b6zYb2KCjd+xk2yZhYw9IQstjtV/NPjMx4kHqYqHbRD7MOBENjT1yxGzYZVbRN
kwQS3znDxFC1Db4yPv8UdwIA6EyuZCGEnfIceXVeROhBVQSMc0opiuvIHowNtfZe
f/MA3fL+KP7cvwcTN0Ezwsf8nbYYhipZOQKuKkLxlLjZiKFaiLYEGAEKACAWIQTB
mTyP+nk6kbIbWzYGf7wmA7LVawUCaRrrOQIbDAAKCRAGf7wmA7LVawTaBACwMK5Y
t5KMGN/p3j7wkFKJoELcLRpQ896z/9N+i+WmNtpXsKrs5Gw5HYjobWSbXXF62u9B
Zpysy6Xz6IE6vIojI4DAIwcPck4eSe9cldKNaVsXUHWs3SRXby3BTyfSs8GxiBV2
TTx3GkRAZLJUIM7Rh3yb4TuYCo5iSufiEWnPrw==
=KjE/
-----END PGP PRIVATE KEY BLOCK-----
1fbcf99a5131a6a0094c2a40a1a0b8dddeka@SKH-KUBUNTU:~$ 


curl -X POST http://127.0.0.1:5001/submit/private -F "file=@priv.key"


deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5001/submit/private -F "file=@priv.key"
{
  "algo": "1",
  "created": "1763371833",
  "expires": "Never",
  "fingerprint": "C1993C8FFA793A91B21B5B36067FBC2603B2D56B",
  "key_id": "067FBC2603B2D56B",
  "length": "1024",
  "trust": "-",
  "type": "private",
  "uids": [
    "jakub (none) <jakub@test.pl>"
  ]
}





zad2

deka@SKH-KUBUNTU:~$ gpg --full-generate-key
gpg (GnuPG) 2.2.40; Copyright (C) 2022 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection? 2
DSA keys may be between 1024 and 3072 bits long.
What keysize do you want? (2048) 1024
Requested keysize is 1024 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: Aki
Name must be at least 5 characters long
Real name: Akis
Name must be at least 5 characters long
Real name: Aakis
Email address: Aakis@test.pl
Comment: skip
You selected this USER-ID:
    "Aakis (skip) <Aakis@test.pl>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: revocation certificate stored as '/home/deka/.gnupg/openpgp-revocs.d/50230753DCA45B5838FAA8715B2D42C08D873620.rev'
public and secret key created and signed.

pub   dsa1024 2025-11-17 [SC]
      50230753DCA45B5838FAA8715B2D42C08D873620
uid                      Aakis (skip) <Aakis@test.pl>
sub   elg1024 2025-11-17 [E]


deka@SKH-KUBUNTU:~$ gpg --armor --export-secret-key Aakis@test.pl >priv.key
deka@SKH-KUBUNTU:~$ gpg --armor --export Aakis@test.pl >pub.key


deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5002/submit/public -F "file=@pub.key"
{
  "algorithm": "DSA",
  "created": "1763372357",
  "expires": "Never",
  "fingerprint": "50230753DCA45B5838FAA8715B2D42C08D873620",
  "format": "GPG/OpenPGP",
  "key_id": "5B2D42C08D873620",
  "key_size": 1024,
  "trust": "-",
  "type": "public",
  "uids": [
    "Aakis (skip) <Aakis@test.pl>"
  ]
}




deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5002/submit/private -F "file=@priv.key"
{
  "algorithm": "DSA",
  "created": "1763372357",
  "expires": "Never",
  "fingerprint": "50230753DCA45B5838FAA8715B2D42C08D873620",
  "format": "GPG/OpenPGP",
  "key_id": "5B2D42C08D873620",
  "key_size": 1024,
  "trust": "-",
  "type": "private",
  "uids": [
    "Aakis (skip) <Aakis@test.pl>"
  ]
}




zad5.3
deka@SKH-KUBUNTU:~$ gpg --full-generate-key
gpg (GnuPG) 2.2.40; Copyright (C) 2022 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 1024
Requested keysize is 1024 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) y
invalid value
Key is valid for? (0) 1y
Key expires at wto, 17 lis 2026, 10:49:25 CET
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: student
Email address: student@uczelnia.pl
Comment: none
You selected this USER-ID:
    "student (none) <student@uczelnia.pl>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: revocation certificate stored as '/home/deka/.gnupg/openpgp-revocs.d/70FD0D34955EDE90D76F4A2BC6685D25EFE79CFA.rev'
public and secret key created and signed.

pub   rsa1024 2025-11-17 [SC] [expires: 2026-11-17]
      70FD0D34955EDE90D76F4A2BC6685D25EFE79CFA
uid                      student (none) <student@uczelnia.pl>
sub   rsa1024 2025-11-17 [E] [expires: 2026-11-17]


deka@SKH-KUBUNTU:~$ gpg --armor --export student@uczelnia.pl >pub.key
deka@SKH-KUBUNTU:~$ gpg --armor --export-secret-key student@uczelnia.pl >priv.key

deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5003/submit/public -F "file=@pub.key"
{
  "algo": "1",
  "created": "1763372981",
  "expires": "1794908981",
  "fingerprint": "70FD0D34955EDE90D76F4A2BC6685D25EFE79CFA",
  "key_id": "C6685D25EFE79CFA",
  "length": "1024",
  "trust": "-",
  "type": "public",
  "uids": [
    "student (none) <student@uczelnia.pl>"
  ],
  "validation": "passed"
}

deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5003/submit/private -F "file=@priv.key"
{
  "algo": "1",
  "created": "1763372981",
  "expires": "1794908981",
  "fingerprint": "70FD0D34955EDE90D76F4A2BC6685D25EFE79CFA",
  "key_id": "C6685D25EFE79CFA",
  "length": "1024",
  "trust": "-",
  "type": "private",
  "uids": [
    "student (none) <student@uczelnia.pl>"
  ],
  "validation": "passed"
}


zad5.4

deka@SKH-KUBUNTU:~$ curl -X GET "http://localhost:5004/decrypt" -H  "accept: application/zip" -o zad54.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   519  100   519    0     0    385      0  0:00:01  0:00:01 --:--:--   385
deka@SKH-KUBUNTU:~$ unzip zad54.zip
Archive:  zad54.zip
  inflating: encrypted.txt           
  inflating: passphrase.txt          
  inflating: session_id.txt          
deka@SKH-KUBUNTU:~$ 


deka@SKH-KUBUNTU:~$ cat passphrase.txt
admin

deka@SKH-KUBUNTU:~$ gpg --cipher-aGNU Privacy Guard - GPG Zadania
5.5 Pod adresem http: // 127. 0. 0. 1: 5005 dziaªa prosty serwer HTTP udost¦pniaj¡cy 2 endpointy: http:
// 127. 0. 0. 1: 5005/ encrypt oraz http: // 127. 0. 0. 1: 5005/ submit .
(a) Uruchom serwer za pomoc¡ poni»szego polecenia:
docker run -p 5005:5005 --name ex5 docker.io/mazurkatarzyna/gpg-ex5:latest
podman run -p 5005:5005 --name ex5 docker.io/mazurkatarzyna/gpg-ex5:latest
Je±li Docker Hub nie odpowiada, u»yj obrazu zapasowego:
docker run -p 5005:5005 --name ex5 ghcr.io/mazurkatarzynaumcs/gpg-ex5:latest
podman run -p 5005:5005 --name ex5 ghcr.io/mazurkatarzynaumcs/gpg-ex5:latest
(b) Wy±lij request do endpointa http://127.0.0.1:5005/encrypt u»ywaj¡c meody HTTP GET. W od-
powiedzi od serwera otrzymasz sªowo do zaszyfrowania (jako word_to_encrypt), hasªo potrzebne do
szyfrowania (jako passphrase) oraz id sesji (jako session_id).
(c) Zaszyfruj odebrane od serwera sªowo (word_to_encrypt) za pomoc¡ algorytmu AES128 oraz odebra-
nego od serwera hasªa (passphrase). Zaszyfrowane sªowo ma by¢ równie» zakodowane przy pomocy
kodowania base64.
(d) Wy±lij request do endpointa http://127.0.0.1:5005/submit u»ywaj¡c meody HTTP POST i prze±lij
do serwera id sesji (jako session_id) oraz zaszyfrowany i zakodowany plik (jako plik, encrypted_file).lgo CAMELLIA128 --decrypt encrypted.txt>decrypted.txt
gpg: CAMELLIA128.CFB encrypted data
gpg: encrypted with 1 passphrase
deka@SKH-KUBUNTU:~$ 
(haslo wpisujemy z passphrase u mnie admin)

test:
curl -X POST "http://localhost:5004/submit" -H  "accept: application/json" -H  "Content-Type: application/json" -d "{  \"decrypted_text\": \"password\",  \"session_id\": \"92358d1a855d1d5236a94b5591545d4e\"}"

{
  "message": "Gratulacje! Poprawnie odszyfrowałeś plik!",
  "passphrase_used": "admin",
  "secret_word": "password",
  "status": "success"
}

zad5.5





curl -X GET "http://localhost:5005/encrypt" -H  "accept: application/json"{
  "session_id": "b847500304f1788e9c992f4969415fdd",
  "word_to_encrypt": "celtics",
  "passphrase": "roses",
  "algorithm": "AES128",
  "instructions": "Użyj GPG do zaszyfrowania słowa algorytmem AES128 z podanym hasłem. Następnie wyślij zaszyfrowany plik do /submit wraz z session_id."


echo -n 'celtics' > zad55.txt


gpg --symmetric --cipher-algo AES128 --armor --output enc55.txt zad55.txt
haslo wpisujemy z polecenia:roses

deka@SKH-KUBUNTU:~$ cat enc55.txt
-----BEGIN PGP MESSAGE-----

jA0EBwMCJv9j0krPfnH/0kYBiH/kuG8cdfr6HjmzTeAddP5cfGO+G4PsTa5YO0M1
y8q63LKRoY08aPnJ2928zvXAdv8s+IPl8hX8lC/AcOaWfWnghMcN
=8c8Z
-----END PGP MESSAGE-----


curl -X POST "http://localhost:5005/submit" -H  "accept: application/json" -H  "Content-Type: multipart/form-data" -F "session_id=b847500304f1788e9c992f4969415fdd" -F "encrypted_file=@enc55.txt;type=text/plain"


{
  "status": "success",
  "message": "Gratulacje! Poprawnie zaszyfrowałeś plik!",
  "word": "celtics",
  "passphrase_used": "roses"
}

zad5.6

}deka@SKH-KUBUNTU:~$ curl -X get http://127.0.0.1:5006/encrypt -o zad56.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  2637  100  2637    0     0   4766      0 --:--:-- --:--:-- --:--:--  4759

deka@SKH-KUBUNTU:~$ unzip zad56.zip
Archive:  zad56.zip
replace word.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: word.txt                
  inflating: public_key.asc          
  inflating: private_key.asc         
replace session_id.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: session_id.txt   


jak nie mamy to mozemy dodac nowy klucz:
deka@SKH-KUBUNTU:~$ gpg --import public_key.asc
gpg: key 4DD9C937F5634DA6: public key "Challenge User <challengex6@example.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1


deka@SKH-KUBUNTU:~$ gpg --encrypt --recipient D1342FBAD3855680D529FDBF4DD9C937F5634DA6 --armor --output encrypted.txt  word.txt
gpg: 4DD9C937F5634DA6: There is no assurance this key belongs to the named user

pub  rsa2048/4DD9C937F5634DA6 2025-11-17 Challenge User <challengex6@example.com>
 Primary key fingerprint: D134 2FBA D385 5680 D529  FDBF 4DD9 C937 F563 4DA6

It is NOT certain that the key belongs to the person named
in the user ID.  If you *really* know what you are doing,
you may answer the next question with yes.

Use this key anyway? (y/N) y
File 'encrypted.txt' exists. Overwrite? (y/N) y



curl -X POST "http://localhost:5006/submit" -H  "accept: application/json" -H  "Content-Type: multipart/form-data" -F "session_id=2915975e86338f370c054d7738d5da24" -F "encrypted_file=@encrypted.txt;type=text/plain"



{
  "status": "success",
  "message": "Gratulacje! Poprawnie zaszyfrowałeś plik!",
  "word": "april"
}

zad5.7
deka@SKH-KUBUNTU:~$ curl -X get http://127.0.0.1:5007/decrypt -o zad57.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  3363  100  3363    0     0   7924      0 --:--:-- --:--:-- --:--:--  7931

deka@SKH-KUBUNTU:~$ unzip zad57.zip
Archive:  zad57.zip
replace public_key.asc? [y]es, [n]o, [A]ll, [N]one, [r]ename: A
  inflating: public_key.asc          
  inflating: private_key.asc         
  inflating: encrypted_word.asc      
  inflating: session_id.txt          
  inflating: README.txt   


gpg --import private_key.asc

gpg --decrypt encrypted_word.asc

curl -X post http://127.0.0.1:5007/submit

curl -X POST "http://localhost:5007/submit" -H  "accept: application/json" -H  "Content-Type: multipart/form-data" -F "session_id=92d19001863fb3ce6b41811b05c70c2a" -F "decrypted_word=simple"

{
  "status": "success",
  "message": "🎉 Gratulacje! Poprawnie odszyfrowałeś słowo!",
  "word": "simple"
}
  
zad5.8

deka@SKH-KUBUNTU:~$curl -X GET "http://localhost:5008/sign" -o zad58.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  2615  100  2615    0     0   2253      0  0:00:01  0:00:01 --:--:--  2254



deka@SKH-KUBUNTU:~$ unzip zad58.zip
Archive:  zad58.zip
replace word.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename: A
  inflating: word.txt                
  inflating: public_key.asc          
  inflating: private_key.asc         
  inflating: session_id.txt    

 gpg --import private_key.asc


gpg --sign -u C32F2976C4E1C2F233FC6DCBAC70C57414D2EBCE word.txt
curl -X POST "http://localhost:5008/submit" -H  "accept: application/json" -H  "Content-Type: multipart/form-data" -F "session_id=64b6cb667c62c137283fd2b375eb29cc" -F "signed_file=@word.txt.gpg;type=application/pgp-encrypted"


{
  "status": "success",
  "message": "✍️ Gratulacje! Poprawnie podpisałeś plik!",
  "word": "mike",
  "signer": "Sign Challenge <sign@example.com>",
  "signature_valid": true
}
  





























