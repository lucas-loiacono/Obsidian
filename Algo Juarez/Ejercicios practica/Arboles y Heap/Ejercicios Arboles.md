
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

**2. Explicación y Seguimiento**

  

El caso base ocurre cuando se evalúa un nodo nulo, retornando 0. Si el nodo existe, se verifica si su dato es múltiplo de N usando el operador módulo (`%`). Si el resto es 0, el nodo suma 1 a la cuenta; de lo contrario, suma 0. Luego, el método se llama recursivamente para los hijos izquierdo y derecho, acumulando la cantidad total desde las hojas hacia la raíz.

Seguimiento sobre un árbol binario completo de altura 2 con valores del 1 al 7 y N = 1 (como todo número es múltiplo de 1, todos los nodos sumarán 1 a la cuenta):

Plaintext

```
      1
     / \
    2   3
   / \ / \
  4  5 6  7
```

**Ejecución paso a paso:**

  

**cMN(1, 1)** evalúa: 1 (porque 1%1 = 0) + cMN(2, 1) + cMN(3, 1)


**cMN(2, 1)** evalúa: 1 (porque 2%1 = 0) + cMN(4, 1) + cMN(5, 1)

**cMN(4, 1)** evalúa: 1 (porque 4%1 = 0) + cMN(null, 1) + cMN(null, 1) = 1 + 0 + 0 = 1

**cMN(5, 1)** evalúa: 1 (porque 5%1 = 0) + cMN(null, 1) + cMN(null, 1) = 1 + 0 + 0 = 1

**Retorno a 2:** cMN(2, 1) = 1 + 1 (de 4) + 1 (de 5) = 3

**cMN(3, 1)** evalúa: 1 (porque 3%1 = 0) + cMN(6, 1) + cMN(7, 1)

**cMN(6, 1)** evalúa: 1 (porque 6%1 = 0) + cMN(null, 1) + cMN(null, 1) = 1 + 0 + 0 = 1

**cMN(7, 1)** evalúa: 1 (porque 7%1 = 0) + cMN(null, 1) + cMN(null, 1) = 1 + 0 + 0 = 1

**Retorno a 3:** cMN(3, 1) = 1 + 1 (de 6) + 1 (de 7) = 3

**Retorno final a 1 (Raíz):** cMN(1, 1) = 1 + 3 (rama izq) + 3 (rama der) = 7.


**3. Complejidad Algorítmica**

  

**Tiempo: O(V)**. Siendo V la cantidad total de nodos en el árbol (se utiliza V para no confundir con la variable N del parámetro). La función recursiva visita todos los elementos del árbol exactamente una vez. Como las operaciones por cada nodo (operación módulo, validaciones lógicas, sumas) toman un tiempo constante O(1), el tiempo total de ejecución escala de forma directamente proporcional a la cantidad de nodos.

  

**Espacio: O(H)**. Siendo H la altura máxima del árbol, correspondiente a la cantidad de memoria que el sistema reserva para la pila de ejecución (Call Stack) debido a las llamadas recursivas anidadas. En un árbol binario completo (como el utilizado en el seguimiento) la altura es O(log V). En el peor de los escenarios (un árbol desbalanceado en forma de lista enlazada) la altura llega a ser O(V).


![[Pasted image 20261108172647.png]]

**1. Implementación del algoritmo iterativo (Búsqueda en Anchura - BFS)**



```Java
public int nivelDeMayorSuma(Nodo<Integer> raiz) {
    int nivelMaximo = -1;
    if (raiz != null) {
        Cola<Nodo<Integer>> cola = new Cola<>();
        cola.encolar(raiz);
        cola.encolar(null); 
        
        int nivelActual = 0;
        int sumaActual = 0;
        int sumaMaxima = Integer.MIN_VALUE;
        nivelMaximo = 0;
        
        while (!cola.estaVacia()) {
            Nodo<Integer> actual = cola.desencolar();
            
            if (actual != null) {
                sumaActual += actual.getDato();
                if (actual.getIzquierdo() != null) {
                    cola.encolar(actual.getIzquierdo());
                }
                if (actual.getDerecho() != null) {
                    cola.encolar(actual.getDerecho());
                }
            } else {
                if (sumaActual > sumaMaxima) {
                    sumaMaxima = sumaActual;
                    nivelMaximo = nivelActual;
                }
                sumaActual = 0;
                nivelActual++;
                
                if (!cola.estaVacia()) {
                    cola.encolar(null);
                }
            }
        }
    }
    return nivelMaximo;
}
```

