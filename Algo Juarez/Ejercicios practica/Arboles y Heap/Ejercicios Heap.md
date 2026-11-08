

![[Pasted image 20261108164702.png]]

Aquí tenés la resolución paso a paso, armada en Markdown para que la puedas guardar directamente en Obsidian.


**1. Árbol inicial** Primero, pasamos el vector `[20, 15, 12, 7, 9, 5, 11, 3, 4, 1]` a un árbol binario. Se completa de arriba hacia abajo y de izquierda a derecha:



```
            20
          /    \
        15      12
       /  \    /  \
      7    9  5    11
     / \  /
    3  4 1
```

**2. Inserción de 17 y proceso de "Upheap" (flote)** Al insertar un elemento en un Heap, siempre se coloca en la primera posición disponible en el último nivel (de izquierda a derecha). En este caso, como hijo derecho del `9`.

  

**Paso A: Inserción inicial**


```
            20
          /    \
        15      12
       /  \    /  \
      7    9  5    11
     / \  / \
    3  4 1  17   <-- Se agrega acá
```

**Paso B: Primer intercambio** Como es un Max-Heap, cada nodo debe ser menor que su padre. Comparamos el `17` con su padre (`9`). Como `17 > 9`, los intercambiamos.



```
            20
          /    \
        15      12
       /  \    /  \
      7   17  5    11
     / \  / \
    3  4 1   9   <-- El 9 bajó, el 17 subió
```

**Paso C: Segundo intercambio** Volvemos a comparar el `17` con su nuevo padre (`15`). Como `17 > 15`, los volvemos a intercambiar.

  

```
            20
          /    \
        17      12
       /  \    /  \
      7   15  5    11
     / \  / \
    3  4 1   9
```

Comparamos el `17` con su nuevo padre (`20`). Como `17 < 20`, se cumple la propiedad del Max-Heap y el algoritmo se detiene.

  

**3. Resolución analítica en el vector (usando fórmulas de índices)** Suponiendo un arreglo indexado en 0, las fórmulas que rigen el heap son:

  

- Hijo izquierdo: `2i + 1`
    
      
    
- Hijo derecho: `2i + 2`
    
      
    
- Padre: `(i - 1) / 2` (división entera)


El vector original tiene tamaño 10 (índices del 0 al 9).

  

1. **Se agrega el 17 al final del vector:** Se coloca en la posición `i = 10`. Vector temporal: `[20, 15, 12, 7, 9, 5, 11, 3, 4, 1, 17]`
    
      
    
2. **Primer cálculo de padre:** El padre del índice `10` está en `(10 - 1) / 2 = 4`. Comparamos `V[10]` (17) contra `V[4]` (9). Como `17 > 9`, hacemos un swap. Vector temporal: `[20, 15, 12, 7, 17, 5, 11, 3, 4, 1, 9]`
    
      
    
3. **Segundo cálculo de padre:** El nuevo índice del 17 es `i = 4`. Su padre está en `(4 - 1) / 2 = 1`. Comparamos `V[4]` (17) contra `V[1]` (15). Como `17 > 15`, hacemos un swap. Vector temporal: `[20, 17, 12, 7, 15, 5, 11, 3, 4, 1, 9]`
    
      
    
4. **Tercer cálculo de padre:** El nuevo índice del 17 es `i = 1`. Su padre está en `(1 - 1) / 2 = 0`. Comparamos `V[1]` (17) contra `V[0]` (20). Como `17 < 20`, no hay swap y terminamos.


**Resultado final:** El vector resultante tras agregar el elemento 17 es:`[20, 17, 12, 7, 15, 5, 11, 3, 4, 1, 9]`



# Si no

Es súper directo. Para pasar el árbol ya acomodado al vector, simplemente tenés que leerlo **por niveles: de arriba hacia abajo y de izquierda a derecha**.

  

Tomando el árbol final que armaste con los intercambios:

  

Plaintext

```
            20
          /    \
        17      12
       /  \    /  \
      7   15  5    11
     / \  / \
    3  4 1   9
```

Lo vas anotando nivel por nivel en ese orden exacto:

  

- **Nivel 0 (Raíz):** `20`
    
      
    
- **Nivel 1:** `17`, `12`
    
      
    
- **Nivel 2:** `7`, `15`, `5`, `11`
    
      
    
- **Nivel 3:** `3`, `4`, `1`, `9`
    
      
    

Juntás todo y te queda el vector final:`[20, 17, 12, 7, 15, 5, 11, 3, 4, 1, 9]`

  

Como los Heaps siempre son árboles binarios completos (se llenan todos los niveles de izquierda a derecha antes de pasar al siguiente), la lectura visual nivel por nivel coincide perfectamente con las posiciones del arreglo.c



![[Pasted image 20261108164827.png]]




