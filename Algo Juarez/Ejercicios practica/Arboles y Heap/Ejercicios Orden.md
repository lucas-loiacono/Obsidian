
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


# Inorder
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

# Recorridos Preorder y Postorder (Árbol Ampliado)

Vamos a usar el árbol modificado al que le agregamos los nodos `15` (hijo izquierdo del 19) y `27` (hijo derecho del 26)[cite: 11]. 

---

## 1. Recorrido Preorder (Pre-orden)
### Regla fundamental: Raíz $\rightarrow$ Izquierda $\rightarrow$ Derecha
La lógica acá es ansiosa: **apenas pisás un nodo por primera vez, lo anotás inmediatamente**. Recién después de anotarlo, intentás ir todo lo que puedas a la izquierda, y cuando no podés más, vas a la derecha.

### Resolución paso a paso:
1. **Raíz y bajada izquierda:**
   - Empezamos en la raíz principal. Apenas llego, lo anoto: **`20`**.
   - Bajo a su izquierda al 19. Lo anoto de una: **`19`**.
   - Bajo a su izquierda al 15. Lo anoto de una: **`15`**[cite: 11].
   - El 15 no tiene hijos. Subo al 19 y ahora voy a su derecha (26).
2. **Subárbol del 26:**
   - Llego al 26. Lo anoto: **`26`**.
   - Voy a su izquierda. Llego al 21. Lo anoto: **`21`**.
   - El 21 no tiene hijos. Subo al 26 y voy a su derecha.
   - Llego al 27. Lo anoto: **`27`**[cite: 11].
   - El 27 no tiene hijos. Terminamos toda la mitad izquierda del árbol original.
3. **Subárbol derecho (mitad derecha del 20):**
   - Subimos hasta el 20 y pasamos a su hijo derecho (28). Lo anoto: **`28`**.
   - Voy a su izquierda. Llego al 18. Lo anoto: **`18`**.
   - El 18 no tiene hijos. Subo al 28 y voy a su derecha (30).
   - Llego al 30. Lo anoto: **`30`**.
   - El 30 no tiene izquierda, así que voy directo a su derecha (50). Lo anoto: **`50`**.
   - Voy a la izquierda del 50. Llego al 40. Lo anoto: **`40`**.

**Secuencia Preorder final:**
**`20, 19, 15, 26, 21, 27, 28, 18, 30, 50, 40`**

---

## 2. Recorrido Postorder (Post-orden)
### Regla fundamental: Izquierda $\rightarrow$ Derecha $\rightarrow$ Raíz
La lógica acá es la más paciente de todas: **un nodo solo se anota cuando ya visitaste absolutamente a todos sus hijos** (izquierdos y derechos). Bajás a la izquierda, si no podés más vas a la derecha, y recién antes de "subir" de vuelta al padre, anotás el nodo actual.

### Resolución paso a paso:
1. **Subárbol izquierdo:**
   - Arranco en el 20. Bajo al 19 $\rightarrow$ Bajo al 15.
   - El 15 no tiene hijos. Como ya revisé su (inexistente) izquierda y derecha, lo anoto: **`15`**[cite: 11].
   - Subo al 19. ¿Lo anoto? NO, porque me falta visitar su derecha (26). Bajo al 26.
   - Llego al 26. Bajo a su izquierda (21).
   - El 21 no tiene hijos. Lo anoto: **`21`**.
   - Subo al 26. Voy a su derecha (27).
   - El 27 no tiene hijos. Lo anoto: **`27`**[cite: 11].
   - Subo al 26. Como ya visité a sus dos hijos (21 y 27), ahora sí lo anoto: **`26`**.
   - Subo al 19. Como ya visité a sus dos hijos (15 y 26), ahora sí lo anoto: **`19`**.
2. **Subárbol derecho:**
   - Subo al 20. ¿Lo anoto? NO, falta toda su rama derecha. Bajo al 28.
   - Del 28 bajo a su izquierda (18). El 18 no tiene hijos, lo anoto: **`18`**.
   - Subo al 28 y voy a su derecha (30). 
   - El 30 no tiene izquierda, así que bajo a su derecha (50).
   - Del 50 bajo a su izquierda (40). El 40 no tiene hijos, lo anoto: **`40`**.
   - Subo al 50. Como no tiene hijo derecho y ya visité el izquierdo, lo anoto: **`50`**.
   - Subo al 30. Como ya visité todo lo que había abajo de él, lo anoto: **`30`**.
   - Subo al 28. Como ya visité su izquierda (18) y su derecha (30), lo anoto: **`28`**.
3. **Cierre en la raíz:**
   - Subo finalmente al 20. Como ya procesé toda su inmensa rama izquierda y derecha, lo anoto: **`20`**.

**Secuencia Postorder final:**
**`15, 21, 27, 26, 19, 18, 40, 50, 30, 28, 20`**


![[Pasted image 20261107193100.png]]

# Práctica: Árbol Binario de 5 Niveles

## 1. Recorrido Preorder (Pre-orden)

### Regla: Raíz $\rightarrow$ Izquierda $\rightarrow$ Derecha

_(Apenas piso un nodo por primera vez, lo anoto)._

- Empezamos en la raíz principal: **`50`**.
    
