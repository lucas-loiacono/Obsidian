
![[Pasted image 20260912182921.png]]

si yo quiero guardar datos, lo tengo que hacer de esta forma, me tengo que crear una clase para cada tipo repitiendo el mismo codigo

![[Pasted image 20260912183312.png]]

![[Pasted image 20260912184301.png]]


Esto esta mal
![[Pasted image 20260912184604.png]]

Casteo todo a clase object, el tema es que cuando quiero sacar un elemento de la caja, se olvida de lo que es y lo tengo que castear de nuevo a la fuerza


Para esto se crearon lo genéricos

![[Pasted image 20260912190022.png]]

declaro entre <> una variable que todavia no se sabe el tipo de dato que va a contener

![[Pasted image 20260912190714.png]]

acá guardo el dato, pero a la hora que lo quiero mostrar si lo casteo mal el archivo se rompe en tiempo de ejecución

## Solución

![[Pasted image 20260912191328.png]]

Acá le tengo que pasar de que tipo es la caja entre los <>, pero si a la de string le paso in interger lo que hace es que se no deja compilar desde el principio