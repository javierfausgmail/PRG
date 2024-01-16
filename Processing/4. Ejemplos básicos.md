
### 10 Ejemplos Prácticos - Nivel Fácil

Estos ejemplos permitirán a los alumnos familiarizarse con el entorno Processing y ejercitar conceptos básicos.


**Ejemplo 0: Coordenadas del ratón**
```java
void setup() {
  size(400, 400); // Tamaño del lienzo
  background(255); // Establece el color de fondo a blanco
}

void draw() {
  background(255); // Limpia el lienzo para que las coordenadas anteriores no se superpongan
  
  // Configura el texto para mostrar las coordenadas del ratón
  fill(0,0,255); // Establece el color de texto a negro
  textSize(12); // Establece el tamaño de texto a 12 píxeles para la posición del ratón
  text("X: " + mouseX + " Y: " + mouseY, mouseX, mouseY); // Muestra las coordenadas del ratón en movimiento

  // Configura el texto para mostrar las coordenadas del ratón en una posición fija
  fill(255, 0, 0); // Establece el color de texto a rojo
  textSize(20); // Cambia el tamaño de texto a 20 píxeles para la posición fija
  text("X: " + mouseX + " Y: " + mouseY, 200, 200); // Muestra las coordenadas del ratón en la posición fija
}

```




**Ejemplo 1: Dibujo de un círculo que sigue al ratón**
```java
void setup() {
  size(400, 400);
  background(255);
}

void draw() {
  background(255); // Limpia el fondo cada vez para no dejar rastro
  ellipse(mouseX, mouseY, 50, 50);
}
```

**Ejemplo 2: Cambio de color con el movimiento del ratón**
```java
void setup() {
  size(400, 400);
}

void draw() {
  background(mouseX, mouseY, mouseX-mouseY);
}
```

**Ejemplo 3: Dibujar una línea que sigue al ratón**
```java
void setup() {
  size(400, 400);
  background(255);
}

void draw() {
  line(mouseX, mouseY, pmouseX, pmouseY);
}
```

**Ejemplo 4: Uso de la función `mousePressed` para dibujar**
```java
void setup() {
  size(400, 400);
  background(255);
}

void draw() {
  if (mousePressed) {
    fill(0);
  } else {
    fill(255);
  }
  ellipse(mouseX, mouseY, 30, 30);
}
```

**Ejemplo 5: Animación de un rectángulo moviéndose**
```java
int x = 0;

void setup() {
  size(400, 400);
  background(255);
}

void draw() {
  background(255);
  x = (x + 1) % width; // Hace que 'x' se reinicie al llegar al ancho del lienzo
  rect(x, height/2, 50, 50);
}
```

**Ejemplo 6: Tecla presionada cambia el color de fondo**
```java
void setup() {
  size(400, 400);
}

void draw() {
  // El fondo cambia con draw() para permitir la reacción en tiempo real al presionar teclas
}

void keyPressed() {
  background(random(255), random(255), random(255));
}
```

**Ejemplo 7: Dibujo de múltiples círculos con un bucle `for`**
```java
void setup() {
  size(400, 400);
  background(255);
}

void draw() {
  background(255);
  for (int i = 0; i < width; i+=50) {
    ellipse(i, height/2, 40, 40);
  }
}
```

**Ejemplo 8: Uso de `mouseClicked()` para dibujar círculos**
```java
void setup() {
  size(400, 400);
  background(255);
}

void draw() {
  // No necesitamos hacer nada aquí para este ejemplo
}

void mouseClicked() {
  ellipse(mouseX, mouseY, 50, 50);
}
```

**Ejemplo 9: Crear una paleta de colores interactivo**
```java
void setup() {
  size(400, 400);
}

void draw() {
  int tileCount = 10;
  int rectSize = width/tileCount;
  
  for (int i = 0; i < tileCount; i++) {
    for (int j = 0; j < tileCount; j++) {
      fill(i*25, j*25, (i+j)*12.5);
      rect(i*rectSize, j*rectSize, rectSize, rectSize);
    }
  }
}
```

**Ejemplo 10: Usar `mouseX` y `mouseY` para cambiar tamaños de figuras**
```java
void setup() {
  size(400, 400);
}

void draw() {
  background(255);
  ellipse(width/2, height/2, mouseX, mouseY);
}
```

