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
Baja: eliminar elementos d e