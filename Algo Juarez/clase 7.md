
![[Pasted image 20260908181012.png]]

![[Pasted image 20260908181229.png]]

![[Pasted image 20260908182349.png]]

![[Pasted image 20260908182358.png]]



![[Pasted image 20260908183000.png]]

![[Pasted image 20260908181925.png]]

![[Pasted image 20260908181948.png]]

El tercer $n$ sale de **la cantidad de elementos que tiene la fila y la columna que estás enfrentando.**

Piensa que cuando ya elegiste una fila de la matriz A y una columna de la matriz B, todavía no tienes el resultado. Tienes en tus manos dos arreglos (arrays) de tamaño $n$.

Para convertir esos dos arreglos en un solo número, tienes que recorrerlos de principio a fin, multiplicando el índice 1 con el 1, el 2 con el 2, el 3 con el 3... hasta llegar al índice $n$. Ese recorrido elemento por elemento es tu tercer $n$.

Desglosemos exactamente qué hace cada $n$:

1. **El primer $n$:** Recorre todas las filas de la matriz A.
    
2. **El segundo $n$:** Recorre todas las columnas de la matriz B.
    
    _(Al multiplicar estos dos, obtienes $n^2$. Esto representa simplemente la cantidad de celdas vacías que tiene la matriz final $C$ que debes llenar)._
    
1. **El tercer $n$ (el que no encontrabas):** Es la caminata que haces dentro de esa fila y esa columna específicas para calcular el valor de la celda. Como la matriz es de $n \times n$, la fila tiene $n$ elementos y la columna tiene $n$ elementos. Debes hacer $n$ multiplicaciones individuales para resolver esa única celda.
    


Por eso, en lenguajes como C, Java o Python, la operación te obliga a escribir tres bucles `for` anidados:


- El `for i` (primer $n$) y el `for j` (segundo $n$) solo sirven para posicionarte en una celda vacía de la matriz final, por ejemplo `C[i][j]`.
    
   
- El `for k` (tercer $n$) es el que hace el trabajo pesado: da $n$ pasos a lo largo de la fila `i` y la columna `j` para multiplicar y sumar los valores.


![[Pasted image 20260908183044.png]]

![[Pasted image 20260908183009.png]]

![[Pasted image 20260908183015.png]]

![[Pasted image 20260908183247.png]]

![[Pasted image 20260911171045.png]]

![[Pasted image 20260908183258.png]]

![[Pasted image 20260908183119.png]]

combinacion de 3 locales, = 3!

![[Pasted image 20260908183729.png]]

![[Pasted image 20260908183739.png]]

![[Pasted image 20260908184054.png]]

![[Pasted image 20260908184128.png]]

![[Pasted image 20260908184210.png]]

![[Pasted image 20260908184442.png]]

![[Pasted image 20260908184536.png]]

![[Pasted image 20260908184922.png]]

![[Pasted image 20260908185017.png]]

![[Pasted image 20260908185737.png]]

![[Pasted image 20260908185841.png]]

![[Pasted image 20260908190145.png]]

![[Pasted image 20260908190307.png]]

![[Pasted image 20260908190457.png]]

![[Pasted image 20260908190740.png]]

![[Pasted image 20260908190816.png]]

![[Pasted image 20260908190928.png]]

![[Pasted image 20260908191821.png]]

![[Pasted image 20260908191849.png]]

![[Pasted image 20260908191902.png]]

![[Pasted image 20260908191926.png]]

![[Pasted image 20260908192044.png]]

OE = operaciones elementales

Mejor caso = 4 y peor caso = 7, tengo que calcular mi probabilidad de salir en cada caso por el caso

por ejemplo el 90% de los casos cae en 4 y el 10% cae en 7
4 x 0.9 o 7 x 0.1


![[Pasted image 20260908192407.png]]

![[Pasted image 20260908194542.png]]


![[Pasted image 20260908194811.png]]

![[Pasted image 20260908195010.png]]