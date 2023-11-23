	Processing proporciona una serie de variables de sistema que son útiles para obtener información sobre el entorno y la interacción del usuario con el sketch. 
	
	A continuación se presenta una lista extensiva pero no completa de estas variables, junto con una breve explicación de su utilidad:

1. **`frameCount`**: 
   - Contiene el número de cuadros (frames) que se han mostrado desde que comenzó el programa.
   - Útil para temporizar eventos o crear animaciones que cambian con el tiempo.

2. **`frameRate`**:
   - La tasa aproximada a la que se están mostrando los frames.
   - Se puede configurar para limitar la velocidad de la animación.

3. **`height`**:
   - La altura del lienzo de visualización en píxeles.
   - Útil para posicionar elementos o calcular movimientos dentro del lienzo.

4. **`width`**:
   - El ancho del lienzo de visualización en píxeles.
   - Utilizado de manera similar a `height`.

5. **`mouseX`, `mouseY`**:
   - La posición actual del cursor del ratón en coordenadas x e y.
   - Esencial para la interactividad basada en el ratón.

6. **`pmouseX`, `pmouseY`**:
   - La posición anterior del cursor del ratón en coordenadas x e y.
   - Útil para calcular el movimiento del ratón entre frames.

7. **`mouseButton`**:
   - Indica qué botón del ratón fue presionado (LEFT, RIGHT, CENTER).
   - Útil para interacciones más complejas con el ratón.

8. **`mousePressed`**:
   - Un booleano que es `true` si algún botón del ratón está presionado y `false` en caso contrario.
   - Permite detectar si el usuario está interactuando con el ratón.

9. **`key`**:
   - La última tecla que fue presionada o soltada.
   - Permite interactuar con el teclado.

10. **`keyCode`**:
    - El código de la última tecla presionada, proporcionando un control más detallado que `key`.
    - Útil para teclas como las flechas del teclado o el Enter.

11. **`keyPressed`**:
    - Un booleano que es `true` si alguna tecla está presionada y `false` en caso contrario.
    - Útil para detectar la interacción continua con el teclado.

12. **`focused`**:
    - `true` si la ventana del sketch está enfocada, `false` si no lo está.
    - Útil para saber si el usuario está interactuando con la ventana del sketch.

13. **`displayWidth`, `displayHeight`**:
    - Las dimensiones totales de la pantalla.
    - Útil para sketches que interactúan con la configuración de la pantalla completa.

14. **`pixels[]`**:
    - Un arreglo que contiene los valores de color de todos los píxeles en el lienzo.
    - Permite un acceso y manipulación directa de los píxeles para efectos gráficos avanzados.

Estas variables son fundamentales en muchos sketches de Processing y ofrecen una amplia gama de posibilidades para la creación de interactividad, animación y efectos visuales.