# 🥁 Batería Digital

**Emulador de batería profesional — vista del baterista — multi-touch — sin dependencias**

> Un kit de batería completo que corre en cualquier navegador móvil o de escritorio. Sin instalación, sin frameworks, sin archivos de audio externos. Todo el sonido se sintetiza en tiempo real con Web Audio API.

---

## Demo

Abrí `fateria.html` directamente en el navegador. No necesita servidor.

---

## Características

### Interfaz
- **Vista POV del baterista** — perspectiva top-down como si estuvieras sentado detrás del kit, igual que en una sesión real.
- **Gráficos SVG vectoriales** generados dinámicamente: parches con aros cromados y pernos de tensión, platillos con campana, acanaladuras y reflejos dorados.
- **Pedales en la fila inferior** — pedal de bombo (centro) y pedal de hi-hat (izquierda), posicionados como en una batería real.
- Layout adaptable al ancho de pantalla, responsive.

### Sonido
- **Motor de audio 100% Web Audio API** — síntesis en tiempo real, sin archivos `.mp3` ni `.wav`.
- Cada pieza tiene su propia cadena de síntesis:
  - **Bombo**: oscilador sinusoidal con pitch-bend descendente + transitorio de click de ruido blanco.
  - **Caja**: oscilador triangular + ruido blanco filtrado con highpass (1.8 kHz).
  - **Hi-Hat cerrado/abierto/pedal**: ruido blanco con highpass alto (6–7.5 kHz), distintos envelopes.
  - **Crash / Splash / China**: ruido bandpass + oscilador de shimmer, con reverb.
  - **Ride / Ride Bell**: oscilador sinusoidal de campana + wash de ruido.
  - **Toms / Floor Tom**: oscilador sinusoidal con pitch-bend, frecuencia y decay según tamaño.
  - **Cowbell**: dos osciladores cuadrados detuneados (562 Hz + 845 Hz).
  - **Clap**: tres capas de ruido bandpass con micro-delay entre ellas.
- **Compresor dinámico global** en la cadena de salida.
- **Reverb convolution** sintético (impulse response generado por código).

### Multi-touch
- Acepta **toques simultáneos ilimitados** — podés golpear bombo, caja y platillo al mismo tiempo con distintos dedos.
- `touchstart` con `preventDefault()` en cada pad para evitar delay de 300 ms en iOS/Android.
- Funciona con mouse para testing en escritorio.

### Grabación y reproducción
- **⏺ REC** — graba todo lo que tocás con timestamps de precisión de milisegundos (`performance.now()`).
- **▶ PLAY** — reproduce la grabación con timing exacto, animando los pads visualmente mientras suena.
- **Waveform display** — mini visualización de los eventos grabados, con playhead animado durante la reproducción.
- **⏹ STOP** y **🗑 borrar** sesión.

### Shop — Kit Builder
- **Pestaña PRESETS**: 5 kits prediseñados listos para usar.
- **Pestaña PLATILLOS**: catálogo de 8 platillos seleccionables.
- **Pestaña TAMBORES**: catálogo de 13 piezas (cajas, toms, bombos, percusión).
- **Pestaña MI KIT**: armás tu batería slot por slot — elegís qué va en platillos traseros, frontales, toms, caja y bombo. Toca cualquier ítem para preescucharlo antes de agregarlo.

---

## Piezas disponibles

### Platillos
| ID | Nombre | Descripción |
|---|---|---|
| `hihat` | Hi-Hat 14" | Cerrado, sonido clásico |
| `hihat_open` | Hi-Hat Abierto | Sustain largo |
| `crash` | Crash 18" | Crash estándar |
| `crash2` | Crash 16" | Bright, corto |
| `splash` | Splash 10" | Pequeño, brillante |
| `china` | China 18" | Trashy, agresivo, distorsionado |
| `ride` | Ride 20" | Ride clásico con wash |
| `ride_bell` | Ride Bell | Acento de campana |

