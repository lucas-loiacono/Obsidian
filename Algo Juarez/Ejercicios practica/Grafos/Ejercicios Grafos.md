
![[Pasted image 20261108195408.png]]


# BFS del 6.1 a ojo: paso a paso

## Idea central
Voy leyendo mi **lista de nodos en el orden en que los fui anotando**. De cada nodo anoto sus **hijos nuevos** (los que todavía no descubrí). Si un nodo tiene varios hijos, **los conservo a todos** y los ordeno **alfabéticamente**.

## Paso a paso

1. **Arranco en A.** Lista: `A`
2. **Leo A.** Tiene dos hijos: C y D. Los dos entran, y C va antes que D por alfabético. Lista: `C, D`
3. **Leo C** (vino primero). Su hijo nuevo es F. Lista: `D, F`
4. **Leo D.** Tiene dos hijos nuevos: B y G. Los acomodo alfabéticamente: primero B, después G. Lista: `F, B, G`
5. **Leo F.** Sus vecinos ya fueron descubiertos, no tiene hijos nuevos. Lo dejo ahí y sigo.
6. **Leo B.** Su hijo nuevo es E. Lista: `G, E`
7. **Leo G.** Su hijo nuevo es I. Lista: `E, I`
8. **Leo E.** Sin hijos nuevos. Sigo.
9. **Leo I.** Su hijo nuevo es J. Lista: `J`
10. **Leo J.** Su hijo nuevo es H. Lista: `H`
11. **Leo H.** Sin hijos nuevos. La lista queda vacía: **fin**.

## Resultado

**Recorrido BFS: A, C, D, F, B, G, E, I, J, H**

## Dos ajustes a la explicación original

- **No me "quedo" con el menor, los conservo a todos.** El alfabético solo decide **cuál se lee primero**. Si descartara a D, nunca aparecería en el recorrido.
- **No sigo una rama hasta H, sigo mi lista en orden.** Llego a H porque es el último eslabón (G → I → J → H), no porque baje por una rama sola. Si hubiera otro nodo en el medio de la lista, lo tendría que leer antes.

## Reglas para recordar

- **Se lee en el orden en que se anotó.** Lo que vino antes se lee antes (por eso F, hijo de C, se lee antes que B y G, hijos de D).
- **Alfabético = desempate entre hermanos**, no orden global del nivel.
- **Un nodo sin hijos nuevos no es un error:** todos sus vecinos ya los descubrió otro.
- **Control final:** 10 nodos, sin repetir, y cada nivel completo antes de pasar al siguiente.

## Por niveles (para verificar)

| Nivel | Nodos   | De quién cuelgan   |
| ----- | ------- | ------------------ |
| 0     | A       | origen             |
| 1     | C, D    | A                  |
| 2     | F, B, G | F de C; B y G de D |
| 3     | E, I    | E de B; I de G     |
| 4     | J       | I                  |
| 5     | H       | J                  |





# Ejercicio 6.1: recorrido BFS desde A

## ¿Qué es BFS?

**BFS** (_Breadth-First Search_, búsqueda en anchura) es una forma de recorrer un grafo **por capas**: primero se visita el nodo inicial, después todos sus vecinos directos, después los vecinos de esos vecinos, y así sucesivamente. Es como una onda que se expande desde el origen.

Se implementa con una **cola**:

1. Se encola el nodo inicial y se lo marca como visitado.
2. Mientras la cola no esté vacía: se saca el primer nodo, se lo visita (se lo agrega al recorrido) y se encolan todos sus vecinos **que todavía no fueron visitados**, marcándolos al encolarlos.

Es el mismo recorrido por niveles que hicimos en el árbol con la cola, pero en un grafo hay que marcar los visitados para no repetir nodos (porque puede haber ciclos).

## Lectura del grafo

Por las líneas del dibujo, las conexiones son:

|Nodo|Vecinos|
|---|---|
|A|C, D|
|B|D, E, G|
|C|A, F|
|D|A, B, F, G|
|E|B|
|F|C, D, G|
|G|B, D, F, I|
|H|J|
|I|G, J|
|J|H, I|

El enunciado no dice en qué orden visitar los vecinos, así que uso el **orden alfabético**, que es la convención habitual.

## Seguimiento

|Paso|Se saca de la cola|Se encolan (nuevos)|Cola resultante|Recorrido hasta ahora|
|---|---|---|---|---|
|inicio||A|[A]||
|1|A|C, D|[C, D]|A|
|2|C|F (A ya visitado)|[D, F]|A, C|
|3|D|B, G (A y F ya están)|[F, B, G]|A, C, D|
|4|F|nada (C, D, G ya están)|[B, G]|A, C, D, F|
|5|B|E (D y G ya están)|[G, E]|A, C, D, F, B|
|6|G|I|[E, I]|A, C, D, F, B, G|
|7|E|nada|[I]|A, C, D, F, B, G, E|
|8|I|J|[J]|A, C, D, F, B, G, E, I|
|9|J|nada (H no es vecino directo de I, y J ya está)|[]|A, C, D, F, B, G, E, I, J|

Al llegar a J, se encolaría H como vecino no visitado. Corrijo el paso 9: J tiene a H como vecino, así que:

| 9 | J | H | [H] | ..., I, J |  
| 10 | H | nada | [] | ..., J, H |

## Resultado

**A, C, D, F, B, G, E, I, J, H**

## Por capas (para verificar)

- **Nivel 0:** A
- **Nivel 1:** C, D (vecinos de A)
- **Nivel 2:** F, B, G (vecinos de C y D)
- **Nivel 3:** E, I (E viene de B, I viene de G)
- **Nivel 4:** J
- **Nivel 5:** H

Si tu cátedra visita los vecinos en otro orden (por ejemplo, el de la lista de adyacencia que hayan definido), el recorrido cambia en el orden dentro de cada nivel, pero los **niveles** siempre son los mismos.

# Método práctico para resolver un BFS a mano

La idea es no armar tablas largas. Con **dos cosas** alcanza: una lista de adyacencia y la cola escrita en una línea.

## Paso 1: armá la lista de adyacencia

Leé el dibujo y anotá los vecinos de cada nodo, **en orden alfabético**. Es lo único que lleva tiempo, y si lo hacés bien el resto es mecánico.

```
A: C, D
B: D, E, G
C: A, F
D: A, B, F, G
E: B
F: C, D, G
G: B, D, F, I
H: J
I: G, J
J: H, I
```

Tip para no equivocarte: contá las líneas del dibujo y verificá que la cantidad de vecinos sumados sea el doble (cada línea aparece en dos nodos). Acá hay 12 líneas y la suma de vecinos da 24.

## Paso 2: recorré con una sola línea de seguimiento

Escribí el **recorrido** (lo ya visitado) y la **cola** (lo pendiente). Cada vez que sacás un nodo, agregás al final de la cola sus vecinos que **todavía no aparecieron ni en el recorrido ni en la cola**.

```
Recorrido: A            Cola: C D
Recorrido: A C          Cola: D F
Recorrido: A C D        Cola: F B G
Recorrido: A C D F      Cola: B G
Recorrido: A C D F B    Cola: G E
Recorrido: A C D F B G  Cola: E I
Recorrido: ... E        Cola: I
Recorrido: ... I        Cola: J
Recorrido: ... J        Cola: H
Recorrido: ... H        Cola: (vacía)
```

**Resultado: A, C, D, F, B, G, E, I, J, H**

## Truco para verificar: por niveles

Una vez que tenés el resultado, chequealo contando distancias desde A:

- **Nivel 1:** vecinos directos de A → C, D
- **Nivel 2:** vecinos de esos que faltan → F, B, G
- **Nivel 3:** E, I
- **Nivel 4:** J
- **Nivel 5:** H

El BFS tiene que listar **todos los del nivel 1, después todos los del nivel 2**, etc. Si en tu resultado aparece un nodo de nivel 3 antes que uno de nivel 2, hay un error.

## Reglas para no fallar en el examen

1. **Orden de vecinos:** si el enunciado no lo aclara, usá alfabético y **escribilo en la respuesta** ("visito los vecinos en orden alfabético").
2. **Marcá al encolar, no al sacar.** Así evitás meter el mismo nodo dos veces en la cola.
3. **Un nodo que ya está en la cola no se vuelve a encolar**, aunque todavía no lo hayas "visitado".
4. **Nodos desconectados:** si algún nodo no es alcanzable desde A, no aparece en el BFS. Acá todos son alcanzables (H se llega por J), así que aparecen los 10.

## Si te piden DFS

Es igual de mecánico, pero con una **pila** (o recursión) en lugar de cola: vas siempre por el primer vecino no visitado hasta que no puedas avanzar, y ahí retrocedés. Si te lo piden, lo hacemos con el mismo método.



# BFS del 6.1 con el método de la tabla

## Paso 1: armar la matriz

El grafo es no dirigido, así que la matriz es **simétrica**: cada línea del dibujo aparece dos veces. Aristas: A-C, A-D, B-D, B-E, B-G, C-F, D-F, D-G, F-G, G-I, I-J, H-J.

