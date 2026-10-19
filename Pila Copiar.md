
# Paso a paso, línea por línea

Uso la pila `[C, B, A]` (C arriba). Recordá: `actualOriginal` y `actualCopia` son **flechas** que señalan nodos, no son nodos.

Al empezar:

```
original:  [C] → [B] → [A] → null
copia:     (vacía)
```

## Antes del while

**Línea 1**

```java
Nodo<T> actualOriginal = pila.ultimo;
```

Creás la flecha `actualOriginal` y la hacés señalar al tope de la original (C).

```
original:  [C] → [B] → [A] → null
            ↑
      actualOriginal
```

**Línea 2**

```java
this.ultimo = new Nodo<>(actualOriginal.dato);
```

Se crea un nodo **nuevo** con el dato de C (lo llamo C') y `this.ultimo` pasa a señalarlo. Es el tope de tu pila.

```
copia:  [C'] → null
          ↑
     this.ultimo
```

**Línea 3**

```java
Nodo<T> actualCopia = this.ultimo;
```

Creás la flecha `actualCopia` y la hacés señalar al mismo nodo que `this.ultimo` (C').

```
copia:  [C'] → null
          ↑
  this.ultimo y actualCopia
```

**Línea 4**

```java
actualOriginal = actualOriginal.siguiente;
```

La flecha `actualOriginal` avanza de C a B. Ya no hay que copiar C porque ya está copiado.

```
original:  [C] → [B] → [A] → null
                  ↑
            actualOriginal
```

## El while

Condición: `actualOriginal != null`. Mientras la flecha señale un nodo, queda algo por copiar.

### Vuelta 1 (`actualOriginal` en B)

**a)** `Nodo<T> nuevo = new Nodo<>(actualOriginal.dato);`  
Se crea B' con el dato de B. Todavía está suelto, nadie lo enlaza.

**b)** `actualCopia.siguiente = nuevo;`  
`actualCopia` señala C', así que C'.siguiente pasa a apuntar a B'. Acá sí se modifica un nodo.

**c)** `actualCopia = nuevo;`  
La flecha `actualCopia` se mueve a B' (ahora es el final de la copia).

**d)** `actualOriginal = actualOriginal.siguiente;`  
La flecha de la original avanza de B a A.

```
original:  [C] → [B] → [A] → null
                         ↑
                   actualOriginal

copia:     [C'] → [B'] → null
                    ↑
               actualCopia
```

### Vuelta 2 (`actualOriginal` en A)

**a)** Se crea A' con el dato de A.  
**b)** B'.siguiente apunta a A'.  
**c)** `actualCopia` se mueve a A'.  
**d)** `actualOriginal` avanza de A a `null`.

```
original:  [C] → [B] → [A] → null
                               ↑
                         actualOriginal (null)

copia:     [C'] → [B'] → [A'] → null
                           ↑
                      actualCopia
```

### Fin

Ahora `actualOriginal == null`, la condición da falso y el while termina.

## Después del while

```java
this.cantidadDatos = pila.cantidadDatos;
```

Se copia el contador: la copia tiene 3 elementos, igual que la original.

## Resultado final

```
original:  ultimo → [C] → [B] → [A] → null
copia:     ultimo → [C'] → [B'] → [A'] → null
```

Dos cadenas separadas, mismo orden, mismos datos.

## Lo que se repite en cada vuelta

|Línea|Qué hace|¿Modifica un nodo o mueve una flecha?|
|---|---|---|
|`nuevo = new Nodo<>(...)`|crea el nodo copia|crea un nodo|
|`actualCopia.siguiente = nuevo`|engancha el nodo al final de la copia|**modifica un nodo**|
|`actualCopia = nuevo`|el final de la copia ahora es `nuevo`|mueve una flecha|
|`actualOriginal = actualOriginal.siguiente`|pasa al próximo de la original|mueve una flecha|

Si querés, hacé el mismo seguimiento a mano con una pila de 2 elementos y me decís en qué paso te trabás.





# Resumen: constructor de copia de `Pila`

## Por qué se hace así

- Una variable de tipo `Nodo` guarda una **referencia** (dirección), no el nodo en sí.
- Si hiciera `this.ultimo = pila.ultimo`, las dos pilas compartirían los **mismos nodos**. El objetivo de una copia es que sean **independientes**, así que hay que crear **nodos nuevos**.
- Se copia solo el **dato** de cada nodo (copia superficial: si `T` es un objeto modificable, ambas pilas apuntan al mismo objeto).

## Las dos flechas

|Variable|Pila|Rol|
|---|---|---|
|`actualOriginal`|original|**leer**: señala el próximo nodo a copiar|
|`actualCopia`|copia|**escribir**: señala el final de la copia, para colgar el nodo siguiente|

`this.ultimo` no se mueve: tiene que seguir señalando el tope de la copia.

## Cómo pasan las direcciones y el contenido

|Código|Qué pasa|
|---|---|
|`actualOriginal = pila.ultimo`|se copia una **dirección**: la flecha señala el tope de la original|
|`new Nodo<>(actualOriginal.dato)`|se copia el **contenido** (el dato) a un nodo **nuevo**|
|`this.ultimo = nodoNuevo`|se guarda la **dirección** del nodo nuevo|
|`actualCopia = this.ultimo`|se copia una **dirección**: las dos flechas señalan el mismo nodo|
|`x = x.siguiente`|**mueve la flecha** `x`, no modifica ningún nodo|
|`x.siguiente = nuevo`|**modifica un nodo**: cambia a dónde apunta su enlace|

## Pasos

1. `actualOriginal` señala el tope de la original.
2. Se crea un nodo nuevo con ese dato → es `this.ultimo`.
3. `actualCopia` señala ese nodo nuevo.
4. `actualOriginal` avanza al siguiente.
5. **While** (`actualOriginal != null`), en cada vuelta:
    - crear `nuevo` con el dato de `actualOriginal`
    - `actualCopia.siguiente = nuevo` (enganchar al final)
    - `actualCopia = nuevo` (mover la flecha de la copia)
    - `actualOriginal = actualOriginal.siguiente` (mover la flecha de la original)
6. `this.cantidadDatos = pila.cantidadDatos`.

## Resultado

```
original:  ultimo → [C]  → [B]  → [A]  → null
copia:     ultimo → [C'] → [B'] → [A'] → null
```

Mismo orden, mismos datos, nodos distintos.

## Diferencia clave con `agregar`

- `agregar` inserta **arriba** (invierte el orden si lo usás recorriendo de arriba a abajo).
- El constructor de copia engancha **al final** de la cadena, por eso mantiene el orden.

## Regla para recordar

> `x = y.siguiente` → muevo mi flecha.  
> `x.siguiente = y` → cambio un enlace del nodo.