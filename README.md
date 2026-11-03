# CSS

## Cálculo de especificidad

La especificidad determina qué regla CSS prevalece cuando varias reglas
afectan al mismo elemento. Para este ejercicio se utiliza la siguiente escala:

- **Etiqueta:** 1 punto. Ejemplo: `h1` = 1 punto.
- **Clase:** 10 puntos. Ejemplo: `.btn-comprar` = 10 puntos.
- **ID:** 100 puntos. Ejemplo: `#btn-destacado` = 100 puntos.

La hoja de estilos fue refactorizada para evitar selectores por `id` y
trabajar exclusivamente con etiquetas y clases. El enlace destacado utiliza
las clases `.btn-comprar` y `.btn-destacado`; ambas reglas tienen 10 puntos de
especificidad. Como `.btn-destacado` aparece después, la cascada resuelve la
colisión visual sin utilizar `!important`.
