
# `IteradorLista<T>`: función por función

## La idea general

Un iterador es un **marcador** que se para sobre un elemento de la lista y puede moverse hacia adelante o atrás. A diferencia del cursor `actual` de tu apunte, que vive dentro de la lista, acá cada iterador es un **objeto aparte** con su propia posición. Podés tener varios sobre la misma lista sin que se pisen.

Es `class` sin `public` (package-private), porque nadie de afuera la usa directamente: la lista la entrega con `iterador()` como un `Iterador<T>`.

## Los atributos

```java
private Lista<T> lista;
private Nodo<T> cursor;
private int indice;
```

- `lista`: la lista que se está recorriendo.
- `cursor`: una **flecha** al nodo donde está parado el iterador.
- `indice`: el número de posición de ese nodo (0, 1, 2...).

La regla que se cumple siempre (invariante) es:

> `cursor` señala el nodo en la posición `indice`. Si `indice == cantidadDatos`, el iterador está "después del último" y `cursor` es `null`.

```
lista:  [A] ⇄ [B] ⇄ [C]      null (después del último)
indice:  0     1     2          3
```

Las dos variables (`cursor` e `indice`) deben ir siempre sincronizadas. Casi todo el código sirve para mantener eso.

## Constructor 1

```java
IteradorLista(Lista<T> lista) {
    this(lista, 0);
}
```

Llama al otro constructor con índice 0: arranca en el primer elemento.

## Constructor 2

```java
this.lista = lista;
this.indice = indice;
```

Guarda la lista y la posición inicial.

```java
if (indice == lista.cantidadDatos) {
    this.cursor = null;
} else {
    this.cursor = lista.primero;
    for (int i = 0; i < indice; i++) {
        this.cursor = this.cursor.siguiente;
    }
}
```

- Si el índice es igual al tamaño, no hay nodo ahí: el cursor queda en `null` ("después del último"). Esto también cubre la lista vacía: con `indice = 0` y `cantidadDatos = 0` queda en `null`.
- Si no, el cursor arranca en `primero` y avanza `indice` veces con el `for` hasta llegar al nodo correcto. Es la misma idea que `dato(indice)` de `Lista`.

Acá `lista.cantidadDatos` y `lista.primero` se pueden leer directo porque son package-private.

## `dato()`

```java
return this.cursor.dato;
```

Devuelve el contenido del nodo donde está parado. **No mueve nada.** Si el cursor es `null` (después del último), da `NullPointerException`.

## `haySiguiente()`

```java
return this.cursor != null;
```

Devuelve `true` mientras el cursor señale un nodo. Ojo con el nombre: en realidad significa "¿estoy parado sobre un elemento válido?". Cuando el cursor pasa el último y queda en `null`, da `false`.

## `siguiente()`

```java
this.cursor = this.cursor.siguiente;
this.indice++;
```

Avanza un casillero: la flecha pasa al nodo siguiente y el índice sube 1. Es `void`: **no devuelve el dato**. Para leerlo hay que llamar a `dato()` antes de avanzar. Si ya está en `null`, da `NullPointerException`.

Por eso el recorrido típico es:

```java
Iterador<String> it = lista.iterador();
while (it.haySiguiente()) {
    System.out.println(it.dato());  // leo
    it.siguiente();                 // avanzo
}
```

Es distinto de tu apunte, donde `obtenerSiguiente()` devolvía el dato y avanzaba en un solo paso.

## `hayAnterior()`

```java
return this.indice > 0;
```

Hay un elemento antes del actual si el índice es mayor que 0. Acá se usa `indice` y no `cursor`, porque el cursor puede ser `null` aunque haya elementos atrás.

## `anterior()`

```java
if (this.cursor == null) {
    this.cursor = this.lista.ultimo;
} else {
    this.cursor = this.cursor.anterior;
}
this.indice--;
```

Retrocede un casillero. Hay dos casos:

