# Catálogo de Productos - Arquitectura y Evolución CSS
**Centro Industrial de Mantenimiento Integral - SENA**  
**Programa de Formación:** Análisis y Desarrollo de Software (ADSO)  
**Ficha:** 3234206  
**Instructor - Tutor:** John Freddy Becerra Castellanos  

---

## 📌 Visión General del Proyecto
Este repositorio documenta el ciclo de vida, desarrollo y refactorización técnica de una interfaz web para un **Catálogo de Productos gastronómicos**. A través de un flujo estructurado de control de versiones con **Git**, el proyecto evoluciona desde una estructura semántica básica hasta una arquitectura modular profesional con especificidad plana (**BEM**) y layouts elásticos unidimensionales modernos (**Flexbox**).

---

## 🌳 Mapa Arquitectónico de Ramas (Git Flow)

```text
[main] ────────────────────────────────────────────────────────────────────────► (Documentación y producción)
  │
  ├──► [develop]                     (Estructura semántica HTML5 y jerarquía CSS base)
  │
  ├──► [feature/modelo-caja]         (Subactividad 3: Box Model, box-sizing y espaciados)
  │
  ├──► [feature/identidad-visual]    (Subactividad 4A: Custom Properties :root y consistencia)
  │
  ├──► [feature/interactividad-css]  (Subactividad 4B: Pseudoclases :hover/:focus y ::before/::after)
  │
  ├──► [feature/arquitectura-bem]    (Subactividad 5: Modularización física @import y clases BEM)
  │
  └──► [feature/arquitectura-flexbox] (Subactividad 6: Macro-layout, sticky footer y resorte elástico)
```

### Tabla Resumen de Ramas

| Rama | Subactividad | Objetivo Técnico Central | Estado / Criterio de Aprobación |
| :--- | :--- | :--- | :--- |
| `main` | Global | Rama raíz de entrega y documentación centralizada del sistema. | Limpia, contiene documentación maestra. |
| `develop` | Inicial | Maquetación HTML5 semántica y jerarquía base de selectores. | Estructura semántica sin etiquetas de diseño obsoletas. |
| `feature/modelo-caja` | Subactividad 3 | Control de dimensiones físicas con `box-sizing: border-box`. | Eliminación de desbordamientos y colapso de márgenes. |
| `feature/identidad-visual` | Subactividad 4A | Estandarización de variables en `:root` (Design Tokens). | Cero valores mágicos; paleta y escalas centralizadas. |
| `feature/interactividad-css` | Subactividad 4B | Estados de interacción (`:hover`, `:focus`) y decoración (`::before`, `::after`). | Accesibilidad por teclado y marcado HTML limpio. |
| `feature/arquitectura-bem` | Subactividad 5 | Modularidad física con `@import` y sintaxis BEM estricta. | Especificidad plana de peso 10; archivos desacoplados en `css/`. |
| `feature/arquitectura-flexbox` | Subactividad 6 | Construcción de layouts unidimensionales elásticos y simétricos. | Sticky footer (`min-height: 100vh`) y alineación con `flex-grow: 1`. |

---

## 🛠️ Documentación Detallada de Cada Rama

```
================================================================================
RAMA 1: develop
================================================================================
```
* **Propósito:** Servir como entorno de integración inicial para el marcado semántico y estilos base.
* **Comandos Git utilizados:**
  ```bash
  git checkout -b develop
  git add .
  git commit -m "feat(styles): maquetar catalogo semantico y aplicar jerarquia CSS"
  ```
