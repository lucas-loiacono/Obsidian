
![[Pasted image 20261023004142.png]]

![[Pasted image 20261023004226.png]]

![[Pasted image 20261023004405.png]]

![[Pasted image 20261023004530.png]]

![[Pasted image 20261023004642.png]]

![[Pasted image 20261023005004.png]]

![[Pasted image 20261023005136.png]]

![[Pasted image 20261023011954.png]]

![[Pasted image 20261023012202.png]]

![[Pasted image 20261023012724.png]]

![[Pasted image 20261023012819.png]]

Esto seria como las materias y las correlativas, ya que varias flechas de materias se necesitan para poder cursar la correlativa

![[Pasted image 20261023013620.png]]

![[Pasted image 20261023013708.png]]

tengo que conectar todos los pares de vértices

![[Pasted image 20261023014055.png]]

Formula para calcular los vertices

![[Pasted image 20261023014125.png]]

Para 5 vertices

![[Pasted image 20261023014611.png]]

![[Pasted image 20261023014910.png]]

![[Pasted image 20261023015223.png]]

![[Pasted image 20261023015436.png]]

![[Pasted image 20261023015954.png]]

![[Pasted image 20261023020106.png]]

![[Pasted image 20261023020350.png]]

![[Pasted image 20261023020427.png]]

Ahi lo converti en un arbol

![[Pasted image 20261023020214.png]]

![[Pasted image 20261023020226.png]]

Sigue siendo conexo


![[Pasted image 20261023020308.png]]

Esto seria un bosque


![[Pasted image 20261023020506.png]]

![[Pasted image 20261023020653.png]]


![[Pasted image 20261023020922.png]]

Si no tiene direcciones queda una matriz simétrica



![[Pasted image 20261023022147.png]]

Cuando hay una matriz con muchos ceros, por ejemplo que tenga muchos vertices pero que tenga pocas aristas, es mas mejor usar la lista de adyacencia, ya que me da mas información justa

Hago un cuadrado para cada vertice y los conecto a cuales esta conectado

![[Pasted image 20261023022308.png]]

Aca puedo elegir arrancar en orden alfabético para que sea mas cómodo, cuando arranco de A voy para B, y como es en profundidad tengo que seguir por el mismo camino

![[Pasted image 20261023023505.png]]

No tengo que volver a B porque ya lo visite, vuelvo pasos hacia atrás (back tracking, lo mismo que en los arboles) y agarro la siguiente rama

![[Pasted image 20261023023747.png]]

Para el back tracking lo puedo hacer con una pila

![[Pasted image 20261023023844.png]]

Una vez que ya recorrí las dos ramas de A, me siguen faltando nodos para recorrer, entonces elijo alguno de esos para seguir, pero los elijo en orden alfabético, voy a F, después a G  y luego a H

![[Pasted image 20261023024121.png]]

![[Pasted image 20261023024342.png]]

La matriz de adyacencia se lee primero arrancando con la A, como la A se conecta con el B, bajo a la fila de B  y veo con quien se conecta, B se conecta con E, bajo a la tabla del E y sigo viendo con quien se conecta, veo que se conecta con D, bajo a la tabla de D y veo que se conecta con E y B, dos que ya recorri

![[Pasted image 20261023024640.png]]

Voy marcando los vertices que ya recorri, y luego recorro los que no 

![[Pasted image 20261023024725.png]]

![[Pasted image 20261023024756.png]]

Voy marcando, visitando y saltando de la misma manera


![[Pasted image 20261023024933.png]]

Para recorrido en ancho se usa Cola 

![[Pasted image 20261023025339.png]]

De A voy a B y C

De B voy a E y a nada mas

De C no puedo ir a ningún lado, esto depende de que lado o que rama elija primero para recorrer

![[Pasted image 20261023025522.png]]

![[Pasted image 20261023025623.png]]

Para mi tabla voy marcando, pero tengo que terminar la fila y después saltar, como marque primero B al final salto hacia su fila y sigo, una vez que termino con la de B no tengo que saltar a la de E, sino que volver a C, la otra rama de A. Voy por ramas

![[Pasted image 20261023025836.png]]

Lo mismo con esto, voy por ramas

![[Pasted image 20261023025913.png]]

![[Pasted image 20261023030149.png]]

![[Pasted image 20261023030422.png]]

Cuento por cuanta cantidad de flechas esta señalado cada vertice

Hacemos una lista con todos los vertices que tienen grado 0

![[Pasted image 20261023030631.png]]

tacho la primera que seria calzón, y le bajo un grado a los que Calzón señalaba 

Ahora mi pantalón tiene grado 0, voy y lo agrego a la lista de todos los que tienen grado 0

![[Pasted image 20261023030746.png]]

Ahora saco a medias, que es el siguiente, y hago el mismo algoritmo

![[Pasted image 20261023030844.png]]

y así con el resto

![[Pasted image 20261023030925.png]]

![[Pasted image 20261023031046.png]]c

![[Pasted image 20261023031107.png]]

y así es un posible orden de procesamiento