```Java
public boolean esHeapDeMaxima(int[] vector) {
    boolean esHeap = true;
    if (vector != null && vector.length > 1) {
        int n = vector.length;
        for (int i = 0; i <= (n / 2) - 1 && esHeap; i++) {
            int hijoIzq = 2 * i + 1;
            int hijoDer = 2 * i + 2;
            if (hijoIzq < n && vector[i] < vector[hijoIzq]) {
                esHeap = false;
            } else if (hijoDer < n && vector[i] < vector[hijoDer]) {
                esHeap = false;
            }
        }
    }
    return esHeap;
}
```

**Cómo funciona:**

- **Variable de estado:** Inicializamos `esHeap` en `true`. Si el vector es nulo o tiene un solo elemento (lo cual ya es un heap válido), se salta la lógica principal y retorna `true` directamente.
    
- **Límite del ciclo `(n / 2) - 1`:** En un árbol binario completo, los elementos desde el índice `n/2` hasta el final son nodos hoja (no tienen hijos). El bucle solo recorre los nodos internos, ahorrando procesamiento.
    
- **Condición de corte:** Al agregar `&& esHeap` en el `for`, el ciclo se interrumpe inmediatamente si encontramos una violación a la regla del heap, evitando iterar el resto del arreglo sin sentido.
    
- **Cálculo de posiciones:** Para cada nodo interno `i`, localizamos a su hijo izquierdo usando `2*i + 1` y a su hijo derecho con `2*i + 2`.
    
- **Comprobación de Máxima:** Verificamos que el hijo exista (`< n`). Si el valor del hijo llega a ser mayor que el de su padre (`vector[i]`), rompemos la regla del heap de máxima, marcando `esHeap = false`.
    
- **Único retorno:** Todo el flujo converge al final del método, devolviendo el estado definitivo de la variable booleana.



- **Tiempo: O(N)**. Siendo N la cantidad de elementos del vector, el ciclo `for` itera únicamente hasta la mitad del arreglo `(n / 2) - 1` ya que no es necesario revisar los nodos hoja (que no tienen hijos). En cada iteración se realizan operaciones aritméticas básicas y comparaciones lógicas que toman tiempo constante O(1).
    
- **Espacio: O(1)**. Al implementar el método de forma iterativa, solo se utilizan unas pocas variables auxiliares de tipo entero (`n`, `i`, `hijoIzq`, `hijoDer`), por lo que la memoria adicional requerida no depende del tamaño del vector de entrada.


![[Pasted image 20261108165242.png]]c


```Java

public boolean esHeapDeMaxima(int[] vector) {
    boolean esHeap = true;
    if (vector != null && vector.length > 1) {
        esHeap = esHeapRecursivo(vector, 0);
    }
    return esHeap;
}

private boolean esHeapRecursivo(int[] vector, int i) {
    boolean cumple = true;
    int n = vector.length;
    int izq = 2 * i + 1;
    int der = 2 * i + 2;
    if (izq < n) {
        cumple = vector[i] >= vector[izq] && esHeapRecursivo(vector, izq);
    }
    if (cumple && der < n) {
        cumple = vector[i] >= vector[der] && esHeapRecursivo(vector, der);
    }
    return cumple;
}
```

**Cómo funciona:**

  

- **Método envoltorio (Wrapper):** El método público principal recibe el vector, descarta casos triviales (nulo o longitud 1) y llama a un método privado pasándole el índice inicial `0` para comenzar la recursión.
    
- **Control de estado (Single Return):** Ambos métodos declaran una única variable booleana al inicio y la retornan al final de su ejecución, manteniendo la estructura limpia y centralizada.
    
- **Cálculo de posiciones:** En cada llamada recursiva, nos ubicamos en el nodo `i` y calculamos dónde deberían estar sus hijos: izquierdo (`2*i + 1`) y derecho (`2*i + 2`).
    
- **Verificación y cortocircuito:** Se comprueba si el hijo izquierdo existe (`izq < n`). De ser así, se valida que el padre sea mayor o igual a ese hijo y, usando el operador `&&`, si esa condición se cumple, se dispara la recursividad hacia ese subárbol. Si el padre ya es menor, el `&&` corta la ejecución y asigna `false` sin hacer la llamada recursiva.
    
- **Comprobación del hijo derecho:** La condición `if (cumple && der < n)` asegura que solo evaluemos el lado derecho si el lado izquierdo resultó ser válido. Si el lado izquierdo falló, ignoramos el derecho y devolvemos `false` inmediatamente.
    
- **Condición de corte natural:** Cuando el índice `i` corresponde a un nodo hoja (no tiene hijo izquierdo ni derecho), las condiciones de los `if` no se cumplen y el método retorna `true` directamente, cerrando esa rama de la recursión.

![[Pasted image 20261108170035.png]]


```Java
public boolean esHeapDeMaxima(int[] vector) {
    boolean esHeap = true;
    if (vector != null && vector.length > 1) {
        int n = vector.length;
        for (int i = 0; i <= (n / 2) - 1 && esHeap; i++) {
            int hijoIzq = 2 * i + 1;
            int hijoDer = 2 * i + 2;
            if (hijoIzq < n && vector[i] < vector[hijoIzq]) {
                esHeap = false;
            } else if (hijoDer < n && vector[i] < vector[hijoDer]) {
                esHeap = false;
            }
        }
    }
    return esHeap;
}
```

