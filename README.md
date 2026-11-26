# NAKOM – Furniture & Design

A NAKOM weboldal és az online bútortervező (prototípus). Teljesen statikus oldal, nincs szükség szerverre vagy adatbázisra: GitHub Pages-en ingyen futtatható.

## Mi van benne

```
index.html              – főoldal (webshop-kirakat)
tervezo/index.html      – online bútortervező (3D, alaprajz, szabásjegyzék, ár)
assets/img/             – helykitöltő képek (cseréld saját renderekre)
assets/vendor/three.min.js – 3D motor (three.js r147), helyben, hogy CDN nélkül is fusson
assets/favicon.svg      – böngészőfül-ikon
.nojekyll               – a GitHub Pages ne dolgozza fel Jekyllel
```

A főoldal „Bútor tervező indítása” és „Tervező” gombjai a `tervezo/` oldalra visznek, a tervező logója vissza a főoldalra.

## Kipróbálás a saját gépen

A tervező fájlként megnyitva (dupla kattintás) nem mindenhol működik, ezért indíts egy kis helyi szervert a mappában:

```
python -m http.server 8000
```

Utána böngészőben: http://localhost:8000

## Feltöltés GitHubra (GitHub Pages)

1. A github.com-on: **New repository** → név pl. `nakom` → Public → Create.
2. A repository oldalán: **Add file → Upload files**, húzd be a mappa **teljes tartalmát** (az `index.html` legyen a gyökérben, ne egy almappában). Commit.
   - A `.nojekyll` rejtett fájl; ha a feltöltő nem látja, nem baj, nélküle is működik.
3. **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main`, mappa: `/ (root)` → Save.
4. 1–2 perc múlva az oldal elérhető: `https://<felhasználónév>.github.io/nakom/`
   A tervező: `https://<felhasználónév>.github.io/nakom/tervezo/`

Parancssorból ugyanez:

```
git init
git add .
git commit -m "NAKOM weboldal és bútortervező"
git branch -M main
git remote add origin https://github.com/<felhasználónév>/nakom.git
git push -u origin main
```

## Beállítandó dolgok

- **E-mail cím az ajánlatkéréshez:** `info@nakom.hu` szerepel kétszer – a `tervezo/index.html` elején (`NAKOM_EMAIL`) és az `index.html` végén. Írd át a valósra. Az ajánlatkérés most az ügyfél e-mail-programját nyitja meg kitöltve, a terv linkjével együtt.
- **Egységárak:** a tervezőben az oldal alján, az „Ár és egységárak” fülön. Ezek **példaértékek**; amit ott átírsz, azt az adott böngésző megjegyzi. Ha mindenkinél más alapértéket akarsz, a `tervezo/index.html`-ben a `let PRICE = {...}` sort írd át.
- **Képek:** az `assets/img/` fájljait cseréld le saját renderekre ugyanazzal a fájlnévvel.

## Tudnivalók a prototípusról

- **Mentés:** a „Mentés és link” a teljes projektet (szoba + elemek) a linkbe teszi – nincs szükség fiókra vagy szerverre. A böngésző a legutóbbi projektet magától is megjegyzi.
- **Kosár:** csak az adott böngészőben él, fizetés és rendelésküldés még nincs bekötve.
- **Bejelentkezés:** nincs. Valódi fiókhoz, mentett projektekhez és rendeléskezeléshez háttérszolgáltatás kell (pl. Supabase vagy Firebase) – ez a következő lépés lehet.
- **Szabásjegyzék és szabási terv:** egyszerűsített szerkezeti szabályokkal készül (ráütődő front, 3 mm fuga, 13 mm fiókcsúszó-hézag, 18 mm lap, 3 mm HDF hátfal). Gyártás előtt asztalosnak ellenőriznie kell.
