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