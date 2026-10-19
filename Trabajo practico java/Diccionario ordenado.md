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













# 2do resumen

# `DiccionarioOrdenado`: explicado con un ejemplo

Uso **un solo árbol de ejemplo** en todas las funciones, para que puedas seguir qué pasa con cada flecha.

## Antes de las funciones

### Qué guarda cada nodo

`Nodo` no está subido, pero por cómo se usa tiene:

```
clave, valor, hijoIzquierdo, hijoDerecho, padre
```

Es igual que el nodo de la lista, pero en vez de `anterior` y `siguiente` tiene tres enlaces.

### La regla del árbol

Para cualquier nodo:

- todo lo que cuelga a su **izquierda** tiene claves **menores**
- todo lo que cuelga a su **derecha** tiene claves **mayores**

### El árbol de ejemplo

```
          5
        /   \
       3     8
      / \   / \
     1   4 6   9
```

Cada nodo apunta a sus hijos y también a su padre. Por ejemplo, el 4 tiene `padre = 3`, y el 3 tiene `hijoDerecho = 4`.

### Los atributos

```java
private Nodo<C, V> raiz;
private Comparador<C> comparador;
private int cantidadDatos;
```

- `raiz`: flecha al nodo de arriba de todo (el 5). Si vale `null`, el árbol está vacío. Es la única entrada al árbol, como `primero` en la lista.
- `comparador`: sirve para comparar dos claves. `comparar(a, b)` da **negativo** si `a < b`, **0** si son iguales y **positivo** si `a > b`.
- `cantidadDatos`: cuántos nodos hay.

## Constructor con comparador

```java
if (comparador == null) {
    throw new ExcepcionDiccionario("El comparador no puede ser nulo.");
}
```

Sin comparador no se puede saber qué clave va a la izquierda y cuál a la derecha. Por eso, si es `null`, lanza excepción.

```java
this.comparador = comparador;
this.raiz = null;
this.cantidadDatos = 0;
```

Guarda el comparador, deja el árbol vacío y el contador en 0.

## `agregar(clave, valor)`

Acá se entiende el 80% del archivo. La idea es: **bajar por el árbol comparando hasta encontrar un hueco, y colgar ahí el nodo nuevo**.

```java
if (clave == null) {
    throw new ExcepcionDiccionario("La clave no puede ser nula.");
}
```

No se puede comparar `null`, así que se rechaza.

```java
if (this.raiz == null) {
    this.raiz = new Nodo<>(clave, valor);
    this.cantidadDatos++;
    return null;
}
```

Si el árbol está vacío, el nodo nuevo es la raíz. Devuelve `null` porque no había un valor anterior. Este caso va aparte porque el código de abajo necesita tener un `padre` para colgar el nodo, y la raíz no tiene.

```java
Nodo<C, V> actual = this.raiz;
Nodo<C, V> padre = null;
int comparacion = 0;
```

Tres variables:

- `actual`: una flecha que **baja** por el árbol. Empieza en la raíz.
- `padre`: una flecha que va **un paso atrás** de `actual`. Siempre señala el nodo del que acabamos de bajar. Empieza en `null`.
- `comparacion`: guarda el último resultado de comparar. Se declara **afuera** del `while` para poder usarla después de que termine.

```java
while (actual != null) {
```

Mientras `actual` señale un nodo real, seguimos bajando. Cuando `actual` vale `null`, llegamos a un **hueco**, o sea el lugar donde va el nodo nuevo.

```java
    comparacion = this.comparador.comparar(clave, actual.clave);
```

Compara la clave que queremos insertar con la del nodo donde estamos parados.

```java
    if (comparacion == 0) {
        V valorAnterior = actual.valor;
        actual.valor = valor;
        return valorAnterior;
    }
```

Si son iguales, la clave **ya existe**. No se crea ningún nodo: se reemplaza el valor, y se devuelve el valor viejo.

