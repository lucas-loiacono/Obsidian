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