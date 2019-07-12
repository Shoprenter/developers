# Kiterjesztett Resourceok (Extend Resource)

A kiterjesztett resurceokkal könnyebb az adatcsere. Jelenleg két ilyen resourceunk van a **productExtend** és az **orderExtend**.
Ezeknek a resourceoknak a lényege, hogy a kapcsolódó adataikat is visszaadjuk a response-ban. 
Tehát például egy termék esetén nem kell külön kéréseket indítani, ha le akarjuk kérni a leírását, akcióit, vevőcsoportárait, stb.

Sőt ezeket módosíthatjuk is egy resourceon belül egyetlen kéréssel.
Viszont itt merőben más működése van a kérés típusoknak.

**POST** kérés esetén a kapcsolódó adatokat (Resource dokumentációban * Kapcsolódó Resource jelölés) mindig létrehozzuk.
Egy példán keresztül szemléltetve. Egy termék 2 kategóriában van. POST kéréssel küldünk 3 kategóriát, akkor azokat pluszban vesszük fel, tehát a termék már 5 kategóriában fog szerepelni. Ha valamelyik kategória kapcsolata már létezett, akkor nem fogjuk végrehajtani a POST kérést azzal a hibaüzenettel, hogy az adott kategória kapcsolat már létezik.

**PUT** kérés esetén a kapcsolódó adatokat (Resource dokumentációban * Kapcsolódó Resource jelölés) felülírjuk.
Egy hasonló példán bemutatva. Egy termék 2 kategóriában van. PUT kéréssel küldünk 3 kategóriát, akkor a meglévő 2 kategóriát felül fogjuk írni a küldött 3 kategóriával. Tehát a sikeres kérés után a termék csak abban a 3 kategóriában fog szerepelni, amelyik a kérésben szerepelt. Ekkor nincs hibaüzenet akkor sem, ha meglévő kategóriákat küldtünk. Egyszerűen a meglévőek le vannak cserélve a küldöttre.
Továbbá PUT kéréssel tudjuk azt megoldani, az előző példáknál maradva, ha azt szeretnénk elérni hogy egyetlen kategóriában sem szerepeljen a termék. Akkor a kategóriák helyett egy üres tömböt küldünk. Ekkor a meglévő kategóriáit lecseréljük üresre azaz nem lesznek kategóriái.

Az API fejlesztői dokumentációban a resource nevek mögötti **Extend** szó jelzi, mely resource-ok rendelkeznek ezzel a funkcionalitással.
Tehát a resource-oknak lényege, hogy a kapcsolódó adataikat is lekérdezhessük a közvetlenül response-ban. Így egy termék esetén nem kell külön kéréseket indítani, ha le akarjuk kérni a leírását, akcióit, vevőcsoportárait, stb.

Ezeket módosíthatjuk is egy resource-on belül egyetlen kéréssel, viszont itt merőben más működése van a kérés típusoknak attól függően, hogy a kapcsolt resource-ok milyen kapcsolatban állnak az aktuális resource-szal.

## OneToMany kapcsolat

Pl. egy termékhez több termékleírás tartozhat. Product Extend esetén a Product Descriptions

**POST kérés esetén** a kapcsolódó adatokat (Resource dokumentációban * Kapcsolódó Resource jelölés) mindig létrehozzuk.
Egy példán keresztül szemléltetve: Egy termék 2 kategóriában van. POST kéréssel küldünk 3 kategóriát, akkor azokat pluszban vesszük fel, tehát a termék már 5 kategóriában fog szerepelni. Ha valamelyik kategória kapcsolata már létezett, akkor nem fogjuk végrehajtani a POST kérést azzal a hibaüzenettel, hogy az adott kategória kapcsolat már létezik.

**PUT kérés esetén** a kapcsolódó adatokat (Resource dokumentációban * Kapcsolódó Resource jelölés) felülírjuk.
Egy hasonló példán bemutatva: Egy termék 2 kategóriában van. PUT kéréssel küldünk 3 kategóriát, akkor a meglévő 2 kategóriát felül fogjuk írni a küldött 3 kategóriával. Tehát a sikeres kérés után a termék csak abban a 3 kategóriában fog szerepelni, amelyik a kérésben szerepelt. Ekkor nincs hibaüzenet akkor sem, ha meglévő kategóriákat küldtünk. Egyszerűen a meglévőek le vannak cserélve a küldöttre.
Ha azt szeretnénk elérni, hogy egyetlen kategóriában sem szerepeljen a termék azt PUT kéréssel tudjuk megoldani. Ekkor a kategóriák helyett egy üres tömböt küldünk, tehát az adott termék meglévő kategóriáit lecseréljük üresre így nem lesznek kategóriái.

## OneToOne kapcsolat

Pl. egy termék egy gyártó alá tartozhat. Product Extend esetén a Manufacturer. (Egyenlőre ez az egyetlen ilyen kinyitott, OneToOne kapcsolat)

POST és PUT működése megegyezik egy ilyen tipusú, Extend resoruce-hoz tartozó mező esetén.

1. Ha a OneToOne mezőhöz tartozó, elküldött adattömb csak egy resource id-t tartalmaz, úgy a kapcsolt resource egyed létezése esetén, erre cseréljük ki az előző resource id-t.<br>
Pl.: Ha az Product Extend resoruce-ra POST-ot küldünk, melyben a **manufacturer**-el kapcsolatos adatokban csak egy resource id található, akkor a rendszer megpróbálja lecserélni az előző gyártót az újonnan elküldöttel.

2. Ha a OneToOne mezőhöz tartozó, elküldött adattömb csak mezőket és hozzá tartozó értékeket tartalmaz, de resouce id-t nem, úgy új kapcsolt resource egyedet hozunk létre, és ezt kötjük az eredeti Extend resourcehoz.<br>
Pl.: Ha az Product Extend resoruce-ra POST-ot küldünk, melyben a **manufacturer**-el kapcsolatos adatok találhatóak, de resource id nem, akkor a rendszer létrehozza az új gyártót, és a terméhez kapcsolja.

3. Ha a OneToOne mezőhöz tartozó, elküldött adattömb resource id-t, mezőket és hozzá tartozó értékeket tartalmaz, úgy a resource id-hoz tartozó, létező resource egyedet próbálja a rendszer frissíteni, egyébként létrehozza azt.
