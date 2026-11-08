
![[Pasted image 20261107205157.png]]

# Ejercicio 4.1: Tabla de Hashing

### a. Definir el tamaño de la tabla
El factor de carga ($\alpha$) de una tabla de hash se define como la cantidad de elementos ($n$) dividida por el tamaño de la tabla ($m$)[cite: 15]. 
La fórmula es: $\alpha = \frac{n}{m}$

Reemplazando con los datos del enunciado[cite: 15]:
$0.8 = \frac{8}{m}$
$m = \frac{8}{0.8}$
$m = 10$

El tamaño de la tabla será de **10 posiciones** (índices del 0 al 9).

---

### b. Operaciones paso a paso

La función de hash a utilizar es el módulo con el tamaño de la tabla: $h(k) = k \pmod{10}$[cite: 15]. 
La resolución de colisiones es *Linear Probing* (exploración lineal), buscando en la siguiente posición libre $h(k) + i$ si hay una colisión[cite: 15]. 
*Nota importante sobre la eliminación en Open Addressing:* Para no romper la cadena de búsqueda de futuros elementos que hayan colisionado, al eliminar un elemento no se deja la celda "vacía", sino que se marca con un estado de **"Borrado Lógico"** (Tombstone).

**Estado inicial:** Tabla vacía con 10 posiciones (0 a 9).

1.  **`inserción(62);`**[cite: 15]
    *   Cálculo: $h(62) = 62 \pmod{10} = 2$.
    *   Explicación: La posición 2 está vacía ($i=0$). Insertamos el 62.
    *   *Estado parcial:* Posición `[2] = 62`.

2.  **`inserción(140);`**[cite: 15]
    *   Cálculo: $h(140) = 140 \pmod{10} = 0$.
    *   Explicación: La posición 0 está vacía ($i=0$). Insertamos el 140.
    *   *Estado parcial:* Posición `[0] = 140`, `[2] = 62`.

3.  **`inserción(216);`**[cite: 15]
    *   Cálculo: $h(216) = 216 \pmod{10} = 6$.
    *   Explicación: La posición 6 está vacía ($i=0$). Insertamos el 216.
    *   *Estado parcial:* Posición `[0] = 140`, `[2] = 62`, `[6] = 216`.

4.  **`eliminación(140);`**[cite: 15]
    *   Cálculo: $h(140) = 140 \pmod{10} = 0$.
    *   Explicación: Buscamos en la posición 0 y encontramos el 140. Lo eliminamos y dejamos una marca de **BORRADO**.
    *   *Estado parcial:* Posición `[0] = BORRADO`, `[2] = 62`, `[6] = 216`.

5.  **`eliminación(216);`**[cite: 15]
    *   Cálculo: $h(216) = 216 \pmod{10} = 6$.
    *   Explicación: Buscamos en la posición 6 y encontramos el 216. Lo eliminamos y dejamos una marca de **BORRADO**.
    *   *Estado Final:* Posición `[0] = BORRADO`, `[2] = 62`, `[6] = BORRADO`.

*(Las posiciones 1, 3, 4, 5, 7, 8 y 9 se mantuvieron completamente vacías durante todo el proceso).*

---

### c. ¿Cuál es la finalidad de guardar elementos en una tabla de hashing?
La finalidad principal de una tabla de hash es **lograr operaciones de búsqueda, inserción y eliminación extremadamente eficientes**, idealmente en tiempo constante **$O(1)$** en el caso promedio. 

Al mapear directamente la "clave" de un elemento a un "índice" de un arreglo mediante una función matemática, se evita tener que recorrer secuencialmente estructuras de datos enteras (como pasa en las listas o los árboles desbalanceados) para encontrar o guardar un valor.

![[Pasted image 20261107205622.png]]

# Ejercicio 4.2: Seguimiento de Tabla Hash

### Datos iniciales
- **Tamaño de la tabla ($N$):** 7 (posiciones del 0 al 6)[cite: 16].
- **Función de Hash:** $h(k) = k \pmod 7$[cite: 16].
- **Resolución de colisiones:** Open Addressing con exploración lineal (Linear Probing). Si hay colisión, se busca en la siguiente posición libre de forma circular ($i+1$, $i+2$, etc.)[cite: 16].

---

### Operaciones paso a paso

**Estado inicial:** Tabla vacía `[ , , , , , , ]`

1.  **`alta(76);`**[cite: 16]
    *   Cálculo: $h(76) = 76 \pmod 7 = 6$.
    *   Explicación: La posición 6 está vacía, insertamos el 76 ahí.
    *   *Estado parcial:* `[ , , , , , , 76]`

2.  **`alta(93);`**[cite: 16]
    *   Cálculo: $h(93) = 93 \pmod 7 = 2$.
    *   Explicación: La posición 2 está vacía, insertamos el 93 ahí.
    *   *Estado parcial:* `[ , , 93, , , , 76]`

