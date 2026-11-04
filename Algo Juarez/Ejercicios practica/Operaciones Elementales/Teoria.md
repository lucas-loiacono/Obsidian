
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

El desglose línea por línea de las Operaciones Elementales (OE) para este **mejor caso**, tal como se anota en la imagen, es el siguiente:

- **Parámetros `(int[] vec, int dato)`:** 2 OE (1 por recibir la referencia de `vec` y 1 por recibir `dato`).
    
- **`int pos = -1, i = 0;`:** 2 OE (dos operaciones de asignación).
    
- **`int n = vec.length;`:** 1 OE (una asignación).
    
- **`while ((i < n) && (pos == -1))`:** 6 OE en total. Se anota como "3 + 3" porque la condición entera cuesta 3 OE (una comparación menor que, el AND lógico y la igualdad) y se evalúa dos veces: la primera da verdadero permitiendo entrar al ciclo, y la segunda evaluación da falso (porque `pos` ya cambió) forzando la salida del ciclo.
    
- **`if (vec[i] == dato)`:** 2 OE (un acceso al índice del arreglo y una comparación de igualdad).
    
- **`pos = i;`:** 1 OE (una asignación). Como estamos en el mejor caso y el dato se encuentra inmediatamente, esta línea sí se ejecuta.
    
- **`else i++;`:** 0 OE. Al haberse cumplido la condición del `if`, el programa ignora esta rama por completo.
    
- **`return pos;`:** 1 OE (por la instrucción de retorno de la función).
    

Sumando todos los valores de este único recorrido, el tiempo de ejecución exacto para el mejor caso es constante: $T(n) = 15$ O.E.


![[Pasted image 20260911182804.png]]

El 1 en el while se da ya que analiza la primera condición nomas, como ve que ya mi i = n deja de seguir con la siguiente condición y lo corta ahí
 
En el peor de los casos tienen que iterar por todo el vector hasta la ultima posición

El análisis línea por línea de las Operaciones Elementales (OE) para este **peor caso** (donde el dato no se encuentra en el arreglo) se estructura de la siguiente manera:

  

- **Parámetros `(int[] vec, int dato)`:** 2 OE (1 por recibir la referencia del arreglo y 1 por el entero).
    

- **`int pos = -1, i = 0;`:** 2 OE (dos asignaciones iniciales).
    

- **`int n = vec.length;`:** 1 OE (una asignación).
    
  
- **`while ((i < n) && (pos == -1))`:** 3 OE por cada iteración que entra al ciclo (una comparación menor que, un operador lógico AND y una comparación de igualdad).
    
 
- **`if (vec[i] == dato)`:** 2 OE por iteración (un acceso al índice del arreglo y una comparación).
    

- **`pos = i;`:** 0 OE. Al ser el peor caso, el dato nunca se encuentra, por lo que esta rama siempre se ignora.
    

- **`else i++;`:** 2 OE por iteración (una suma y una asignación).
    

- **Bloque del ciclo iterativo (`7 * n`):** La llave roja agrupa las operaciones internas repetitivas (3 del `while` + 2 del `if` + 2 del `i++`). Como el ciclo recorre los $n$ elementos del arreglo, el costo se multiplica resultando en $7 * n$.
    

- **Salida del ciclo (Cuadro azul con "1"):** 1 OE extraída con una flecha roja. En la última evaluación, `i` alcanza el valor de `n`, haciendo que `i < n` sea falso. Por evaluación de cortocircuito, el procesador omite la segunda mitad de la condición lógica, por lo que cortar el bucle cuesta solo 1 OE.
    

- **`return pos;`:** 1 OE (círculo azul inferior por la instrucción de retorno).


Al sumar las operaciones que se ejecutan una única vez (2+2+1 al inicio, 1 de corte del bucle y 1 de retorno) con el bloque iterativo, se obtiene la función final de tiempo de ejecución para el peor caso: $T(n) = 7n + 7$ O.E.

![[Pasted image 20260911183051.png]]


![[Pasted image 20260911184036.png]]

Los azules se ejecutan 1 sola vez, mientras que los amarillos depende de mi n

![[Pasted image 20260908194542.png]]

El código de la imagen muestra el algoritmo de ordenamiento por selección (Selection Sort). Al no tener las anotaciones manuales, el desglose teórico de Operaciones Elementales (OE) para el **peor caso** se realiza analizando cada estructura:

  

- **`public void ordenar (int v[], int n)`:** 2 OE (1 por recibir la referencia del arreglo y 1 por el entero).
    

- Bucle externo `for (int i = 0; i < n - 1; i++)`:
    
      
    - `int i = 0`: 1 OE (inicialización, se ejecuta una sola vez al inicio).
        
    - `i < n - 1`: 2 OE por evaluación (una resta y una comparación menor que).
        
    - `i++`: 2 OE por iteración (una suma y una asignación).
        
- Dentro del bucle externo:
    
      
    - `int posMin = i;`: 1 OE (asignación).
        
- Bucle interno `for (int j = i + 1; j < n; j++)`:
    
      
    - `int j = i + 1`: 2 OE por inicialización (una suma y una asignación).
        
    - `j < n`: 1 OE por evaluación (comparación).
        
    - `j++`: 2 OE por iteración (suma y asignación).
        
- Cuerpo del bucle interno (Peor caso):
    
      
    - `if (v[j] < v[posMin])`: 3 OE (dos accesos a los índices del arreglo y una comparación).
        
    - `posMin = j;`: 1 OE (asignación). En el peor escenario (si el vector estuviera ordenado en sentido inverso), esta condición siempre es verdadera y la asignación se ejecuta en todas las iteraciones.
        
- Llamada final del ciclo externo:
    
      
    - `inter(vec[], I, posMin);`: Invocar una función suma OE. Generalmente se cuenta 1 OE por la invocación y 1 OE por cada parámetro pasado (total de 4 OE en esta línea), más el costo interno que tenga dicha función de intercambio.
  

Al tener un bucle `for` anidado dentro de otro que depende de $n$, la cantidad de operaciones ejecutadas crece de manera cuadrática, lo que resulta en una función de tiempo $T(n)$ con complejidad $O(n^2)$.

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