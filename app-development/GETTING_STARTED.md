## Getting started

### Az Alkalmazás integrációhoz szükséges adatok:

Az alkalmazás beregisztrálásához szükséges adatokat kérjük elküldeni a partnersupport@shoprenter.hu email címre.

**Az alkalmazás tulajának a következő adatokat kell biztosítania.**
- **Alkalmazás neve:** ez fog megjelenni a telepíthető alkalmazások listájába.
- **EntryPoint:** Az alkalmazás belépési pontja. Az alkalmazás fejlesztője adja. HTTPS-protokollon keresztül elérhetőnek kell lennie.
- **RedirectUri:** Az alkalmazás authentikációs belépési pontja ezen az url-en keresztül fogja az authentikációs adatokat igényelni az adott ShopRenter-es bolt API-jához. HTTPS protokollon keresztül elérhetőnek kell lennie. **Figyelem!** Ha pl. single-page application lesz a kliens, ahol URL resource azonosítóval van megadva egy-egy route (https://example.com/shoprenter#redirect), azt technikai okokból, nem tudjuk elfogadni.
- **UninstallUri:** Az alkalmazás törlése után egy GET kérés lesz elküldve erre az URL-re, hogy az alkalmazás még egy utolsó műveletet tudjon végrehajtani. (Megjegyzés: QueryString-ben hozzá lesznek fűzve a következő adatok: shopname, code, timestamp, hmac.)
- **Alkalmazás logo:** az alkalmazás listában megjelenő logó kép (**250x150px**).
- **Alkalmazás rövid leírása:** Maximum 70 karakteres rövid szöveg.
- **Alkalmazás részletek link:** Az alkalmazás részleteire/sales oldalára mutató link.
- **Alakalmazás típusa:** Az alkalmazás lehet admin felületbe ágyazott vagy átírányításos. Beágyazásnál az apphoz tartozó, ShopRenter adminonos url-jére érkezve, az entry point-nak megadott url-t hívjuk be egy iframe-be. Átírányításnál pedig szimplán átírányítunk az entry pointra.
- **A tesztbolt neve:** Az alkalmazás fejelsztése elején igényelni kell a shoprenter.hu oldalon egy próbaboltot. Itt megadható a boltnév, amit a bolt domainja első részeben - <bolt_nev>.shoprenter.hu - lesz látható.

**Az alkalmazás rendszerbe való felvétele után a következő adatokat a ShopRenter küldi el:**
- **AppId:** alkalmazás azonosítója a ShopRenteren belül. 
- **ClientId:** alkalmazás azonosító.
- **ClientSecret:** Kulcs a kérések azonosításához.
- **App URL:** Az alkalmazás ShopRenter-es URL-e.

### Alkalmazás telepítésének menete:
1. A felhasználó az alkalmazás telepítésére kattint a ShopRenter admin felületén.
2. A Shoprenter meghívja az alkalmazás által bíztosított RedirectUri-t (GET request).
    A hívás során átadott paraméterek:
    - **shopname:** a bolt neve amiből a hívást indították
    - **code:** generált hash
    - **timestamp:** kérés ideje
    - **hmac:** ellenőrző hash
3. Kiszolgáló félnek célszerű ellenőrizni hogy a kérést valóban a ShopRenter küldte:
Annak ellenőrzése, hogy a kérést a ShopRenter küldte:
A querystring hmac nélüli részének (code=0907a61c0c8d55e99db179b68161bc00&shopname=example&timestamp=1337178173) a **ClientSecret**-el sha256 elkódolva egyenértékűnek kell lennie a querystring hmac paraméterének értékével.
4. A kiszolgáló fél ha rendben találta a kérést. Küld egy POST requestet a ShopRenter felé az https://[shopname].shoprenter.hu/admin/oauth/access_credential url-re.
A post requestnek tarttalmaznia kell az alábbi mezőket:
    - **client_id:** Az Alkalmazás ClientId-ja
    - **client_secret:** Az Alkalmazás ClientSecret-e 
    - **code:** a requestben kapod code
    - **timestamp:** a requestben kapott timestamp
    - **hmac:** a requestben kapott hmac
    
    Amennyiben valamelyik adat hiányos vagy téves, úgy az API hibaüzenetet fog küldeni a megfelelő hibakóddal json formátumban. 
    
    **Hibák**:
    - Ha elküldendő adatok közül valamelyik hiányzik, akkor **{"message":"Missing data in credential request","code":400}** választ fog adni.
    - Ha elküldendő client_id és secret_id eltér, akkor **{"message":"App client and request client data mismatch","code":401}** választ fog adni.
    - Ha a hitelesítési idő meghaladja a 30 másodpercet, akkor **{"message":"Authorization time expired","code":408}** választ fog adni.
    - Ha a telepítés közben hiba merült fel, akkor  **{"message":"App is not installed","code":409}** választ fog adni.
5. Amennyiben a ShopRenter megfelelőnek találja a POST requestet egy username, password párossal fog válaszolni amivel az Alkalmazás hozzáfér az adott bolt API-jához. A 2. lépésben indított ShopRenteres kérésben lévő timestamp arra szolgál, hogy megvizsgáljuk, a kliens alkalmazás **30 másodpercen belül** megkezdi-e a API hozzáférés kérését!
6. Az alkalmazás, ha megkapta az authentikációs adatokat, redirecttel a https://[primaryDomain]/admin/app/[appId] url-re, ahol a primaryDomain-t a [Domain Resource](https://doc.shoprenter.hu/api/domain.html#tulajdonsagok)-ból lehet lekérdezni. Ez azért fontos, mert a boltoknak egyedi domain neve is lehet!

    **Megjegyzés:** Van lehetőség az app Shoprenteres url-jére való redirect alkalmával tetszőleges query paramétereket küldeni. Ezek a paraméterek az entryPoint       URL-jében jelennek meg, az authentikációhoz használt (shopname, code, timestamp, hmac) paramétereken felül.

    Példa: 
    Legyen az EntryPoint: https://demoapp.com/entryPoint
    Erre redirecttel az alkalmazás: https://[primaryDomain]/admin/app/[appId]?pelda=parameter
    Ez esetben az EntryPoint íly módon hívódik meg: https://demoapp.com/entryPoint?shopname=[shopname]&code=[code]&timestamp=[timestamp]&hmac=                  [hmac]&pelda=parameter


7. A ShopRenter egy Iframeben megnyitja az alkalmazáshoz tartozó EntryPoint-ot. A request tartalmazni fogja a 2. pontban írt paramétereket.
8. Feltelepítés után a ShopRenter csak az Entrypointra küld kéréseket. Minden esetben a 2. pontban írt paraméterekkel.

## Példa alkalmazások
- [SR Demo app PHP](https://github.com/Shoprenter/sr-demo-app-php)
- [SR Demo app Node.js](https://github.com/Shoprenter/sr-demo-app-node)
