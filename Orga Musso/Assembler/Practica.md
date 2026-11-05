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







# Saltos de bytes


Exactamente. Cada instrucción en este código ensamblador ocupa 32 bits, lo que equivale exactamente a 4 bytes de memoria.

  

Por eso puedes ver entre paréntesis a la derecha de cada línea cómo el contador de programa va avanzando de a 4 posiciones por cada instrucción ejecutada:

  

- La primera instrucción arranca en **2048** (pusiste un cero de más, pero la lógica es impecable).
    
      
    
- La segunda instrucción está en **2052**.
    
      
    
- La tercera (donde arranca el `for`) está en **2056**.
    
      
    
- El salto `be done` está en **2060**, y así sucesivamente.
    
      
    

Tener un tamaño fijo de 4 bytes por instrucción es típico de las arquitecturas tipo RISC para que el procesador pueda leer y decodificar el código de manera más rápida y predecible. ¡Lo dedujiste a la perfección!