
zad1
echo -n 'Linux' |md5sum
echo -n 'Linux' | openssl dgst -md5


zad2
echo -n 'Linux' | openssl dgst -sha256

zad3
echo -n "Linux" | base64

jesli chcemy zakodowac slowo zaszyfrowane:
echo -n 'Linux' | openssl dgst -md5 | base64 <-to zwroci blad bo md5 dostajemy ciag znakow z przodu

prawidlowe:
echo -n 'edc9f0a5a5d57797bf68e37364743831' >hash.txt
base64 hash.txt


zad4
echo -n "TGludXg=" | base64 --decode


zad5
generacja klucza przykladowa: (256bit->32*8)
openssl rand -hex 32

echo -n 'Linux' >slowo.txt

openssl enc -aes-256-ecb -in slowo.txt -out slowo.enc -K  e592bc9e5fa8618a02edf437bdf3ffd4fcdfbe9e588749db898a3662b461a80e 

jak wpiszemy **openssl** to dostaniemy liste algorytmow symetrycznych!!!

cat slowo.enc
���R��'�(���

i mozemy to zakodowac w base64 dodajac -a

openssl enc -a -aes-256-ecb -in slowo.txt -out slowo.enc -K  e592bc9e5fa8618a02edf437bdf3ffd4fcdfbe9e588749db898a3662b461a80e 

openssl enc -d -aes-256-ecb -in slowo.enc -out slowo.dec -K e592bc9e5fa8618a02edf437bdf3ffd4fcdfbe9e588749db898a3662b461a80e

cat slowo.dec
Linux

dziala :)


zad6
robie -a odrazu bo ladniej wyglada (jesli szyfrujemy z -a to i deszyfrujemy z -a to **wazne**)

openssl enc -a -aes-256-cfb -in slowo.txt -out slowo.enc -K e592bc9e5fa8618a02edf437bdf3ffd4fcdfbe9e588749db898a3662b461a80e -iv 83c468dc477543a6906912b6a1344416

cat slowo.enc

openssl enc -a -d -aes-256-cfb -in slowo.enc -out slowo.dec -K e592bc9e5fa8618a02edf437bdf3ffd4fcdfbe9e588749db898a3662b461a80e -iv 83c468dc477543a6906912b6a1344416

zad7

byloby tak samo z tym -a ja uzylem w 6 gdzie nie powinno byc ale dziala

zad8
f6NB8w==

echo -n 'f6NB8w==' | base64 -d >slowo.enc



openssl enc -d -aes-256-cfb -in slowo.enc -out slowo.dec -K e592bc9e5fa8618a02edf437bdf3ffd4fcdfbe9e588749db898a3662b461a80e -iv 83c468dc477543a6906912b6a1344416

cat slowo.dec
MFI


zad9
openssl rand -hex 16

zad10
echo -n 'Linux' >slowo.txt

openssl enc -aes-128-cbc -nosalt -in slowo.txt -out slowo.enc -pbkdf2 -iter 256 -a -pass pass:Ubuntu

cat slowo.enc
gpIb5SsCn+wwuKhTOCHAqw==


openssl enc -d -aes-128-cbc -nosalt -in slowo.enc -out slowo.dec -pbkdf2 -iter 256 -pass pass:Ubuntu

zad11

zad12

zad13

echo -n 'Linux' >slowo.txt

prywatny+publiczny:
openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out private.pem
publiczny z prywatnego:
openssl rsa -in private.pem -pubout -out public.pem


jesli dlugosc soli ma odpowiadac to np dla sha256 to jest 32 (z wikipedi)

podpisanie pliku (klucz prywatny):
openssl dgst -sha256 -sigopt rsa_padding_mode:pss -sigopt rsa_pss_saltlen:32 -sign private.pem -out signature slowo.txt

weryfikacja(klucz publiczny):
openssl dgst -sha256 -sigopt rsa_padding_mode:pss -sigopt rsa_pss_saltlen:32 -verify public.pem -signature signature slowo.txt

Verified OK

zad19
curl -X POST "http://127.0.0.1:5000/accepttext" -H  "accept: application/json" -H  "Content-Type: application/x-www-form-urlencoded" -d "text=test"


curl -X POST "http://127.0.0.1:5000/acceptfile" -F "file=@pub.key;type=application/vnd.apple.keynote"