| origen \ destino | a   | b   | c   | d   | e   | f   | g   | h   | i   | j   |
| ---------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **a**            | 0   | 0   | 1   | 1   | 0   | 0   | 0   | 0   | 0   | 0   |
| **b**            | 0   | 0   | 0   | 1   | 1   | 0   | 1   | 0   | 0   | 0   |
| **c**            | 1   | 0   | 0   | 0   | 0   | 1   | 0   | 0   | 0   | 0   |
| **d**            | 1   | 1   | 0   | 0   | 0   | 1   | 1   | 0   | 0   | 0   |
| **e**            | 0   | 1   | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   |
| **f**            | 0   | 0   | 1   | 1   | 0   | 0   | 1   | 0   | 0   | 0   |
| **g**            | 0   | 1   | 0   | 1   | 0   | 1   | 0   | 0   | 1   | 0   |
| **h**            | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 1   |
| **i**            | 0   | 0   | 0   | 0   | 0   | 0   | 1   | 0   | 0   | 1   |
| **j**            | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 1   | 1   | 0   |

Las columnas ya están en orden alfabético, así que al leer una fila de izquierda a derecha los vecinos salen en el orden correcto.

## Paso 2: recorrer

Cada vez que **descubrís** un nodo lo marcás con el siguiente número de orden. Terminás de leer la fila y saltás al **siguiente número que todavía no leíste**, que es el orden de la cola.

|Fila que leo|1s en la fila|Marco (nuevos)|Próximos saltos|
|---|---|---|---|
|inicio||**a = 1**|a|
|**a**|c, d|**c = 2, d = 3**|c, d|
|**c**|a, f|a ya marcado, **f = 4**|d, f|
|**d**|a, b, f, g|**b = 5, g = 6**|f, b, g|
|**f**|c, d, g|todos marcados|b, g|
|**b**|d, e, g|**e = 7**|g, e|
|**g**|b, d, f, i|**i = 8**|e, i|
|**e**|b|ya marcado|i|
|**i**|g, j|**j = 9**|j|
|**j**|h, i|**h = 10**|h|
|**h**|j|ya marcado|(vacía)|

La cola se vació y los 10 nodos están marcados, así que no hace falta reiniciar desde un nodo no visitado. Acá el grafo es conexo desde A.

## Resultado

|a|c|d|f|b|g|e|i|j|h|
|---|---|---|---|---|---|---|---|---|---|
|1|2|3|4|5|6|7|8|9|10|

**Recorrido BFS: A, C, D, F, B, G, E, I, J, H**

## Dónde se nota que es BFS y no "por ramas"

- Después de leer **c** (que descubrió f), no saltás a f. Saltás a **d**, el otro vecino de a. F espera su turno.
- Después de **d** tampoco saltás a b ni g: primero leés **f**, que se marcó antes.
- La regla es siempre la misma: el próximo salto es el **menor número de orden que todavía no leíste**.

Si en cambio saltaras al último nodo marcado cada vez, estarías haciendo DFS y obtendrías otro recorrido.


![[Pasted image 20261108195708.png]]


Sí, a ojo se puede, y es incluso más fácil que el BFS. La diferencia es que acá **no leés una lista en orden**: vas **siempre a fondo por un camino**, y cuando te trabás, retrocedés.

**Cómo hacerlo:**

1. Parás en un nodo y elegís su **vecino no visitado de menor alfabético**.
2. **Bajás enseguida** a ese vecino, sin terminar de mirar los otros.
3. Si un nodo no tiene vecinos nuevos, **retrocedés** al anterior y seguís con el próximo vecino pendiente de ese.
4. Al retroceder no anotás nada. Solo anotás cuando descubrís un nodo por primera vez.

**En el 6.2:**

- **A:** vecinos D, E, F, G, I. Voy al menor, **D**.
- **D:** vecinos A, B, G. A ya está, voy a **B**.
- **B:** vecinos C, D, E. Voy a **C**.
- **C:** su único vecino es B, que ya está. Retrocedo a B.
- **B (sigo):** quedaba E. Voy a **E**.
- **E:** vecinos A, B, I. Voy a **I**.
- **I:** vecinos A y E, ya están. Retrocedo a E, a B y a D.
- **D (sigo):** quedaba G. Voy a **G**.
- **G:** vecinos A, D, H. Voy a **H**.
- **H:** su único vecino es G. Retrocedo a G, a D y a A.
- **A (sigo):** quedaba F. Voy a **F**.
- **F:** su único vecino es A. Retrocedo a A, que no tiene pendientes: **fin**.

**Recorrido DFS: A, D, B, C, E, I, G, H, F**

**La diferencia clave con el BFS:**

- En BFS terminás de leer un nodo y saltás al siguiente de tu lista.
- En DFS bajás de inmediato al recién descubierto y solo volvés cuando te quedás sin salida.

**Lo que más se olvida:** al retroceder, **seguir mirando los vecinos que quedaron pendientes**. Al volver a D quedaba G, y al volver a A quedaba F. Si te salteás eso, el recorrido te sale incompleto.

**Truco a ojo:** podés ir dibujando el camino como una pila (A, D, B, C), tachando el último cuando te trabás. El nodo que queda al final de la pila es el que tenés que revisar de nuevo.

Si querés, te lo paso en markdown para Obsidian, junto con la comparación BFS contra DFS.

# Ejercicio 6.2: DFS desde A

**DFS** (_Depth-First Search_, búsqueda en profundidad) recorre el grafo yendo **lo más lejos posible** por un camino. Cuando se llega a un nodo sin vecinos nuevos, se **retrocede** hasta el último nodo que todavía tenga vecinos sin visitar. Se implementa con una **pila** o con recursión.

## Camino práctico

**Paso 1: lista de adyacencia en orden alfabético.** La nota del enunciado pide elegir siempre el menor, así que conviene tener los vecinos ya ordenados.

```
A: D, E, F, G, I
B: C, D, E
C: B
D: A, B, G
E: A, B, I
F: A
G: A, D, H
H: G
I: A, E
```

Verificación: hay 11 líneas en el dibujo y la suma de vecinos da 22, el doble.

**Paso 2: seguí un solo camino.** En cada nodo, andá al **primer vecino no visitado** de su lista. Si todos están visitados, retrocedé al nodo anterior y seguí con su próximo vecino pendiente. Anotá solo el recorrido y el camino de retroceso.

## Seguimiento

|Estoy en|Próximo vecino no visitado|Acción|
|---|---|---|
|A|D|avanzo a D|
|D|B (A ya visitado)|avanzo a B|
|B|C|avanzo a C|
|C|ninguno (B ya está)|**retrocedo** a B|
|B|E (D ya está)|avanzo a E|
|E|I (A y B ya están)|avanzo a I|
|I|ninguno (A y E ya están)|**retrocedo** a E, B, D|
|D|G (A y B ya están)|avanzo a G|
|G|H (A y D ya están)|avanzo a H|
|H|ninguno|**retrocedo** a G, D, A|
|A|F (D, E ya visitados; F es el siguiente no visitado)|avanzo a F|
|F|ninguno|retrocedo a A: no quedan pendientes, **fin**|

## Resultado

**A, D, B, C, E, I, G, H, F**

Se visitan los 9 nodos, así que el grafo es conexo.

## Para no fallar

1. **Al retroceder, no se anota nada.** Solo se anota un nodo cuando se lo visita por primera vez.
2. **Mirá siempre la lista del nodo al que volvés.** Es lo que más se olvida: al volver a B o a D todavía quedan vecinos pendientes (E y G).
3. **Control final:** el resultado debe tener todos los nodos, sin repetir ninguno.

## Diferencia con BFS

- **BFS** explora por capas y usa una **cola**.
- **DFS** se mete a fondo por un camino y usa una **pila** o recursión.

Por eso el mismo grafo da recorridos distintos: acá A va primero a D y baja hasta C, mientras que BFS listaría primero todos los vecinos de A (D, E, F, G, I).





## DFS del 6.2 con el método de la tabla

### Paso 1: la matriz

Es no dirigido, así que es simétrica. Aristas: A-D, A-E, A-F, A-G, A-I, B-C, B-D, B-E, D-G, E-I, G-H.

| origen \ destino | a | b | c | d | e | f | g | h | i |
|---|---|---|---|---|---|---|---|---|---|
| **a** | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 0 | 1 |
| **b** | 0 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 0 |
| **c** | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| **d** | 1 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| **e** | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| **f** | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| **g** | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 |
| **h** | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| **i** | 1 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 |

### Paso 2: la regla

1. Marcás el nodo inicial con el **1**.
2. Leés su fila de izquierda a derecha y tomás el **primer 1 cuyo nodo no esté marcado**.
3. **Lo marcás con el siguiente número y bajás enseguida a su fila.** No terminás de leer la fila actual.
4. Si en una fila **todos los 1 ya están marcados**, volvés a la fila anterior y seguís leyéndola desde donde la dejaste.

### Seguimiento

| Fila que leo | 1s en la fila | Primer no marcado | Acción |
|---|---|---|---|
| inicio | - | - | **a = 1** |
| **a** | d, e, f, g, i | d | **d = 2**, bajo a d |
| **d** | a, b, g | b | **b = 3**, bajo a b |
| **b** | c, d, e | c | **c = 4**, bajo a c |
| **c** | b | ninguno | vuelvo a b |
| **b** (sigo) | d, e | e (d ya está) | **e = 5**, bajo a e |
| **e** | a, b, i | i | **i = 6**, bajo a i |
| **i** | a, e | ninguno | vuelvo a e |
| **e** (sigo) | - | ninguno | vuelvo a b |
| **b** (sigo) | - | ninguno | vuelvo a d |
| **d** (sigo) | g | g | **g = 7**, bajo a g |
| **g** | a, d, h | h | **h = 8**, bajo a h |
| **h** | g | ninguno | vuelvo a g |
| **g** (sigo) | - | ninguno | vuelvo a d |
| **d** (sigo) | - | ninguno | vuelvo a a |
| **a** (sigo) | e, f, g, i | f (e ya está) | **f = 9**, bajo a f |
| **f** | a | ninguno | vuelvo a a, sin pendientes: **fin** |

