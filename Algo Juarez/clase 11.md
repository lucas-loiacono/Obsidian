![[Pasted image 20260927192224.png]]

uno no sabe quien es el primero, pero sabe quien es el ultimo y se tiene de referencia
cada uno tiene lo que tiene que representar y la referencia al de delante suyo, el primero tiene referencia nula al no tener nadie delante suya

para la pila se hace la referencia al anterior y para la cola al posterior

![[Pasted image 20260927193255.png]]

![[Pasted image 20260927195027.png]]

![[Pasted image 20260927195203.png]]

si corto mi cadena, una parte se pierde de la otra, se separan

![[Pasted image 20260927200442.png]]

para referenciar a otro nodo se le pasa la misma clase a siguiente, ya que es del mismo tipo de dato

![[Pasted image 20260927200502.png]]


# Pila dinámica

![[Pasted image 20260927200718.png]]

Lo único que necesito es tener la referencia al ultimo dato, que se encarga de quien le viene delante 
antes metíamos la pila dentro de un vector, ahora como tenemos nodos, podemos no tener un vector y tener referencias enlazadas 

![[Pasted image 20260927232404.png]]

Mi ultimo es el A, cuando doy de baja a A mi ultimo pasa a ser mi C

![[Pasted image 20260927232513.png]]

![[Pasted image 20260927235305.png]]

cuando doy de baja al ultimo, mi referencia queda en null

![[Pasted image 20260928000330.png]]

Cuando doy de baja al ultimo, tengo que pasar mi referencia de ultimo a siguiente




![[Pasted image 20260928000539.png]]

Para dar de alta un dato lo que tengo que hacer es meter el dato en un nodo

1. Primero lo tengo que enganchar al ultimo,
2. Después le paso la referencia de mi ultimo al nuevo

![[Pasted image 20260928001058.png]]





![[Pasted image 20260928003849.png]]

yo cuando creo una pila, mi ultimo no va a estar referenciando a nada

![[Pasted image 20260928004048.png]]

# Cola

entra por el final y sale al principio

los nuevos van al final, y se van procesando y consultando los primeros de la cola

![[Pasted image 20260928005525.png]]


Para esto tengo que tener dos referencias, una al primero y otra al ultimo, asi para las funciones del ultimo, por ejemplo procesar o consultar no me tengo que recorrer todo para llevar al ultimo al primer lugar

![[Pasted image 20260928005843.png]]

![[Pasted image 20260928010916.png]]

![[Pasted image 20260928011208.png]]


![[Pasted image 20260928011547.png]]

Cuando me queda un elemento los dos me apuntan a ese, el siguiente se simboliza con la pata de la derecha

por lo cual al tener doble referencia y yo quiero dar de baja para que pasa el recolector de basura voy a tener que eliminar las dos

![[Pasted image 20260928012122.png]]


![[Pasted image 20260928012008.png]]

para el alta, mi ultimo si esta la cola vacía va a estar apuntando a null, entonces al hacer el movimiento de apuntar al nuevo no lo puedo hacer