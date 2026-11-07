# Web de L'Espiral d'Osona

Web estàtica de L'Espiral d'Osona (psicoteràpia i mindfulness a Vic), feta amb el mateix sistema que elarasocial.com (repositori `lespiral/elarasocial`).
Es publica amb GitHub Pages des de la carpeta `docs/`. Ara és a **espiralosona.com** (des del 7/11/2026), i surt als cercadors.

Estat (6 de novembre de 2026): totes les pàgines de la web de WordPress (gestaltmindfulness.lespiral.cat, on redirigia espiralosona.com) passades amb els seus textos i les mateixes adreces. Les imatges encara no hi són: surten com a requadres marcats (vegeu «Imatges»).

## On és cada cosa

- `data/site.json`: el nom, l'adreça pública (`publish`), el menú (`nav`, amb desplegables a `children`), el botó de la capçalera (`cta`), el contacte i l'horari (`contact`), les xarxes (`social`), la franja «Si necessites ajuda» (`help`), els tres centres amb mapa (`maps`), el peu (`footer`), les adreces antigues (`redirects`) i la pàgina d'inici (`home`).
- `data/pages/<adreça>.json`: una pàgina per fitxer. `data/pages/contacte-2.json` es publica a `/contacte-2/`.
- `src/templates/`: les plantilles. `page.html` pinta qualsevol pàgina; `parts.html` té les peces (capçalera de pàgina, seccions, targetes, imatges).
- `src/site.css` i `src/site.js`: l'aspecte (Playfair Display + Inter i els blaus del logo) i el menú del mòbil.
- `src/img/`: els logos; `src/img/fotos/`: les fotos de les pàgines.
- `docs/`: la web generada. No s'edita a mà: es torna a generar.
- `tools/proves.py`: prova totes les pàgines en mòbil i en ordinador.

## Com es fa un canvi

1. Canvia el text al fitxer de `data/`.
2. Genera la web: `python3 build.py`. Si hi ha alguna errada (un tipus de secció que no existeix, un enllaç del menú a una pàgina que no hi és, un JSON mal escrit), ho diu i no genera res.
3. Prova-la: `python3 tools/proves.py` (errors de JavaScript, scroll lateral i enllaços trencats; amb `--captures` desa captures).
4. Desa i puja els canvis. GitHub Pages la publica sola.

No s'han d'inventar dades: si en falta alguna, es deixa marcada amb `[PENDENT]`. En generar la web, `build.py` diu quantes marques queden.

## Una pàgina

```json
{
  "seo_title": "El títol de la pestanya i dels cercadors",
  "kicker": "Avantítol petit",
  "title": "El títol gran (h1)",
  "lead": "Una frase sota el títol.",
  "sub": "Una altra línia més petita.",
  "image": "2024/07/foto-de-fons.jpg",
  "buttons": [{"text": "Demana hora", "href": "contacte-2"}, {"text": "Sobre nosaltres", "href": "sobre-nosaltres"}],
  "description": "El text dels cercadors.",
  "sections": [ ... ]
}
```

Tipus de secció (`"type"`):

- `text`: `title`, `kicker`, `intro`, `paragraphs`, `list`, `blocks` (subtítols amb paràgrafs o llista: `{"h": …, "paragraphs": […], "list": […]}`), `after`. Amb `"image"`, el text va al costat de la foto (`"reverse": true` la posa a l'esquerra). El primer paràgraf surt més gran si n'hi ha més d'un (`"lead": false` ho treu).
- `cards`: targetes (`items`) amb `image`, `icon`, `badge`, `title`, `lead`, `text`, `paragraphs`, `list`, `href` i `button` (el text de l'enllaç). `"cols": 2` per dues columnes; `before` posa paràgrafs abans.
- `list`: llista en quadres; amb `"band": "dark"` surt en blau fosc amb la foto al costat (Què aconseguiràs…).
- `steps`: passos numerats (`items` amb `title`, `lead`, `text` o `paragraphs`; `"n"` per triar el número).
- `team`: l'equip (`items` amb `photo`, `name`, `paragraphs`).
- `note`: un quadre destacat (`"style": "info"` blau, `"care"` per als avisos).
- `quote`: una cita gran (`text`) amb paràgrafs a sota.
- `cta`: un quadre blau amb paràgrafs i botons.
- `help`: la franja «Si necessites ajuda» (es pot canviar `title`, `text` i `items` en una pàgina concreta).
- `contact`: l'adreça, el telèfon, el correu i l'horari de `data/site.json`.
- `maps`: els tres centres amb el mapa de Google.
- `video`: vídeos de YouTube (`items` amb `title` i `youtube`); es carreguen quan es clica.

Cada secció pot portar `"band"` (`white`, `soft`, `stone`, `cream`, `dark`), `"buttons"` i `"id"`. Els enllaços (`href`) amb una paraula sola són pàgines de la web (`"contacte-2"` porta a `/contacte-2/`; `""` és l'inici). `**així**` surt en negreta. Amb `"html": true` a la secció, els textos poden portar HTML (enllaços).

## Imatges

A les dades s'escriu el camí de la imatge a WordPress (p. ex. `"2026/08/terapia-individual-vic-osona-lespiral.jpg"`). Si el fitxer (`terapia-individual-vic-osona-lespiral.jpg`) és a `src/img/fotos/`, surt la foto; si no, surt un requadre «Imatge pendent» amb el nom del fitxer.

`IMATGES-PENDENTS.md` (es refà sol amb `build.py`) diu quines falten, a quina pàgina surten i on són a la web antiga.

Logos que falten (de la carpeta del Drive *L'espiral › Logo nou 2021*):

- `src/img/logo-espiral.png`: la icona del cap amb l'espiral, quadrada i amb fons transparent (uns 200 × 200 px). Mentre no hi és, la capçalera porta una icona provisional.
- `src/img/favicon-48.png` (48 × 48 px) i `src/img/apple-touch-icon.png` (180 × 180 px).

## Adreces antigues

Les adreces de WordPress que ja no són una pàgina porten a la nova (`redirects` de `data/site.json`): `/blog/`, `/home-2-2/` i les entrades de prova de la plantilla porten a l'inici.

## Publicació

- GitHub Pages, branca `main`, carpeta `/docs`.
- L'adreça i si surt als cercadors són a `data/site.json`, a `publish`. Ara: `https://espiralosona.com/` i `"index": true`.
- Com es va passar el domini (7/11/2026): posar el fitxer `CNAME` amb `espiralosona.com`, canviar `publish` a `https://espiralosona.com/` i `"index": true`, i als DNS de Bluehost: A `@` a les 4 IP de GitHub Pages i CNAME `www` → `lespiral.github.io`. El correu (MX) no es toca.