```java
    padre = actual;
```

Antes de bajar, `padre` se queda parado en el nodo actual. Esto es lo que hace que `padre` siempre vaya un paso atrás.

```java
    if (comparacion < 0) {
        actual = actual.hijoIzquierdo;
    } else {
        actual = actual.hijoDerecho;
    }
}
```

Si la clave nueva es menor, baja a la izquierda; si es mayor, a la derecha. Esto es solo **mover la flecha** `actual`; no se modifica ningún nodo.

```java
Nodo<C, V> nuevo = new Nodo<>(clave, valor, padre);
```

Salimos del `while`: `actual` es `null` y `padre` es el último nodo real. Se crea el nodo nuevo y se le dice quién es su padre.

```java
if (comparacion < 0) {
    padre.hijoIzquierdo = nuevo;
} else {
    padre.hijoDerecho = nuevo;
}
```

El nodo nuevo todavía no está enganchado desde arriba. `comparacion` guarda cómo se comparó la clave con el padre en la **última** vuelta, así que sabemos de qué lado está el hueco: si fue menor, va a la izquierda del padre; si no, a la derecha. Acá sí **se modifica un nodo**.

```java
this.cantidadDatos++;
return null;
```

Suma 1 y devuelve `null` (no había valor anterior).

### Seguimiento: `agregar(7, "x")` en el árbol de ejemplo

|Vuelta|`actual`|comparación|`padre` después|`actual` después|
|---|---|---|---|---|
|1|5|7 > 5 → positivo|5|8 (derecha)|
|2|8|7 < 8 → negativo|8|6 (izquierda)|
|3|6|7 > 6 → positivo|6|`null` (derecha de 6 está vacía)|

Sale del `while`. `padre = 6` y `comparacion` es positivo, así que `6.hijoDerecho = [7]`.

```
       8
      / \
     6   9
      \
       7   ← nuevo
```

## `buscarNodo(clave)`

Es la misma bajada que `agregar`, pero sin insertar.

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

- `actual` arranca en la raíz.
- Si la clave es igual a la del nodo, **lo encontró** y devuelve el nodo.
- Si es menor, baja a la izquierda; si es mayor, a la derecha.
- Si `actual` llega a `null`, bajó hasta un hueco sin encontrarla: la clave no está y devuelve `null`.

Seguimiento de `buscarNodo(4)`: 4 < 5 → izquierda (3). 4 > 3 → derecha (4). 4 == 4 → devuelve el nodo 4.

## `obtenerValor(clave)`

```java
if (clave == null) { throw ... }
Nodo<C, V> nodo = buscarNodo(clave);
return (nodo != null) ? nodo.valor : null;
```

Busca el nodo y devuelve su valor. La última línea es un `if` abreviado (operador ternario):

```java
return (nodo != null) ? nodo.valor : null;
```

significa: "si `nodo` no es `null`, devolvé `nodo.valor`; si no, devolvé `null`". Hace falta porque, si el nodo no existe, `nodo.valor` daría `NullPointerException`.

## `eliminar(clave)`

Es la función más difícil, pero se divide en **tres casos** según cuántos hijos tiene el nodo a eliminar.

```java
Nodo<C, V> nodoAEliminar = buscarNodo(clave);
if (nodoAEliminar == null) {
    return null;
}
V valorEliminado = nodoAEliminar.valor;
```

Busca el nodo. Si no existe, no hace nada. Si existe, **guarda su valor antes de tocar nada**, porque en el caso de dos hijos ese valor se va a pisar.

```java
if (nodoAEliminar.hijoIzquierdo != null && nodoAEliminar.hijoDerecho != null) {
    // CASO 3: dos hijos
} else {
    // CASOS 1 y 2: cero o un hijo
}
```

### Casos 1 y 2: cero o un hijo

