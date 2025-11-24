
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







