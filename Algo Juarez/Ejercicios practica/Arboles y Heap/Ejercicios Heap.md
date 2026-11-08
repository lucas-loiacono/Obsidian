
Aquí tenés la resolución paso a paso, armada en Markdown para que la puedas guardar directamente en Obsidian.


**1. Árbol inicial** Primero, pasamos el vector `[20, 15, 12, 7, 9, 5, 11, 3, 4, 1]` a un árbol binario. Se completa de arriba hacia abajo y de izquierda a derecha:



```
            20
          /    \
        15      12
       /  \    /  \
      7    9  5    11
     / \  /
    3  4 1
```

**2. Inserción de 17 y proceso de "Upheap" (flote)** Al insertar un elemento en un Heap, siempre se coloca en la primera posición disponible en el último nivel (de izquierda a derecha). En este caso, como hijo derecho del `9`.

  

**Paso A: Inserción inicial**


```
            20
          /    \
        15      12
       /  \    /  \
      7    9  5    11
     / \  / \
    3  4 1  17   <-- Se agrega acá
```

**Paso B: Primer intercambio** Como es un Max-Heap, cada nodo debe ser menor que su padre. Comparamos el `17` con su padre (`9`). Como `17 > 9`, los intercambiamos.



```
            20
          /    \
        15      12
       /  \    /  \
      7   17  5    11
     / \  / \
    3  4 1   9   <-- El 9 bajó, el 17 subió
```

**Paso C: Segundo intercambio** Volvemos a comparar el `17` con su nuevo padre (`15`). Como `17 > 15`, los volvemos a intercambiar.

  

```
            20
          /    \
        17      12
       /  \    /  \
      7   15  5    11
     / \  / \
    3  4 1   9
```

Comparamos el `17` con su nuevo padre (`20`). Como `17 < 20`, se cumple la propiedad del Max-Heap y el algoritmo se detiene.

  

**3. Resolución analítica en el vector (usando fórmulas de índices)** Suponiendo un arreglo indexado en 0, las fórmulas que rigen el heap son:

  

- Hijo izquierdo: `2i + 1`
    
      
    
- Hijo derecho: `2i + 2`
    
      
    
- Padre: `(i - 1) / 2` (división entera)


El vector original tiene tamaño 10 (índices del 0 al 9).

  

1. **Se agrega el 17 al final del vector:** Se coloca en la posición `i = 10`. Vector temporal: `[20, 15, 12, 7, 9, 5, 11, 3, 4, 1, 17]`
    
      
    
2. **Primer cálculo de padre:** El padre del índice `10` está en `(10 - 1) / 2 = 4`. Comparamos `V[10]` (17) contra `V[4]` (9). Como `17 > 9`, hacemos un swap. Vector temporal: `[20, 15, 12, 7, 17, 5, 11, 3, 4, 1, 9]`
    
      
    
3. **Segundo cálculo de padre:** El nuevo índice del 17 es `i = 4`. Su padre está en `(4 - 1) / 2 = 1`. Comparamos `V[4]` (17) contra `V[1]` (15). Como `17 > 15`, hacemos un swap. Vector temporal: `[20, 17, 12, 7, 15, 5, 11, 3, 4, 1, 9]`
    
      
    
4. **Tercer cálculo de padre:** El nuevo índice del 17 es `i = 1`. Su padre está en `(1 - 1) / 2 = 0`. Comparamos `V[1]` (17) contra `V[0]` (20). Como `17 < 20`, no hay swap y terminamos.


**Resultado final:** El vector resultante tras agregar el elemento 17 es:`[20, 17, 12, 7, 15, 5, 11, 3, 4, 1, 9]`



# Si no

Es súper directo. Para pasar el árbol ya acomodado al vector, simplemente tenés que leerlo **por niveles: de arriba hacia abajo y de izquierda a derecha**.

  

Tomando el árbol final que armaste con los intercambios:

  

Plaintext

```
            20
          /    \
        17      12
       /  \    /  \
      7   15  5    11
     / \  / \
    3  4 1   9
```

Lo vas anotando nivel por nivel en ese orden exacto:

  

- **Nivel 0 (Raíz):** `20`
    
      
    
- **Nivel 1:** `17`, `12`
    
      
    
- **Nivel 2:** `7`, `15`, `5`, `11`
    
      
    
- **Nivel 3:** `3`, `4`, `1`, `9`
    
      
    

Juntás todo y te queda el vector final:`[20, 17, 12, 7, 15, 5, 11, 3, 4, 1, 9]`

  

Como los Heaps siempre son árboles binarios completos (se llenan todos los niveles de izquierda a derecha antes de pasar al siguiente), la lectura visual nivel por nivel coincide perfectamente con las posiciones del arreglo.c