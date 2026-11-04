

![[Pasted image 20261017193159.png]]

![[Pasted image 20261017193211.png]]


Metodo de expansion

![[Pasted image 20261017193652.png]]

es el tiempo que tardo en hacer la cuenta mas la llamada recursiva para reducir de nuevo

![[Pasted image 20261017193759.png]]

![[Pasted image 20261017193850.png]]

![[Pasted image 20261017193945.png]]

![[Pasted image 20261017194120.png]]

en total da O(Log(N))



Teorema maestro

![[Pasted image 20261017194217.png]]

Solo sirve en divide y vencerás, tengo que buscar los parámetros a b c y d


![[Pasted image 20261017194521.png]]

N= no recursiva
R= recursiva


![[Pasted image 20261017194613.png]]

![[Pasted image 20261017194759.png]]

ya con todos mi datos voy a la tabla de abajo y me fijo con que orden machea mis parámetros


![[Pasted image 20261017195058.png]]

Así seria con merge



El proceso paso a paso para aplicar el Teorema Maestro en algoritmos de "divide y vencerás" consiste en identificar las variables de la ecuación y compararlas en su tabla lógica:

  

**1. Identificar las partes de la ecuación** Debés separar tu función de tiempo en dos bloques: la parte recursiva ("R", que vuelve a llamar a la función $T$) y la parte no recursiva ("N", el costo fijo del bloque). El objetivo es llevar tu función a la estructura base: $T(n) = a \cdot T(n/b) + c \cdot n^d$.

  

**2. Extraer los parámetros $a, b, c$ y $d$**

  

- **a:** Es el número que multiplica a la función $T$, representando cuántas llamadas recursivas se ejecutan.
    
      
    
- **b:** Es el divisor de la fracción $n/b$, representando la proporción en la que se achica el problema original en cada paso.
    
      
    
- **c y d:** Se despejan igualando la parte no recursiva ("N") a la expresión $c \cdot n^d$. Si la parte no recursiva es un tiempo constante equivalente a $O(1)$, entonces $c \cdot n^d = 1$, lo que matemáticamente obliga a que $d = 0$. Si la parte no recursiva depende de $n$ (como en el algoritmo merge), entonces $c \cdot n^d = n$, lo que significa que $d = 1$.
    
      
    

**3. Evaluar la condición $b^d$** Con los datos extraídos, calculás el valor de $b$ elevado a la $d$ ($b^d$) y lo comparás directamente contra el valor de $a$. Por ejemplo, si $a=1, b=2$ y $d=0$, comparás $1$ contra $2^0$ (que da $1$), resultando en la igualdad $1 = 1$.

  

**4. Mapear el resultado en la tabla** Una vez resuelta la comparación, vas a la tabla de resoluciones del teorema y te fijás con qué orden "matchea" (coincide) tu caso:

  

- Si $a < b^d$, la complejidad final es $\theta(n^d)$.
    
      
    
- Si $a = b^d$, la complejidad final es $\theta(n^d \log(n))$.
    
      
    
- Si $a > b^d$, la complejidad final es $\theta(n^{\log_b(a)})$.





Aquí tenés el desglose con la fórmula de recurrencia inicial y el paso a paso para cada algoritmo según las imágenes:

**1. Ejemplo Base (Búsqueda recursiva dividiendo a la mitad)**

- **Fórmula inicial:** $T(n) = 1 \cdot T(n/2) + 1$. (Se realiza una sola llamada recursiva y el trabajo externo es constante, $O(1)$).
    
- **Paso 1 (Extracción):** $a = 1$, $b = 2$, $c = 1$, $d = 0$. El valor $d=0$ sale de igualar la parte constante a la fórmula $c \cdot n^d = 1$.
    
- **Paso 2 (Evaluación):** Se compara $a$ con $b^d$, lo que da $1 = 2^0$. Matemáticamente, esto verifica que $1 = 1$.
    
- **Paso 3 (Tabla del teorema):** Al cumplirse la igualdad ($a = b^d$), aplica el caso $\theta(n^d \log(n))$.
    

- **Paso 4 (Resultado final):** Reemplazando $d=0$, se obtiene $\theta(n^0 \log(n))$, lo que se reduce a una complejidad de **$O(\log n)$**.


**2. Algoritmo Merge (Dividir en dos mitades y procesar todos los elementos)**

  

- **Fórmula inicial:** $T(n) = 2 \cdot T(n/2) + n$. (Se realizan dos llamadas recursivas y el trabajo para fusionar recorre los $n$ elementos).
    
      
    
- **Paso 1 (Extracción):** $a = 2$, $b = 2$, $c = 1$, $d = 1$. El valor $d=1$ surge porque el trabajo externo es proporcional a $n$, cumpliendo que $c \cdot n^d = n$.
    
      
    
- **Paso 2 (Evaluación):** Se compara $a$ con $b^d$, resultando en $2 = 2^1$. Esto verifica la igualdad $2 = 2$.
    
      
    
- **Paso 3 (Tabla del teorema):** Al estar nuevamente en un escenario de igualdad ($a = b^d$), se utiliza la misma fórmula $\theta(n^d \log(n))$.
    
      
    
- **Paso 4 (Resultado final):** Sustituyendo $d=1$, la ecuación queda como $\theta(n^1 \log(n))$, resultando en una complejidad final de **$O(n \log n)$**.