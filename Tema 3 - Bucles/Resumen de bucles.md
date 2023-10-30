**Bucles**
Los bucles son estructuras que permiten repetir bloques de código hasta que se cumpla una condición o se cumplan varias iteraciones.

**3.1. Bucles controlados por condición**
Estos bucles repiten bloques de código mientras una condición sea verdadera.

**3.1.1. while**
Repite un bloque de código mientras la condición sea verdadera.
```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

**3.1.2. do-while**
Ejecuta el bloque de código al menos una vez y luego repite mientras la condición sea verdadera.
```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);
```

**3.2. Bucles controlados por contador: for**
Repite un bloque de código un número específico de veces.
```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

**3.3. Salidas anticipadas**
Permite salir de un bucle antes de que se cumpla la condición principal utilizando `break`.
```java
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    System.out.println(i);
}
```

**3.4. Bucles anidados**
Son bucles dentro de bucles, utilizados comúnmente para trabajar con estructuras bidimensionales.

**3.4.1. Bucles independientes**
Cuando el bucle interno no depende del contador del bucle externo.
```java
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        System.out.println(i + ", " + j);
    }
}
```

**3.4.2. Bucles dependientes**
Cuando el comportamiento del bucle interno depende del contador del bucle externo.
```java
for (int i = 0; i < 3; i++) {
    for (int j = 0; j <= i; j++) {
        System.out.println(i + ", " + j);
    }
}
```