**2. Explicación y Seguimiento** Para sumar los elementos nivel por nivel, es necesario recorrer el árbol a lo ancho utilizando una Cola. Usamos el valor `null` como delimitador visual dentro de la estructura para saber exactamente cuándo termina un nivel y empieza el siguiente. Al terminar de desencolar un nivel entero, comparamos la suma con la máxima histórica. Si es estrictamente mayor, actualizamos. Al usar mayor estricto, garantizamos quedarnos con el de menor número en caso de empate.

  

Seguimiento sobre un árbol binario completo de altura 2 (Raíz en nivel 0):

  

Plaintext

```
      10
     /  \
    5    6
   / \  / \
  1  2 3   4
```

**Ejecución paso a paso:**

  

- **Inicialización:** cola = [10, null], nivelActual = 0, sumaMax = MIN_VALUE, nivelMax = 0.
    
      
    
- **Desencolo 10:** sumaActual = 10, encolo 5 y 6. cola = [null, 5, 6].
    
      
    
- **Desencolo null (Fin Nivel 0):** sumaActual (10) > sumaMax (MIN) -> sumaMax = 10, nivelMax = 0. nivelActual = 1, sumaActual = 0, encolo null. cola = [5, 6, null].
    
      
    
- **Desencolo 5:** sumaActual = 5, encolo 1 y 2. cola = [6, null, 1, 2].
    
      
    
- **Desencolo 6:** sumaActual = 5 + 6 = 11, encolo 3 y 4. cola = [null, 1, 2, 3, 4].
    
      
    
- **Desencolo null (Fin Nivel 1):** sumaActual (11) > sumaMax (10) -> sumaMax = 11, nivelMax = 1. nivelActual = 2, sumaActual = 0, encolo null. cola = [1, 2, 3, 4, null].
    
      
    
- **Desencolo 1:** sumaActual = 1. cola = [2, 3, 4, null].
    
      
    
- **Desencolo 2:** sumaActual = 1 + 2 = 3. cola = [3, 4, null].
    
      
    
- **Desencolo 3:** sumaActual = 3 + 3 = 6. cola = [4, null].
    
      
    
- **Desencolo 4:** sumaActual = 6 + 4 = 10. cola = [null].
    
      
    
- **Desencolo null (Fin Nivel 2):** sumaActual (10) NO es mayor que sumaMax (11). nivelMax queda en 1. nivelActual = 3, sumaActual = 0. No se encola null porque la cola quedó vacía.
    
      
    
- **Retorno final:** 1 (correspondiente a la suma de 11).
    
      
    

**3. Complejidad Algorítmica**

  

- **Tiempo: O(N)**. Siendo N la cantidad total de nodos. Cada nodo se encola y desencola exactamente una vez. Las operaciones con la cola y las sumas son de tiempo constante O(1), por lo que el tiempo total de ejecución es lineal proporcional a la cantidad de elementos.
    
      
    
- **Espacio: O(N)**. El consumo de memoria adicional está dictado por la Cola, que almacena como máximo todos los nodos del nivel más ancho del árbol. En un árbol completo, esto corresponde a la mitad de los nodos (N/2), resultando en un espacio lineal O(N).

![[Pasted image 20261108175812.png]]

**1. Implementación del algoritmo recursivo**


```Java
public int sumaEnRango(Nodo<Integer> raiz, int desde, int hasta) {
    int suma = 0;
    if (raiz != null) {
        int valor = raiz.getDato();
        
        if (valor >= desde && valor <= hasta) {
            suma += valor;
        }
        if (valor > desde) {
            suma += sumaEnRango(raiz.getIzquierdo(), desde, hasta);
        }
        if (valor < hasta) {
            suma += sumaEnRango(raiz.getDerecho(), desde, hasta);
        }
    }
    return suma;
}
```

**2. Explicación del funcionamiento** El algoritmo aprovecha la propiedad fundamental del Árbol Binario de Búsqueda (ABB) para "podar" ramas y evitar recorrer nodos innecesariamente. Si el nodo actual existe, primero evalúa si su valor pertenece al rango para sumarlo. Luego, utiliza los límites para decidir hacia dónde continuar la recursividad:

  

