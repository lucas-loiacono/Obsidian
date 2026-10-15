![[Pasted image 20261014220430.png]]

esto lo hago ya que de la otra manera tengo que empezar el recorrido de 0

tengo una referencia al que le sigue y al anterior

![[Pasted image 20261014220655.png]]

![[Pasted image 20261014220955.png]]

ahora tengo que enganchar el nuevo y después desenganchar los demás

![[Pasted image 20261014223344.png]]


![[Pasted image 20261014223442.png]]

![[Pasted image 20261014224013.png]]

![[Pasted image 20261014224836.png]]

![[Pasted image 20261014225022.png]]

![[Pasted image 20261014225400.png]]

si tengo un nodo este se tiene que referenciar a si mismo

![[Pasted image 20261014225649.png]]

si yo quiero los últimos 500 datos sin agregar, lo que hago es reemplazar el dato del primero con el que quiero agregar, este seria el valor de mi nodo 501, y le paso el puntero de primero a mi segundo, ya que mi ultimo nodo o dato es el actual "primero"

![[Pasted image 20261014232922.png]]

o sino con ultimo también se puede hacer así


![[Pasted image 20261014235137.png]]

![[Pasted image 20261014235201.png]]

![[Pasted image 20261015004437.png]]

son como caminos, relaciones

![[Pasted image 20261015004859.png]]

![[Pasted image 20261015004953.png]]

acá si quiero ir de A hasta C tengo una sola forma de llegar, a esto se le dice árbol

Árbol: es un grafo conexo sin ciclos.

![[Pasted image 20261015005312.png]]

esto no es un árbol, ya que no es conexo, no esta conectado

![[Pasted image 20261015005709.png]]

![[Pasted image 20261015011755.png]]

no es una lista porque no es lineal

![[Pasted image 20261015011943.png]]

esto no es un árbol porque tengo un ciclo


![[Pasted image 20261015012316.png]]

es sin raíz ya que no tienen una estructura jerárquica

![[Pasted image 20261015012351.png]]

esta si tiene raíz, y la raíz es el nodo que esta arriba de todo

![[Pasted image 20261015013146.png]]


![[Pasted image 20261015013215.png]]

![[Pasted image 20261015013602.png]]

![[Pasted image 20261015015140.png]]

![[Pasted image 20261015015955.png]]

![[Pasted image 20261015020010.png]]

Arboles binario: AB

Es un árbol jerárquico en el cual cada nodo puede tener como mucho 2 hijos, osea puede tener 0, 1 o 2

![[Pasted image 20261015020305.png]]

![[Pasted image 20261015021135.png]]

voy a tener 2 referencias, una al hijo izquierdo y otra al hijo derecho

![[Pasted image 20261015021315.png]]


Esto lo tengo que completar por niveles, primero por hijo izquierdo y luego por hijo derecho.


![[Pasted image 20261015021456.png]]

De vacío pasa a estar así


![[Pasted image 20261015021601.png]]

Para la consulta tengo que recorrer todo el árbol

Esto se mejora con ABB

![[Pasted image 20261015021641.png]]

ABB: árbol de búsqueda binaria

![[Pasted image 20261015021807.png]]

si es menor que el nodo raiz va a ir a la izquierda, si es mayor a la derecha