slowniki musza byc w /home nigdzie indziej inaczej nie zadziala! w tym samym pliku.
hashcat --help po numerek

,	WIELKIE litery
@	małe litery
%	cyfry
^	znaki specjalne


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

{"success": true, "message": "Gratulacje! Poprawnie złamano hash!", "word": "kingsley", "hash": "d763fbf7e641f036d7840799eb7ddd8cb167a33b"}



zad4.3
curl -X 'GET' \
  'http://127.0.0.1:4003/hash' \
  -H 'accept: application/json'

  {
  "hash": "0ffe1abd1a08215353c233d6e009613e95eec4253832a761af28ff37ac5a150c",
  "message": "Spr\u00f3buj z\u0142ama\u0107 ten hash!"
}

echo -n '0ffe1abd1a08215353c233d6e009613e95eec4253832a761af28ff37ac5a150c'>hash43.txt

 hashcat -m 1400 -a 0 hash43.txt wordlist.txt

poprawnie wiec skip

zad4.4
 hashcat -m 1700 -a 0 hash44.txt wordlist.txt



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

zad4.6

echo -n 'SCRYPT:1024:1:1:11NVfz2YM//PS/fwvEvHXw==:5/+1x4C7w8ucH6s+0PXzW2dlCfTzMOYURRkEmhjeXlk=' >hash44.txt
 hashcat -m 8900 -a 0 hash44.txt wordlist.txt
                                                
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 8900 (scrypt)
Hash.Target......: SCRYPT:1024:1:1:11NVfz2YM//PS/fwvEvHXw==:5/+1x4C7w8...jeXlk=
Time.Started.....: Sun Nov 30 19:42:11 2025 (2 secs)
Time.Estimated...: Sun Nov 30 19:42:13 2025 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (wordlist.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:       22 H/s (0.33ms) @ Accel:16 Loops:1024 Thr:1 Vec:1
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 32/50 (6
zad4.7

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


zad4.8

echo -n 'f322989d01b7600a3ae2a3b3a45b22c8' > hash48.txt


crunch 4 4 ABCDEFGHIJKLMNOPQRSTUVWXYZ > wordlist.txt

hashcat -m 0 -a 0 hash.txt wordlist.txt

                                      
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 0 (MD5)
Hash.Target......: f322989


zad4.9 (blad w poleceniu tam sa 2liczby zamiast 4)
generacja:

deka@SKH-KUBUNTU:~$ curl -X 'GET'   'http://127.0.0.1:4009/hash'   -H 'accept: application/json'
{
  "hash": "0c4f5f8fd16ab0b20a152fab22c3c11c",
  "message": "Spr\u00f3buj z\u0142ama\u0107 ten hash!"
}

echo -n 0c4f5f8fd16ab0b20a152fab22c3c11c >hash

tworzenie slownika:
crunch 8 8 -t pass%% -o slownik49.txt
Crunch will now generate the following amount of data: 90000 bytes
0 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 10000 

crunch: 100% completed generating output


lamanie z uzyciem slownika i maski: (dlatego -a 3)
hashcat -m 0 -a 3 hash slownik49.txt


(podglad):
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 0 (MD5)
Hash.Target......: 0c4f5f8fd1

wyswietlanie zlamanego hasha:
hashcat -m 0 hash --show

deka@SKH-KUBUNTU:~$ hashcat -m 0 hash --show
0c4f5f8fd16ab0b20a152fab22c3c11c:pass99



zad4.10
echo -n 'bb0f7e021d52a4e31613d463fc0525d8' >hash410.txt

generacja z permutacji:
crunch 1 1 -p admin password 123 > wordlist.txt

 hashcat -m 0 -a 0 hash410.txt wordlist.txt


bb0f7e021d52a4e31613d463fc0525d8:adminpassword123         
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 0 (MD

zad4.11

crunch 5 5 -t ,@%^^ -o wordlist.txt


echo -n '23f734bbf3744e2ad797bf6071afaae0' >hash411.txt

 hashcat -m 0 -a 0 hash411.txt wordlist.txt


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
echo -n '09408778b720080d6c1024362c49ec8ae2b8b23f' >hash415.txt

hashcat -m 100 -a 3 hash415.txt -1 0123456789abcdef '00:14:22:ff:ff:?1?1


                                   
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 100 (SH

zad4.16
curl -X 'GET' \
  'http://127.0.0.1:4016/hash' \
  -H 'accept: application/json'

echo -n 'c7ca70b16e73f70ee493f773952b77e190d1afffd5596a8c92bc1ef48926e5db' >hash416.txt


sha256-1400
  6 | Hybrid Wordlist + Mask
  7 | Hybrid Mask + Wordlist



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

zad4.17
 echo -n 'b877e59a00217961b92230e39e131250de2e44b7d3e7ceeae95a0d858b6b652d' >hash417.txt

 hashcat -m 0 -a 7 hash.txt top10.txt -1 '!@#$%&*' '?l?d?1'

zad4.18
nano imiona_zenskie.txt

wpisuje

Anna
Alicja
Natalia
Eliza
Kinga
Karolina
Nela
Monika
Martyna
Agnieszka

plik z zasadami:
nano leet.rule

sa@
se3
si1

s a @ → zamień a na @

s e 3 → zamień e na 3

s i 1 → zamień i na 1

hashcat -m 100 -a 0 hash.txt imiona_zenskie.txt -r leet.rule

jezeli chcielisbysmy dodawac wiecej zasad to mozemy tak: -r rules/best64.rule -r leet.rule


zad4.19
tak smao jak wyzej ale plik z zasadami wyglada tak:

sa4
se3
so0
$_
$2
$0
$2
$5
$!


sa4	a → 4
se3	e → 3
so0	o → 0
$_	dodaje _
$2	dodaje 2
$0	dodaje 0
$2	dodaje 2
$5	dodaje 5
$!	dodaje !

zad4.20

^!
$#
| Reguła | Działanie              |
| ------ | ---------------------- |
| `^!`   | dodaje `!` na początku |
| `$#`   | dodaje `#` na końcu    |

przypomniam schemat uzycia:
hashcat -m 0 -a 0 hash.txt cert.txt -r cert.rule



zad4.21
fcrackzip -u -D -p wordlist.txt secure.zip
-u – sprawdza poprawność hasła

-D – tryb słownikowy

-p – plik ze słownikiem

unzip secure.zip



. zip2john + hashcat
Krok 1 – wyciągnij hash z ZIP-a
zip2john secure.zip > zip_hash.txt

Krok 2 – uruchom hashcat

Tryb ZIP (najczęściej):

hashcat -m 13600 -a 0 zip_hash.txt wordlist.txt


Jeśli to starszy zip:

hashcat -m 17200 -a 0 zip_hash.txt wordlist.txt


Kiedy hasło zostanie znalezione – rozpakuj:

unzip secure.zip

zad4.22
zip2john challenge.zip > zip_hash.txt
crunch 5 6 0123456789 -o słownik.txt

to co mi zadzialalo:

fcrackzip -b -c 1 -l 5-6 -u challenge.zip

-b ->brute force
-c ->cyfry
-l ->dlugosc 5 do 6
-u ->weryfikacja przed wyswietleniem
4.23
potrzebuje slownik np:
crunch 11 11 92070100000 92123199999 -o pesel.txt

pdfcrack -w pesel.txt challenge.pdf






5cyfr:
hashcat -m 13600 -a 3 zip_hash.txt ?d?d?d?d?d
6cyfr:
hashcat -m 13600 -a 3 zip_hash.txt ?d?d?d?d?d?d

hashcat -m 13600 -a 3 zip_hash.txt ?d?d?d?d?d,?d?d?d?d?d?d

unzip secure.zip









  

