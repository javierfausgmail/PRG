Ideas de programas en Processing que utilizan arrays. Cada idea viene acompañada de un breve código de ejemplo y una explicación.

### Cambio de Colores en una Cuadrícula

**Concepto**: Crear una cuadrícula de cuadrados en la pantalla, donde cada cuadrado cambia de color al hacer clic sobre él.

**Código de Ejemplo**:

```java
int[][] colores;
int tamCuadrado = 50;

void setup() {
  size(400, 400);
  int filas = width / tamCuadrado;
  int columnas = height / tamCuadrado;
  colores = new int[filas][columnas];
}

void draw() {
  for (int i = 0; i < colores.length; i++) {
    for (int j = 0; j < colores[i].length; j++) {
      fill(colores[i][j]);
      rect(i*tamCuadrado, j*tamCuadrado, tamCuadrado, tamCuadrado);
    }
  }
}

void mousePressed() {
  int fila = mouseX / tamCuadrado;
  int columna = mouseY / tamCuadrado;
  colores[fila][columna] = color(random(255), random(255), random(255));
}
```

**Explicación**: Este programa utiliza un array bidimensional para almacenar colores. Al hacer clic en un cuadrado, se cambia su color de manera aleatoria.

---

### Visualización de Datos con Barras

**Concepto**: Crear un gráfico de barras simple donde cada barra representa un valor almacenado en un array.

**Código de Ejemplo**:

```java
float[] valores;
int numBarras = 10;

void setup() {
  size(400, 400);
  valores = new float[numBarras];
  for (int i = 0; i < valores.length; i++) {
    valores[i] = random(height);
  }
}

void draw() {
  background(255);
  for (int i = 0; i < valores.length; i++) {
    float anchoBarra = width / valores.length;
    rect(i * anchoBarra, height - valores[i], anchoBarra, valores[i]);
  }
}
```

**Explicación**: Este programa muestra cómo usar un array para almacenar y visualizar datos en forma de un gráfico de barras. Cada elemento del array representa la altura de una barra.

---

### Dibujar en array con sus valores

Vamos a crear un programa que muestre visualmente un array de números, representando cada número como un cuadrado en la pantalla, con el valor del número escrito dentro del cuadrado. Por simplicidad, haremos que los cuadrados se dispongan en una fila.

```java
int[] edades = {23, 4, 6, 18, 35, 12}; // Array de edades
int tamCuadrado = 50; // Tamaño de cada cuadrado

void setup() {
  size(400, 200); // Configurar el tamaño de la ventana
  textAlign(CENTER, CENTER); // Alinear texto en el centro
}

void draw() {
  background(255); // Fondo blanco
  for (int i = 0; i < edades.length; i++) {
    // Dibujar cada cuadrado
    fill(200); // Color del cuadrado
    rect(i * tamCuadrado, 50, tamCuadrado, tamCuadrado); // Dibujar el cuadrado
    fill(0); // Color del texto
    text(edades[i], i * tamCuadrado + tamCuadrado/2, 75); // Dibujar el número
  }
}
```

**Explicación del código**:

1. **Array de Edades**: Creamos un array llamado `edades` que contiene varios números.

2. **Tamaño de Cada Cuadrado**: Definimos el tamaño de cada cuadrado que representa un elemento del array.

3. **Función `setup`**: Configuramos el tamaño de la ventana y la alineación del texto.

4. **Función `draw`**: Dibujamos los cuadrados y sus correspondientes números. Usamos un bucle `for` para recorrer el array `edades`. En cada iteración, dibujamos un cuadrado y el número dentro de él. La posición de cada cuadrado en el eje X se determina por el índice del array multiplicado por el tamaño del cuadrado.

Este programa creará una fila de cuadrados, cada uno representando un elemento del array `edades`, y mostrará el número correspondiente centrado dentro de cada cuadrado. Es una manera visual e interactiva de enseñar cómo funcionan los arrays y cómo se pueden usar para almacenar y acceder a datos.