- Solo busca en el subárbol izquierdo si el valor del nodo actual es mayor que el límite inferior (`desde`). Si fuera menor o igual, es matemáticamente imposible que sus hijos izquierdos (que son aún más pequeños) entren en el rango.
    
      
    
- Solo busca en el subárbol derecho si el valor del nodo actual es menor que el límite superior (`hasta`). Si fuera mayor o igual, todos sus hijos derechos quedarían fuera de rango.
    
      
    

**3. Complejidad Algorítmica**

  

- **Mejor caso: O(1) u O(H)**. El mejor caso absoluto ocurre si el árbol está vacío (raíz nula), tomando tiempo O(1). Si el árbol tiene elementos, el mejor caso se da cuando el rango buscado está completamente fuera de los valores del árbol y ubicado en un extremo (por ejemplo, buscando un rango de valores negativos en un árbol de puros positivos). El algoritmo descarta subárboles enteros en cada paso y solo desciende por una única rama hasta llegar a una hoja, tomando un tiempo proporcional a la altura del árbol O(H).
    
      
    
- **Peor caso: O(N)**. Siendo N la cantidad total de nodos en el árbol. Ocurre cuando la totalidad de los elementos del árbol caen dentro del rango `[desde, hasta]`. Al estar todos los valores en rango, las condiciones de poda nunca logran descartar ramas, obligando al método a visitar exhaustivamente el subárbol izquierdo y derecho de cada uno de los nodos, resultando en un recorrido lineal completo.

![[Pasted image 20261108175853.png]]

Cierto, el enunciado dice que asumas implementados los métodos de `Nodo<T>`, así que la comparación tiene que salir de ahí. No sé cómo se llaman en tu cátedra, por eso asumo que `Nodo<T>` tiene estos métodos (cambiá los nombres por los reales):

- `Nodo(T dato)`: constructor con hijos en `null`.
- `boolean esMayor(T otro)`: true si `this.dato > otro`.
- `boolean esMenor(T otro)`: true si `this.dato < otro`.

Si tu `Nodo` tiene otra forma de comparar (un `comparar(T)` que devuelve int, por ejemplo), la lógica es la misma. Mi versión anterior no usaba `break`, pero sí `return` en medio del ciclo, así que acá lo resuelvo con una bandera.

## Versión iterativa (sin `break` ni `return` intermedios)

```java
public void alta(T dato) {
    if (raiz == null) {
        raiz = new Nodo<>(dato);
    } else {
        Nodo<T> actual = raiz;
        boolean insertado = false;
        while (!insertado) {
            if (actual.esMayor(dato)) {              // dato < actual.dato → izquierda
                if (actual.izquierdo == null) {
                    actual.izquierdo = new Nodo<>(dato);
                    insertado = true;
                } else {
                    actual = actual.izquierdo;
                }
            } else if (actual.esMenor(dato)) {       // dato > actual.dato → derecha
                if (actual.derecho == null) {
                    actual.derecho = new Nodo<>(dato);
                    insertado = true;
                } else {
                    actual = actual.derecho;
                }
            } else {                                 // ya existe, no se inserta
                insertado = true;
            }
        }
    }
}
```

## Versión recursiva (no necesita `break`)

```java
public void alta(T dato) {
    raiz = alta(raiz, dato);
}

private Nodo<T> alta(Nodo<T> nodo, T dato) {
    if (nodo == null) {
        nodo = new Nodo<>(dato);
    } else if (nodo.esMayor(dato)) {
        nodo.izquierdo = alta(nodo.izquierdo, dato);
    } else if (nodo.esMenor(dato)) {
        nodo.derecho = alta(nodo.derecho, dato);
    }
    return nodo;
}
```

## Complejidad

La complejidad es **O(h)**, con `h` la altura del árbol. Se baja por un solo camino y en cada nivel se hace trabajo constante (una o dos comparaciones y, como mucho, una asignación de referencia).

- **Peor caso: O(n).** El árbol está degenerado (por ejemplo, datos insertados en orden), queda como una lista y `h = n`.
- **Árbol balanceado: O(log n).** Ahí `h ≈ log₂ n`.

La versión iterativa usa O(1) de espacio extra y la recursiva O(h) por la pila de llamadas.

Si me pasás la firma de los métodos de `Nodo<T>` que dio tu cátedra, lo ajusto exacto.


![[Pasted image 20261108181314.png]]


