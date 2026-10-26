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