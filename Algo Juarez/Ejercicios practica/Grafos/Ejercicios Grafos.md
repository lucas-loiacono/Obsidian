
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