# Ejercicio 3.18: seguimiento del ABB

**Regla del ABB:** menores a la izquierda, mayores a la derecha.

## Seguimiento paso a paso

**1. `alta(15)`**: el árbol está vacío, así que 15 pasa a ser la raíz.

```
15
```

**2. `alta(7)`**: 7 < 15, va a la izquierda de 15.

```
  15
 /
7
```

**3. `alta(3)`**: 3 < 15 y 3 < 7, va a la izquierda de 7.

```
    15
   /
  7
 /
3
```

**4. `alta(25)`**: 25 > 15, va a la derecha de 15.

```
      15
     /  \
    7    25
   /
  3
```

**5. `alta(18)`**: 18 > 15 y 18 < 25, va a la izquierda de 25.

```
      15
     /  \
    7    25
   /    /
  3    18
```

**6. `alta(10)`**: 10 < 15 y 10 > 7, va a la derecha de 7.

```
        15
       /  \
      7    25
     / \   /
    3  10 18
```

**7. `baja(15)`**: se elimina la raíz, que tiene **dos hijos**.

**Estrategia utilizada:** cuando el nodo a eliminar tiene dos hijos, se lo reemplaza por su **sucesor inorden**, es decir, el **mínimo del subárbol derecho** (el menor de los mayores). Después se elimina ese nodo de su posición original, lo cual es fácil porque el mínimo nunca tiene hijo izquierdo. Los otros casos son:

- Hoja: se elimina directamente.
- Un solo hijo: el hijo ocupa su lugar.

Aplicado acá:

1. Se busca el 15 (es la raíz).
2. Se busca el mínimo del subárbol derecho: se baja a 25 y luego a su izquierdo, 18. Como 18 no tiene hijo izquierdo, el mínimo es **18**.
3. Se copia el 18 en la raíz.
4. Se elimina el nodo 18 original (es una hoja), con lo que 25 queda sin hijo izquierdo.

**Árbol final:**

```
        18
       /  \
      7    25
     / \
    3  10
```

(Con la estrategia simétrica, el predecesor, el reemplazo sería el 10 y también quedaría un ABB válido. Lo importante es indicar cuál elegís y ser consistente.)

## Complejidad

Cada operación recorre un único camino desde la raíz, con trabajo constante por nivel, así que cuesta **O(h)**, con `h` la altura del árbol.

|Operación|Nodos recorridos|Costo|
|---|---|---|
|`alta(15)`|0 (árbol vacío)|O(1)|
|`alta(7)`|1|O(h)|
|`alta(3)`|2|O(h)|
|`alta(25)`|1|O(h)|
|`alta(18)`|2|O(h)|
|`alta(10)`|2|O(h)|
|`baja(15)`|1 (buscar) + 2 (hasta el sucesor)|O(h)|

En `baja`, buscar el nodo y bajar hasta el sucesor suman a lo sumo `h` niveles en total, porque el camino al sucesor continúa el camino hacia el nodo. Por eso sigue siendo O(h).

**Complejidad total:** para `n` operaciones, el costo es O(n · h).

- **Peor caso** (árbol degenerado, por ejemplo datos insertados en orden): h = n, total **O(n²)**.
- **Árbol balanceado:** h ≈ log n, total **O(n log n)**.

En este ejemplo, con 7 operaciones y una altura máxima de 2, el árbol queda bastante balanceado, así que cada operación hace muy pocas comparaciones.



![[Pasted image 20261108181338.png]]


# Ejercicio 3.19: `factorBalanceo`

**Convenciones que asumo** (cambialas si tu cátedra usa otras):

- La altura de un árbol vacío (`null`) es **-1** y la de una hoja es **0**. Así un árbol completo de altura 2 tiene 7 nodos, como pide el enunciado.
- Accedo a los hijos con los campos `izquierdo` y `derecho`. Si tu `Nodo<T>` tiene getters, reemplazalos.
- Sigo sin usar `break` ni `return` en medio del código, como pediste antes.

## Implementación

Hace falta un método auxiliar recursivo que calcule la altura, y la función pedida lo usa para los dos hijos.

```java
public int factorBalanceo(Nodo<T> raiz) {
    int resultado = 0;
    if (raiz != null) {
        resultado = altura(raiz.derecho) - altura(raiz.izquierdo);
    }
    return resultado;
}

private int altura(Nodo<T> nodo) {
    int resultado = -1;                         // caso base: árbol vacío
    if (nodo != null) {
        resultado = 1 + Math.max(altura(nodo.izquierdo), altura(nodo.derecho));
    }
    return resultado;
}
```

