# `Cola<T>`: función por función

## La idea general

Una **cola** es una estructura FIFO (_First In, First Out_): el primero que entra es el primero que sale. Es como la fila de una caja: te sumás al final y atienden al que está al principio.

Se implementa con los mismos nodos que `Lista`, y en la práctica es una `Lista` con menos operaciones: solo se agrega al **final** y solo se saca del **principio**.

## Los atributos

```java
private Nodo<T> primero;
private Nodo<T> ultimo;
private int cantidadDatos;
```

- `primero`: el nodo del frente de la cola (el próximo en salir).
- `ultimo`: el nodo del final (donde entra el próximo).
- `cantidadDatos`: cuántos elementos hay.

```
primero → [A] ⇄ [B] ⇄ [C] ← ultimo
 (sale)                      (entra)
```

A diferencia de `Lista`, son `private`: acá no hay iterador que necesite acceder.

## Constructor vacío

```java
this.primero = null;
this.ultimo = null;
this.cantidadDatos = 0;
```

Cola vacía: sin nodos y contador en 0.

## Constructor de copia

Es **idéntico al de `Lista`**:

```java
if (cola == null) {
    throw new ExcepcionLista("La cola a copiar no puede ser nula.");
}
this.primero = null;
this.ultimo = null;
this.cantidadDatos = 0;

Nodo<T> actual = cola.primero;
while (actual != null) {
    agregar(actual.dato);
    actual = actual.siguiente;
}
```

1. Si te pasan `null`, lanza excepción.
2. Deja la cola nueva vacía.
3. `actual` es una **flecha** que arranca en el `primero` de la original.
4. En cada vuelta agrega el dato al final de **tu** cola y avanza la flecha.

Se puede usar `agregar` porque inserta **al final**: recorrés de adelante hacia atrás y vas agregando atrás, así que el orden se mantiene. (En la `Pila` no se podía, porque `agregar` insertaba arriba e invertía el orden.) `this.ultimo` hace de `actualCopia`, y `agregar` suma el contador.

## `agregar(T dato)`

```java
Nodo<T> nuevo = new Nodo<>(dato, this.ultimo, null);
if (vacio()) {
    this.primero = nuevo;
} else {
    this.ultimo.siguiente = nuevo;
}
this.ultimo = nuevo;
this.cantidadDatos++;
```

Es el mismo `agregar` de `Lista`.

1. Crea un nodo con `anterior = ultimo actual` y `siguiente = null` (va a ser el último).
2. Si la cola estaba vacía, el nuevo también es el `primero`.
3. Si no, el último viejo apunta hacia adelante al nuevo (`ultimo.siguiente = nuevo`).
4. `ultimo` pasa a señalar al nuevo.
5. Suma 1 al contador.

```
antes:   primero → [A] ⇄ [B] ← ultimo
agregar(C):
después: primero → [A] ⇄ [B] ⇄ [C] ← ultimo
```

## `eliminar()`

```java
if (vacio()) {
    throw new ExcepcionLista("La cola está vacía.");
}
T datoEliminado = this.primero.dato;
this.primero = this.primero.siguiente;
if (this.primero == null) {
    this.ultimo = null;
} else {
    this.primero.anterior = null;
}
this.cantidadDatos--;
return datoEliminado;
```

Saca el elemento del **frente**.

1. Si está vacía, lanza excepción.
2. Guarda el dato del primero para devolverlo después.
3. `primero` avanza al siguiente nodo.
4. Dos casos:
    - **Si `primero` quedó en `null`**: había un solo elemento y ahora no queda ninguno. Hay que poner también `ultimo = null`; si no, `ultimo` seguiría señalando un nodo eliminado.
    - **Si no**: al nuevo primero se le pone `anterior = null`, porque antes apuntaba hacia atrás al nodo que acaba de salir. Así el nodo viejo queda sin referencias y Java lo libera.
5. Resta 1 al contador y devuelve el dato.

```
antes:   primero → [A] ⇄ [B] ⇄ [C] ← ultimo
eliminar() devuelve A:
después: primero → [B] ⇄ [C] ← ultimo     (B.anterior = null)
```

## `siguiente()`

```java
if (vacio()) {
    throw new ExcepcionLista("La cola está vacía.");
}
return this.primero.dato;
```

Devuelve el dato del frente **sin sacarlo** (_peek_). Es el próximo que saldría con `eliminar()`. Lanza excepción si está vacía.

## `tamanio()`

```java
return this.cantidadDatos;
```

Devuelve el contador, que se mantiene en `agregar` y `eliminar`, así que no hay que recorrer nada (O(1)).

## `vacio()`

```java
return this.primero == null;
```

Está vacía si no hay primer nodo. Como `eliminar` deja `primero` y `ultimo` en `null` cuando saca el último elemento, esta comprobación es confiable.

## Ejemplo

```java
Cola<String> c = new Cola<>();
c.agregar("A");     // A
c.agregar("B");     // A, B
c.siguiente();      // "A" (no lo saca)
c.eliminar();       // devuelve "A" → queda B
c.tamanio();        // 1
c.vacio();          // false
```

## Comparación con `Pila` y `Lista`

||`Pila`|`Cola`|`Lista`|
|---|---|---|---|
|Orden|LIFO|FIFO|acceso por índice|
|Punteros|solo `ultimo`|`primero` y `ultimo`|`primero` y `ultimo`|
|Enlaces usados|solo `siguiente`|`anterior` y `siguiente`|`anterior` y `siguiente`|
|`agregar`|arriba (tope)|al final|al final o por índice|
|`eliminar`|del tope|del frente|por índice|
|`vacio()`|`ultimo == null`|`primero == null`|`cantidadDatos == 0`|

## Un detalle

La cola usa el enlace `anterior`, pero en realidad **no lo necesita**: solo se recorre hacia adelante (`primero` → `siguiente`). Podría funcionar con nodos simplemente enlazados. Se mantiene `anterior` porque `Nodo` ya lo trae y porque `eliminar` lo deja prolijo (`primero.anterior = null`). Es una decisión de reutilizar `Nodo`, no una necesidad de la estructura.

Si querés, hacemos un seguimiento completo con `agregar` y `eliminar` en secuencia, dibujando `primero` y `ultimo` en cada paso, en especial el caso del último elemento.