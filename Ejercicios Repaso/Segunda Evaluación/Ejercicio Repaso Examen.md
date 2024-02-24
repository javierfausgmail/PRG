### Ejercicios Unidad 5. Arrays/Tablas:

Por supuesto, a continuación le proporciono 10 ejercicios de programación que abarcan el uso de arrays en Java, adecuados para sus alumnos del ciclo de grado superior de formación profesional de Desarrollo de Aplicaciones Multiplataforma.

1.  **Inicialización y Recorrido**: Escriba un programa que cree un array de 10 números enteros. Inicialice el array con valores del 1 al 10 y, luego, imprima estos valores utilizando un bucle `for`.
    
2.  **Promedio de Valores**: Cree un programa que calcule y muestre el promedio de una serie de valores almacenados en un array de `float`.
    
3.  **Mínimo y Máximo**: Desarrolle un programa que, dado un array de números enteros, encuentre el valor mínimo y el valor máximo y los muestre.
    
4.  **Inversión de un Array**: Implemente un método que reciba un array de enteros y lo devuelva con sus elementos en orden inverso.
    
5.  **Tabla de Multiplicar**: Realice un programa que genere e imprima una tabla de multiplicar hasta 10, utilizando arrays bidimensionales.
    
6.  **Búsqueda Secuencial**: Escriba un programa que implemente la búsqueda secuencial de un valor dentro de un array de enteros y muestre la posición en la que se encuentra.
    
7.  **Ordenación de Arrays**: Implemente el algoritmo de ordenación de burbuja para ordenar un array de números enteros de forma ascendente.
    
8.  **Filtrado de Elementos**: Cree un programa que dado un array de números enteros, cree un nuevo array que contenga solo los números pares del array original.
    
9.  **Arrays como Parámetros**: Escriba un método que reciba dos arrays de enteros y devuelva un nuevo array que sea la unión de los dos arrays recibidos.
    
10.  **Arrays Multidimensionales - Matrices**: Desarrolle un programa que cree una matriz de 5x5 enteros, la inicialice con valores aleatorios y luego muestre la suma de los elementos de cada fila y cada columna.
    

Estos ejercicios están diseñados para reforzar diferentes aspectos del trabajo con arrays en Java, desde la inicialización y recorrido, hasta operaciones más complejas como la búsqueda, ordenación y manipulación de arrays multidimensionales.

### Ejercicios que utilizan funciones y arrays:

1.  Enunciado: Eres el gerente de una tienda de comestibles y necesitas un programa para rastrear tus ventas. Crea una función "trackSales" que tome un array de números enteros, donde cada número representa las ventas de un día determinado. La función debe devolver la cantidad total de ventas. Además, crea una función "bestSalesDay" que devuelva el índice del día con las ventas más altas.
    
2.  Enunciado: Estás organizando un concurso de fotografía y necesitas una forma de calificar las entradas. Cada entrada recibe tres calificaciones de tres jueces diferentes, de 1 a 10. Crea una función "calculateAverageScore" que tome un array de tres números y devuelva la puntuación promedio. Además, crea una función "calculateFinalScore" que tome un array de arrays con las puntuaciones y devuelva un array con las puntuaciones promedio.
    
3.  Enunciado: Eres un investigador estudiando una especie particular de aves. Cada día cuentas el número de aves que ves y almacenas esa información en un array. Crea una función "getTotalBirds" que sume todos los números en el array y devuelva ese total. También, crea una función "getBusiestDay" que devuelva el índice del día en el que viste más aves.
    

### Ejercicios Unidad 7. Clases

Ejercicio 4. Diseñar una clase `Temporizador` que represente un cronómetro digital con horas, minutos y segundos. La clase debe disponer de:

- `Temporizador (int horas, int minutos, int segundos)`: que crea un objeto con los datos pasados como parámetros.
- `void incrementarSegundo()`: que incrementa el temporizador en un segundo.
- `void incrementarMinuto()`: que incrementa el temporizador en un minuto.
- `void incrementarHora()`: que incrementa el temporizador en una hora.
- `void mostrar()`: que muestra el tiempo del temporizador por consola.
- `boolean esIgual(Temporizador otroTemporizador)`: que determina si el temporizador invocante y el que se pasa como parámetro representan el mismo momento del tiempo.

