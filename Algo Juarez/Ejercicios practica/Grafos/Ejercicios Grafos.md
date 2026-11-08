
![[Pasted image 20261108195408.png]]


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


![[Pasted image 20261108195708.png]]

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