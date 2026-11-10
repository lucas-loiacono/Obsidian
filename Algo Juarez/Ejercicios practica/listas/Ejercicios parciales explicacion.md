
Esta es la guía definitiva de operaciones posicionales para listas simples y dobles, con todos los casos especiales contemplados y listos para usar en tus exámenes o proyectos.

**Alta con Un Enlace (Lista Simple)** La regla de oro es "nunca soltar la mano antes de agarrar la nueva". Como los nodos solo miran hacia adelante, el caso general exige pararse en el nodo anterior. Si la posición es 0, no hay nodo anterior, por lo que se modifica directamente el puntero `primero`.


```Java
public void altaUnEnlace(T dato, int pos) {
    Nodo<T> nuevo = new Nodo<>(dato);

    // Caso Especial: Insertar al principio (o en lista vacía)
    if (pos == 0) {
        nuevo.siguiente = this.primero;
        this.primero = nuevo;
    } 
    // Caso General: Insertar en el medio o al final
    else {
        Nodo<T> anterior = this.obtenerNodo(pos - 1);
        Nodo<T> siguiente = anterior.siguiente;
        
        nuevo.siguiente = siguiente;  // El nuevo se agarra a la cadena
        anterior.siguiente = nuevo;   // El anterior suelta y agarra al nuevo
    }
    
    // Si tu clase usa puntero 'ultimo', acá validarías:
    // if (nuevo.siguiente == null) this.ultimo = nuevo;
    
    this.cantidadDatos++;
}
```

**Baja con Un Enlace (Lista Simple)** Para eliminar, el concepto es "puentear" al nodo que queremos borrar, haciendo que su anterior apunte directamente a su siguiente. Nuevamente, borrar en la posición 0 es el caso especial porque carece de nodo anterior.


```Java
public T bajaUnEnlace(int pos) {
    // Validación de seguridad
    if (this.primero == null || pos < 0 || pos >= this.cantidadDatos) {
        return null; 
    }

    T datoEliminado;

    // Caso Especial: Borrar el primero
    if (pos == 0) {
        datoEliminado = this.primero.dato;
        this.primero = this.primero.siguiente;
    } 
    // Caso General: Borrar en el medio o el último
    else {
        Nodo<T> anterior = this.obtenerNodo(pos - 1);
        Nodo<T> nodoEliminar = anterior.siguiente;
        
        datoEliminado = nodoEliminar.dato;
        anterior.siguiente = nodoEliminar.siguiente; // Se puentea el nodo
    }
    
    // Si tu clase usa puntero 'ultimo', acá validarías si borraste el final:
    // if (anterior != null && anterior.siguiente == null) this.ultimo = anterior;
    
    this.cantidadDatos--;
    return datoEliminado;
}
```

**Alta con Dos Enlaces (Lista Doblemente Enlazada)** Al tener puntero `.anterior`, debes gestionar cuatro conexiones (las dos manos del nuevo nodo, la del anterior y la del siguiente). El peligro aquí son los extremos: debes asegurarte de que el nodo al que le vas a pedir la mano no sea `null`.


```Java
public void altaDosEnlaces(T dato, int pos) {
    Nodo<T> nuevo = new Nodo<>(dato);

    // Caso Especial: Insertar al principio (o en lista vacía)
    if (pos == 0) {
        nuevo.siguiente = this.primero;
        
        if (this.primero != null) { // Evita NullPointerException si estaba vacía
            this.primero.anterior = nuevo;
        }
        this.primero = nuevo;
    } 
    // Caso General: Insertar en el medio o al final
    else {
        Nodo<T> anterior = this.obtenerNodo(pos - 1);
        Nodo<T> siguiente = anterior.siguiente;

        nuevo.siguiente = siguiente;
        nuevo.anterior = anterior;
        
        anterior.siguiente = nuevo;
        
        if (siguiente != null) { // Evita NullPointerException si insertamos al final
            siguiente.anterior = nuevo;
        }
    }
    
    this.cantidadDatos++;
}
```

**Baja con Dos Enlaces (Lista Doblemente Enlazada)** Gracias al doble enlace, si tienes el nodo a eliminar, no necesitas buscar a su anterior con un ciclo (salvo que uses `obtenerNodo(pos)` para llegar a él). El objetivo es que el nodo anterior y el siguiente se apunten mutuamente, puenteando y desconectando por completo al nodo central.


```Java
public T bajaDosEnlaces(int pos) {
    // Validación de seguridad
    if (this.primero == null || pos < 0 || pos >= this.cantidadDatos) {
        return null;
    }

    T datoEliminado;

    // Caso Especial: Borrar el primero
    if (pos == 0) {
        datoEliminado = this.primero.dato;
        this.primero = this.primero.siguiente;
        
        if (this.primero != null) { // Cortamos el rastro hacia atrás
            this.primero.anterior = null;
        }
    } 
    // Caso General: Borrar en el medio o el último
    else {
        Nodo<T> nodoEliminar = this.obtenerNodo(pos);
        datoEliminado = nodoEliminar.dato;
        
        Nodo<T> anterior = nodoEliminar.anterior;
        Nodo<T> siguiente = nodoEliminar.siguiente;
        
        anterior.siguiente = siguiente; // Puente de ida
        
        if (siguiente != null) { // Puente de vuelta (si no estamos borrando el último)
            siguiente.anterior = anterior;
        }
    }
    
    this.cantidadDatos--;
    return datoEliminado;
}
```


# 🚨 Análisis de Casos Especiales y Rupturas en Listas

## 1. Alta Simple: Insertar al principio (`pos = 0`)

### ❌ ¿Qué pasa si intento hacerlo "normal"? (El Error)