## Cómo funciona

- `altura(nodo)`: si el nodo es `null` devuelve -1 (caso base). Si no, la altura es 1 más la mayor de las alturas de sus dos hijos.
- `factorBalanceo(raiz)`: si la raíz es `null` devuelve 0. Si no, devuelve `altura(derecho) - altura(izquierdo)`.

Si el resultado es positivo, el árbol pesa más a la derecha. Si es negativo, pesa más a la izquierda. Si es 0, ambos lados tienen la misma altura.

## Seguimiento sobre un árbol completo de altura 2

```
        1
      /   \
     2     3
    / \   / \
   4   5 6   7
```

**`factorBalanceo(1)`** calcula `altura(3) - altura(2)`.

**Cálculo de `altura(3)`:**

- `altura(6)` = 1 + max(altura(null), altura(null)) = 1 + max(-1, -1) = **0**
- `altura(7)` = 1 + max(-1, -1) = **0**
- `altura(3)` = 1 + max(0, 0) = **1**

**Cálculo de `altura(2)`:**

- `altura(4)` = **0**
- `altura(5)` = **0**
- `altura(2)` = 1 + max(0, 0) = **1**

**Resultado:** `factorBalanceo(1)` = 1 - 1 = **0**.

Tiene sentido: un árbol completo está perfectamente balanceado. Lo mismo pasa con cualquier otro nodo: el 2 y el 3 tienen factor 0 - 0 = 0, y las hojas tienen (-1) - (-1) = 0.

Si usaras la convención `altura(null) = 0`, todas las alturas subirían en 1 y el factor daría igual, porque es una resta.

## Complejidad

**`altura(nodo)`** visita **cada nodo del subárbol una sola vez** y hace trabajo constante en cada uno (una comparación con `null`, una suma y un máximo). Su recurrencia es:

T(n) = T(izq) + T(der) + O(1)

Esto da **O(m)**, con m la cantidad de nodos del subárbol.

**`factorBalanceo(raiz)`** llama a `altura` sobre el hijo izquierdo y el derecho, que juntos tienen n - 1 nodos, y hace trabajo constante extra. Por lo tanto:

- **Tiempo: O(n)**, con n la cantidad de nodos del árbol. Es igual en mejor y peor caso, porque `altura` siempre recorre todo el subárbol.
- **Espacio: O(h)** por la pila de llamadas recursivas, con h la altura del árbol. Es O(log n) en un árbol completo y O(n) en uno degenerado.

Si en vez de uno quisieras el factor de **todos** los nodos, el costo subiría a O(n · h), porque habría que llamar a `altura` en cada nodo. Pero el enunciado pide solo el de la raíz que se le pasa.



![[Pasted image 20261108182241.png]]


# Ejercicio 3.20

Leo el árbol así:

```
          34
        /    \
      23      25
     /  \    /  \
   14   18  20   24
        /
       3
```

## a. ¿Es un ABB?

**No.** Un ABB exige que, para cada nodo, todo el subárbol izquierdo tenga valores menores y todo el derecho valores mayores. Acá se rompe en varios lugares:

- **18 es hijo derecho de 23, pero 18 < 23.** Un hijo derecho debería ser mayor.
- **25 es hijo derecho de 34, pero 25 < 34.** Todo el subárbol derecho de 34 (25, 20, 24) tiene valores menores que la raíz.
- **20 y 24 son menores que 25**, pero 24 está a su derecha.

Con que falle una sola de estas condiciones ya no es ABB.

## b. Recorrido in-order (izquierdo, raíz, derecho)

**14, 23, 3, 18, 34, 20, 25, 24**

Para el subárbol de 23: primero 14, luego 23, luego el subárbol de 18, que da 3 y 18. Después viene la raíz 34. Por último el subárbol de 25: 20, 25, 24.

## c. Post-order recursivo (izquierdo, derecho, raíz)

```java
public List<T> postOrder() {
    List<T> resultado = new ArrayList<>();
    postOrder(raiz, resultado);
    return resultado;
}

private void postOrder(Nodo<T> nodo, List<T> resultado) {
    if (nodo != null) {
        postOrder(nodo.izquierdo, resultado);   // 1. subárbol izquierdo
        postOrder(nodo.derecho, resultado);     // 2. subárbol derecho
        resultado.add(nodo.dato);               // 3. la raíz al final
    }
}
```

