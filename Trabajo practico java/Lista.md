# `Lista<T>`: función por función, línea por línea

## La idea general

Es una lista **doblemente enlazada**: cada nodo tiene `anterior` y `siguiente`, y la lista guarda los dos extremos.

```
primero → [A] ⇄ [B] ⇄ [C] ← ultimo
 null ← A.anterior          C.siguiente → null
```

Los índices van de 0 a `cantidadDatos - 1`, como en un array.

## Los atributos

```java
Nodo<T> primero;
Nodo<T> ultimo;
int cantidadDatos;
```

- `primero`: flecha al nodo del inicio.
- `ultimo`: flecha al nodo del final.
- `cantidadDatos`: cuántos elementos hay.

Son **package-private** (sin `private`) porque `IteradorLista` los lee directamente.

## Constructor vacío

```java
this.primero = null;
this.ultimo = null;
this.cantidadDatos = 0;
```

Sin nodos y con contador en 0.

## Constructor de copia

```java
if (lista == null) {
    throw new ExcepcionLista("La lista a copiar no puede ser nula.");
}
```

Si te pasan `null`, no hay nada que copiar y lanza una excepción.

```java
this.primero = null;
this.ultimo = null;
this.cantidadDatos = 0;
```

Tu lista arranca vacía. Es necesario porque `agregar` se apoya en ese estado.

```java
Nodo<T> actual = lista.primero;
```

`actual` es una flecha que **lee** de la original. Arranca en su primer nodo.

```java
while (actual != null) {
    agregar(actual.dato);
    actual = actual.siguiente;
}
```

Mientras la flecha señale un nodo:

1. `agregar(actual.dato)` crea un nodo **nuevo** en tu lista, al final, con ese dato.
2. `actual = actual.siguiente` mueve la flecha al próximo nodo de la original.

Se puede usar `agregar` porque inserta **al final** y el orden se mantiene. `this.ultimo` hace el trabajo de `actualCopia` de la pila, y `agregar` va sumando el contador.

## `agregar(T dato)`: agrega al final

```java
Nodo<T> nuevo = new Nodo<>(dato, this.ultimo, null);
```

Crea el nodo con `anterior = ultimo actual` y `siguiente = null`, porque va a ser el último.

```java
if (vacio()) {
    this.primero = nuevo;
} else {
    this.ultimo.siguiente = nuevo;
}
```

- Si la lista estaba vacía, el nuevo es también el `primero`.
- Si no, el último viejo apunta hacia adelante al nuevo.

```java
this.ultimo = nuevo;
this.cantidadDatos++;
```

El nuevo pasa a ser `ultimo`, y se suma 1 al contador.

```
antes:    primero → [A] ⇄ [B] ← ultimo
agregar(C):
después:  primero → [A] ⇄ [B] ⇄ [C] ← ultimo
```

Importante: se usa `vacio()` **antes** de mover `ultimo`. Si lo movieras primero, `this.ultimo.siguiente` fallaría con la lista vacía.

## `agregar(T dato, int indice)`: inserta en una posición

```java
if (indice < 0 || indice > this.cantidadDatos) {
    throw new ExcepcionLista("El índice no es válido.");
}
```

El índice puede ir de 0 a `cantidadDatos` inclusive. El último valor significa "al final".

### Caso 1: al final

```java
if (indice == this.cantidadDatos) {
    agregar(dato);
}
```

Reutiliza el `agregar` de arriba. Este caso también cubre la lista vacía con índice 0.

### Caso 2: al principio

```java
} else if (indice == 0) {
    Nodo<T> nuevo = new Nodo<>(dato, null, this.primero);
    this.primero.anterior = nuevo;
    this.primero = nuevo;
    this.cantidadDatos++;
}
```

1. El nuevo tiene `anterior = null` y `siguiente = primero viejo`.
2. El primero viejo apunta hacia atrás al nuevo.
3. `primero` pasa a ser el nuevo.
4. Suma 1.

```
antes:    primero → [A] ⇄ [B]
después:  primero → [X] ⇄ [A] ⇄ [B]
```

Acá `this.primero` nunca es `null`, porque la lista vacía ya la atrapó el caso 1.

### Caso 3: en el medio

```java
} else {
    Nodo<T> actual = this.primero;
    for (int i = 0; i < indice; i++) {
        actual = actual.siguiente;
    }
```

Recorre `indice` veces desde `primero`. `actual` queda en el nodo que **hoy ocupa** esa posición, y el nuevo se va a meter justo antes.

