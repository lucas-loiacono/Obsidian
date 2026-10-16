![[Pasted image 20261016174009.png]]

![[Pasted image 20261016174516.png]]

![[Pasted image 20261016175658.png]]

Para el alta le pongo el puntero ultimo, así no es de orden N
Pero la consulta y la baja va a ser del orden N

La prioridad mas alta es 1 y la mas baja es 3

![[Pasted image 20261016184034.png]]

si yo agrego uno le paso el ultimo a este mismo

pero lo que puedo hacer es dar un alta dependiendo de la prioridad

![[Pasted image 20261016184149.png]]

acá tendría que recorrer todos los nodos y fijarme que este sea el de mayor prioridad, ahi lo paso al principio. Acá para el alta seria de O(N), pero gano en la consulta y en la baja

![[Pasted image 20261016184353.png]]

Aca agrego a juan 2do, ya que tiene prioridad 2, aca en mi peor caso el alta es de O(N), pero mi consulta y baja va a ser O(1)




![[Pasted image 20261016185242.png]]

Se puede hacer también un vector de colas, en la cual si yo agrupo cada espacio del vector de acuerdo a su prioridad

Aca el alta es inmediato, O(1)
La consulta es de orden k, ya que en mi peor caso tengo que recorrer el vector y si es por ejemplo con mi ultima prioridad, tengo que recorrer todas hasta encontrarlo. Pero si conozco las prioridades es mucho mas rápido

Lo que se hace a veces es como si siguen llegando de la primera prioridad, nunca van a ser consultados los de las siguiente, entonces a veces se suben de prioridad algunos datos para que puedan ser consultados mas rápidos


![[Pasted image 20261016202508.png]]


![[Pasted image 20261016203347.png]]

El único nivel que puede estar incompleto es el ultimo y se debe completar de izquierda a derecha

![[Pasted image 20261016203508.png]]

este no sirve, ya que no se completo antes el hijo izquierdo

![[Pasted image 20261016203819.png]]

![[Pasted image 20261016204100.png]]


![[Pasted image 20261016205242.png]]

este es un heap de máxima

![[Pasted image 20261016205311.png]]

Heap de mínima