## Order.js
Sikeres rendelés oldalon el lehet helyezni olyan scripteket, amelyek képesek az adott rendelés adatait elérni. 

A ShopRenter javascript objektum **lastOrder** property-je tartalmazza a rendeléshez tartozó adatokat, úgy mint az általános adatok (szállítási és fizetési mód, valuta stb.), illetve a megrendelt termékek adatait.

Az objektum szenzitív adatokat nem tartalmaz, amely alapján azonosítható lenne a Vevő.

Példa:
```javascript
console.log(ShopRenter.lastOrder);
```

### Egyes mezők jelentése:

<table> 
    <tr>
        <th>property</th>
        <th>jelentés</th>
    </tr>
    <tr>
        <td>id</td>
        <td>a rendelés azonosítója</td>
    </tr>
    <tr>
        <td>customerGroup</td>
        <td>a vevő csoport azonosítója</td>
    </tr>  
    <tr>
        <td>total</td>
        <td>Rendelés utáni teljes fizetendő összeg</td>
    </tr> 
    <tr>
        <td>orderStatusId</td>
        <td>A rendelés utáni állapot azonosítója</td>
    </tr>
    <tr>
        <td>currency</td>
        <td>A valuta, amellyel végbement a rendelés</td>
    </tr>
    <tr>
        <td>dateAdded</td>
        <td>A rendelés létrejöttének a dátuma</td>
    </tr>
    <tr>
        <td>shipping.methodName</td>
        <td>A szállítási mód a rendelés nyelvén megjelenített neve</td>
    </tr>
    <tr>
        <td>shipping.methodCode</td>
        <td>A szállítási mód szöveges azonosítója</td>
    </tr>
    <tr>
        <td>shipping.country</td>
        <td>Ország neve, a rendelés nyelvén</td>
    </tr>
    <tr>
        <td>shipping.countryId</td>
        <td>Az ország azonosítója</td>
    </tr>
    <tr>
        <td>shipping.vatRate</td>
        <td>A szállítási módhoz tartozó áfa mértéke</td>
    </tr>
    <tr>
        <td>shipping.expectedDelivery</td>
        <td>Várható szállítási idő timestamp-ben</td>
    </tr>
    <tr>
        <td>payment.methodName</td>
        <td>A fizetési mód a rendelés nyelvén megjelenített neve</td>
    </tr>
    <tr>
        <td>payment.methodCode</td>
        <td>A fizetési mód szöveges azonosítója</td>
    </tr>
    <tr>
        <td>payment.vatRate</td>
        <td>A fizetési módhoz tartozó áfa mértéke</td>
    </tr>
    <tr>
        <td>coupon.id</td>
        <td>A coupon azonosítója</td>
    </tr>
    <tr>
        <td>coupon.vatRate</td>
        <td>A kuponhoz tartozó áfa mértéke.</td>
    </tr>
    <tr>
        <td>products</td>
        <td>Tartalmazza a rendelésben szereplő termékeket</td>
    </tr>
    <tr>
        <td>products.id</td>
        <td>A termék azonosítója</td>
    </tr>
    <tr>
        <td>products.title</td>
        <td>A termék neve</td>
    </tr>
    <tr>
        <td>products.unitPrice</td>
        <td>A termék egységára</td>
    </tr>
    <tr>
        <td>products.totalPrice</td>
        <td>A termék teljes ára (mennyiség * egységár)</td>
    </tr>
    <tr>
        <td>products.vatRate</td>
        <td>A termékhez tartozó áfa mértéke</td>
    </tr>
    <tr>
        <td>products.quantity</td>
        <td>Mennyiség</td>
    </tr>
    <tr>
        <td>products.sku</td>
        <td>A termék cikkszáma</td>
    </tr>
    <tr>
        <td>products.giftWrapping</td>
        <td>Az egyes termékekre, a Vevő által kért ajándékcsomagolás adatai. Ha az adott termékre nem kér csomagolást, úgy üres tömb lesz ezen a property-n</td>
    </tr>
    <tr>
        <td>products.giftWrapping.id</td>
        <td>A csomagolás belső azonosítója</td>
    </tr>
    <tr>
        <td>products.giftWrapping.sku</td>
        <td>A csomagolás cikkszáma</td>
    </tr>
    <tr>
        <td>products.giftWrapping.price</td>
        <td>A csomagolás nettó ára</td>
    </tr>
    <tr>
        <td>products.giftWrapping.vat</td>
        <td>A csomagolás ÁFÁ-ja</td>
    </tr>
    <tr>
        <td>products.giftWrapping.name</td>
        <td>A csomagolás neve</td>
    </tr>
    <tr>
        <td>products.giftWrapping.quantityName</td>
        <td>A csomagolás mértékegységének a neve, pl.: doboz</td>
    </tr>
    <tr>
        <td>giftWrapping</td>
        <td>A kosár ajándék csomagolása. Ugyan olyan a felépítése, mint amikor egyesével csomagolnánk be a termékeket. Ha a teljes kosárra nem kér a Vevő csomaglást, úgy üres tömb lesz ezen a property-n</td>
    </tr>
    <tr>
        <td>loyaltyPoints</td>
        <td>A rendelésben felhasznált hűségpont adatai. Ha nincs engedélyve a hűségpont rendszer, vagy az adott rendeléshez nem használtak hűségpontot, úgy üres tömb van ezen property-n</td>
    </tr>
    <tr>
        <td>loyaltyPoints.usedPoints</td>
        <td>A rendelésben felhasznált pontok darabszáma</td>
    </tr>
    <tr>
        <td>loyaltyPoints.valueOfOnePoint</td>
        <td>Egy pont értéke HUF-ban</td>
    </tr>
    <tr>
        <td>loyaltyPoints.vatRate</td>
        <td>ÁFA értéke. Csak a számlázó programba való átadást érinti, a hűségpont értékét nem módosítja.</td>
    </tr>
    <tr>
        <td>loyaltyPoints.totalValue</td>
        <td>A teljes összeg, amit a Vevő hűségponttal fedezett a rendelés során. Ez a rendelésnek megfelelő valutába átváltva jelenik meg. (<strong>currency</strong> property)</td>
    </tr>
</table>
