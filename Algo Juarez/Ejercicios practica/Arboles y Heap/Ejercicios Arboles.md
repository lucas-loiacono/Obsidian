
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

```
      A
     / \
    B   C
   / \ / \
  D  E F  G
```

**Ejecución paso a paso:****altura(A)** evalúa: 1 + max(altura(B), altura(C))

**altura(B)** evalúa: 1 + max(altura(D), altura(E))

**altura(D)** evalúa: 1 + max(altura(null), altura(null)) = 1 + max(-1, -1) = 0

**altura(E)** evalúa: 1 + max(altura(null), altura(null)) = 1 + max(-1, -1) = 0

**Retorno a B:** altura(B) = 1 + max(0, 0) = 1

**altura(C)** evalúa: 1 + max(altura(F), altura(G))

**altura(F)** evalúa: 1 + max(altura(null), altura(null)) = 1 + max(-1, -1) = 0

**altura(G)** evalúa: 1 + max(altura(null), altura(null)) = 1 + max(-1, -1) = 0

**Retorno a C:** altura(C) = 1 + max(0, 0) = 1

**Retorno final a A (Raíz):** altura(A) = 1 + max(1, 1) = 2.

**3. Complejidad Algorítmica****Tiempo: O(N)**. Siendo N la cantidad total de nodos. El algoritmo debe recorrer exhaustivamente todos los elementos del árbol una única vez para poder calcular la altura de cada subrama. En cada llamada recursiva se efectúan operaciones aritméticas y comparaciones simples que toman tiempo constante O(1).

**Espacio: O(H)**. Siendo H la altura máxima del árbol. Esta complejidad espacial está directamente dada por el uso de la memoria en la pila de ejecución (Call Stack) debido a las llamadas recursivas. En el mejor escenario (un árbol balanceado o completo como el del ejemplo), la profundidad máxima de la pila es logarítmica O(log N). En el peor caso (un árbol degenerado asimétrico donde todos los nodos caen hacia un solo lado), la recursión llega a una profundidad de O(N).

![[Pasted image 20261108172131.png]]

**1. Implementación del algoritmo recursivo**


```Java
public void espejar(Nodo<T> raiz) {
    if (raiz != null) {
        Nodo<T> aux = raiz.getIzquierdo();
        raiz.setIzquierdo(raiz.getDerecho());
        raiz.setDerecho(aux);
        
        espejar(raiz.getIzquierdo());
        espejar(raiz.getDerecho());
    }
}
```

**2. Explicación y Seguimiento** El algoritmo recorre el árbol modificando las referencias _in place_. Para cada nodo que no sea nulo, guarda su hijo izquierdo en una variable auxiliar, le asigna el hijo derecho a la rama izquierda, y finalmente le asigna el nodo guardado en la auxiliar a la rama derecha. Una vez invertidos los punteros del nodo actual, lanza la recursividad sobre sus nuevos hijos izquierdo y derecho para propagar el efecto hasta las hojas del árbol.

  

Seguimiento sobre un árbol binario completo de altura 2: Árbol inicial:

  

Plaintext

```
      A
     / \
    B   C
   / \ / \
  D  E F  G
```

**Ejecución paso a paso:****espejar(A)** evalúa: Intercambia los subárboles B y C. Llama recursivamente a espejar(C) y luego a espejar(B).

  

**espejar(C)** (ahora hijo izquierdo de A) evalúa: Intercambia sus hijos F y G. Llama a espejar(G) y espejar(F).

  

**espejar(G)** y **espejar(F)** evalúan: Como sus hijos son nulos, el intercambio no produce cambios. Retornan.

  

**espejar(B)** (ahora hijo derecho de A) evalúa: Intercambia sus hijos D y E. Llama a espejar(E) y espejar(D).

  

**espejar(E)** y **espejar(D)** evalúan: Intercambian referencias nulas. Retornan.

  

Árbol final reflejado:

  

Plaintext

```
      A
     / \
    C   B
   / \ / \
  G  F E  D
```

**3. Complejidad Algorítmica** **Tiempo: O(N)**. Siendo N la cantidad total de nodos. El método debe visitar exhaustivamente todos los elementos del árbol exactamente una vez. En cada visita (llamada recursiva), realiza operaciones de lectura, asignación temporal y reasignación de punteros que toman un tiempo constante O(1).

  

**Espacio: O(H)**. Siendo H la altura máxima del árbol. Al modificar la estructura _in place_, el algoritmo no requiere memoria extra para almacenar nuevos nodos o estructuras de datos auxiliares. El único espacio adicional se consume en la pila de llamadas del sistema (Call Stack) debido a la recursividad. En el caso de un árbol binario completo (como el del ejemplo), el espacio ocupado será O(log N). En el peor de los casos (un árbol desbalanceado que adopte la forma de una lista enlazada), la pila de ejecución escalará hasta O(N).


