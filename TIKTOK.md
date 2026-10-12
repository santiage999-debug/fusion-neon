# FUSIÓN NEÓN en TikTok LIVE (guía rápida)

Los regalos del público activan efectos en el juego. Puedes hacerlo de dos formas:
**A) Teclas** (lo más sencillo) o **B) Conexión directa con TikFinity** (modo `?tikfinity=1`).

> Los nombres de menús de TikFinity / TikTok LIVE Studio / OBS cambian con las versiones.
> Revisa los nombres exactos en tu versión; aquí se describen de forma general.

## 1. Abrir el juego con un servidor local
Las imágenes y sonidos se cargan mejor desde un servidor (no con doble clic en el archivo):

```
cd carpeta-del-juego      (donde están index.html, img/ y snd/)
python -m http.server 8000
```
Abre: `http://localhost:8000/index.html?live=1`
(`?live=1` activa el **Modo Directo**: leyenda de regalos abajo, feed de eventos, botones discretos.
También puedes activarlo con el botón **📺 Modo Directo**.)

Formato recomendado: vertical **9:16** (p. ej. 1080×1920 o 720×1280).

## 2. Ponerlo en el directo
- **TikTok LIVE Studio**: añade una fuente tipo *Captura de ventana* (o *Enlace/Link* si tu versión lo tiene) apuntando a la ventana del navegador con el juego.
- **OBS**: añade una fuente **Navegador** (Browser Source) con la URL de arriba, tamaño 1080×1920.
  Para que funcionen las **teclas** necesitas que la ventana del navegador tenga el foco; con *Fuente de navegador* de OBS es mejor usar la opción B (TikFinity WebSocket) o el modo *Interactuar* de OBS.

## Opción A — TikFinity enviando teclas
1. Instala TikFinity (tikfinity.zerody.one) y conéctalo a tu usuario de TikTok.
2. Ve a **Actions & Events** (Acciones y eventos) → crea una **acción** por efecto con *Simulate Keystroke / Pulsar tecla*.
3. Crea **eventos**: *Gift* (regalo concreto) → la acción correspondiente.
4. Deja la ventana del navegador del juego enfocada (TikFinity envía la tecla a la ventana activa).

| Tecla | Efecto | Regalo sugerido |
|---|---|---|
| 1 | 🌧️ Lluvia de bolas (10-15 bolitas) | 🌹 Rose |
| 2 | 🟣 Bola gigante | 🎁 Otros regalos |
| 3 | 🌋 Modo LAVA (10 s, el suelo quema) | 🌌 Perfume / Galaxy |
| 4 | 🌍 Terremoto | 🫰 Finger Heart |
| 5 | 🪐 Gravedad loca (5 s) | 🍩 Doughnut |
| 6 | 🎨 Cambio de tema | 💌 Heart Me |
| 7 | 💣 Bomba | 🫶 Hand Hearts |
| 8 | ✨ Fusión mágica | 🎮 GG |
| 9 | 🧊 Congelar (5 s) | 🍦 Ice Cream |
| 0 | 🗿 Bola meme sorpresa | 🎵 TikTok |
| - | ☢️ SÚPER LAVA (la lava sube, derrite casi todas las bolas y el progreso del nivel vuelve a 0) | 🦁 Lion / Universe |

## Cola y tiempos de espera (anti-spam)
Los regalos no se ejecutan todos a la vez: entran en una **cola** (máx. 20) y se ejecutan **de uno en uno cada ~3,5 s**.
Regalos iguales seguidos se **agrupan** (p. ej. "Rose x11" = una sola lluvia). Cada efecto tiene su propio enfriamiento:
lluvia 8 s · bola gigante 8 s · lava 10 s · terremoto 5 s · gravedad 8 s · tema 10 s · bomba 6 s · fusión mágica 15 s · congelar 8 s · meme 5 s · súper lava 25 s.
En Modo Directo la leyenda muestra ✅ (listo) o ⏳ segundos restantes y cuántos hay en cola.
Además, las fusiones provocadas por regalos dan menos puntos durante unos segundos y ningún nivel se puede pasar en sus primeros 20 s.