Hacen falta `import java.util.List;` e `import java.util.ArrayList;`. Si tu cátedra usa su propia lista, cambiá `add` por el método que corresponda. Si solo piden imprimir, reemplazá `resultado.add(nodo.dato)` por `System.out.print(nodo.dato + " ")`.

**Resultado sobre este árbol:** **14, 3, 18, 23, 20, 24, 25, 34**

**Complejidad:** tiempo **O(n)**, porque cada nodo se visita una vez con trabajo constante. Espacio **O(h)** por la pila de llamadas, además de la lista de salida.

## d. ¿El in-order de un ABB siempre devuelve los elementos ordenados?

**Sí, en orden ascendente.** Se justifica por inducción sobre el árbol:

- Un ABB vacío o con un solo nodo está trivialmente ordenado.
- En un ABB con raíz `r`, todos los elementos del subárbol izquierdo son menores que `r` y todos los del derecho son mayores.
- El in-order imprime primero el subárbol izquierdo (ordenado por hipótesis inductiva), luego `r`, luego el derecho (también ordenado).
- Entonces la secuencia completa es: [menores que r, ordenados], r, [mayores que r, ordenados], que está ordenada.

Si el ABB admitiera repetidos, la salida sería no decreciente. En la práctica esto es lo que permite ordenar con un ABB: se insertan los datos y se hace in-order, con costo O(n) para el recorrido.

## e. ¿Es un heap de máxima?

**No.** Un heap de máxima tiene que cumplir dos propiedades:

1. **Orden:** cada padre es mayor o igual que sus hijos. **Acá se cumple:** 34 ≥ 23, 25; 23 ≥ 14, 18; 18 ≥ 3; 25 ≥ 20, 24.
2. **Forma:** el árbol debe ser **completo**, con todos los niveles llenos salvo el último, que se llena de izquierda a derecha sin huecos. **Acá no se cumple:** el 3 está en el último nivel como hijo de 18, pero el nodo 14, que está más a la izquierda en el nivel anterior, no tiene hijos. Quedó un hueco.

Se ve también en la representación por arreglo, que tendría posiciones vacías: `[34, 23, 25, 14, 18, 20, 24, _, _, 3]`.

Como no es un heap, no corresponde hacer la inserción del 26.







Armé el resumen con todo lo que vimos: los ejercicios, la forma de pensarlo y los errores típicos.


# Recursión en árboles binarios

## 1. Las dos piezas de toda función recursiva

- **Caso base:** el problema más chico, que se responde directo sin llamarse. Es lo que corta la recursión.
- **Caso recursivo:** resuelvo "un pedacito" y le delego a la misma función **el resto, que es más chico**.
- Cada llamada tiene que **acercarse al caso base**. Si no, la recursión es infinita (`StackOverflowError`).

### Ejemplo base: sumar un vector

```java
int sumar(int[] v, int n) {          // n = cantidad de elementos a considerar
    int resultado;
    if (n == 0) {                    // caso base: vector vacío
        resultado = 0;
    } else {                         // recursivo: último + suma del resto
        resultado = v[n - 1] + sumar(v, n - 1);
    }
    return resultado;
}
```

- Lo que se achica: el índice `n`
- Las llamadas bajan hasta `n == 0` y después **vuelven resolviéndose**: `0 → 3+0 → 5+3 → 2+8 = 10`

### Traducción al árbol

| | Vector | Árbol |
|---|---|---|
| Lo que se achica | el índice `n` | el subárbol (cada hijo es raíz de uno más chico) |
| Caso base | `n == 0` | `raiz == null` |
| Delego | `sumar(v, n-1)` | `f(izq)` y `f(der)` |

---

## 2. Cómo se ejecuta: bajada y subida

- **Bajada:** cada nodo llama a sus hijos y queda esperando. Todavía no se calculó nada.
- **Caso base:** se alcanza en el `null` (un nivel **debajo** de las hojas), no en la hoja.
- **Subida:** los `null` devuelven el valor base y cada nodo combina los resultados de sus hijos y se lo devuelve al padre.
- El cálculo real ocurre en la **subida**.

