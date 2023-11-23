Processing proporciona una serie de funciones de sistema que son esenciales para controlar el flujo y la configuración del entorno de un sketch. Estas funciones permiten a los programadores manejar eventos, configurar propiedades del entorno y realizar tareas específicas de Processing. 

Algunas de las funciones de sistema más importantes en Processing son:

1. **`setup()`**:
   - Se ejecuta una vez al inicio del sketch.
   - Utilizada para configuraciones iniciales como tamaño del lienzo, colores de fondo, cargar medios, etc.

2. **`draw()`**:
   - Se ejecuta repetidamente después de `setup()` y es donde se dibuja y actualiza el contenido del sketch.
   - Ideal para animaciones y para reaccionar a eventos de usuario.

3. **`settings()`**:
   - Se ejecuta antes de `setup()`.
   - Utilizada para configurar elementos que deben establecerse antes de que el lienzo se cree, como `size()` o `fullScreen()`.

4. **`mousePressed()`, `mouseReleased()`, `mouseClicked()`, `mouseMoved()`, `mouseDragged()`**:
   - Funciones que se llaman automáticamente en respuesta a eventos del ratón.
   - Permiten la interacción con el usuario a través del ratón.

5. **`keyPressed()`, `keyReleased()`, `keyTyped()`**:
   - Funciones que se activan en respuesta a eventos del teclado.
   - Permiten la interacción con el usuario a través del teclado.

6. **`frameRate(fps)`**:
   - Establece la velocidad a la que el sketch procesa y dibuja frames por segundo.
   - Útil para controlar la fluidez de las animaciones.

7. **`noLoop()`, `loop()`**:
   - `noLoop()` detiene el ciclo de `draw()`, `loop()` lo reinicia.
   - Útiles para controlar cuándo se actualiza el sketch.

8. **`delay(milliseconds)`**:
   - Pausa el sketch por un número específico de milisegundos.
   - Útil para temporizaciones y pausas.

9. **`save(filename)`, `saveFrame(filename)`**:
   - Permiten guardar imágenes del lienzo.
   - `saveFrame()` es útil para crear animaciones frame por frame.

10. **`loadImage()`, `image()`, `imageMode()`**:
    - Para cargar y mostrar imágenes.
    - `imageMode()` cambia la forma en que las imágenes se dibujan en relación a sus coordenadas.

11. **`createGraphics()`**:
    - Crea un objeto gráfico que puede ser utilizado como un lienzo independiente.
    - Útil para dibujos complejos o para aplicar efectos a una porción del lienzo.

12. **`beginShape()`, `endShape()`**:
    - Permiten la creación de formas personalizadas.
    - Entre estas dos funciones, se usan vértices y otros comandos para definir la forma.

13. **`translate()`, `rotate()`, `scale()`**:
    - Funciones de transformación para cambiar la posición, orientación y escala de los elementos del lienzo.

14. **`colorMode()`**:
    - Cambia el modo de interpretar los colores (RGB, HSB).

Estas funciones proporcionan la estructura básica y las herramientas para crear sketches interactivos y dinámicos en Processing. Son fundamentales para entender cómo Processing gestiona el flujo de un programa, la interacción con el usuario y la manipulación del lienzo.