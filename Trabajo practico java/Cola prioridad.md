# `ColaPrioridad<T>`: función por función

## La idea general

Una **cola de prioridad** no atiende por orden de llegada (como `Cola`), sino por **prioridad**: siempre sale el elemento de mayor prioridad, sin importar cuándo entró. Es como la guardia de un hospital: atienden primero al más grave.

Se implementa con un **heap** (montículo) guardado en un **vector**, no con nodos enlazados. Por eso ya no hay `Nodo`, `primero` ni `ultimo`.

## Los atributos

```java
private VectorDinamico<T> datos;
private Comparador<T> comparador;
```

- `datos`: un vector que crece solo y guarda los elementos ordenados como heap.
- `comparador`: un objeto que decide **quién tiene más prioridad**. Tiene un método `comparar(a, b)`. En este código:
    - `comparar(a, b) > 0` significa que **`a` tiene mayor prioridad que `b`**.

No se subió `VectorDinamico`, así que asumo lo que muestran los usos: `agregar(dato)` suma al final, `obtener(i)` lee, `cambiar(i, dato)` pisa la posición `i`, `eliminar()` quita **el último** y lo devuelve, y `tamanio()` y `vacio()`.

## Cómo es un heap en un vector

Un heap es un **árbol** con una regla (el invariante):

> Cada elemento tiene **mayor o igual prioridad que sus hijos**.

Por eso el de mayor prioridad siempre está arriba de todo (posición 0). El árbol se guarda en el vector, por niveles, sin punteros:

```
vector:  [8, 3, 5, 1]
índice:   0  1  2  3

árbol:        8          (índice 0)
            /   \
           3     5       (índices 1 y 2)
          /
         1               (índice 3)
```

Las fórmulas para moverse en el árbol:

|Quién|Fórmula|
|---|---|
|padre de `i`|`(i - 1) / 2`|
|hijo izquierdo de `i`|`2 * i + 1`|
|hijo derecho de `i`|`2 * i + 2`|

Con eso se navega el árbol solo con aritmética.

## Constructor con comparador

```java
if (comparador == null) {
    throw new ExcepcionColaPrioridad("El comparador no puede ser nulo.");
}
this.comparador = comparador;
this.datos = new VectorDinamico<>();
```

Sin comparador no se puede saber quién tiene más prioridad, así que si es `null` lanza excepción. Si no, guarda el comparador y crea un vector vacío.

## Constructor de copia

```java
if (colaPrioridad == null) {
    throw new ExcepcionColaPrioridad("La cola de prioridad a copiar no puede ser nula.");
}
this.comparador = colaPrioridad.comparador;
this.datos = new VectorDinamico<>(colaPrioridad.datos);
```

1. Si te pasan `null`, excepción.
2. Reutiliza el **mismo comparador** (se comparte la referencia; no tiene estado que haya que separar).
3. Copia el vector con el constructor de copia de `VectorDinamico`. Como el vector ya cumple el invariante del heap, **la copia también lo cumple**: no hace falta reordenar nada ni recorrer elemento por elemento como en `Lista`.

## `agregar(T dato)`

```java
this.datos.agregar(dato);
heapificarHaciaArriba();
```

1. Agrega el dato al **final** del vector (última hoja del árbol). Esto puede romper el invariante: el nuevo podría tener más prioridad que su padre.
2. `heapificarHaciaArriba()` lo "sube" hasta su lugar.

## `heapificarHaciaArriba()` (privado)

```java
int indiceActual = this.datos.tamanio() - 1;
boolean cumpleInvariante = false;
```

Arranca en el **último** elemento (el recién agregado). `cumpleInvariante` es una bandera para cortar el ciclo.

```java
while (indiceActual > 0 && !cumpleInvariante) {
```

Repite mientras no haya llegado a la raíz (índice 0, que no tiene padre) y mientras no esté ya en su lugar.

```java
int indicePadre = (indiceActual - 1) / 2;
T datoActual = this.datos.obtener(indiceActual);
T datoPadre = this.datos.obtener(indicePadre);
```

Calcula dónde está el padre y lee ambos datos.

```java
if (this.comparador.comparar(datoActual, datoPadre) > 0) {
    this.datos.cambiar(indiceActual, datoPadre);
    this.datos.cambiar(indicePadre, datoActual);
    indiceActual = indicePadre;
} else {
    cumpleInvariante = true;
}
```

- **Si el actual tiene más prioridad que su padre**: los **intercambia** (el padre baja a donde estaba el actual, y el actual sube a donde estaba el padre) y pasa a mirar la nueva posición del dato (`indiceActual = indicePadre`), para ver si tiene que seguir subiendo.
- **Si no**: ya está bien ubicado, corta.

Como el árbol tiene altura de log₂(n), sube como mucho esa cantidad de niveles.

## `eliminar()`

```java
if (vacio()) {
    throw new ExcepcionColaPrioridad("La cola de prioridad está vacía.");
}
T datoEliminado = this.datos.obtener(0);
```

Si está vacía, excepción. Si no, guarda el dato de la posición 0: es el de mayor prioridad y el que se va a devolver.

