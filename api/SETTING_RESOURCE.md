# Setting Resource értékeinek jelentése


Az alábbi táblázatban az API által visszaadott kulcsok jelentései találhatóak:

| Kulcs | Jelentés |
|:------|:---------|
|stockfilter_default|Csak a raktáron lévő termékeket listázza ki. Értékei:<br>0 - Nem<br>1 - Igen|
|stock_countdown|Raktárkészlet megjelenítéseinek módjai. Értékei:<br>1 - Hagyományos (Előnézet: x db raktáron)<br>2 - Visszaszámlálás (Előnézet: Utolsó x darab)|
|config_stock_status_id|Készletállapot azonosítója, ha a termék mindkét raktárkészlete nulla|
|config_instock_status_id|Készletállapot azonosítója, ha a termék mindkét raktárkészlete nagyobb, mint nulla|
|config_stock_count|Kezelendő raktárok száma. Maximum érték: 4|
|config_wh2_stock_status_id|Raktár 1 készletállapotának azonosítója|
|config_wh3_stock_status_id|Raktár 2 készletállapotának azonosítója|
|config_wh4_stock_status_id|Raktár 3 készletállapotának azonosítója|
|config_wh5_stock_status_id|Raktár 4 készletállapotának azonosítója|
|config_disable_addtocart_no_quantity|0 raktár esetén a **KOSÁRBA** gomb tiltása. Jelentése: Amennyiben a termékből nincs készleten, ne lehessen kosárba tenni. Értékei:<br>0 - Nem<br>1 - Igen|
|config_request_quantity_notify|0 raktár esetén értesítés kérés engedélyezése. Jelentése: Amennyiben a termékből nincs készleten, a látogató értesítést kérhet a készletváltozásról. Értékei:<br>0 - Nem<br>1 - Igen|
|prior_quantity|Elsődleges raktár|
|show_children_in_stock|Gyerek termék mutatása, ha a szülő nincs raktáron. Ha a szülő termék nincs raktáron, és van olyan gyerek termék, ami igen, akkor azt mutatja a szülő helyett. Értékei:<br>0 - Nem<br>1 - Igen|
|filter_all_childen|Az összes gyerektermék megjelenítése. Kategórialista oldal megjelenítését szabályozza, nincs hatással a szűrő működésére. Értékei:<br>0 - Nem<br>1 - Igen|
|config_stock_display_list|Készlet megjelenítése listázó oldalon. Értékei:<br>0 - Nem<br>1 - Igen|
|stock_countdown_limit|A raktárkészlet ettől a darabszámtól kisebb értékek esetén jelenik meg|
|stock_countdown_force|A raktárkészlet visszaszámláló megjelenítődik a raktárállapottól függetlenül. Aktiválva a visszaszámlálás akkor is megjelenik, ha készlet kijelzés megjelenítése a termékoldalon, a listázó oldalakon vagy a modulokban nemre van állítva. Értékei:<br>0 - Nem<br>1 - Igen|
|config_owner|A bolt üzemeltetőjének a neve|
|config_telephone|A bolt üzemeltetőjének a telefonszáma|
|config_address|A bolt üzemeltetőjének a címe|
|config_email|Kapcsolati e-mail cím, ahová a kapcsolat menüpontban megírt üzenetek fognak érkezni|
|config_language|A bolt nyelvének ISO kódja pl: hu|
|config_currency|A bolt által használt pénznem pl: HUF|
|config_tax_class_id|A bolt által használt ÁFA kulcs Tax Class Resource azonosítója|
|config_maintenance|A karbantartás oldal státusza. Értékei:<br>0 - Karbantartás oldal kikapcsolva.<br>1 - Karbantartás oldal bekapcsolva.|
|cart_ajax|Kosárba rakás módja. Értékei:<br>0 - Normál (a felhasználó a kosárhoz ugrik)<br>1 - AJAX-os (a felhasználó az oldalon marad)<br>4 - Felugró ablakos|
|config_customer_group_id|Regisztráció után a felhasználó ezzel a Customer Group Resource azonosítóval rendelkező vevőcsoportba fog kerülni|
|config_image_product_width|Kategóriaoldalon és termékmodulokban megjelenő termékképek szélessége|
|config_image_product_height|Kategóriaoldalon és termékmodulokban megjelenő termékképek magassága|
|config_catalog_limit|Katalógus oldalanként megjelenő termékek száma|
|config_template|A bolt által használt sablon neve pl: tokyo_blue, korfu_global|
|config_sort|A Kategóriaoldalak alapértelmezett rendezési módja. Értékei:<br>p.sort_order&#124;ASC - Alapértelmezett<br>pd.name&#124;ASC - Név, A - Z<br>pd.name&#124;DESC - Név, Z - A<br>m.name&#124;ASC - Gyártó, A - Z<br>m.name&#124;DESC - Gyártó, Z - A<br>p.price&#124;ASC - Ár, alacsony > magas<br>p.price&#124;DESC - Ár, magas > alacsony<br>rating&#124;DESC - Értékelés, legjobb<br>p.date_available&#124;DESC - Elérhetőség, legújabb
|config_sort_options|A Kategóriaoldalak választott rendezési módjai. Értékei a config_sort által visszaadott értékekből képzett tömb|
|sort_by_price_offer_request_position|Ár szerinti rendezés esetén az árajánlatkéréses termékek poziciója a kategóriaoldalon. Értékei:<br>start - Lista elején<br>end - Lista végén|
|config_customer_price|Termékárak elrejtése. Csak bejelentkezett vásárlók láthatják az árat. Értékei:<br>0 - Nem<br>1 - Igen|
|config_display_mode|Ár kiírás módja a termékoldalon. Értékei:<br>1 - Csak a bruttó ár kiírása<br>2 - Bruttó ár, mögötte zárójelben a nettó + ÁFA kiírása<br>3 - Csak a nettó ár kiírása<br>4 - A nettó ár és mögötte a + ÁFA kiírása<br>5 - A nettó ár és mögötte a + ÁFA kiírása, illetve zárójelben a bruttó ár kiírása|
|list_price_display_mode|Ár kiírás módja a kategóriaoldalon. Értékei:<br>1 - Csak a bruttó ár kiírása<br>2 - Bruttó ár, mögötte zárójelben a nettó + ÁFA kiírása<br>3 - Csak a nettó ár kiírása<br>4 - A nettó ár és mögötte a + ÁFA kiírása<br>5 - A nettó ár és mögötte a + ÁFA kiírása, illetve zárójelben a bruttó ár kiírása|
|module_price_display_mode|Ár kiírás módja a modul-termékkártyán. Értékei:<br>1 - Csak a bruttó ár kiírása<br>2 - Bruttó ár, mögötte zárójelben a nettó + ÁFA kiírása<br>3 - Csak a nettó ár kiírása<br>4 - A nettó ár és mögötte a + ÁFA kiírása<br>5 - A nettó ár és mögötte a + ÁFA kiírása, illetve zárójelben a bruttó ár kiírása|
|config_special_original_list|Akciós árnál az eredeti ár megjelenítése a listázó oldalakon. Értékei:<br>0 - Nem<br>1 - Igen|
|config_special_original_search|Akciós árnál az eredeti ár megjelenítése a keresési javaslatoknál. Értékei:<br>0 - Nem<br>1 - Igen|
|config_price_tag|Ár kiírás módja szülő-gyerek viszony esetén. Értékei:<br>0 - Szülőtermék árának megjelenítése<br>1 - Legalacsonyabb termék árának megjelenítése + “-tól” toldattal|
|fictive_parent|Szülőtermékek fiktív szülőként viselkedése. Értékei:<br>0 - Nem<br>1 - Igen|
|search_description|A kereső alapértelmezetten keressen-e termékleírásokban. Értékei:<br>0 - Nem<br>1 - Igen|
|search_subcategory|A kereső alapértelmezetten keressen az alkategóriákban is. Értékei:<br>0 - Nem<br>1 - Igen|
|storno_order_status_id|A törölt rendelés státusz azonosítója|
|product_url_without_category|Kategória oldali URL-ek felépítése. Értékei:<br>0 - Teljes elérési út<br>1 - Csak termékoldal|