```
        A
      /   \
     B     C
    / \   / \
   D   E F   G       (árbol completo de altura 2, 7 nodos)
```

Orden real de ejecución: baja por A, B, D, null, vuelve, baja por otro null, vuelve a B, baja por E... y recién después pasa a C. Es un recorrido tipo preorder.

---

## 3. Los tres momentos de la acción en cada nodo

| Momento | Equivale a | Cuándo usarlo |
|---|---|---|
| **Antes de bajar** | preorder | modifico el nodo y no dependo de los hijos (`espejar`) |
| **Entre las dos llamadas** | inorder | necesito el orden izq, nodo, der (imprimir un ABB ordenado) |
| **Después de volver** | postorder | necesito los resultados de los hijos (`altura`, `cantidadNodos`) |

**Regla para decidir:** ¿necesito lo que devuelven los hijos para calcular el mío?
- Sí → acción al volver
- No → acción al bajar (o da igual)

---

## 4. Ejercicios resueltos

### 4.1 `cantidadNodos`

```java
public int cantidadNodos(Nodo<T> raiz) {
    int cantidad = 0;                                  // base implícita: vacío → 0
    if (raiz != null) {
        cantidad = 1 + cantidadNodos(raiz.getIzquierdo())
                     + cantidadNodos(raiz.getDerecho());
    }
    return cantidad;
}
```

- Base: `raiz == null` → 0
- Recursivo: 1 (la raíz) + nodos del izquierdo + nodos del derecho
- **Seguimiento (completo, altura 2):**
  - hoja = 1 + 0 + 0 = 1
  - B = 1 + 1 + 1 = 3, C = 3
  - A = 1 + 3 + 3 = 7
- **Tiempo O(n):** `n` llamadas sobre nodos + `n+1` sobre `null` = `2n+1` llamadas, cada una O(1)
- **Espacio (pila) O(h):** O(log n) si está balanceado, O(n) en el peor caso (árbol degenerado)

### 4.2 `altura`

```java
public int altura(Nodo<T> raiz) {
    int alt = -1;                                      // vacío → -1
    if (raiz != null) {
        int altIzq = altura(raiz.getIzquierdo());
        int altDer = altura(raiz.getDerecho());
        alt = 1 + Math.max(altIzq, altDer);
    }
    return alt;
}
```

- Base: vacío = **-1**, de ahí sale que una hoja tenga altura 0
- Si la cátedra cuenta niveles (hoja = 1), la base pasa a 0 y el resto queda igual. **Confirmar la convención.**
- **Seguimiento:**
  - hoja = 1 + max(-1, -1) = 0
  - B = 1 + max(0, 0) = 1, C = 1
  - A = 1 + max(1, 1) = 2
- Misma plantilla que `cantidadNodos`, cambia solo cómo combino los hijos:
  - cantidad: `1 + izq + der`
  - altura: `1 + max(izq, der)`
- Tiempo O(n), pila O(h)

### 4.3 `espejar`

```java
public void espejar(Nodo<T> raiz) {
    if (raiz != null) {
        Nodo<T> aux = raiz.getIzquierdo();             // acción al bajar
        raiz.setIzquierdo(raiz.getDerecho());
        raiz.setDerecho(aux);

        espejar(raiz.getIzquierdo());                  // bajo
        espejar(raiz.getDerecho());
    }
}
```

- `void`: **modifica el árbol en el lugar**, no hay resultados que combinar
- Acción al bajar (preorder), pero haciéndola al volver (postorder) da lo mismo
- Lo obligatorio: intercambiar en **todos** los nodos
- Tiempo O(n), pila O(h)

### 4.4 `cantidadMultiplosN`

```java
public int cantidadMultiplosN(Nodo<Integer> raiz, int N) {
    int cantidad = 0;                                  // base implícita
    if (raiz != null) {
        if (raiz.getDato() % N == 0) {                 // acción del nodo (al bajar)
            cantidad = 1;
        }
        cantidad += cantidadMultiplosN(raiz.getIzquierdo(), N)
                  + cantidadMultiplosN(raiz.getDerecho(), N);
    }
    return cantidad;
}
```

- Patrón "contar con condición": igual a `cantidadNodos`, pero sumo 1 solo si el nodo cumple
- Cuidados:
  - `Nodo` crudo → `getDato()` es `Object` y `% N` no compila; usar `Nodo<Integer>`
  - `N == 0` → `ArithmeticException`; validar antes de la recursión
