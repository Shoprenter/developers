# A full paraméter

A Resource-okból való lekérdezés során visszatérő feladat, hogy a visszakapott link-lista feldolgozásához további API hívást kell intézni, azért hogy visszakapjuk a Resource-hoz tartozó adatokat.

**A lenti példákat szemléltetésképp mutatjuk be, ezért nem tartalmazzák az egész API response-t!**

**Például:**

a terméklista lekérdezése során az alábbi eredménnyel találkozhatunk:

<table>
  <tr>
    <td><b>method:</b></td>
    <td>GET</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/products</td>
  </tr>
  <tr>
    <td><b>headers:</b></td>
    <td>Accept:application/json</td>
  </tr>
</table>

```json
{
  "response": {
    "items": {
      "item": [
        {
          "href": "http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTQ5"
        },
        {
          "href": "http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTUw"
        }
      ]
    }
  }
}
```

A kevesebb API hívások érdekében minden Resource GET-es hívás esetén rendelkezik egy **full** nevű paraméterrel. 
A `full=1` paraméter alkalmazásával a link-lista helyett a meghívott linkek tartalma jelenik meg.

<table>
  <tr>
    <td><b>method:</b></td>
    <td>GET</td>
  </tr>
  <tr>
    <td><b>url:</b></td>
    <td>http://shopname.api.shoprenter.hu/products?full=1</td>
  </tr>
  <tr>
    <td><b>headers:</b></td>
    <td>Accept:application/json</td>
  </tr>
</table>

```json
{
  "response": {
    "items": {
      "item": [
        {
          "href": "http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTQ5",
          "id": "cHJvZHVjdC1wcm9kdWN0X2lkPTQ5",
          "innerId": "49",
          "sku": "9789639884328"
        },
        {
          "href": "http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTQ5",
          "id": "cHJvZHVjdC1wcm9kdWN0X2lkPTQ5",
          "innerId": "49",
          "sku": "9789639884328"
        }
      ]
    }
  }
}
```

Használata gyorsabb és átláthatóbb kódot eredményez.
