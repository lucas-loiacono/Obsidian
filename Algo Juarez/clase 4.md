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