**Complejidad Algorítmica**

- **Tiempo: O(N)**. Siendo N la cantidad de elementos del vector, el ciclo recorre a lo sumo la mitad del arreglo `(n / 2) - 1`, procesando solo los nodos internos. Cada iteración realiza operaciones aritméticas y comparaciones de tiempo constante O(1).
    
      
    
- **Espacio: O(1)**. La implementación iterativa asigna únicamente variables primitivas auxiliares (`esHeap`, `n`, `i`, `hijoIzq`, `hijoDer`), ocupando una cantidad de memoria fija que no depende del tamaño del vector.
    
      
    

**Cómo funciona:**

  

- **Variable de estado:** Inicializamos `esHeap` en `true`. Si el vector es nulo o de un solo elemento (ya es un heap), no entra al condicional y retorna `true`.
    
      
    
- **Límite del ciclo `(n / 2) - 1`:** Se optimiza el recorrido iterando solo sobre los nodos que tienen al menos un hijo, evitando procesar nodos hoja innecesariamente.
    
      
    
- **Condición de corte:** La condición `&& esHeap` en el `for` interrumpe el ciclo apenas se encuentra un hijo mayor que su padre, optimizando el tiempo de ejecución.
    
      
    
- **Cálculo de posiciones:** Para cada nodo `i`, sus hijos se calculan con `2*i + 1` (izquierdo) y `2*i + 2` (derecho).
    
      
    
- **Comprobación de Máxima:** Se verifica que el índice del hijo esté dentro del límite del vector (`< n`) y que su valor no supere al del padre (`vector[i]`). Si lo supera, se rompe la regla marcando `esHeap = false`.
    
      
    
- **Único retorno:** Se preserva un solo punto de salida al final del método, retornando la variable `esHeap`.
- 
  
  # Recursiva

```Java
public boolean esHeapDeMaxima(int[] vector) {
    boolean esHeap = true;
    if (vector != null && vector.length > 1) {
        esHeap = esHeapRecursivo(vector, 0);
    }
    return esHeap;
}

private boolean esHeapRecursivo(int[] vector, int i) {
    boolean cumple = true;
    int n = vector.length;
    int izq = 2 * i + 1;
    int der = 2 * i + 2;
    if (izq < n) {
        cumple = vector[i] >= vector[izq] && esHeapRecursivo(vector, izq);
    }
    if (cumple && der < n) {
        cumple = vector[i] >= vector[der] && esHeapRecursivo(vector, der);
    }
    return cumple;
}
```

**Complejidad Algorítmica**

  

- **Tiempo: O(N)**. En el peor de los casos (cuando el arreglo efectivamente es un heap válido), la recursión visita cada nodo del árbol una vez. Cada llamada recursiva realiza comparaciones lógicas simples que toman tiempo constante O(1).
    
      
    
- **Espacio: O(log N)**. A diferencia de la versión iterativa, este enfoque utiliza memoria adicional en la pila de ejecución del sistema (Call Stack). Al tratarse de un heap (que estructuralmente es un árbol binario completo), la altura máxima del árbol es logarítmica respecto a N, lo que determina el límite de llamadas apiladas simultáneamente.
    
      
    

**Cómo funciona:**

  

- **Método envoltorio:** El método público sirve como punto de entrada seguro. Filtra vectores nulos o unitarios y lanza la recursión delegando el trabajo al método privado con el índice raíz `0`.
    
      
    
- **Control de estado (Single Return):** Ambos métodos utilizan una única variable booleana (`esHeap` y `cumple`) declarada al inicio y retornada al final, respetando estrictamente un único punto de salida por función.
    
      
    
- **Cálculo de posiciones:** En cada instancia recursiva, el nodo actual `i` identifica a sus hijos mediante las fórmulas matemáticas `2*i + 1` (izquierdo) y `2*i + 2` (derecho).
    
      
    
- **Evaluación izquierda y cortocircuito:** Si el hijo izquierdo existe, se verifica la propiedad de máxima (`vector[i] >= vector[izq]`). Gracias al operador `&&`, la llamada recursiva `esHeapRecursivo(vector, izq)` solo se ejecuta si la primera condición fue verdadera, cortando la ejecución temprana si se detecta un error.
    
      
    
- **Evaluación derecha:** El bloque `if (cumple && der < n)` asegura que el hijo derecho únicamente sea procesado si todo el subárbol izquierdo resultó válido hasta el momento.
    
      
    
- **Condición de corte (Nodos Hoja):** Cuando el índice `i` pertenece a un nodo sin hijos, las comprobaciones de existencia (`izq < n` y `der < n`) fallan, por lo que el método no entra a los condicionales y retorna el `cumple = true` inicial, finalizando esa rama de la recursión correctamente.
-
![[Pasted image 20261108170234.png]]