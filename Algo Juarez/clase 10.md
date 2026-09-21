![[Pasted image 20260921003917.png]]

![[Pasted image 20260921004514.png]]

El de arriba seria el tamaño lógico, que es lo que realmente ocupa, mientras que el de abajo es el tamaño físico, que seria el tamaño fijo

# Que es un TDA?

Exactamente. Hay una **interfaz** (lo que ves y usás) y detrás la **implementación** (cómo funciona realmente). El TDA es esa interfaz: el contrato que dice "estas son las operaciones y esto es lo que hacen".

Y en Java se ve literalmente así:



```java
List<String> nombres = new ArrayList<>();
```

- `List` es la interfaz, el "qué se puede hacer".
- `ArrayList` es la implementación, el "cómo se hace por dentro".

Vos escribís tu código contra `List`, y por debajo puede haber un `ArrayList` o un `LinkedList`. Como usás solo los "botones" de `List`, podés cambiar la implementación sin tocar el resto.

Un matiz para que no se te mezcle: "interfaz" acá tiene dos sentidos parecidos. Uno es el concepto general (el conjunto de operaciones que ofrece algo), y otro es la palabra clave `interface` de Java, que es una forma de expresar ese concepto en código. `List` es ambas cosas a la vez, pero el TDA como idea existe aunque no uses la palabra `interface` (por ejemplo, en un pseudocódigo de la facultad).

Con el array no hay esa capa intermedia: trabajás directo con la estructura, sin "botones" en el medio.

![[Pasted image 20260921004805.png]]

Son estructuras lineales ya que siguen una secuencia

![[Pasted image 20260921010030.png]]

![[Pasted image 20260921010424.png]]

Las listas sirven para almacenar datos

Alta: agregar elementos a la lista
Baja: eliminar elementos de la lista
Consulta: consultar elementos de la lista

![[Pasted image 20260921010722.png]]

![[Pasted image 20260921010751.png]]

Falta modificación, pero esta no hace falta mucho ya que es lo mismo que de de baja y de de alta para modificar


# Pila 
Es un tipo de lista con ciertas restricciones
El ultimo que entra es el primero que sale, por lo cual si yo quiero consultar varias cosas lo que hace es consultar el ultimo
Siempre trabaja con el ultimo

![[Pasted image 20260921011407.png]]

Para el alta lo tengo que poner arriba de todo, suponiendo que arriba esta el final

![[Pasted image 20260921012019.png]]

![[Pasted image 20260921012054.png]]

Yo con la consulta lo único que puedo averiguar es el que esta al final de la pila

![[Pasted image 20260921012201.png]]

Con las bajas es lo mismo, ya que voy eliminando primero los del final

![[Pasted image 20260921012256.png]]

Un ejemplo de uso son en las paginas web cuando volvemos para atrás, ya que vamos desapilando.
Podemos decir que estamos apilando cuando empezamos a buscar y profundizar desde el navegador y desapilando cuando estamos volviendo para atrás

Lo mismo en un editor de texto con el Ctrl + Z


## Lo que pasa con ir hacia atrás y hacia adelante

![[Pasted image 20260921013340.png]]

![[Pasted image 20260921013359.png]]

![[Pasted image 20260921013415.png]]

Cada vez que voy hacia atrás lo que hace es desapilar y apilar en otra pila

Cuando voy hacia adelante, tiene que reconstruir la pila, sacando de una y poniéndosela a la otra

![[Pasted image 20260921013633.png]]

![[Pasted image 20260921013638.png]]


### si yo voy desapilando y apilando en otra pila: 

![[Pasted image 20260921013802.png]]

me queda la inversa de la pila original

![[Pasted image 20260921015659.png]]

# Colas

![[Pasted image 20260921013955.png]]

Es como la fila del colectivo, yo llego y me pongo al final, y la gente empieza a subir al colectivo del principio, se empieza a procesar mientras va avanzando, por eso es "baja al principio"

Acá se representan de izquierda a derecha

![[Pasted image 20260921014527.png]]

Van llegando y lo voy poniendo al final

![[Pasted image 20260921014542.png]]

![[Pasted image 20260921014613.png]]

Con la consulta y las bajas siempre se van los primeros

![[Pasted image 20260921014629.png]]

El sentido en la mayoría de casos que se le da a la baja en las colas es el sentido de procesamiento
Por ejemplo si yo hago una cola del supermercado, llego a la caja pago(ósea me proceso) y me voy, una vez que lo procesan lo sacan de la cola

![[Pasted image 20260921014659.png]]

![[Pasted image 20260921014710.png]]

# Listas generales

![[Pasted image 20260921015339.png]]