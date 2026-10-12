# Ki a kém? — Who's the spy?

Szavas partijáték egy telefonnal. Ingyenes, reklám és telepítés nélkül, offline is megy.
A word party game played on one phone you pass around. Free, no ads, no install, works offline.

- 26 témakör / categories, ~1080 magyar és ~1000 angol szó
- 3–15 játékos, több kém is lehet
- Öt kémmód: semmi · téma · betűk · nyom · álszó
- Beépített szabályok (HU/EN), szójavaslat és hibajelzés GitHub issue-ként

## Felépítés / Layout

| Fájl | Mire való |
|---|---|
| `index.html` | Az egész játék: stílus, szólisták (`PACKS`), nyomok (`CLUES`), szövegek (`T`), logika |
| `sw.js` | Service worker az offline módhoz. **Minden kiadásnál emeld a `CACHE` verziót**, különben a telepített példányok a régit mutatják. |
| `manifest.webmanifest`, `icon-*.png` | Telepíthető webapp (PWA) |
| `fonts/` | Saját tárhelyről kiszolgált betűtípusok (SIL Open Font License, lásd `OFL-*.txt`) |
| `og-image.jpg` | Linkmegosztási előnézet (1200×630). Forrása: `tools/og-image.html` |

## Szó hozzáadása / Adding a word

1. Írd be a szót a megfelelő `PACKS` sorba (`|`-vel elválasztva).
2. Ha a témának van nyoma, tedd be a `CLUES` alatt a megfelelő csoportba is — a nyom mód csak azokat a témákat kínálja, ahol a szavak legalább 90%-ának van nyoma.
3. Ugyanaz a szó ne szerepeljen két témában (kivéve, ha mást jelent: pl. *cápa* állat / *Cápa* film).
4. Emeld a `CACHE` verziót a `sw.js`-ben.

A játékosok a beállítások alján lévő linkkel, illetve az eredményképernyőn („Gond van ezzel a szóval?”) előre kitöltött GitHub issue-t nyithatnak.

## Előnézeti kép / Share image

Ha változik a `tools/og-image.html`, generáld újra (Edge vagy Chrome, headless):

```sh
msedge --headless=new --hide-scrollbars --force-device-scale-factor=1 --window-size=1200,630 \
  --virtual-time-budget=3000 --screenshot=og.png tools/og-image.html
```

Aztán mentsd JPEG-be (~90-es minőség) `og-image.jpg` néven — 300 KB alatt kell maradnia, különben a WhatsApp nem mutatja.

## Futtatás helyben / Run locally

A service worker miatt webszerver kell (nem elég duplán kattintani a fájlra):

```sh
python -m http.server 8000
```

Aztán: http://localhost:8000

## Kiadás / Deploy

Bármilyen statikus tárhely jó: GitHub Pages, Netlify, Cloudflare Pages. Build lépés nincs.