- **Cursor en `null`** (después del último): no hay nodo del cual tomar `.anterior`, así que se salta al `ultimo` de la lista.
- **Cursor en un nodo**: se usa su enlace `anterior`.

En los dos casos baja el índice. Es la parte que **necesita lista doblemente enlazada**.

```
antes:   [A] ⇄ [B] ⇄ [C]      null      (indice = 3)
                                ↑
                              cursor
después: [A] ⇄ [B] ⇄ [C]      (indice = 2)
                       ↑
                    cursor
```

## `agregar(T dato)`

```java
this.lista.agregar(dato, this.indice);
this.indice++;
```

Inserta el dato **en la posición actual**, o sea justo **antes** del elemento donde está parado el iterador. Delega el trabajo en `Lista.agregar(dato, indice)`.

Después hace `indice++`. ¿Por qué? Porque al insertar en la posición `indice`, el nodo del cursor se corrió una posición a la derecha. El cursor **sigue señalando el mismo nodo**, pero su número de posición ahora es uno más. Si no se sumara, `cursor` e `indice` quedarían desincronizados.

```
antes:    [A] ⇄ [C]       cursor en C, indice = 1
agregar(B):
después:  [A] ⇄ [B] ⇄ [C] cursor en C, indice = 2
```

Si el cursor estaba en `null` (indice == cantidad), agrega al final, el índice sube y sigue valiendo `indice == cantidadDatos`, así que el cursor `null` sigue siendo correcto.

## `modificarDato(T dato)`

```java
this.cursor.dato = dato;
```

Cambia el contenido del nodo actual. No toca enlaces, ni el índice. Da `NullPointerException` si el cursor es `null`.

## `eliminar()`

```java
Nodo<T> siguienteNodo = this.cursor.siguiente;
T datoEliminado = this.lista.eliminar(this.indice);
this.cursor = siguienteNodo;
return datoEliminado;
```

Línea por línea:

1. **Guarda** el nodo que viene después del actual. Hay que hacerlo **antes** de eliminar, porque después ya no se podría llegar a él de forma segura desde el nodo eliminado.
2. **Elimina** el nodo en la posición `indice` llamando a `Lista.eliminar(indice)`, que ya arregla los enlaces y el contador, y devuelve el dato borrado.
3. **Mueve el cursor** al nodo guardado.
4. Devuelve el dato eliminado.

El `indice` **no se modifica**, y está bien: al sacar el elemento de la posición 1, el que estaba en la 2 pasa a ser el de la 1.

```
antes:    [A] ⇄ [B] ⇄ [C]      cursor en B, indice = 1
eliminar():
después:  [A] ⇄ [C]            cursor en C, indice = 1
```

Si se elimina el último, `siguienteNodo` es `null`, y `indice` pasa a ser igual a `cantidadDatos`, lo cual es consistente con cursor `null`.

## Resumen en una tabla

|Método|Mueve cursor|Cambia `indice`|Toca la lista|
|---|---|---|---|
|`dato()`|no|no|no|
|`haySiguiente()`|no|no|no|
|`siguiente()`|adelante|`+1`|no|
|`hayAnterior()`|no|no|no|
|`anterior()`|atrás|`-1`|no|
|`agregar(dato)`|no (el nodo sigue igual)|`+1`|sí|
|`modificarDato(dato)`|no|no|cambia un dato|
|`eliminar()`|al siguiente nodo|no|sí|

## Un detalle a tener en cuenta

El iterador asume que **solo él** modifica la lista mientras lo usás. Si agregás o eliminás directo con `lista.agregar(...)` mientras tenés un iterador creado, `cursor` e `indice` pueden quedar desincronizados, porque el iterador no se entera del cambio.

Si querés, hacemos un ejemplo completo con una lista de 3 elementos, llamando a `siguiente`, `agregar` y `eliminar` en secuencia, dibujando `cursor` e `indice` en cada paso.