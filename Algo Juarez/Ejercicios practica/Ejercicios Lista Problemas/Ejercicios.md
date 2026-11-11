
Asumo que la `Lista<T>` tiene la semántica habitual del cursor: `iniciarCursor()` lo deja en el primer elemento, `obtenerCursor()` devuelve `null` si no hay elemento válido, y `avanzarCursor()` devuelve `true` si después de avanzar el cursor apunta a un elemento. Si tu cátedra lo define distinto, ajustá solo las condiciones de los `while`.

```java
// POS: devuelve una lista con los nombres de las comidas
//      que no tienen ningún ingrediente prohibido.
public Lista<String> comidasPermitidas(Lista<String> ingredientesProhibidos) {
    Lista<String> resultado = new Lista<>();

    comidas.iniciarCursor();
    boolean hayComida = comidas.obtenerCursor() != null;

    while (hayComida) {
        Comida comida = comidas.obtenerCursor();

        if (!tieneProhibido(comida.getIngredientes(), ingredientesProhibidos)) {
            resultado.agregar(comida.getNombre());
        }
        hayComida = comidas.avanzarCursor();
    }
    return resultado;
}

// true si algún ingrediente de la lista está en prohibidos
private boolean tieneProhibido(Lista<String> ingredientes, Lista<String> prohibidos) {
    ingredientes.iniciarCursor();
    boolean hayIngrediente = ingredientes.obtenerCursor() != null;

    while (hayIngrediente) {
        if (contiene(prohibidos, ingredientes.obtenerCursor())) {
            return true;                 // corte temprano
        }
        hayIngrediente = ingredientes.avanzarCursor();
    }
    return false;
}

// true si el elemento está en la lista
private boolean contiene(Lista<String> lista, String elemento) {
    lista.iniciarCursor();                // reinicia el cursor en cada búsqueda
    boolean hayMas = lista.obtenerCursor() != null;

    while (hayMas) {
        if (lista.obtenerCursor().equals(elemento)) {
            return true;
        }
        hayMas = lista.avanzarCursor();
    }
    return false;
}
```

Hay que llamar a `iniciarCursor()` al principio de cada recorrido, sobre todo en `contiene`. La lista de prohibidos se recorre una vez por cada ingrediente, y si no reiniciás el cursor, la segunda búsqueda arranca donde terminó la anterior.

Acá va la complejidad, en markdown para pegar en Obsidian:


## Complejidad de `comidasPermitidas`

**Variables**
- `C` = cantidad de comidas del menú
- `I` = máx. de ingredientes de una comida
- `P` = cantidad de ingredientes prohibidos

**Justificación**
- `contiene`: recorre la lista de prohibidos como mucho una vez → **O(P)**
- `tieneProhibido`: llama a `contiene` por cada ingrediente de la comida → **O(I · P)**
- `comidasPermitidas`: llama a `tieneProhibido` por cada comida → **O(C · I · P)**
- Operaciones con cursor (`iniciarCursor`, `avanzarCursor`, `obtenerCursor`) son **O(1)**

**Costo de `agregar` al resultado**
- Si `agregar(T)` inserta al final **sin puntero a último**, cuesta O(k) con k = tamaño actual
- Se hace hasta C veces → suma O(C²) en el peor caso
- Total: **O(C · I · P + C²)**
- Si la lista tiene puntero a último (agregar O(1)): total **O(C · I · P)**

**Mejora posible**
- Volcar los prohibidos a un `HashSet` antes de empezar: costo O(P)
- Cada consulta pasa a O(1) esperado → **O(P + C · I)** (más lo de `agregar`)

El costo de `agregar` depende de cómo esté implementada tu `Lista`. En el enunciado 2.3 solo se ven `primero`, `cursor` y `tamanio`, o sea que probablemente no hay `ultimo`. Si tu implementación tampoco lo tiene, justificá con el término `C²`. Si lo tiene, queda en O(C · I · P).