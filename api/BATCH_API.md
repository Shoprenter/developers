# API batch feldolgozó

Az API kérések számának csökkentése, valamint a kérések gyorsabb kiszolgálása érdekében, az API kéréseket kötegelt (batch) módon is fel tudjuk dolgozni. Ahhoz, hogy a batch feldolgozót igénybe tudjuk venni, egy speciális szerkezetű tömböt kell elküldenünk POST metódussal, az `[API_DOMAIN]/batch` URL-re.

## Működés

1. A kliens elküldi **POST** metódus segítségével, a kéréseket tartalmazó tömböt a `[API_DOMAIN]/batch` URL-re.

2. Az API ellenőrzi hogy a kliens rendelkezik-e megfelelő jogosultsággal a kérések kiszolgáláshoz, valamint hogy a kérések megfelelő szerkezetűk-e. Ha igen, akkor megkezdődik a kérések feldolgozása, ellenkező esetben a válasz valamilyen hibaüzenet formájában, a válaszoknak megfelelő struktúrában kerül visszaküldésre a kliensnek.

3. Egy ciklusban feldolgozza a szerver a kéréseket és egy speciális szerkezetű tömbben összegyűjti a kapott válaszokat.

4. Miután lefutott az összes kérés feldolgozása, a válaszokat tartalmazó tömböt a kérésnek megfelelő formátumban (javasoltan JSON, esetleg XML) a kimenetre küldi a szerver, amit aztán a kliens megkap és feldolgoz.

Batch kérés esetén az **ajánlott request szám 1000** legyen.

Egy post mérete *(max_post_size)* **32MB** lehet. Érdemes figyelni kép feltöltés esetén, hogy ezt ne lépjük túl.

**A lenti példákat szemléltetésképp mutatjuk be, ezért nem tartalmazzák az egész API request-et és response-t!**

## API kérés

<table>
  <tr>
    <td><b>method:</b></td>
    <td>POST</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/batch</td>
  </tr>
  <tr>
    <td><b>headers:</b></td>
    <td>
        Accept:application/json<br>
        Content-Type:application/json
    </td>
  </tr>
</table>

A API kérés a következő struktúrát kell hogy kövesse:

```json
{
  "data": {
    "requests": [
      {
        "method": "GET",
        "uri": "http://shopname.api.shoprenter.hu/productExtend?full=1&limit=200&page=0"
      },
      {
        "method": "POST",
        "uri": "http://shopname.api.shoprenter.hu/products/[ID]"
      }
    ]
  }
}
```

- **method:** GET, POST, PUT, DELETE
- **uri:** A resource-okhoz kapcsolódó API URI
- **data:** POST vagy PUT esetén az adatokat tartalmazó objektum

## API válasz

```json
{
  "requests": {
    "request": [
      {
        "method": "GET",
        "uri": "http://shopname.api.shoprenter.hu/productExtend?full=1&limit=200&page=0",
        "response": {
          "header": { "statusCode": "200" },
          "body": {}
        }
      },
      {
        "method": "POST",
        "uri": "http://shopname.api.shoprenter.hu/products/[ID]",
        "response": {
          "header": { "statusCode": "200" },
          "body": {}
        }
      }
    ]
  }
}
```

- **statusCode:** HTTP státusz kódja. Ha rendben volt a kérés kiszolgálása, ennek az értéke 200, 201 vagy 204 egyébként a hibára utaló státuszkód
- **body:** a választ tartalmazza, hiba esetén a hiba szöveges üzenete

**Bármilyen error keletkezik a batch API-n belüli kérésekben, technikai okok miatt, minden esetben 200-as státuszkóddal tér vissza, így a batch requestekben szereplő statusCode-okat a kliens alkalmazásban kell vizsgálni.**

[További gyakorlati példák a tömeges küldés használatára.](http://www.shoprenter.hu/images/batch.txt)

## Gyakori problémák

1. **Üres válasz, vagy "Data parameter not found in POST/PUT!" hibaüzenet 400-as státusz kóddal:**<br>
Értelemszerűen nem található **data** paraméter a küldött tömbben.
