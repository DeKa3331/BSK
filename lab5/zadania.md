slowniki musza byc w /home nigdzie indziej inaczej nie zadziala! w tym samym pliku.

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



zad46








  



