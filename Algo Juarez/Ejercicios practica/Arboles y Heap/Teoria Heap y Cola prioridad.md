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

# Tabla de Complejidad: Implementaciones de Colas de Prioridad

Esta tabla resume el costo computacional (en notación $O$ grande) de las tres operaciones básicas de una Cola de Prioridades, dependiendo de la estructura de datos subyacente que se utilice para programarla[cite: 14]. 

Recordemos las operaciones:
- **Consulta (Peek/Find-Max):** Ver cuál es el elemento con mayor prioridad sin sacarlo.
- **Baja (Dequeue/Extract-Max):** Sacar y devolver el elemento con mayor prioridad.
- **Alta (Enqueue/Insert):** Agregar un nuevo elemento a la estructura.

Aquí va la explicación de cada fila:

### 1. Lista desordenada (Lista des.)
*   **Alta - $O(1)$:** Como no nos importa mantener un orden, simplemente insertamos el nuevo elemento al principio de la lista enlazada (operación de costo constante)[cite: 14].
*   **Consulta - $O(N)$:** Al estar todo desordenado, no sabemos dónde está el elemento más prioritario. Tenemos que recorrer los $N$ elementos uno por uno para encontrar al mayor[cite: 14].
*   **Baja - $O(N)$:** Igual que la consulta. Hay que recorrer toda la lista para encontrar al elemento de mayor prioridad, y una vez encontrado, lo desenlazamos[cite: 14].

### 2. Lista ordenada
*   **Alta - $O(N)$:** Cuando llega un elemento nuevo, tenemos que recorrer la lista nodo por nodo hasta encontrar su posición correcta para que la lista siga ordenada de mayor a menor prioridad[cite: 14]. En el peor caso, recorremos los $N$ elementos.
*   **Consulta - $O(1)$:** Como la lista está ordenada, el elemento con mayor prioridad siempre va a estar en la cabeza (el primer nodo). Solo lo leemos[cite: 14].
*   **Baja - $O(1)$:** El de mayor prioridad está primero, así que sacarlo es simplemente eliminar el primer nodo de la lista[cite: 14].

### 3. Vector de colas
*Se asume que hay una cantidad finita $k$ de prioridades distintas.*
*   **Alta - $O(1)$:** El vector tiene tamaño $k$. Si el elemento tiene prioridad `p`, accedemos a la posición `p` del vector de forma directa (costo 1) y lo agregamos al final de esa cola (costo 1)[cite: 14].
*   **Consulta - $O(k)$:** Para saber a quién atender, hay que buscar cuál es la prioridad más alta que tiene gente esperando. Para esto, se recorre el vector de prioridades (de tamaño $k$) hasta encontrar la primera cola que no esté vacía[cite: 14].
*   **Baja - $O(k)$:** Se hace exactamente lo mismo que en la consulta para encontrar la cola correcta ($O(k)$), y luego se saca el primer elemento de esa cola ($O(1)$)[cite: 14].

### 4. ABB (Árbol Binario de Búsqueda)
*La tabla muestra los costos del **peor caso** para un árbol que no se balancea automáticamente.*
*   **Consulta y Baja - $O(N)$:** El elemento de mayor prioridad estará lo más a la derecha posible del árbol. Si el árbol se degenera y forma una "línea recta" (como una lista enlazada), ir hasta el final de la rama derecha nos costará $O(N)$[cite: 14].
*   **Alta - $O(N)$:** Para insertar, debemos bajar por el árbol comparando valores. De nuevo, si el árbol está degenerado (completamente desbalanceado), podemos llegar a recorrer $N$ nodos para insertarlo en el fondo[cite: 14].

### 5. Heap (Montículo)
*Es la estructura ideal y más eficiente en la práctica para colas de prioridad.*
*   **Consulta - $O(1)$:** Por definición matemática del Heap, el elemento de mayor prioridad **siempre** está en la raíz del árbol. Con solo mirar la raíz ya lo obtenemos[cite: 14].
*   **Baja - $O(\log N)$:** Sacamos la raíz, pero ahora el árbol queda "roto". Para arreglarlo, subimos el último elemento a la raíz y lo hacemos "hundirse" (bubble-down) hasta que recupere la propiedad de Heap. Como el árbol Heap siempre está perfectamente balanceado, la altura máxima a recorrer es $\log N$[cite: 14].
*   **Alta - $O(\log N)$:** Se inserta el nuevo elemento en la última posición del árbol y se lo hace "flotar" (bubble-up) hacia arriba hasta que encuentre su lugar correcto. Por la misma razón de la altura, el costo máximo es $\log N$[cite: 14].

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


![[Pasted image 20261017185829.png]]

Ordenamientos por heapsort
Si yo quiero de menor a mayo el vector lo que tengo que hacer es armar un heap de máxima

Los datos como llegan al vector los tengo que dar de alta en el heap con toda la metodología que vimos antes

![[Pasted image 20261017190848.png]]

![[Pasted image 20261017190917.png]]

![[Pasted image 20261017191207.png]]

esto se hace para armar el heap, ahora hay que hacer el ordenamiento

Ahora lo que tengo que hacer es como cuando doy de baja, pero en vez de eliminar la raiz la llevo al ultimo elemento

![[Pasted image 20261017191416.png]]

una vez que subo al 3 tengo que ir comparándolo con los hijos y lo voy bajando, voy subiendo al hijo mas grande

![[Pasted image 20261017191611.png]]

![[Pasted image 20261017191627.png]]

![[Pasted image 20261017191645.png]]

ahora vuelvo a dar la "baja"

![[Pasted image 20261017191757.png]]

pero como el 25 ya esta ordenado no lo toco, toco una posicion antes

![[Pasted image 20261017191905.png]]

![[Pasted image 20261017192043.png]]

![[Pasted image 20261017192635.png]]

![[Pasted image 20261017192834.png]]

