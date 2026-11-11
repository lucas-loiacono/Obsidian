

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