- Bajo a la izquierda: **`30`**.
    
    - Sigo a la izquierda: **`20`**.
        
        - Sigo a la izquierda: **`10`**.
            
            - Sigo a la izquierda (hoja): **`5`**.
                
            - Subo al 10, voy a su derecha (hoja): **`15`**.
                
        - Subo al 20, voy a su derecha: **`25`**.
            
            - No tiene izquierdo. Voy a su derecha (hoja): **`28`**.
                
    - Subo al 30, voy a su derecha: **`40`**.
        
        - Voy a su izquierda: **`35`**.
            
            - No tiene izquierdo. Voy a su derecha (hoja): **`38`**.
                
        - Subo al 40, voy a su derecha (hoja): **`45`**.
            
- Subo hasta la raíz 50 y paso a toda su gran mitad derecha: **`70`**.
    
    - Voy a su izquierda: **`60`**.
        
        - No tiene izquierdo (solo derecho). Voy a su derecha: **`55`**.
            
    - Subo al 70, voy a su derecha: **`80`**.
        
        - Voy a su izquierda: **`75`**.
            
            - Sigo a su izquierda: **`72`**.
                
        - Subo al 80, voy a su derecha: **`90`**.
            
            - No tiene izquierdo. Voy a su derecha: **`95`**.
                

**Secuencia Preorder:**

`50, 30, 20, 10, 5, 15, 25, 28, 40, 35, 38, 45, 70, 60, 55, 80, 75, 72, 90, 95`

## 2. Recorrido Inorder (En-orden)

### Regla: Izquierda $\rightarrow$ Raíz $\rightarrow$ Derecha

_(Voy todo a la izquierda que pueda; cuando me tranco, anoto el nodo y miro a su derecha)._

- Bajo todo a la izquierda hasta el final: **`5`**.
    
- Subo al padre: **`10`**.
    
- Voy a la derecha del 10: **`15`**.
    
- Subo al abuelo: **`20`**.
    
- Paso al 25 (el 25 no tiene izquierdo, así que es el siguiente): **`25`**.
    
    - Bajo a su derecha: **`28`**.
        
- Subo al padre de esa gran rama: **`30`**.
    
- Paso a la derecha del 30 (llegamos al 40, pero antes de anotarlo hay que ir a su izquierda y bajar todo, es decir, el 35. Pero el 35 no tiene izquierdo, así que): **`35`**.
    
    - Voy a su derecha: **`38`**.
        
- Subo de vuelta: **`40`**.
    
- Voy a la derecha del 40: **`45`**.
    
- Ya completamos toda la mitad izquierda. Le toca a la raíz principal: **`50`**.
    
- Pasamos a la mitad derecha (llegamos al 70, pero hay que bajar a su izquierda al 60. El 60 no tiene hijo izquierdo, así que): **`60`**.
    
    - Bajo a su hijo derecho: **`55`**.
        
- Subo de vuelta: **`70`**.
    
- Pasamos a la rama del 80. Bajamos a su izquierda (75 $\rightarrow$ 72). El 72 no tiene izquierdo: **`72`**.
    
- Subo al padre: **`75`**.
    
- Subo de vuelta: **`80`**.
    
- Paso a su derecha (90. No tiene izquierdo, así que): **`90`**.
    
    - Bajo a su derecha: **`95`**.
        

**Secuencia Inorder (queda ordenada de menor a mayor):**

`5, 10, 15, 20, 25, 28, 30, 35, 38, 40, 45, 50, 60, 55, 70, 72, 75, 80, 90, 95`

## 3. Recorrido Postorder (Post-orden)

### Regla: Izquierda $\rightarrow$ Derecha $\rightarrow$ Raíz

_(Solo anoto un nodo cuando ya he visitado todas sus sub-ramas y no me queda nada más abajo de él)._

- Bajo todo lo que puedo a la izquierda: el 5 no tiene hijos, así que: **`5`**.
    
- Voy a la derecha del 10: el 15 no tiene hijos, así que: **`15`**.
    
- Ahora que visité izquierdo y derecho, anoto su padre: **`10`**.
    
- Subo. Antes del 20, me falta su derecha (25). Voy al 25.
    
    - Bajo a su derecha: **`28`**.
        
    - Ahora anoto su padre: **`25`**.
        
- Ahora que visité la izquierda (10) y la derecha (25) del 20, anoto: **`20`**.
    
- Subo. Antes del 30, me falta toda su derecha (la rama del 40).
    
    - Bajo al 40 $\rightarrow$ bajo a su izquierda (35) $\rightarrow$ bajo a su derecha: **`38`**.
        
    - Anoto al padre: **`35`**.
        
    - Voy a la derecha del 40: **`45`**.
        
    - Anoto al padre: **`40`**.
        
- Ahora que procesé la izquierda (20) y la derecha (40) del 30, lo anoto: **`30`**.
    
- Subo al 50. ¡Todavía no! Falta toda la inmensa mitad derecha.
    
    - Bajo al 70 $\rightarrow$ bajo al 60 $\rightarrow$ bajo a su derecha: **`55`**.
        
    - Anoto al 60: **`60`**.
        
    - Pasamos a la derecha del 70 (80).
        
        - Bajo a su izquierda (75) $\rightarrow$ bajo a su izquierda: **`72`**.
            
        - Anoto al padre: **`75`**.
            
        - Paso a la derecha del 80 (90) $\rightarrow$ bajo a su derecha: **`95`**.
            
        - Anoto al 90: **`90`**.
            
        - Anoto al 80: **`80`**.
            
    - Anoto al 70: **`70`**.
        
- Por último, con la izquierda y derecha del árbol completas, anoto la raíz: **`50`**.
    

**Secuencia Postorder:**

`5, 15, 10, 28, 25, 20, 38, 35, 45, 40, 30, 55, 60, 72, 75, 95, 90, 80, 70, 50