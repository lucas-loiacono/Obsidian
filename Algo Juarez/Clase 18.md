![[Pasted image 20261026012655.png]]

![[Pasted image 20261026013826.png]]

Es poner claves en un lugar reducido, pero de manera uniforme, tener una buena dispersión equilibrada en la distribución de las claves 

![[Pasted image 20261026014000.png]]

![[Pasted image 20261026014252.png]]

![[Pasted image 20261026014335.png]]

![[Pasted image 20261026014415.png]]

Hay hash cerrado y hash abierto, el cerrado es aquel que tiene un tamaño fijo, mientras que el abierto no, en el caso del cerrado puede ser un array

![[Pasted image 20261026014606.png]]

Mi funcion es donde entra mi clave a guardar y esta decide donde y como se guarda

![[Pasted image 20261026014650.png]]

Casi siempre se busca mi M, poniendo a lambda con 0,8 y pasando de lado la m en la ecuación

![[Pasted image 20261026014918.png]]

osea yo voy a tener varias claves y si por ejemplo lo quiero meter en un vector, lo que hago es que todas las claves compartan el mismo comportamiento o base, es como un cambio de base de sistemas numericos practicamente


Transformar las claves aplicándoles una función matemática uniforme asegura que cualquier dato, sin importar su formato original, aterrice en una posición predecible dentro de tu vector.

  

Pensarlo como un cambio de base numérica es una analogía muy precisa. Al igual que cuando resolvés conversiones de base-N, al usar el método ASCII estás tomando una cadena de caracteres y evaluándola prácticamente como un polinomio en base 128 para obtener un único valor entero. Todos los elementos que quieras guardar deben someterse a esta misma regla algorítmica para mantener la coherencia del sistema.

  

Una vez que obtenés ese número entero representativo, la función de división (el operador módulo) actúa como un límite. Si implementaste un vector con capacidad para 31 posiciones, aplicar el módulo 31 a ese entero gigante fuerza al resultado a caer exactamente en un índice válido entre 0 y 30. El único desafío de meter toda esta información en un mismo vector es que distintas claves originales pueden terminar calculando el mismo índice final. Esto genera una colisión, lo que exige programar una estrategia secundaria dentro de la estructura de datos para acomodar ambos valores sin sobreescribir la memoria.

![[Pasted image 20261026015009.png]]

![[Pasted image 20261026015022.png]]

![[Pasted image 20261026015343.png]]

![[Pasted image 20261026015550.png]]

![[Pasted image 20261026015700.png]]

![[Pasted image 20261026015724.png]]

![[Pasted image 20261026015815.png]]

![[Pasted image 20261026015938.png]]

![[Pasted image 20261026020130.png]]

![[Pasted image 20261026020151.png]]

Para cada clave uso funciones randoms de mi bolsa, como las que recién vimos, esto funciona mejor para que no haya colisiones

![[Pasted image 20261026020404.png]]

![[Pasted image 20261026020726.png]]

![[Pasted image 20261026020742.png]]

![[Pasted image 20261026020839.png]]

![[Pasted image 20261026020904.png]]

![[Pasted image 20261026020923.png]]

![[Pasted image 20261026020934.png]]

![[Pasted image 20261026020946.png]]


![[Pasted image 20261026020958.png]]

![[Pasted image 20261026021050.png]]

![[Pasted image 20261026021100.png]]

![[Pasted image 20261026021113.png]]

![[Pasted image 20261026021209.png]]

cuando las colisiones empiezan a repetirse con el método cuadrático, este método deja de funcionar, ya que usándolo van a parar las nuevas al mismo lugar que las demás

![[Pasted image 20261026021318.png]]

![[Pasted image 20261026021413.png]]

![[Pasted image 20261026021454.png]]

![[Pasted image 20261026021521.png]]

![[Pasted image 20261026021719.png]]

![[Pasted image 20261026021853.png]]

![[Pasted image 20261026022016.png]]

![[Pasted image 20261026021914.png]]

![[Pasted image 20261026022107.png]]

