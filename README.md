# Netflix Italia Top 10 — v2

Addon Stremio/Nuvio con due cataloghi distinti:

- Netflix Italia • Top 10 Film
- Netflix Italia • Top 10 Serie TV

## Poster personalizzati

La v2 costruisce ogni cover così:

1. prova a recuperare da TMDb un poster **textless** (senza scritte), usando l'IMDb ID;
2. applica una sfumatura dal 48% dell'immagine fino al nero in basso;
3. applica il numero di posizione (`01`–`10`);
4. recupera automaticamente da TMDb il **logo ufficiale del film/serie** e lo mette sopra la gradient;
5. aggiunge il wordmark Netflix in fondo.

`assets/ranks/01.svg` contiene il tuo SVG 01. Per i rank mancanti viene generato automaticamente un fallback; puoi sostituirli aggiungendo `02.svg` ... `10.svg` nella stessa cartella.

## Avvio

```bash
npm install
npm start
```

Poi apri:

```text
http://localhost:7000/manifest.json
```

Cataloghi:

```text
http://localhost:7000/catalog/movie/netflix-it-top10-movies.json
http://localhost:7000/catalog/series/netflix-it-top10-series.json
```

Per testare una cover:

```text
http://localhost:7000/poster/movie/tt0111161/1.jpg
```

## TMDb

La chiave è letta da `.env`:

```env
TMDB_API_KEY=...
```

**Non pubblicare `.env` su GitHub.** `.gitignore` è già configurato per escluderlo.

## Logo Netflix

Il pacchetto include `assets/netflix-logo.svg`, modificabile/sostituibile. Se hai un tuo PNG/SVG del logo, puoi sostituire il file mantenendo lo stesso nome o aggiornando `NETFLIX_LOGO_PATH` in `src/poster.js`.

## Regolazioni grafiche

In `src/poster.js` puoi cambiare rapidamente:

- gradient: `bottomFadeSvg()`;
- grandezza rank: `.resize({ width: 275 })`;
- posizione rank: `top: 42, left: 14`;
- grandezza logo titolo: `width: 360, height: 150`;
- posizione logo titolo: `top: 735 - height / 2`;
- grandezza Netflix: `.resize({ width: 108 })`;
- margine Netflix dal fondo: `22` pixel.

Durante le prove `POSTER_CACHE_SECONDS=300`. Puoi portarlo a `0` nel `.env` se vuoi evitare cache.