### Dibujar en array con sus valores en forma de histograma (diagrama de barras) coloreadas

Un histograma es una representación gráfica que muestra la distribución de un conjunto de datos y es perfecto para enseñar cómo se pueden analizar y visualizar datos usando programación.

Cada año de edad se represente con una altura fija de 10px, y se varia el color de las barras según su altura. 

```java
int[] edades = {23, 4, 6, 18, 35, 12}; // Array de edades
int alturaPorAno = 10; // Altura por cada año de edad
int anchoBarra = 20; // Ancho fijo para todas las barras

void setup() {
  size(400, 400); // Tamaño de la ventana
  background(255); // Fondo blanco
  noStroke(); // Sin bordes en las barras
  for (int i = 0; i < edades.length; i++) {
    int alturaBarra = edades[i] * alturaPorAno;
    // El color varía de claro a oscuro según la altura
    fill(255 - alturaBarra, 100, 100); 
    rect(i * anchoBarra, height - alturaBarra, anchoBarra, alturaBarra);
  }
}
```

Otra variante, más compleja, que adapta el tamaño de las barras al del canvas para  implementar un histograma de barras para el array de edades:

```java
int[] edades = {23, 4, 6, 18, 35, 12}; // Array de edades
int maxEdad = 50; // Edad máxima para escala del histograma

void setup() {
  size(360, 200); // Tamaño de la ventana
  background(255); // Fondo blanco
  drawHistogram(edades, maxEdad);
}

void drawHistogram(int[] datos, int maxValor) {
  int numBarras = datos.length;
  int anchoBarra = width / numBarras;

  for (int i = 0; i < numBarras; i++) {
    int alturaBarra = int(map(datos[i], 0, maxValor, 0, height));
    fill(100, 100, 250); // Color de la barra
    rect(i * anchoBarra, height - alturaBarra, anchoBarra, alturaBarra);
  }
}
```

**Explicación del código**:

1. **Array de Edades**: Usamos el array `edades` que contiene varias edades.

2. **Máximo Valor para el Histograma**: Establecemos un valor máximo para la escala del histograma. En este caso, `50` es un número arbitrario, pero podría ser el valor más alto que espera en su conjunto de datos.

3. **Función `setup`**: Configuramos el tamaño de la ventana y el fondo, y llamamos a la función `drawHistogram`.

4. **Función `drawHistogram`**: Esta función dibuja el histograma. Calculamos el ancho de cada barra basándonos en el número de elementos en el array. La función `map()` se usa para escalar la altura de cada barra basándose en la altura de la ventana y el valor máximo del histograma.

Este ejemplo crea un histograma básico donde cada barra representa la edad de una persona. La altura de cada barra es proporcional a la edad que representa.


Por supuesto, enseñar arrays bidimensionales en Processing a estudiantes que aún no están familiarizados con la programación orientada a objetos es un desafío interesante. Aquí le propongo algunas ideas que pueden ser útiles para introducir este concepto de manera visual y atractiva:

### Cuadrícula de Colores

**Concepto**: Crear una cuadrícula donde cada celda tiene un color que se almacena en un array bidimensional.

**Código de Ejemplo**:

```java
int filas = 10;
int columnas = 10;
color[][] colores;

void setup() {
  size(400, 400);
  colores = new color[filas][columnas];
  for (int i = 0; i < filas; i++) {
    for (int j = 0; j < columnas; j++) {
      colores[i][j] = color(random(255), random(255), random(255));
    }
  }
}

void draw() {
  for (int i = 0; i < filas; i++) {
    for (int j = 0; j < columnas; j++) {
      fill(colores[i][j]);
      rect(i * width/filas, j * height/columnas, width/filas, height/columnas);
    }
  }
}
```

**Explicación**: Este programa crea una cuadrícula de colores. Cada celda de la cuadrícula es representada por un elemento en el array bidimensional `colores`. Los colores se asignan aleatoriamente.

