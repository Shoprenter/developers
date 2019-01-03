## Getting started

### Az App integrációhoz szükséges adatok:

- **App neve:** ez fog megjelenni a telepíthető alkalmazások listájába. **Az app tulaja adja.**
- **AppId:** app azonosítója a ShopRenteren belül. ShopRenter adja.
- **ClientId:** App azonosító. ShopRenter adja
- **ClientSecret:** Kulcs a kérések azonosításához. ShopRenter adja.
- **EntryPoint:** Az app belépési pontja. Az app fejlesztője adja. HTTPS-protokollon keresztül elérhetőnek kell lennie. **Az app tulaja adja.**
- **RedirectUri:** Az app authentikációs belépési pontja ezen az url-en keresztül fogja az authentikációs adatokat igényelni az adott ShopRenter-es bolt API-jához. HTTPS protokollon keresztül elérhetőnek kell lennie. **Az app tulaja adja.**


### App telepítésének menete:
1. A felhasználó az app telepítésére kattint a ShopRenter admin felületén.
2. A Shoprenter egy iframeban meghívja az app által bíztosított RedirectUri-t (GET request).
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
    - **client_id:** Az App ClientId-ja
    - **client_secret:** Az app ClientSecret-e 
    - **code:** a requestben kapod code
    - **timestamp:** a requestben kapott timestamp
    - **hmac:** a requestben kapott hmac
5. Amennyiben a ShopRenter megfelelőnek találja a POST requestet egy username, password párossal fog válaszolni amivel az app hozzáfér az adott bolt API-jához.
6. A kiszolgáló ha megkapta az authentikációs adatokat redirecttel a [refererDomain]/admin/app/[appId] url-re, ahol a refererDomain-t érdemes a request header-ből kiszedni, mivel a boltoknak egyedi domain neve is lehet.
7. A ShopRenter egy Iframeben megnyitja az apphoz tartozó EntryPoint-ot. A request tartalmazni fogja a 2. pontban írt paramétereket.
8. Feltelepítés után a ShopRenter csak az Entrypointra küld kéréseket. Minden esetben a 2. pontban írt paraméterekkel.