### Resultado

| a | d | b | c | e | i | g | h | f |
|---|---|---|---|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

**Recorrido DFS: A, D, B, C, E, I, G, H, F**

### Para no fallar

- **Al volver a una fila, seguí desde donde la dejaste.** Al volver a `d` todavía quedaba `g`, y al volver a `a` quedaba `f`.
- **Al volver no se marca nada.** Solo se numera cuando se descubre un nodo por primera vez.
- **Control final:** los 9 nodos tienen número y ninguno se repite.



![[Pasted image 20261108200003.png]]

# Ejercicio 6.3

Orden de filas y columnas: A, B, C, D.

```
      A  B  C  D
  A [ 0  1  0  0 ]
  B [ 1  1  2  1 ]
  C [ 0  2  0  1 ]
  D [ 0  1  1  0 ]
```

Cada entrada `M[i][j]` es la cantidad de aristas entre `i` y `j`.

## a. Representación gráfica

Aristas que se leen de la matriz:

- **A-B**: 1 arista
- **B-B**: 1 **lazo** (`M[B][B] = 1`)
- **B-C**: **2 aristas paralelas** (`M[B][C] = 2`)
- **B-D**: 1 arista
- **C-D**: 1 arista

```
        ┌─┐
        │ ↻ (lazo)
  A ─── B ═══ C
        │     │
        └──── D
```

Entre B y C se dibujan dos líneas, y B tiene un lazo sobre sí mismo.

## b. Clasificación

1. **¿Dirigido? No.** La matriz es **simétrica** (`M[i][j] = M[j][i]` para todo par), así que cada arista va en ambos sentidos: es no dirigido.
2. **¿Simple? No.** Un grafo simple no tiene lazos ni aristas múltiples, y acá hay un lazo en B (`M[B][B] = 1`) y dos aristas entre B y C (`M[B][C] = 2`).
3. **¿Conexo? Sí.** B está conectado con A, C y D, así que desde cualquier vértice se llega a cualquier otro.
4. **¿DAG? No.** Un DAG es un grafo **dirigido** sin ciclos, y este es no dirigido. Además tiene ciclos (el lazo en B, las dos aristas paralelas B-C, y el triángulo B-C-D).

## c. Matriz de caminos de longitud 3

La entrada `(i, j)` de **M³** da la cantidad de caminos de longitud 3 entre `i` y `j`. Esto vale porque cada multiplicación de la matriz por sí misma suma, sobre todos los vértices intermedios, el producto de las cantidades de aristas.

**Primero M²:**

```
M² = [ 1  1  2  1 ]
     [ 1  7  3  3 ]
     [ 2  3  5  2 ]
     [ 1  3  2  2 ]
```

**Luego M³ = M² · M:**

```
M³ = [ 1   7   3   3 ]
     [ 7  17  17  10 ]
     [ 3  17   8   8 ]
     [ 3  10   8   5 ]
```

**Comprobación de una entrada:** `M³[A][A] = 1`. El único camino de longitud 3 de A a A es A→B→B→A, usando el lazo de B. Sale de la cuenta: `fila A de M² · columna A de M = 1·0 + 1·1 + 2·0 + 1·0 = 1`.

La matriz resultante es simétrica, como corresponde a un grafo no dirigido. Dejé el lazo contado como 1, tal cual figura en la matriz del enunciado.

## d. BFS desde D

Los vecinos de cada vértice, en orden alfabético:

```
A: B
B: A, B, C, D    (B es vecino de sí mismo por el lazo, ya visitado al encolar)
C: B, D
D: B, C
```

|Se saca|Se encolan|Cola|Recorrido|
|---|---|---|---|
|D|B, C|[B, C]|D|
|B|A|[C, A]|D, B|
|C|nada (B y D ya están)|[A]|D, B, C|
|A|nada|[]|D, B, C, A|

**Recorrido BFS: D, B, C, A**

Por niveles: **nivel 0** = D, **nivel 1** = B, C, **nivel 2** = A. El lazo y las aristas paralelas no cambian el recorrido, porque un vértice ya marcado no se vuelve a encolar.


# Metodología de cada punto (ejercicio 6.3)

La matriz ya tiene toda la información. Lo importante es saber qué mirar en cada punto.

## a. Dibujar el grafo desde la matriz

1. Dibujá un círculo por cada vértice (A, B, C, D).
2. Mirá **solo la mitad superior** de la matriz, incluida la diagonal, porque es simétrica y la otra mitad repite lo mismo.
3. Para cada entrada `M[i][j]`:
    - **Fuera de la diagonal:** el número es la cantidad de aristas entre `i` y `j`. Un 0 es sin arista, un 1 una línea y un 2 dos líneas paralelas.
    - **En la diagonal:** el número es la cantidad de **lazos** en ese vértice.

Si el grafo fuera dirigido (matriz no simétrica), `M[i][j]` sería una flecha de `i` a `j`, y habría que mirar la matriz entera.

## b. Clasificar el grafo

Cada propiedad se resuelve mirando algo distinto de la matriz:

|Propiedad|Qué mirar|Criterio|
|---|---|---|
|**Dirigido**|Simetría|Si `M[i][j] = M[j][i]` para todo par, es **no dirigido**. Si hay algún par distinto, es dirigido.|
|**Simple**|Diagonal y valores|Es simple solo si la **diagonal es toda 0** (sin lazos) y **ningún valor supera 1** (sin aristas múltiples). Basta un 1 en la diagonal o un 2 en cualquier lugar para que no sea simple.|
|**Conexo**|Alcanzabilidad|Elegí un vértice y fijate si podés llegar a todos. El atajo es buscar un vértice con la fila toda en 0 (aislado). Si no hay ninguno, hacé un BFS rápido para confirmar.|
|**DAG**|Dirigido + ciclos|Primero, ¿es dirigido? Si no lo es, **no puede ser DAG**, y ahí termina la justificación. Si lo es, buscá algún ciclo (incluidos los lazos). Sin ciclos es DAG.|

En la justificación, citá **la entrada concreta** que decide cada caso (por ejemplo `M[B][B] = 1` o `M[B][C] = 2`).

## c. Matriz de caminos de longitud 3

**Fundamento teórico (es lo que se justifica en el examen):** la entrada `(i, j)` de `Mᵏ` es la cantidad de caminos de longitud `k` entre `i` y `j`. Para `k = 2`, `M²[i][j] = Σ M[i][x] · M[x][j]`, que suma sobre todos los vértices intermedios `x` el número de formas de ir `i → x → j`. Para `k = 3` se repite el argumento por inducción: `M³ = M² · M`.

**Procedimiento práctico:**

1. Calculá `M²`. Como la matriz es simétrica, la **columna `j` es igual a la fila `j`**. Entonces cada entrada es un producto escalar de dos filas. Calculá solo la mitad superior y copiá la otra.
2. Calculá `M³ = M² · M`, también con producto escalar fila por columna.
3. Verificá con tres controles:
    - **Simetría:** `M³` tiene que salir simétrica. Si no, hay un error de cuenta.
    - **Una entrada a mano:** elegí una pequeña (como `M³[A][A]`) y enumerá los caminos. Acá es solo A→B→B→A.
    - **Suma de filas:** la suma de una fila de `M³` debe coincidir con `(M² · M · 1)`, es decir, multiplicar por el vector de unos.

Cuando hay lazos o aristas paralelas, "camino" significa que se pueden repetir vértices y aristas, y las aristas paralelas cuentan como caminos distintos (por eso aparece el 2 multiplicando).

## d. BFS desde D

1. **Lista de adyacencia a partir de la matriz:** cada fila, mirada de izquierda a derecha, te da los vecinos **ya en orden alfabético**, porque las columnas están ordenadas A, B, C, D. Tomá las columnas con valor distinto de 0.
2. **Ignorá la diagonal y los múltiples:** un lazo no agrega vecinos nuevos, y un 2 sigue siendo un solo vecino.
3. Aplicá el método de siempre: recorrido en una línea y cola en otra. Al sacar un nodo, encolás sus vecinos que no estén ni en el recorrido ni en la cola.
4. Verificá por niveles: nivel 0 = D, nivel 1 = sus vecinos (B, C), nivel 2 = A.

## Resumen del orden de trabajo

1. Leé la matriz una vez para obtener las aristas y la lista de adyacencia.
2. Con eso resolvés **a, b y d** sin más cuentas.
3. El único punto que requiere cálculo es **c**, y se resuelve multiplicando matrices.


![[Pasted image 20261108200239.png]]

# Ejercicio 6.4: respuesta (c)

Se pide M³, porque la entrada `(i, j)` de `M³` es la cantidad de caminos de longitud 3 entre `i` y `j`.

## Cálculo

```
M = [ 1 1 0 ]
    [ 1 0 1 ]
    [ 0 1 0 ]
```

