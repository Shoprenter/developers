## Theme.json

A bolt frontendjének minden oldalán lekérhető az aktuális sablon néhány adata,
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
        <td>A sablon neve</td>
    </tr>
    <tr>
        <td>family</td>
        <td>A sablon család neve, amelybe az aktuélis sablon tartozik</td>
    </tr>  
    <tr>
        <td>parent</td>
        <td>
           A szülő sablon neve 
        </td>
    </tr>
</table>
