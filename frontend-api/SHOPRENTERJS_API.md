# Tartalomjegyzék
* [ShopRenter Object](#shoprenter-object)
  * [Properties](#properties)
    * [customer](#customer)
    * [theme](#theme)
    * [shop](#shop)
    * [page](#page)
    * [product](#product)
  * [Events](#events)
    * [onItemAdd](#onitemadd)
    * [onCartUpdate](#oncartupdate)
    * [onItemDelete](#onitemdelete)
    * [Események használata](#esem%C3%A9nyek-haszn%C3%A1lata)

# ShopRenter Object
A frontendre beépülő alkalmazásoknál szükség lehet olyan adatokra, melyek elengedhetetlenek az alkalmazás üzleti logikájához.
A ShopRenter globális JavaScript objektum frontenden elérhető minden oldalbetöltődésnél, amely webshop adatokat tároló objektumokat és eseményfigyelőket tartalmaz.

## Properties

### customer
A bolt frontendjének minden oldalán lekérhető az aktuális Vevő néhány adata,
melyet ShopRenter javascript objektum **customer** property-je tartalmazza. 
Az objektum szenzitív adatokat nem tartalmaz, amely alapján azonosítható lenne a Vevő.

Példa:
```javascript
console.log(ShopRenter.customer);
```

Kimenet:
```javascript
{
    userId: 0, 
    userGroupId: 8, 
    customerGroupTaxMode: "gross", 
    customerGroupPriceMode: "gross_net_tax"
}
```

Egyes mezők jelentése:
<table> 
    <tr>
        <th>property</th>
        <th>jelentés</th>
    </tr>
    <tr>
        <td>userId</td>
        <td>A Vevő belső id-ja. Ha 0, akkor a Vevő nem regisztrált felhasználó</td>
    </tr>
    <tr>
        <td>userGroupId</td>
        <td>A vevő vásárlói csoportjának azonosítója</td>
    </tr>  
    <tr>
        <td>customerGroupTaxMode</td>
        <td>
           Megadja az aktuális Vevő vásárlói csoportja szerint, hogy a <strong>termékoldalon kívül</strong>, milyen módon jelenjen meg az ár
           <ul>
              <li><strong>gross</strong>: Bruttó ár</li>
              <li><strong>net</strong>: Nettó ár</li>
           </ul>
        </td>
    </tr> 
    <tr>
        <td>customerGroupPriceMode</td>
        <td>
           Megadja az aktuális Vevő vásárlói csoportja szerint, hogy a <strong>termékoldalon</strong>, milyen módon jelenjen meg az ár
              <li><strong>only_gross</strong>: Csak a bruttó ár kiírása</li>
              <li><strong>gross_net_tax</strong>: Bruttó ár, mögötte zárójelben a nettó + ÁFA kiírása</li>
              <li><strong>only_net</strong>: Csak a nettó ár kiírása</li>
              <li><strong>net_tax</strong>: A nettó ár és mögötte a + ÁFA kiírása/li>
              <li><strong>net_tax_gross</strong>: A nettó ár és mögötte a + ÁFA kiírása, illetve zárójelben a bruttó ár kiírása</li>
        </td>
    </tr>
</table>

### theme
A bolt frontendjének minden oldalán lekérhető az aktuális sablon néhány adata,
melyet ShopRenter javascript objektum **theme** property-je tartalmazza. 

Példa:
```javascript
console.log(ShopRenter.theme);
```

Kimenet:
```javascript
{
    name: "tokyo_glacierblue", 
    family: "tokyo", 
    parent: "bootstrap"
}
```

Egyes mezők jelentése:
<table> 
    <tr>
        <th>property</th>
        <th>jelentés</th>
    </tr>
    <tr>
        <td>name</td>
        <td>A sablon neve</td>
    </tr>
    <tr>
        <td>family</td>
        <td>A sablon család neve, amelybe az aktuális sablon tartozik</td>
    </tr>  
    <tr>
        <td>parent</td>
        <td>
           A szülő sablon neve 
        </td>
    </tr>
</table>

### shop
A bolt frontendjének minden oldalán lekérhető a bolt fontosabb adata,
melyet ShopRenter javascript objektum **theme** property-je tartalmazza. 

Példa:
```javascript
console.log(ShopRenter.shop);
```

Kimenet:
```javascript
{
    name: "tokyo", 
    locale: "hu", 
    currency: {
        code: "HUF", 
        rate: 1
    }, 
    domain: "tokyo.shoprenter.hu"
}
```

Egyes mezők jelentése:
<table> 
    <tr>
        <th>property</th>
        <th>jelentés</th>
    </tr>
    <tr>
        <td>name</td>
        <td>A bolt neve</td>
    </tr>
    <tr>
        <td>locale</td>
        <td>A bolt aktuális frontend nyelve</td>
    </tr>  
    <tr>
        <td>currency</td>
        <td>
           A bolt aktuális valutájára vonatkozó adatok:
           <ul>
              <li><strong>code</strong>: A valuta nyelvi kódja</li>
              <li><strong>rate</strong>: A bolt alapértelmezett valutájához mérten használt pénznem váltó érték.
                  Pl.: 1-et kell elosztanunk az adott pénznem árfolyamának értékével, például ha a valuta árfolyama 195 Ft, akkor az értékmező: 1/195, tehát 0,005128 lesz a rate
              </li>
           </ul>
        </td>
    </tr>
    <tr>
        <td>domain</td>
        <td>
           A bolt rendszer domain-ja
        </td>
    </tr>
</table>

### page
A ShopRenter objektum **page** property tartalmazza az aktuális oldal adatait.

Példa:
```javascript
console.log(ShopRenter.page);
```

Kimenet:
```javascript
{
    route: "product/list"
}
```

Egyes mezők jelentése:
<table> 
    <tr>
        <th>property</th>
        <th>jelentés</th>
    </tr>
    <tr>
        <td>route</td>
        <td>Az adott aloldal route értéke</td>
    </tr>
</table>

### product
A ShopRenter objektum **product** property tartalmazza a termékhez tartozó információkat. Ez a property csak termékoldalon érhető el!

Példa:
```javascript
console.log(ShopRenter.product);
```

Kimenet:
```javascript
{
    id: "201",
    sku: "ASDF201",
    parent: {
        id: "200",
        sku: "ASDF200"
    }
}
```

Egyes mezők jelentése:
<table> 
    <tr>
        <th>property</th>
        <th>jelentés</th>
    </tr>
    <tr>
        <td>id</td>
        <td>Az aktuális termék azonosítója</td>
    </tr>
    <tr>
        <td>sku</td>
        <td>Az aktuális termék cikkszáma</td>
    </tr>
    <tr>
        <td>parent.id</td>
        <td>Az szülő termék azonosítója</td>
    </tr>
    <tr>
        <td>parent.sku</td>
        <td>Az szülő termék cikkszáma</td>
    </tr>
</table>

## Events
A ShopRenter egyes kosár események bekövetkezésekor kiváltanak olyan javascript eseményeket, melyre feliratkozva, azok kiváltódása után, további viselkedést valósíthatunk meg.

Az új, hozzáadott eseményfigyelők (Event Listener) megkapják az eseményhez tartozó adatokat.

A rendszer az eseményt egy CustomEvent objektumba adja vissza, melynek a **detail** property-je tartalmazza a kosárral és termékekkel kapcsolatos adatokat.

### onItemAdd
Kosárba helyezés a bolt bármely részéről (modul termékkártya, termékoldal, kategóriaoldal). Megkapja a kosárba helyezett termék adatait.

Példa:
```json
{
    "detail": {
        "cartToken": "27828acb2141b0b16bbfc14358b0cbcd1d26aee0860c5",
        "product": {
            "id": "[367]",
            "sku": 9950000044,
            "price": "18415.00",
            "currency": "HUF",
            "quantity": "1",
            "name": "Sztreccs farmer"
        }
    }
}
```

### onCartUpdate
A kosár módosításakor (termék hozzáadásakor/törlésekor/módosításakor) végbemenő eseményre lehet feliratkozni. A feliratkozott eventlistener paraméterben megkapja a módosított kosár adatait.

Példa:
```json
{
    "detail": {
                "cartToken": "27828acb2141b0b16bbfc14358b0cbcd1d26aee0860c5",
                "products": [
                  {
                    "0": "",
                    "productId": 318,
                    "sku": "TTA1234",
                    "minimumPlural": "0",
                    "isPresent": false,
                    "shippingTime": 1565965848,
                    "isParentOrChild": false,
                    "image": "",
                    "cartKey": "S7QytqrOtDKwzrQyNrQAkoYgbAQkjKwTrQytqoutzK2U8gtKMvPzipWAQgZW1bW1tQA=",
                    "download": [],
                    "cartItemType": "Product",
                    "name": "Teszt termék akcióhoz",
                    "thumbWidth": "60",
                    "thumbHeight": "60",
                    "imageUrl": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/no_image.jpg?lastmod=0.1560858478",
                    "option": [],
                    "quantity": 12,
                    "quantityName": "db",
                    "minimum": "1",
                    "maximum": "0",
                    "summedQuantity": 48,
                    "step": 1,
                    "stock": true,
                    "priceNumber": 10000,
                    "totalNumber": 120000,
                    "totalOriginalNumber": 120000,
                    "originalPriceNumber": 10000,
                    "isSpecial": false,
                    "href": "https://demo.shoprenter.hu/teszt_termek_akciohoz_318",
                    "values": [],
                    "displaySpecialPrice": false,
                    "isModified": false,
                    "customerMessage": null,
                    "needToShip": true,
                    "weight": 0,
                    "weightClass": "kg",
                    "isMaximumQuantityReached": false
                  },
                  {
                    "0": "",
                    "productId": 317,
                    "sku": "TESZTOPC1234",
                    "minimumPlural": "0",
                    "isPresent": false,
                    "shippingTime": 1565965848,
                    "isParentOrChild": false,
                    "image": "",
                    "cartKey": "S7QytqrOtDKwzrQyNjQHkoZQbGSdaGVoVV1sZW6llF9QkpmfV6wEFDKwqq6trQUA",
                    "download": [],
                    "cartItemType": "Product",
                    "name": "Teszt opciós termék",
                    "thumbWidth": "60",
                    "thumbHeight": "60",
                    "imageUrl": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/no_image.jpg?lastmod=0.1560858478",
                    "option": [],
                    "quantity": 1,
                    "quantityName": "db",
                    "minimum": "1",
                    "maximum": "0",
                    "summedQuantity": 1228,
                    "step": 1,
                    "stock": true,
                    "priceNumber": 10000,
                    "totalNumber": 10000,
                    "totalOriginalNumber": 10000,
                    "originalPriceNumber": 10000,
                    "isSpecial": false,
                    "href": "https://demo.shoprenter.hu/teszt_opcios_termek_317",
                    "values": [],
                    "displaySpecialPrice": false,
                    "isModified": false,
                    "customerMessage": null,
                    "needToShip": true,
                    "weight": 0,
                    "weightClass": "kg",
                    "isMaximumQuantityReached": false
                  }
                ]
              }
}
```

### onItemDelete
A kosárból való törlés eseményre lehet feliratkozni. A feliratkozott eventlistener paraméterben megkapja a törlés utáni kosár adatait.

Példa:
```json
{
    "detail": {
                "cartToken": "27828acb2141b0b16bbfc14358b0cbcd1d26aee0860c5",
                "products": [
                  {
                    "0": "",
                    "productId": 318,
                    "sku": "TTA1234",
                    "minimumPlural": "0",
                    "isPresent": false,
                    "shippingTime": 1565965848,
                    "isParentOrChild": false,
                    "image": "",
                    "cartKey": "S7QytqrOtDKwzrQyNrQAkoYgbAQkjKwTrQytqoutzK2U8gtKMvPzipWAQgZW1bW1tQA=",
                    "download": [],
                    "cartItemType": "Product",
                    "name": "Teszt termék akcióhoz",
                    "thumbWidth": "60",
                    "thumbHeight": "60",
                    "imageUrl": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/no_image.jpg?lastmod=0.1560858478",
                    "option": [],
                    "quantity": 12,
                    "quantityName": "db",
                    "minimum": "1",
                    "maximum": "0",
                    "summedQuantity": 48,
                    "step": 1,
                    "stock": true,
                    "priceNumber": 10000,
                    "totalNumber": 120000,
                    "totalOriginalNumber": 120000,
                    "originalPriceNumber": 10000,
                    "isSpecial": false,
                    "href": "https://demo.shoprenter.hu/teszt_termek_akciohoz_318",
                    "values": [],
                    "displaySpecialPrice": false,
                    "isModified": false,
                    "customerMessage": null,
                    "needToShip": true,
                    "weight": 0,
                    "weightClass": "kg",
                    "isMaximumQuantityReached": false
                  },
                  {
                    "0": "",
                    "productId": 317,
                    "sku": "TESZTOPC1234",
                    "minimumPlural": "0",
                    "isPresent": false,
                    "shippingTime": 1565965848,
                    "isParentOrChild": false,
                    "image": "",
                    "cartKey": "S7QytqrOtDKwzrQyNjQHkoZQbGSdaGVoVV1sZW6llF9QkpmfV6wEFDKwqq6trQUA",
                    "download": [],
                    "cartItemType": "Product",
                    "name": "Teszt opciós termék",
                    "thumbWidth": "60",
                    "thumbHeight": "60",
                    "imageUrl": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/no_image.jpg?lastmod=0.1560858478",
                    "option": [],
                    "quantity": 1,
                    "quantityName": "db",
                    "minimum": "1",
                    "maximum": "0",
                    "summedQuantity": 1228,
                    "step": 1,
                    "stock": true,
                    "priceNumber": 10000,
                    "totalNumber": 10000,
                    "totalOriginalNumber": 10000,
                    "originalPriceNumber": 10000,
                    "isSpecial": false,
                    "href": "https://demo.shoprenter.hu/teszt_opcios_termek_317",
                    "values": [],
                    "displaySpecialPrice": false,
                    "isModified": false,
                    "customerMessage": null,
                    "needToShip": true,
                    "weight": 0,
                    "weightClass": "kg",
                    "isMaximumQuantityReached": false
                  }
                ]
              }
}
```

Figyelni kell arra, hogy az átadott javascript closure-nek legyen egy paramétere, melynek a neve tetszőleges lehet, pl. event vagy e. Így az e.details property kikéréssel, hozzájutunk az esemény adataihoz.

### Események használata
A ShopRenter nevű objektum a frontend egész felületén elérhető, így bármely oldalon fel tudunk iratkozni a kosár eseményekre a következőképpen:

```html
<script type="application/javascript">
ShopRenter.onCartUpdate(function(event) {
    console.log(event.detail)
});
</script>
```