**Primero M².** La matriz es simétrica, así que cada fila de `M²` se arma sumando filas de `M` según los coeficientes de la fila de `M`:

- Fila A: `[1,1,0]` → fila A + fila B = `[2, 1, 1]`
- Fila B: `[1,0,1]` → fila A + fila C = `[1, 2, 0]`
- Fila C: `[0,1,0]` → fila B = `[1, 0, 1]`

```
M² = [ 2 1 1 ]
     [ 1 2 0 ]
     [ 1 0 1 ]
```

**Luego M³ = M² · M**, con el mismo truco:

- Fila A: `[2,1,1]` → 2·(fila A) + fila B + fila C = `[2,2,0] + [1,0,1] + [0,1,0]` = `[3, 3, 1]`
- Fila B: `[1,2,0]` → fila A + 2·(fila B) = `[1,1,0] + [2,0,2]` = `[3, 1, 2]`
- Fila C: `[1,0,1]` → fila A + fila C = `[1,1,0] + [0,1,0]` = `[1, 2, 0]`

```
M³ = [ 3 3 1 ]
     [ 3 1 2 ]
     [ 1 2 0 ]
```

Esto coincide con la opción **(c)**.

## Camino práctico: descartar sin calcular todo

Como es de opción múltiple, alcanza con calcular **algunas entradas a mano** contando caminos. El grafo tiene un lazo en A y las aristas A-B y B-C.

1. **`M³[B][B]`**: los únicos caminos de longitud 3 de B a B son B→A→A→B (usa el lazo de A). Eso da **1**. La opción (a) tiene un 0 ahí y la (b)... veamos todas: (a) tiene `M³[B][B] = 0`, así que se descarta. Las demás tienen 1.
2. **`M³[C][C]`**: C solo es vecino de B, y B no tiene lazo, así que no hay camino C→B→x→C. Eso da **0**. La opción (d) tiene 1 ahí, así que se descarta.
3. **`M³[A][C]`**: el único camino es A→A→B→C. Eso da **1**. La opción (b) tiene 0 ahí, así que se descarta.

Queda solo la **(c)**.

## Control de `M³[A][A] = 3`

Los caminos de longitud 3 de A a A son:

- A→A→A→A
- A→A→B→A
- A→B→A→A

Son 3, igual que en la matriz.

## Reglas generales

1. **Fundamento:** `Mᵏ` cuenta caminos de longitud `k`, y se puede repetir vértices y aristas (por eso el lazo suma).
2. **Simetría:** si `M` es simétrica, `M³` también. Si el resultado no lo es, hay un error de cuenta.
3. **Con opciones:** calculá entradas sueltas contando caminos y descartá, en vez de multiplicar matrices completas.

![[Pasted image 20261108200409.png]]

# Ejercicio 6.5

**Respuesta: de B hacia A hay 6 caminos, y de A hacia B hay 4.**

## Qué mirar primero

Esta matriz **no es simétrica** (`M[A][B] = 1` pero `M[B][A] = 1`, y `M[A][C] = 0` pero `M[C][A] = 1`), así que el grafo es **dirigido**. Por eso importa el sentido: `M[i][j]` cuenta las flechas de `i` hacia `j`, y la entrada `(i, j)` de `M⁴` cuenta los caminos de longitud 4 **de `i` hacia `j`**.

```
      A  B  C
  A [ 1  1  0 ]
  B [ 1  0  1 ]
  C [ 1  0  0 ]
```

## Cálculo

Cada fila de `M · N` se arma sumando las filas de `N` según los coeficientes de la fila correspondiente de `M`.

**M²:**

- Fila A: `[1,1,0]` → fila A + fila B = `[2, 1, 1]`
- Fila B: `[1,0,1]` → fila A + fila C = `[2, 1, 0]`
- Fila C: `[1,0,0]` → fila A = `[1, 1, 0]`

```
M² = [ 2 1 1 ]
     [ 2 1 0 ]
     [ 1 1 0 ]
```

**M⁴ = M² · M²:**

- Fila A: `[2,1,1]` → 2·`[2,1,1]` + `[2,1,0]` + `[1,1,0]` = `[7, 4, 2]`
- Fila B: `[2,1,0]` → 2·`[2,1,1]` + `[2,1,0]` = `[6, 3, 2]`
- Fila C: `[1,1,0]` → `[2,1,1]` + `[2,1,0]` = `[4, 2, 1]`

```
M⁴ = [ 7 4 2 ]
     [ 6 3 2 ]
     [ 4 2 1 ]
```

## Lectura

- **B hacia A** = `M⁴[B][A]` = **6**
- **A hacia B** = `M⁴[A][B]` = **4**

## Verificación

Calculé también `M³ = M² · M` y después `M⁴ = M³ · M`, y da lo mismo:

```
M³ = [ 4 2 1 ]
     [ 3 2 1 ]
     [ 2 1 1 ]
```

Comprobación de una entrada contando caminos, `A hacia B` de longitud 4 (los pasos posibles son A→A, A→B, B→A, B→C, C→A):

- A→A→A→A→B
- A→A→B→A→B
- A→B→A→A→B
- A→B→C→A→B

Son **4**, igual que en la matriz.

## Trampa típica

Si el grafo fuera no dirigido, las dos respuestas serían iguales. Acá son distintas (6 y 4) justamente porque es dirigido, así que no hay que intercambiar fila y columna al leer el resultado.


![[Pasted image 20261108200854.png]]



# Kruskal del 6.9 con grupos entre paréntesis

## Aristas ordenadas por peso

| Peso | Aristas |
|---|---|
| 1 | H-G |
| 2 | B-E |
| 3 | B-D, G-F |
| 4 | B-C, H-F |
| 5 | A-C |
| 6 | D-G |
| 7 | D-F, E-F |
| 8 | C-H |
| 9 | C-D |
| 10 | A-B |

## Reglas

1. Ninguna letra está en un grupo: **grupo nuevo**.
2. Una letra está en un grupo y la otra no: **la agrego a ese grupo**.
3. Las dos están en el mismo grupo: **salteo** (ciclo).
4. Cada letra está en un grupo distinto: **uno los dos grupos**.

## Paso a paso

| Iteración | Arista | Qué pasa | Grupos después |
|---|---|---|---|
| 1 | H-G (1) | ninguna está en un grupo: grupo nuevo | (H, G) |
| 2 | B-E (2) | ninguna está en un grupo: grupo nuevo | (H, G) (B, E) |
| 3 | B-D (3) | B está en un grupo, D no: agrego D | (H, G) (B, E, D) |
| 4 | G-F (3) | G está en un grupo, F no: agrego F | (H, G, F) (B, E, D) |

**Con estas cuatro iteraciones se responde el ejercicio:** dos grupos, (H, G, F) y (B, E, D), con A y C sueltos. Es la opción **(a)**.

## Cómo sigue (para completar el árbol)

| Iteración | Arista | Qué pasa | Grupos después |
|---|---|---|---|
| 5 | B-C (4) | B está en un grupo, C no: agrego C | (H, G, F) (B, E, D, C) |
| - | H-F (4) | H y F ya están en el mismo grupo: **salteo** | sin cambios |
| 6 | A-C (5) | C está en un grupo, A no: agrego A | (H, G, F) (B, E, D, C, A) |
| 7 | D-G (6) | D está en un grupo y G en otro: **uno los grupos** | (H, G, F, B, E, D, C, A) |

Con 7 aristas aceptadas (V - 1 con 8 vértices) se termina. Las que quedan (D-F, E-F, C-H, C-D, A-B) formarían ciclos.

**Árbol final:** H-G, B-E, B-D, G-F, B-C, A-C, D-G.

**Peso total:** 1 + 2 + 3 + 3 + 4 + 5 + 6 = **24**

## Controles

- Antes de decidir, buscá cada letra en **todos** los grupos, no solo en el primero.
- Los empates (B-D y G-F, B-C y H-F) se pueden tomar en cualquier orden.
- H-F se saltea sin sumar iteración, pero hay que mirarla para saber que cierra un ciclo.








# Ejercicio 6.9: respuesta (a)

## Método

Kruskal ordena las aristas por peso de menor a mayor. Va agregando cada una **solo si no forma un ciclo** (es decir, si une dos componentes distintas). Se detiene al tener V - 1 aristas.

**Paso 1: aristas del grafo, ordenadas por peso**

|Peso|Aristas|
|---|---|
|1|H-G|
|2|B-E|
|3|B-D, G-F|
|4|B-C, H-F|
|5|A-C|
|6|D-G|
|7|D-F, E-F|
|8|C-H|
|9|C-D|
|10|A-B|

**Paso 2: cuatro iteraciones**

|Iteración|Arista|¿Forma ciclo?|Componentes después|
|---|---|---|---|
|1|H-G (1)|No|{H,G}|
|2|B-E (2)|No|{B,E}|
|3|B-D (3)|No|{B,E,D}|
|4|G-F (3)|No|{H,G,F}|

Hay dos aristas de peso 3, así que el orden entre ellas no importa: después de cuatro iteraciones las dos están incluidas.

**Estado final:**

- Componente 1: **H-G, G-F**
- Componente 2: **B-D, B-E**
- **A** y **C** siguen aislados.

## Qué opción es

La que muestra exactamente esas cuatro aristas, con A y C sueltos, es la **(a)**.

Las otras no coinciden:

- **(b) y (c)** incluyen A-C (peso 5), que todavía no se agregó en la iteración 4. En (b) además faltan aristas del lado H-G-F.
- **(d)** tiene las mismas aristas que (a), pero no dibuja los vértices A y C. En la figura del árbol deben aparecer todos los vértices, aunque estén aislados, así que se descarta.

## Para continuar

Las siguientes aristas serían **B-C (4)**, que une las dos componentes mayores con C, y **H-F (4)**, que se descartaría por formar ciclo en {H,G,F}. Después entraría **A-C (5)**.

## Atajo para el examen

1. Anotá las aristas ordenadas por peso.
2. Tomá las primeras 4 que no formen ciclo. Como se piden pocas iteraciones, casi siempre alcanza con las de peso 1, 2 y 3.
3. Compará con las opciones fijándote en qué aristas están presentes y en cuáles faltan.



# Kruskal paso a paso (ejercicio 6.9)

**Regla:** tomo las aristas de menor a mayor peso. Cada una se conecta **solo si une dos grupos distintos**. Si sus dos extremos ya están en el mismo grupo, se descarta porque cerraría un ciclo. El grafo tiene 8 vértices, así que el árbol termina con **7 aristas**.

**Aristas ordenadas:** H-G (1), B-E (2), B-D (3), G-F (3), B-C (4), H-F (4), A-C (5), D-G (6), D-F (7), E-F (7), C-H (8), C-D (9), A-B (10).

## Construcción

Al inicio cada vértice es su propio grupo: {A} {B} {C} {D} {E} {F} {G} {H}

|Paso|Arista|Grupos de los extremos|Decisión|Grupos después|
|---|---|---|---|---|
|1|H-G (1)|{H} y {G}, distintos|**Se agrega**|{H,G}|
|2|B-E (2)|{B} y {E}, distintos|**Se agrega**|{B,E}|
|3|B-D (3)|{B,E} y {D}, distintos|**Se agrega**|{B,E,D}|
|4|G-F (3)|{H,G} y {F}, distintos|**Se agrega**|{H,G,F}|
|5|B-C (4)|{B,E,D} y {C}, distintos|**Se agrega**|{B,E,D,C}|
|6|H-F (4)|H y F están en {H,G,F}|**Se descarta (ciclo H-G-F)**|sin cambios|
|7|A-C (5)|{A} y {B,E,D,C}, distintos|**Se agrega**|{A,B,C,D,E}|
|8|D-G (6)|{A,B,C,D,E} y {H,G,F}, distintos|**Se agrega**|todos en un grupo|

Con la 8.ª arista ya hay 7 aristas aceptadas, así que **se termina**. Las demás (D-F, E-F, C-H, C-D, A-B) formarían ciclos.

## Cómo se ve el grafo en cada momento

**Después del paso 4** (el que pide el ejercicio):

```
H — G — F        B — D        A     C
                 |
                 E
```

**Después del paso 5:**

```
H — G — F        C — B — D        A
                      |
                      E
```

**Después del paso 7:**

```
H — G — F        A — C — B — D
                          |
                          E
```

**Árbol final (paso 8):**

```
A — C — B — E
        |
        D — G — H
            |
            F
```

**Peso total:** 1 + 2 + 3 + 3 + 4 + 5 + 6 = **24**

## Cómo detectar un ciclo rápido

Antes de agregar una arista, fijate si sus dos extremos **ya están conectados** por lo que dibujaste. En el paso 6, H y F ya estaban unidos a través de G (H-G y G-F), así que H-F sobraba.

## Detalle con empates

H-F (4) y B-C (4) tienen el mismo peso. Si hubieras tomado primero H-F, también se habría descartado, así que el árbol final no cambia. Lo mismo pasa con G-F y B-D (3). Con empates, el orden puede cambiar qué arista se acepta solo cuando dos de ellas compiten por cerrar el mismo ciclo, y acá no ocurre.


![[Pasted image 20261108201913.png]]


# Ejercicio: BFS y A* sobre la grilla

## Lectura del grafo

Los vértices están en una grilla de 4×4, y solo hay arista donde hay línea dibujada:

```
A — B — C   D
    |   |   |
E — F   G — H
|       |
I — J — K — L
|       |   |
M — N   O   P
```

Lista de adyacencia, en orden alfabético:

```
A: B          I: E, M, J → (E, J, M)
B: A, C, F    J: I, K
C: B, G       K: G, J, L, O
D: H          L: K, P
E: F, I       M: I, N
F: B, E       N: M
G: C, H, K    O: K
H: D, G       P: L
```

Verificación: hay 16 líneas en el dibujo y la suma de vecinos da 32, el doble.

## a. BFS desde A

|Se saca|Se encolan|Cola|
|---|---|---|
|A|B|[B]|
|B|C, F|[C, F]|
|C|G|[F, G]|
|F|E|[G, E]|
|G|H, K|[E, H, K]|
|E|I|[H, K, I]|
|H|D|[K, I, D]|
|K|J, L, O|[I, D, J, L, O]|
|I|M|[D, J, L, O, M]|
|D|nada|[J, L, O, M]|
|J|nada|[L, O, M]|
|L|P|[O, M, P]|
|O|nada|[M, P]|
|M|N|[P, N]|
|P|nada|[N]|
|N|nada|[]|

**Recorrido BFS: A, B, C, F, G, E, H, K, I, D, J, L, O, M, P, N**

Verificación por niveles:

- Nivel 0: A
- Nivel 1: B
- Nivel 2: C, F
- Nivel 3: G, E
- Nivel 4: H, K, I
- Nivel 5: D, J, L, O, M
- Nivel 6: P, N

## b. A* de A a P con distancia Manhattan

**Datos:**

- Cada arista cuesta 1, así que `g` es la cantidad de pasos desde A.
- Coordenadas `(columna, fila)`: A(0,0), B(1,0), C(2,0), D(3,0), E(0,1)... hasta P(3,3).
- Heurística `h(n) = |x - 3| + |y - 3|`, la distancia Manhattan a P.
- `f = g + h`. Siempre se expande el nodo abierto con menor `f`, y en empate el de menor orden alfabético.

**Valores de h:**

|A|B|C|D|E|F|G|H|
|---|---|---|---|---|---|---|---|
|6|5|4|3|5|4|3|2|

|I|J|K|L|M|N|O|P|
|---|---|---|---|---|---|---|---|
|4|3|2|1|3|2|1|0|

**Seguimiento:**

|Paso|Se expande|Se agregan a abiertos (g, f)|Abiertos después (f)|
|---|---|---|---|
|1|A (g=0, f=6)|B (1, 6)|B6|
|2|B (f=6)|C (2, 6), F (2, 6)|C6, F6|
|3|C (empate con F, gana C)|G (3, 6)|F6, G6|
|4|F (empate con G, gana F)|E (3, 8)|G6, E8|
|5|G (f=6)|H (4, 6), K (4, 6)|E8, H6, K6|
|6|H (empate con K, gana H)|D (5, 8)|E8, K6, D8|
|7|K (f=6)|J (5, 8), L (5, 6), O (5, 6)|E8, D8, J8, L6, O6|
|8|L (empate con O, gana L)|P (6, 6)|E8, D8, J8, O6, P6|
|9|O (empate con P, gana O por orden alfabético)|nada nuevo (K ya cerrado)|E8, D8, J8, P6|
|10|P (f=6)|**destino alcanzado**||

**Orden de expansión: A, B, C, F, G, H, K, L, O, P**

**Camino encontrado: A → B → C → G → K → L → P**, de costo **6**.

Se reconstruye siguiendo los padres hacia atrás: P viene de L, L de K, K de G, G de C, C de B y B de A.

## Observaciones

- **El camino es óptimo.** La heurística Manhattan es admisible (nunca sobreestima), y 6 es la distancia mínima de A a P.
- **El empate entre O y P** se resuelve con el orden alfabético que pide la nota: O se expande antes. No cambia el resultado, porque O es un callejón sin salida. Si expandieras P primero, el camino sería el mismo, pero te ahorrarías un paso en el seguimiento.
- **Nodos que A* nunca expandió:** E, D, J (quedaron en abiertos con f=8) e I, M, N (nunca se generaron). La heurística evitó explorar la zona de la izquierda, a diferencia del BFS, que recorrió todo el grafo.


![[Pasted image 20261108203208.png]]


# Prim en papel con tabla (estilo Dijkstra)

## Reglas

1. Cada vértice tiene un valor: el **peso de la arista más barata** que lo une al grupo. Al inicio es ∞, y el vértice de partida vale 0.
2. Elijo el vértice **no visitado con menor valor** y lo sumo al grupo.
3. Miro sus vecinos no visitados: si el **peso de la arista** (no la suma acumulada) es menor que el valor que tienen, lo reemplazo y anoto de quién vino (padre).
4. Repito hasta visitar todos. Las aristas del árbol son (padre, vértice).

## Diferencia con Dijkstra

| | Dijkstra | Prim |
|---|---|---|
| Valor de un vecino | distancia del vértice + peso de la arista | **solo el peso de la arista** |
| Qué busca | camino mínimo desde el origen | árbol de expansión mínima |

## 6.11 desde E

Vector en el orden [A, B, C, D, E, F, G, H]:

