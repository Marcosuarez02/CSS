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