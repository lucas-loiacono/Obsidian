

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