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

![[Pasted image 20261016205519.png]]

![[Pasted image 20261016210628.png]]

Lo puedo representar en un array por niveles

![[Pasted image 20261016211018.png]]

Aca para averiguar cual es el padre y cual es el hijo con esta formula se saca, esto es para saber en el array

![[Pasted image 20261016211139.png]]

En las divisiones me tengo que quedar con la entera

![[Pasted image 20261016211341.png]]

Mi prioridad mas alta esta en la raiz, en este caso seria el 2

Pero si quiero el numero mayor, tendría que hacerlo por el heap de máximo

![[Pasted image 20261016212901.png]]

![[Pasted image 20261017155638.png]]

solo se puede dar de baja a la raiz

![[Pasted image 20261017155900.png]]

y mi espacio en el vector va a quedar vacío

yo siempre voy a querer mi vector completo desde el inicio, ya que siempre se referencia al primero, por lo cual lo que tengo que hacer es agarrar el ultimo y lo paso al primer lugar

![[Pasted image 20261017160542.png]]

una vez que paso el ultimo al primer lugar, me fijo entre los nuevos hijos del 29 en este caso y lo intercambio por el menor 

![[Pasted image 20261017163027.png]]

![[Pasted image 20261017163058.png]]

y mi ultimo lo sigo comparando con sus hijos y lo voy intercambiando

![[Pasted image 20261017163140.png]]



ahora si yo quiero dar el alta: 

![[Pasted image 20261017164018.png]]

yo aca lo pongo al final, como va al final y se tienen que ir ordenando de izquierda a derecha seria el hijo derecho del 12

![[Pasted image 20261017165513.png]]

ahora al 9 lo comparo con su padre, si es mas chico que el padre lo subo
![[Pasted image 20261017165553.png]]

y lo hago de nuevo hasta que no haya menor

![[Pasted image 20261017170049.png]]

![[Pasted image 20261017170743.png]]

![[Pasted image 20261017170852.png]]

![[Pasted image 20261017170911.png]]

![[Pasted image 20261017170921.png]]

![[Pasted image 20261017170932.png]]