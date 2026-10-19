# `Pila<T>`: función por función, línea por línea

## La idea general

Una pila es **LIFO** (_Last In, First Out_): el último que entra es el primero que sale. Se arma con nodos enlazados, donde cada nodo apunta con `siguiente` al que está **debajo** de él:

```
ultimo → [C] → [B] → [A] → null
         tope         fondo
```

## Los atributos

```java
private Nodo<T> ultimo;
private int cantidadDatos;
```

- `ultimo`: flecha al nodo que está **arriba de todo** (el tope). Es la única puerta de entrada a la pila.
- `cantidadDatos`: cuántos elementos hay. Se mantiene al día en cada `agregar` y `eliminar`.

Los dos son `private`: nadie de afuera los toca.

## Constructor vacío

```java
public Pila() {
    this.ultimo = null;
    this.cantidadDatos = 0;
}
```

- `this.ultimo = null;`: no hay ningún nodo, así que el tope no señala nada.
- `this.cantidadDatos = 0;`: hay 0 elementos.

## Constructor de copia

Crea una pila nueva con **nodos propios** pero los mismos datos y el mismo orden.

```java
if (pila == null) {
    throw new ExcepcionLista("La pila a copiar no puede ser nula.");
}
```

Si te pasan `null` no hay nada que copiar, así que lanza una excepción.

```java
if (pila.vacio()) {
    this.ultimo = null;
    this.cantidadDatos = 0;
}
```

Si la original está vacía, la copia también. No hay nada que recorrer.

```java
} else {
    Nodo<T> actualOriginal = pila.ultimo;
```

Se crea la flecha `actualOriginal` y apunta al tope de la original. Esta flecha **lee** de la original.

```java
    this.ultimo = new Nodo<>(actualOriginal.dato);
```

Se crea un nodo **nuevo** con el dato del tope original y se lo asigna como tope de la copia. Es otro objeto en memoria, no el mismo nodo.

```java
    Nodo<T> actualCopia = this.ultimo;
```

Se crea la flecha `actualCopia`, que señala el último nodo construido de la copia. Esta flecha **escribe** en la copia. Por ahora coincide con `this.ultimo`.

```java
    actualOriginal = actualOriginal.siguiente;
```

La flecha de la original avanza un casillero. El tope ya está copiado, así que sigue el nodo de abajo.

```java
    while (actualOriginal != null) {
```

Mientras la flecha señale un nodo, queda algo por copiar.

```java
        Nodo<T> nuevo = new Nodo<>(actualOriginal.dato);
```

Crea el nodo copia del nodo actual de la original. Por ahora está suelto.

```java
        actualCopia.siguiente = nuevo;
```

Engancha el nodo nuevo **debajo** del último nodo de la copia. Acá **se modifica un nodo** (cambia un enlace).

```java
        actualCopia = nuevo;
```

Mueve la flecha `actualCopia` al nodo recién agregado, que ahora es el final de la copia.

```java
        actualOriginal = actualOriginal.siguiente;
    }
```

Avanza la flecha de la original. Cuando pasa el fondo vale `null` y el `while` termina.

```java
    this.cantidadDatos = pila.cantidadDatos;
}
```

La copia tiene la misma cantidad de elementos.

Resultado con `[C, B, A]`:

```
original:  ultimo → [C]  → [B]  → [A]  → null
copia:     ultimo → [C'] → [B'] → [A'] → null
```

Por qué no se usa `agregar` acá: `agregar` inserta **arriba**, así que recorriendo de arriba a abajo la copia quedaría invertida. Por eso se engancha al final a mano.

Regla para no confundirte: `x = y.siguiente` mueve tu flecha, mientras que `x.siguiente = y` cambia un enlace de un nodo.

## `agregar(T dato)` (apilar / push)

```java
Nodo<T> nuevo = new Nodo<>(dato, null, this.ultimo);
```

Crea el nodo con `anterior = null` y `siguiente = this.ultimo`. El nuevo apunta hacia abajo al tope actual. (`anterior` no se usa en la pila, queda siempre en `null`.)

```java
this.ultimo = nuevo;
```

El tope pasa a ser el nodo nuevo.

```java
this.cantidadDatos++;
```

Suma 1 al contador.

```
antes:    ultimo → [B] → [A]
agregar(C):
paso 1:   nuevo = [C] → [B] → [A]      (C apunta al tope viejo)
paso 2:   ultimo → [C] → [B] → [A]     (el tope ahora es C)
```

El orden importa: primero el nuevo se engancha al tope viejo, y recién después se mueve `ultimo`. Si movieras `ultimo` primero, perderías el resto de la pila.

Funciona también con la pila vacía: `this.ultimo` es `null`, entonces el nuevo queda con `siguiente = null`. (El Javadoc dice "al final", pero en realidad agrega arriba, en el tope.)

## `eliminar()` (desapilar / pop)

```java
if (vacio()) {
    throw new ExcepcionLista("La pila está vacía.");
}
```

No se puede sacar de una pila vacía, así que lanza una excepción.

```java
T datoEliminado = this.ultimo.dato;
```

Guarda el dato del tope para devolverlo al final.

```java
this.ultimo = this.ultimo.siguiente;
```

El tope pasa al nodo de abajo. El nodo viejo queda sin ninguna referencia y Java lo libera solo (_garbage collector_). Si había un solo elemento, `siguiente` es `null` y la pila queda vacía.

```java
this.cantidadDatos--;
return datoEliminado;
```

Resta 1 al contador y devuelve el dato guardado.

```
antes:    ultimo → [C] → [B] → [A]
eliminar() devuelve C:
después:  ultimo → [B] → [A]
```

## `siguiente()` (mirar / peek)

```java
if (vacio()) {
    throw new ExcepcionLista("La pila está vacía.");
}
return this.ultimo.dato;
```

Si está vacía, lanza una excepción. Si no, devuelve el dato del tope **sin sacarlo**: no cambia ningún enlace ni el contador. Es el próximo que saldría con `eliminar()`.

## `tamanio()`

```java
return this.cantidadDatos;
```

Devuelve el contador. No hay que recorrer la pila, así que es O(1).

## `vacio()`

```java
return this.ultimo == null;
```

La pila está vacía si no hay tope. Es confiable porque `eliminar` deja `ultimo` en `null` cuando saca el último elemento.

## Ejemplo completo

```java
Pila<String> p = new Pila<>();
p.agregar("A");     // A
p.agregar("B");     // B, A   (B arriba)
p.agregar("C");     // C, B, A
p.siguiente();      // "C" (no lo saca)
p.eliminar();       // devuelve "C" → B, A
p.tamanio();        // 2
p.vacio();          // false
```

## Resumen para el anotador

|Método|Qué hace|Costo|
|---|---|---|
|`Pila()`|pila vacía|O(1)|
|`Pila(pila)`|copia con nodos nuevos, mismo orden|O(n)|
|`agregar`|nuevo nodo arriba, apunta al tope viejo|O(1)|
|`eliminar`|baja el tope un nodo y devuelve el dato|O(1)|
|`siguiente`|devuelve el tope sin sacarlo|O(1)|
|`tamanio`|devuelve el contador|O(1)|
|`vacio`|`ultimo == null`|O(1)|

Si querés, hacemos un seguimiento de `agregar` y `eliminar` en secuencia dibujando `ultimo` en cada paso.