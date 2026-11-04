
![[Pasted image 20260908190740.png]]

![[Pasted image 20260908190816.png]]

![[Pasted image 20260908190928.png]]

![[Pasted image 20260908191821.png]]

El desglose del código contabiliza las operaciones elementales (OE) línea por línea para calcular el costo total de ejecución:

  

- **`int a, b = 5;` (1 OE):** Cuenta como una sola operación por la asignación del valor 5 a la variable `b`.
    
- **`a = b + 1;` (2 OE):** Requiere dos operaciones sucesivas porque primero se resuelve la operación aritmética (`b + 1`) y luego se realiza la asignación del resultado a la variable `a`.
    
- **`a++;` (2 OE):** Al ser lógicamente equivalente a `a = a + 1`, el procesador debe ejecutar una suma aritmética y luego una asignación para actualizar el valor en memoria.

La notación **$T(n)$** se lee como "Tiempo en función de $n$" e indica el tiempo total de ejecución. Representa la función matemática que describe cuántas operaciones realizará un algoritmo dependiendo del tamaño de su entrada de datos ($n$). En este ejemplo, como no existen bucles iterativos ni parámetros que modifiquen la cantidad de instrucciones ejecutadas, el bloque tiene un costo estrictamente constante, sumando un total final de $T(n) = 5$ O.E.. Dominar la construcción de esta función es la base para analizar la complejidad asintótica al diseñar algoritmos y estructuras de datos.

![[Pasted image 20260908191849.png]]

![[Pasted image 20260908191902.png]]

- **`int a, b = 2;` (1 OE):** Contabiliza una operación por la asignación del valor 2 a la variable `b`.
    
- **`a = ingreso("...");` (1 OE):** Se cuenta como una sola operación por la asignación del valor retornado a la variable `a`.
    
- **`if (a > 5)` (1 OE):** Representa una única operación por la comparación lógica requerida para evaluar la condición.
    
- **Bloque `if` (4 OE totales):** Si la condición es verdadera, se ejecutan `a = a + 3;` (2 OE por una suma y una asignación) y `b = a + 1;` (2 OE por otra suma y asignación).
    
- **Bloque `else` (1 OE total):** Si la condición es falsa, únicamente se ejecuta `b = 1;` (1 OE por la asignación)


![[Pasted image 20260908191926.png]]


![[Pasted image 20260908192044.png]]

el caso promedio depende de la cantidad de veces que entre en el if o en el else

OE = operaciones elementales

Mejor caso = 4 y peor caso = 7, tengo que calcular mi probabilidad de salir en cada caso por el caso

por ejemplo el 90% de los casos cae en 4 y el 10% cae en 7
4 x 0.9 o 7 x 0.1


![[Pasted image 20260908192407.png]]


![[Pasted image 20260911182337.png]]
En total = 15

En el mejor caso

Acceder al vector cuesta 1 y luego igualar cuesta otro

El while es una vez que entra, luego de cumplir 1 ciclo lo vuelve a examinar la condición (en el mejor caso)

![[Pasted image 20260911182804.png]]

El 1 en el while se da ya que analiza la primera condición nomas, como ve que ya mi i = n deja de seguir con la siguiente condición y lo corta ahí
 
En el peor de los casos tienen que iterar por todo el vector hasta la ultima posición

![[Pasted image 20260911183051.png]]


![[Pasted image 20260911184036.png]]

Los azules se ejecutan 1 sola vez, mientras que los amarillos depende de mi n

![[Pasted image 20260908194542.png]]

![[Pasted image 20260908194811.png]]

![[Pasted image 20260908195010.png]]

![[Pasted image 20260911184459.png]]

Le pongo que es 9n ya que le hago una cota superior, como le puedo hacer una mucho mas grande como una mucho mas chica, pero nos alejamos del orden exacto

![[Pasted image 20260911184937.png]]

Acá tenemos el orden exacto que es 7n+7 

También podemos poner 5n ya que una constante cualquiera multiplicado por mi orden tiene que ser mas grande que mi orden exacto, entonces si yo tengo 5n y lo multiplico por 2 me da 10n que también funciona como techo
Por esta razón lo que se hace es sacar todas las constantes y poner la n sola, en este caso O(n)

![[Pasted image 20260911185302.png]]

![[Pasted image 20260911185812.png]]

de todas estas me quedo con n^2 

![[Pasted image 20260911185900.png]]

![[Pasted image 20260911190539.png]]

Una puede ser el orden de la otra, ya que se multiplican por una constante y el orden de las dos son O(n^2)


![[Pasted image 20260911190904.png]]

Con la suma de los algoritmos me tengo que quedar con el mas grande

![[Pasted image 20260911191015.png]]

# Anidados ->  se multiplica


![[Pasted image 20260911191557.png]]

![[Pasted image 20260911191840.png]]

![[Pasted image 20260911191935.png]]

![[Pasted image 20260911191955.png]]

![[Pasted image 20260911192052.png]]

![[Pasted image 20260911192138.png]]

![[Pasted image 20260911192254.png]]


![[Pasted image 20260911192440.png]]

es lo mismo, ya que si tengo una constante lo multiplico por 1/100 y me queda mas chico que el de arriba


![[Pasted image 20260911192530.png]]

![[Pasted image 20260911192642.png]]

acá lo que pasa es que si lo multiplico por un numero tiene que ser cota inferior y si lo multiplico por otro numero tiene que ser cota superior
si a n^2 lo multiplico por 1/100 me da una cota inferior y si lo multiplico por 100 me da una superior

![[Pasted image 20260911193505.png]]

![[Pasted image 20260911193515.png]]


![[Pasted image 20260911193542.png]]

![[Pasted image 20260911193556.png]]

![[Pasted image 20260911193251.png]]