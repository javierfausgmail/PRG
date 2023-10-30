Relacionados: [Resumen de bucles](Resumen%20de%20bucles.md)


A continuación se presentan varios enunciados de ejemplos junto con sus soluciones en Java, cubriendo los conceptos básicos:

### 1. **Uso Básico de Bucles**
#### a. **Bucle `while`**:
   - **Enunciado**: Crear un programa que imprima los números del 1 al 10 utilizando un bucle `while`.
   - **Solución**:
     ```java
     public class EjemploWhile {
         public static void main(String[] args) {
             int i = 1;  // Inicializar contador
             while (i <= 10) {  // Condición de continuación
                 System.out.println(i);  // Acción
                 i++;  // Incrementar contador
             }
         }
     }
     ```

#### b. **Bucle `do-while`**:
   - **Enunciado**: Crear un programa que pida al usuario un número y lo imprima. El programa debe continuar pidiendo números hasta que el usuario ingrese el número 0.
   - **Solución**:
     ```java
     import java.util.Scanner;

     public class EjemploDoWhile {
         public static void main(String[] args) {
             Scanner scanner = new Scanner(System.in);
             int numero;
             do {
                 System.out.print("Ingrese un número (0 para salir): ");
                 numero = scanner.nextInt();  // Leer número
                 if (numero != 0) {
                     System.out.println("Ingresaste: " + numero);
                 }
             } while (numero != 0);  // Condición de salida
         }
     }
     ```

#### c. **Bucle `for`**:
   - **Enunciado**: Crear un programa que imprima la tabla de multiplicar del 5 utilizando un bucle `for`.
   - **Solución**:
     ```java
     public class EjemploFor {
         public static void main(String[] args) {
             for (int i = 1; i <= 10; i++) {  // Inicialización, condición y actualización
                 System.out.println("5 * " + i + " = " + (5 * i));  // Acción
             }
         }
     }
     ```

### 2. **Uso de `break` y `continue`**
#### a. **`break`**:
   - **Enunciado**: Crear un programa que imprima los números del 1 al 5, y luego salga del bucle cuando el contador alcance el número 3 utilizando `break`.
   - **Solución**:
     ```java
     public class EjemploBreak {
         public static void main(String[] args) {
             for (int i = 1; i <= 5; i++) {
                 if (i == 3) {
                     break;  // Salir del bucle
                 }
                 System.out.println(i);
             }
         }
     }
     ```

#### b. **`continue`**:
   - **Enunciado**: Crear un programa que imprima los números impares entre 1 y 10, saltando los números pares utilizando `continue`.
   - **Solución**:
     ```java
     public class EjemploContinue {
         public static void main(String[] args) {
             for (int i = 1; i <= 10; i++) {
                 if (i % 2 == 0) {
                     continue;  // Saltar iteración actual
                 }
                 System.out.println(i);
             }
         }
     }
     ```

### 3. **Bucles Anidados**
#### a. **Independientes**:
   - **Enunciado**: Crear un programa que imprima las tablas de multiplicar del 1 al 3.
   - **Solución**:
     ```java
     public class EjemploBuclesAnidados {
         public static void main(String[] args) {
             for (int i = 1; i <= 3; i++) {  // Bucle externo
                 System.out.println("Tabla del " + i + ":");
                 for (int j = 1; j <= 10; j++) {  // Bucle interno
                     System.out.println(i + " * " + j + " = " + (i * j));
                 }
                 System.out.println();  // Línea en blanco entre tablas
             }
         }
     }
     ```

#### b. **Dependientes**:
   - **Enunciado**: Crear un programa que imprima un triángulo rectángulo de asteriscos, donde el usuario ingrese la altura del triángulo.
   - **Solución**:
     ```java
     import java.util.Scanner;

     public class EjemploTriangulo {
         public static void main(String[] args) {
             Scanner scanner = new Scanner(System.in);
             System.out.print("Ingrese la altura del triángulo: ");
             int altura = scanner.nextInt();  // Leer altura
             for (int i = 1; i <= altura; i++) {  // Bucle externo
                 for (int j = 1; j <= i; j++) {  // Bucle interno
                     System.out.print("*");
                 }
                 System.out.println();  // Nueva línea al final de cada fila
             }
         }
     }
     ```

