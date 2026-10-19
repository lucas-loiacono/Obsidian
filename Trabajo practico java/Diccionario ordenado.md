# `DiccionarioOrdenado<C, V>`: función por función, línea por línea

Este archivo es el mismo que subiste antes, sin cambios. Es un **árbol binario de búsqueda (ABB)** que guarda pares (clave, valor) y los mantiene ordenados por clave.

`Nodo<C, V>` no está subido. Por cómo se usa, asumo que tiene `clave`, `valor`, `hijoIzquierdo`, `hijoDerecho` y `padre`, con dos constructores: `(clave, valor)` y `(clave, valor, padre)`.

## La idea general

Regla del ABB: para cada nodo, todas las claves de su subárbol izquierdo son **menores** y las de su subárbol derecho son **mayores**.

```
        [5]
       /   \
     [3]   [8]
    /   \
  [1]   [4]
```

A diferencia de la lista, cada nodo tiene **tres** enlaces: hijo izquierdo, hijo derecho y padre.

## Atributos

```java
private Nodo<C, V> raiz;
private Comparador<C> comparador;
private int cantidadDatos;
```

- `raiz`: flecha al nodo de arriba de todo. Si es `null`, el árbol está vacío.
- `comparador`: decide si una clave es menor, igual o mayor que otra. `comparar(a, b)` devuelve negativo si `a < b`, 0 si son iguales y positivo si `a > b`.
- `cantidadDatos`: cuántos pares hay.

## Constructor con comparador

```java
if (comparador == null) {
    throw new ExcepcionDiccionario("El comparador no puede ser nulo.");
}
this.comparador = comparador;
this.raiz = null;
this.cantidadDatos = 0;
```

Sin comparador no se puede ordenar, así que `null` lanza excepción. Si no, guarda el comparador y deja el árbol vacío.

## Constructor de copia

```java
if (diccionarioOrdenado == null) {
    throw new ExcepcionDiccionario("El diccionario a copiar no puede ser nulo.");
}
this.comparador = diccionarioOrdenado.comparador;
this.cantidadDatos = diccionarioOrdenado.cantidadDatos;
this.raiz = clonarSubarbol(diccionarioOrdenado.raiz, null);
```

1. Si te pasan `null`, excepción.
2. Comparte el **mismo comparador** (no tiene estado que haya que separar).
3. Copia el contador.
4. Clona todo el árbol con `clonarSubarbol`, empezando por la raíz. Como la raíz no tiene padre, se le pasa `null`.

## `clonarSubarbol(actual, padre)` (privado)

Copia un nodo y, recursivamente, todo lo que cuelga de él.

```java
if (actual == null) {
    return null;
}
```

**Caso base**: si no hay nodo, no hay nada que copiar. Es lo que frena la recursión.

```java
Nodo<C, V> copia = new Nodo<>(actual.clave, actual.valor, padre);
```

Crea un nodo **nuevo** con la misma clave y valor, y con el `padre` que le pasaron. Todavía no tiene hijos.

```java
copia.hijoIzquierdo = clonarSubarbol(actual.hijoIzquierdo, copia);
copia.hijoDerecho = clonarSubarbol(actual.hijoDerecho, copia);
return copia;
```

Clona el subárbol izquierdo y lo cuelga como hijo izquierdo de `copia`. Hace lo mismo con el derecho. A los hijos se les pasa `copia` como padre, así quedan bien enlazados hacia arriba. Devuelve la `copia` para que quien llamó la cuelgue donde corresponde.

Es lo que en `Pila` hacías con dos flechas, pero en un árbol la recursión lo resuelve sola: cada llamada se ocupa de **un** nodo y delega el resto.

## `obtenerSucesorInmediato(nodo)` (privado)

El **sucesor** de un nodo es el que le sigue en el orden de claves, es decir, la menor clave que es mayor que la suya.

```java
if (nodo == null) {
    return null;
}
```

Si no hay nodo, no hay sucesor.

**Caso A: el nodo tiene hijo derecho.**

