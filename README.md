# Hallazgos: El modelo de caja 

#### 1.Diferenca padding y margin 
La diferencia fundamental radica en su ubicación respecto a los límites del elemento: el `padding` (relleno) es el espacio interno que existe entre el contenido y el borde de la caja, mientras que el `margin` (margen) es el espacio exterior que separa al elemento de sus contenedores adyacentes o hermanos dentro del flujo del documento.

### 2.Por qué es obligatorio usar box-sizing: border-box
Es una regla esencial en la arquitectura CSS porque reestructura el cálculo matemático nativo del navegador. Al establecer `box-sizing: border-box`, los valores asignados a `padding` y `border` se absorben hacia el interior del elemento sin incrementar sus dimensiones totales (`width` y `height`), garantizando que la caja mantenga su tamaño exacto y evitando desbordamientos que rompan la maquetación.

### 3.Cómo se ven afectados los elementos hermanos cuando le aplicas un margen grande a uno de ellos.
Cuando se aplica un margen grande a un elemento, este crea un área de separación exterior que empuja físicamente a sus elementos hermanos adyacentes en el flujo del documento, desplazándolos hacia abajo o hacia los lados según su disposición; en flujos verticales tradicionales puede activar el colapso de márgenes (donde solo prevalece el margen más amplio entre hermanos), en flujos horizontales puede provocar saltos de línea no deseados al agotar el ancho del contenedor padre, y en contenedores modernos como Flexbox o Grid suma las distancias exactas sin colapsar, pudiendo forzar a los demás elementos hermanos a comprimirse o reubicarse en los extremos opuestos