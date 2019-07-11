# APP és API - Gyakori kérdések app fejlesztőknek

#### Ha le akarom kérdezni egy resource adatait, akkor nekem kell a base64-es resource kódot legenerálnom?

Ez a legelső lépés, amit el szoktak rontani az API-ra történő fejlesztésnél. Ne generáld magadnak az azonosítókat! Miért? Időközben a resource azonosítás változhat az API-ban, esetleg teljesen átalakulhat a linkek generálása részünkről. URL visszafejtéssel sose foglalkozz. Bár így több lekérdezést kell elvégezned, de nem fogsz függeni a resource azonosításának funkcionalitásától.

---

#### Mi a helyes megoldás, ha mégis konkrét resource-ra szeretnék rákérdezni?

Ez helyzetfüggő, ha konkrétan tudod, mire akarsz rákérdezni az API-ból, akkor már legalább egy resource ID-d van. A termékeknél például van lehetőség **_sku_** szerint lekérdezni. Még egy lehetőség az Outer ID használata. Arról, hogy hogyan tudsz kereső paramétereket használni egy adott resource-nál vagy hogyan lehet létrehozni Outer ID-kat, a dokumentációban olvashatsz bővebben:

https://www.shoprenter.hu/api/doc#product
https://support.shoprenter.hu/hc/hu/articles/215106158-ShopRenter-API#outerid

---

#### Az Outer ID-t is base64 formában kellene létrehoznunk?

Nem, az Outer ID bármilyen string lehet. A lényeg, hogy ezt a ti oldalatokon letárolva, 
könnyen lekérdezhettek resource-okat, nem kell a base64-es resource azonosítókkal bajlódnotok.

---

#### Az app fejlesztésekor nekünk kell kérni a felhasználótól az API autentikációs adatokat?

Nem, ez teljesen automatikus. Mikor települ az appotok, az autentikációs URL-eken lévő kód
 fogja elkérni az aktuális ShopRenter bolthoz az API autentikációs adatokat. Itt le kell 
 mentenetek ezeket és ezt használva tudjátok elérni a bolt API-ját.

---

#### Mire szolgál a client secret és a client id, ha az API-nak van külön autentikációs adata?

A ShopRenter az appokkal való kommunikáció során Oauth szabványú hitelesítést használ.
Ez arra szolgál, hogy az ShopRenter tudja, hogy tőletek származnak a kérések,
 illetve hogy ti is megbizonyosodjatok, hogy az ShopRenter kérések valóban az ShopRentertől érkeznek.

---

#### Az ShopRenter adminon ugye az Integrációk menüpontban kellene látnom az appunkat. Miért nem látom?

Nem ott fog megjelenni. Az applikációk az Alkalmazások menüpont alatt találhatóak meg.

---

#### Új Vevő resource létrehozásánál milyen formátumú telefonszám az elfogadott?

https://github.com/googlei18n/libphonenumber package-et használjuk a 
telefonszámok kezelésére. Érdemes áttanulmányozni, illetve ezt használni a telefonszámok 
bevitelénél, így a formátum probléma elkerülhető.

---

#### Új Vevő resource létrehozásánál, a jelszavakat miképpen kezeli a ShopRenter?

A jelszavak kódolására bcryptet használunk, azaz nektek is így kell felvenni új Vevő (Customer) esetén.

---

#### Ha rendelésekkel dolgozok, és nyomon akarom követni az újonnan beérkezett rendeléseket, mindig le kell kérdeznem az API-n keresztül az összes rendelést?

Nem szükséges. Van lehetőség webhook-ot létrehozni például “Új rendelés feladás” eseményre, melynek megadható
egy endpoint. Az esemény kiváltása után az általatok megadott URL-re a rendszer elküldi az új rendelés adatait:

https://www.shoprenter.hu/api/doc#webhook

---

#### Mi a különbség az Extend resource-ok és a full kapcsoló között?
**Extend resource:** Egy konkrét resource egyed adatainak kapcsolódó adatainak a lekérdezését, illetve módosítását tudjuk egyetlen egy kéréssel végrehajtani. (Pl. így megkaphatjuk egy termék adatait, illetve a hozzátartozó leírásokat és nem csak egy link-et kapunk a termék leírását tartalmazó resource egyedre.)

**A full paraméter:** Egy resource egyed kollekció lekérdezésénél a normál resource-ok esetén a kapott listában csak a resource egyedekre mutató link-et látjuk. Ahhoz hogy elérjük a konkrét adatokat, egyedenként még egy kérést kell intéznünk a szerverhez. Hogy spórolni tudjunk a szükséges kérések számával, a `full=1` paraméterrel 1 lépésben kikérhetjük a kollekcióban az egyes resource egyedek adatait.

---

#### Nem látjuk az alkalmazásunkat az iframe-ben, mi lehet a gond?
'Refused to display' hibát kapunk a DevTools console-ban. A megjelenítést valószínűleg a 'X-Frame-Options' HTTP response header blokkolja, mivel ez jelzi a böngészőnek, hogy engedélyeznie kell-e az oldal megjelenítését.
(Bővebben erről: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)

---

#### A cUrl hívás nem működik Batch API-val a terminálban, mi a gond?
`-F` kapcsolóval küldöm a POST adatokat, de `40014 - 'POST is either empty or content length exceeds the limit of %s bytes'` hibát kapom.
Az `-F` kapcsoló eleve `multipart/form-data`-ként küldi el az adatot, így nem kell a 'content-type' header-t mellékelned.
(Bővebben erről: https://ec.haxx.se/http-postvspost.html)