```java
    Nodo<T> nuevo = new Nodo<>(dato, actual.anterior, actual);
    actual.anterior.siguiente = nuevo;
    actual.anterior = nuevo;
    this.cantidadDatos++;
}
```

1. El nuevo apunta atrás al vecino izquierdo (`actual.anterior`) y adelante a `actual`.
2. El vecino izquierdo apunta adelante al nuevo.
3. `actual` apunta atrás al nuevo.

```
antes:    [X] ⇄ [actual]
después:  [X] ⇄ [nuevo] ⇄ [actual]
```

El orden importa: `actual.anterior.siguiente = nuevo` va **antes** de `actual.anterior = nuevo`. Si cambiaras `actual.anterior` primero, perderías la referencia a `X`.

## `eliminar()`: elimina el último

```java
if (vacio()) {
    throw new ExcepcionLista("La lista está vacía.");
}
return eliminar(this.cantidadDatos - 1);
```

Si está vacía, excepción. Si no, delega en `eliminar(indice)` con el índice del último.

## `eliminar(int indice)`: elimina por posición

```java
if (indice < 0 || indice >= this.cantidadDatos) {
    throw new ExcepcionLista("El índice no es válido.");
}
T datoEliminado;
```

Valida que el índice exista (de 0 a `cantidadDatos - 1`) y declara la variable donde se guarda el dato a devolver.

### Caso 1: un solo elemento

```java
if (this.cantidadDatos == 1) {
    datoEliminado = this.primero.dato;
    this.primero = null;
    this.ultimo = null;
}
```

Guarda el dato y deja la lista vacía. Hay que anular **los dos** extremos.

### Caso 2: el primero

```java
} else if (indice == 0) {
    datoEliminado = this.primero.dato;
    this.primero = this.primero.siguiente;
    this.primero.anterior = null;
}
```

`primero` avanza al siguiente, y a ese nuevo primero se le corta el enlace hacia atrás (apuntaba al nodo que sale).

### Caso 3: el último

```java
} else if (indice == this.cantidadDatos - 1) {
    datoEliminado = this.ultimo.dato;
    this.ultimo = this.ultimo.anterior;
    this.ultimo.siguiente = null;
}
```

`ultimo` retrocede, y al nuevo último se le corta el enlace hacia adelante.

### Caso 4: en el medio

```java
} else {
    Nodo<T> actual = this.primero;
    for (int i = 0; i < indice; i++) {
        actual = actual.siguiente;
    }
    datoEliminado = actual.dato;
    actual.anterior.siguiente = actual.siguiente;
    actual.siguiente.anterior = actual.anterior;
}
```

Busca el nodo, guarda su dato y lo **saltea** desde los dos lados:

```
antes:    [X] ⇄ [actual] ⇄ [Y]
después:  [X] ⇄ [Y]        (actual queda sin referencias)
```

### Final, común a todos los casos

```java
this.cantidadDatos--;
return datoEliminado;
```

Resta 1 y devuelve el dato.

## `dato(int indice)`: consulta

```java
if (indice < 0 || indice >= this.cantidadDatos) {
    throw new ExcepcionLista("El índice no es válido.");
}
Nodo<T> actual = this.primero;
for (int i = 0; i < indice; i++) {
    actual = actual.siguiente;
}
return actual.dato;
```

Valida el índice, recorre desde `primero` avanzando `indice` veces y devuelve el contenido del nodo. No modifica nada.

## `modificarDato(T dato, int indice)`

```java
if (indice < 0 || indice >= this.cantidadDatos) {
    throw new ExcepcionLista("El índice no es válido.");
}
Nodo<T> actual = this.primero;
for (int i = 0; i < indice; i++) {
    actual = actual.siguiente;
}
actual.dato = dato;
```

Igual que `dato`, pero en vez de devolver el contenido, lo **reemplaza**. No toca ningún enlace.

## `tamanio()` y `vacio()`

```java
return this.cantidadDatos;       // tamanio
return this.cantidadDatos == 0;  // vacio
```

Los dos usan el contador, así que son O(1). (En la pila, `vacio` miraba `ultimo == null`.)

## `iterador()` y `iterador(int indice)`

```java
return new IteradorLista<>(this);
```

Crea un iterador posicionado en el primer dato. Le pasa `this`, o sea la lista misma.

```java
if (indice < 0 || indice > this.cantidadDatos) {
    throw new ExcepcionLista("El índice no es válido.");
}
return new IteradorLista<>(this, indice);
```

