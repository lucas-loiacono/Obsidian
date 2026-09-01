![[Pasted image 20260831200425.png]]

![[Pasted image 20260831200441.png]]
Tienen que ser todos los datos del mismo tipo

![[Pasted image 20260831200611.png]]

![[Pasted image 20260831200727.png]]
 
![[Pasted image 20260831200837.png]]
Todo lo que declare con new va a estar en el heap, en java no hace falta borrar la memoria dinamica despues de usarla

![[Pasted image 20260831201532.png]]


la variable esta en el stack (su referencia), pero cuando hago new int me reservo los lugares hacia donde apunta  mi vec, vec apunta a la primera posición donde esta la memoria en el heap

![[Pasted image 20260831201924.png]]

se va moviendo por la cantidad de bytes que es el tipo del vector


![[Pasted image 20260831202222.png]]



Ese "salto" sirve justamente para decirle al programa dónde empieza el siguiente elemento. Como el programa sabe desde el principio que tu vector es de tipo `int`, sabe dos cosas fundamentales al momento de leer la memoria:

1. **El tamaño del salto:** Para pasar de `vec[0]` a `vec[1]`, sabe que tiene que avanzar 4 posiciones en la memoria (por eso en tu imagen salta del 8020 al 8024).
    
2. **Cuánto tiene que leer (el tamaño del "casillero"):** Cuando le pedís que lea `vec[1]`, el programa va a la dirección 8024 y sabe que tiene que leer exactamente **4 bytes enteros** (es decir, lee las direcciones 8024, 8025, 8026 y 8027 juntas) para poder armar los 32 bits que componen tu número 8.
    

Por eso los lenguajes de programación usan los índices (`[0]`, `[1]`, `[2]`). Internamente, el programa hace una cuenta matemática muy simple para saber dónde leer: **Dirección de memoria inicial + (Índice * 4 bytes)**.

Así se asegura de empezar a leer en el casillero correcto y detenerse justo donde termina ese número, sin pisar la información del siguiente.



![[Pasted image 20260831202838.png]]


cuanto tengo una variable dentro de una función donde se que no la voy a usar mas la tengo que declarar como null, lo que ocurre es que vec deja de refenciar a la parte de la memoria en el heap,  y se le asigna la direccion 0, lo que tiene java es que cada cierto tiempo analiza el código y ve si hay memoria en el heap que no la referencia nada elimina esa memoria, al ponerle null a vec, deja de referenciar a la memoria en el heap y pasa a tener el  valor 0, cuando pasa el garbage collector lo ve y elimina la memoria del heap ya que no tiene referencia


![[Pasted image 20260831214224.png]]

se libera si no tiene ninguna referencia, ya con que almenos tenga una no se elimina


![[Pasted image 20260901000715.png]]


![[Pasted image 20260901002114.png]]

![[Pasted image 20260901002838.png]]

![[Pasted image 20260901005304.png]]

![[Pasted image 20260901011849.png]]

si yo tengo un vector y le tengo que agregar elementos, lo que hago es crear un nuevo vector y le pego en el nuevo, lo que pasa es que si después tengo que seguir agregando elementos voy a tener que copiar de nuevo todos los elementos y pegarlos, entonces lo que se hace es en vez de crear nuevos vectores agregando un tamaño para los elementos que tengo en el momento, lo que se hace es crear un vector nuevo pero duplicado su tamaño, recién cuando se llena este vector ahí creo otro con el doble de tamaño y así
También esto ocurre con la eliminación de elementos en el cual voy a redimensionarlo si tengo que eliminar muchos espacios

![[Pasted image 20260901012210.png]]


La lógica que describís es exacta. Como los arreglos en Java tienen un tamaño de memoria fijo desde que se crean, la única forma de "agrandarlos" es creando uno nuevo y redirigiendo las referencias.

  

Este es el código paso a paso implementando esa misma secuencia:

  

Java

```java
// Supongamos que este es tu vector original, que ya está lleno (tamaño 3)
int[] miVector = {5, 10, 15}; 

// El número que queremos agregar
int nuevoNumero = 20;

// 1. Crear un vector nuevo pidiendo una posición más de memoria
int[] vectorNuevo = new int[miVector.length + 1];

// 2. Copiar los elementos del vector viejo al nuevo usando un bucle
for (int i = 0; i < miVector.length; i++) {
    vectorNuevo[i] = miVector[i];
}

// 3. Insertar el nuevo elemento en la última posición disponible
vectorNuevo[vectorNuevo.length - 1] = nuevoNumero;

// 4. Cambiar la referencia para que tu variable apunte al arreglo nuevo
miVector = vectorNuevo;
```

Cuando el programa ejecuta `miVector = vectorNuevo;`, la variable `miVector` (que vive en el _stack_) suelta el arreglo de 3 posiciones y empieza a apuntar a la dirección de memoria del arreglo nuevo de 4 posiciones en el _heap_.

  

El arreglo viejo original queda flotando en la memoria sin ninguna variable que lo referencie. El Recolector de Basura de Java (Garbage Collector) detecta esto automáticamente y elimina ese arreglo viejo para liberar el espacio.