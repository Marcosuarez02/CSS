# Hallazgos: El modelo de caja 

#### 1.Diferenca padding y margin 
La diferencia fundamental radica en su ubicación respecto a los límites del elemento: el `padding` (relleno) es el espacio interno que existe entre el contenido y el borde de la caja, mientras que el `margin` (margen) es el espacio exterior que separa al elemento de sus contenedores adyacentes o hermanos dentro del flujo del documento.

### 2.Por qué es obligatorio usar box-sizing: border-box
Es una regla esencial en la arquitectura CSS porque reestructura el cálculo matemático nativo del navegador. Al establecer `box-sizing: border-box`, los valores asignados a `padding` y `border` se absorben hacia el interior del elemento sin incrementar sus dimensiones totales (`width` y `height`), garantizando que la caja mantenga su tamaño exacto y evitando desbordamientos que rompan la maquetación.

### 3.Cómo se ven afectados los elementos hermanos cuando le aplicas un margen grande a uno de ellos.
Cuando se aplica un margen grande a un elemento, este crea un área de separación exterior que empuja físicamente a sus elementos hermanos adyacentes en el flujo del documento, desplazándolos hacia abajo o hacia los lados según su disposición; en flujos verticales tradicionales puede activar el colapso de márgenes (donde solo prevalece el margen más amplio entre hermanos), en flujos horizontales puede provocar saltos de línea no deseados al agotar el ancho del contenedor padre, y en contenedores modernos como Flexbox o Grid suma las distancias exactas sin colapsar, pudiendo forzar a los demás elementos hermanos a comprimirse o reubicarse en los extremos opuestos

## Hallazgos: Centralización de Identidad Visual y Espaciado

1. **Lista completa de variables declaradas:**
   - **Colores:** `--color-primario`, `--color-secundario`, `--color-fondo`, `--color-texto`, `--color-blanco`.
   - **Tipografía:** `--fuente-principal` ('roboto').
   - **Espaciados:** `--espaciado-pequeno` (8px), `--espaciado-medio` (16px), `--espaciado-grande` (24px).

2. **Ventaja de reutilizar medidas de margen y relleno:**
   Permite mantener una proporción visual estricta y coherente (*consistencia de diseño*). Si necesitamos ajustar el "aire" entre componentes, solo se modifica el token en el `:root` en lugar de buscar selector por selector.

3. **Prevención de colisiones visuales:**
   Centralizar en `:root` evita la deuda técnica y el caos de valores mágicos (números al azar como 13px o 17px), asegurando que a medida que la hoja de estilos crezca, la interfaz conserve un orden matemático y estético predecible.

## Hallazgos: Pseudoclases y Pseudoelementos

1. **Diferencia funcional entre pseudoclase y pseudoelemento:**
   - **Pseudoclase (`:hover`, `:active`, `:focus`):** Selecciona elementos basándose en su estado actual o en la interacción del usuario con la interfaz.
   - **Pseudoelemento (`::before`, `::after`):** Permite insertar contenido o elementos decorativos virtuales en el DOM sin necesidad de modificar el código HTML estructurado.

2. **Importancia técnica de la pseudoclase `:focus` para accesibilidad:**
   Garantiza que los usuarios que navegan mediante tecnología de asistencia o mediante la tecla `Tab` del teclado puedan identificar con precisión visual el elemento activo en el que se encuentran posicionados.

3. **Ventaja de inyectar elementos decorativos desde CSS:**
   Evita contaminar el código HTML con etiquetas vacías o redundantes únicamente con propósitos de diseño, manteniendo el marcado limpio, semántico y fácil de mantener.

## Hallazgos: Arquitectura BEM y Modularidad

### 1. Qué significa la sigla BEM y cómo se escribe visualmente
**BEM** es el acrónimo de **Block (Bloque)**, **Element (Elemento)** y **Modifier (Modificador)**, una metodología y convención de nomenclatura desarrollada para estructurar código CSS escalable, reutilizable y mantenible:
- **Bloque (`.bloque` / ej. `.card`, `.btn`, `.menu-lateral`):** Representa una entidad visual y funcional independiente con significado propio dentro de la interfaz. Puede existir de forma autónoma en cualquier parte del DOM.
- **Elemento (`.bloque__elemento` / ej. `.card__title`, `.card__price`, `.menu-lateral__link`):** Representa una parte interna que pertenece y depende exclusivamente de su bloque padre; se conecta mediante dos guiones bajos (`__`). No tiene sentido funcional fuera del bloque que lo contiene.
- **Modificador (`.bloque--modificador` o `.bloque__elemento--modificador` / ej. `.card--destacada`, `.btn--secundario`, `.header__link--active`):** Representa un estado, variante visual, comportamiento o tema alternativo de un bloque o elemento; se denota mediante dos guiones medios (`--`).