Valida el índice (acá se permite `== cantidadDatos`, que es "después del último") y crea el iterador en esa posición.

## Ejemplo completo

```java
Lista<String> l = new Lista<>();
l.agregar("A");            // A
l.agregar("C");            // A ⇄ C
l.agregar("B", 1);         // A ⇄ B ⇄ C
l.dato(1);                 // "B"
l.modificarDato("X", 1);   // A ⇄ X ⇄ C
l.eliminar(0);             // devuelve "A" → X ⇄ C
l.eliminar();              // devuelve "C" → X
l.tamanio();               // 1
```

## Resumen para el anotador

|Método|Qué hace|Costo|
|---|---|---|
|`Lista()`|lista vacía|O(1)|
|`Lista(lista)`|copia con nodos nuevos, mismo orden|O(n)|
|`agregar(dato)`|nuevo nodo al final|O(1)|
|`agregar(dato, i)`|inserta en la posición `i`|O(1) en los extremos, O(n) en el medio|
|`eliminar()`|saca el último|O(1)|
|`eliminar(i)`|saca por posición|O(1) en los extremos, O(n) en el medio|
|`dato(i)` / `modificarDato`|leer / cambiar por posición|O(n)|
|`tamanio` / `vacio`|contador|O(1)|
|`iterador`|crea un iterador|O(1), o O(n) si se le da un índice|

Regla para no confundirte: `x = y.siguiente` mueve tu flecha, mientras que `x.siguiente = y` cambia un enlace de un nodo. Al insertar o eliminar en el medio, siempre hay que ajustar **dos enlaces de cada vecino**, uno en cada sentido.

Si querés, hacemos un seguimiento del caso "en el medio" de `agregar` y `eliminar` dibujando los cuatro enlaces paso a paso.






# Cómo se declara y por qué `this`

## La declaración

```java
public Iterador<T> iterador() {
    return new IteradorLista<>(this);
}
```

Se lee de izquierda a derecha:

|Parte|Significado|
|---|---|
|`public`|cualquiera puede llamarlo|
|`Iterador<T>`|**lo que devuelve**: un iterador de elementos de tipo `T`|
|`iterador`|el nombre del método (lo elegís vos, podría llamarse `crearIterador`, pero las pruebas esperan `iterador`)|
|`()`|no recibe parámetros|
|`return new IteradorLista<>(this);`|crea el objeto y lo devuelve|

La segunda versión es igual, pero recibe `int indice`. Es una **sobrecarga**: mismo nombre, distintos parámetros.

## Qué es `this`

`this` **no es un nombre que elegís**. Es una palabra reservada de Java que significa "el objeto sobre el que se llamó a este método". Por ejemplo:

```java
Lista<String> miLista = new Lista<>();
Iterador<String> it = miLista.iterador();
```

Cuando se ejecuta `miLista.iterador()`, adentro del método `this` es `miLista`. Si tuvieras otra lista `otra` y llamaras `otra.iterador()`, ahí `this` sería `otra`.

## Por qué se lo pasa al iterador

El constructor de `IteradorLista` pide una lista:

```java
IteradorLista(Lista<T> lista) { ... }
```

El iterador necesita saber **qué lista recorrer** para llegar a `lista.primero`, `lista.ultimo` y `lista.cantidadDatos`. Con `this` le pasás justo la lista que lo creó.

## ¿Se puede pasar otra cosa?

El tipo tiene que ser `Lista<T>`, porque es lo que declara el constructor. Compilar compilaría con otra lista, pero sería un error de lógica:

```java
public Iterador<T> iterador() {
    return new IteradorLista<>(otraLista);   // recorrería OTRA lista, no esta
}
```

`miLista.iterador()` te devolvería un iterador de otra lista, y eso rompe lo que el método promete. Lo correcto es `this`.

Tampoco hay un "nombre" que poner en su lugar: `this` no es una variable que declarás, es el propio objeto. Podrías pasarlo antes en una variable local, pero no aporta nada:

```java
Lista<T> estaLista = this;
return new IteradorLista<>(estaLista);   // equivalente, pero innecesario
```

## Resumen para el anotador

> `iterador()` crea un `IteradorLista` y le entrega `this`, o sea **la propia lista sobre la que se llamó**, para que el iterador sepa qué recorrer.  
> `this` es una palabra reservada, no se renombra ni se reemplaza por otra cosa.