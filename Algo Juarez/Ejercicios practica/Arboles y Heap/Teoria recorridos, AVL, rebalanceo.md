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

![[Pasted image 20261015225558.png]]



![[Pasted image 20261015225806.png]]

![[Pasted image 20261015230054.png]]

Para cada nodo me fijo que tan larga es la rama de la izquierda con la de la derecha y ahí hago la resta

Este árbol esta balanceado si el valor de D es 2 o mas

![[Pasted image 20261015230235.png]]

acá el factor de balanceo seria la diferencia, ósea puede tomar el valor -1, 0 o 1

Los AVL tambien tienen que ser un ABB

![[Pasted image 20261015230508.png]]]


![[Pasted image 20261015230652.png]]

siempre se hace la rama derecha - rama izquierda

![[Pasted image 20261015230749.png]]

si yo agrego el 16, tengo un FB = -2 y tengo que rebalancear

![[Pasted image 20261015231153.png]]

acá con el 12 tengo que agarrar mi rama mas larga

![[Pasted image 20261015231547.png]]


![[Pasted image 20261015231647.png]]

hay 2 tipos de desbalanceos, uno tipo lineal y el otro en zigzag

![[Pasted image 20261015231812.png]]

acá mi B pasa a ser mi pivote, lo único que tengo que hacer es rotarla, o quebrarla

![[Pasted image 20261016002524.png]]

![[Pasted image 20261016002656.png]]

![[Pasted image 20261016002751.png]]

acá roto pero los hijos de mi nueva raiz se los pongo al que roto. Los hijos de B se los paso a A

![[Pasted image 20261016002906.png]]

![[Pasted image 20261016002919.png]]

![[Pasted image 20261016005339.png]]

la imagen va de izquierda a derecha

![[Pasted image 20261016005405.png]]

2do cuadro: le paso el hijo derecho de C a B

![[Pasted image 20261016005610.png]]

![[Pasted image 20261016005759.png]]

![[Pasted image 20261016005746.png]]

![[Pasted image 20261016010106.png]]

![[Pasted image 20261016010423.png]]

así lo balanceo

![[Pasted image 20261016011554.png]]

![[Pasted image 20261016011629.png]]

![[Pasted image 20261016012013.png]]

![[Pasted image 20261016012033.png]]

En borrar se hace lo mismo que con el alta

Siempre el orden de los arboles AVL son log(N)






![[Pasted image 20261016012801.png]]


![[Pasted image 20261016012503.png]]

Son nodos pero que guardan vectores

![[Pasted image 20261016012709.png]]

Los voy agrupando de a 3 con sus direcciones de memorias al izquierdo y al derecho

![[Pasted image 20261016013041.png]]

Acá este es un árbol que puede tener 4 hijos y 3 datos

![[Pasted image 20261016013108.png]]



![[Pasted image 20261016013119.png]]

Todos los nodos hojas están al mismo nivel, por lo cual va a ser un árbol balanceado

![[Pasted image 20261016013503.png]]

llegan estos números

![[Pasted image 20261016013539.png]]

Meto el 5 y el 28

![[Pasted image 20261016013602.png]]

el 16 debería ir en el medio, pero como máximo tengo 2 claves

![[Pasted image 20261016013648.png]]
Al que debería ir al medio lo subo y parto al otro vector, dividiendo en hijo izquierdo e hijo derecho

![[Pasted image 20261016013750.png]]

sigo colocando números normalmente como en un árbol


![[Pasted image 20261016013833.png]]

bajo el catorce, el cual debería estar a la derecha del nueve, como no tengo mas espacio, subo el nueve y vuelvo a dividir

![[Pasted image 20261016013959.png]]

lo que hago es subir a la raiz, ya que ahora en la raiz puedo tener varias referencias

![[Pasted image 20261016014108.png]]


![[Pasted image 20261016014136.png]]

si yo quiero agregar el 35, no tengo espacio y debo subir al 30 a la raiz, pero como el máximo por nodo son dos datos no lo puedo subir

![[Pasted image 20261016014239.png]]

![[Pasted image 20261016014327.png]]

como se me formo un nodo de 3 tengo que subir al 16 y partir a la mitad el vector

Siempre este árbol va a crecer hacia arriba, y siempre va a estar balanceado



![[Pasted image 20261016014622.png]]

![[Pasted image 20261016014742.png]]

los nodos internos solo tienen las claves, que funcionan como índice, en donde busco en que pagina quiero estar

![[Pasted image 20261016014855.png]]

en el cual el nombre de pagina se le da a cada uno de los nodos


![[Pasted image 20261016015041.png]]

yo acá cuando quiero agregar el 16, lo que hago es cortar el vector y subirlo


![[Pasted image 20261016015131.png]]

el 16 de arriba lo dejo como índice, pero le pego al 28 todos los datos que contiene el 16


![[Pasted image 20261016015226.png]]


![[Pasted image 20261016015328.png]]

Aca agrego el 19 y lo pongo al lado

Como me manejo por índice acá tengo listas enlazadas, puedo acceder a las que están al mismo nivel


![[Pasted image 20261016015534.png]]

cuando quiero poner el 14 hago lo mismo, subo el nueve y se lo pego al hijo derecho


![[Pasted image 20261016015719.png]]

cuando quiero agregar el 30, no hay mas espacio, subo el 28, como en el 9 y 16 no hay mas espacio ahí si lo subo al 16, como es la raiz no le tengo que dejar la referencia al 28



hay que pensarlo que puedo acceder por índice o de forma secuencial ya que están todos pegados, además no copio el 16 ya que el único lugar donde tengo que copiar es en la capa 0 donde están todos los nodos en secuencia