
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




![[Pasted image 20260912193004.png]]

java acá con los métodos java es mas inteligente, ya que le pasamos los argumentos y java ya lee el tipo que son compilando normal



![[Pasted image 20260912195741.png]]

Contrato: te obliga a programar ciertos métodos
En este caso el contrato que me debe dar dos métodos, k y v getclave y getvalor


![[Pasted image 20260912200143.png]]

A lo genéricos los restrinjo para que no me pueda tomar ciertos tipos de datos, por ejemplo si yo tengo una calculadora puedo hacer que me tome tipos de datos como int, float, doble, pero no quiero que me tome un string
De todos los datos que puede tomar el genérico lo restrinjo a unos pocos

En el caso es acepta cualquier tipo t, pero que sea heredado de la clase Numbers
Es como "t se extiende de Numbers" ósea que t extiende una rama de la clase Numbers

![[Pasted image 20260912200735.png]]