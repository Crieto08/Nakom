# NAKOM – Furniture & Design

A NAKOM weboldal és az online bútortervező (prototípus). Teljesen statikus oldal, nincs szükség szerverre vagy adatbázisra: GitHub Pages-en ingyen futtatható.

## Mi van benne

```
index.html              – főoldal (webshop-kirakat)
tervezo/index.html      – online bútortervező (3D, alaprajz, szabásjegyzék, ár)
assets/img/             – helykitöltő képek (cseréld saját renderekre)
assets/vendor/three.min.js – 3D motor (three.js r147), helyben, hogy CDN nélkül is fusson
assets/vendor/TransformControls.js – mozgató/forgató gizmó a tervezőhöz
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

## Funkciók

**Bolt (főoldal):** kategória-menü (asztali gépen lenyíló, mobilon oldalsó menü), élő kereső javaslatokkal (kategóriák és termékek, ékezet nélkül is talál), szűrés kategóriára, rendezés ár/név szerint, termék-gyorsnézet méret- és színválasztással, kosár mennyiséggel. Mobilon 2 oszlopos termékrács.

**Tervező:** szoba + több bútor, 3D és alaprajz nézet. A kijelölt bútor a gizmóval húzható (nyilak) vagy forgatható (Forgatás gomb, 90°-onként); a falhoz és egymáshoz igazodik. Törlés: a felső eszköztár Törlés gombja, a Delete billentyű vagy az Elemek listája. Padló és fal: 6–6 textúra + szabad színválasztó. Mobilon két ujjal nagyítható.

**Közös kosár:** a bolt és a tervező ugyanazt a kosarat használja (a böngészőben tárolva). A tervezőből kosárba tett projekt a boltban is megjelenik, a terv linkjével együtt.

## Termékek és kategóriák szerkesztése

Az `index.html` alján, a `<script>` elején:
- `CATS` – főkategóriák és alkategóriák (azonosító, név, kép).
- `P` – termékek: név, kategória, alkategóriák, ár (Ft), kép, leírás, méretválasztó (`[felirat, felár]`), és opcionálisan `preset` – melyik tervező-sablonnal nyíljon a „Testreszabom a tervezőben” gomb.
- `COLORS` – a gyorsnézet színválasztója.

## Beállítandó dolgok

- **E-mail cím az ajánlatkéréshez:** `info@nakom.hu` szerepel kétszer – a `tervezo/index.html` elején (`NAKOM_EMAIL`) és az `index.html` végén. Írd át a valósra. Az ajánlatkérés most az ügyfél e-mail-programját nyitja meg kitöltve, a terv linkjével együtt.
- **Egységárak:** a tervezőben az oldal alján, az „Ár és egységárak” fülön. Ezek **példaértékek**; amit ott átírsz, azt az adott böngésző megjegyzi. Ha mindenkinél más alapértéket akarsz, a `tervezo/index.html`-ben a `let PRICE = {...}` sort írd át.
- **Képek:** az `assets/img/` fájljait cseréld le saját renderekre ugyanazzal a fájlnévvel.

## Tudnivalók a prototípusról

- **Mentés:** a „Mentés és link” a teljes projektet (szoba + elemek) a linkbe teszi – nincs szükség fiókra vagy szerverre. A böngésző a legutóbbi projektet magától is megjegyzi.
- **Kosár és rendelés:** a kosár az adott böngészőben él; a „Megrendelés kérése” kitöltött e-mailt nyit. Online fizetés még nincs bekötve.
- **Árak:** a bolt árai és a tervező egységárai példaértékek.
- **Bejelentkezés:** nincs. Valódi fiókhoz, mentett projektekhez és rendeléskezeléshez háttérszolgáltatás kell (pl. Supabase vagy Firebase) – ez a következő lépés lehet.
- **Szabásjegyzék és szabási terv:** szerkezet: felső (falra szerelt) elemnél az oldalak adják a teljes magasságot, a tető és a fenék az oldalak közé kerül; alsó (álló) elemnél – a konyhai alsókat is beleértve – fordítva: a tető és a fenék teljes szélességű, az oldalak közéjük kerülnek. Ráütődő front, 3 mm fuga, 13 mm fiókcsúszó-hézag, 18 mm lap, 3 mm HDF hátfal. A polcközök és a fiókmagasságok rekeszenként állíthatók. Bútorlap mindig 18 mm. Elemenként választható: felső lezárás (tetőlap, vagy konyhai alsónál 2 db 10 cm-es merevítő vízszintesen / mosogatószekrénynél függőlegesen), MDF hátfal van/nincs, zsanér fékes/sima. Rekesztípus: nyitott, egyajtós, kétajtós, fiókos. Gyártás előtt asztalosnak ellenőriznie kell.
