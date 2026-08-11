# Dojo de Karate 🥋

Juego para aprender vocabulario de karate (estilo Shotokan básico) al estilo del
juego de banderas de Encarta: cuatro opciones, **verde** si aciertas, **rojo**
si fallas (mostrándote la correcta). Tú controlas el ritmo con el botón
**Siguiente**, así puedes leer con calma el kanji y la nota de cada término.

Diseño moderno y amigable: paleta cálida (coral, menta, crema) e ilustraciones
tiernas estilo chibi dibujadas como SVG dentro del propio archivo — sin imágenes
descargadas, sin licencias, 100% offline.

## Cómo jugar

Doble clic en `index.html` (o desde la terminal):

```sh
open index.html
```

No necesita internet, servidor ni instalación: es un único archivo HTML sin
dependencias externas.

## Desde el móvil

El diseño es **mobile-first**: las reglas base del CSS son las del teléfono y el
layout de dos columnas del escritorio empieza en `@media (min-width: 761px)`.

- Una opción por fila, objetivos táctiles de 54 px y sin efectos `:hover`
  (se quedan pegados en pantallas táctiles: van dentro de `@media (hover: hover)`).
- El botón **Siguiente** flota fijo al alcance del pulgar mientras se muestra la
  corrección — abajo a lo ancho en vertical, abajo a la derecha en horizontal.
- Cada pregunta vuelve arriba sola; la corrección se desplaza sola a la vista.
- Respeta el notch y la barra de inicio (`env(safe-area-inset-*)`), no se dispara
  el "tirar para recargar" a mitad de sesión y no hay zoom por doble toque.
- El plan de cinturones pasa debajo del panel, en rejilla de dos columnas.
- Añádelo a la pantalla de inicio y se abre a pantalla completa, como una app.

### Publicarlo como página

El `index.html` es el original completo y offline. Para publicarlo hay que quitar
las etiquetas que pone el propio host (`<!DOCTYPE>`, `<html>`, `<head>`, `<body>`):

```sh
node -e 'const fs=require("fs");const s=fs.readFileSync("index.html","utf8");
fs.writeFileSync("dojo-karate.html", s.split("\n").filter(l=>
  !/^\s*(<!DOCTYPE html>|<html[^>]*>|<\/?head>|<\/?body>|<\/html>)\s*$/i.test(l)).join("\n"))'
```

## Plan de cinturones (100 términos)

Cada cinturón de la barra lateral contiene **los conocimientos que debe tener
un karateka de ese grado** — tócalo para practicarlo (sesiones de hasta 12
preguntas, priorizando lo que te falta):

| Cinturón | Grado | Qué se aprende |
|---|---|---|
| Blanca | 10.º kyū | Etiqueta (rei, osu, seiza…), números 1–10, direcciones (mae/yoko/ushiro), tsuki/geri/uke genéricos, dōjō kun, primer kata, musubi-dachi, choku-zuki |
| Amarilla | 9.º kyū | Zenkutsu, kiba, heisoku · oi-zuki, age-uke, gedan-barai, mae-geri · kihon, kiai, jōdan/chūdan/gedan, seiken, Heian Shodan |
| Naranja | 8.º kyū | Kōkutsu · soto/uchi-uke · gyaku-zuki, yoko-geri · kata, kumite, hidari/migi · te, ashi, hiza |
| Verde | 7.º kyū | Shutō-uke · kizami-zuki, uraken, mawashi-geri · sempai/kohai, waza, kyū/dan · hara, koshi, atama |
| Azul | 6.º–5.º kyū | Morote-uke · empi, tettsui · ushiro-geri, hiza-geri · neko-ashi, shiko · kamae, kubi, kakato, sokutō |
| Morada | 4.º–3.er kyū | Jūji-uke · shutō-uchi · mikazuki, fumikomi · bunkai, kime, hikite, onegai shimasu |
| Marrón | 2.º–1.er kyū | Sanchin · nukite · tobi-geri · zanshin, maai, kokoro, arigatō, otagai ni rei |
| Negra | Dan | **Examen final**: 15 preguntas mezclando todos los cinturones |

En las ilustraciones de técnicas, el personaje chibi lleva el cinturón del
grado en el que se aprende esa técnica. 🎀

## Otros modos

- **⚡ Sesión rápida** — 10 preguntas de todo, priorizando lo que fallas o no has visto.
- **🔁 Reforzar fallos** — solo los términos que has fallado y aún no dominas.
- **🌊 Maratón** — los 100 términos, uno por uno.

## Progreso y refuerzo

- El progreso se guarda en el navegador (`localStorage`), por navegador y máquina.
- Un término se considera **dominado** con 2 aciertos seguidos.
- Las sesiones ponderan los términos: los fallados y los nunca vistos aparecen
  con más frecuencia (repetición de refuerzo).
- **🗑️ Borrar progreso** (arriba a la derecha) reinicia todo.

## Atajos de teclado

- `1–4` o `A–D`: responder
- `Enter` / `Espacio`: siguiente pregunta
- `Esc`: volver al menú

## Añadir o editar términos

Edita el array `TERMS` dentro de `index.html`. Cada entrada:

```js
{ id:'maegeri', grade:'amarilla', cat:'geri', jp:'Mae-geri', kanji:'前蹴り',
  es:'Patada frontal', note:'Impacta con la bola del pie.', art: kickFig({...}) }
```

`grade` es el cinturón cuyo plan incluye el término; `cat` es el tema (se usa
para elegir opciones incorrectas verosímiles). `art` es opcional (helpers:
`artKanji`, `artFeet`, `chibiTorso`, `kickFig`).