En el caso general, la regla es: "busco al nodo `anterior`, el nuevo se engancha al `siguiente`, y el `anterior` se engancha al nuevo". Si `pos = 0`, el nodo anterior matemáticamente estaría en la posición `-1`. Ese nodo no existe (`null`).



```Plaintext
[ PUNTERO NULL ]
+-------------------+
| null (No existe)  |
+-------------------+
          |
          V
💣 CRASH: NullPointerException al intentar hacer `anterior.siguiente = nuevo`
```

### ✅ La Solución Correcta

Como no hay nodo anterior, omitimos el puente y operamos directamente sobre el puntero maestro `primero`.



```
SITUACIÓN INICIAL:
primero ---> +-------------------+
             | Dato: "A"         |
             | Siguiente: -----> | (Apunta al resto o a null)
             +-------------------+

PASO 1: nuevo.siguiente = primero;
+-------------------+             +-------------------+
| Dato: "NUEVO"     |             | Dato: "A"         |
| Siguiente: -----> | ----------> | Siguiente: -----> |
+-------------------+             +-------------------+

PASO 2: primero = nuevo;
primero ---> +-------------------+             +-------------------+
             | Dato: "NUEVO"     |             | Dato: "A"         |
             | Siguiente: -----> | ----------> | Siguiente: -----> |
             +-------------------+             +-------------------+
```

## 2. Baja Simple: Borrar el primero (`pos = 0`)

### ❌ ¿Qué pasa si intento hacerlo "normal"? (El Error)

El caso general nos dice: "buscá al nodo anterior y puentealo (que su `.siguiente` apunte al `.siguiente` del que vas a borrar)". De nuevo, al intentar buscar al anterior a la posición 0, obtenemos `null`.



```
[ PUNTERO NULL ]
+-------------------+
| null (No existe)  |
+-------------------+
          |
          V
💣 CRASH: NullPointerException al intentar hacer `anterior.siguiente = ...`
```

### ✅ La Solución Correcta

Como no hay nadie atrás que deba "puentear", simplemente agarramos el puntero `primero` y lo corremos una posición hacia adelante.



```
SITUACIÓN INICIAL:
             +-------------------+             +-------------------+
primero ---> | Dato: "A" (Borrar)|             | Dato: "B"         |
             | Siguiente: -----> | ----------> | Siguiente: -----> |
             +-------------------+             +-------------------+

PASO ÚNICO: primero = primero.siguiente;
                                               +-------------------+
primero -------------------------------------> | Dato: "B"         |
                                               | Siguiente: -----> |
                                               +-------------------+
(El nodo "A" se queda sin flechas que lo apunten y Java lo elimina).
```

## 3. Alta Doble: Insertar al principio con Lista Vacía

En la lista doble tenemos los punteros hacia atrás (`Anterior`).

### ❌ ¿Qué pasa si intento hacerlo "normal"? (El Error)

La lógica dice: "El nuevo mira hacia adelante (al primero), y el primero mira hacia atrás (al nuevo)". Código: `nuevo.siguiente = primero;` -> `primero.anterior = nuevo;`


Si la lista está vacía, `primero` es `null`.

```
+-------------------+
| Dato: "NUEVO"     | 
| Siguiente: null   | 
+-------------------+

Queremos que el 'primero' mire hacia atrás:
`primero.anterior = nuevo;`
          |
          V
💣 CRASH: NullPointerException. Como 'primero' es null, no tiene el atributo '.anterior'.
```

### ✅ La Solución Correcta

Antes de pedirle al primer nodo que "nos dé la mano hacia atrás", preguntamos si ese nodo existe de verdad.


```
CÓDIGO:
nuevo.siguiente = primero;
if (primero != null) {            <--- LA CLAVE SALVADORA
    primero.anterior = nuevo;
}
primero = nuevo;

RESULTADO (Lista que estaba vacía):
primero ---> +-------------------+
             | <--- Ant: null    |
             | Dato: "NUEVO"     |
             | Siguiente: null   |
             +-------------------+
```

## 4. Baja Doble: Borrar el último elemento

### ❌ ¿Qué pasa si intento hacerlo "normal"? (El Error)

El caso general dice: "Hacé que el anterior y el siguiente se agarren de las manos entre ellos, puenteando al nodo central". Código del puente de ida: `anterior.siguiente = siguiente;` Código del puente de vuelta: `siguiente.anterior = anterior;`


Si borramos el último nodo, su `siguiente` es `null`.


```
Queremos hacer el puente de vuelta desde el "siguiente":
`siguiente.anterior = anterior;`
          |
          V
💣 CRASH: NullPointerException. Al borrar el último, 'siguiente' es null. 
No podés pedirle a 'null' que se agarre de la mano hacia atrás.
```

### ✅ La Solución Correcta

El puente de ida (hacia adelante) se hace siempre. Pero el puente de vuelta (hacia atrás) **solo se hace si el nodo de adelante existe**.


```
SITUACIÓN INICIAL (Borrando a "C"):
+-------------------+             +-------------------+
| <--- Ant          |             | <--- Ant          |
| Dato: "B"         | <=========> | Dato: "C" (Borrar)| ---> null
| Siguiente: -----> |             | Siguiente: null   |
+-------------------+             +-------------------+

CÓDIGO:
Nodo anterior = C.anterior;   // Es "B"
Nodo siguiente = C.siguiente; // Es null

PASO 1: Puente de ida
anterior.siguiente = siguiente; // B.siguiente ahora es null

PASO 2: Puente de vuelta (SE EVITA EL CRASH)
if (siguiente != null) {          <--- LA CLAVE SALVADORA
    siguiente.anterior = anterior;
}

RESULTADO FINAL:
+-------------------+
| <--- Ant          |
| Dato: "B"         | ---> null
| Siguiente: null   |
+-------------------+
(El nodo C queda totalmente desconectado).
```