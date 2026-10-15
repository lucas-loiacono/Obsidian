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

si es menor que el nodo raíz va a ir a la izquierda, si es mayor a la derecha

![[Pasted image 20261015021928.png]]

![[Pasted image 20261015022036.png]]

Acá pongo el 10, después el 8 al ser menor lo pongo a la izquierda
el 4 es menor que el 10, lo bajo por la izquierda y sigo preguntado
el 4 es menor que el 8, lo pongo como su izquierdo

es como que se va deslizando hasta que encuentra su lugar
hay que preguntar si tiene hijo izquierdo o derecho para colocarlo

![[Pasted image 20261015022311.png]]


![[Pasted image 20261015022341.png]]

![[Pasted image 20261015022721.png]]

si yo tengo un árbol en el cual todos los nodos tienen un solo hijo, queda como una lista, y se dice que el árbol degenera en una lista

![[Pasted image 20261015023048.png]]

Para la consulta voy preguntando por menor o mayor y voy bajando dependiendo del lado del nodo hasta llegar al que quiero, también puede ser que no lo encuentre

Para la baja me tengo que fijar en encontrarlo y luego dependiendo el caso lo elimino


![[Pasted image 20261015023328.png]]

Si quiero pasar a eliminar el 4, este como tiene un solo hijo lo que hago es que pase a referenciar al hijo de este


![[Pasted image 20261015023911.png]]

Cuando quiero eliminar a uno que tenga 2 hijos, lo que tengo que hacer es eliminar al inmediato predecesor o el sucesor

El predecesor es: del lado izquierdo, ya que es el mas chico, pero el mas grande de los del lado izquierdo, ósea en ese caso seria mi 9
Una a la izquierda y después todo a la derecha

![[Pasted image 20261015024202.png]]

piso el 10 con mi nueve, ósea mi nuevo valor

Ahora el 9 lo que va a pasar es que o va a ser un nodo hoja o no va a tener un solo hijo

Va a poder tener un solo hijo ya que al buscar al que va a reemplazar al 10 tuve que recorrer todo lo de las derecha hasta llegar al ultimo, por lo cual solo va a poder llegar a tener un hijo izquierdo

![[Pasted image 20261015024436.png]]

Hago la eliminación como hacíamos antes


![[Pasted image 20261015024544.png]]

si yo lo quiero hacer con el sucesor, lo que hago es de los mas grandes quiero al mas chico,
ósea hago uno a la derecha y después voy bajando hasta el ultimo de la izquierda


![[Pasted image 20261015024654.png]]

Lo que se recomienda para que el árbol no este desbalanceado es hacer una y una, ósea una baja con el predecesor y otra con el sucesor

![[Pasted image 20261015025017.png]]

Si o si voy a tener una referencia al nodo raíz

![[Pasted image 20261015025222.png]]

Solo voy a tener las referencias de mis hijos


# Alta

![[Pasted image 20261015025431.png]]a

si yo empiezo así, siempre mi primer dato va a ser la raíz

![[Pasted image 20261015025545.png]]

creo un nuevo nodo, comparo con la raiz, como es menor lo pongo al lado izquierdo, como no tiene hijo izquierdo la raíz lo pongo ahí


![[Pasted image 20261015030001.png]]

![[Pasted image 20261015030521.png]]

El alta lo puedo hacer recursivo o iterativo, lo que si siempre se va a terminar cuando encuentre el espacio null y se ponga ahí



![[Pasted image 20261015030259.png]]

También para la implementación puedo agregar la referencia del padre, esto sirve mucho para la baja


