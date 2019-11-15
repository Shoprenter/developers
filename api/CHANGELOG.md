# API changelog

#### 2019.10.24.
- Elérhető vált a **Payment Mode Resource** API végpont, amellyel kikérhetjük az aktuális bolt **telepített** fizetési módjait. Mivel a rendszer nem támogatja a saját fizetési módok létrehozását, így ez a resource teljesen readOnly. [dokumentáció](https://www.shoprenter.hu/api/doc#payment_mode)

#### 2019.10.21.
- A **ProductExtend** resource-ba bekerült egy új property, a "**productAttributeExtend**" nevű lista, ami tartalmazza a termékhez tartozó tulajdonságokat. Fontos megjegyezni, hogy ez jelenleg csak readonly, tehát nem lehet küldeni rá POST adatokat. [dokumentáció](https://www.shoprenter.hu/api/doc#product_extend)

#### 2019.10.17.
- Setting resource kiegészült a bolt üzemeltetőjének címével (**config_address**) és telefonszámával (**config_telephone**). [dokumentáció](SETTING_RESOURCE.md)

#### 2019.10.14
- Elérhetővé vált a szöveges tartalmak menedzseléséhez szükséges API végpont Information Extend néven. [dokumentáció](https://www.shoprenter.hu/api/doc#information_extend)

#### 2019.09.23
- Sok problémát okozott ügyfeleinknek az egyes fő resoruce-ok (Product, Order, Category stb.) törlése esetén, hogy bár a rájuk küldött DELETE kérések esetén, a hozzájuk tartozó OuterID megfelelelően törlődött. Viszont, ha volt kapcsolódó resource-a, pl. egy termék esetén a termék leírások, így ehhez is tartozott külön OuterID, ez sajnos nem törlődött automatikusan. Ezt oldottuk meg, így most már nem kell tartani attól, hogy később név ütközésbe futnak bele a fejlesztők, OuterID felvételekor.

#### 2019.09.10
- Bekerült a Shipping Mode Extend resource, amellyel a szállítási módokkal kapcsolatos műveleteket lehet végrehajtani. [dokumentáció](https://www.shoprenter.hu/api/doc#shipping_mode_extend)
- Bekerült a Shipping Mode Description resource, amellyel a szállítási módokkal kapcsolatos adatokat (név, leírás, nyelv) lehet kezelni. [dokumentáció](https://www.shoprenter.hu/api/doc#shipping_mode_description)
- Bekerült a Shipping Lane resource, amellyel a szállítási módokkal kapcsolatos szállítási sávokat lehet kezelni. [dokumentáció](https://www.shoprenter.hu/api/doc#shipping_lane)
- Order resource kiegészült egy shippingMode kereső paraméterrel és egy shippingMode propertyvel. [dokumentáció](https://www.shoprenter.hu/api/doc#order)
- Order Extend resource kiegészült egy shippingMode kereső paraméterrel és egy shippingMode propertyvel. [dokumentáció](https://www.shoprenter.hu/api/doc#order_extend)

#### 2019.09.03
- Bekerült a GeoZone resource, amellyel le lehet kérdezni, hogy milyen földrajzi zónához milyen országok tartoznak. [dokumentáció](https://www.shoprenter.hu/api/doc#geo_zone)
- A Country resource kiegészült a geoZones propertyvel, amellyel megkaphatjuk, hogy egy adott ország milyen földrajzi zónákhoz tartozik. [dokumentáció](https://www.shoprenter.hu/api/doc#country)
- Az OrderProduct resource kiegészült további propertykkel, amellyel megkaphatjuk a rendelt termék szélességét (**width**), magasságát (**height**), hosszát (**length**) és súlyát (**weight**). [dokumentáció](https://www.shoprenter.hu/api/doc#order_product)
- A ProductImage resource kiegészült egy sortOrder propertyvel, amellyel meg lehet adni a termékképek sorrendjét. [dokumentáció](https://www.shoprenter.hu/api/doc#product_image)
- Elérhetővé vált a Domain Resource. Ezzel kikérhető az adott bolthoz felvett domainek adatai: a domain-ek nyelve és hogy elsődleges domain-ek vagy sem. [dokumentáció](https://www.shoprenter.hu/api/doc#domain)

#### 2019.08.08
- Bekerült a **Json-alapú** kommunikáció az API-val. Emellett az API dokumentáció ki lett bővítve **Json** formátumú példákkal. [dokumentáció](https://www.shoprenter.hu/api/doc#address)

#### 2019.08.06
- A Product és Product Extend resource-ban elérhető lett az **allImages** property, mely az adott terméhez tartozó fő termékkép (mainImage) és a hozzá tartozó további képek (image1, image2,...) **teljes** url elérését tartalmazza, cache-elt formában.

#### 2019.07.05.
- Customer és Customer Extend resource-khoz elkészült egy **updatedAtMin** filter, ami a megadott dátum után módosított 
vásárlókat adja vissza. [dokumentáció](https://www.shoprenter.hu/api/doc#customer_extend)

#### 2019.06.23. 
- **Product Extend** resource-ba belekerült a **manufacturer** kibontva, hogy ne kelljen újabb lekérés hozzá 
[dokumentáció](https://www.shoprenter.hu/api/doc#product_extend)    

#### 2019.06.21.
- **API batch feldolgozó**nál memória optimalizálás történt, hogy egyszerre több request-et is tudjon kezelni. 
[dokumentáció](BATCH_API.md)

#### 2019.05.30.
- Order resource-ba bekerült az **originalPrice** mező [dokumentáció](https://www.shoprenter.hu/api/doc#order)

#### 2019.05.03.
- Product és ProductExtend resource-ba bekerült a **cost** mező [dokumentáció](https://www.shoprenter.hu/api/doc#product)

#### 2019.04.29.
- A **full** paraméter segítségével a lista lekéréseknél már egy requestben elérjük a lista elemek tartalmát, 
análkül hogy újabb kéréseket kellene indítani. Ez minden resource esetén elérhető. 
[dokumentáció](FULL_PARAMETER.md) 

#### 2019.02.01.
- **Address resource**-ba bekerült a telephone mező [dokumentáció](https://www.shoprenter.hu/api/doc#address)

#### 2018.12.05.
- **CategoryExtend resource** elkészítése [dokumentáció](https://www.shoprenter.hu/api/doc#category_extend)
- **CustomerExtend resource** elkészítése [dokumentáció](https://www.shoprenter.hu/api/doc#customer_extend)  
- [Mire használhatóak a kiterjesztett Resourceok?](EXTEND_RESOURCE.md)

#### 2018.09.25.
- **Webhook resource** elkészítése, aminek segítségével webhook-ot lehet létrehozni
 [dokumentáció](https://www.shoprenter.hu/api/doc#webhook)

#### 2018.09.13.
- **ScriptTag resource** elkészítése, aminek segítségével a frontendre lehet API-n keresztül script-et elhelyezni
 [dokumentáció](https://www.shoprenter.hu/api/doc#script_tag)

#### 2017.10.20.
- **ProductExtend resource** elkészítése [dokumentáció](https://www.shoprenter.hu/api/doc#product_extend)
- **OrderExtend resource** elkészítése [dokumentáció](https://www.shoprenter.hu/api/doc#order_extend)
- [Mire használhatóak a kiterjesztett Resourceok?](EXTEND_RESOURCE.md)

#### 2017.07.27. 
- **Többnyelvűség** lekezelése a **Document Description** resource-nál
 [dokumentáció](https://www.shoprenter.hu/api/doc#document_description)

#### 2017.06.30. 
- Beszédes **hibaüzenetek** visszaadása [dokumentáció](STATUS_CODES.md)
