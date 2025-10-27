# Narzędzia Zadania

## 0.1 Wyświetl wszystkie informacje użytkownika Alice.  
curl -s http://127.0.0.1:5000/user/alice | jq .

## 0.2 Wyświetl imię i nazwisko użytkownika Alice.  
curl -s http://127.0.0.1:5000/user/alice | jq -r '"\(.name) \(.surname)"'

## 0.3 Wyświetl adres e-mail użytkownika Bob.  
curl -s http://127.0.0.1:5000/user/bob | jq -r .email

## 0.4 Wyświetl wiek użytkownika Alice.  
curl -s http://127.0.0.1:5000/user/alice | jq -r .age

## 0.5 Wyświetl nazwę miasta, w którym mieszka użytkownik Bob.  
curl -s http://127.0.0.1:5000/user/bob | jq -r .city

## 0.6 Wyświetl hobby użytkownika Alice.  
curl -s http://127.0.0.1:5000/user/alice | jq -r .hobbies

## 0.7 Sprawdź, czy jednym z hobby użytkownika Bob są gry.  
curl -s http://127.0.0.1:5000/user/bob | jq -r '(.hobbies | index("games")) != null'

## 0.8 Wyświetl pierwsze hobby użytkownika Alice.  
curl -s http://127.0.0.1:5000/user/alice | jq -r .hobbies[0]

## 0.9 Sprawdź, ile hobby ma użytkownik Bob, a ile użytkownik Alice.  
for u in alice bob; do
  echo "$u:" $(curl -s http://127.0.0.1:5000/user/$u | jq -r '.hobbies | length')
done

## 0.10 Wyświetl nazwę użytkownika i miasto jako jeden ciąg znaków, np. "Alice Smith from Warsaw".  
curl -s http://127.0.0.1:5000/user/alice | jq -r '"\(.name) \(.surname) from \(.city)"'

## 0.11 Wyświetl wszystkie przedmioty. Wyświetl nazwy wszystkich przedmiotów.  
curl -s http://127.0.0.1:5000/items | jq -r '.[].name'

## 0.12 Wyświetl przedmioty droższe niż 20 pln.  
curl -s http://127.0.0.1:5000/items | jq -r '.[] | select(.price > 20)'

## 0.13 Wyświetl przedmioty tańsze niż 30 pln.  
curl -s http://127.0.0.1:5000/items | jq -r '.[] | select(.price < 30)'

## 0.14 Posortuj przedmioty według ceny rosnąco, a następnie malejąco.  
### rosnąco  
curl -s http://127.0.0.1:5000/items | jq -r 'sort_by(.price)'  
### malejąco  
curl -s http://127.0.0.1:5000/items | jq -r 'sort_by(.price) | reverse'

## 0.15 Pobierz sumę cen wszystkich przedmiotów.  
curl -s http://127.0.0.1:5000/items | jq -r 'map(.price) | add'

## 0.16 Wyświetl przedmioty, których nazwa zawiera "item".  
curl -s http://127.0.0.1:5000/items | jq -r '.[] | select(.name | test("item"; "i"))'

## 0.17 Wyświetl przedmioty w przedziale cenowym 10-30 pln.  
curl -s http://127.0.0.1:5000/items | jq -r '.[] | select(.price > 10 and .price < 30)'

## 0.18 Wyświetl użytkowników, którzy mają więcej niż 2 hobby.  
for u in alice bob; do
  curl -s http://127.0.0.1:5000/user/$u | jq -r 'select(.hobbies | length > 2)'
done

## 0.19 Wyślij do serwera request typu POST (endpoint /echo) i wyświetl odpowiedź.  
curl -s -X POST http://127.0.0.1:5000/echo \
  -H "Content-Type: application/json" \
  -d '{"a": "b"}' | jq .

## 0.20 Wyślij do serwera request typu POST, który doda nowy przedmiot. Wyświetl wszystkie przedmioty po dodaniu.  
curl -s -X POST http://127.0.0.1:5000/items \
  -H "Content-Type: application/json" \
  -d '{"name": "ABC", "price": 123}' | jq .  
curl -s http://127.0.0.1:5000/items | jq .

## 0.21 Za pomocą requestu typu PUT, aktualizuj cenę przedmiotu o numerze 1. Wyświetl wszystkie przedmioty.  
curl -s -X PUT http://127.0.0.1:5000/items/1 \
  -H "Content-Type: application/json" \
  -d '{"price":321}' | jq .  
curl -s http://127.0.0.1:5000/items | jq .

## 0.22 Za pomocą requestu typu DELETE, usuń przedmiot o numerze 3. Wyświetl wszystkie przedmioty.  
curl -s -X DELETE http://127.0.0.1:5000/items/3 | jq .  
curl -s http://127.0.0.1:5000/items | jq .

## 0.23 Wyświetl przedmiot o największej cenie.  
curl -s http://127.0.0.1:5000/items | jq -r 'max_by(.price)'

## 0.24 Wyświetl wszystkie przedmioty z ceną podwyższoną o 10%.  
curl -s http://127.0.0.1:5000/items | jq -r 'map(.price = (.price * 1.1))'

## 0.25 Pobierz nazwy wszystkich użytkowników i ich wiek.  
for u in alice bob; do
  curl -s http://127.0.0.1:5000/user/$u | jq -r '"\(.name) \(.surname): \(.age)"'
done

## 0.26 Wyświetl hobby Alice jako string połączony przecinkami.  
curl -s http://127.0.0.1:5000/user/alice | jq -r '.hobbies | join(", ")'

## 0.27 Pobierz pierwszy i ostatni przedmiot z listy.  
curl -s http://127.0.0.1:5000/items | jq -r '.[0], .[-1]'

## 0.28 Sprawdź, czy są przedmioty droższe niż 100 pln.  
curl -s http://127.0.0.1:5000/items | jq -r '.[] | select(.price > 100)'

## 0.29 Utwórz nowy przedmiot za pomocą POST /items. Wyświetl odpowiedź serwera i następnie listę wszystkich przedmiotów.  
curl -s -X POST http://127.0.0.1:5000/items \
  -H "Content-Type: application/json" \
  -d '{"name": "NewItem", "price": 50}' | jq .  
curl -s http://127.0.0.1:5000/items | jq .

## 0.30 Zaktualizuj przedmiot id=2. Wyświetl odpowiedź serwera i następnie listę wszystkich przedmiotów.  
curl -s -X PUT http://127.0.0.1:5000/items/2 \
  -H "Content-Type: application/json" \
  -d '{"price": 200}' | jq .  
curl -s http://127.0.0.1:5000/items | jq .
