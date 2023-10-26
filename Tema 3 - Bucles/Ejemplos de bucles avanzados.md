A continuación, se presentan enunciados y soluciones para casos de uso más avanzados de bucles `while`, `do-while` y `for`:

### 1. **Uso Avanzado de Bucles**
#### a. **Bucle `while`**:
   - **Enunciado**: Crear un programa que calcule el factorial de un número ingresado por el usuario utilizando un bucle `while`.
   - **Solución**:
     ```java
     import java.util.Scanner;

     public class FactorialWhile {
         public static void main(String[] args) {
             Scanner scanner = new Scanner(System.in);
             System.out.print("Ingrese un número para calcular su factorial: ");
             int numero = scanner.nextInt();  // Leer número
             int factorial = 1;
             int i = 1;
             while (i <= numero) {  // Condición de continuación
                 factorial *= i;  // Calcular factorial
                 i++;  // Incrementar contador
             }
             System.out.println("El factorial de " + numero + " es: " + factorial);
         }
     }
     ```

#### b. **Bucle `do-while`**:
   - **Enunciado**: Crear un programa que permita al usuario ingresar números hasta que la suma de los números ingresados alcance o exceda 100.
   - **Solución**:
     ```java
     import java.util.Scanner;

     public class SumaDoWhile {
         public static void main(String[] args) {
             Scanner scanner = new Scanner(System.in);
             int suma = 0;
             do {
                 System.out.print("Ingrese un número: ");
                 int numero = scanner.nextInt();  // Leer número
                 suma += numero;  // Acumular suma
             } while (suma < 100);  // Condición de salida
             System.out.println("La suma de los números ingresados es: " + suma);
         }
     }
     ```

#### c. **Bucle `for`**:
   - **Enunciado**: Crear un programa que imprima una pirámide de números del 1 al número ingresado por el usuario, donde cada fila tiene un número más que la fila anterior.
   - **Solución**:
     ```java
     import java.util.Scanner;

     public class PiramideFor {
         public static void main(String[] args) {
             Scanner scanner = new Scanner(System.in);
             System.out.print("Ingrese la altura de la pirámide: ");
             int altura = scanner.nextInt();  // Leer altura
             int numero = 1;
             for (int i = 1; i <= altura; i++) {  // Bucle externo
                 for (int j = 1; j <= i; j++) {  // Bucle interno
                     System.out.print(numero + " ");
                     numero++;  // Incrementar número
                 }
                 System.out.println();  // Nueva línea al final de cada fila
             }
         }
     }
     ```

### 2. **Uso Combinado de `break` y Bucles**:
   - **Enunciado**: Crear un programa que encuentre y muestre el primer número primo mayor que 100.
   - **Solución**:
     ```java
     public class PrimoMayor100 {
         public static void main(String[] args) {
             int numero = 101;  // Iniciar búsqueda en 101
             while (true) {  // Bucle infinito
                 boolean esPrimo = true;
                 for (int i = 2; i <= numero / 2; i++) {
                     if (numero % i == 0) {
                         esPrimo = false;  // No es primo
                         break;  // Salir del bucle for
                     }
                 }
                 if (esPrimo) {
                     System.out.println("El primer número primo mayor que 100 es: " + numero);
                     break;  // Salir del bucle while
                 }
                 numero++;  // Incrementar número
             }
         }
     }
     ```

Estos ejemplos presentan situaciones más complejas que requieren un buen entendimiento del control de flujo y la lógica de los bucles en Java.