```java
Nodo<C, V> hijo = (nodoAEliminar.hijoIzquierdo != null)
        ? nodoAEliminar.hijoIzquierdo
        : nodoAEliminar.hijoDerecho;
reemplazarNodo(nodoAEliminar, hijo);
```

`hijo` es el hijo izquierdo si existe; si no, el derecho. Si el nodo es una hoja, `hijo` queda en `null`. Después, `reemplazarNodo` hace que ese hijo **ocupe el lugar** del nodo eliminado.

**Ejemplo, eliminar una hoja (el 1):** `hijo = null`. El 3 pasa a tener `hijoIzquierdo = null`.

```
antes:    3          después:   3
         / \                     \
        1   4                     4
```

**Ejemplo, un hijo:** si ahora eliminás el 3 (que solo tiene al 4), `hijo = 4`. El 4 sube a ocupar el lugar del 3 colgando del 5.

```
antes:    5            después:   5
         /                       /
        3                       4
         \
          4
```

### Caso 3: dos hijos

No se puede simplemente sacar el nodo, porque quedarían dos subárboles sueltos. El truco es **no sacar el nodo, sino cambiarle el contenido**:

```java
Nodo<C, V> sucesor = obtenerSucesorInmediato(nodoAEliminar);
nodoAEliminar.clave = sucesor.clave;
nodoAEliminar.valor = sucesor.valor;
reemplazarNodo(sucesor, sucesor.hijoDerecho);
```

1. Se busca el **sucesor**: el nodo con la clave que sigue inmediatamente a la que borramos (la menor de las mayores).
2. Se **copia** su clave y valor sobre el nodo a eliminar. El nodo físico se queda, pero ahora tiene otro contenido.
3. Se elimina el nodo del sucesor, que como mucho tiene un hijo derecho. Es un caso fácil (0 o 1 hijo).

**Ejemplo, eliminar el 5 del árbol original:**

- sucesor del 5 = **6**.
- el nodo que tenía el 5 pasa a tener el 6.
- se elimina el nodo viejo del 6 (hoja), así que `8.hijoIzquierdo = null`.

```
antes:         5                 después:       6
             /   \                            /   \
            3     8                          3     8
           / \   / \                        / \     \
          1   4 6   9                      1   4     9
```

El orden de claves sigue siendo válido: 1, 3, 4, 6, 8, 9.

```java
this.cantidadDatos--;
return valorEliminado;
```

Se resta 1 (en cualquier caso se elimina un nodo físico) y se devuelve el valor guardado al principio.

## `obtenerSucesorInmediato(nodo)`

El sucesor es la clave que sigue en orden. Hay dos casos.

```java
if (nodo == null) {
    return null;
}
```

Si no hay nodo, no hay sucesor.

### Caso A: el nodo tiene hijo derecho

```java
if (nodo.hijoDerecho != null) {
    Nodo<C, V> actual = nodo.hijoDerecho;
    while (actual.hijoIzquierdo != null) {
        actual = actual.hijoIzquierdo;
    }
    return actual;
}
```

Se baja **una vez a la derecha**, y después **todo lo que se pueda a la izquierda**. El último nodo así es el menor del subárbol derecho, o sea el que sigue.

Sucesor del 5: derecha → 8; izquierda → 6; el 6 no tiene hijo izquierdo, así que se frena. **Sucesor = 6.**

Este es el único caso que usa `eliminar`, porque solo llama a esta función con nodos de dos hijos.

### Caso B: el nodo no tiene hijo derecho

```java
Nodo<C, V> actual = nodo;
Nodo<C, V> padre = actual.padre;
while (padre != null && actual == padre.hijoDerecho) {
    actual = padre;
    padre = padre.padre;
}
return padre;
```

Hay que **subir** hasta el primer ancestro que quede a la derecha de donde veníamos. Mientras `actual` sea el hijo **derecho** de su padre, sigo subiendo (ese padre es menor que yo, no me sirve). Cuando vengo por la **izquierda**, ese padre es mayor: es el sucesor.

