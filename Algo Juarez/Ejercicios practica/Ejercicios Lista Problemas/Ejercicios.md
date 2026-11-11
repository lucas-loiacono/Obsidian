
Asumo que la `Lista<T>` tiene la semántica habitual del cursor: `iniciarCursor()` lo deja en el primer elemento, `obtenerCursor()` devuelve `null` si no hay elemento válido, y `avanzarCursor()` devuelve `true` si después de avanzar el cursor apunta a un elemento. Si tu cátedra lo define distinto, ajustá solo las condiciones de los `while`.

```java
public Lista<String> comidasPermitidas(Lista<String> ingredientesProhibidos) {
    Lista<String> resultado = new Lista<>();

    comidas.iniciarCursor();
    while (comidas.obtenerCursor() != null) {
        Comida comida = comidas.obtenerCursor();

        if (!tieneProhibido(comida.getIngredientes(), ingredientesProhibidos)) {
            resultado.agregar(comida.getNombre());
        }
        comidas.avanzarCursor();
    }
    return resultado;
}

private boolean tieneProhibido(Lista<String> ingredientes, Lista<String> prohibidos) {
    boolean encontrado = false;

    ingredientes.iniciarCursor();
    while (!encontrado && ingredientes.obtenerCursor() != null) {
        if (contiene(prohibidos, ingredientes.obtenerCursor())) {
            encontrado = true;
        } else {
            ingredientes.avanzarCursor();
        }
    }
    return encontrado;
}

private boolean contiene(Lista<String> lista, String elemento) {
    boolean encontrado = false;

    lista.iniciarCursor();
    while (!encontrado && lista.obtenerCursor() != null) {
        if (lista.obtenerCursor().equals(elemento)) {
            encontrado = true;
        } else {
            lista.avanzarCursor();
        }
    }
    return encontrado;
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