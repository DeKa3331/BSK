slowniki musza byc w /home nigdzie indziej inaczej nie zadziala! w tym samym pliku.
hashcat --help po numerek

zad4.1
tworzenie:
curl -X 'GET' \
  'http://127.0.0.1:4001/hash' \
  -H 'accept: application/json'

 echo -n '193cebe9624d90431f3ba55150677351' >hash.txt

brute force slownikowy:
 hashcat -m 0 -a 0 hash.txt wordlist.txt

 musimy dostac cracked:
 Session..........: hashcat
Status...........: Cracked


rozkodowane haslo:
deka@SKH-KUBUNTU:~$ hashcat -m 0  hash.txt --show
193cebe9624d90431f3ba55150677351:mystyno1

test:
curl -X 'POST' \
  'http://127.0.0.1:4001/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "word": "mystyno1"
}'

}'
{"success": true, "message": "Gratulacje! Poprawnie złamano hash!", "word": "mystyno1", "hash": "193cebe9624d90431f3ba55150677351"}d

zad4.2
generacja:
curl -X 'GET' \
  'http://127.0.0.1:4002/hash' \
  -H 'accept: application/json'

aby zmienic musimy sparwdzic jaki numer ma sha-1 (100)
hashcat --help
-a 0 <-tryb slownikowy
-m 0 <-wyborw ktorego hasha
 hashcat -m 100 -a 0 hash42.txt wordlist.txt


d763fbf7e641f036d7840799eb7ddd8cb167a33b:kingsley     
 Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 100 (SHA1)

hashcat -m 100  hash42.txt --show
d763fbf7e641f036d7840799eb7ddd8cb167a33b:kingsley

TEST:

curl -X 'POST' \
  'http://127.0.0.1:4002/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "word": "kingsley"
}'

{"success": true, "message": "Gratulacje! Poprawnie złamano hash!", "word": "kingsley", "hash": "d763fbf7e641f036d7840799eb7ddd8cb167a33b"}d

zad4.5
generacja:
curl -X 'GET' \
  'http://127.0.0.1:4005/hash' \
  -H 'accept: application/json'

echo -n '$2b$12$LGOhydY0Vh1oXUZ1kdvN9.2UfiPlF8A2ekVSaFT48X42SBmy2RPIu' >hash45.txt

bcrypt number: 3200
 hashcat -m 3200 -a 0 hash45.txt wordlist.txt



  $2b$12$LGOhydY0Vh1oXUZ1kdvN9.2UfiPlF8A2ekVSaFT48X42SBmy2RPIu:wattere
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 3200 (bcrypt $2*$, Blowfish (Unix))


deka@SKH-KUBUNTU:~$ curl -X 'POST' \
  'http://127.0.0.1:4005/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "word": "wattere"
}'
{"success": true, "message": "Gratulacje! Poprawnie złamano hash!", "word": "wattere", "hash": "$2b$12$LGOhydY0Vh1oXUZ1kdvN9.2UfiPlF8A2ekVSaFT48X42SBmy2RPIu"}



zad47

crunch minimumZnakow maximumZnakow zCzegoSieSklada
crunch 3 3 0123456789 -o digits.txt
Crunch will now generate the following amount of data: 4000 bytes
0 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 1000 

crunch: 100% completed generating output


echo -n '5c7d5705ab73466c0584cc782cb12d2e' >hash47.txt
 hashcat -m 0 -a 0 hash47.txt digits.txt

 5c7d5705ab73466c0584cc782cb12d2e:029                      
                                                          
Session..........: hashcat
Status...........: Cracked

curl -X 'POST' \
  'http://127.0.0.1:4007/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "word": "029"
}'

{"success": true, "message": "Gratulacje! Poprawnie złamano hash!", "word": "029", "hash": "5c7d5705ab73466c0584cc782cb12d2e"}



zad4.12

hashcat maski: https://github.com/noobosaurus-r3x/Cheat-sheets/blob/main/Hashcat%20Cheat%20Sheet.md#mask-attack

generacja:
curl -X 'GET' \
  'http://127.0.0.1:4012/hash' \
  -H 'accept: application/json'
echo -n '99c9e12638272e9beae26726d05b8bf2f6abaf2c' >hash412.txt


hashcat -a 3 -m 100 hash412.txt '?l?l?l?l'

99c9e12638272e9beae26726d05b8bf2f6abaf2c:klsa             
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 100 (SHA1)

curl -X 'POST' \
  'http://127.0.0.1:4012/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "word": "klsa"
}'

{
  "success": true,
  "message": "Gratulacje! Poprawnie złamano hash!",
  "word": "klsa",
  "hash": "99c9e12638272e9beae26726d05b8bf2f6abaf2c"
}



zad4.13
generujemy tak jak zawsze:
echo -n '6aeec887749cf0651bd1418576c4d0992d9a5331'>hash413.txt


tak bedzie wygladac maska:
hashcat -m 100 -a 3 hash413.txt '?u?d?d?d'

6aeec887749cf0651bd1418576c4d0992d9a5331:O629             
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 100 (SHA1)



curl -X 'POST' \
  'http://127.0.0.1:4013/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "word": "O629"
}'

{
  "success": true,
  "message": "Gratulacje! Poprawnie złamano hash!",
  "word": "O629",
  "hash": "6aeec887749cf0651bd1418576c4d0992d9a5331"
}


4.14
generacja:
ship, zapisuje tylko:
echo -n '2db3588f39a4001e5e37f6c07bd27936b10924fc' >hash414.txt

lamanie, napierw wpisujemy co chcemy -1abc -2 468 tutaj ustawiamy ze 1 to ma byc tylko a,b lub c itd nastepnie maski na koncu uzywamy z 1,2,3.:
hashcat -m 100 -a 3 hash_to_crack.txt -1 abc -2 468 -3 '*%:' '?1?2?3'

2db3588f39a4001e5e37f6c07bd27936b10924fc:c6*              
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 100 (SHA1)

curl -X 'POST' \
  'http://127.0.0.1:4014/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "word": "c6*"
}'

{
  "success": true,
  "message": "Gratulacje! Poprawnie złamano hash!",
  "word": "c6*",
  "hash": "2db3588f39a4001e5e37f6c07bd27936b10924fc"
}


zad4.15
TBD
zad4.16
curl -X 'GET' \
  'http://127.0.0.1:4016/hash' \
  -H 'accept: application/json'

echo -n 'c7ca70b16e73f70ee493f773952b77e190d1afffd5596a8c92bc1ef48926e5db' >hash416.txt


sha256-1400

hashcat -a 6 -m 1400 hash416.txt input.txt '?d?d'
c7ca70b16e73f70ee493f773952b77e190d1afffd5596a8c92bc1ef48926e5db:12345672
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 1400 (SHA2-256)

curl -X 'POST' \
  'http://127.0.0.1:4016/submit' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "word": "12345672"
}'

{
  "success": true,
  "message": "Gratulacje! Poprawnie złamano hash!",
  "word": "12345672",
  "hash": "c7ca70b16e73f70ee493f773952b77e190d1afffd5596a8c92bc1ef48926e5db"
}



  

