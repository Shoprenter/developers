# API changelog

##### 2019.07.05.
- Customer és Customer Extend resource-khoz elkészült egy **updatedAtMin** filter, ami a megadott dátum után módosított 
vásárlókat adja vissza. [dokumentáció](https://www.shoprenter.hu/api/doc#customer_extend)

##### 2019.06.25.
- **API batch feldolgozó**nál memória optimalizálás történt, hogy egyszerre több request-et is tudjon kezelni. 
[dokumentáció](BATCH_API.md)

##### 2019.06.23. 
- **Product Extend** resource-ba belekerült a **manufacturer** kibontva, hogy ne kelljen újabb lekérés hozzá 
[dokumentáció](https://www.shoprenter.hu/api/doc#product_extend)

##### 2019.05.30.
- Order resource-ba bekerült az **originalPrice** mező [dokumentáció](https://www.shoprenter.hu/api/doc#order)

##### 2019.05.03.
- Product és ProductExtend resource-ba bekerült a **cost** mező [dokumentáció](https://www.shoprenter.hu/api/doc#product)

##### 2019.04.29.
- A **full** paraméter segítségével a lista lekéréseknél már egy requestben elérjük a lista elemek tartalmát, 
análkül hogy újabb kéréseket kellene indítani. Ez minden resource esetén elérhető. 
[dokumentáció](FULL_PARAMETER.md) 

##### 2019.02.01.
- **Address resource**-ba bekerült a telephone mező [dokumentáció](https://www.shoprenter.hu/api/doc#address)

##### 2018.12.05.
- **CategoryExtend resource** elkészítése [dokumentáció](https://www.shoprenter.hu/api/doc#category_extend)
- **CustomerExtend resource** elkészítése [dokumentáció](https://www.shoprenter.hu/api/doc#customer_extend)  
- [Mire használhatóak a kiterjesztett Resourceok?](EXTEND_RESOURCE.md)

##### 2018.09.25.
- **Webhook resource** elkészítése, aminek segítségével webhook-ot lehet létrehozni
 [dokumentáció](https://www.shoprenter.hu/api/doc#webhook)

##### 2018.09.13.
- **ScriptTag resource** elkészítése, aminek segítségével a frontendre lehet API-n keresztül script-et elhelyezni
 [dokumentáció](https://www.shoprenter.hu/api/doc#script_tag)

##### 2017.10.20.
- **ProductExtend resource** elkészítése [dokumentáció](https://www.shoprenter.hu/api/doc#product_extend)
- **OrderExtend resource** elkészítése [dokumentáció](https://www.shoprenter.hu/api/doc#order_extend)
- [Mire használhatóak a kiterjesztett Resourceok?](EXTEND_RESOURCE.md)

##### 2017.07.27. 
- **Többnyelvűség** lekezelése a **Document Description** resource-nál
 [dokumentáció](https://www.shoprenter.hu/api/doc#document_description)

##### 2017.06.30. 
- Beszédes **hibaüzenetek** visszaadása [dokumentáció](STATUS_CODES.md)