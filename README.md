#  Map Explorer

Un explorador de mapas web completo, ligero y de un solo archivo, construido con **Leaflet** y APIs abiertas (OpenStreetMap, Nominatim, OSRM). No necesita backend, build ni dependencias: abre el `.html` y funciona.

![Leaflet](https://img.shields.io/badge/Leaflet-1.9.4-199900?logo=leaflet) ![Licencia](https://img.shields.io/badge/licencia-MIT-blue) ![Sin build](https://img.shields.io/badge/build-no%20requerido-success)

---

##  Características

###  Mapa
- **6 capas base**: Mapa, Satélite, Relieve, Oscuro, Claro y Bici (CyclOSM).
- **URL compartible**: la posición (`#zoom/lat/lng`) se actualiza en la barra de direcciones y se restaura al recargar.
- **Vista persistente**: guarda centro y zoom en `localStorage`.
- **Escala métrica** integrada.
- **Pantalla completa**, tema claro/oscuro automático o manual.

###  Búsqueda
- Búsqueda por nombre, dirección o **coordenadas** (`lat, lng`).
- **Historial** de las últimas 6 búsquedas.
- **Categorías cercanas**: 🍽️ restaurantes, ☕ cafeterías, 💊 farmacias, ⛽ gasolineras, 🏨 hoteles, 🏧 cajeros, 🛒 supermercados.
- **Reverse geocoding**: clic en el mapa para obtener la dirección del punto.
- **Clic derecho** → fija el origen de la ruta y avisa.

###  Rutas
- Modos: **🚗 Auto**, **🚴 Bici**, **🚶 A pie**.
- Instrucciones paso a paso traducidas (con giros, rotondas, etc.).
- Cálculo de **tiempo estimado** y **hora de llegada**.
- Botones: **Invertir**, **Desde mi ubicación**, **Borrar**.
- Clic en un paso → vuela a ese punto del recorrido.

###  Ubicación
- Botón **◎** para centrar en tu posición.
- ** Seguimiento en vivo** con círculo de precisión.
- Funciona con `navigator.geolocation` (requiere HTTPS o `localhost`).

###  Guardados
- Guarda lugares favoritos.
- Añade/quita desde la tarjeta del lugar.
- Persistencia en `localStorage`.

###  Medir distancia
- Toca puntos en el mapa para trazar una polilínea y ver la distancia acumulada.
- `Esc` para salir del modo medición.

###  Interfaces intercambiables
Cambia el aspecto completo de la app con un clic:

| Interfaz | Estilo |
|---|---|
| **Map Explorer** | Diseño original |
| **Google Maps** | Bordes rectos, azul `#1a73e8`, tipografía Roboto |
| **Apple Maps** | Cristal esmerilado (`backdrop-filter`), azul `#0a84ff` |
| **Waze** | Cian `#33ccff`, esquinas muy redondeadas, tipografía Nunito |

###  Idiomas
- **Español, English, Português, Français, 日本語**.
- Traducción **completa y reactiva** (incluye textos generados dinámicamente, rutas, toasts, etc.) mediante `MutationObserver`.
- Cambio de idioma sin recargar lógica: se aplica al vuelo.

###  Accesibilidad y atajos
- Navegación con teclado en listas.
- `aria-label` en todos los botones.
- Soporte para `prefers-reduced-motion` y `prefers-color-scheme`.
- Atajos:
  - `/` → enfocar buscador
  - `L` → mi ubicación
  - `M` → medir distancia
  - `+` / `-` → zoom
  - `Esc` → cancelar medición / cerrar

---

##  Uso

### Opción 1: abrir directamente
1. Descarga `index.html`.
2. Ábrelo en el navegador.

>  Algunas funciones (geolocalización, portapapeles) requieren **HTTPS** o **`localhost`**. Para probar en local puedes usar:
> ```bash
> python3 -m http.server 8000
> # o
> npx serve
> ```
> y visitar `http://localhost:8000`.

### Opción 2: clonar el repo
```bash
git clone https://github.com/David4524-maker/map-explorer.git
cd map-explorer
# abre index.html o sirve con tu servidor favorito
```

---

##  Tecnologías

| Componente | Uso |
|---|---|
| [Leaflet 1.9.4](https://leafletjs.com/) | Motor del mapa |
| [Nominatim](https://nominatim.openstreetmap.org/) | Geocodificación / búsqueda |
| [OSRM](https://routing.openstreetmap.de/) | Cálculo de rutas |
| [Esri ArcGIS](https://www.arcgis.com/) | Tiles de mapa base |
| [CyclOSM](https://www.cyclosm.org/) | Tiles para bicicletas |
| Vanilla JS + CSS | Sin frameworks, sin build |

---

##  Estructura

```
map-explorer/
├── index.html   # Todo el proyecto en un solo archivo
└── README.md
```

Sí, todo está en un único HTML: estilos, script y datos. Fácil de copiar, hostear y modificar.

---

## ⌨️ Atajos de teclado

| Tecla | Acción |
|---|---|
| `/` | Buscar |
| `L` | Mi ubicación |
| `M` | Medir distancia |
| `+` | Zoom in |
| `-` | Zoom out |
| `Esc` | Salir de medición / cerrar menús |

---

##  Personalización

### Añadir una capa base
```js
LAYERS.miCapa = ["Mi capa", L.tileLayer("https://.../{z}/{x}/{y}.png", {
  maxZoom: 19,
  attribution: "© …"
})];
```

### Añadir un idioma
1. Añade una fila a `LANGS`:
   ```js
   const LANGS = [["es","Español"],["en","English"], /* … */ ["de","Deutsch"]];
   ```
2. Añade la columna correspondiente en las tablas `D` y `MD` (formato `es~en~pt~fr~ja~de`).

### Añadir una categoría
```js
[["🍕","pizzería"], /* … */].forEach(/* … */);
```

---

##  Limitaciones

- Depende de servicios **públicos y gratuitos** de OSM (Nominatim y OSRM). Respeta sus [políticas de uso](https://operations.osmfoundation.org/policies/nominatim/).
- El enrutado se pide siempre a `/routed-{prof}/route/v1/driving/…` (la URL de OSRM usa `driving` como perfil genérico). El perfil real (`car`, `bike`, `foot`) se pasa en el subdominio.
- Sin Service Worker ni caché offline del mapa.

---

##  Licencia

MIT. Los datos del mapa son © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright).

---

## Otras alternativas

[Google Maps](https://www.google.com/maps)

[Apple Maps](https://maps.apple.com/)

[Waze](https://www.waze.com/es/live-map/)

---

##  Créditos

- Datos: © OpenStreetMap contributors
- Tiles: Esri, HERE, Garmin, USGS, NOAA, CyclOSM
- Motor: Leaflet
- Hecho para explorar el mundo desde el navegador 
