# API Outer ID használata

Felmerült az igény, hogy egyes ügyfeleink saját egyedi azonosítókkal (OUTER_ID) szeretnék ellátni és használni a resource-okat, az általunk generáltakkal (API_ID) szemben, erre az alább ismertetett módon biztosítunk lehetőséget.

Az OuterID használatát csak batch kérés esetén javasoljuk, hogy a batch kérés ideéig lehetséges legyen hivatkozni egy adott resource-ra. Kliens oldali tárolását nem javasoljuk, mert egyrészt felülírható, így más integráció felülírhatja, másrészt az OuterID nem törlődik az adott resource törlése esetén. Ezért a kérések alkalmával félrevezető lehet hogy nem létező resource-ra érkezik módosítás, ami hibára fut vagy más resource-ra fog mutatni az OuterID mint amihez eredetileg fel lett véve. A fentiek miatt csak batch kérés esetén javasoljuk a használatát és az egyes batch kérések alkalmával egyedi OuterID használata javallott.

## Resource létrehozásakor

### POST

POST esetén, ha nem adunk meg ID-t, akkor a rendszer létrehoz egyet és ezt adja vissza válaszként. Ha megadunk ID-t, akkor azt a rendszer OUTER_ID-ként tárolja le és ezt rendeli a resourcehoz. A későbbiekkel erre az azonosítóra lehet hivatkozni GET, PUT, DELETE metódus során.

Például OUTER_ID használata nélkül egy termékhívás:

```
Array
(
    [sku] => SKU-11
    [modelNumber] => 0
    [orderable] => 1
    [price] => 139900.0000
    [multiplier] => 1.0000
    [multiplierLock] => 0
    [loyaltyPoints] => 
...
)
```

**Válasz:**

```
HTTP STATUS CODE: 200 vagy 201
```

```
<response>
    <href>
        <![CDATA[http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTI0NTE=]]>
    </href>
    <id>
        <![CDATA[cHJvZHVjdC1wcm9kdWN0X2lkPTI0NTE=]]>
    </id>
    <innerId>
        <![CDATA[1]]>
    </innerId>
    <sku>
        <![CDATA[SKU-11]]>
    </sku>
    ...
</response>
```

OUTER_ID használatával:

```
uri => http://shopname.api.shoprenter.hu/products/SKU-11
data => Array
(
    [sku] => SKU-11
    [modelNumber] => 0
    [orderable] => 1
    [price] => 139900.0000
    [multiplier] => 1.0000
    [multiplierLock] => 0
    [loyaltyPoints] => 
...
)
```

**Válasz:**

```
HTTP STATUS CODE: 200 vagy 201
```

```
<response>
    <href>
        <![CDATA[http://shopname.api.shoprenter.hu/products/SKU-11]]>
    </href>
    <innerId>
        <![CDATA[1]]>
    </innerId>
    <id>
        <![CDATA[SKU-11]]>
    </id>
    <sku>
        <![CDATA[SKU-11]]>
    </sku>
    ...
</response>
```

### PUT

PUT esetében kötelező megadni vagy API_ID-t vagy OUTER_ID-t az URI-ban. Ha ez az ID OUTER_ID, akkor megköveteli a rendszer, hogy már létezzen hozzá resource, egyéb tekintetben minden a POST-nál ismertetett módon zajlik. Ez azt jelenti, hogy PUT-tal és OUTER_id-val nem tudunk új resource-ot létrehozni, ellentétben az API_ID-val történő létrehozással szemben.

### GET

GET esetén hivatkozhatunk a kérés során az URI-ben OUTER_ID-ra, ha korábban már létrehoztuk a resourcet OUTER_ID-val ellátva.

### DELETE
 
Törlés esetén ha létezik a resource-hoz OUTER_ID, azt töröljük vele egyetemben.

## Létező resource esetén

Amennyiben már egy létező resource-ot szeretnénk ellátni OUTER_ID-val vagy éppen a meglévőt szeretnénk módosítani, ezentúl erre is biztosítunk lehetőséget. Minden resource tartalmaz egy id property-t, amely az OUTER_ID amennyiben létezik, ha nem akkor pedig az általunk generált API_ID, példa egy resource-ra:

```
<response>
    <href>
        <![CDATA[http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTk2]]>
    </href>
    <id>
        <![CDATA[cHJvZHVjdC1wcm9kdWN0X2lkPTk2]]>
    </id>
    <innerId>
        <![CDATA[96]]>
    </innerId>
    <sku>
        <![CDATA[BI-NAT004HU30]]>
    </sku>
    <price>
        <![CDATA[2759]]>
    </price>
    <stock1>
        <![CDATA[10]]>
    </stock1>
    <stock2>
        <![CDATA[20]]>
    </stock2>
    <stock3>
        <![CDATA[0]]>
    </stock3>
    <stock4>
        <![CDATA[0]]>
    </stock4>
    ...
</response>
```

### POST/PUT

POST és PUT kérés esetén egyszerűen a küldött adatokban szerepelni kell az id property-nek. Amennyiben az adott resourcehoz nem létezik OUTER_ID, akkor létrehozzuk azt. Ha pedig létezik, akkor felülírjuk.

Példa egy POST/PUT kérésre:

```
uri => http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTk2
data => Array
(
    [id] => TesztOuterID
    [price] => 2760
    [stock1] => 12
...
)
```

Ebben az esetben az id property-ként elküldtük a TesztOuterID-t. Így az adott resource megkapja az OUTER_ID-nak. Tehát az API válaszban már az id property az újonnan beálított OUTER_ID lesz. Továbbá az adott resource elérése is megváltozik.

```
<response>
    <href>
        <![CDATA[http://shopname.api.shoprenter.hu/products/TesztOuterID]]>
    </href>
    <id>
        <![CDATA[TesztOuterID]]>
    </id>
    <innerId>
        <![CDATA[96]]>
    </innerId>
    <sku>
        <![CDATA[BI-NAT004HU30]]>
    </sku>
    <price>
        <![CDATA[2760]]>
    </price>
    <stock1>
        <![CDATA[12]]>
    </stock1>
    ...
</response>
```

### GET

GET kérés esetén hivatkozhatunk az URI-ben OUTER_ID-ra:

```
/products/TesztOuterID
```

### DELETE

Törlés esetén ha létezik a resource-hoz OUTER_ID, azt töröljük vele egyetemben.
