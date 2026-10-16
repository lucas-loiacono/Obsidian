![[Pasted image 20261015162309.png]]

yo si tengo 1000 datos voy a tener 10 niveles, por lo cual si yo quiero consultar voy a tener que recorrer como mucho 10 nodos si esta bien balanceado. por lo cual es Log2(N) 

si no esta balanceado y queda como el primero, ósea una lista, en mi peor caso voy a tener que recorrer O(N)


![[Pasted image 20261015162833.png]]

![[Pasted image 20261015163845.png]]

recorrido en ancho: se recorre por niveles y de izquierda a derecha

![[Pasted image 20261015164049.png]]

![[Pasted image 20261015164119.png]]

El 7 como es el primero que entro es el primero que sale

![[Pasted image 20261015164215.png]]

Antes de sacarlos, me tengo que fijar si tiene hijos y los agrego a la cola, y después lo saco
Acá estoy apunto de sacar el 9, me fijo si tiene hijos, tiene el 8 y el 10, los agrego y después saco al 9

![[Pasted image 20261015164440.png]]


![[Pasted image 20261015165330.png]]

![[Pasted image 20261015165344.png]]

en profundidad lo que hago es ir hasta lo mas profundo de una rama, una vez que llego al final vuelvo un pasa para atrás y recorro en la otra direccion, volver un paso para atrás se le dice back tracking, pueden ser varios pasos para atrás, hasta encontrar ramas que no recorrí

![[Pasted image 20261015165716.png]]

![[Pasted image 20261015165725.png]]

![[Pasted image 20261015165736.png]]

![[Pasted image 20261015171734.png]]


pre order
![[Pasted image 20261015171904.png]]

arranco desde la raiz y me voy por su rama izquierda

![[Pasted image 20261015172010.png]]

una vez que termino la rama izquierda me paso a la rama derecha


in order

![[Pasted image 20261015172158.png]]

primero voy al hijo izquierdo, mas izquierdo de todos, una vez que lo imprimo paso a la "raiz" de ese izquierdo, ósea su nodo padre, y de ahí me voy al derecho, y del derecho me voy a sus hijos izquierdos

![[Pasted image 20261015172321.png]]

una vez que agoto toda la rama izquierda recién ahí imprimo mi raiz


Queda siempre en orden creciente




Pos order

![[Pasted image 20261015173157.png]]

voy al hijo izquierdo,, agoto toda la rama del izquierdo y luego voy al derecho, después que termino mis ramas imprimo mi "raiz" o el padre de mis nodos.

Siempre imprimo la raiz al final



![[Pasted image 20261015173952.png]]

![[Pasted image 20261015174017.png]]

![[Pasted image 20261015174033.png]]



![[Pasted image 20261015222708.png]]

AVL: arboles binarios balanceados

![[Pasted image 20261015222754.png]]


![[Pasted image 20261015224023.png]]


# Mediciones

![[Pasted image 20261015224152.png]]

el peso de un nodo es la cantidad de nodos que están debajo del mismo y su nodo, por ejemplo acá los 1 tienen peso 1, el 3 son los dos de abajo y si mismo y así


![[Pasted image 20261015224834.png]]