* **Archivos intervenidos:** `index.html`, `style.css`.
* **Conceptos técnicos aplicados:**
  - Uso estricto de etiquetas semánticas de HTML5: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`.
  - Atributos de accesibilidad: `aria-label` para regiones de navegación y listas de productos, `aria-current="page"` para el enlace activo.
  - Reset básico de márgenes y tipografía de herencia global.
* **¿Qué se hizo bien? (Criterio de validación):** Se eliminó el uso de `<div>` sin semántica para estructurar la página, permitiendo a los motores de búsqueda y tecnologías de asistencia identificar las áreas clave de la aplicación.

```
================================================================================
RAMA 2: feature/modelo-caja (Subactividad 3)
================================================================================
```
* **Propósito:** Comprender y controlar el cálculo matemático de las dimensiones físicas en los navegadores.
* **Comandos Git utilizados:**
  ```bash
  git checkout -b feature/modelo-caja
  git add .
  git commit -m "feat(ui): implementar modelo de caja y backgrounds"
  ```
* **Archivos intervenidos:** `style.css`, `index.html`, carpeta `img/`.
* **Conceptos técnicos aplicados:**
  - **`box-sizing: border-box`:** Aplicado en el selector universal `*` para que el `padding` y el `border` se resten hacia adentro de las dimensiones declaradas (`width` y `height`), evitando que la caja aumente su tamaño físico y desborde el layout.
  - **Diferenciación espacial:** Implementación de `padding: 40px` como espacio interno entre contenido y borde del artículo, y `margin: 80px` como separación exterior entre artículos hermanos.
  - **Fondos e imágenes:** `background-image: url("img/header.jpg"); background-size: cover; background-position: center;` garantizando cobertura simétrica y responsiva en la cabecera.
* **¿Qué se hizo bien? (Criterio de validación):** El catálogo no genera desbordamientos horizontales ni colapsos indeseados, y cada artículo preserva su área física sin deformar la rejilla.

```
================================================================================
RAMA 3: feature/identidad-visual (Subactividad 4 - Parte 1)
================================================================================
```
* **Propósito:** Centralizar la identidad visual eliminando "valores mágicos" (números o colores quemados en el código).
* **Comandos Git utilizados:**
  ```bash
  git checkout -b feature/identidad-visual
  git add .
  git commit -m "refactor(styles): estandarizar colores, tipografia y espaciados con custom properties"
  ```
* **Archivos intervenidos:** `style.css`.
* **Conceptos técnicos aplicados:**
  - **Declaración en `:root`:**
    ```css
    :root {
        --color-principal: rgb(140, 255, 0);
        --color-secundario: rgb(0, 180, 18);
        --color-terciario: rgb(70, 130, 70);
        --color-fondo: rgb(250, 255, 255);
        --color-texto: rgb(13, 13, 13);
        --fuente-pequena: 14px;
        --fuente-mediana: 16px;
        --fuente-grande: 32px;
        --fuente-principal: 'Roboto', sans-serif;
        --espaciado-pequeno: 8px;
        --espaciado-medio: 16px;
        --espaciado-grande: 24px;
    }
    ```
  - **Consumo de variables:** `var(--color-principal)`, `var(--fuente-principal)`, etc.
* **¿Qué se hizo bien? (Criterio de validación):** Toda la identidad visual quedó desacoplada; cambiar un color de marca en el `:root` actualiza de forma instantánea y coherente todo el sitio web.

```
================================================================================
RAMA 4: feature/interactividad-css (Subactividad 4 - Parte 2)
================================================================================
```
* **Propósito:** Implementar interactividad visual de alta fidelidad, accesibilidad por teclado y decoración visual pura.
* **Comandos Git utilizados:**
  ```bash
  git checkout -b feature/interactividad-css
  git add .
  git commit -m "feat(ui): implementar pseudoclases interactivas en aside y pseudoelementos en productos"
  ```
* **Archivos intervenidos:** `style.css`.
* **Conceptos técnicos aplicados:**
  - **Pseudoclases dinámicas:**
    - `.btn-comprar:hover`: Transición de color y elevación con `transform: translateY(-2px);`.
    - `.btn-comprar:active`: Sensación de pulsación táctil con `transform: translateY(2px) scale(0.98);`.
    - `aside ul li a:focus`: Indicador de foco obligatorio (`outline: 2px solid var(--color-secundario); outline-offset: 2px;`) garantizando accesibilidad para usuarios de navegación por teclado (`Tab`).
  - **Pseudoelementos virtuales:**
    - `aside ul li::before`: Inserción de la viñeta visual `>` sin crear elementos `<span>` en el HTML.
    - `.productos article h3::after`: Inyección de la insignia decorativa `¡Nuevo!` con color de fondo principal y espaciado proporcional.
* **¿Qué se hizo bien? (Criterio de validación):** El código HTML se mantuvo 100% semántico y limpio, mientras que la interfaz ofrece retroalimentación visual clara y accesible ante cualquier acción del usuario.

```
================================================================================
RAMA 5: feature/arquitectura-bem (Subactividad 5)
================================================================================
```
* **Propósito:** Desacoplar la hoja de estilos en módulos independientes y adoptar la metodología BEM para aplanar la especificidad.
* **Comandos Git utilizados (Commits Intermedios requeridos):**
  ```bash
  git checkout -b feature/arquitectura-bem
  # Paso 1: División física de archivos
  git add .
  git commit -m "refactor(styles): modularizar codigo en archivos css independientes"
  # Paso 2: Refactorización BEM en el marcado HTML
  git add index.html
  git commit -m "refactor(html): aplicar nomenclatura BEM en los componentes del catalogo"
  # Paso 3: Selectores planos y documentación
  git add .
  git commit -m "refactor(styles): actualizar modulos css con clases BEM planas y documentar hallazgos"
  ```
* **Archivos creados e intervenidos:**
  - `css/tarjeta.css`: Estilos del componente de tarjeta `.card`.
  - `css/botones.css`: Componente `.btn` y sus modificadores.
  - `css/aside.css`: Componente `.menu-lateral`.
  - `style.css`: Archivo maestro orquestador mediante directivas `@import`.
  - `index.html`: Nomenclatura BEM aplicada.
* **Conceptos técnicos aplicados:**
  - **Modularidad:** Conexión con `@import url('css/...');` en la cabecera del archivo maestro.
  - **Metodología BEM estricta:**
    - **Bloque:** `.card`, `.btn`, `.menu-lateral`.
    - **Elemento:** `.card__title`, `.card__price`, `.card__description`, `.menu-lateral__link`.
    - **Modificador:** `.card--destacada`, `.btn--secundario`, `.btn--destacado`.
  - **Especificidad Plana (Peso 10 / 0-1-0):** Se reemplazaron selectores anidados complejos (`.productos article h3`) por clases directas (`.card__title`).
* **¿Qué se hizo bien? (Criterio de validación):** Cada módulo gestiona una única responsabilidad (SRP), se previenen colisiones de clases y el peso de especificidad es idéntico y predecible en todo el código.

```
================================================================================
RAMA 6: feature/arquitectura-flexbox (Subactividad 6)
================================================================================
```
* **Propósito:** Construir un sistema de diseño elástico unidimensional con alineación simétrica y control total de ejes (X e Y).
* **Comandos Git utilizados:**
  ```bash
  git checkout -b feature/arquitectura-flexbox
  git add .
  git commit -m "feat(layout): implementar arquitectura total flexbox en todas las vistas y componentes del proyecto"
  git commit -m "style(header): ajustar espaciado de cabecera"
  ```
* **Archivos intervenidos:** `index.html`, `style.css`, `css/header.css`, `css/aside.css`, `css/tarjeta.css`, `css/botones.css`, `css/footer.css`, `css/variables.css`.
* **Conceptos técnicos aplicados:**
  - **Macro-Layout y Sticky Footer:**
    - `.app-layout`: `display: flex; flex-direction: column; min-height: 100vh;`
    - `.main-wrapper`: `display: flex; flex: 1;` colocando el `<aside>` y el `<main>` lado a lado y absorbiendo todo el espacio vertical sobrante para que el `footer` quede siempre pegado a la base de la pantalla.
  - **Reemplazo de márgenes por `gap`:** En `.nav__list` (`gap: var(--espaciado-medio);`) y en el menú lateral, evitando el uso de márgenes perimetrales y selectores `:last-child`.
  - **Simetría vertical con el resorte elástico:**
    - `.card`: `display: flex; flex-direction: column; height: 100%;`
    - `.card__description`: `flex-grow: 1;` actúa como un resorte que absorbe cualquier variación en la longitud del texto y empuja el botón `.card__button` milimétricamente hacia la base en todas las tarjetas de la vitrina.
  - **Micro-flexbox en precios:** `.card__price-wrapper`: `display: flex; justify-content: space-between; align-items: baseline;` alineando el precio de oferta junto al precio original tachado (`<del>`) sobre la misma línea tipográfica de base.
* **¿Qué se hizo bien? (Criterio de validación):** La página es completamente responsiva, el footer nunca flota en pantallas grandes con poco contenido, y las tarjetas conservan una alineación horizontal perfecta y profesional.

---

## 📚 Compendio Teórico de Hallazgos

### 1. Hallazgos: El Modelo de Caja
1. **Diferencia fundamental entre `padding` y `margin`:**  
   El `padding` (relleno) es el espacio interno que existe entre el contenido y el borde de la caja; forma parte del área clicable del elemento y adopta su color de fondo. El `margin` (margen) es el espacio exterior transparente que separa la caja de sus elementos hermanos o contenedores en el flujo del documento.
2. **Por qué es obligatorio usar `box-sizing: border-box`:**  
   Bajo el modelo tradicional (`content-box`), agregar padding o border suma píxeles al tamaño declarado de la caja (`width + padding + border`), causando desbordamientos horizontales. Al usar `border-box`, el navegador absorbe dichos valores hacia el interior, garantizando que el elemento mantenga de forma estricta el ancho y alto asignados.
3. **Comportamiento ante un margen grande en un elemento hermano:**  
   Crea una zona exterior de repulsión física que empuja a los elementos adyacentes en el flujo. En flujos verticales tradicionales puede activar el *colapso de márgenes* (donde solo prevalece el margen de mayor valor), mientras que en flujos en línea o flexibles suma las distancias exactas sin colapsar.

### 2. Hallazgos: Centralización de Identidad Visual y Espaciado
1. **Tokens centralizados:** Variables de paleta cromática (`--color-principal`, `--color-secundario`, `--color-fondo`, `--color-texto`), familia tipográfica (`--fuente-principal`) y medidas proporcionales (`--espaciado-pequeno`, `--espaciado-medio`, `--espaciado-grande`).
2. **Ventaja de reutilizar medidas:** Asegura *consistencia de diseño* en toda la interfaz. Si se requiere ajustar el aire entre componentes, se modifica un solo valor en `:root` en lugar de editar cientos de selectores.
3. **Prevención de colisiones visuales:** Evita la deuda técnica producida por valores numéricos al azar (ej. 13px o 17px), asegurando un orden estético matemáticamente armónico.

### 3. Hallazgos: Pseudoclases y Pseudoelementos
1. **Diferencia funcional:** Una **pseudoclase** (`:hover`, `:active`, `:focus`) selecciona un elemento basándose en su estado o en la interacción del usuario. Un **pseudoelemento** (`::before`, `::after`) genera contenido o cajas decorativas virtuales en el árbol de renderizado sin modificar el HTML.
2. **Importancia de `:focus` para accesibilidad:** Proporciona un indicador visual imprescindible para usuarios que navegan mediante tecnología de asistencia o mediante la tecla `Tab` del teclado.
3. **Ventaja de inyectar elementos desde CSS:** Mantiene el código HTML con valor exclusivamente semántico, delegando los detalles ornamentales a la capa de presentación.

### 4. Hallazgos: Arquitectura BEM y Modularidad
1. **Significado de BEM y sintaxis visual:**  
   - **Bloque (`.bloque`):** Componente independiente con significado propio (ej. `.card`, `.btn`).
   - **Elemento (`.bloque__elemento`):** Parte interna subordinada al bloque conectada con doble guion bajo (ej. `.card__title`, `.card__price`).
   - **Modificador (`.bloque--modificador`):** Variante visual o de estado conectada con doble guion medio (ej. `.card--destacada`, `.btn--secundario`).
2. **Facilidad para el trabajo colaborativo:** Dividir el código en módulos (`tarjeta.css`, `botones.css`, `aside.css`) permite que varios desarrolladores trabajen en paralelo en distintos componentes sin generar conflictos de fusión (*merge conflicts*) en Git.
3. **Prevención de la guerra de especificidad:** En CSS tradicional, anidar selectores (`header nav ul li a`) infla la especificidad (0-1-4). BEM asegura que cada regla apunte a una clase plana única (peso 0-1-0 o valor 10), garantizando que las reglas se apliquen de forma limpia y predecible por orden de cascada.

### 5. Hallazgos: Arquitectura Total con Flexbox
1. **Por qué fue crucial `min-height: 100vh` y `flex-direction: column`:**  
   Garantiza que el contenedor global abarque como mínimo el 100% de la altura visible de la pantalla. Al trabajar en columna junto a `flex: 1` en el contenedor central (`.main-wrapper`), este absorbe el espacio vertical disponible y empuja de manera natural y permanente el pie de página hacia el fondo de la pantalla (*Sticky Footer*).
2. **Cómo `gap` reemplazó los márgenes laterales en menús:**  
   `gap` distribuye el espaciado interno estricto únicamente *entre* los elementos flexibles (gutter). Elimina la necesidad de aplicar márgenes y de escribir selectores de excepción como `:last-child` o `:first-child`, manteniendo el CSS conciso y limpio.
3. **Tarjeta de producto resistente a diferentes longitudes de texto:**  
   La combinación de `.card { display: flex; flex-direction: column; height: 100%; }` con `flex-grow: 1;` en el contenedor de texto (`.card__description`) permite que el texto absorba dinámicamente todo el espacio sobrante. Este efecto de "resorte invisible" nivela automáticamente los bloques de precio y el botón de compra en la misma línea horizontal en todas las tarjetas de la vitrina, independientemente de si una descripción tiene dos líneas o cinco líneas de contenido.

---
*Documentación consolidada y validada según el instrumento de evaluación del SENA.*