| Paso | Visito (valor) | Qué calculo | Vector después |
|---|---|---|---|
| inicio | | | [∞, ∞, ∞, ∞, 0, ∞, ∞, ∞] |
| 1 | **E (0)** | B = 2, F = 7 | [∞, 2, ∞, ∞, 0, 7, ∞, ∞] |
| 2 | **B (2)** | A = 10, C = 4, D = 3 | [10, 2, 4, 3, 0, 7, ∞, ∞] |
| 3 | **D (3)** | G = 6, C por D = 9 (no mejora), F por D = 7 (igual) | [10, 2, 4, 3, 0, 7, 6, ∞] |
| 4 | **C (4)** | A = 5 (mejora 10), H = 8 | [5, 2, 4, 3, 0, 7, 6, 8] |
| 5 | **A (5)** | sin vecinos nuevos | sin cambios |
| 6 | **G (6)** | H = 1 (mejora 8), F = 3 (mejora 7) | [5, 2, 4, 3, 0, 3, 6, 1] |
| 7 | **H (1)** | F por H = 4 (no mejora 3) | sin cambios |
| 8 | **F (3)** | | fin |

## Padres (de dónde vino cada valor final)

| Vértice | Valor | Padre |
|---|---|---|
| B | 2 | E |
| D | 3 | B |
| C | 4 | B |
| A | 5 | C |
| G | 6 | D |
| H | 1 | G |
| F | 3 | G |

**Aristas del árbol:** E-B, B-D, B-C, C-A, D-G, G-H, G-F

**Peso total:** 2 + 3 + 4 + 5 + 6 + 1 + 3 = **24**

## Respuesta del ejercicio (cuatro iteraciones)

Las primeras cuatro aristas agregadas son **E-B, B-D, B-C y C-A**, que es la opción **(ii)**.

## Controles

- El peso total tiene que dar **24**, igual que el Kruskal del 6.9 (el árbol mínimo es el mismo).
- Hay **7 aristas** (V - 1 con 8 vértices), una por cada vértice menos el inicial.
- En el paso 6, F baja de 7 a 3 porque la arista G-F (3) es más barata que E-F (7): se reemplaza aunque F ya tuviera un valor.
- Si por costumbre de Dijkstra sumás el acumulado, te sale mal. Acá H vale 1 (arista G-H), no 7.



# Ejercicio 6.11

El grafo es el mismo del 6.9. Las aristas son: A-C 5, A-B 10, B-C 4, B-D 3, B-E 2, C-D 9, C-H 8, D-G 6, D-F 7, E-F 7, H-G 1, H-F 4, G-F 3.

## a. Prim desde E, cuatro iteraciones

**Método:** Prim hace crecer **un solo árbol** a partir del vértice inicial. En cada paso se mira **todas las aristas que salen del árbol hacia un vértice que todavía no está**, y se agrega la de menor peso. A diferencia de Kruskal, el árbol siempre es una sola componente conexa.

|Iteración|Árbol antes|Aristas candidatas|Se agrega|Árbol después|
|---|---|---|---|---|
|1|{E}|E-B 2, E-F 7|**E-B (2)**|{E, B}|
|2|{E, B}|B-D 3, B-C 4, E-F 7, B-A 10|**B-D (3)**|{E, B, D}|
|3|{E, B, D}|B-C 4, D-G 6, D-F 7, E-F 7, D-C 9, B-A 10|**B-C (4)**|{E, B, D, C}|
|4|{E, B, D, C}|C-A 5, D-G 6, D-F 7, E-F 7, C-H 8|**C-A (5)**|{E, B, D, C, A}|

Después de cuatro iteraciones el árbol tiene las aristas **E-B, B-D, B-C y A-C**:

```
A — C — B — D
        |
        E
```

Los vértices F, G y H todavía no están conectados.

**Respuesta: la opción (ii)**, que es la que muestra A-C, C-B, B-D y B-E.

**Diferencia con Kruskal (ejercicio 6.9):** Kruskal, con las mismas cuatro iteraciones, elegía H-G, B-E, B-D y G-F, que forman **dos grupos separados**. Prim desde E construye un solo grupo. Por eso la opción (i), que era la respuesta de Kruskal, acá se descarta. La (iii) tampoco sirve porque no conecta C con B, que Prim agrega en la tercera iteración.

## b. Dijkstra desde A: orden de visita

**Método:** se mantiene la distancia mínima conocida a cada vértice. En cada paso se **visita el vértice no visitado con menor distancia** y se actualiza la de sus vecinos si se mejora pasando por él.

|Paso|Se visita (dist.)|Actualizaciones|
|---|---|---|
|1|**A (0)**|C = 5, B = 10|
|2|**C (5)**|B = 9 (por C, mejora 10), H = 13, D = 14|
|3|**B (9)**|E = 11, D = 12 (por B, mejora 14)|
|4|**E (11)**|F = 18|
|5|**D (12)**|G = 18, F sigue en 18 (por D sería 19)|
|6|**H (13)**|G = 14 (mejora 18), F = 17 (mejora 18)|
|7|**G (14)**|F = 17 (por G también es 17, no cambia)|
|8|**F (17)**|fin|

**Orden de visita: A, C, B, E, D, H, G, F**

Distancias finales desde A: A 0, C 5, B 9, E 11, D 12, H 13, G 14, F 17.

## Atajo para el examen

1. **Prim:** en cada paso, listá las aristas que **salen** del conjunto ya armado y tomá la menor.
2. **Dijkstra:** anotá la distancia acumulada de cada vértice y recordá que **se suma el recorrido desde el origen**, no solo el peso de la última arista. Por eso H (13) se visita antes que D... no, D (12) va antes que H (13): se ordena siempre por distancia acumulada.
3. **Cuidado con los parecidos:** Prim compara pesos de aristas sueltas, y Dijkstra compara distancias acumuladas desde el origen.



# 6.11 Prim y Dijkstra

Aristas: A-C 5, A-B 10, B-C 4, B-D 3, B-E 2, C-D 9, C-H 8, D-G 6, D-F 7, E-F 7, H-G 1, H-F 4, G-F 3.

**Convención:** `-` = todavía no llegué a ese vértice.

## a. Prim desde E (valor por arista)

**Regla:** el valor de un vecino es **solo el peso de la arista** que lo une al grupo, sin sumar lo acumulado. Elijo el no visitado de menor valor.

| Paso | Visito (valor) | Qué calculo | A | B | C | D | E | F | G | H |
|---|---|---|---|---|---|---|---|---|---|---|
| inicio | | | - | - | - | - | 0 | - | - | - |
| 1 | **E (0)** | B = 2, F = 7 | - | 2 | - | - | 0 | 7 | - | - |
| 2 | **B (2)** | A = 10, C = 4, D = 3 | 10 | 2 | 4 | 3 | 0 | 7 | - | - |
| 3 | **D (3)** | G = 6; C por D = 9 (no mejora), F por D = 7 (igual) | 10 | 2 | 4 | 3 | 0 | 7 | 6 | - |
| 4 | **C (4)** | A = 5 (mejora 10), H = 8 | 5 | 2 | 4 | 3 | 0 | 7 | 6 | 8 |
| 5 | **A (5)** | sin vecinos nuevos | 5 | 2 | 4 | 3 | 0 | 7 | 6 | 8 |
| 6 | **G (6)** | H = 1 (mejora 8), F = 3 (mejora 7) | 5 | 2 | 4 | 3 | 0 | 3 | 6 | 1 |
| 7 | **H (1)** | F por H = 4 (no mejora 3) | 5 | 2 | 4 | 3 | 0 | 3 | 6 | 1 |
| 8 | **F (3)** | fin | 5 | 2 | 4 | 3 | 0 | 3 | 6 | 1 |

### Padres (de dónde vino cada valor final)

| Vértice | Valor | Padre |
|---|---|---|
| B | 2 | E |
| D | 3 | B |
| C | 4 | B |
| A | 5 | C |
| G | 6 | D |
| H | 1 | G |
| F | 3 | G |

**Aristas del árbol:** E-B, B-D, B-C, C-A, D-G, G-H, G-F (peso total 24)

### Respuesta (cuatro iteraciones)

Los primeros cuatro vértices que se suman son B, D, C y A, o sea las aristas **E-B, B-D, B-C y C-A**. Es la opción **(ii)**.

## b. Dijkstra desde A (valor acumulado)

**Regla:** el valor de un vecino es **distancia del vértice visitado + peso de la arista**. Elijo el no visitado de menor distancia.

| Paso | Visito (dist.) | Qué calculo | A | B | C | D | E | F | G | H |
|---|---|---|---|---|---|---|---|---|---|---|
| inicio | | | 0 | - | - | - | - | - | - | - |
| 1 | **A (0)** | B = 10, C = 5 | 0 | 10 | 5 | - | - | - | - | - |
| 2 | **C (5)** | B = 5+4 = 9 (mejora 10), D = 5+9 = 14, H = 5+8 = 13 | 0 | 9 | 5 | 14 | - | - | - | 13 |
| 3 | **B (9)** | D = 9+3 = 12 (mejora 14), E = 9+2 = 11 | 0 | 9 | 5 | 12 | 11 | - | - | 13 |
| 4 | **E (11)** | F = 11+7 = 18 | 0 | 9 | 5 | 12 | 11 | 18 | - | 13 |
| 5 | **D (12)** | G = 12+6 = 18; F por D = 19 (no mejora) | 0 | 9 | 5 | 12 | 11 | 18 | 18 | 13 |
| 6 | **H (13)** | G = 13+1 = 14 (mejora 18), F = 13+4 = 17 (mejora 18) | 0 | 9 | 5 | 12 | 11 | 17 | 14 | 13 |
| 7 | **G (14)** | F por G = 14+3 = 17 (igual, no cambia) | 0 | 9 | 5 | 12 | 11 | 17 | 14 | 13 |
| 8 | **F (17)** | fin | 0 | 9 | 5 | 12 | 11 | 17 | 14 | 13 |

