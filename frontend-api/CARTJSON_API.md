## Cart.json API

### GET /cart.json

Ezt az endpointot lehet használni, ha szeretnénk kikérni a kosár tartalmát JavaScripttel.

A válasz JSON formátumban kerül átadásra.

Példa:
```json
{
    "subTotal": 1950,
    "subTotalWithTax": 2476.5,
    "total": 2476.5,
    "taxTotal": 526.5,
    "itemCount": 1,
    "items": {
        "409": {
            "id": 409,
            "name": "Potted Double Stem Kaleidoscope Orchid",
            "quantity": 1,
            "image": "product/00011.jpg",
            "href": "https://demo.shoprenter.hu/potted-double-stem-kaleidoscope-orchid-409",
            "price": 2476.5,
            "total": 2476.5,
            "totalOriginal": 2476.5,
            "priceOriginal": 2476.5,
            "special": false,
            "present": false,
            "requiresShipping": true,
            "option": [
              
            ],
            "values": [
              
            ]
        }
    }
}
```

Példa üres kosárra:
```json
{
    "subTotal": 0,
    "subTotalWithTax": 0,
    "total": 0,
    "taxTotal": 0,
    "itemCount": 0,
    "items": []
}
```

Példakód a használatra:
```javascript
$.ajax({
    type: 'GET',
    url: 'https://demo.shoprenter.hu/frontend/cart',
    success: function(res) {
        console.log(res);
    },
    error: function (request, status, error) {
        alert(request.responseText);
    }
});
```
### GET /cart/reload/{token}

Ez az endpoint a kosár visszatöltésére szolgál.
A token helyére a cart tokent kell megadni.
Ha helyes tokent adtunk meg, akkor visszakapjuk az adott tokenhez tartozó kosár tartalmat, majd átirányít minket a kosár oldalra.
Ha rossz tokent adunk át, akkor nem változik a kosár tartalma, de szintén átirányít a kosár oldalra.