Si la clase `Nodo` no tiene los métodos _getters_ y _setters_, significa que los atributos que apuntan a sus hijos son de acceso directo (probablemente declarados como `public` o con visibilidad de paquete dentro de la misma estructura de datos).

La lógica recursiva es exactamente la misma, pero la sintaxis cambia para leer y sobreescribir las variables directamente (`raiz.izquierdo` y `raiz.derecho`) en lugar de invocar funciones.

**Implementación accediendo a los atributos directamente:**

```Java

public void espejar(Nodo<T> raiz) {
    if (raiz != null) {
        Nodo<T> aux = raiz.izquierdo;
        raiz.izquierdo = raiz.derecho;
        raiz.derecho = aux;
        
        espejar(raiz.izquierdo);
        espejar(raiz.derecho);
    }
}
```

La explicación del seguimiento, el árbol resultante y el análisis de complejidad (Tiempo O(N) y Espacio O(H)) se mantienen exactamente iguales que en la respuesta anterior, ya que el comportamiento del algoritmo y su costo computacional no cambian en lo más mínimo. Solo cambia la interfaz de comunicación con el objeto `Nodo`.

![[Pasted image 20261108172523.png]]


**1. Implementación del algoritmo recursivo**



```Java
public int cantidadMultiplosN(Nodo raiz, int N) {
    int cantidad = 0;
    if (raiz != null) {
        if (raiz.getDato() % N == 0) {
            cantidad = 1;
        }
        cantidad += cantidadMultiplosN(raiz.getIzquierdo(), N) + cantidadMultiplosN(raiz.getDerecho(), N);
    }
    return cantidad;
}
```

**2. Explicación y Seguimiento** El caso base ocurre cuando se evalúa un nodo nulo, retornando 0. Si el nodo existe, se verifica si su dato es múltiplo de N usando el operador módulo (`%`). Si el resto es 0, el nodo suma 1 a la cuenta; de lo contrario, suma 0. Luego, el método se llama recursivamente para los hijos izquierdo y derecho, acumulando la cantidad total desde las hojas hacia la raíz.

  

Seguimiento sobre un árbol binario completo de altura 2 con valores del 1 al 7 y N = 1 (como todo número es múltiplo de 1, todos los nodos sumarán 1 a la cuenta):

  

```
      1
     / \
    2   3
   / \ / \
  4  5 6  7
```

**Ejecución paso a paso:****cMN(1, 1)** evalúa: 1 (porque 1%10) + cMN(2, 1) + cMN(3, 1)

  

**cMN(2, 1)** evalúa: 1 (porque 2%10) + cMN(4, 1) + cMN(5, 1)

  

**cMN(4, 1)** evalúa: 1 (porque 4%10) + cMN(null, 1) + cMN(null, 1) = 1 + 0 + 0 = 1

  

**cMN(5, 1)** evalúa: 1 (porque 5%10) + cMN(null, 1) + cMN(null, 1) = 1 + 0 + 0 = 1

  

**Retorno a 2:** cMN(2, 1) = 1 + 1 (de 4) + 1 (de 5) = 3

  

**cMN(3, 1)** evalúa: 1 (porque 3%10) + cMN(6, 1) + cMN(7, 1)

  

**cMN(6, 1)** evalúa: 1 (porque 6%10) + cMN(null, 1) + cMN(null, 1) = 1 + 0 + 0 = 1

  

**cMN(7, 1)** evalúa: 1 (porque 7%1==0) + cMN(null, 1) + cMN(null, 1) = 1 + 0 + 0 = 1

  

**Retorno a 3:** cMN(3, 1) = 1 + 1 (de 6) + 1 (de 7) = 3

  

**Retorno final a 1 (Raíz):** cMN(1, 1) = 1 + 3 (rama izq) + 3 (rama der) = 7.

  

**3. Complejidad Algorítmica** **Tiempo: O(V)**. Siendo V la cantidad total de nodos en el árbol (se utiliza V para no confundir con la variable N del parámetro). La función recursiva visita todos los elementos del árbol exactamente una vez. Como las operaciones por cada nodo (operación módulo, validaciones lógicas, sumas) toman un tiempo constante O(1), el tiempo total de ejecución escala de forma directamente proporcional a la cantidad de nodos.

  

**Espacio: O(H)**. Siendo H la altura máxima del árbol, correspondiente a la cantidad de memoria que el sistema reserva para la pila de ejecución (Call Stack) debido a las llamadas recursivas anidadas. En un árbol binario completo (como el utilizado en el seguimiento) la altura es O(log V). En el peor de los escenarios (un árbol desbalanceado en forma de lista enlazada) la altura llega a ser O(V).


![[Pasted image 20261108172647.png]]