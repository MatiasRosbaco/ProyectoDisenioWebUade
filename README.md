# Estación Federico Lacroze — Sitio Web Informativo

Sitio web estático para la **Estación Federico Lacroze**, el hub multimodal de transporte ubicado en Av. Federico Lacroze 4100, Chacarita, Ciudad Autónoma de Buenos Aires. Desarrollado como proyecto final para la materia **Diseño Web** en la **Universidad Abierta Interamericana (UADE)**.

---

## Descripción general

El sitio centraliza toda la información operativa de la estación en un único portal: medios de transporte disponibles, plano interactivo del edificio, planificador de viajes, servicios internos y datos de contacto. Está orientado a pasajeros que utilizan la terminal como punto de conexión entre el Tren Urquiza, el Subterráneo Línea B y más de 20 líneas de colectivos.

---

## Páginas y funcionalidades

### `index.html` — Inicio
**Tecnologías:** HTML5 · CSS3 · JavaScript (Vanilla ES6+)

- Carrusel de imágenes construido con JavaScript puro: rotación automática cada 4 segundos mediante `setInterval`, botones anterior/siguiente y navegación por puntos. No se usó ninguna librería de carrusel para mantener control total sobre el comportamiento y evitar dependencias.
- Tarjetas de acceso rápido a las secciones principales: Consulta de Viajes, Mapa de la Terminal y Servicios de la Terminal.
- Animación de pulso en el encabezado hero declarada 100% en CSS con `@keyframes`; respeta `prefers-reduced-motion` mediante media query.

### `servicios.html` — Servicios de transporte
**Tecnologías:** HTML5 · CSS3 · Bootstrap 5.3.3

- Listado de los 5 medios de transporte que operan en la estación: Tren Urquiza, Subte Línea B, Colectivos, Taxis y Remises, y Movilidad Sustentable.
- Tarjetas horizontales con imagen, descripción y enlace a la página de detalle de cada servicio. El grid responsivo se maneja con el sistema de columnas de Bootstrap (`col-md-*`), sin JavaScript.

### `consulta-viajes.html` — Consulta de viajes
**Tecnologías:** HTML5 · CSS3 · JavaScript (Vanilla ES6+) · Bootstrap 5.3.3

- Formulario con selector de destino (12 opciones) y franja horaria de salida.
- Panel de resultados dinámico generado con JavaScript puro mediante manipulación del DOM (`innerHTML`, `classList`): muestra medio de transporte recomendado, andén o acceso, tiempo estimado, costo orientativo, advertencia de hora pico y consejos de viaje. Los datos de cada destino están hardcodeados en un objeto JS.
- Sin llamadas a APIs externas; toda la lógica corre en el cliente.
- En mobile, hace scroll automático hasta los resultados con `scrollIntoView()`.

### `mapa.html` — Mapa interactivo de la terminal
**Tecnologías:** HTML5 · CSS3 · SVG · JavaScript (Vanilla ES6+) · Bootstrap 5.3.3

