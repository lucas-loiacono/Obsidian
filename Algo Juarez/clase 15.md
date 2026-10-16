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