---

### Tablero de Ajedrez

**Concepto**: Dibujar un tablero de ajedrez, alternando colores entre las celdas.

**Código de Ejemplo**:

```java
int tamano = 8; // Tamaño del tablero de ajedrez
boolean[][] tablero = new boolean[tamano][tamano];

void setup() {
  size(320, 320);
  for (int i = 0; i < tamano; i++) {
    for (int j = 0; j < tamano; j++) {
      tablero[i][j] = (i + j) % 2 == 0;
    }
  }
}

void draw() {
  for (int i = 0; i < tamano; i++) {
    for (int j = 0; j < tamano; j++) {
      fill(tablero[i][j] ? 255 : 0);
      rect(i * width/tamano, j * height/tamano, width/tamano, height/tamano);
    }
  }
}
```

**Explicación**: En este ejemplo, usamos un array bidimensional de valores booleanos para representar un tablero de ajedrez. Cada celda alterna su color basándose en su posición.

---


### Array animado

Este programa dibuja cuadrados que representan las celdas de un array unidimensional. Cada cuadrado muestra el valor numérico del elemento del array y el cuadrado correspondiente al índice actual se resalta. Además, se muestra el nombre del array y el índice actual con la sintaxis de Java:


```java
int[] myArray = {10, 20, 30, 40, 50}; // Array de ejemplo
int squareSize = 50; // Tamaño de cada cuadrado
int spacing = 10; // Espaciado entre cuadrados
int currentIndex = 0; // Índice actual en el array

void setup() {
  size(400, 200); // Establece el tamaño de la ventana
  textSize(16); // Establece el tamaño del texto
}

void draw() {
  background(255); // Establece el fondo a blanco
  fill(0); // Establece el color del texto a negro
  text("myArray[ ]", 10, 30); // Muestra el nombre del array

  for (int i = 0; i < myArray.length; i++) {
    int x = i * (squareSize + spacing) + 30; // Calcula la posición x
    int colorValue = (i == currentIndex) ? color(255, 200, 200) : color(200); // Determina el color
    dibujarCuadrado(squareSize, squareSize, x, 50, colorValue, myArray[i]);
  }

  fill(0); // Establece el color del texto a negro
  text("[" + currentIndex + "]", 90, 30); // Muestra el índice actual

  if (frameCount % 60 == 0) { // Cambia el índice cada segundo
    currentIndex = (currentIndex + 1) % myArray.length;
  }
}

void dibujarCuadrado(int ancho, int alto, int posX, int posY, color col, int valor) {
  fill(col); // Establece el color del cuadrado
  rect(posX, posY, ancho, alto); // Dibuja el cuadrado
  fill(0); // Establece el color del texto a negro
  text(valor, posX + ancho/2 - 10, posY + alto/2 + 5); // Muestra el valor en el cuadrado
}
```

La función `dibujarCuadrado` toma el ancho, alto, posición X e Y, color, y valor numérico como argumentos para dibujar cada cuadrado del array. 


### Array Bidimensional

Ampliamos el código para trabajar con un array bidimensional. Ahora, el programa coloreará los elementos a medida que se van recorriendo. Los índices de fila y columna se muestran claramente, lo que permite seguir visualmente la iteración a través del array. 