Sucesor del 4: el 4 es hijo derecho del 3, así que subo a 3. El 3 es hijo **izquierdo** del 5, así que freno. **Sucesor = 5.** Y el sucesor del 9 sería `null`, porque sube hasta pasar la raíz (es el mayor de todos).

## `reemplazarNodo(nodoAReemplazar, reemplazo)`

Hace que `reemplazo` ocupe el lugar de `nodoAReemplazar`. Como el árbol tiene enlaces en **los dos sentidos**, hay que arreglar los dos.

```java
if (nodoAReemplazar.padre == null) {
    this.raiz = reemplazo;
} else if (nodoAReemplazar == nodoAReemplazar.padre.hijoIzquierdo) {
    nodoAReemplazar.padre.hijoIzquierdo = reemplazo;
} else {
    nodoAReemplazar.padre.hijoDerecho = reemplazo;
}
```

**Enlace de arriba hacia abajo** (padre → hijo). Hay que averiguar de qué lado colgaba el nodo:

- Si no tiene padre, era la raíz: `raiz` pasa a ser `reemplazo`.
- Si era el hijo izquierdo de su padre, el padre apunta a `reemplazo` por la izquierda.
- Si no, era el derecho, y el padre apunta a `reemplazo` por la derecha.

```java
if (reemplazo != null) {
    reemplazo.padre = nodoAReemplazar.padre;
}
```

**Enlace de abajo hacia arriba** (hijo → padre). El reemplazo ahora tiene el padre del nodo viejo. El `if` es necesario porque `reemplazo` puede ser `null` (si se elimina una hoja), y `null.padre` daría error.

Es igual a lo que hacías en la lista doble: arreglar `anterior` y `siguiente`.

## `clonarSubarbol(actual, padre)`

Copia un nodo **y todo lo que cuelga de él**. Es **recursiva**: se llama a sí misma.

La forma de entenderla es: _"cada llamada se ocupa de UN nodo y le delega el resto a otras llamadas"_.

```java
if (actual == null) {
    return null;
}
```

**Caso base**: si no hay nodo, no hay nada que copiar. Es lo que frena la recursión.

```java
Nodo<C, V> copia = new Nodo<>(actual.clave, actual.valor, padre);
```

Crea un nodo **nuevo** con la misma clave y valor. Recibe como `padre` el que le pasaron.

```java
copia.hijoIzquierdo = clonarSubarbol(actual.hijoIzquierdo, copia);
copia.hijoDerecho = clonarSubarbol(actual.hijoDerecho, copia);
return copia;
```

Le pide a otras llamadas que clonen el subárbol izquierdo y el derecho, y cuelga lo que devuelvan. A los hijos se les pasa `copia` como padre, así quedan bien enlazados hacia arriba. Al final devuelve `copia`.

Seguimiento con un árbol de 3 nodos (5 con hijos 3 y 8):

```
clonar(5, null)
 ├─ crea 5' (padre null)
 ├─ 5'.izq = clonar(3, 5')
 │     ├─ crea 3' (padre 5')
 │     ├─ clonar(null) → null  (3 no tiene hijos)
 │     └─ devuelve 3'
 ├─ 5'.der = clonar(8, 5')
 │     └─ ... devuelve 8'
 └─ devuelve 5'
```

Y en el constructor de copia se usa así:

```java
this.raiz = clonarSubarbol(diccionarioOrdenado.raiz, null);
```

La raíz no tiene padre, por eso se pasa `null`. El comparador se comparte (no tiene estado) y `cantidadDatos` se copia como número.

## Recorridos: `inorder`, `preorder`, `postorder`

Los tres funcionan igual. Hay un método público que crea una lista vacía y llama a uno recursivo:

```java
Lista<Tupla<C, V>> resultado = new Lista<>();
inorderRecursivo(this.raiz, resultado);
return resultado;
```

Y el recursivo es:

