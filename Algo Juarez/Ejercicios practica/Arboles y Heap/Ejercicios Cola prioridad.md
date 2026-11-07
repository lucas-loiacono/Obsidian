
![[Pasted image 20261107200204.png]]

# Ejercicio 3.5: Cola de Prioridades con Lista Simplemente Enlazada

### Enunciado
Se implementa una cola con $k$ prioridades con una lista simplemente enlazada sin conservar ningún orden en particular, por lo que los nodos se insertan al principio[cite: 13]. Entonces, el orden de las operaciones, si $n$ es la cantidad de datos, es[cite: 13]:
- (a) Alta: $\Theta(1)$ - Consulta: $\Theta(n)$ - Baja: $\Theta(n)$
- (b) Alta: $\Theta(n)$ - Consulta: $\Theta(n)$ - Baja: $\Theta(n)$
- (c) Alta: $\Theta(1)$ - Consulta: $\Theta(k)$ - Baja: $\Theta(n)$
- (d) Alta: $\Theta(1)$ - Consulta: $\Theta(k)$ - Baja: $\Theta(k)$

### Análisis y Solución
Analizamos cada operación para una **lista enlazada desordenada**:

1.  **Alta (Inserción):** El enunciado aclara explícitamente que "los nodos se insertan al principio"[cite: 13]. En una lista simplemente enlazada, insertar un nodo en la cabeza (head) toma un tiempo constante porque solo implica reasignar un par de punteros, sin importar cuántos elementos $n$ haya.
    $\implies$ **$\Theta(1)$**
2.  **Consulta (Obtener el de mayor prioridad):** Como la lista está completamente desordenada, no sabemos dónde está el elemento con la prioridad más alta. La única forma de encontrarlo es recorrer los $n$ elementos de la lista uno por uno, guardando el máximo encontrado.
    $\implies$ **$\Theta(n)$**
3.  **Baja (Eliminar el de mayor prioridad):** Para eliminarlo, primero tenemos que encontrarlo. Como vimos en la consulta, buscarlo cuesta $\Theta(n)$. Una vez encontrado, desenlazarlo cuesta $\Theta(1)$, pero el costo dominante del proceso completo sigue siendo la búsqueda.
    $\implies$ **$\Theta(n)$**

**Opción correcta: (a)**[cite: 13]

---

# Ejercicio 3.6: Cola de Prioridades con Vector de Colas

### Enunciado
Se implementa una cola con $K$ prioridades con un vector de colas[cite: 13]. Si $N$ es la cantidad de datos, el orden exacto de las operaciones es[cite: 13]:
- (a) Alta: $\Theta(1)$ - Consulta: $\Theta(N)$ - Baja: $\Theta(N)$
- (b) Alta: $\Theta(1)$ - Consulta: $\Theta(1)$ - Baja: $\Theta(1)$
- (c) Alta: $\Theta(1)$ - Consulta: $\Theta(K)$ - Baja: $\Theta(N)$
- (d) Alta: $\Theta(1)$ - Consulta: $\Theta(K)$ - Baja: $\Theta(K)$

### Análisis y Solución
En esta implementación, tenemos un arreglo (vector) de tamaño $K$, donde cada índice representa una prioridad. En cada índice hay una cola normal (FIFO) que guarda los elementos que tienen esa prioridad específica.

1.  **Alta (Inserción):** Cuando llega un dato, sabemos su prioridad (supongamos que es $p$). Simplemente accedemos a la posición $p$ del vector (`vector[p]`) y lo encolamos al final de esa cola. El acceso a un índice de un vector es constante, y encolar en una cola estándar también es constante.
    $\implies$ **$\Theta(1)$**
2.  **Consulta (Obtener el de mayor prioridad):** Para saber cuál es el próximo elemento a atender, debemos buscar la prioridad más alta que tenga al menos un elemento. Esto implica recorrer el vector de prioridades (de tamaño $K$) desde la prioridad más alta hacia la más baja hasta encontrar una cola que no esté vacía. En el peor caso (cuando solo la prioridad más baja tiene elementos, o están todas vacías), tendremos que revisar las $K$ posiciones del vector.
    $\implies$ **$\Theta(K)$**
3.  **Baja (Eliminar el de mayor prioridad):** Al igual que en la consulta, primero debemos buscar cuál es la cola no vacía con mayor prioridad revisando el vector, lo cual cuesta $\Theta(K)$. Una vez encontrada esa cola, hacer el `dequeue` (desencolar) del primer elemento cuesta $\Theta(1)$. El costo dominante es la búsqueda en el vector.
    $\implies$ **$\Theta(K)$**

**Opción correcta: (d)**[cite: 13]