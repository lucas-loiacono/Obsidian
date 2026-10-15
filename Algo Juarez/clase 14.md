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