![[Pasted image 20261026022130.png]]

**Hash abierto (chaining)**

  

- Cada posición de la tabla hash actúa en realidad como un puntero dirigido hacia una lista enlazada que contiene las claves.
    
      
    
- Cuando múltiples claves obtienen el mismo valor al aplicarles la función de hash, se encadenan sucesivamente en la misma posición.
    
      
    
- Siguiendo el orden de ingreso del ejemplo (A, H, E, T, F y B), las claves A, E y F colisionan en el valor 1 y forman una cadena, las claves T y B forman otra cadena en el valor 3, y la H se ubica en el valor 4.
    
      
    

**Bucket addressing**

  

- En lugar de listas externas, este método utiliza una estructura de matriz para que varios elementos se almacenen directamente en una misma posición de la tabla.
    
      
    
- A cada posición se la denomina "bucket", ya que funciona como un bloque rígido capaz de contener múltiples elementos en su interior.
    
      
    
- Aplicado al mismo conjunto de datos, los elementos que colisionan en el índice 1 (A, E, F) se acomodan en las columnas disponibles dentro de esa misma fila de la matriz, repitiendo el comportamiento para T y B en la fila 3.

![[Pasted image 20261026022214.png]]



![[Pasted image 20261026023029.png]]

![[Pasted image 20261026023010.png]]

Para resolver este ejercicio de direccionamiento abierto (asumiendo exploración lineal o "linear probing", que es el estándar al no especificarse otro método), la función hash es $h(k) = k \pmod{11}$, utilizando una tabla con índices del 0 al 10.

  

**Estado inicial** Tabla vacía con 11 posiciones (0 a 10).

  

**insertar(37)**

  

- Cálculo: $37 \pmod{11} = 4$.
    
      
    
- Acción: La posición 4 está libre. Se inserta el 37.
    
      
    
- Tabla: `[4]=37`
    
      
    

**insertar(12)**

  

- Cálculo: $12 \pmod{11} = 1$.
    
      
    
- Acción: La posición 1 está libre. Se inserta el 12.
    
      
    
- Tabla: `[1]=12, [4]=37`
    
      
    

**insertar(8)**

  

- Cálculo: $8 \pmod{11} = 8$.
    
      
    
- Acción: La posición 8 está libre. Se inserta el 8.
    
      
    
- Tabla: `[1]=12, [4]=37, [8]=8`
    
      
    

**insertar(26)**

  

- Cálculo: $26 \pmod{11} = 4$.
    
      
    
- Acción: La posición 4 está ocupada por el 37 (colisión). Se busca la siguiente posición libre secuencialmente. La posición 5 está libre. Se inserta el 26 en el índice 5.
    
      
    
- Tabla: `[1]=12, [4]=37, [5]=26, [8]=8`
    
      
    

**eliminar(37)**

  

- Cálculo: $37 \pmod{11} = 4$.
    
      
    
- Acción: Se encuentra el 37 en la posición 4. Al usar direccionamiento abierto, no se deja la celda totalmente vacía, sino que se marca con una bandera de "Borrado" (o "Tombstone"). Esto es crucial para no cortar la cadena de búsqueda de elementos que colisionaron previamente (como el 26).
    
      
    
- Tabla: `[1]=12, [4]=BORRADO, [5]=26, [8]=8`
    
      
    

**insertar(34)**

  

- Cálculo: $34 \pmod{11} = 1$.
    
      
    
- Acción: La posición 1 está ocupada por el 12 (colisión). Se verifica la posición siguiente. La posición 2 está libre. Se inserta el 34 en el índice 2.
    
      
    
- Tabla: `[1]=12, [2]=34, [4]=BORRADO, [5]=26, [8]=8`
    
      
    

**buscar(26)**

  

- Cálculo: $26 \pmod{11} = 4$.
    
      
    
- Acción: Se revisa la posición 4. Se encuentra la marca "BORRADO". Como no es una celda vacía original, el algoritmo sabe que debe seguir buscando. Avanza a la posición 5 y encuentra el 26 exitosamente.