# Ki a kém? — Who's the spy?

Szavas partijáték egy telefonnal. Ingyenes, reklám és telepítés nélkül, offline is megy.
A word party game played on one phone you pass around. Free, no ads, no install, works offline.

- 26 témakör / categories, ~1090 magyar és ~1010 angol szó
- 3–15 játékos, több kém is lehet
- Öt kémmód: semmi · téma · betűk · nyom · álszó

## Felépítés / Layout

| Fájl | Mire való |
|---|---|
| `index.html` | Az egész játék: stílus, szólisták (`PACKS`), nyomok (`CLUES`), szövegek (`T`), logika |
| `sw.js` | Service worker az offline módhoz. **Minden kiadásnál emeld a `CACHE` verziót**, különben a telepített példányok a régit mutatják. |
| `manifest.webmanifest`, `icon-*.png` | Telepíthető webapp (PWA) |
| `fonts/` | Saját tárhelyről kiszolgált betűtípusok (SIL Open Font License, lásd `OFL-*.txt`) |

## Szó hozzáadása / Adding a word

1. Írd be a szót a megfelelő `PACKS` sorba (`|`-vel elválasztva).
2. Ha a témának van nyoma, tedd be a `CLUES` alatt a megfelelő csoportba is — a nyom mód csak azokat a témákat kínálja, ahol a szavak legalább 90%-ának van nyoma.
3. Emeld a `CACHE` verziót a `sw.js`-ben.

## Futtatás helyben / Run locally

A service worker miatt webszerver kell (nem elég duplán kattintani a fájlra):

```sh
python -m http.server 8000
```

Aztán: http://localhost:8000

## Kiadás / Deploy

Bármilyen statikus tárhely jó: GitHub Pages, Netlify, Cloudflare Pages. Build lépés nincs.