### 2. Por qué dividir el CSS en varios archivos facilita el trabajo colaborativo
Dividir una hoja de estilos monolítica en módulos independientes (`tarjeta.css`, `botones.css`, `menu-lateral.css` conectados mediante `@import`) ofrece múltiples beneficios en el desarrollo en equipo:
- **Prevención de conflictos de fusión (merge conflicts):** Cada desarrollador puede trabajar de manera concurrente en componentes específicos sin modificar el mismo archivo físico al mismo tiempo en el repositorio de control de versiones (Git).
- **Principio de Responsabilidad Única (SRP):** Cada módulo gestiona exclusivamente los estilos de un componente delimitado, facilitando su localización, lectura, depuración y mantenimiento sin efectos colaterales imprevistos.
- **Reutilización y escalabilidad del sistema de diseño:** Permite ensamblar interfaces compuestas por bloques independientes y desacoplados, haciendo que el proyecto crezca de forma limpia y organizada.

### 3. Cómo esta metodología evita la guerra de especificidad (Cascada) al mantener un peso plano
En CSS convencional, el anidamiento profundo de selectores (como `header nav ul li a` o `.productos article h3`) eleva progresivamente la especificidad (sumando pesos de etiquetas y clases, como 0-1-4 o 0-2-1), lo que genera una "guerra de especificidad" donde para sobrescribir una regla se requiere anidar aún más selectores o recurrir al antipatrón `!important`.

La metodología BEM soluciona este problema estableciendo una **arquitectura de especificidad plana**:
- Todos los selectores estilizan directamente mediante **una única clase** (peso 0-1-0 o valor 10 en la escala de especificidad), independientemente de la profundidad que tenga el elemento en el árbol DOM.
- Al tener todas las reglas el mismo peso predecible (10), los estilos se rigen limpiamente por el orden de la cascada y la aplicación explícita de modificadores (`.card--destacada`), eliminando las colisiones accidentales y asegurando que ninguna regla sobreescriba a otra de forma involuntaria.

## Hallazgos: Arquitectura Total con Flexbox

### 1. Por qué fue crucial aplicar `min-height: 100vh` y `flex-direction: column` al contenedor global para controlar el pie de página
Al configurar el contenedor principal (`.app-layout`) con `display: flex; flex-direction: column; min-height: 100vh;` y otorgarle al contenedor intermedio (`.main-wrapper`) la propiedad `flex: 1;`, se soluciona de forma limpia y moderna el problema del *sticky footer*. 
`min-height: 100vh` asegura que el layout abarque como mínimo el 100% de la altura de la ventana gráfica (viewport height), incluso si el contenido del catálogo es breve. Al ser un contenedor flexible en columna, el elemento central con `flex: 1` se expande dinámicamente absorbiendo todo el espacio vertical sobrante, lo que empuja de manera automática y permanente al `footer` hacia el borde inferior de la pantalla sin recurrir a trucos obsoletos o posicionamientos fijos y absolutos que causaban solapamientos.

### 2. Cómo la propiedad `gap` reemplazó el uso excesivo de márgenes laterales en los menús de navegación
Históricamente, para separar elementos de un menú horizontal (`ul li`) se recurría a `margin-right` o `margin-left`, obligando a usar selectores auxiliares como `:last-child` o `:first-child` (por ejemplo `margin-right: 0`) para eliminar el margen sobrante en los extremos y evitar descuadres visuales.
La propiedad `gap` dentro de un contenedor flexible (como `.nav__list { display: flex; gap: var(--espaciado-medio); }`) define el espaciado estricto e intermedio **únicamente entre los elementos flexibles (gutter)**. Esto elimina por completo la necesidad de márgenes perimetrales, selectores de excepción, floats o hacks de inline-block, manteniendo el marcado y las reglas de diseño limpios, matemáticamente consistentes y controlados mediante variables.

### 3. Cómo la unión de BEM, Custom Properties y Flexbox te permitió crear una tarjeta de producto resistente a diferentes longitudes de texto
La integración de estas tres herramientas resuelve el problema de las tarjetas asimétricas y botones desalineados cuando las descripciones de los productos tienen diferente cantidad de texto:
- **BEM (`.card`, `.card__description`, `.card__button`, `.card__price-wrapper`):** Proporciona una estructura semántica clara y desacoplada, permitiendo apuntar a cada sub-bloque con especificidad plana.
- **Custom Properties (`var(--espaciado-medio)`, etc.):** Estandariza los márgenes, paddings, gaps y tipografías desde un único punto centralizado en `:root`.
- **Flexbox unidimensional (`display: flex; flex-direction: column; height: 100%;`):** Obliga a todas las tarjetas dentro de la fila a estirarse uniformemente al alto de la tarjeta más alta.
- **El resorte elástico (`flex-grow: 1;` en `.card__description`):** Al aplicar `flex-grow: 1` al texto descriptivo, este absorbe todo el espacio vertical disponible sobrante dentro de la tarjeta. Como resultado, actúa como un pistón que empuja el bloque de precios y el botón de compra (`.card__button`) exactamente a la base inferior de todas las tarjetas, garantizando una alineación visual horizontal simétrica y con acabado de producción.
