## Shop.js

A bolt frontendjének minden oldalán lekérhető a bolt fontosabb adata,
melyet ShopRenter javascript objektum **theme** property-je tartalmazza. 

Példa:
```javascript
console.log(ShopRenter.theme.name);
```

### Egyes mezők jelentése:

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
                  Pl.: 1-et kell elosztanunk az adott pénznem árfolyamának értékével, például ha a valuta árfolyama 195 Ft, akkor az értékmező: 1/195, tehát 0,005128-at
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