**Orden de visita: A, C, B, E, D, H, G, F**

## Diferencia entre las dos tablas

| | Prim | Dijkstra |
|---|---|---|
| Valor de un vecino | solo el peso de la arista | distancia acumulada + peso de la arista |
| Ejemplo: H al visitar G | 1 (arista G-H) | 14 + 1... ya valía 13 por C, y G queda en 14 gracias a H |
| Qué obtengo | árbol de expansión mínima | camino mínimo desde A |
| Qué se anota | padres → aristas del árbol | orden de visita y distancias |

## Controles

- **Prim:** el peso total da 24 y hay 7 aristas (V - 1).
- **Dijkstra:** el orden se decide por distancia acumulada, por eso D (12) se visita antes que H (13).
- Si en Prim sumás el acumulado, te sale mal: H vale 1, no 14.



![[Pasted image 20261108203302.png]]


# Ejercicio 6.12

En el dibujo hay **dos nodos rotulados H**. El de la derecha, conectado a E (8) y a J (2), seguramente es **G** y es un error de tipeo del enunciado. Lo llamo **G**; el H del medio es el que conecta con D, E, F e I.

## Lectura del grafo

Aristas: A-B 6, A-C 5, A-D 3, B-E 7, C-D 4, D-E 1, D-F 2, D-H 10, E-H 5, E-G 8, F-H 3, F-I 6, H-I 1, G-J 2.

Lista de adyacencia en orden alfabético:

```
A: B, C, D       F: D, H, I
B: A, E          G: E, J
C: A, D          H: D, E, F, I
D: A, C, E, F, H I: F, H
E: B, D, G, H    J: G
```

Verificación: 14 líneas en el dibujo y la suma de vecinos da 28, el doble.

## a. DFS desde A

En cada nodo voy al primer vecino no visitado. Si no hay, retrocedo.

|Estoy en|Voy a|Nota|
|---|---|---|
|A|B||
|B|E|A ya visitado|
|E|D|B ya visitado, D es el menor pendiente|
|D|C|A ya visitado|
|C||sin pendientes, retrocedo a D|
|D|F|E ya visitado, C ya visitado|
|F|H|D ya visitado|
|H|I|D, E, F ya visitados|
|I||sin pendientes, retrocedo a H, F, D, E|
|E|G|quedaba G pendiente|
|G|J||
|J||fin|

**Recorrido DFS: A, B, E, D, C, F, H, I, G, J**

Los 10 nodos aparecen sin repetir. Lo más fácil de olvidar es volver a E después de recorrer toda la zona de D, porque G quedaba pendiente.

## b. Prim desde A

En cada paso miro **todas las aristas que salen del árbol** hacia un vértice nuevo y tomo la de menor peso.

|Paso|Árbol antes|Candidatas que salen|Se agrega|
|---|---|---|---|
|1|{A}|A-D 3, A-C 5, A-B 6|**(A, D)** 3|
|2|{A, D}|D-E 1, D-F 2, D-C 4, A-C 5, A-B 6, D-H 10|**(D, E)** 1|
|3|{A, D, E}|D-F 2, D-C 4, E-H 5, A-B 6, E-B 7, E-G 8|**(D, F)** 2|
|4|{A, D, E, F}|F-H 3, D-C 4, A-B 6, F-I 6, E-B 7, E-G 8|**(F, H)** 3|
|5|{A, D, E, F, H}|H-I 1, D-C 4, A-B 6, F-I 6, E-B 7, E-G 8|**(H, I)** 1|
|6|{A, D, E, F, H, I}|D-C 4, A-B 6, E-B 7, E-G 8|**(D, C)** 4|
|7|+ C|A-B 6, E-B 7, E-G 8|**(A, B)** 6|
|8|+ B|E-G 8|**(E, G)** 8|
|9|+ G|G-J 2|**(G, J)** 2|

**Árbol de expansión mínima, en orden de visita:**

**(A, D), (D, E), (D, F), (F, H), (H, I), (D, C), (A, B), (E, G), (G, J)**

Son 9 aristas, o sea V - 1 con 10 vértices, como corresponde. **Peso total:** 3 + 1 + 2 + 3 + 1 + 4 + 6 + 8 + 2 = **30**.

## Para no fallar

1. **Escribí cada tupla como (vértice que ya estaba, vértice nuevo)**, porque el enunciado pide el orden en que fueron visitadas.
2. **Las candidatas cambian en cada paso.** Cuando un vértice entra al árbol, sus aristas hacia nodos que ya están dejan de ser candidatas. Por eso E-H 5 desaparece en el paso 5.
3. **Una arista chica puede quedar esperando.** En el paso 2 la mejor es D-E 1, pero A-C 5 y A-B 6 ya estaban disponibles y se usan recién más tarde.


![[Pasted image 20261108203446.png]]


# Ejercicio 6.13

## Lectura del grafo

Aristas (16): A-B 2, A-C 9, A-D 1, B-E 3, B-H 6, C-D 6, C-F 2, D-G 8, D-H 7, E-H 5, E-I 4, F-G 4, G-H 1, H-I 2, H-K 10, J-K 8.

Hay 11 vértices, así que el árbol de expansión mínima tiene **10 aristas**.

## a. Kruskal

Aristas ordenadas por peso: A-D 1, G-H 1, A-B 2, C-F 2, H-I 2, B-E 3, E-I 4, F-G 4, E-H 5, B-H 6, C-D 6, D-H 7, D-G 8, J-K 8, A-C 9, H-K 10.

|Arista|Grupos de los extremos|Decisión|Grupos después|
|---|---|---|---|
|A-D (1)|distintos|**Se agrega**|{A,D}|
|G-H (1)|distintos|**Se agrega**|{G,H}|
|A-B (2)|distintos|**Se agrega**|{A,B,D}|
|C-F (2)|distintos|**Se agrega**|{C,F}|
|H-I (2)|distintos|**Se agrega**|{G,H,I}|
|B-E (3)|distintos|**Se agrega**|{A,B,D,E}|
|E-I (4)|{A,B,D,E} y {G,H,I}|**Se agrega**|{A,B,D,E,G,H,I}|
|F-G (4)|{C,F} y el grupo grande|**Se agrega**|{A,B,C,D,E,F,G,H,I}|
|E-H (5)|ya están juntos|Se descarta (ciclo)||
|B-H (6), C-D (6), D-H (7), D-G (8)|ya están juntos|Se descartan (ciclo)||
|J-K (8)|{J} y {K}|**Se agrega**|{J,K}|
|A-C (9)|ya están juntos|Se descarta (ciclo)||
|H-K (10)|{J,K} y el grupo grande|**Se agrega**|todos juntos|

**Árbol de expansión mínima, en orden de generación:**

**(A, D), (G, H), (A, B), (C, F), (H, I), (B, E), (E, I), (F, G), (J, K), (H, K)**

Son 10 aristas, o sea V - 1. **Peso total:** 1 + 1 + 2 + 2 + 2 + 3 + 4 + 4 + 8 + 10 = **37**.

Los empates (A-D con G-H, y A-B, C-F y H-I entre sí) se pueden tomar en cualquier orden, porque ninguno compite con otro por cerrar el mismo ciclo. La nota del enunciado lo permite.

## b. Dijkstra de A a J

Interpreto "el grafo del ejercicio 1" como el grafo de este mismo ejercicio. Los vectores van en el orden **[A, B, C, D, E, F, G, H, I, J, K]**, con ∞ para lo no alcanzado.

|Paso|Se visita (dist.)|Vector de distancias después|
|---|---|---|
|inicio||[0, ∞, ∞, ∞, ∞, ∞, ∞, ∞, ∞, ∞, ∞]|
|1|**A (0)**|[0, 2, 9, 1, ∞, ∞, ∞, ∞, ∞, ∞, ∞]|
|2|**D (1)**|[0, 2, 7, 1, ∞, ∞, 9, 8, ∞, ∞, ∞]|
|3|**B (2)**|[0, 2, 7, 1, 5, ∞, 9, 8, ∞, ∞, ∞]|
|4|**E (5)**|[0, 2, 7, 1, 5, ∞, 9, 8, 9, ∞, ∞]|
|5|**C (7)**|[0, 2, 7, 1, 5, 9, 9, 8, 9, ∞, ∞]|
|6|**H (8)**|[0, 2, 7, 1, 5, 9, 9, 8, 9, ∞, 18]|
|7|**F (9)**|sin cambios|
|8|**G (9)**|sin cambios|
|9|**I (9)**|sin cambios|
|10|**K (18)**|[0, 2, 7, 1, 5, 9, 9, 8, 9, **26**, 18]|
|11|**J (26)**|destino alcanzado|

Detalles de las actualizaciones:

