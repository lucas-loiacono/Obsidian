¡Excelente! Este ejercicio es el ejemplo perfecto para aplicar todo lo que venimos charlando. Es idéntico en estructura al de "las monedas de Harvey": tenés un parámetro discreto (la cantidad de bolas) y una muestra que extraés. Vamos a resolverlo paso a paso usando la lógica de la "mezcla" (sumatoria).

### Definición del modelo

Primero, traducimos el texto a variables estadísticas:

- **El Parámetro ($B$):** Es la cantidad de bolas blancas en la urna. Como la urna tiene 6 bolas en total, los valores posibles son $b \in \{1, 2, 3, 4, 5, 6\}$.
    
- **Distribución _A Priori_:** Nos dicen que es equiprobable. Por lo tanto, para cualquier valor de $b$:
    
    $$P(B=b) = \frac{1}{6}$$
    
- **La Muestra ($X$):** Extraemos 2 bolas al azar (sin reposición) y observamos 1 blanca y 1 negra. Si definimos $X$ como "cantidad de bolas blancas en la muestra", observamos $X=1$.
    
- **Distribución de la Muestra (Verosimilitud):** Como sacamos sin reposición, $X$ sigue una distribución Hipergeométrica. La probabilidad de sacar exactamente 1 blanca sabiendo que hay $b$ blancas en la urna es:
    
    $$P(X=1 \vert{} B=b) = \frac{\binom{b}{1} \binom{6-b}{1}}{\binom{6}{2}} = \frac{b \cdot (6-b)}{15}$$
    

### (a) Hallar la distribución _a posteriori_ de $b$

Acá aplicamos la fórmula de Bayes usando la sumatoria en el denominador (porque $B$ es discreta).

$$P(B=b \vert{} X=1) = \frac{P(X=1 \vert{} B=b) \cdot P(B=b)}{\sum_{i=1}^{6} P(X=1 \vert{} B=i) \cdot P(B=i)}$$

**1. Calculamos el denominador (Probabilidad Total):**

Reemplazamos en la fórmula de la Hipergeométrica para cada caso posible y multiplicamos por la _a priori_ ($1/6$):

- Si $b=1$: $[(1 \cdot 5)/15] \cdot (1/6) = (5/15) \cdot (1/6) = 5/90$
    
- Si $b=2$: $[(2 \cdot 4)/15] \cdot (1/6) = (8/15) \cdot (1/6) = 8/90$
    
- Si $b=3$: $[(3 \cdot 3)/15] \cdot (1/6) = (9/15) \cdot (1/6) = 9/90$
    
- Si $b=4$: $[(4 \cdot 2)/15] \cdot (1/6) = (8/15) \cdot (1/6) = 8/90$
    
- Si $b=5$: $[(5 \cdot 1)/15] \cdot (1/6) = (5/15) \cdot (1/6) = 5/90$
    
- Si $b=6$: $[(6 \cdot 0)/15] \cdot (1/6) = 0$ _(Lógico: si las 6 son blancas, es imposible sacar una negra)._
    

Sumamos todo para obtener el denominador:

$$P(X=1) = \frac{5 + 8 + 9 + 8 + 5 + 0}{90} = \frac{35}{90}$$

**2. Armamos la distribución _a posteriori_:**

Ahora, dividimos el resultado individual de cada rama por la probabilidad total ($35/90$). Los $90$ se cancelan, simplificando la cuenta:

- $P(B=1 \vert{} X=1) = \frac{5/90}{35/90} =$ **$5/35$** (o $1/7$)
    
- $P(B=2 \vert{} X=1) = \frac{8/90}{35/90} =$ **$8/35$**
    
- $P(B=3 \vert{} X=1) = \frac{9/90}{35/90} =$ **$9/35$**
    
- $P(B=4 \vert{} X=1) = \frac{8/90}{35/90} =$ **$8/35$**
    
- $P(B=5 \vert{} X=1) = \frac{5/90}{35/90} =$ **$5/35$** (o $1/7$)
    
- $P(B=6 \vert{} X=1) = \frac{0}{35/90} =$ **$0$**
    

¡Esa lista de probabilidades es tu respuesta al inciso A!

### (b) Calcular el estimador Máximo A Posteriori de $b$

El estimador Máximo A Posteriori (MAP) es simplemente el valor de tu parámetro que **tiene la probabilidad más alta** en tu nueva distribución _a posteriori_. Es decir, la moda.

Si miramos los resultados del inciso (a), la probabilidad más alta es $9/35$, la cual ocurre cuando $b=3$.

Por lo tanto, la respuesta es:

$$\hat{b}_{MAP} = 3$$

### (c) Calcular el estimador bayesiano de $b$

Como repasamos en la teoría de tus apuntes, cuando te piden "el estimador de Bayes" sin especificar la función de pérdida, se asume por defecto la **pérdida cuadrática**. Bajo pérdida cuadrática, el estimador es la **Esperanza Matemática** de tu distribución _a posteriori_.

Como $B$ es discreta, la esperanza se calcula multiplicando cada valor posible de $b$ por su nueva probabilidad, y sumando todo:

$$\hat{b}_{Bayes} = E[B \vert{} X=1] = \sum_{b=1}^{6} b \cdot P(B=b \vert{} X=1)$$

$$\hat{b}_{Bayes} = 1\left(\frac{5}{35}\right) + 2\left(\frac{8}{35}\right) + 3\left(\frac{9}{35}\right) + 4\left(\frac{8}{35}\right) + 5\left(\frac{5}{35}\right) + 6(0)$$

$$\hat{b}_{Bayes} = \frac{5 + 16 + 27 + 32 + 25}{35}$$

$$\hat{b}_{Bayes} = \frac{105}{35} = 3$$

Por lo tanto, el estimador bayesiano es:

$$\hat{b}_{Bayes} = 3$$

_(Nota: En este caso particular, como la distribución a posteriori te quedó perfectamente simétrica, la moda (MAP) y la media (Bayesiano) coincidieron y dieron 3, pero tené en cuenta que en otros ejercicios suelen dar resultados distintos)._