# Tartalomjegyzék
* [ShopRenter Object](#shoprenter-object)
  * [Properties](#properties)
    * [customer](#customer)
    * [theme](#theme)
    * [shop](#shop)
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
console.log(ShopRenter.customer.userId);
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
console.log(ShopRenter.theme.name);
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
console.log(ShopRenter.shop.name);
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
A kosár módosítása (termék hozzáadás, darabszám). Megkapja a kosárba helyezett termék adatait.

Példa:
```json
{
    "detail": {
        "cartToken": "27828acb2141b0b16bbfc14358b0cbcd1d26aee0860c5",
        "products": [
            {
                "productId": "379",
                "isPresent": "",
                "cartKey": "S7QytqrOtDKwzrQyNrcEkoZAbATGiVaGVtXFVuZWSvkFJZn5ecVKQCEDq+ra2loA",
                "name": "Utcai cipő, Adidas Cireo Mid",
                "safeName": "Utcai cipő, Adidas Cireo Mid",
                "option": [],
                "quantity": "2",
                "quantityName": "db",
                "image": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/product/adidas-ciero-mid-blue-pink-black.jpg?lastmod=-62169987600.1521455705",
                "stock": "1",
                "price": "19.685 Ft",
                "priceWithoutCurrency": "19685.00",
                "href": "https://demo.shoprenter.hu/utcai-cipo-adidas-cireo-mid-379",
                "values": [],
                "valueDisplay": "",
                "currency": "HUF",
            },
            {
                "productId": "307",
                "isPresent": "",
                "cartKey": "S7QytqrOtDKwzrQyNjAHkoZQbGSdaGVoVV1sZW6llF9QkpmfV6wEFDKwqq6trQUA",
                "name": "Kensington ValuCase One",
                "safeName": "Kensington ValuCase One",
                "option": [],
                "quantity": "1",
                "quantityName": "db",
                "image": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/product/UM07-05-0080n.jpg?lastmod=-62169987600.1521455705",
                "stock": "1",
                "price": "6.756 Ft",
                "priceWithoutCurrency": "6756.40",
                "href": "https://demo.shoprenter.hu/kensington-valucase-one-307",
                "values": {
                    "2": {
                        "attrId": "2",
                        "attrLabel": "Szín",
                        "postfix": "",
                        "prefix": "",
                        "rawValue": "4",
                        "value": "Piros",
                        "values": ["4"],
                        "priority": "2",
                        "valueDisplay": "<div>Piros</div>",
                        "valueTextDisplay": "Piros",
                        "valueIds": ["1","4","5","6","7","8","9"],
                    },
                    "3": {
                        "attrId": "3",
                        "attrLabel": "Méret",
                        "postfix": "",
                        "prefix": "",
                        "rawValue": "1",
                        "value": "M",
                        "values": ["1"],
                        "priority": "0",
                        "valueDisplay": "M",
                        "valueTextDisplay": "M",
                        "valueIds":[],
                    }
                },
                "valueDisplay": " <span class=\"paf_attrib_values\"><span class=\"paf_attrib\"><span class=\"paf_attrib_label\">Szín:</span> <span class=\"paf_attrib_value\">Piros</span></span><br/><span class=\"paf_attrib\"><span class=\"paf_attrib_label\">Méret:</span> <span class=\"paf_attrib_value\">M</span></span></span>",
                "currency": "HUF",
            }
        ]
    }
}
```

### onItemDelete
A kosár modulból való termék törlése. Megkapja a kosárból törölt elem adatait.

Példa:
```json
{
    "detail": {
        "cartToken": "27828acb2141b0b16bbfc14358b0cbcd1d26aee0860c5",
        "products": [
            {
                "productId": "379",
                "isPresent": "",
                "cartKey": "S7QytqrOtDKwzrQyNrcEkoZAbATGiVaGVtXFVuZWSvkFJZn5ecVKQCEDq+ra2loA",
                "name": "Utcai cipő, Adidas Cireo Mid",
                "safeName": "Utcai cipő, Adidas Cireo Mid",
                "option": [],
                "quantity": "2",
                "quantityName": "db",
                "image": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/product/adidas-ciero-mid-blue-pink-black.jpg?lastmod=-62169987600.1521455705",
                "stock": "1",
                "price": "19.685 Ft",
                "priceWithoutCurrency": "19685.00",
                "href": "https://demo.shoprenter.hu/utcai-cipo-adidas-cireo-mid-379",
                "values": [],
                "valueDisplay": "",
                "currency": "HUF",
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