```java
if (this.datos.tamanio() == 1) {
    this.datos.eliminar();
} else {
    T ultimoDato = this.datos.eliminar();
    this.datos.cambiar(0, ultimoDato);
    heapificarHaciaAbajo();
}
return datoEliminado;
```

- **Un solo elemento**: se quita y listo.
- **Más de uno**: no se puede dejar un "agujero" en la raíz. El truco es:
    1. `this.datos.eliminar()` quita el **último** del vector (es barato, no hay que correr nada) y lo devuelve en `ultimoDato`.
    2. `cambiar(0, ultimoDato)` lo pone en la raíz, pisando al que se va.
    3. Ese dato probablemente no tiene la prioridad más alta, así que rompe el invariante desde arriba. `heapificarHaciaAbajo()` lo "hunde" hasta su lugar.

## `heapificarHaciaAbajo()` (privado)

```java
int indiceActual = 0;
int tamanio = this.datos.tamanio();
boolean cumpleInvariante = false;
```

Arranca en la raíz.

```java
while (2 * indiceActual + 1 < tamanio && !cumpleInvariante) {
```

Repite mientras el nodo tenga **al menos un hijo** (si el hijo izquierdo no existe, tampoco el derecho, porque el heap se llena de izquierda a derecha) y no esté ya bien ubicado.

```java
int indiceHijoIzq = 2 * indiceActual + 1;
int indiceHijoDer = 2 * indiceActual + 2;
int indiceMayorPrioridad = indiceHijoIzq;
```

Calcula los dos hijos y asume que el mayor es el izquierdo.

```java
if (indiceHijoDer < tamanio
        && this.comparador.comparar(
        this.datos.obtener(indiceHijoDer),
        this.datos.obtener(indiceHijoIzq)) > 0) {
    indiceMayorPrioridad = indiceHijoDer;
}
```

Si el hijo derecho **existe** y tiene más prioridad que el izquierdo, el mayor pasa a ser el derecho. El chequeo `indiceHijoDer < tamanio` va primero para no leer fuera del vector.

```java
T datoActual = this.datos.obtener(indiceActual);
T datoHijoMayor = this.datos.obtener(indiceMayorPrioridad);

if (this.comparador.comparar(datoHijoMayor, datoActual) > 0) {
    this.datos.cambiar(indiceActual, datoHijoMayor);
    this.datos.cambiar(indiceMayorPrioridad, datoActual);
    indiceActual = indiceMayorPrioridad;
} else {
    cumpleInvariante = true;
}
```

- Si el **hijo de mayor prioridad** supera al actual: intercambia y sigue bajando por ese camino.
- Si no: el actual ya es mayor o igual que sus hijos, corta.

**¿Por qué se compara con el mayor de los dos hijos?** Porque el que suba a ocupar el lugar tiene que ser mayor que su hermano también. Si subiera el menor, el hermano mayor quedaría debajo de un elemento de menor prioridad y se rompería el invariante.

## `siguiente()`, `tamanio()` y `vacio()`

- `siguiente()`: si está vacía lanza excepción; si no, devuelve `datos.obtener(0)` **sin sacarlo**. Es O(1) porque el de mayor prioridad siempre está en la raíz.
- `tamanio()`: delega en el vector.
- `vacio()`: delega en el vector.

## Ejemplo paso a paso

Supongamos un comparador donde **mayor número = mayor prioridad**.

```java
cp.agregar(5);   // [5]
cp.agregar(3);   // [5, 3]       3 no supera a 5, queda
cp.agregar(8);   // [5, 3, 8] → 8 supera a su padre 5 → [8, 3, 5]
```

```
agregar(8):
      5               8
     / \     →       / \
    3   8           3   5
```

```java
cp.eliminar();
```

1. `datoEliminado = 8`.
2. Se quita el último (5) del vector: queda `[8, 3]`.
3. Se pone el 5 en la raíz: `[5, 3]`.
4. `heapificarHaciaAbajo`: el único hijo es 3, y 3 no supera a 5, así que corta.
5. Devuelve 8. Queda `[5, 3]`.

## Complejidad

|Operación|Costo|
|---|---|
|`siguiente()`, `tamanio()`, `vacio()`|O(1)|
|`agregar`|O(log n) (sube como mucho la altura del árbol)|
|`eliminar`|O(log n) (baja como mucho la altura del árbol)|

El comentario `NOTA` del código dice que el `VectorDinamico` tiene que **duplicar su capacidad** cuando se llena (_factor of two_). Así, agregar al final del vector cuesta O(1) amortizado, y el `agregar` de la cola se mantiene en O(log n). Si el vector creciera de a uno, cada alta copiaría todo y se perdería esa complejidad.

## Comparación con `Cola`

||`Cola`|`ColaPrioridad`|
|---|---|---|
|Estructura|nodos enlazados|heap en un vector|
|Quién sale|el que llegó primero|el de mayor prioridad|
|`agregar`|O(1)|O(log n)|
|`eliminar`|O(1)|O(log n)|
|Necesita comparador|no|sí|

Si querés, hacemos un seguimiento más largo (por ejemplo, agregar 4, 9, 2, 7 y después dos `eliminar`) dibujando el árbol en cada paso, que es la mejor forma de que se entienda cómo suben y bajan los elementos.