## Opción B — Conexión directa con TikFinity (sin teclas)
TikFinity ofrece un WebSocket local (por defecto `ws://localhost:21213/`; verifica en su configuración que la API/WebSocket esté activada).
Abre el juego con:

`http://localhost:8000/index.html?tikfinity=1`

- Regalos → efecto según la tabla de arriba (nombre del regalo en inglés, sin importar mayúsculas). Los combos solo cuentan al terminar la racha.
- Cada ~15 likes → cae una bolita. Follow / Share → mini-celebración.
- Abajo a la derecha verás 🟢 conectado / 🔴 reconectando (se reconecta solo).

Cambiar el mapeo por URL: `&map=Rose:lava,Lion:bomba,Galaxy:lluvia`
Acciones válidas: `lluvia, gigante, lava, terremoto, gravedad, tema, bomba, fusion, congelar, meme, superlava`.

## Opción C — Tu propio WebSocket
`?ws=ws://localhost:PUERTO` y envía JSON: `{"action":"lava","user":"pepito","gift":"Rose"}`
(o mensajes con formato TikFinity `{"event":"gift","data":{"giftName":"Rose","nickname":"Pepito"}}`).

## Otros parámetros
- `?level=N` empieza en el nivel N. Cada nivel combina tema, física (luna, agua, hielo, viento, imán, giratorio…), forma del recipiente y obstáculos.
- `#test` activa el modo Auto al cargar.

## 🌍 Mundos: efectos por mundo
En los mundos nuevos (menú ☰ → 🌍 Mundos) las mismas teclas/regalos hacen efectos propios de cada mundo. Todos usan la misma cola y tiempos de espera. El panel "Probar regalos" muestra los nombres del mundo activo. **SÚPER LAVA** reinicia el progreso del nivel actual del mundo. Tocar la pantalla también interactúa (dominó: derriba el más cercano · duplicación: suelta una bola · bucles: empuja las bolas · extraño: perturba el patrón).

| Tecla | Regalo | Dominós | Duplicación al vacío | Bucles | Algo extraño |
|---|---|---|---|---|---|
| 1 | 🌹 Rosa | 👉 Empujón x3 | 🌧️ Lluvia de bolas | ⚪ +3 bolas | ✨ Chispas |
| 2 | 🎁 Otros regalos | 🟨 Dominó gigante | ✖️ Puerta x5 | ⭕ Nuevo anillo | 🔀 Siguiente patrón |
| 3 | 🌌 Perfume / Galaxy | 🔥 Dominós de fuego | 🔥 Portal x3 | 🔥 Bola de fuego | 🔥 Colores fuego |
| 4 | 🫰 Finger Heart | 🌋 Terremoto | 🌋 Sacudida | 🌀 Giro loco | 🌪️ Caos |
| 5 | 🍩 Doughnut | 🐢 Cámara lenta | 🙃 Antigravedad | 🪐 Sin gravedad | ⏪ Reversa |
| 6 | 💌 Heart Me | 🎨 Nuevo diseño | 🎨 Nuevo tablero | 🎨 Nuevos colores | 🎨 Paleta nueva |
| 7 | 🫶 Hand Hearts | 💣 Bomba | 🕳️ Agujero negro | 💥 Romper anillo | 💥 Explosión |
| 8 | 🎮 GG | ⛓️ Reacción en cadena | ➗ Duplicar todo | 🚪 Hueco gigante | 🎯 Sincronizar |
| 9 | 🍦 Ice Cream | 🧊 Congelar | 🧊 Congelar | 🧊 Congelar anillos | 🧊 Congelar |
| 0 | 🎵 TikTok | 🌈 Arcoíris | 🟡 Bola dorada x10 | 🔴 Bola gigante | ⚡ Turbo |
| - | 🦁 Lion / Universe | 🌋 SÚPER LAVA: reinicia nivel | 🌋 SÚPER LAVA: reinicia nivel | 🌋 SÚPER LAVA: reinicia nivel | 🌋 SÚPER LAVA: reinicia nivel |

Cada mundo tiene niveles casi infinitos: puntos propios, meta que crece en cada nivel y variaciones (diseños, colores, velocidades, obstáculos, número de anillos). El progreso se guarda en el dispositivo.