- Nodo primero o hijos primero: da igual, la suma es conmutativa
- Tiempo O(n), pila O(h)

#### Versión con `if/else` (caso base visible)

```java
public int cantidadMultiplosN(Nodo<Integer> raiz, int N) {
    int cantidad;
    if (raiz == null) {                                // base
        cantidad = 0;
    } else {                                           // recursivo
        cantidad = cantidadMultiplosN(raiz.getIzquierdo(), N)
                 + cantidadMultiplosN(raiz.getDerecho(), N);
        if (raiz.getDato() % N == 0) {
            cantidad++;
        }
    }
    return cantidad;
}
```

- Cada rama asigna `cantidad` una sola vez, sin doble inicialización
- El nodo se evalúa después de los hijos
- No existe un `if/else` con "nodo primero" y un solo `0` sin truco: hay que elegir

---

## 5. Caso base: cómo decidirlo

- Más común: `raiz == null` (árbol vacío)
- `raiz != null` es la condición para **seguir**, no para cortar
- Son la misma pregunta vista desde los dos lados

**Excepciones (otros casos base):**
- **Hoja** (`izq == null && der == null`): cuando el árbol vacío no tiene respuesta válida (ej: máximo)
- **Elemento encontrado:** en búsquedas, además del `null` (no está)
- **ABB:** además del `null`, descarto un lado entero según la comparación

**Pregunta clave:** ¿cuál es el árbol más chico para el que sé la respuesta sin llamar a nadie?

**Valor del caso base según el problema:**

| Problema | Base (árbol vacío) |
|---|---|
| contar / sumar | 0 |
| buscar (¿está?) | `false` |
| altura (hoja = 0) | -1 |
| recolectar en lista | lista vacía |

### Forma implícita vs explícita

- **Implícita** (`int r = base; if (raiz != null) {...}`): más corta, sirve cuando la base es un valor neutro
- **Explícita** (`if (raiz == null) ... else ...`): más clara para explicar en un examen, o cuando la base no es neutra

---

## 6. Metodología para un ejercicio nuevo

1. **¿Cuál es el caso base?** (árbol vacío → ¿qué devuelve?)
2. **¿Qué hago con la raíz?** (contar 1, comparar, intercambiar...)
3. **¿Qué le pido a cada hijo?** (la misma función sobre `izq` y `der`)
4. **¿Cómo combino?** (sumar, `max`, `&&`, `||`, concatenar, nada si es `void`)
5. **¿Cuándo va la acción?** Si dependo de los hijos → al volver. Si no → al bajar.
6. **Confiar en la recursión:** asumo que la llamada sobre el hijo ya devuelve la respuesta correcta para **su** subárbol, y solo resuelvo mi nivel.

**Seguimiento en un examen:** dibujar el árbol completo de altura 2, anotar el valor que devuelve cada nodo de abajo hacia arriba, y mostrar el resultado en la raíz.

**Complejidad (casi siempre igual):**
- Tiempo: O(n), cada nodo se visita una vez con trabajo O(1)
- Espacio de pila: O(h), con h = altura (O(log n) balanceado, O(n) degenerado)

---

## 7. Errores típicos

- Acceder a `raiz.getIzquierdo()` sin descartar antes que `raiz` es `null` → `NullPointerException`
- Olvidar el caso base → recursión infinita
- Llamadas que no achican el problema
- Usar `Nodo` crudo en vez de `Nodo<T>` (warnings, o no compila operaciones sobre el dato)
- En `altura`, confundir la convención (-1 vs 0 para el vacío)
- En `espejar`, olvidar bajar por ambos hijos (hay que intercambiar en todos los nodos)
- Pensar que termina en la hoja: termina un nivel más abajo, en los `null`

---

## 8. Simetría con lo anterior (listas con cursor)

| Listas con cursor | Árboles recursivos |
|---|---|
| `while` con cursor | llamada recursiva |
| `iniciarCursor()` | pasar la raíz del subárbol |
| `obtenerCursor() != null` | `raiz != null` |
| `avanzarCursor()` | bajar a `izq` / `der` |
| un método por nivel de anidamiento | una sola función que se llama a sí misma |

- En listas: de lista vs lista a elemento vs elemento, un método auxiliar por nivel
- En árboles: la misma función se aplica a cada subárbol, cada vez más chico
