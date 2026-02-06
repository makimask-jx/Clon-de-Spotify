# Documentación Técnica: Clon de Spotify

Este documento detalla las decisiones arquitectónicas y técnicas tomadas durante el desarrollo de la interfaz de este clon de Spotify.

## 1. Estructura del HTML

La estructura se divide en bloques semánticos claros para facilitar el mantenimiento y la accesibilidad:

- **`<aside>` (Sidebar)**: Contiene la navegación principal y la biblioteca del usuario. Está fijado a la izquierda.
- **`<main>` (Contenido Principal)**: El área central que permite scroll independiente. Incluye el encabezado (`header`) y las secciones de música.
- **`<header>`**: Dentro de `<main>`, contiene la navegación retroceder/avanzar y los botones de autenticación.
- **`.bottom-banner`**: El pie de página promocional que invita al registro.

## 2. Flexbox vs. CSS Grid: ¿Por qué y dónde?

Hemos alternado entre estas dos herramientas potentes basándonos en la naturaleza del layout:

### CSS Grid (Diseño 2D)
Se utilizó **Grid** principalmente para el catálogo de música (`.card-grid`).
- **Razón**: Necesitábamos una alineación perfecta tanto en filas como en columnas. Grid nos permite definir cuántos elementos caben por fila de forma sencilla y gestionar los espacios (`gap`) de manera uniforme.
- **Caso Crítico**: Gracias a `grid-template-columns`, pudimos implementar la "expansión de dominio" (density expansion) para pasar de 2 a 8 columnas de forma fluida mediante Media Queries.

### Flexbox (Diseño 1D)
Se utilizó **Flexbox** para componentes alineados en un solo eje o con comportamiento elástico:
- **Sidebar (`.sidebar-section`)**: Para alinear iconos y texto horizontalmente.
- **Encabezado (`header`)**: Para separar los controles de navegación (izquierda) de los botones de login (derecha) usando `justify-content: space-between`.
- **Cabeceras de sección (`.section-header`)**: Para mantener el título ("Canciones en tendencia") y el enlace ("Mostrar todo") en la misma línea.

## 3. Estrategia de Diseño Responsivo

El objetivo principal fue alcanzar la **alta densidad visual** oficial de Spotify:
- **Breakpoints**: Definimos puntos de corte agresivos (768px, 1024px, 1280px, 1440px, 1600px) para ajustar el número de columnas de la rejilla.
- **Ajuste de Tarjetas**: A medida que la pantalla se ensancha, las tarjetas se reducen ligeramente en relleno (`padding: 6px`) para permitir que las imágenes sean más pequeñas y quepan más elementos sin abarrotar la vista.

## 4. Estética y Tipografía
- **Fuente**: Se eligió `Montserrat` (Google Fonts) como reemplazo de la fuente propietaria de Spotify, ya que ofrece un peso y una legibilidad geométrica muy similar.
- **Colores**: Uso intensivo de variables CSS (`--spotify-negro`, `--spotify-gris-tarjeta`) para mantener consistencia en el "Dark Mode".
- **Imágenes**: Uso de Unsplash con parámetros de optimización (`w=300&auto=format`) para garantizar que la carga sea rápida a pesar de la alta cantidad de elementos.
