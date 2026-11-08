
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