Realice una prueba del funcionamiento de la clase y sus métodos en un `main()`.

Ejercicio 5. Crear una clase `Libro` que represente la información de un libro. Incluya:

- Atributos para el título, autor, año de publicación y número de páginas.
- Un constructor que inicialice esos datos.
- Métodos para obtener y modificar cada uno de los atributos.
- Un método `toString()` que devuelva una cadena con toda la información del libro.

Implemente un pequeño programa en `main()` que cree un objeto `Libro` y muestre su información.

Ejercicio 6. Escribir la clase `Caja` que representa una caja rectangular con largo, ancho y altura, incluya:

- Un constructor que reciba y asigne las dimensiones de la caja.
- Métodos para calcular y devolver el volumen y el área superficial de la caja.
- Un método que compare si el volumen de la caja invocante es mayor que otra caja pasada como parámetro.

Testee los métodos en un `main()`.

Ejercicio 7. Desarrollar una clase `Círculo` que modele un círculo mediante un radio, incluir:

- Un constructor para inicializar el radio.
- Métodos para calcular el área y el perímetro del círculo.
- Un método que determine si el círculo actual es igual en área a otro círculo.

Compruebe el funcionamiento de la clase con un método `main()`.

Ejercicio 8. Implementar una clase `Contador` que simule un contador de personas, que incluya:

- Un constructor sin parámetros que inicie el contador en cero.
- Métodos para incrementar y decrementar el contador.
- Un método para reiniciar a cero el contador.
- Un método que muestre el valor actual del contador.

Utilice esta clase en un método `main()` para simular la entrada y salida de personas en una tienda.

Ejercicio 9. Diseñar una clase `Conjunto` que represente un conjunto de números enteros con operaciones de:

- Añadir y eliminar elementos del conjunto.
- Verificar si un elemento pertenece al conjunto.
- Unión y intersección con otro conjunto.
- Un método `toString()` para mostrar el conjunto.

Demuestre su uso en un `main()`.

Ejercicio 10. Crear una clase `Vehículo` con atributos para la marca, modelo y kilometraje y:

- Un constructor que inicialice la marca y el modelo.
- Métodos para obtener y modificar el kilometraje.
- Un método para imprimir los datos del vehículo.

Realizar pruebas de estos métodos en `main()`.

Ejercicio 11. Desarrollar una clase `Estudiante` que modele la información de un alumno, con:

- Atributos para nombre, DNI y calificaciones.
- Un constructor para inicializar los datos.
- Métodos para modificar y obtener los datos del estudiante.
- Un método para calcular el promedio de sus calificaciones.

Probar la clase en un `main()`.

Ejercicio 12. Implementar una clase `Agenda` que gestione los contactos telefónicos, con métodos para:

- Añadir, eliminar y buscar contactos.
- Mostrar todos los contactos.
- Cargar y guardar los contactos en un archivo.

Escriba un `main()` para demostrar su funcionamiento.


Ejercicio 13. Estás construyendo un sistema para una biblioteca.
Cada libro tiene un número de páginas y una clasificación de 1 a 5. Los libros están almacenados como un array de objetos, donde cada objeto tiene un número de páginas y una clasificación. Crea una función "findBestBook" que encuentre el libro con la clasificación más alta y devuelva el número de páginas de ese libro. También, crea una función "findWorstBook" que encuentre el libro con la clasificación más baja y devuelva el número de páginas de ese libro.

Escriba un `main()` para demostrar su funcionamiento.


### Ejercicios Unidad 8. Herencia


1. Diseñar la clase Hora que representa un instante de tiempo compuesto por una hora (de 0 a 23) y los minutos.

Dispone de los métodos:

·       inc ( ) , que incrementa la hora en un minuto.

·       setMinutos (valor), que asigna un valor, entre O y 59, a los minutos.

·       setHora(valor) , que asigna un valor, entre 0 y 23, a la hora.

·       toString(), que devuelve un String con la representación del reloj.

