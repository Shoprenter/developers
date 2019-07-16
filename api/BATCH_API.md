# API batch feldolgozó

Az API kérések számának csökkentése, valamint a kérések gyorsabb kiszolgálása érdekében, az API kéréseket kötegelt (batch) módon is fel tudjuk dolgozni. Ahhoz, hogy a batch feldolgozót igénybe tudjuk venni, egy speciális szerkezetű tömböt kell elküldenünk POST metódussal, az `[API_DOMAIN]/batch` URL-re.

## Működés

1. A kliens elküldi **POST** metódus segítségével, a kéréseket tartalmazó tömböt a `[API_DOMAIN]/batch` URL-re.

2. Az API ellenőrzi hogy a kliens rendelkezik-e megfelelő jogosultsággal a kérések kiszolgáláshoz, valamint hogy a kérések megfelelő szerkezetűk-e. Ha igen, akkor megkezdődik a kérések feldolgozása, ellenkező esetben a válasz valamilyen hibaüzenet formájában, a válaszoknak megfelelő struktúrában kerül visszaküldésre a kliensnek.

3. Egy ciklusban feldolgozza a szerver a kéréseket és egy speciális szerkezetű tömbben összegyűjti a kapott válaszokat.

4. Miután lefutott az összes kérés feldolgozása, a válaszokat tartalmazó tömböt a kérésnek megfelelő formátumban (javasoltan JSON, esetleg XML) a kimenetre küldi a szerver, amit aztán a kliens megkap és feldolgoz.

Batch kérés esetén az **ajánlott request szám 1000** legyen.

Egy post mérete *(max_post_size)* **32MB** lehet. Érdemes figyelni kép feltöltés esetén, hogy ezt ne lépjük túl.

## API kérés

A API kérés a következő struktúrát kell hogy kövesse:

```
array(
    'requests' => array(
        0 => array(
            'method' => ...,
            'uri' => ...,
        ),
        1 => array(
            'method' => ...,
            'uri' => ...,
            'data' => array(...)
        ),
        ...
    )
)
```

- **method:** GET, POST, PUT, DELETE
- **uri:** A resource-okhoz kapcsolódó API URI
- **data:** POST vagy PUT esetén az adatokat tartalmazó tömb

## API válasz

```
<requests>
    <request>
        <method>GET</method>
        <uri>...</uri>
        <response>
            <header>
                <statusCode>...</statusCode>
            </header>
            <body>
                ...
            </body>
        <response>
    </request>
    <request>
        ...
    </request>
    ...
</requests>
```

- **statusCode:** HTTP státusz kódja. Ha rendben volt a kérés kiszolgálása, ennek az értéke 200, 201 vagy 204 egyébként a hibára utaló státuszkód
- **body:** a választ tartalmazza, hiba esetén a hiba szöveges üzenete

**Az API batch url technikai okok miatt minden esetben 200-as státuszkóddal tér vissza, így a batch requestekben szereplő statusCode-okat a kliens alkalmazásban kell vizsgálni.**

[További gyakorlati példák a tömeges küldés használatára.](http://www.shoprenter.hu/images/batch.txt)

## Gyakori problémák

1. **Üres válasz (<\/response>), vagy "Data parameter not found in POST/PUT!" hibaüzenet 400-as státusz kóddal:**<br>
Értelemszerűen nem található **data** paraméter a küldött tömbben. Ilyen formában küldjük el az adatok a /batch-re:

```
data[requests][0][method]=GET
data[requests][0][uri]=http://shopname.api.shoprenter.hu/products
data[requests][1][method]=GET
data[requests][1][uri]=http://shopname.api.shoprenter.hu/orders
```
