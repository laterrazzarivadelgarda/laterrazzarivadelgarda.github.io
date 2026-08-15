# La Terrazza — mini sito

Sito statico a pagina singola per prenotazioni dirette via WhatsApp.
Nessuna build, nessuna dipendenza: è tutto dentro `index.html` + la cartella `img/`.

## 1. Impostare il numero WhatsApp

Apri `index.html`, cerca `CONFIGURAZIONE` (verso l'inizio del blocco `<script>`) e cambia due righe:

```js
const WHATSAPP = "393000000000";    // numero internazionale, SENZA + e senza spazi
const TEL_SHOW = "+39 300 000 000"; // come appare a schermo
```

Esempio: per `+39 347 1234567` → `WHATSAPP = "393471234567"`.

## 2. Provare in locale

```sh
cd sito
python3 -m http.server 8080
```

Poi apri <http://localhost:8080>.

## 3. Pubblicare su GitHub Pages (gratis)

1. Crea un repo su GitHub, es. `la-terrazza` (pubblico).
2. Carica il **contenuto** di questa cartella (`index.html` + `img/`) nella root del repo.
   Da terminale:
   ```sh
   cd sito
   git init && git add . && git commit -m "sito La Terrazza"
   git branch -M main
   git remote add origin https://github.com/TUO-UTENTE/la-terrazza.git
   git push -u origin main
   ```
3. Su GitHub: **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**.
4. Dopo ~1 minuto il sito è online su
   `https://TUO-UTENTE.github.io/la-terrazza/`

Alternativa ancora più rapida senza git: [app.netlify.com/drop](https://app.netlify.com/drop) — trascini la cartella `sito` e ottieni subito un URL.

## 4. QR code

Genera il QR sull'URL finale (es. con [qr.io](https://qr.io) o `qrencode`):

```sh
brew install qrencode
qrencode -o qr-laterrazza.png -s 12 -m 2 "https://TUO-UTENTE.github.io/la-terrazza/"
```

## Struttura

| Cosa | Dove |
|---|---|
| Testi in IT / EN / DE | oggetto `T` in `index.html` |
| Ordine e didascalie foto | array `PHOTOS` |
| Foto dei dintorni | array `NEAR` |
| Recensioni | array `REVIEWS` + chiavi `r1…r5` in `T` |
| Servizi elencati | array `AM_KEYS` + chiavi `a1…a18` in `T` |

Le foto sono in due versioni: `*-s.webp` (900 px, per griglia e anteprime) e `*.webp` (1700 px, per lo zoom a schermo intero).

## Note

- La lingua si rileva dal browser; la scelta manuale resta salvata (`localStorage`).
- Le recensioni sono quelle reali dell'annuncio Airbnb (valutazione 4,79 · 116 recensioni), tradotte in EN/DE con nota "tradotto".
- Non ci sono prezzi, date, policy né form: solo foto, descrizione e contatto.