3.  **`alta(40);`**[cite: 16]
    *   Cálculo: $h(40) = 40 \pmod 7 = 5$.
    *   Explicación: La posición 5 está vacía, insertamos el 40 ahí.
    *   *Estado parcial:* `[ , , 93, , , 40, 76]`

4.  **`alta(47);`**[cite: 16]
    *   Cálculo: $h(47) = 47 \pmod 7 = 5$.
    *   Explicación: ¡Colisión! La posición 5 está ocupada por el 40. 
        - Revisamos la siguiente posición (6): ocupada por el 76.
        - Revisamos la siguiente posición (0, damos la vuelta al arreglo): está vacía. Insertamos el 47 en la posición 0.
    *   *Estado parcial:* `[47, , 93, , , 40, 76]`

5.  **`alta(10);`**[cite: 16]
    *   Cálculo: $h(10) = 10 \pmod 7 = 3$.
    *   Explicación: La posición 3 está vacía, insertamos el 10 ahí.
    *   *Estado parcial:* `[47, , 93, 10, , 40, 76]`

6.  **`alta(55);`**[cite: 16]
    *   Cálculo: $h(55) = 55 \pmod 7 = 6$.
    *   Explicación: ¡Colisión! La posición 6 está ocupada por el 76.
        - Revisamos la siguiente (0): ocupada por el 47.
        - Revisamos la siguiente (1): está vacía. Insertamos el 55 en la posición 1.
    *   *Estado parcial:* `[47, 55, 93, 10, , 40, 76]`

7.  **`baja(10);`**[cite: 16]
    *   Cálculo: $h(10) = 10 \pmod 7 = 3$.
    *   Explicación: Buscamos en la posición 3 y encontramos el 10. Para no romper futuras búsquedas con linear probing, se elimina el valor pero se deja una marca de **BORRADO** lógico (Tombstone).
    *   *Estado parcial:* `[47, 55, 93, BORRADO, , 40, 76]`

8.  **`consulta(55);`**[cite: 16]
    *   Cálculo: $h(55) = 55 \pmod 7 = 6$.
    *   Explicación: 
        - Buscamos en la posición 6: está el 76 (no es el 55).
        - Seguimos explorando en la posición 0: está el 47 (no es el 55).
        - Seguimos explorando en la posición 1: está el 55. ¡Encontrado!
    *   *Estado final:* `[47, 55, 93, BORRADO, , 40, 76]` (La consulta no modifica la tabla).


![[Pasted image 20261107205727.png]]


# Ejercicio 4.3: Implementación de Baja en Hash con Chaining

### Enunciado
Implemente el método `public void baja(int dato)` para una clase `Hash` que almacena enteros, usa la función módulo 13 y resuelve colisiones con *Chaining* (vector de listas enlazadas)[cite: 11]. Asumir que los métodos de las clases `Vector` y `Lista` están implementados[cite: 11]. Indicar y justificar la complejidad algorítmica[cite: 11].

### Implementación (Código)

Asumiendo que la clase tiene un atributo interno (por ejemplo, `tabla` o `vector`) que representa el arreglo de listas:

```java
public void baja(int dato) {
    // 1. Calcular el índice usando la función de hash (módulo 13)
    int indice = dato % 13;
    
    // 2. Acceder a la lista correspondiente en esa posición del vector
    Lista lista = tabla.obtener(indice); // (o tabla[indice] dependiendo de la sintaxis)
    
    // 3. Eliminar el dato de la lista (delegando en el método de la clase Lista)
    if (lista != null) {
        lista.eliminar(dato);
    }
}
````

### Complejidad Algorítmica y Justificación

Para determinar la complejidad total, analizamos cada paso del método:

  

1. **Cálculo de la función hash (`dato % 13`):** Es una simple operación aritmética que se resuelve en tiempo constante **$\Theta(1)$**.
    
      
    
2. **Acceso al vector:** Acceder a un índice específico de un arreglo/vector cuesta tiempo constante **$\Theta(1)$**.
    
      
    
3. **Eliminación en la lista (`lista.eliminar(dato)`):** Para eliminar un elemento de una lista simplemente enlazada, el algoritmo interno debe recorrer los nodos hasta encontrar el `dato`.
    
      
    - **Peor caso:** Si la función de hash distribuye mal y absolutamente todos los $N$ elementos insertados previamente en la tabla cayeron en ese mismo `indice` (colisión masiva), la lista tendrá tamaño $N$. Buscar y eliminar el dato ahí costará **$O(N)$**.
        
          
        
    - **Caso promedio:** Si los elementos están bien distribuidos, el tamaño de la lista será igual al factor de carga ($\alpha = N/13$), lo cual tiende a un costo constante $O(1)$.
        
          
        

**Respuesta final de complejidad:** La complejidad temporal del método en el **peor caso** es **$O(N)$**, donde $N$ es la cantidad de datos almacenados en la tabla hash, debido al costo de buscar secuencialmente en la lista enlazada.
