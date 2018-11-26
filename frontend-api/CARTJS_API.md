## Cart.js API

A ShopRenter egyes kosár események bekövetkezésekor kiváltanak olyan javascript eseményeket, melyre feliratkozva, azok kiváltódása után, további viselkedést valósíthatunk meg.

Az új, hozzáadott eseményfigyelők (Event Listener) megkapják az eseményhez tartozó adatokat.

A rendszer az eseményt egy CustomEvent objektumba adja vissza, melynek a **detail** property-je tartalmazza a kosárral és termékekkel kapcsolatos adatokat.

### onItemAdd
Kosárba helyezés a bolt bármely részéről (modul termékkártya, termékoldal, kategóriaoldal). Megkapja a kosárba helyezett termék adatait.

Example:
```json
{
    "detail": {
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
    "detail": [
        {
            "product_id": "379",
            "isPresent": "",
            "cartKey": "S7QytqrOtDKwzrQyNrcEkoZAbATGiVaGVtXFVuZWSvkFJZn5ecVKQCEDq+ra2loA",
            "name": "Utcai cipő, Adidas Cireo Mid",
            "safeName": "Utcai cipő, Adidas Cireo Mid",
            "option": [],
            "quantity": "2",
            "quantity_name": "db",
            "image": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/product/adidas-ciero-mid-blue-pink-black.jpg?lastmod=-62169987600.1521455705",
            "stock": "1",
            "price": "19.685 Ft",
            "price_without_currency": "19685.00",
            "href": "https://demo.shoprenter.hu/utcai-cipo-adidas-cireo-mid-379",
            "values": [],
            "valueDisplay": "",
            "currency": "HUF",
        },
        {
            "product_id": "307",
            "isPresent": "",
            "cartKey": "S7QytqrOtDKwzrQyNjAHkoZQbGSdaGVoVV1sZW6llF9QkpmfV6wEFDKwqq6trQUA",
            "name": "Kensington ValuCase One",
            "safeName": "Kensington ValuCase One",
            "option": [],
            "quantity": "1",
            "quantity_name": "db",
            "image": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/product/UM07-05-0080n.jpg?lastmod=-62169987600.1521455705",
            "stock": "1",
            "price": "6.756 Ft",
            "price_without_currency": "6756.40",
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
```

### onItemDelete
A kosár modulból való termék törlése. Megkapja a kosárból törölt elem adatait.

Példa:
```json
{
    "detail": [
        {
            "product_id": "379",
            "isPresent": "",
            "cartKey": "S7QytqrOtDKwzrQyNrcEkoZAbATGiVaGVtXFVuZWSvkFJZn5ecVKQCEDq+ra2loA",
            "name": "Utcai cipő, Adidas Cireo Mid",
            "safeName": "Utcai cipő, Adidas Cireo Mid",
            "option": [],
            "quantity": "2",
            "quantity_name": "db",
            "image": "https://demo.shoprenter.hu/custom/demo/image/cache/w60h60/product/adidas-ciero-mid-blue-pink-black.jpg?lastmod=-62169987600.1521455705",
            "stock": "1",
            "price": "19.685 Ft",
            "price_without_currency": "19685.00",
            "href": "https://demo.shoprenter.hu/utcai-cipo-adidas-cireo-mid-379",
            "values": [],
            "valueDisplay": "",
            "currency": "HUF",
        }
    ]
}
```

## Használata:

A ShopRenter nevű objektum a frontend egész felületén elérhető, így bármely oldalon fel tudunk iratkozni a kosár eseményekre a következőképpen:


```html
<script type="application/javascript">
ShopRenter.onCartUpdate(function(event){
    console.log(event.detail)
});
</script>
```

Figyelni kell arra hogy az átadott javascript closure-nek legyen egy paramétere, melynek a neve tetszőleges lehet, pl.: event vagy e. Így az e.details property kikéréssel, hozzájutunk az esemény adataihoz.
