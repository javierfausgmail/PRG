Las funciones `beginShape()` y `endShape()` en Processing se utilizan para crear formas personalizadas complejas que pueden no ser directamente realizables con las formas básicas de Processing como `rect()`, `ellipse()`, etc. Estas funciones te permiten definir tus propios polígonos y formas a través de una serie de vértices. Aquí te explico los conceptos fundamentales y te proporciono algunos ejemplos.

### Conceptos Fundamentales

1. **`beginShape()`**:
   - Marca el inicio de una forma personalizada.
   - Se pueden especificar modos para determinar cómo se interpretarán los vértices (como `POINTS`, `LINES`, `TRIANGLES`, `TRIANGLE_FAN`, `TRIANGLE_STRIP`, `QUADS`, `QUAD_STRIP`).

2. **Vértices**:
   - `vertex(x, y)`: Define los puntos (vértices) de la forma. Los parámetros `x` y `y` son las coordenadas del vértice.
   - También puedes usar `curveVertex()` para vértices que forman parte de una curva.

3. **`endShape()`**:
   - Finaliza la forma.
   - Puede tomar un parámetro opcional `CLOSE` para cerrar la forma, conectando el último vértice con el primero.

4. **Otros Comandos**:
   - `bezierVertex()`: Para crear curvas de Bézier dentro de la forma.
   - `quadraticVertex()`: Para crear puntos de control de curvas cuadráticas.

### Ejemplos de Formas Personalizadas

#### Ejemplo 1: Triángulo Simple
```java
void setup() {
  size(200, 200);
}

void draw() {
  background(255);
  beginShape();
  vertex(50, 50);
  vertex(150, 50);
  vertex(100, 150);
  endShape(CLOSE);
}
```
Este ejemplo dibuja un triángulo simple.

#### Ejemplo 2: Forma de Estrella
```java
void setup() {
  size(200, 200);
}

void draw() {
  background(255);
  beginShape();
  vertex(100, 20);
  vertex(120, 90);
  vertex(190, 90);
  vertex(135, 130);
  vertex(160, 200);
  vertex(100, 160);
  vertex(40, 200);
  vertex(65, 130);
  vertex(10, 90);
  vertex(80, 90);
  endShape(CLOSE);
}
```
Una forma de estrella más compleja utilizando múltiples vértices.

#### Ejemplo 3: Forma con Curvas
```java
void setup() {
  size(200, 200);
}

void draw() {
  background(255);
  beginShape();
  vertex(40, 120);
  bezierVertex(40, 20, 160, 20, 160, 120);
  vertex(160, 180);
  quadraticVertex(100, 120, 40, 180);
  endShape(CLOSE);
}
```
Este ejemplo crea una forma utilizando tanto `bezierVertex()` como `quadraticVertex()` para curvas más complejas.

#### Ejemplo 4: Forma con Curvas y Líneas Suaves
```java
void setup() {
  size(200, 200);
  smooth();
}

void draw() {
  background(255);
  beginShape();
  curveVertex(84,  91);
  curveVertex(84,  91);
  curveVertex(68,  19);
  curveVertex(21,  17);
  curveVertex(32, 100);
  curveVertex(32, 100);
  endShape();
}
```
Una forma con curvas suaves usando `curveVertex()`.

Estos ejemplos ilustran cómo puedes crear una variedad de formas, desde las más básicas hasta las más complejas, utilizando `beginShape()` y `endShape()`. La clave es experimentar con la ubicación de los vértices y diferentes tipos de comandos de vértices para crear formas únicas.