2.      Escribir la clase Hora, que funciona de forma similar a la clase Hora, con la diferencia de que las horas solo pueden tomar un valor entre la 1 y las 12; y se distingue la mañana de la tarde mediante 'am" y "pm".

3.      A partir de la clase Hora implementar la clase HoraExacta, que incluye en la hora los segundos. Además de los métodos visibles de Hora dispondrá de:

·       HoraExacta(hora, minuto, segundo), que construye un objeto con los datos pasados como parámetros.

·       setSegundo (valor), que asigna el valor indicado, entre 0 y 59, al atributo segundos.

·       Inc() que incrementa la hora en un segundo.

4.      Añadir a la clase HoraExacta un método que compare si dos horas (la invocante y otra pasada como parámetro de entrada al método) son iguales o distintas.

5.      Crear la clase Instrumento que cs una clase abstracta que almacena un máximo de 100 notas musicales. Mientras haya sitio es posible añadir nuevas notas musicales, al final, con el método add(). La clase también dispone del método abstracto interpretar() que en cada subclase que herede de Instrumento, mostrará por consola las notas musicales según las interprete. Utilizar enumerados para definir las notas musicales.

6.      Crear Plas clases Piano y Campana que heredan de la clase Instrumento.


Ejercicio 7. Desarrolle una clase abstracta `DispositivoElectronico` con un método abstracto `encender()`. A partir de esta, derive clases como `Smartphone` y `Tablet`, implementando el método `encender()` y añadiendo atributos como `tamañoPantalla` o `memoriaRAM`.

Ejercicio 8. Implemente una clase `Vehiculo` con atributos para marca, modelo y número de ruedas. A partir de esta, derive dos clases: `Coche` y `Moto`, añadiendo atributos específicos como `numPuertas` para `Coche` y `tieneSidecar` para `Moto`. Para cada clase, implemente métodos `toString()` y `equals()`.

Ejercicio 9. Defina la clase `Figura` con atributos para color y nombre. Derive dos clases: `Circulo` y `Rectangulo`, que añadan sus atributos específicos (radio para `Circulo` y lado para `Rectangulo`). Implemente un método `area()` en la clase `Figura` y sobrescríbalo en las clases hijas.

Ejercicio 10. Cree una clase `Empleado` con información básica del empleado. Derive dos clases: `Programador` y `Analista`, añadiendo atributos como `lenguajesDominados` para `Programador` y `proyectosDirigidos` para `Analista`. Implemente un método `mostrarInformacion()` en cada clase.

Ejercicio 11. Desarrolle una clase abstracta `InstrumentoMusical` con un método abstracto `tocar()`. A partir de esta, cree clases como `Guitarra` y `Piano`, que implementen el método `tocar()` de manera específica para cada instrumento.

Ejercicio 12. Cree una clase `Electrodomestico` con atributos de consumo energético y categoría. Derive clases como `Lavadora` y `Refrigerador`, agregando atributos y métodos específicos, como `capacidad` para `Lavadora` y `temperaturaMinima` para `Refrigerador`.

Ejercicio 13. Implemente una clase `Animal` con un método `emitirSonido()`. Derive clases como `Perro` y `Gato`, sobrescribiendo el método `emitirSonido()` para cada animal con sonidos característicos.

Ejercicio 14. Diseñe una clase `Producto` con un precio base y un método `calcularPrecioFinal()`. Derive clases como `ProductoFresco` y `ProductoCongelado`, sobrescribiendo el método `calcularPrecioFinal()` considerando características como la fecha de envasado y la temperatura de mantenimiento, respectivamente.

Ejercicio 15. Defina una clase abstracta `FormaGeometrica` con un método abstracto `calcularPerimetro()`. Derive clases como `Triangulo` y `Cuadrado`, implementando el método `calcularPerimetro()` según las propiedades de cada forma.

Ejercicio 16. Cree una clase `CuentaBancaria` con métodos para depositar y retirar dinero. Derive clases como `CuentaAhorro` y `CuentaCorriente`, añadiendo funcionalidades específicas como calcular intereses en `CuentaAhorro` y un método para emitir cheques en `CuentaCorriente`.




