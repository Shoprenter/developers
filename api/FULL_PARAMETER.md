# A full paraméter

A Resourceokból való lekérdezés során visszatérő feladat, hogy a visszakapott linklista feldolgozásához további API hívást kell intézni, azért hogy visszakapjuk a Resource-hoz tartozó adatokat.

**Például:**

a terméklista lekérdezése során az alábbi eredménnyel találkozhatunk:

- **method:** GET
- **url:** http://shopname.api.shoprenter.hu/products

```
<response>
...
<items>
    <item>
        <href>
            <![CDATA[http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTQ5]]>
        </href>
    </item>
    <item>
        <href>
            <![CDATA[http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTUw]]>
        </href>
    </item>
</items>
...
</response>
```

A kevesebb API hívások érdekében minden Resource GET-es hívás esetén rendelkezik egy **full** nevű paraméterrel. 
A `full=1` paraméter alkalmazásával a link lista helyett a meghívott linkek tartalma jelenik meg.

- **method:** GET
- **url:** http://shopname.api.shoprenter.hu/products?full=1

```
<response>
...
<items>
    <item>
        <href>
            <![CDATA[http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTQ5]]>
        </href>
        <id>
            <![CDATA[cHJvZHVjdC1wcm9kdWN0X2lkPTQ5]]>
        </id>
        <innerId>
            <![CDATA[49]]>
        </innerId>
        <sku>
            <![CDATA[9789639884328]]>
        </sku>
        ...
    </item>
    <item>
        <href>
            <![CDATA[http://shopname.api.shoprenter.hu/products/cHJvZHVjdC1wcm9kdWN0X2lkPTQ5]]>
        </href>
        <id>
            <![CDATA[cHJvZHVjdC1wcm9kdWN0X2lkPTQ5]]>
        </id>
        <innerId>
            <![CDATA[49]]>
        </innerId>
        <sku>
            <![CDATA[9789639884328]]>
        </sku>
        ...
   </item>
</items>
...
</response>
```

Használata gyorsabb és átláthatóbb kódot eredményez.