```java
int[][] my2DArray = {{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}}; // Array bidimensional de ejemplo
int squareSize = 50; // Tamaño de cada cuadrado
int spacing = 10; // Espaciado entre cuadrados
int currentRow = 0; // Fila actual
int currentCol = 0; // Columna actual

void setup() {
  size(400, 300); // Establece el tamaño de la ventana
  textSize(16); // Establece el tamaño del texto
}

void draw() {
  background(255); // Establece el fondo a blanco
  for (int i = 0; i < my2DArray.length; i++) {
    for (int j = 0; j < my2DArray[i].length; j++) {
      int x = j * (squareSize + spacing) + 30; // Calcula la posición x
      int y = i * (squareSize + spacing) + 50; // Calcula la posición y
      int colorValue = (i == currentRow && j == currentCol) ? color(255, 200, 200) : color(200); // Determina el color
      dibujarCuadrado(squareSize, squareSize, x, y, colorValue, my2DArray[i][j], i, j);
    }
  }

  if (frameCount % 30 == 0) { // Cambia el índice cada medio segundo
    currentCol++;
    if (currentCol >= my2DArray[currentRow].length) {
      currentCol = 0;
      currentRow = (currentRow + 1) % my2DArray.length;
    }
  }
}

void dibujarCuadrado(int ancho, int alto, int posX, int posY, color col, int valor, int fila, int columna) {
  fill(col); // Establece el color del cuadrado
  rect(posX, posY, ancho, alto); // Dibuja el cuadrado
  fill(0); // Establece el color del texto a negro
  text(valor, posX + ancho/2 - 10, posY + alto/2 + 5); // Muestra el valor en el cuadrado
  text("[" + fila + "," + columna + "]", posX, posY - 5); // Muestra los índices de fila y columna
}
```


### Ejemplos de aplicaciones a crear

Especialmente en el contexto del desarrollo de juegos y aplicaciones.

1. **3 en Raya (Tic-Tac-Toe)**: Se juega en una matriz 3x3. Cada jugador marca alternativamente una celda de la matriz con su símbolo (X o O), y gana quien primero alinea tres de sus símbolos horizontal, vertical o diagonalmente.

2. **Conecta 4**: Se juega en una matriz vertical, generalmente 6x7. Los jugadores van colocando fichas en las columnas, que se acumulan en la fila más baja disponible. El objetivo es formar una línea de cuatro fichas del mismo color, ya sea horizontal, vertical o diagonal.

3. **Crucigrama**: Se basa en una matriz de celdas blancas y negras. Las celdas blancas se llenan con letras, formando palabras que se cruzan horizontal y verticalmente, según las pistas proporcionadas.

4. **Sudoku**: Se juega en una matriz 9x9, dividida en submatrices de 3x3. El objetivo es llenar la matriz con números del 1 al 9 de tal manera que cada fila, columna y submatriz contenga todos los números sin repetir.

5. **Hundir la Flota (Battleship)**: Se juega con dos matrices, generalmente 10x10, una para cada jugador. Los jugadores colocan barcos en su matriz y adivinan la ubicación de los barcos del oponente en la otra matriz, tratando de "hundir" todos los barcos enemigos.

6. **Tablero de Ajedrez**: El ajedrez se juega en una matriz de 8x8. Cada jugador controla un conjunto de piezas con diferentes movimientos y objetivos, y el juego se basa en la estrategia y táctica para capturar al rey del oponente.


7. **Laberintos**: Crear un laberinto en una matriz y programar un algoritmo para encontrar la salida. Esto puede enseñar sobre algoritmos de búsqueda y recursividad.

8. **Tetris**: Un clásico juego de rompecabezas donde las piezas de diferentes formas caen en una matriz y el jugador debe acomodarlas para completar líneas y evitar que la pila alcance la parte superior.

9. **Buscaminas**: Un juego donde los jugadores descubren cuadrados en una matriz, tratando de evitar las minas. Este juego es excelente para enseñar sobre eventos de clic del ratón y la lógica de juego.

10. **Juego de la Vida de Conway**: Un autómata celular donde las células en una matriz evolucionan en cada paso de tiempo según reglas específicas. Es un excelente ejemplo para enseñar sobre simulaciones y sistemas dinámicos.

11. **Snake (Serpiente)**: El clásico juego donde el jugador controla una serpiente creciente en una matriz, evitando chocar con las paredes o consigo misma.




Estos juegos son ejercicios prácticos a realizar en equipo (elegid uno) para programar **versiones simples** de estos.
