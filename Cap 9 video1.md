Me dan datos y busco las distribuciones de los resultados

Inferencia: construir un modelo sobre la base de datos experimentales y extraer concluciones 
Poblacion: totalidad de los resultados experimentales posibles
Muestra: conjunto de datos que se obtiene al realizar el experimento una cierta candtidad de veces





![[Pasted image 20260625205902.png]]



### La diferencia entre Variable Aleatoria y Resultado Observado

El error más común es pensar que "los resultados son otra variable aleatoria". No es así. La clave está en la diferencia entre las **letras mayúsculas** y las **letras minúsculas**.

#### 1. El mundo teórico (Letras Mayúsculas: $X, X_1, X_2$)

Una Variable Aleatoria (VA) no es un número fijo, es una **promesa de un resultado**. Es el experimento antes de que ocurra.

- **La Población ($X$):** Es el concepto general. Por ejemplo: _"Tirar un dado de 6 caras y anotar el número"_. No sabemos qué va a salir, pero conocemos sus reglas (probabilidad de 1/6 para cada número).
    
- **La Muestra Aleatoria ($X_1, X_2, \dots, X_n$):** Acá está tu duda. No es agarrar "algunos resultados posibles", sino **decidir repetir el experimento $n$ veces**.
    
    - $X_1$ significa _"Lo que sea que vaya a salir en la primera tirada"_.
        
    - $X_2$ significa _"Lo que sea que vaya a salir en la segunda tirada"_.
        
    - Como **todavía no tiraste los dados**, $X_1$ y $X_2$ siguen siendo inciertas. Siguen siendo Variables Aleatorias. Por eso en tus apuntes dice que la muestra es una "Sucesión de V.A.".
        

#### 2. El mundo empírico (Letras Minúsculas: $x_1, x_2, \dots, x_n$)

Una vez que efectivamente agarrás los dados, los tirás y anotás los números en un papel, la aleatoriedad desaparece.

- **Los Resultados o Realizaciones ($x_i$):** Son los números concretos.
    
    - Tiraste el primer dado y salió un 4. Entonces $x_1 = 4$.
        
    - Tiraste el segundo y salió un 1. Entonces $x_2 = 1$.
        
- Esos números ($4$ y $1$) **ya no son variables aleatorias**, son datos fijos (constantes).
    

### Respondiendo a tu pregunta directamente:

> _"¿Es de todos los resultados posibles que me da el experimento me quedo con algunos?"_

**No exactamente.** No es que tenés una bolsa con todos los resultados posibles (1, 2, 3, 4, 5, 6) y sacás un par para ver qué onda.

Es más bien: **Ejecutás el experimento original varias veces de forma independiente.** Cada vez que lo ejecutás, la variable aleatoria $X$ "escupe" un resultado concreto $x$. Tu muestra observada es el conjunto de esos datos reales que recolectaste ($x_1, x_2, x_3, \dots$).

**En resumen para tu Obsidian:**

- **$X$ (Mayúscula):** El experimento general (La población).
    
- **$X_i$ (Mayúscula):** La $i$-ésima vez que **vas a hacer** el experimento. Sigue siendo aleatorio porque aún no lo hiciste (La muestra aleatoria teórica).
    
- **$x_i$ (Minúscula):** El número concreto que **ya mediste/anotaste**. No tiene nada de aleatorio (El dato u observación).


### La Función de Distribución Conjunta (La fórmula final)

Acá es donde la matemática encastra todo. En teoría de probabilidades, cuando tenés eventos **independientes**, la probabilidad de que ocurran todos al mismo tiempo es igual a la multiplicación de sus probabilidades individuales (la regla del producto).

Por eso, en la última línea de tu apunte, la función de distribución conjunta de toda la muestra ($X_1 \dots X_n$) se escribe utilizando la notación de productoria ($\prod$):

$$F_{X_1, \dots, X_n}(x_1, \dots, x_n) = P(X_1 \le x_1, \dots, X_n \le x_n) = \prod_{i=1}^n F_X(x_i), \quad \forall n \in \mathbb{N}$$
