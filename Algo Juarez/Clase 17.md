![[Pasted image 20261025201624.png]]

![[Pasted image 20261025203456.png]]

Nuestro vertice origen es el 0, se usan 2 matrices una de distancias y otra de visitados

La matriz de distancias guarda la distancia acumulada para llegar a los vertices
En ambos son 6 posiciones porque hay 6 vertices


Me voy fijando los vertices adyacentes, y elijo el camino mas bajo, por eso en la tabla solo aparece el valor de los adyacentes y el resto con signo infinito


De los no visitados me quedo con el mas chico

Aca del 0, veo los adyacentes, me quedo con el 1 que es el que menor costo tiene y me muevo a su lugar, y marco como visitado al 1
Ahora repito lo mismo pero desde el 1, pero para llegar al 3 tengo que sumar lo que me moví mas de donde esto y parado hasta el 3, por eso da 22.
Todo esto porque son distancias acumuladas

Una vez que llego a ver el vertice calculo su acumulada desde mi inicio


Lo que tengo que hacer es por cada vez que me muevo es si el valor que tengo en hacer 2 movimientos es mas chico que hacer un  movimiento, es decir que tenga menos peso, y con esto mi tabla la voy actualizando

Voy descubriendo camino moviéndome adyacentemente y voy actualizando con los nuevos vertices descubiertos mi tabla con los menores valores


![[Pasted image 20261025214344.png]]

aca por ejemplo para llegar al 3 es lo que acumule hasta 4 + la arista hasta 3 que vale 6, en total seria 26, pero como es mayor al dato que tenia lo dejo como esta, siempre tengo que ver las acumuladas




El algoritmo de Dijkstra calcula el camino más corto desde un nodo de origen hacia todos los demás nodos de un grafo mediante el análisis de costos acumulados. Para lograrlo, emplea un arreglo que registra la distancia mínima descubierta hasta el momento y un arreglo booleano para marcar los vértices que ya fueron procesados de manera definitiva.

  

**Dinámica general del algoritmo**

  

- Inicia asignando una distancia de 0 al nodo origen y un valor de infinito al resto, indicando que aún son inalcanzables.
    
      
    
- En cada iteración, selecciona el vértice no visitado que tenga la menor distancia acumulada en su registro.
    
      
    
- Desde el vértice seleccionado, suma su costo acumulado con el peso de la arista hacia cada vértice adyacente.
    
      
    
- Si esta nueva suma es estrictamente menor que el valor almacenado previamente para el nodo destino, la tabla de distancias se actualiza con el nuevo valor óptimo.
    
      
    
- Una vez evaluados todos los vecinos, el vértice de partida se marca como visitado (`t`) para no volver a procesarlo.
    
      
    

**Paso a paso del caso práctico**

  

- **Paso 1:** Se arranca en el nodo 0, actualizando los costos hacia sus vecinos directos: nodo 1 (costo 7), nodo 2 (costo 9) y nodo 5 (costo 14). El nodo 0 se marca como visto (`t`).
    
      
    
- **Paso 2:** El nodo no visitado más cercano es el 1 (distancia 7). Hacia el nodo 2 el costo sería 17 (7+10), que se descarta por existir un camino de 9. Hacia el nodo 3 el costo es 22 (7+15), valor que se registra reemplazando al infinito. Se marca el nodo 1 como visto (`t`).
    
      
    
- **Paso 3:** Se selecciona el nodo 2 (distancia 9). El costo acumulado hacia el nodo 5 pasa a ser 11 (9+2), actualizando el registro anterior de 14. El costo hacia el nodo 3 pasa a ser 20 (9+11), mejorando el registro anterior de 22. Se marca el nodo 2 como visto (`t`).
    
      
    
- **Paso 4:** El siguiente nodo más cercano es el 5 (distancia actualizada a 11). Desde aquí se alcanza el nodo 4 con un costo acumulado de 20 (11+9), reemplazando el valor infinito. Se marca el nodo 5 como visto (`t`).
    
      
    
- **Paso 5:** Existen dos nodos con la misma distancia mínima de 20 (nodos 3 y 4), seleccionándose el nodo 4. El camino desde el nodo 4 hacia el 3 resulta en un costo de 26 (20+6). Al ser mayor que el costo ya registrado (20), se ignora y se marca el nodo 4 como visto (`t`).
    
      
    
- **Paso 6:** Queda por procesar el nodo 3 (distancia 20). Al no tener rutas salientes hacia vértices no visitados, no se generan actualizaciones. El nodo 3 se marca como visto (`t`), finalizando la ejecución al tener todos los vértices en estado `t`.

