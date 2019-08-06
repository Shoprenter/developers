### API hívásokkal kapcsolatos követelmények és korlátozások:

- A Header adatok közül, a **Content-Type** érték megadása kötelező!<br>
A alábbi formátumok elérhetőek, majd a kiválasztott formátum fogja meghatározni a kommunikációt az API-val.
  + JSON: **application/json** (ajánlott)
  + FormData: **multipart/form-data**
- API hívás válaszát alapértelmezetten XML formátumban kapja meg az alkalmazás
- Amennyiben az API hívás válaszát JSON formátumban szeretnénk visszakapni, akkor már az API hívásnál a Headerben meg kell adni, hogy **Accept: application/json**
- A maximálisan indítható requestek limitje **180/perc**. Túllépés esetén 429-as hibakódot kapunk válaszként
