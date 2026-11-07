
![[Pasted image 20261107190850.png]]

# Ejercicio 3.2: Recorrido de Árboles (Inorder)

### ¿Cómo funciona el recorrido Inorder (En-orden)?
El recorrido *inorder* en un árbol binario sigue siempre un patrón recursivo estricto para cada nodo, conocido como la regla **I-R-D** (Izquierdo - Raíz - Derecho):
1. **Izquierda:** Visita recursivamente todo el subárbol izquierdo.
2. **Raíz:** Imprime (o procesa) el valor del nodo actual.
3. **Derecha:** Visita recursivamente todo el subárbol derecho.

*Truco visual rápido:* Si te imaginás que "aplastás" el árbol verticalmente hacia abajo como si proyectaras una sombra en el piso, el orden de izquierda a derecha en el que caen los nodos es exactamente el recorrido inorder[cite: 10].

### Análisis Paso a Paso
Vamos a aplicar la regla (Izquierda $\rightarrow$ Nodo $\rightarrow$ Derecha) empezando por la raíz principal (20)[cite: 10]:

1. **Subárbol izquierdo del 20:**
   - Bajamos al 19. Como no tiene hijo izquierdo, lo imprimimos directamente: **19**.
   - Vamos a su subárbol derecho (26). Antes de imprimir el 26, debemos visitar su hijo izquierdo (21).
   - El 21 no tiene hijos, se imprime: **21**.
   - Volvemos al padre e imprimimos: **26**. (Como no tiene hijo derecho, terminamos esta parte).
   - *Secuencia acumulada:* `19, 21, 26`
2. **Raíz principal:**
   - Habiendo procesado todo el subárbol izquierdo, imprimimos la raíz: **20**.
   - *Secuencia acumulada:* `19, 21, 26, 20`
3. **Subárbol derecho del 20:**
   - Bajamos al 28. Antes de imprimirlo, procesamos su hijo izquierdo (18).
   - El 18 no tiene hijos, se imprime: **18**.
   - Volvemos al padre e imprimimos: **28**.
   - Vamos a su subárbol derecho (30). Como no tiene hijo izquierdo, imprimimos directamente: **30**.
   - Vamos a su subárbol derecho (50). Antes de imprimirlo, procesamos su hijo izquierdo (40).
   - El 40 no tiene hijos, se imprime: **40**.
   - Volvemos al padre e imprimimos: **50**.
   - *Secuencia finalizada:* `18, 28, 30, 40, 50`

### Resultado Final
Al concatenar todas las etapas obtenemos la secuencia completa:
**19, 21, 26, 20, 18, 28, 30, 40, 50**

La opción correcta es la **(a)**[cite: 10].




¡Exactamente! Lo dedujiste perfecto. La clave está en entender que cada vez que te movés hacia un "hijo derecho", **ese hijo derecho se convierte automáticamente en la raíz de su propio mini-árbol**, y tenés que volver a aplicar la misma regla desde cero.

  

Cada vez que pisás un nodo nuevo, tu cerebro (o el algoritmo) tiene que hacerse siempre estas 3 preguntas en orden:

  

1. **¿Tiene hijo izquierdo?** Si tiene, me voy para allá al fondo a la izquierda hasta que no haya más.
    
      
    
2. **Lo anoto / imprimo.** (Solo cuando ya no hay más nada a la izquierda).
    
      
    
3. **¿Tiene hijo derecho?** Si tiene, doy un paso a la derecha y **vuelvo a empezar la regla 1** para ese nuevo nodo.
    
      
    

### Ejemplo práctico con el árbol anterior (parte derecha)

Venías de la raíz principal (20). Ahora toca ir a su hijo derecho, que es el **28**.

  

1. Llegas al **28**. ¿Podés anotarlo de una? No. Primero tenés que ver si tiene hijo izquierdo.
    
      
    
2. Como tiene al **18**, bajás al 18.
    
      
    
3. Llegas al **18**. ¿Tiene hijo izquierdo? No. Entonces lo anotás: **`18`**.
    
      
    
4. ¿El 18 tiene hijo derecho? No. Entonces terminaste con el 18. Subís de vuelta a su padre (el 28).
    
      
    
5. Como ya visitaste la izquierda del **28**, ahora sí lo anotás: **`28`**.
    
      
    
6. Ahora vas al hijo derecho del 28, que es el **30**.
    
      
    
7. Llegás al **30**. ¿Tiene hijo izquierdo? No. Entonces lo anotás directo: **`30`**.
    
      
    
8. Vas al hijo derecho del 30, que es el **50**.
    
      
    
9. Llegás al **50**. ¿Lo anotás de una? No, porque tiene un hijo izquierdo (el 40). Entonces bajás al 40.
    
      
    
10. Llegás al **40**. Como no tiene izquierdo, lo anotás: **`40`**.
    
      
    
11. Subís al **50**, y como ya hiciste su izquierda, ahora lo anotás: **`50`**.
    
      
    

Por eso el orden de esa rama te quedó `18, 28, 30, 40, 50`. Siempre que des un paso a la derecha, tu primer instinto tiene que ser buscar inmediatamente si de ahí podés tirarte hacia la izquierda.