### Tambores
| ID | Nombre | Frecuencia base |
|---|---|---|
| `snare` | Snare 14" | 200 Hz → 100 Hz |
| `snare2` | Snare Fat | 160 Hz → 78 Hz |
| `snare3` | Rimshot | 900 Hz → 280 Hz |
| `tom1` | Tom 10" | 265 Hz → 122 Hz |
| `tom2` | Tom 12" | 202 Hz → 92 Hz |
| `tom3` | Tom 14" | 162 Hz → 76 Hz |
| `floortom` | Floor Tom 16" | 112 Hz → 56 Hz |
| `floortom2` | Floor Tom 18" | 90 Hz → 46 Hz |
| `kick` | Bass Drum 22" | 150 Hz → 42 Hz |
| `kick2` | Bass Drum Punch | 185 Hz → 50 Hz |
| `cowbell` | Cowbell | 562 + 845 Hz |
| `clap` | Clap | 1200 Hz bandpass × 3 |
| `tambourine` | Tamboril | Highpass 8200 Hz |

---

## Kits prediseñados

| Preset | Descripción |
|---|---|
| **Estándar** | Rock clásico — ride, crash × 2, toms, snare, bombo |
| **Jazz** | Ride frontal, un crash, toms reducidos, feel ligero |
| **Metal** | China, doble crash, toms completos, snare fat, kick punch |
| **Electrónico** | Hi-Hat abierto, splash, rimshot, clap, kick punch |
| **Minimalista** | Solo lo esencial — hi-hat, crash, 2 toms, snare, bombo |

---

## Atajos de teclado (desktop)

| Tecla | Pieza |
|---|---|
| `Espacio` / `N` | Bombo |
| `J` | Caja |
| `F` | Hi-Hat |
| `G` | Hi-Hat Pedal |
| `C` | Crash |
| `V` | Crash 2 |
| `B` | Ride |
| `Q` | Tom 1 |
| `W` | Tom 2 |
| `E` | Tom 3 |
| `R` | Floor Tom |
| `H` | Cowbell |

---

## Estructura del proyecto

```
fateria/
├── fateria.html      # Todo el proyecto — HTML + CSS + JS en un solo archivo
└── README.md
```

No hay dependencias externas en tiempo de ejecución. Las únicas peticiones de red son las fuentes de Google Fonts (`Bebas Neue` y `Rajdhani`) — si no hay conexión, el navegador usa fuentes del sistema como fallback sin romper nada.

---

## Compatibilidad

| Plataforma | Estado |
|---|---|
| Android (Chrome) | ✅ Óptimo |
| iOS (Safari) | ✅ Funciona — requiere primer toque para activar AudioContext |
| Desktop (Chrome, Firefox, Edge) | ✅ Completo con teclado |
| WebView Android | ✅ Apto para APK via WebView |

### Notas de iOS
Safari requiere que el `AudioContext` se reactive en respuesta a un gesto del usuario. La app lo maneja automáticamente en el primer `touchstart`.

### Empaquetado como APK
El archivo es compatible con WebView de Android. Puede ser empaquetado directamente con cualquier wrapper de WebView (Capacitor, una Activity WebView nativa, etc.) apuntando a `fateria.html` como `file:///android_asset/`.

---

## Arquitectura interna

### Audio Engine
```
Pads / Pedales
     │
     ▼
  SND[sound]()          ← síntesis específica por instrumento
     │
     ▼
  master (GainNode)
     │
     ▼
  comp (DynamicsCompressor)
     │
     ▼
  AC.destination
     │
     └──→ reverb (ConvolverNode) ──→ wet GainNode ──→ master
```

### Render del Kit
El layout se regenera completamente con `renderKit()` cada vez que se aplica un preset o se cambia el kit desde el Shop. Los SVGs de cada pieza se generan en JS con funciones parametrizadas (`cymbalSVG`, `tomSVG`, `kickSVG`, etc.) que reciben tipo y tamaño, escalan al ancho disponible y son responsivos.

### Recording
Los eventos se guardan como `{t: DOMHighResTimeStamp, s: soundId}`. La reproducción usa `setTimeout` con el delta `t` original respecto al inicio de la sesión, garantizando el timing exacto independientemente de la velocidad del render.

---

## Créditos

Construido por **NMFT Studio** — nmft.ar  
Valle de Calamuchita, Córdoba, Argentina

Vanilla HTML · CSS · JS — sin frameworks, sin build step, sin dependencias.
