# Nap terméke

Az alábbi példában bemutatásra kerül, hogy miként lehet a ShopRenter API-n keresztül nap termékét felvinni és módosítani.

## Bevezetés

A nap terméke egy speciális akciós árnak számít, ahol megadhatjuk, hogy a hét egy adott napján melyik termék legyen kiemelve, aminek akciós ára van.
 Ennek megadása az akciós árnál ismert [Product Special resource](https://www.shoprenter.hu/api/doc#product_special) segítségével történik.
 A nap termékét a webshop admin felületén a **Beállítások > Megjelenés > Modul beállítása** menüpont alatt lehet beállítani. [Bővebb információ](https://support.shoprenter.hu/hc/hu/articles/215106328-Aj%C3%A1nl%C3%B3-modulok#nap_termeke)
 
## Nap terméke hozzáadása

Habár a nap termék ugyanazt a **Product Special resource**-t használja, mint amikor akciós árakat veszünk fel, viszont a küldendő request az alábbiakban eltér:
- **A priority értéke -1**. Ennek az oka, hogy egy beállítandó nap terméken már lehetséges, hogy van akció beállítva.
- Kiegészül egy **type** mezővel, aminek `day_spec` értéket kell megadni.
- Kiegészül egy **dayOfWeek** mezővel, aminek 1-7 közötti egész számnak kell lennie.<br>
A hét napjai: 
  - 1 - hétfő;
  - 2 - kedd; 
  - 3 - szerda;
  - 4 - csütörtök;
  - 5 - péntek;
  - 6 - szombat;
  - 7 - vasárnap.
- Nem kötelező megadni a dateFrom mezőt.
- Nem kötelező megadni a dateTo mezőt.
- Nem kötelező megadni a minQuantity mezőt.
- Nem kötelező megadni a maxQuantity mezőt.
- Nem kötelező megadni a customerGroup mezőt.

### Példa

#### Request

<table>
  <tr>
    <td><b>method:</b></td>
    <td>POST</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/productSpecials</td>
  </tr>
  <tr>
    <td><b>headers:</b></td>
    <td>
        Accept:application/json<br>
        Content-Type:application/json
    </td>
  </tr>
</table>

```json
{
    "data": {
        "priority": -1,
        "price": 1000.0000,
        "product": {
            "id": "cHJvZHVjdC1wcm9kdWN0X2lkPTE2OQ=="
        },
        "type": "day_spec",
        "dayOfWeek": 4
    }
}
```

#### Response

```json
{
    "href": "http://shopname.api.shoprenter.hu/productSpecials/cHJvZHVjdFNwZWNpYWwtcHJvZHVjdF9zcGVjaWFsX2lkPTg4",
    "id": "cHJvZHVjdFNwZWNpYWwtcHJvZHVjdF9zcGVjaWFsX2lkPTg4",
    "priority": "-1",
    "price": "1000.0000",
    "dateFrom": "0000-00-00 00:00:00",
    "dateTo": "0000-00-00 00:00:00",
    "minQuantity": "0",
    "maxQuantity": "0",
    "dateCreated": "2019-09-12T13:04:33",
    "type": "day_spec",
    "dayOfWeek": "4",
    "product": {
        "href": "http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTE2OQ=="
    },
    "customerGroup": null
}
```

## Nap terméke módosítása

Módosítás esetén a módosítandó mezők mellett kötelező elemként meg kell adni a product resource azonosítóját.
Amennyiben a vevőcsoportot szeretnénk módosítani "Mindenki" vevőcsoportra, úgy érdemes törölni előbb a nap termékét és egy újat létrehozni. Minden más vevőcsoport esetén a módosítás végrehajtható.
 
### Példa

#### Request

<table>
  <tr>
    <td><b>method:</b></td>
    <td>PUT</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/productSpecials/[ProductSpecialResourceID]</td>
  </tr>
  <tr>
    <td><b>headers:</b></td>
    <td>
        Accept:application/json<br>
        Content-Type:application/json
    </td>
  </tr>
</table>

```json
{
    "data": {
        "price": 900.0000,
        "dayOfWeek": 5,
        "product": {
            "id": "cHJvZHVjdC1wcm9kdWN0X2lkPTE2OQ"
        }
    }
}
```

#### Response

```json
{
    "href": "http://shopname.api.shoprenter.hu/productSpecials/cHJvZHVjdFNwZWNpYWwtcHJvZHVjdF9zcGVjaWFsX2lkPTg4",
    "id": "cHJvZHVjdFNwZWNpYWwtcHJvZHVjdF9zcGVjaWFsX2lkPTg4",
    "priority": "-1",
    "price": 900.0000,
    "dateFrom": "0000-00-00 00:00:00",
    "dateTo": "0000-00-00 00:00:00",
    "minQuantity": "0",
    "maxQuantity": "0",
    "dateCreated": "2019-09-12T13:04:33",
    "type": "day_spec",
    "dayOfWeek": 5,
    "product": {
        "href": "http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTE2OQ=="
    },
    "customerGroup": null
}
```
