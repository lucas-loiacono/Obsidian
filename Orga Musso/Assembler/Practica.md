![[Pasted image 20261105180858.png]]

![[Pasted image 20261105162021.png]]


- **`main: andcc %r3, %r0, %r3`**: Inicializa el registro `%r3` en 0. Este registro funcionará como el acumulador de la suma (equivalente a `SumaParcial=0;` en C).
    
      
    
- **`ld [length], %r1`**: Carga el tamaño total del array en bytes (el valor 20, ya que son 5 elementos de 4 bytes cada uno) en el registro `%r1`. Este registro se utilizará como un índice de desplazamiento que recorrerá el array de atrás hacia adelante.
    
      
    
- **`for: andcc %r1, %r1, %r0`**: Inicia el bucle y evalúa si el índice `%r1` ha llegado a 0. Hace una operación lógica AND sobre `%r1` y guarda el resultado en el registro nulo `%r0` solo para actualizar las banderas de estado del procesador.
    
      
    
- **`be done`**: Significa "Branch if Equal". Si la evaluación de la línea anterior determinó que `%r1` es igual a 0, el programa salta a la etiqueta `done` y sale del ciclo.
    
      
    
- **`addcc %r1, -4, %r1`**: Resta 4 al índice `%r1`. Como cada número en el array ocupa 4 bytes, esto retrocede una posición en la memoria para apuntar al elemento actual que se va a procesar (por ejemplo, en la primera iteración pasa de 20 a 16 para leer el último elemento).
    
      
    
- **`ld %r1,[arrayA],%r5`**: Carga en el registro `%r5` el valor que se encuentra en la dirección de memoria de `arrayA` más el desplazamiento (offset) indicado por `%r1`. Básicamente, lee el número actual del array.
    
      
    
- **`addcc %r3, %r5, %r3`**: Suma el valor del elemento recién cargado (`%r5`) al acumulador total (`%r3`) y actualiza el resultado en el mismo `%r3`.
    
      
    
- **`ba for`**: Significa "Branch Always". Es un salto incondicional que hace que el programa vuelva automáticamente a la etiqueta `for:` para repetir el proceso con el siguiente elemento.




# Por que r1 r1 r0

Es una excelente pregunta, porque la lógica de este ciclo `for` en ensamblador funciona "al revés" de lo que haríamos habitualmente en C.

  

**1. ¿Por qué se carga el valor 20 en `%r1`?** El valor 20 representa el tamaño total del arreglo en bytes. Como el arreglo tiene 5 números y cada uno ocupa 4 bytes en memoria, el total es 20 ($5 \times 4$).

  

En lugar de contar desde el elemento 0 hacia adelante (como hace `i = 0; i < 5` en C), este programa usa `%r1` como un contador de desplazamiento (offset) que arranca en el tamaño total y va retrocediendo hacia atrás. En cada vuelta del ciclo, a ese 20 se le restan 4 bytes (`addcc %r1, -4, %r1`) para ir leyendo el elemento anterior, hasta llegar al inicio del arreglo.

  

**2. ¿Por qué se hace `andcc %r1, %r1, %r0`?** Esta línea es el "chequeo de elementos restantes" del ciclo. Básicamente sirve para evaluar si el contador `%r1` finalmente llegó a 0 y es hora de salir del bucle:

  

- **`and`**: Hace una operación lógica AND de `%r1` consigo mismo. El resultado de hacer "A AND A" es simplemente el mismo valor original, no se altera nada.
    
      
    
- **`cc` (Condition Codes)**: Este sufijo le ordena al procesador que actualice sus "banderas de estado" internas, específicamente la bandera de Cero (Z), dependiendo del resultado de la operación.
    
      
    
- **`%r0`**: Es el registro destino. En esta arquitectura (SPARC), `%r0` es un registro que siempre vale 0 y descarta cualquier cosa que intentes guardar en él.
    
      
    

En resumen, `andcc %r1, %r1, %r0` es un truco clásico en ensamblador para "mirar" cuánto vale un registro sin gastar memoria para guardar el resultado. Si `%r1` llegó a 0, la operación da 0, se enciende la bandera de estado de Cero, y la instrucción que le sigue inmediatamente (`be done`, "salta si es igual a cero") detecta esa bandera y termina el programa saltando a la línea 2060.





# Saltos de bytes


Exactamente. Cada instrucción en este código ensamblador ocupa 32 bits, lo que equivale exactamente a 4 bytes de memoria.

  

Por eso puedes ver entre paréntesis a la derecha de cada línea cómo el contador de programa va avanzando de a 4 posiciones por cada instrucción ejecutada:

  

- La primera instrucción arranca en **2048** (pusiste un cero de más, pero la lógica es impecable).
    
      
    
- La segunda instrucción está en **2052**.
    
      
    
- La tercera (donde arranca el `for`) está en **2056**.
    
      
    
- El salto `be done` está en **2060**, y así sucesivamente.
    
      
    

Tener un tamaño fijo de 4 bytes por instrucción es típico de las arquitecturas tipo RISC para que el procesador pueda leer y decodificar el código de manera más rápida y predecible. ¡Lo dedujiste a la perfección!