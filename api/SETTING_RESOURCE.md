#Setting Resource értékeinek jelentése

A Setting Resource lekérdezésével a bolt adminisztrációs oldalán megadott fontosabb bolt beállításokat tudjuk lekérdezni, amelyeket a többek közt az alábbi oldalakon tudunk beállítani az admin oldalt.
 - Beállítások -> Bolt beállíátsok -> Általános beállítások
 - Beállítások -> Bolt beállíátsok -> Árak, Árkerekítés, Pénznem
 - Beállítások -> Bolt beállíátsok -> Kosár és Pénztár beállítások
 - Beállítások -> Bolt beállíátsok -> Belépés és Regisztráció beállítások
 - Beállítások -> Termék beállítások -> Működési beállítások
 - Beállítások -> Megjelenés -> Modulok beállítása
 - Beállítások -> Megjelenés -> Megjelenés beállítások

Az alábbi táblázatban az API által visszaadott kulcsok jelentései találhatók.

| Kulcs | Jelentés |
|:------|:---------|
|stockfilter_default|Csak a raktáron lévő termékeket listázása ki. Érékei:<br> 0 - Nem<br> 1 - Igen|
|stock_countdown|Raktárkészlet megjelenítési módja. Értékei:<br> 1 - Hagyományos (Előnézet: x db raktáron)<br> 2 - Visszaszámlálás (Előnézet: Utolsó x darab)|
|config_customer_price|Ár elrejtése. Csak bejelentkezett vásárlók láthatják az árat. Érékei:<br> 0 - Nem<br> 1 - Igen|
|config_display_mode|Ár kiírás módja. Értékei:<br>1 - Csak a bruttó ár kiírása<br>2 - Bruttó ár, mögötte zárójelben a nettó + ÁFA kiírása<br>3 - Csak a nettó ár kiírása<br>4 - A nettó ár és mögötte a + ÁFA kiírása<br>5 - A nettó ár és mögötte a + ÁFA kiírása, illetve zárójelben a bruttó ár kiírása|
|config_special_original_list|Akciós árnál az eredeti ár megjelenítése a listázó oldalakon. Érékei:<br> 0 - Nem<br> 1 - Igen|
|config_special_original_search|Akciós árnál az eredeti ár megjelenítése a keresési javaslatoknál. Érékei:<br> 0 - Nem<br> 1 - Igen|
|config_price_tag|Ár kiírás módja szülő-gyerek viszony esetén. Értékei:<br>0 - Szülőtermék árának megjelenítése<br>1 - Legalacsonyabb termék árának megjelenítése + “-tól” toldattal|
|config_stock_status_id|Készletállapot azonosítója, ha a termék mindkét raktárkészlete nulla.|
|config_instock_status_id|Készletállapot azonosítója, ha a termék mindkét raktárkészlete nagyobb mint nulla.|
|config_stock_count|Kezelendő raktárkészletek száma. Maximum érték 4.          |
|config_wh2_stock_status_id|Raktár 1 készletállapotának azonosítója|
|config_wh3_stock_status_id|Raktár 2 készletállapotának azonosítója|
|config_wh4_stock_status_id|Raktár 3 készletállapotának azonosítója|
|config_wh5_stock_status_id|Raktár 4 készletállapotának azonosítója|
|config_owner|A bolt üzemeltetőjének a neve|
|config_email|Kapcsolati e-mail cím. Ide fognak érkezni a kapcsolat menüpontban megírt üzenetek.           |
|config_language|A bolt nyelvének ISO kódja pl: hu|
|config_currency|A bolt által használt pénznem pl: HUF|
|config_tax_class_id|A bolt által használt ÁFA kulcs Tax Class Resource-beli azonosítója|
|config_maintenance|Karbantartás alatt van-e a bolt. Értékei:<br>0 - Nincs karbantartás alatt<br>1 -Karbantartás alatt|
|config_disable_addtocart_no_quantity|0 raktár esetén **KOSÁRBA** gomb tiltása. Amennyiben a termékből nincs készleten, ne lehessen kosárba tenni. Érékei:<br> 0 - Nem<br> 1 - Igen|
|config_request_quantity_notify|0 raktár esetén értesítés kérés engedélyezése. Amennyiben a termékből nincs készleten, a látogató értesítést kérhet a készletváltozásról. Érékei:<br> 0 - Nem<br> 1 - Igen|
|prior_quantity|Elsődleges raktár|
|cart_ajax|Kosárba rakás módja. Értékei:<br>0 - Normál (a felhasználó a kosárhoz ugrik)<br>1 - AJAX-os (a felhasználó az oldalon marad)<br>4 - Felugró ablakos|
|config_customer_group_id|Regisztráció után a felhasználó ezzel az azonosítóval rendelkező vevőcsoportba fog kerülni|
|config_image_product_width|Kategóriaoldalon és termékmodulokban megjelenő termékképek szélessége|
|config_image_product_height|Kategóriaoldalon és termékmodulokban megjelenő termékképek magassága|
|config_catalog_limit|Katalógus oldalanként megjelenő termékek száma|
|config_template|A bolt által használt sablon neve pl: tokyo_blue, korfu_global|
|fictive_parent|Szülőtermékek fiktív szülőként viselkedése. Érékei:<br> 0 - Nem<br> 1 - Igen|
|search_description|Alapértelmezetten keressen termékleírásokban. Érékei:<br> 0 - Nem<br> 1 - Igen|
|search_subcategory|Alapértelmezetten keressen az alkategóriákban is. Érékei:<br> 0 - Nem<br> 1 - Igen|
|storno_order_status_id|A sztornó rendelés státusz azonosítója|