- **Paso 2:** C baja de 9 a 7 pasando por D (1 + 6), y D da G = 1 + 8 = 9 y H = 1 + 7 = 8.
- **Paso 3:** B daría H = 2 + 6 = 8, igual que el valor actual, así que no cambia.
- **Paso 4:** E daría H = 5 + 5 = 10 (no mejora) e I = 5 + 4 = 9.
- **Paso 6:** H da K = 8 + 10 = 18. G e I por H también darían 9, sin mejora.
- **Pasos 7 a 9:** F, G e I empatan en 9 y se visitan en orden alfabético. No mejoran a nadie.

**Distancia mínima de A a J: 26.**

**Camino:** A → D → H → K → J, con costo 1 + 7 + 10 + 8 = 26. También sirve A → B → H → K → J, que cuesta 2 + 6 + 10 + 8 = 26. Hay dos caminos óptimos porque H se alcanza con 8 por D y por B.

**Orden de visita:** A, D, B, E, C, H, F, G, I, K, J.

## Atajo para el examen

1. **Kruskal:** anotá las aristas ordenadas y, antes de agregar cada una, chequeá si sus extremos ya están conectados por lo dibujado.
2. **Dijkstra:** en cada fila actualizá solo los vecinos del vértice recién visitado. Recordá que el vector se arma con la distancia acumulada, no con el peso de la última arista.

![[Pasted image 20261108204204.png]]


# Ejercicio 6.14

Filas y columnas en orden A, B, C, D, E, F. La matriz es **simétrica** (`M[i][j] = M[j][i]`), así que el grafo es no dirigido. Un 0 significa que no hay arista.

## a. Representación gráfica

Leyendo la mitad superior de la matriz, las aristas son (10 en total):

|Arista|Peso|Arista|Peso|
|---|---|---|---|
|A-B|7|C-D|4|
|A-C|3|C-F|3|
|A-D|5|D-F|2|
|B-C|1|E-F|8|
|B-E|9|B-F|6|

Lista de adyacencia:

```
A: B7, C3, D5
B: A7, C1, E9, F6
C: A3, B1, D4, F3
D: A5, C4, F2
E: B9, F8
F: B6, C3, D2, E8
```

Dibujo aproximado:

```
        7
   A ───────── B ─────── 9 ─────── E
   │ ╲         │ ╲                 │
   │   5       1   6               8
   3     ╲     │     ╲             │
   │       D   │       F ──────────┘
   C ──4───┘   │      ╱│
   │ ╲_________│     ╱ 2 (hacia D)
   └──────3────────╱
```

Si el dibujo te confunde, dibujá los 6 círculos y uní los pares de la tabla de aristas, que es lo que importa.

## b. Kruskal (AEM)

Con 6 vértices, el árbol tiene **5 aristas**.

**Aristas ordenadas:** B-C 1, D-F 2, A-C 3, C-F 3, C-D 4, A-D 5, B-F 6, A-B 7, E-F 8, B-E 9.

### Dos pasos en detalle

**Paso 1: B-C (1).** Al inicio cada vértice es su propio grupo: {A} {B} {C} {D} {E} {F}. B y C están en grupos distintos, así que unirlos no forma ciclo. **Se agrega.** Grupos: {B,C} {A} {D} {E} {F}.

**Paso 2: D-F (2).** D y F están en grupos distintos ({D} y {F}). **Se agrega.** Grupos: {B,C} {D,F} {A} {E}.

### Simplificado hasta la solución

|Arista|¿Mismo grupo?|Decisión|Grupos|
|---|---|---|---|
|B-C (1)|No|**Se agrega**|{B,C}|
|D-F (2)|No|**Se agrega**|{D,F}|
|A-C (3)|No|**Se agrega**|{A,B,C}|
|C-F (3)|No|**Se agrega**|{A,B,C,D,F}|
|C-D (4), A-D (5), B-F (6), A-B (7)|Sí|Se descartan (ciclo)||
|E-F (8)|No ({E} y el grupo grande)|**Se agrega**|todos|

Con 5 aristas aceptadas se termina (B-E ni se mira).

**AEM: (B, C), (D, F), (A, C), (C, F), (E, F)**

**Peso total:** 1 + 2 + 3 + 3 + 8 = **17**

## c. Dijkstra de A a F

Vector de distancias en el orden **[A, B, C, D, E, F]**.

### Dos pasos en detalle

**Paso 1: se visita A (distancia 0).** Es el origen. Se actualizan sus vecinos con la distancia acumulada: B = 0 + 7 = 7, C = 0 + 3 = 3, D = 0 + 5 = 5. Vector: [0, 7, 3, 5, ∞, ∞].

**Paso 2: se visita C (distancia 3),** que es el menor no visitado. Sus vecinos:

- B: 3 + 1 = 4, mejora el 7, **se actualiza**.
- D: 3 + 4 = 7, no mejora el 5.
- F: 3 + 3 = 6, mejora el ∞, **se actualiza**.

Vector: [0, 4, 3, 5, ∞, 6].

### Simplificado hasta la solución

|Paso|Se visita (dist.)|Vector después|
|---|---|---|
|inicio||[0, ∞, ∞, ∞, ∞, ∞]|
|1|**A (0)**|[0, 7, 3, 5, ∞, ∞]|
|2|**C (3)**|[0, 4, 3, 5, ∞, 6]|
|3|**B (4)**|[0, 4, 3, 5, 13, 6] (E = 4 + 9; F por B sería 10, no mejora)|
|4|**D (5)**|sin cambios (F por D sería 7, no mejora)|
|5|**F (6)**|destino alcanzado|

**Distancia mínima de A a F: 6.**

**Camino:** A → C → F, con costo 3 + 3 = 6. Se reconstruye siguiendo los predecesores hacia atrás: F viene de C, y C viene de A.

Los otros caminos son peores: A→D→F cuesta 7, A→B→F cuesta 13 y A→C→D→F cuesta 9.

**Orden de visita:** A, C, B, D, F.


![[Pasted image 20261108204227.png]]


# Ejercicio 6.15

Filas y columnas en orden A, B, C, D, E, F.

## a. Representación gráfica

**G₁** es simétrica, así que es **no dirigido y con pesos**. Aristas (9):

|Arista|Peso|Arista|Peso|
|---|---|---|---|
|A-B|2|C-D|4|
|A-C|7|C-E|1|
|A-D|3|C-F|9|
|B-D|8|D-E|6|
|E-F|5|||

```
A: B2, C7, D3
B: A2, D8
C: A7, D4, E1, F9
D: A3, B8, C4, E6
E: C1, D6, F5
F: C9, E5
```

**G₂** **no es simétrica**, así que es **dirigido**. `M[i][j] = 1` es una flecha de `i` hacia `j`. Flechas (8):

```
A → E
B → C
D → A, B, C, E
E → F
F → C
```

La fila C está toda en 0, así que C no tiene flechas de salida.

## b. Prim sobre G₁

El enunciado no dice el vértice inicial, así que parto de **A**. El resultado es el mismo desde cualquier inicio si no hay empates entre pesos.

En cada paso tomo la arista más barata que **sale del árbol** hacia un vértice nuevo.

|Paso|Árbol antes|Candidatas|Se agrega|
|---|---|---|---|
|1|{A}|A-B 2, A-D 3, A-C 7|**(A, B)** 2|
|2|{A, B}|A-D 3, A-C 7, B-D 8|**(A, D)** 3|
|3|{A, B, D}|D-C 4, D-E 6, A-C 7|**(D, C)** 4|
|4|{A, B, D, C}|C-E 1, D-E 6, C-F 9|**(C, E)** 1|
|5|{A, B, C, D, E}|E-F 5, C-F 9|**(E, F)** 5|

**AEM: (A, B), (A, D), (D, C), (C, E), (E, F)**

Son 5 aristas, o sea V - 1. **Peso total:** 2 + 3 + 4 + 1 + 5 = **15**.

Aunque C-E (1) es la arista más barata del grafo, no entra primero: recién es candidata cuando C ya está en el árbol.

## c. ¿Orden topológico de G₂?

**Sí se puede.** Un grafo dirigido admite orden topológico si y solo si es un **DAG** (no tiene ciclos dirigidos). Para verificarlo, uso el algoritmo de Kahn: se elige siempre un vértice con **grado de entrada 0**, se lo agrega al orden y se borran sus flechas.

**Grados de entrada iniciales:** A: 1 (de D), B: 1 (de D), C: 3 (de B, D, F), D: 0, E: 2 (de A, D), F: 1 (de E).

|Paso|Se elige|Grados de entrada después|Candidatos (grado 0)|
|---|---|---|---|
|1|**D** (el único con 0)|A 0, B 0, C 2, E 1, F 1|A, B|
|2|**A**|E 0|B, E|
|3|**B**|C 1|E|
|4|**E**|F 0|F|
|5|**F**|C 0|C|
|6|**C**|||

Se pudieron sacar los 6 vértices, así que no hay ciclos.

**Un orden topológico posible: D, A, B, E, F, C**

Se puede comprobar con las flechas: D→A, D→B, D→C, D→E, A→E, B→C, E→F y F→C van siempre de un vértice anterior a uno posterior.

Hay otros órdenes válidos. Por ejemplo, D, B, A, E, F, C también sirve, porque en el paso 2 se podía elegir B antes que A. Si el ejercicio dijera "optar por el menor orden alfabético", el resultado sería el de arriba.

**Si hubiera un ciclo,** el algoritmo se trabaría con vértices pendientes y ninguno con grado de entrada 0, y no existiría orden topológico.