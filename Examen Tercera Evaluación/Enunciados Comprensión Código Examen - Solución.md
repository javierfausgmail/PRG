### ¿Qué hace este código?

```java
import java.util.*;

public class Ejercicio {
    public static List<String> metodoA(List<String> listaStrings) {
        Set<String> conjuntoStrings = new HashSet<>();
        List<String> lista = new ArrayList<>();
        for (String str : listaStrings) {
            if (conjuntoStrings.add(str)) {
                lista.add(str);
            }
        }
        return lista;
    }

    public static void main(String[] args) {
        List<String> listaOriginal = Arrays.asList("Juan", "Ana", "Pedro", "Ana", "Juan");
        List<String> resultado = metodoA(listaOriginal);
        System.out.println(resultado);
    }
}
```

### Solución con Explicación Esperada del Alumno

Este código toma una lista de cadenas y elimina los duplicados, manteniendo solo la primera aparición de cada elemento. Primero, recorre la lista original y agrega cada cadena a un conjunto. Si la cadena no estaba ya en el conjunto, también se agrega a una nueva lista. Finalmente, devuelve la lista sin duplicados.

[Juan, Ana, Pedro]

### ¿Qué hace este código?

```java
import java.util.*;
import java.util.function.*;
import java.util.stream.*;

public class Ejercicio {
    public static List<Integer> metodoF(List<Integer> listaNumeros) {
        Function<Integer, Integer> funcion = n -> n + 10;
        return listaNumeros.stream()
                           .map(funcion)
                           .collect(Collectors.toList());
    }

    public static void main(String[] args) {
        List<Integer> lista = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> resultado = metodoF(lista);
        System.out.println(resultado);
    }
}
```

### Solución con Explicación Esperada del Alumno

Este código toma una lista de enteros y aplica una función a cada elemento que suma 10 al valor original. La función se define como una expresión lambda (`n -> n + 10`). El resultado es una lista con cada número incrementado en 10.

[11, 12, 13, 14, 15]

### ¿Qué hace este código?

```java
import java.util.*;
import java.util.stream.*;

public class Ejercicio {
    public static int metodoI(List<Integer> listaNumeros) {
        return listaNumeros.stream()
                           .reduce(0, Integer::sum);
    }

    public static void main(String[] args) {
        List<Integer> lista = Arrays.asList(1, 2, 3, 4, 5);
        int resultado = metodoI(lista);
        System.out.println(resultado);
    }
}
```

### Solución con Explicación Esperada del Alumno
Este código suma todos los elementos de una lista de enteros utilizando la operación de reducción de Streams en Java. La función `reduce` se inicializa con un valor inicial de 0 y utiliza el método de referencia `Integer::sum` para sumar los números de la lista. La operación de reducción procesa secuencialmente cada elemento, acumulando el resultado hasta que todos los elementos han sido procesados, y finalmente retorna el resultado total.

**Resultado:** 15


#### ¿Qué hace este código?

```java
import java.util.*;
import java.util.stream.*;

public class Ejercicio {
    public static List<String> metodoG(List<String> listaStrings) {
        return listaStrings.stream()
                           .filter(s -> s.length() > 3)
                           .sorted()
                           .collect(Collectors.toList());
    }

    public static void main(String[] args) {
        List<String> listaOriginal = Arrays.asList("pear", "apple", "fig", "banana", "kiwi");
        List<String> resultado = metodoG(listaOriginal);
        System.out.println(resultado);
    }
}
```

### Solución con Explicación Esperada del Alumno

Este código toma una lista de cadenas y filtra aquellas que tienen una longitud mayor a 3 caracteres. Luego, ordena las cadenas filtradas alfabéticamente y las recopila en una nueva lista. La lista resultante se devuelve y se imprime.

[apple, banana, kiwi, pear]