- Plano esquemático completo de la estación dibujado directamente en SVG inline, con fondo cuadriculado estilo blueprint definido en CSS.
- Tooltips implementados con JavaScript puro: se escuchan eventos `mousemove` sobre las zonas SVG, se calculan las coordenadas del cursor y se posiciona el tooltip dinámicamente. Si el tooltip se acerca al borde del viewport, JavaScript lo reposiciona automáticamente para que no se corte.
- Leyenda con código de colores para cada tipo de servicio o área, construida en HTML/CSS puro.
- Sección de "Puntos de Acceso" debajo del mapa con las 3 entradas principales.
- **Accesibilidad:** textos secundarios corregidos de `--muted` (#6B7280) a `--ink-soft` (#3A3A3A), mejorando la relación de contraste de ~4.4:1 a ~9:1 (WCAG AA).

### `servicios-terminal.html` — Servicios internos
**Tecnologías:** HTML5 · CSS3 · JavaScript (Vanilla ES6+) · Bootstrap 5.3.3

- Tarjetas informativas de 6 servicios internos: Baños, Información, Gastronomía, Áreas de espera, Estacionamiento y Wi-Fi gratuito. Diseño en CSS puro.
- Chatbot FAQ construido con JavaScript puro: el sistema compara el input del usuario contra un diccionario de palabras clave y retorna la respuesta correspondiente. Los mensajes se agregan al DOM dinámicamente, el historial hace scroll automático con `scrollTop`, y se diferencia visualmente el mensaje del usuario del del bot con clases CSS. Respuesta de fallback para preguntas no reconocidas.

### `contacto.html` — Contacto
**Tecnologías:** HTML5 · CSS3 · JavaScript (Vanilla ES6+) · Google Maps Embed API

- Formulario de consulta con **validación client-side en JavaScript puro**: campos obligatorios (nombre, apellido, email, mensaje), validación de formato de email con expresión regular, y mínimo de 10 caracteres en el mensaje. Cada error se muestra debajo del campo correspondiente con borde rojo; se limpia automáticamente cuando el usuario empieza a corregirlo.
- Al enviar el formulario correctamente se muestra un **mensaje de éxito visual** (sin envío real al servidor): el formulario se oculta con `hidden` y se muestra un panel de confirmación con ícono SVG. El botón "Enviar otro mensaje" resetea el estado completo.
- **Galería de imágenes** de la estación en grid asimétrico CSS: la imagen principal ocupa toda la altura izquierda (`grid-row: span 2`), y tres fotos secundarias se distribuyen en la columna derecha con la última expandida a ancho completo (`grid-column: span 2`). Colapsa a 2 columnas en mobile.
- Mapa embebido de Google Maps Embed API mostrando la ubicación real de la estación (`<iframe>` sin API key).
- Cards de contacto por servicio (Subte/Tren/CNRT/Ciudad) y **acordeón FAQ** implementado en JavaScript puro: un único ítem puede estar abierto a la vez, el ícono `+` rota 45° con CSS `transform`, el panel se muestra/oculta con `display: block/none`.
- Sección de información de contacto con iconos SVG inline (sin dependencias de icon fonts).

### `servicios/tren-urquiza.html` — Tren Urquiza
**Tecnologías:** HTML5 · CSS3 · Google Maps Embed API

- Estadísticas clave: 26 km de recorrido, 48 minutos de viaje extremo a extremo, 23 estaciones.
- Lista completa de estaciones con distancia desde Lacroze, construida en HTML con tablas semánticas (`<table>`, `<thead>`, `<tbody>`).
- Mapa embebido vía `<iframe>` de Google Maps Embed API para mostrar el recorrido georreferenciado real sin necesidad de una API key.
- Tablas de frecuencias diferenciadas (hora pico, valle, fin de semana) y horarios de ejemplo, todo en HTML/CSS sin JS.
- Sección de accesibilidad con 6 subsecciones.

### `servicios/subte-linea-b.html` — Subte Línea B
**Tecnologías:** HTML5 · CSS3 · SVG · Google Maps Embed API

- Hero con **stats-row**: 17 estaciones · 11,4 km · 23 min · 200.000 pasajeros/día.
- Layout de dos columnas (`content-sidebar`): mapa SVG del recorrido a la izquierda, lista completa de 16 estaciones (con cabeceras marcadas) a la derecha.
- **Mapa real de Google Maps** embebido vía `<iframe>` mostrando la Estación Federico Lacroze, con grid de 4 cards de acceso debajo (dirección, combinaciones, accesibilidad, horario).
- Sección histórica "Viejos de Japón" con ficha técnica de los coches Tokyu (fabricante, años en servicio, apodo) en formato tabla navy.
- Ficha técnica del material CAF Serie 6000 (velocidad máxima, capacidad, accesibilidad PMR).
- Tabla de frecuencias completa: hora pico/valle por tipo de día, con `freq-card` visuales arriba.
- Formas de pago con `feature-grid` de 4 cards (SUBE, SUBE Digital, contactless, billeteras virtuales).

### `servicios/colectivos.html` — Colectivos
**Tecnologías:** HTML5 · CSS3

- Más de 20 líneas de colectivos representadas con badges de colores generados con clases CSS (`span` con estilos de color de fondo).
- Tabla de frecuencias para 5 líneas principales con HTML semántico. Sin JavaScript.

### `servicios/taxis-remises.html` — Taxis y Remises
**Tecnologías:** HTML5 · CSS3

- Descripción de las 3 paradas de taxis, tabla de tarifas y listado de aplicaciones, todo en HTML/CSS estático.
- Alertas de seguridad con estilos CSS destacados (`border-left` de color, fondo suave). Sin JavaScript.

### `servicios/movilidad-sustentable.html` — Movilidad Sustentable
**Tecnologías:** HTML5 · CSS3

- Información básica sobre el punto de anclaje de EcoBici y monopatines eléctricos próximos a la estación. Página estática, sin JavaScript.

---

## Tecnologías utilizadas

| Tecnología | Versión | Uso y motivo |
|---|---|---|
| **HTML5** | — | Estructura semántica de todas las páginas. Se usan etiquetas como `<nav>`, `<main>`, `<section>`, `<article>` y `<figure>` para favorecer la accesibilidad y el SEO. |
| **CSS3** | — | Diseño completo del sitio mediante un único archivo `css/style.css`. Se usan variables CSS (`--navy`, `--yellow`, etc.) para mantener coherencia visual y facilitar cambios globales. |
| **JavaScript (Vanilla)** | ES6+ | Lógica del carrusel, tooltips del mapa, planificador de viajes y chatbot. Se eligió JavaScript sin frameworks para mantener el sitio liviano y sin dependencias innecesarias. |
| **Bootstrap** | 5.3.3 | Grid system y utilidades de layout en las páginas de servicios, mapa y consulta. Se incorpora vía CDN para no agregar archivos al repositorio. |
| **Google Fonts** | — | Tres tipografías: **Fraunces** (display/títulos, serif con personalidad), **DM Sans** (cuerpo e interfaz, legibilidad en pantalla) y **JetBrains Mono** (datos, tablas y horarios, claridad en contenido tabulado). |
| **SVG** | — | Plano interactivo de la estación (`mapa.html`) y mapa de ruta del Subte Línea B. SVG permite escala sin pérdida de calidad y manipulación desde JavaScript. |
| **Google Maps Embed** | — | Mapa embebido en la página del Tren Urquiza para mostrar el recorrido georreferenciado real. |

### Sistema de diseño

El archivo `css/style.css` define un sistema de diseño completo con:

- **Variables de color:** `--navy` (#1A2940), `--yellow` (#F4B842), `--cream` (#FAF6EF), `--red` (#C8102E), `--green` (#4A7C59).
- **Escala tipográfica** coherente en títulos, subtítulos y cuerpo.
- **Componentes reutilizables:** tarjetas con borde superior de color y efecto hover, tablas con encabezado navy y filas alternadas, alertas, badges de línea y botones.
- **Animaciones declaradas en CSS:** pulso en el hero, transiciones de hover (0.2 s–0.5 s) y efectos de elevación en tarjetas.

---

## Accesibilidad

- Etiquetas `aria-label` y `aria-live` en el mapa interactivo y el chatbot.
- Atributos `alt` en todas las imágenes.
- Soporte para `prefers-reduced-motion`: la animación de pulso del hero se desactiva si el usuario lo configura en el sistema operativo.
- Contraste de color revisado: textos secundarios en el mapa y contacto corregidos para superar la relación mínima de 4.5:1 exigida por WCAG AA. Los textos decorativos de baja opacidad en el SVG del mapa son intencionales (fondo, no contenido).
- Tipografía monoespaciada (`JetBrains Mono`) para datos numéricos y horarios, mejorando la legibilidad de tablas.
- Estructura de encabezados jerárquica (`h1` → `h2` → `h3`) en todas las páginas.

---

## Estructura del proyecto

```
proyectoDisenioWebUade/
├── index.html                     Página de inicio con carrusel
├── servicios.html                 Listado de medios de transporte
├── consulta-viajes.html           Planificador de viajes interactivo
├── mapa.html                      Plano SVG interactivo de la terminal
├── servicios-terminal.html        Servicios internos + chatbot FAQ
├── contacto.html                  Datos de contacto
│
├── css/
│   └── style.css                  Sistema de diseño completo
│
├── servicios/
│   ├── tren-urquiza.html          Detalle del Tren Urquiza
│   ├── subte-linea-b.html         Detalle del Subte Línea B
│   ├── colectivos.html            Detalle de líneas de colectivos
│   ├── taxis-remises.html         Detalle de taxis y remises
│   └── movilidad-sustentable.html Detalle de EcoBici y monopatines
│
└── img/
    ├── terminal.jpg
    ├── trenUrquiza.jpg
    ├── subteLineaB.jpg
    ├── LineaBViejosJapon.jpg
    ├── NuevaLineaSubteB.webp
    ├── ViejoSubteB.jpg
    ├── ColectivoLacroze.jpg
    ├── colectivo-42.jpg
    ├── recorrido-65.jpg
    ├── mapa-paradas.jpg
    ├── TaxisLacroze2.jpg
    ├── BiciPublica.jpg
    └── Línea_B_del_Subte_de_Buenos_Aires.svg
```

---

## Cómo visualizar el sitio

Al ser un sitio 100 % estático, basta con abrir `index.html` en cualquier navegador moderno. No requiere servidor, base de datos ni instalación de dependencias.

Para evitar problemas con rutas relativas al abrir archivos directamente desde el sistema de archivos, se recomienda usar una extensión como **Live Server** en VS Code.

---

## Autores

Proyecto desarrollado por estudiantes de la **Universidad Abierta Interamericana (UADE)** para la materia Diseño Web.
