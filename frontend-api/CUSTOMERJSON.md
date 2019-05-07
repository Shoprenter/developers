## Customer.json

A bolt frontendjének minden oldalán lekérhető az aktuális Vevő néhány adata,
melyet ShopRenter javascript objektum **customer** property-je tartalmazza. 
Az objektum szenzitív adatokat nem tartalmaz, amely alapján azonosítható lenne a Vevő.

Példa:
```javascript
console.log(ShopRenter.customer.user_id);
```

### Egyes mezők jelentése:

<table> 
    <tr>
        <th>property</th>
        <th>jelentés</th>
    </tr>
    <tr>
        <td>user_id</td>
        <td>A Vevő belső id-ja. Ha 0, akkor a Vevő nem regisztrált felhasználó</td>
    </tr>
    <tr>
        <td>user_group_id</td>
        <td>A vevő vásárlói csoportjának azonosítója</td>
    </tr>  
    <tr>
        <td>customer_group_tax_mode</td>
        <td>
           Megadja az aktuális Vevő vásárlói csoportja szerint, hogy a <strong>termékoldalon kívül</strong>, milyen módon jelenjen meg az ár
           <ul>
              <li><strong>gross</strong>: Bruttó ár</li>
              <li><strong>net</strong>: Nettó ár</li>
           </ul>
        </td>
    </tr> 
    <tr>
        <td>customer_group_price_mode</td>
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
