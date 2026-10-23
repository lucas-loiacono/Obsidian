
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

Una vez que ya recorri las dos ramas de A, me siguen faltando nodos para re