```java
if (nodo.hijoDerecho != null) {
    Nodo<C, V> actual = nodo.hijoDerecho;
    while (actual.hijoIzquierdo != null) {
        actual = actual.hijoIzquierdo;
    }
    return actual;
}
```

El sucesor es el **más a la izquierda** del subárbol derecho: se baja a la derecha una vez y después todo a la izquierda.

```
      [5]
         \
         [8]        sucesor de 5: derecha (8), luego izquierda (6)
        /   \
      [6]   [9]
```

**Caso B: no tiene hijo derecho.**

```java
Nodo<C, V> actual = nodo;
Nodo<C, V> padre = actual.padre;
while (padre != null && actual == padre.hijoDerecho) {
    actual = padre;
    padre = padre.padre;
}
return padre;
```

Hay que **subir** por los padres mientras se venga "desde la derecha". El primer ancestro al que se llega desde la izquierda es el sucesor. Si se llega a `null`, el nodo era el mayor de todos y no tiene sucesor.

Ojo: en `eliminar` solo se la llama con nodos que tienen dos hijos, así que ahí siempre se usa el caso A.

## `agregar(clave, valor)`

```java
if (clave == null) {
    throw new ExcepcionDiccionario("La clave no puede ser nula.");
}
```

No se puede comparar una clave nula.

**Árbol vacío:**

```java
if (this.raiz == null) {
    this.raiz = new Nodo<>(clave, valor);
    this.cantidadDatos++;
    return null;
}
```

El nodo nuevo es la raíz. Devuelve `null` porque no había valor anterior. Este caso va aparte porque en el código de abajo `padre` quedaría en `null`.

**Árbol con datos:** se baja comparando hasta encontrar la clave o un hueco.

```java
Nodo<C, V> actual = this.raiz;
Nodo<C, V> padre = null;
int comparacion = 0;
```

- `actual`: flecha que baja por el árbol.
- `padre`: flecha que va **un paso atrás** de `actual`.
- `comparacion`: se declara afuera del `while` para poder usar su último valor después.

```java
while (actual != null) {
    comparacion = this.comparador.comparar(clave, actual.clave);
```

Compara la clave a insertar con la del nodo actual.

```java
    if (comparacion == 0) {
        V valorAnterior = actual.valor;
        actual.valor = valor;
        return valorAnterior;
    }
```

Si la clave ya existe, **reemplaza el valor** y devuelve el anterior. No se crea un nodo ni cambia el contador.

```java
    padre = actual;
    if (comparacion < 0) {
        actual = actual.hijoIzquierdo;
    } else {
        actual = actual.hijoDerecho;
    }
}
```

Si no, `padre` pasa a ser el nodo actual, y `actual` baja a la izquierda (si la clave es menor) o a la derecha (si es mayor).

El `while` termina cuando `actual == null`, o sea cuando se llegó a un hueco. Ahí, `padre` es el último nodo real y `comparacion` indica de qué lado del padre está el hueco.

```java
Nodo<C, V> nuevo = new Nodo<>(clave, valor, padre);
if (comparacion < 0) {
    padre.hijoIzquierdo = nuevo;
} else {
    padre.hijoDerecho = nuevo;
}
this.cantidadDatos++;
return null;
```

Crea el nodo con su `padre`, lo cuelga del lado correcto, suma 1 y devuelve `null`.

Ejemplo: insertar 4 en `5 → 3 → (1, _)`:

```
comparar(4,5) < 0 → izquierda (3)
comparar(4,3) > 0 → derecha (hueco)
padre = 3, comparacion > 0 → 3.hijoDerecho = [4]
```

## `buscarNodo(clave)` (privado)

```java
Nodo<C, V> actual = this.raiz;
while (actual != null) {
    int comparacion = this.comparador.comparar(clave, actual.clave);
    if (comparacion == 0) {
        return actual;
    } else if (comparacion < 0) {
        actual = actual.hijoIzquierdo;
    } else {
        actual = actual.hijoDerecho;
    }
}
return null;
```

Es la misma bajada que `agregar`: si es igual, devuelve el nodo; si es menor, va a la izquierda; si es mayor, a la derecha. Si baja hasta `null`, la clave no está y devuelve `null`.

