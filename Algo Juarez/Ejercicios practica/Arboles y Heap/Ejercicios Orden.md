
![[Pasted image 20261107190850.png]]


# Ejercicio 3.2: Recorrido Inorder (Árbol Original)

### Regla fundamental (Izquierda $\rightarrow$ Raíz $\rightarrow$ Derecha)
En cada nodo, el algoritmo intenta bajar todo lo posible hacia su hijo izquierdo. Solo cuando no hay más camino a la izquierda, se anota el nodo actual y luego se intenta dar un paso hacia su hijo derecho (para repetir el proceso desde ahí)[cite: 10].

### Resolución paso a paso

Arrancamos en la raíz principal (**20**). No la anotamos, buscamos su izquierda[cite: 10].

#### 1. Subárbol Izquierdo
*   Bajamos al **19**. ¿Tiene hijo izquierdo? No. Entonces ya no podemos ir más a la izquierda y lo anotamos: **`19`**[cite: 10].
*   Ahora miramos la derecha del 19. Tiene al **26**.
*   Llegamos al **26**. ¿Lo anotamos? No, primero buscamos su izquierda. Tiene al **21**[cite: 10].
*   Llegamos al **21**. ¿Tiene hijo izquierdo? No. Lo anotamos: **`21`**[cite: 10].
*   El 21 no tiene hijo derecho. Subimos de vuelta al **26**.
*   Como ya visitamos toda la izquierda del 26, ahora lo anotamos: **`26`**[cite: 10].
*   El 26 no tiene hijo derecho. Terminamos con toda la rama izquierda del árbol original.

*Secuencia hasta ahora:* `19, 21, 26`

#### 2. Raíz Principal
*   Como ya procesamos absolutamente todo el subárbol izquierdo del **20**, ahora es su turno. Lo anotamos: **`20`**[cite: 10].
*   Damos el paso hacia su hijo derecho (**28**) para empezar de nuevo[cite: 10].

*Secuencia hasta ahora:* `19, 21, 26, 20`

#### 3. Subárbol Derecho
*   Llegamos al **28**. Buscamos su izquierda y bajamos al **18**[cite: 10].
*   El **18** no tiene hijo izquierdo. Lo anotamos: **`18`**[cite: 10].
*   El 18 no tiene derecho. Subimos al **28**.
*   Como ya hicimos la izquierda del 28, lo anotamos: **`28`**[cite: 10].
*   Bajamos a la derecha del 28 y llegamos al **30**[cite: 10].
*   El **30** no tiene hijo izquierdo. Lo anotamos directamente: **`30`**[cite: 10].
*   Bajamos a la derecha del 30 y llegamos al **50**[cite: 10].
*   El **50** tiene hijo izquierdo. Bajamos al **40**[cite: 10].
*   El **40** no tiene hijo izquierdo. Lo anotamos: **`40`**[cite: 10].
*   Subimos al **50**. Como ya visitamos su izquierda, lo anotamos: **`50`**[cite: 10].

### Resultado Final
Uniendo los pasos, la secuencia de recorrido inorder es:
**`19, 21, 26, 20, 18, 28, 30, 40, 50`**

Por lo tanto, la opción correcta es la **(a)**[cite: 10].

![[Pasted image 20261107191706.png]]

### Ejemplo hipotético: El 26 tiene un hijo derecho (ej. `27`) y el 19 tiene un hijo izquierdo (ej. `15`).

Imaginemos que la rama izquierda del árbol ahora es así:

- **19** tiene como hijo izquierdo al `15` y como derecho al `26`.
    
- **26** tiene como hijo izquierdo al `21` y como derecho al `27`.
    

Aplicamos la regla estricta de nuevo (Izquierda $\rightarrow$ Raíz $\rightarrow$ Derecha):

1. **Bajamos todo a la izquierda:**
    
    - Arrancás en el 20. Vas a su hijo izquierdo (19).
        
    - Estás en el 19. Vas a su hijo izquierdo (`15`).
        
    - Estás en el `15`. No tiene hijo izquierdo.
        
    - Lo anotás: **`15`**.
        
    - El `15` no tiene hijo derecho. Terminaste ahí. Subís al 19.
        
2. **Procesamos el 19 y bajamos a su derecha:**
    
    - Como ya visitaste toda la izquierda del 19, ahora lo anotás: **`19`**.
        
    - Vas al hijo derecho del 19 (el 26).
        
3. **Procesamos el subárbol del 26:**
    
    - Llegas al 26. ¿Lo anotás? NO. Siempre buscás su izquierda primero. Vas al `21`.
        
    - El `21` no tiene hijo izquierdo. Lo anotás: **`21`**.
        
    - Subís al 26. Como ya visitaste su izquierda, lo anotás: **`26`**.
        
    - Vas al hijo derecho del 26 (el `27`).
        
    - El `27` no tiene hijo izquierdo. Lo anotás: **`27`**.
        
4. **Subimos a la raíz principal:**
    
    - Ya terminaste con el 26, que era la derecha del 19.
        
    - Ya terminaste todo el subárbol izquierdo del 20.
        
    - Ahora sí, anotás la raíz: **`20`**.
        

### Resumen del orden en este caso hipotético:

El orden de impresión para esa rama quedaría: **`15`** $\rightarrow$ **`19`** $\rightarrow$ **`21`** $\rightarrow$ **`26`** $\rightarrow$ **`27`** $\rightarrow$ **`20`** (y luego seguiría con la rama derecha del 28 como en el original).

**La regla de oro:** "Bajo todo lo que puedo" siempre significa "Bajo a la izquierda". Cuando terminás de anotar algo, el movimiento natural es subir un nivel, anotar a ese padre, y dar un paso a la derecha para ver qué hay. Si hay algo a la derecha, volvés a tirarte de cabeza hacia la izquierda de ese nuevo nodo.