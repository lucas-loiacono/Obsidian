
![[Pasted image 20261108171208.png]]


**1. Implementación del algoritmo recursivo**
```java
public int cantidadNodos(Nodo<T> raiz) {
    int cantidad = 0;
    if (raiz != null) {
        cantidad = 1 + cantidadNodos(raiz.getIzquierdo()) + cantidadNodos(raiz.getDerecho());
    }
    return cantidad;
}
````

**2. Explicación y Seguimiento** El caso base ocurre cuando se evalúa un nodo nulo, retornando una cantidad de 0. Si el nodo actual existe, el método se cuenta a sí mismo (1) y suma los resultados de invocar recursivamente a la función para sus hijos izquierdo y derecho, acumulando el total desde las hojas hacia la raíz.

  

Seguimiento sobre un árbol binario completo de altura 2 (raíz en nivel 0, hojas en nivel 2):


```
      A
     / \
    B   C
   / \ / \
  D  E F  G
```

**Ejecución paso a paso:**
* **cantidadNodos(A)** evalúa: 1 + cN(B) + cN(C)
* **cN(B)** evalúa: 1 + cN(D) + cN(E)
* **cN(D)** evalúa: 1 + cN(null) + cN(null) = 1 + 0 + 0 = 1
* **cN(E)** evalúa: 1 + cN(null) + cN(null) = 1 + 0 + 0 = 1
* **Retorno a B:** cN(B) = 1 + 1 (de D) + 1 (de E) = 3
* **cN(C)** evalúa: 1 + cN(F) + cN(G)
* **cN(F)** evalúa: 1 + cN(null) + cN(null) = 1 + 0 + 0 = 1
* **cN(G)** evalúa: 1 + cN(null) + cN(null) = 1 + 0 + 0 = 1
* **Retorno a C:** cN(C) = 1 + 1 (de F) + 1 (de G) = 3
* **Retorno final a A (Raíz):** 1 + 3 (de B) + 3 (de C) = 7.

**3. Complejidad Algorítmica**
* **Tiempo: O(N)**. Siendo N el número total de nodos en el árbol. La función recursiva se ejecuta exactamente una vez por cada nodo (más los retornos constantes de los punteros nulos). Como dentro de cada llamada solo se realizan sumas y validaciones simples O(1), el tiempo de ejecución crece de forma directamente proporcional a la cantidad de elementos.
* **Espacio: O(H)**. Siendo H la altura máxima del árbol, correspondiente a la memoria adicional consumida por la pila de llamadas recursivas (Call Stack). En el mejor de los casos (árbol balanceado o completo como el del ejemplo), la complejidad espacial es O(log N). En el peor de los casos (un árbol totalmente desbalanceado que funciona como lista enlazada), la altura coincide con los nodos, requiriendo un espacio O(N).

![[Pasted image 20261108171519.png]]




**1. Implementación del algoritmo recursivo**

  

```Java
public int altura(Nodo<T> raiz) {
    int alt = -1;
    if (raiz != null) {
        int altIzq = altura(raiz.getIzquierdo());
        int altDer = altura(raiz.getDerecho());
        alt = 1 + Math.max(altIzq, altDer);
    }
    return alt;
}
```

**2. Explicación y Seguimiento** El caso base ocurre cuando se evalúa un nodo nulo, retornando -1. Si el nodo existe, se calculan recursivamente las alturas de sus subárboles izquierdo y derecho. La altura del nodo actual será 1 más el valor máximo entre ambas alturas. De esta manera, se acumulan los niveles desde las hojas (que tendrán altura 0) hacia la raíz.

  

Seguimiento sobre un árbol binario completo de altura 2:
D

Plaintext

```
      A
     / \
    B   C
   / \ / \
  D  E F  G
```

**Ejecución paso a paso:****altura(A)** evalúa: 1 + max(altura(B), altura(C)) **altura(B)** evalúa: 1 + max(altura(D), altura(E)) **altura(D)** evalúa: 1 + max(altura(null), altura(null)) = 1 + max(-1, -1) = 0 **altura(E)** evalúa: 1 + max(altura(null), altura(null)) = 1 + max(-1, -1) = 0 **Retorno a B:** altura(B) = 1 + max(0, 0) = 1 **altura(C)** evalúa: 1 + max(altura(F), altura(G)) **altura(F)** evalúa: 1 + max(altura(null), altura(null)) = 1 + max(-1, -1) = 0 **altura(G)** evalúa: 1 + max(altura(null), altura(null)) = 1 + max(-1, -1) = 0 **Retorno a C:** altura(C) = 1 + max(0, 0) = 1 **Retorno final a A (Raíz):** altura(A) = 1 + max(1, 1) = 2.

  

**3. Complejidad Algorítmica****Tiempo: O(N)**. Siendo N la cantidad total de nodos. El algoritmo debe recorrer exhaustivamente todos los elementos del árbol una única vez para poder calcular la altura de cada subrama. En cada llamada recursiva se efectúan operaciones aritméticas y comparaciones simples que toman tiempo constante O(1).**Espacio: O(H)**. Siendo H la altura máxima del árbol. Esta complejidad espacial está directamente dada por el uso de la memoria en la pila de ejecución (Call Stack) debido a las llamadas recursivas. En el mejor escenario (un árbol balanceado o completo como el del ejemplo), la profundidad máxima de la pila es logarítmica O(log N). En el peor caso (un árbol degenerado asimétrico donde todos los nodos caen hacia un solo lado), la recursión llega a una profundidad de O(N).