## `obtenerValor(clave)`

```java
if (clave == null) {
    throw new ExcepcionDiccionario("La clave no puede ser nula.");
}
Nodo<C, V> nodo = buscarNodo(clave);
return (nodo != null) ? nodo.valor : null;
```

Valida la clave, busca el nodo y devuelve su valor, o `null` si no existe. Con esto no se puede distinguir "la clave no existe" de "la clave existe con valor `null`".

## `eliminar(clave)`

```java
if (clave == null) { throw ... }
Nodo<C, V> nodoAEliminar = buscarNodo(clave);
if (nodoAEliminar == null) {
    return null;
}
V valorEliminado = nodoAEliminar.valor;
```

Busca el nodo. Si no existe, no hace nada y devuelve `null`. Si existe, guarda su valor **antes** de tocar nada, porque en el caso de dos hijos se va a pisar.

**Caso 1: dos hijos.**

```java
if (nodoAEliminar.hijoIzquierdo != null && nodoAEliminar.hijoDerecho != null) {
    Nodo<C, V> sucesor = obtenerSucesorInmediato(nodoAEliminar);
    nodoAEliminar.clave = sucesor.clave;
    nodoAEliminar.valor = sucesor.valor;
    reemplazarNodo(sucesor, sucesor.hijoDerecho);
}
```

No se puede sacar un nodo con dos hijos sin dejar un agujero. El truco es:

1. Buscar el **sucesor** (el menor del subárbol derecho).
2. **Copiar** su clave y valor en el nodo a eliminar. El nodo físico se queda, pero ahora tiene otro contenido.
3. Eliminar el nodo del sucesor, que como mucho tiene un hijo derecho (nunca izquierdo, porque es el más a la izquierda). Se lo reemplaza por ese hijo.

```
eliminar 5:
        [5]                 [6]
       /   \               /   \
     [3]   [8]    →      [3]   [8]
          /   \                  \
        [6]   [9]                [9]
```

**Caso 2: cero o un hijo.**

```java
} else {
    Nodo<C, V> hijo = (nodoAEliminar.hijoIzquierdo != null)
            ? nodoAEliminar.hijoIzquierdo
            : nodoAEliminar.hijoDerecho;
    reemplazarNodo(nodoAEliminar, hijo);
}
```

`hijo` es el hijo izquierdo si existe; si no, el derecho (que puede ser `null` si es una hoja). Después se reemplaza el nodo por ese hijo, o sea, el hijo "sube" a ocupar su lugar.

```java
this.cantidadDatos--;
return valorEliminado;
```

Resta 1 y devuelve el valor guardado al principio.

## `reemplazarNodo(nodoAReemplazar, reemplazo)` (privado)

Hace que `reemplazo` ocupe el lugar de `nodoAReemplazar` en el árbol.

```java
if (nodoAReemplazar.padre == null) {
    this.raiz = reemplazo;
} else if (nodoAReemplazar == nodoAReemplazar.padre.hijoIzquierdo) {
    nodoAReemplazar.padre.hijoIzquierdo = reemplazo;
} else {
    nodoAReemplazar.padre.hijoDerecho = reemplazo;
}
```

Arregla el enlace de **arriba hacia abajo** (padre → hijo). Hay tres casos:

- Sin padre: era la raíz, así que `raiz` pasa a ser `reemplazo`.
- Era el hijo izquierdo de su padre: el padre apunta a `reemplazo` por la izquierda.
- Si no, era el hijo derecho: el padre apunta a `reemplazo` por la derecha.

```java
if (reemplazo != null) {
    reemplazo.padre = nodoAReemplazar.padre;
}
```

Arregla el enlace de **abajo hacia arriba** (hijo → padre). El `if` es necesario porque `reemplazo` puede ser `null`.

Como el árbol tiene enlaces en las dos direcciones, hay que arreglar los dos, igual que en la lista doble cuando se arreglaban `anterior` y `siguiente`.

## Recorridos