Exactamente, siempre partís del costo que ya acumulaste hasta el vértice donde estás parado. Al ubicarte en el nodo 2, tu tabla indica que la distancia acumulada desde el origen es 9. Desde allí, observás la arista que conecta con el nodo 3, la cual tiene un peso o costo de 11. Calculás la nueva ruta potencial sumando tu acumulado de 9 más el costo de la arista de 11, resultando en un total de 20. En el paso anterior, tu tabla había registrado un costo de 22 para el nodo 3 (al evaluarlo desde el nodo 1), por lo que comparás ambos valores. Como la nueva suma de 20 es estrictamente menor que el 22 que ya tenías, encontraste un camino más eficiente y actualizás la matriz de distancias reemplazando el 22 por el nuevo valor de 20.



![[Pasted image 20261025215700.png]]

![[Pasted image 20261025222306.png]]

![[Pasted image 20261025222345.png]]


![[Pasted image 20261025222716.png]]

![[Pasted image 20261025223612.png]]


![[Pasted image 20261025224326.png]]

Marco el vertice que estoy evaluando con amarillo

Sigo con el concepto de adyacencia, por lo cual de A a D o E es infinito
Con adyacencia completo la tabla de distancias para cada uno 

![[Pasted image 20261025234105.png]]

Empiezo por el 1, ya que seria mi primer elemento, la diagonal y lo amarillo no cuenta, lo que tengo que hacer es una rectángulo de donde esta, lo estiro para la izquierda y para la derecha, si la suma de las esquinas opuestas es menor lo reemplazo, si es mayor o igual lo dejo como esta

Por ejemplo: aca en 1 agarro y hago el rectángulo, sumo los opuestos, osea 8+4, como es mayor dejo el 1

sigo con el 2, trazo el rectángulo, hago 4+infinito < infinito?, no, es igual, lo dejo como esta, el infinito también, lo dejo como esta ya que da el mismo resultado que el 2

sigo con la fila de abajo, agarro el infinito y hago su rectángulo,  8+4 < infinito? si, entonces reemplazo el 12 por mi infinito, lo mismo que se ve en el cuadro de primera iteración de la derecha

Tengo que sumar los extremos en amarillo con un rectangulo

![[Pasted image 20261025234630.png]]

![[Pasted image 20261025234652.png]]

![[Pasted image 20261025234726.png]]

En la matriz de recorridos también lo tengo que reemplazar, ya que estoy usando de referencia a A


![[Pasted image 20261026001235.png]]

![[Pasted image 20261026001331.png]]

![[Pasted image 20261026001344.png]]

![[Pasted image 20261026001941.png]]

![[Pasted image 20261026002349.png]]

![[Pasted image 20261026001954.png]]

y al final queda así, arriba tengo lo que me cuesta y abajo tengo que para llegar desde (mi fila) hasta (mi columna) primero tengo que pasar por (lo que contiene la matriz en ij)

![[Pasted image 20261026002557.png]]

si yo quiero llegar de A a E, primero tengo que pasar por C, y para llegar a C tengo que pasar por B, y para llegar a B a B, osea que no paso por nadie mas, seria entonces A -> B -> C -> E

se lee por fila


Para determinar el trayecto óptimo desde el nodo A hasta el nodo E utilizando la matriz final de recorridos (Iteración 4), se debe rastrear la secuencia de nodos leyendo las intersecciones.

  

1. El costo mínimo registrado para ir de A hacia E es 7 (`distancias[A][E] = 7`).
    

2. Al consultar la intersección de la fila A y columna E en la matriz de recorridos, el valor es C (`recorridos[A][E] = C`). Esto indica que para alcanzar E desde A, el nodo intermediario o paso previo requerido es C, estructurando la ruta momentáneamente como A $\to$ ... $\to$ C $\to$ E.
    
3. Para resolver el tramo restante desde A hasta C, se consulta la celda de la fila A y columna C, cuyo valor es B (`recorridos[A][C] = B`). Esto establece que para alcanzar C desde A, se debe pasar por B, actualizando la ruta a A $\to$ ... $\to$ B $\to$ C $\to$ E.
    
4. Al verificar cómo ir desde A hasta B, la celda respectiva indica B (`recorridos[A][B] = B`), lo que confirma que es una conexión directa y el origen del trayecto no requiere más intermediarios.
El camino final reconstruido es A $\to$ B $\to$ C $\to$ E. Tu razonamiento para leer la matriz y encadenar los nodos paso a paso hasta dar con la conexión directa es correcto.



![[Pasted image 20261026003442.png]]

aca si quiero cambiar el 12  que es si quiero ir de C a B, que pasa si hago de C a D y de D a B, sumo los dos caminos, que la suma me da 6, entonces al ser mas chico lo cambio 

![[Pasted image 20261026002903.png]]


![[Pasted image 20261026003809.png]]

Esto es mas por coordenadas, mas usados en los videojuegos para calcular distancias


Heurística, resolver un algoritmo grande por un algoritmo mas chico pero por aproximación

![[Pasted image 20261026004708.png]]

![[Pasted image 20261026004803.png]]

![[Pasted image 20261026004941.png]]