

Sí, es ir cada vez más adentro, pero lo importante es **qué te hace bajar un nivel**. Y tu intuición de "siempre estoy comparando con algo" es justo la clave.

**La idea central**

Cada ejercicio es una cadena de preguntas. Empezás con la pregunta grande del enunciado y la vas partiendo en preguntas más chicas hasta llegar a una comparación simple (dos valores, un `equals` o un `>=`).

Tomá `comidasPermitidas`:

1. ¿Qué comidas no tienen ningún ingrediente prohibido? → recorro las comidas y por cada una pregunto:
2. ¿Esta comida tiene algún ingrediente prohibido? → recorro sus ingredientes y por cada uno pregunto:
3. ¿Este ingrediente está en la lista de prohibidos? → recorro los prohibidos y por cada uno comparo:
4. ¿Este prohibido es igual a este ingrediente? → `equals`. Ahí termina.

**Cuándo bajás un nivel**

Bajás un nivel cada vez que, para responder una pregunta, necesitás **recorrer otra lista**. Y eso pasa en dos situaciones:

- **El elemento contiene una lista** (la comida tiene ingredientes, la película tiene actores).
- **Tenés que compararlo contra una lista** (¿está en prohibidos? ¿está en favoritos?).

Por eso sentís que siempre comparás con algo: el filtro del enunciado casi siempre es "los elementos de A que cumplen algo respecto de la lista B". Ese "respecto de B" es el nivel nuevo.

**Cómo se traduce a código**

Cada pregunta es un método, y cada método tiene un solo `while`:

|Nivel|Método|Recorre|Devuelve|
|---|---|---|---|
|1|el método del enunciado|la lista principal|la lista resultado|
|2|`tieneIngredienteProhibido`|la lista interna del elemento|`boolean`|
|3|`esProhibido`|la lista contra la que comparás|`boolean`|

**Cómo se ve la diferencia entre los dos tipos de recorrido**

- **Nivel 1 (filtrar):** recorre _todo_, sin corte temprano, y `avanzarCursor()` va siempre al final. Tiene que pasar por todos los elementos porque cada uno puede ir al resultado.
- **Niveles 2 y 3 (preguntar "¿hay alguno?" o "¿está?"):** cortan apenas encuentran, con `encontrado`, y `avanzarCursor()` va en el `else`.

**Cómo atacarlo cuando te enfrentás a un ejercicio nuevo**

1. Leé el enunciado y marcá qué listas aparecen y cuál es la que se devuelve.
2. Escribí el método principal asumiendo que los auxiliares ya existen: `if (cumple && hayAlgo(...))`.
3. Implementá cada auxiliar como un recorrido que responde una sola pregunta.
4. Repetí hasta que la pregunta sea una comparación simple.

Si querés, te lo dejo en markdown para pegar en Obsidian.







Sí, es exactamente un triple `for` anidado, pero con el cursor en lugar del índice. Cada pieza del `for` tiene su equivalente:

|`for` con índice|`while` con cursor|
|---|---|
|`int i = 0`|`lista.iniciarCursor()`|
|`i < n`|`lista.obtenerCursor() != null`|
|`lista[i]`|`lista.obtenerCursor()`|
|`i++`|`lista.avanzarCursor()`|
|`&& !encontrado` en la condición|igual (corte temprano sin `break`)|

Así se ve el mismo ejercicio (`comidasPermitidas`) de las dos formas:

```java
// Con arrays e índices: todo anidado en un método
for (int i = 0; i < comidas.length; i++) {
    boolean prohibido = false;
    for (int j = 0; !prohibido && j < comidas[i].ingredientes.length; j++) {
        for (int k = 0; !prohibido && k < prohibidos.length; k++) {
            if (prohibidos[k].equals(comidas[i].ingredientes[j])) {
                prohibido = true;
            }
        }
    }
    if (!prohibido) filtradas.add(comidas[i].nombre);
}
```

Con cursor es lo mismo, pero cada `for` pasa a ser un método:

|`for`|Método con cursor|
|---|---|
|`for i` (comidas)|`comidasPermitidas`|
|`for j` (ingredientes)|`tieneIngredienteProhibido`|
|`for k` (prohibidos)|`esProhibido`|

Hay dos diferencias importantes:

- **El índice vive en tu variable, el cursor vive dentro de la lista.** Con `for` podés tener `j` y `k` sobre la misma lista sin problema. Con cursor, cada lista tiene un solo cursor, así que no podés recorrer la misma lista con dos niveles a la vez. Por eso hay que llamar a `iniciarCursor()` antes de cada recorrido: es el equivalente a escribir `int k = 0` de nuevo en cada vuelta del `for` de afuera.
- **Separar en métodos evita pisar cursores y se lee mejor,** pero el costo es el mismo que el del triple `for`: O(C · I · P).

Para Obsidian:


## Simetría: doble/triple `for` ↔ `while` con cursor

| `for` con índice | `while` con cursor |
|---|---|
| `int i = 0` | `iniciarCursor()` |
| `i < n` | `obtenerCursor() != null` |
| `arr[i]` | `obtenerCursor()` |
| `i++` | `avanzarCursor()` |
| `&& !encontrado` en la condición | igual (corte sin `break`) |

**Anidamiento**
- `for i` (principal) → método del enunciado
- `for j` (lista interna) → auxiliar booleano nivel 2
- `for k` (lista de comparación) → auxiliar booleano nivel 3

**Diferencias**
- El índice es una variable mía, el cursor está dentro de la lista (uno solo por lista)
- Hay que hacer `iniciarCursor()` antes de cada recorrido (equivale a reiniciar `k = 0`)
- La complejidad es la misma: producto de los tamaños, O(C · I · P)
