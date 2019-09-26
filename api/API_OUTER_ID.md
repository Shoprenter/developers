# API Outer ID használata

Felmerült az igény, hogy egyes ügyfeleink saját egyedi azonosítókkal (OUTER_ID) szeretnék ellátni és használni a resource-okat, az általunk generáltakkal (API_ID) szemben, erre az alább ismertetett módon biztosítunk lehetőséget.

Az Outer ID használatát **csak** olyan batch kérés esetén javasoljuk, amikor egy resource egyed létrehozása során további hozzá kapcsolódó resource egyedet kell létrehozni.
Outer ID nélkül a batchben a kérésekre a válaszok csak együtt fognak visszaérkezni a batch folyamat végén, ezért például egy termék (Product resource egyed) felvétele után, nem tudjuk, hogy a hozzá tartozó termék leírást (Product Description resource egyedet) milyen resource id-val vegyük fel.
Ellenben ha **Outer ID**-val hozzuk létre a terméket, akkor ezzel később tudunk hivatkozni a leírás létrehozásánál, függetlenül attól, hogy tudnánk, mi lesz a tényleges belső resource azonosítója a létrehozni kívánt terméknek.
Ez a megoldás még az egyszerűbb használatú [Resource Extend](EXTEND_RESOURCE.md) megjelenése előtt lesz használva, így amennyibe egy resource-nak van extendelt változata pl: [Product Extend](https://www.shoprenter.hu/api/doc#product_extend), úgy annak használatát javasoljuk az Outer ID-s batcheléssel szemben.

Ezenfelül, ha mégis az Outer ID-s megoldást választjuk, akkor a kliens oldali tárolását nem javasoljuk, mert egyrészt felülírható, így más integráció felülírhatja, másrészt az Outer ID nem törlődik az adott resource törlése esetén.

**A lenti példákat szemléltetésképp mutatjuk be, ezért nem tartalmazzák az egész API request-et és response-t!**

## Resource létrehozásakor

### POST

POST esetén, ha nem adunk meg ID-t, akkor a rendszer létrehoz egyet és ezt adja vissza válaszként. Ha megadunk ID-t, akkor azt a rendszer OUTER_ID-ként tárolja le és ezt rendeli a resourcehoz. A későbbiekkel erre az azonosítóra lehet hivatkozni GET, PUT, DELETE metódus során.

Például OUTER_ID használata nélkül egy termékhívás:

<table>
  <tr>
    <td><b>method:</b></td>
    <td>POST</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/products</td>
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
    "sku": "SKU-11",
    "modelNumber": 0,
    "orderable": 1,
    "price": 139900.0000,
    "multiplier": 1.0000,
    "multiplierLock": 0
  }
}
```

**Válasz:**

```
HTTP STATUS CODE: 200 vagy 201
```

```json
{
  "response": {
    "href": "http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTI0NTE=",
    "id": "cHJvZHVjdC1wcm9kdWN0X2lkPTI0NTE=",
    "innerId": "1",
    "sku": "SKU-11"
  }
}
```

OUTER_ID használatával:

<table>
  <tr>
    <td><b>method:</b></td>
    <td>POST</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/products/SKU-11</td>
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
    "sku": "SKU-11",
    "modelNumber": 0,
    "orderable": 1,
    "price": 139900.0000,
    "multiplier": 1.0000,
    "multiplierLock": 0
  }
}
```

**Válasz:**

```
HTTP STATUS CODE: 200 vagy 201
```

```json
{
  "response": {
    "href": "http://shopname.api.shoprenter.hu/products/SKU-11",
    "innerId": "1",
    "id": "SKU-11",
    "sku": "SKU-11"
  }
}
```

**Megjegyzés**: A példában életszerűen a cikkszámot (SKU) adtuk meg OUTER_ID-nak, viszont ez eltérhet.  

### PUT

PUT esetében kötelező megadni vagy API_ID-t vagy OUTER_ID-t az URI-ban. Ha ez az ID OUTER_ID, akkor megköveteli a rendszer, hogy már létezzen hozzá resource, egyéb tekintetben minden a POST-nál ismertetett módon zajlik. Ez azt jelenti, hogy PUT-tal és OUTER_id-val nem tudunk új resource-ot létrehozni, ellentétben az API_ID-val történő létrehozással szemben.

### GET

GET esetén hivatkozhatunk a kérés során az URI-ben OUTER_ID-ra, ha korábban már létrehoztuk a resourcet OUTER_ID-val ellátva.

### DELETE
 
Törlés esetén ha létezik a resource-hoz OUTER_ID, azt töröljük vele egyetemben.

## Létező resource esetén

Amennyiben már egy létező resource-ot szeretnénk ellátni OUTER_ID-val vagy éppen a meglévőt szeretnénk módosítani, ezentúl erre is biztosítunk lehetőséget. Minden resource tartalmaz egy id property-t, amely az OUTER_ID amennyiben létezik, ha nem akkor pedig az általunk generált API_ID, példa egy resource-ra:

```json
{
  "response": {
    "href": "http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTk2",
    "id": "cHJvZHVjdC1wcm9kdWN0X2lkPTk2",
    "innerId": "96",
    "sku": "BI-NAT004HU30",
    "price": "2759",
    "stock1": "10",
    "stock2": "20",
    "stock3": "0",
    "stock4": "0"
  }
}
```

### POST/PUT

POST és PUT kérés esetén egyszerűen a küldött adatokban szerepelni kell az id property-nek. Amennyiben az adott resourcehoz nem létezik OUTER_ID, akkor létrehozzuk azt. Ha pedig létezik, akkor felülírjuk.

Példa egy POST/PUT kérésre:

<table>
  <tr>
    <td><b>method:</b></td>
    <td>POST/PUT</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTk2</td>
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
    "id": "TesztOuterID",
    "price": 2760,
    "stock1": 12
  }
}
```

Ebben az esetben az id property-ként elküldtük a TesztOuterID-t. Így az adott resource megkapja az OUTER_ID-nak. Tehát az API válaszban már az id property az újonnan beálított OUTER_ID lesz. Továbbá az adott resource elérése is megváltozik.

```json
{
  "response": {
    "href": "http://shopname.api.shoprenter.hu/products/TesztOuterID",
    "id": "TesztOuterID",
    "innerId": "96",
    "sku": "BI-NAT004HU30",
    "price": "2760",
    "stock1": "12"
  }
}
```

### GET

GET kérés esetén hivatkozhatunk az URI-ben OUTER_ID-ra:

```
/products/TesztOuterID
```

### DELETE

Törlés esetén ha létezik a resource-hoz OUTER_ID, azt töröljük vele egyetemben.
