### API hívásokkal kapcsolatos követelmények és korlátozások:

- API híváskor a Headerben a **Content-Type: multipart/form-data** megadása kötelező
- API hívás válaszát alapértelmezetten XML formátumban kapja meg az alkalmazás
- Amennyiben az API hívás válaszát JSON formátumban szeretnénk visszakapni, akkor már az API hívásnál a Headerben meg kell adni, hogy **Accept: application/json**
- A maximálisan indítható requestek limitje **180/perc**. Túllépés esetén 429-as hibakódot kapunk válaszként
