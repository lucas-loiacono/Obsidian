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




Pensalo con la misma lógica que usás al programar. Las matemáticas en esta unidad se comportan exactamente igual que definir funciones y arreglos (arrays) en código:

- **La Población ($X$):** Es la definición de la función misma. Imaginate una función `tirar_dado()` que tiene la lógica de devolver un entero del 1 al 6. Conoces la lógica, pero la función en sí no es un valor.
    
- **La Muestra Teórica ($X_1, X_2, X_3, X_4, X_5, X_6$):** Es como inicializar un arreglo de 6 posiciones, donde en cada posición ponés un llamado a la función, pero **todavía no ejecutaste el código**.
    
    `muestra_teorica = [tirar_dado(), tirar_dado(), tirar_dado(), ...]`
    
    Sabés que son variables independientes entre sí y que todas usan la misma lógica poblacional (son iid a $X$), pero aún están "en suspenso". Son promesas de un valor.
    
- **La Muestra Observada ($x_1, x_2, x_3, x_4, x_5, x_6$):** Es el resultado después de correr el script. Las funciones se evaluaron y ahora tenés un vector de valores reales en memoria.
    
    `muestra_observada = [4, 1, 6, 2, 2, 5]`



![[Pasted image 20260625211538.png]]


### . La Muestra Teórica ($\underline{X}$)

$$\underline{X} = (X_1, \dots, X_n)$$

- **¿Qué es?** Es el vector que contiene la "promesa" de las $n$ observaciones. Representa a la **muestra aleatoria** teórica antes de hacer el experimento.
    
- **El símbolo $\sim$ (Distribuye como):** El apunte dice $X_1, \dots, X_n \overset{iid}{\sim} X$. Esto se lee como: "Las variables $X_1$ a $X_n$ _distribuyen_ de forma Independiente e Idénticamente Distribuida a la variable $X$". Es la forma elegante y resumida de decir que todas siguen la misma función de distribución $F_X(x)$ que tu población original.
    
- **En términos de programación:** Es como declarar la estructura de un array en C o una lista en Python de $n$ posiciones, donde cada posición contiene el llamado a una función, pero el código todavía no se ejecutó.
    

### 2. La Muestra Observada ($\underline{x}$)

$$\underline{x} = (x_1, \dots, x_n)$$

- **¿Qué es?** Es el vector con los números fijos y concretos. Son las **$n$ observaciones** reales que obtuviste después de realizar las repeticiones del experimento.
    
- **El cambio a minúscula:** Al pasar de $\underline{X}$ a $\underline{x}$, la matemática te está avisando que se acabó la incertidumbre. Adentro de ese vector ya no hay variables aleatorias, hay constantes (datos empíricos).
    
- **En términos de programación:** Es el array o lista alojada en memoria con los valores reales (los _integers_ o _floats_) una vez que el script ya corrió.


**1. La Muestra Aleatoria ($\underline{X}$)**

Es como armar un array o una tupla con llamadas a una función, pero **antes de ejecutar el script**. Tenés la estructura armada y sabés qué tipo de dato va a devolver cada posición (por ejemplo, sabés que todas van a devolver un entero regido por las reglas de tu variable original), pero todavía son "promesas" de un resultado. Hay incertidumbre.


```PYTHON
X = (experimento(), experimento(), experimento()) 
# Aún no hay datos empíricos, son Variables Aleatorias.
```

**2. La Muestra Observada ($\underline{x}$)**

Es el estado de la memoria **después de correr el programa**. Las funciones ya se ejecutaron, hicieron su trabajo y devolvieron su valor. La aleatoriedad desapareció por completo. Ahora tenés una tupla de _integers_ puros y duros para analizar o guardar en una base de datos.


```python
x = (4, 1, 6) 
# Son datos reales y constantes. Cero incertidumbre.
```