```java
if (actual != null) {
    inorderRecursivo(actual.hijoIzquierdo, resultado);   // 1) izquierda
    resultado.agregar(new Tupla<>(actual.clave, actual.valor)); // 2) el nodo
    inorderRecursivo(actual.hijoDerecho, resultado);     // 3) derecha
}
```

El `if (actual != null)` es el caso base. **Lo único que cambia entre los tres es en qué momento se agrega el nodo**:

|Recorrido|Orden|
|---|---|
|**preorder**|nodo, izquierda, derecha|
|**inorder**|izquierda, nodo, derecha|
|**postorder**|izquierda, derecha, nodo|

Con el árbol de ejemplo:

- **inorder**: 1, 3, 4, 5, 6, 8, 9 (**ordenado**)
- **preorder**: 5, 3, 1, 4, 8, 6, 9
- **postorder**: 1, 4, 3, 6, 9, 8, 5

Seguimiento de `inorder` con el árbol 5 (hijos 3 y 8):

```
inorder(5)
  inorder(3)
     inorder(null) → nada
     agrega 3
     inorder(null) → nada
  agrega 5
  inorder(8)
     ... agrega 8
```

Resultado: 3, 5, 8.

Es ordenado porque, primero, se agrega todo lo menor que el nodo (su izquierda), después el nodo, y después todo lo mayor (su derecha).

## `ancho()`

Recorre **por niveles**, de arriba hacia abajo y de izquierda a derecha. Usa una **cola**, no recursión.

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

Crea una cola de **nodos** y arranca con la raíz.

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

En cada vuelta: saca el nodo del frente, lo agrega al resultado, y **encola sus hijos** (si existen). Como la cola es FIFO, los hijos esperan detrás de todos los que ya estaban, y por eso se avanza nivel por nivel.

Seguimiento con el árbol de ejemplo:

|Sale|Entra|Cola después|Resultado|
|---|---|---|---|
|5|3, 8|[3, 8]|5|
|3|1, 4|[8, 1, 4]|5, 3|
|8|6, 9|[1, 4, 6, 9]|5, 3, 8|
|1|—|[4, 6, 9]|5, 3, 8, 1|
|4|—|[6, 9]|..., 4|
|6|—|[9]|..., 6|
|9|—|[]|5, 3, 8, 1, 4, 6, 9|

La cola es la estructura correcta acá porque el primero que entra tiene que ser el primero en procesarse.

## `tamanio()` y `vacio()`

```java
return this.cantidadDatos;
return this.cantidadDatos == 0;
```

Devuelven el contador, sin recorrer nada.

## Resumen para el anotador

|Función|En una frase|
|---|---|
|`agregar`|bajo comparando con dos flechas (`actual` y `padre`) hasta un hueco, y cuelgo ahí el nodo|
|`buscarNodo`|la misma bajada, devuelvo el nodo o `null`|
|`eliminar`|0 o 1 hijo: el hijo sube. 2 hijos: copio el sucesor y elimino el nodo del sucesor|
|`obtenerSucesorInmediato`|con hijo derecho: derecha una vez y toda la izquierda. Sin hijo derecho: subo hasta venir por la izquierda|
|`reemplazarNodo`|arreglo padre→hijo e hijo→padre|
|`clonarSubarbol`|recursiva: copio un nodo y delego los hijos|
|`inorder/pre/post`|recursivas, solo cambia cuándo se agrega el nodo|
|`ancho`|cola: saco uno, lo guardo, encolo sus hijos|

Las dos ideas que más sirve tener clara:

> **Bajar por el árbol** (agregar, buscar): menor → izquierda, mayor → derecha.  
> **Enlazar**: siempre se arreglan los dos sentidos (padre → hijo e hijo → padre).

Si querés, hacemos juntos el seguimiento de `eliminar(5)` con los valores de cada flecha (`sucesor`, `padre`, `raiz`) antes y después de `reemplazarNodo`.