Los cuatro devuelven una `Lista<Tupla<C, V>>` y usan el mismo esquema: un método público que crea la lista de resultado y llama a uno privado recursivo. Los tres recursivos tienen el mismo caso base (`if (actual != null)`) y solo cambia **cuándo** se agrega el nodo respecto de sus hijos.

|Recorrido|Orden|Línea del `agregar`|
|---|---|---|
|**inorder**|izquierdo, nodo, derecho|en el medio|
|**preorder**|nodo, izquierdo, derecho|primero|
|**postorder**|izquierdo, derecho, nodo|al final|

Con el árbol del ejemplo (`5; 3 y 8; 1 y 4` bajo el 3):

- **inorder**: 1, 3, 4, 5, 8. Sale **ordenado por clave**.
- **preorder**: 5, 3, 1, 4, 8. Sirve, por ejemplo, para copiar la estructura.
- **postorder**: 1, 4, 3, 8, 5. Primero los hijos y al final el padre.

Cada nodo se guarda como `new Tupla<>(clave, valor)`.

## `ancho()`: recorrido por niveles

```java
Lista<Tupla<C, V>> resultado = new Lista<>();
if (this.raiz == null) {
    return resultado;
}
```

Si el árbol está vacío, devuelve la lista vacía.

```java
Cola<Nodo<C, V>> cola = new Cola<>();
cola.agregar(this.raiz);
```

Usa una **cola** de nodos y arranca con la raíz.

```java
while (!cola.vacio()) {
    Nodo<C, V> actual = cola.eliminar();
    resultado.agregar(new Tupla<>(actual.clave, actual.valor));
    if (actual.hijoIzquierdo != null) {
        cola.agregar(actual.hijoIzquierdo);
    }
    if (actual.hijoDerecho != null) {
        cola.agregar(actual.hijoDerecho);
    }
}
return resultado;
```

Mientras haya nodos en la cola:

1. Saca el primero (el más antiguo).
2. Lo agrega al resultado.
3. Encola sus hijos, izquierdo y luego derecho, si existen.

Como la cola es FIFO, los hijos se atienden **después** de todos los nodos que ya estaban esperando, y por eso se recorre nivel por nivel:

```
cola: [5]                → sale 5, entran 3, 8
cola: [3, 8]             → sale 3, entran 1, 4
cola: [8, 1, 4]          → sale 8
cola: [1, 4]             → salen 1 y 4
resultado: 5, 3, 8, 1, 4
```

Con la lista y los recursivos no se podía hacer, porque los recursivos usan la pila de llamadas (que es una pila, LIFO) y el ancho necesita una cola.

## `tamanio()` y `vacio()`

```java
return this.cantidadDatos;        // tamanio
return this.cantidadDatos == 0;   // vacio
```

Los dos usan el contador, O(1).

## Resumen para el anotador

|Método|Qué hace|Costo (árbol parejo / degenerado)|
|---|---|---|
|`agregar`|baja comparando y cuelga una hoja, o reemplaza el valor|O(log n) / O(n)|
|`buscarNodo` / `obtenerValor`|baja comparando|O(log n) / O(n)|
|`eliminar`|0-1 hijo: lo reemplaza por su hijo; 2 hijos: copia el sucesor y elimina el sucesor|O(log n) / O(n)|
|`obtenerSucesorInmediato`|menor del subárbol derecho, o primer ancestro "desde la izquierda"|O(altura)|
|`clonarSubarbol`|copia recursiva con nodos nuevos|O(n)|
|`inorder` / `preorder` / `postorder` / `ancho`|recorren todo el árbol|O(n)|
|`tamanio` / `vacio`|contador|O(1)|

Reglas para no confundirte:

> Al **eliminar**: 0 o 1 hijo → el hijo sube. 2 hijos → copio el sucesor y elimino el sucesor.  
> Al **enlazar** en un árbol: siempre arreglo los dos sentidos (padre → hijo e hijo → padre).

Si querés, hacemos un seguimiento de `eliminar` con un nodo de dos hijos dibujando los enlaces antes y después de `reemplazarNodo`.