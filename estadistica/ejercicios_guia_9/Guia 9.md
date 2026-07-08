![[Pasted image 20260708003846.png]]


El objetivo es probar que la probabilidad de la muestra, dado el estadístico, **no depende del parámetro $p$**.

### 1. Planteamos la Definición Condicional

$$P(\underline{X} = \underline{x} \mid T = t) = \frac{P(\underline{X} = \underline{x} \text{ y } T = t)}{P(T = t)}$$

### 2. Resolvemos el Numerador (La Muestra)

Acá evaluamos dos escenarios lógicos:

- **Si la suma de tu muestra NO da $t$ ($\sum x_i \neq t$):** Es un escenario imposible. La probabilidad es $0$ (y $0$ no depende de $p$, así que vamos bien).
    
- **Si la suma de tu muestra SÍ da $t$ ($\sum x_i = t$):** Como la muestra ya cumple la condición, la intersección se reduce a la probabilidad conjunta de la muestra.
    

Como son 3 variables Bernoulli, multiplicamos sus probabilidades y sumamos los exponentes (como vimos recién):

$$P(\underline{X} = \underline{x}) = \prod_{i=1}^3 p^{x_i}(1-p)^{1-x_i}$$

$$P(\underline{X} = \underline{x}) = p^{\sum x_i} (1-p)^{3 - \sum x_i}$$

Como estamos asumiendo el caso donde $\sum x_i = t$, lo reemplazamos directamente:

$$\text{Numerador} = p^t (1-p)^{3 - t}$$

### 3. Resolvemos el Denominador (El Estadístico)

Necesitamos saber qué distribución tiene $T$.

$T$ es la suma de $3$ variables Bernoulli independientes ($X_1 + X_2 + X_3$). Por definición de estadística, la suma de variables Bernoulli independientes genera una distribución **Binomial**.

- $T \sim \mathcal{B}(n=3, p)$
    

Escribimos la fórmula de la probabilidad exacta para la Binomial:

$$\text{Denominador} = P(T = t) = \binom{3}{t} p^t (1-p)^{3 - t}$$

### 4. El Choque Final (La División)

Ahora juntamos todo en nuestra fórmula condicional asumiendo que $\sum x_i = t$:

$$P(\underline{X} = \underline{x} \mid T = t) = \frac{p^t (1-p)^{3 - t}}{\binom{3}{t} p^t (1-p)^{3 - t}}$$

Fijate lo hermoso que es esto algebraicamente. Todo el bloque $p^t (1-p)^{3 - t}$ está exactamente igual arriba y abajo. **¡Se cancela por completo!**

$$P(\underline{X} = \underline{x} \mid T = t) = \frac{1}{\binom{3}{t}}$$

### Conclusión

El resultado final es $\frac{1}{\binom{3}{t}}$. ¿Ves alguna $p$ en esa fórmula? ¡No!
Como el resultado final de la probabilidad condicional **no depende del parámetro $p$**, queda demostrado por definición pura que $T = X_1 + X_2 + X_3$ **es un estadístico suficiente**. Toda la información sobre $p$ quedó absorbida en la suma, y la muestra individual no nos aporta nada nuevo.





Como vimos en tus apuntes, la forma más rápida y elegante de demostrar que un estadístico es suficiente es usando el **Teorema de Factorización (Fisher-Neyman)**.

El teorema dice que $T$ es suficiente si podemos desarmar la función de probabilidad conjunta de la muestra en dos bloques multiplicados:

$$f(\underline{x}; p) = g(T(\underline{x}), p) \cdot h(\underline{x})$$

**1. Armamos la función conjunta de la muestra:**

Al ser una muestra aleatoria, multiplicamos las $3$ variables Bernoulli individuales:

$$f(\underline{x}; p) = \prod_{i=1}^3 p^{x_i} (1-p)^{1-x_i}$$

**2. Agrupamos usando propiedades de potencias:**

$$f(\underline{x}; p) = p^{\sum_{i=1}^3 x_i} \cdot (1-p)^{\sum_{i=1}^3 (1-x_i)}$$

$$f(\underline{x}; p) = p^{\sum x_i} \cdot (1-p)^{3 - \sum x_i}$$

**3. Aplicamos el Teorema:**

Reemplazamos $\sum x_i$ por nuestro estadístico propuesto $T$:

$$f(\underline{x}; p) = \underbrace{p^T (1-p)^{3-T}}_{g(T, p)} \cdot \underbrace{1}_{h(\underline{x})}$$

Como logramos aislar el parámetro $p$ exclusivamente adentro de una función que depende de $T$ (nuestra $g(T,p)$), y la función que sobra ($h(\underline{x}) = 1$) no depende de $p$, **queda demostrado por factorización que $T = X_1 + X_2 + X_3$ es un estadístico suficiente para $p$.**

- **$h(\underline{x})$ tiene prohibido tocar el parámetro $p$.**
    
- **$g(T, p)$ tiene prohibido tocar las $x_i$ sueltas** (solo puede conocer a la muestra a través del valor de $T$).

### Un ejemplo donde se rompe todo

Supongamos el mismo caso de recién: tirás la moneda 3 veces, tenés una muestra $X_1, X_2, X_3 \sim \text{Bernoulli}(p)$.

Pero esta vez viene alguien y te propone un estadístico malísimo: _"Che, para mí el estadístico suficiente es mirar solo el primer tiro y tirar los otros dos a la basura"_.

Es decir, te propone: **$T = X_1$**

Vamos a intentar aplicar el teorema para ver cómo choca contra la pared:

**1. Armamos la conjunta:**

$$f(\underline{x}; p) = p^{x_1 + x_2 + x_3} \cdot (1-p)^{3 - (x_1 + x_2 + x_3)}$$

**2. Intentamos reemplazar nuestro $T$ (donde dice $x_1$, ponemos $T$):**

$$f(\underline{x}; p) = p^{T + x_2 + x_3} \cdot (1-p)^{3 - T - x_2 - x_3}$$

**3. Desarmamos las potencias para intentar armar las cajas $g$ y $h$:**

$$f(\underline{x}; p) = p^T \cdot p^{x_2 + x_3} \cdot (1-p)^{3-T} \cdot (1-p)^{-(x_2 + x_3)}$$

**4. El callejón sin salida:**

Ahora yo te pido que armes la función $g(T, p)$ y la función $h(\underline{x})$.

- Agarrás $p^T$ y $(1-p)^{3-T}$ y los metés lo más bien adentro de $g(T, p)$.
    
- ¿Pero qué hacemos con el término $p^{x_2 + x_3}$?
    

Acá se rompe la matrix:

- ¿Lo metemos en $h(\underline{x})$? **No podés**, porque tiene la letra $p$, y $h$ tiene prohibido tener el parámetro.
    
- ¿Lo metemos en $g(T, p)$? **Tampoco podés**, porque tiene las letras $x_2$ y $x_3$ sueltas. La función $g$ es "ciega" a la muestra original, solo entiende el idioma de $T$ y de $p$.








![[Pasted image 20260708004802.png]]

### 1. Armar la función conjunta (La Productoria)

Como tenemos una muestra aleatoria $X_1, \dots, X_n$, tenemos que multiplicar la función de densidad individual $n$ veces:

$$f(\underline{x}; \theta) = \prod_{i=1}^n \left( e^{-(x_i - \theta)} \mathbf{1}\{x_i > \theta\} \right)$$

### 2. Trabajar los exponentes (Tu especialidad)

Como todo se está multiplicando, separamos la parte del número $e$ de la indicadora.

Si multiplicamos bases iguales, **los exponentes se suman**:

$$\prod_{i=1}^n e^{-(x_i - \theta)} = e^{-\sum_{i=1}^n (x_i - \theta)}$$

Ahora distribuimos esa sumatoria adentro del paréntesis. ¡Ojo acá! Sumar $x_i$ te da $\sum x_i$, pero sumar una constante $\theta$ un total de $n$ veces, te da $n\theta$:

$$e^{-(\sum x_i - n\theta)} = e^{-\sum x_i + n\theta}$$

Por último, separamos esto en dos bases multiplicadas para tener las cosas bien limpitas:

$$e^{-\sum x_i} \cdot e^{n\theta}$$

### 3. La magia de la Indicadora

Acá aplicamos la misma lógica que vimos antes con la distribución Uniforme, pero al revés.

Tenemos un montón de indicadoras multiplicándose:

$$\prod_{i=1}^n \mathbf{1}\{x_i > \theta\}$$

Para que esta multiplicación no dé cero, **todas** las $x_i$ tienen que ser mayores a $\theta$. Pensalo con lógica: si querés garantizar que absolutamente todos los alumnos de una clase midan más de $1.50m$ (tu $\theta$), te alcanza con agarrar al más bajito de todos (el **mínimo**) y ver si él pasa la marca. Si el mínimo es mayor a $\theta$, ¡todos los demás también lo son!

Entonces, toda esa productoria gigante colapsa en una sola indicadora:

$$\mathbf{1}\{\min(x_1, \dots, x_n) > \theta\}$$

### 4. Aplicar el Teorema de Factorización

Juntemos el resultado del Paso 2 y el Paso 3 en un solo renglón:

$$f(\underline{x}; \theta) = e^{-\sum x_i} \cdot e^{n\theta} \cdot \mathbf{1}\{\min(x_1, \dots, x_n) > \theta\}$$

Llegó el momento de armar las "cajas":

- **La caja de la información ($g(T, \theta)$):** Metemos acá todo lo que tenga nuestro parámetro $\theta$ y el estadístico $T$ que nos propone el ejercicio.
    
    $$g(T, \theta) = e^{n\theta} \cdot \mathbf{1}\{\min(x_1, \dots, x_n) > \theta\}$$
    
- **La caja del "ruido" ($h(\underline{x})$):** Metemos acá lo que sobró, que solo depende de la muestra y **no tiene** a la letra $\theta$.
    
    $$h(\underline{x}) = e^{-\sum x_i}$$
    

Como logramos desarmar la función original en $g(T, \theta) \cdot h(\underline{x})$ de forma perfecta y sin romper ninguna regla matemática, **queda verificado por el Teorema de Factorización que $T = \min(X_1, \dots, X_n)$ es un estadístico suficiente para $\theta$.**



![[Pasted image 20260708005115.png]]

### 1. Planteamos la condicional

Por definición, la probabilidad condicional de la muestra dado el estadístico es:

$$P(\mathbf{X}_n = \mathbf{x} \mid T = t) = \frac{P(\mathbf{X}_n = \mathbf{x} \text{ y } T = t)}{P(T = t)}$$

Si la suma de nuestra muestra no da $t$ ($\sum x_i \neq t$), la probabilidad es $0$.

Si la suma sí da $t$ ($\sum x_i = t$), la intersección de arriba es simplemente la probabilidad conjunta de la muestra. Vamos a enfocarnos en este caso.

### 2. El Numerador (La Muestra Conjunta)

Tenemos $n$ variables independientes que siguen una distribución Poisson($\lambda$). La probabilidad conjunta es la productoria de todas ellas:

$$P(\mathbf{X}_n = \mathbf{x}) = \prod_{i=1}^n \frac{e^{-\lambda} \lambda^{x_i}}{x_i!}$$

Acá aplicamos las propiedades que ya dominás:

- Multiplicar la base $e^{-\lambda}$ un total de $n$ veces es sumar sus exponentes: $e^{-n\lambda}$.
    
- Multiplicar las bases $\lambda^{x_i}$ es sumar sus exponentes: $\lambda^{\sum x_i}$.
    
- Abajo queda la productoria de los factoriales.
    

$$P(\mathbf{X}_n = \mathbf{x}) = \frac{e^{-n\lambda} \lambda^{\sum x_i}}{x_1! \cdot x_2! \dots x_n!}$$

Como estamos bajo la condición de que la suma de todos los valores da $t$ ($\sum x_i = t$), reemplazamos esa suma en el exponente de $\lambda$:

$$\text{Numerador} = \frac{e^{-n\lambda} \lambda^t}{\prod_{i=1}^n x_i!}$$

### 3. El Denominador (La distribución de $T$)

Necesitamos saber qué distribución tiene la suma de $n$ variables Poisson.

Por propiedad reproductiva, la suma de variables Poisson independientes también es una Poisson, pero sus parámetros se suman.

Como sumamos $n$ variables idénticas con parámetro $\lambda$, nuestro estadístico $T$ se distribuye así:

$$T \sim \text{Poisson}(n\lambda)$$

Escribimos la fórmula de la probabilidad para este estadístico $T=t$:

$$\text{Denominador} = P(T = t) = \frac{e^{-n\lambda} (n\lambda)^t}{t!}$$

_Nota: Fijate que en el paréntesis del numerador agrupamos el parámetro completo de la nueva distribución, que es $(n\lambda)$. Al distribuir ese exponente nos queda $n^t \cdot \lambda^t$._

### 4. La División (La "Masacre" Algebraica)

Ahora juntamos numerador y denominador:

$$P(\mathbf{X}_n = \mathbf{x} \mid T = t) = \frac{ \frac{e^{-n\lambda} \lambda^t}{\prod_{i=1}^n x_i!} }{ \frac{e^{-n\lambda} n^t \lambda^t}{t!} }$$

¡Empieza la limpieza!

- El término $e^{-n\lambda}$ está arriba y abajo $\rightarrow$ **Se cancela.**
    
- El término $\lambda^t$ está arriba y abajo $\rightarrow$ **Se cancela.**
    

Acomodamos las fracciones (el $t!$ sube multiplicando y el $n^t$ queda abajo junto con la productoria de los factoriales):

$$P(\mathbf{X}_n = \mathbf{x} \mid T = t) = \frac{t!}{x_1! \cdot x_2! \dots x_n!} \cdot \frac{1}{n^t}$$

_(Dato de color para lucirte: esta fórmula final que quedó es la de una famosa distribución llamada "Distribución Multinomial")._

### La Conclusión (Lo que el profe quiere leer)

Observá detenidamente la fórmula final a la que llegamos. ¿Ves el parámetro $\lambda$ por algún lado?

**No, desapareció por completo.**

El texto de conclusión que tenés que escribir en el parcial es:

> _"Como la distribución condicional de la muestra $\mathbf{X}_n$ dado $T=t$ depende únicamente de los datos muestrales ($x_i, n$ y $t$) y **no depende del parámetro $\lambda$**, deducimos por definición que $T = \sum_{i=1}^n X_i$ es un estadístico suficiente para $\lambda$."_



![[Pasted image 20260708005927.png]]

### (a) Bernoulli($p$)

Partimos de la función original:

$$f(x; p) = p^x (1-p)^{1-x} \cdot \mathbf{1}_{\{0, 1\}}(x)$$

1. **Separar términos:** Rompemos la resta en el exponente de $(1-p)$ para aislar lo que tiene $x$ de lo que no.
    
    $$f(x; p) = \mathbf{1}_{\{0, 1\}}(x) \cdot p^x \cdot (1-p)^1 \cdot (1-p)^{-x}$$
    
2. **Agrupar lo suelto y juntar las $x$:** Movemos el $(1-p)$ para adelante (será nuestro $A$) y juntamos las bases que están elevadas a la $x$.
    
    $$f(x; p) = \mathbf{1}_{\{0, 1\}}(x) \cdot (1-p) \cdot \left( \frac{p}{1-p} \right)^x$$
    
3. **Aplicar el truco a la mezcla:** Ahora sí, metemos el último término en un exponente usando el logaritmo para bajar la $x$.
    
    $$f(x; p) = \mathbf{1}_{\{0, 1\}}(x) \cdot (1-p) \cdot \exp\left\{ x \ln\left( \frac{p}{1-p} \right) \right\}$$
    

**Identificamos las partes:**

- $h(x) = \mathbf{1}_{\{0, 1\}}(x)$
    
- **$A(p) = 1-p$**
    
- $c(p) = \ln\left(\frac{p}{1-p}\right)$
    
- $T(x) = x$
    

### (b) Pascal($4, p$)

Partimos de la función original:

$$f(x; p) = \binom{x-1}{3} p^4 (1-p)^{x-4} \cdot \mathbf{1}_{\{x \ge 4\}}(x)$$

1. **Separar términos:** Rompemos la resta en el exponente de $(1-p)$.
    
    $$f(x; p) = \binom{x-1}{3} \mathbf{1}_{\{x \ge 4\}}(x) \cdot p^4 \cdot (1-p)^{-4} \cdot (1-p)^x$$
    
2. **Agrupar lo suelto:** Juntamos todas las $p$ que no tienen ninguna $x$ al lado para armar nuestro $A(p)$.
    
    $$f(x; p) = \binom{x-1}{3} \mathbf{1}_{\{x \ge 4\}}(x) \cdot \left( \frac{p}{1-p} \right)^4 \cdot (1-p)^x$$
    
3. **Aplicar el truco a la mezcla:** Usamos el logaritmo solo para el término $(1-p)^x$.
    
    $$f(x; p) = \binom{x-1}{3} \mathbf{1}_{\{x \ge 4\}}(x) \cdot \left( \frac{p}{1-p} \right)^4 \cdot \exp\{ x \ln(1-p) \}$$
    

**Identificamos las partes:**

- $h(x) = \binom{x-1}{3} \mathbf{1}_{\{x \ge 4\}}(x)$
    
- **$A(p) = \left(\frac{p}{1-p}\right)^4$**
    
- $c(p) = \ln(1-p)$
    
- $T(x) = x$
    

### (c) Poisson($\lambda$)

Partimos de la función original:

$$f(x; \lambda) = \frac{e^{-\lambda} \lambda^x}{x!} \cdot \mathbf{1}_{\{x \ge 0\}}(x)$$

1. **Separar términos y agrupar:** Sacamos el $e^{-\lambda}$ (que no tiene $x$) y lo mandamos al frente.
    
    $$f(x; \lambda) = \frac{1}{x!} \mathbf{1}_{\{x \ge 0\}}(x) \cdot e^{-\lambda} \cdot \lambda^x$$
    
2. **Aplicar el truco a la mezcla:** Transformamos solo la $\lambda^x$.
    
    $$f(x; \lambda) = \frac{1}{x!} \mathbf{1}_{\{x \ge 0\}}(x) \cdot e^{-\lambda} \cdot \exp\{ x \ln(\lambda) \}$$
    

**Identificamos las partes:**

- $h(x) = \frac{1}{x!} \mathbf{1}_{\{x \ge 0\}}(x)$
    
- **$A(\lambda) = e^{-\lambda}$**
    
- $c(\lambda) = \ln(\lambda)$
    
- $T(x) = x$
    

### (d) Exponencial($\lambda$)

Partimos de la función original:

$$f(x; \lambda) = \lambda e^{-\lambda x} \cdot \mathbf{1}_{\{x > 0\}}(x)$$

Este es el caso más directo porque las cosas ya están en su lugar. No hace falta usar ningún truco de logaritmos porque la $x$ ya está adentro de una función $e$.

1. **Acomodar visualmente:** Simplemente reordenamos para que quede igual al molde que te piden.
    
    $$f(x; \lambda) = \mathbf{1}_{\{x > 0\}}(x) \cdot \lambda \cdot \exp\{ -\lambda x \}$$
    

**Identificamos las partes:**

- $h(x) = \mathbf{1}_{\{x > 0\}}(x)$
    
- **$A(\lambda) = \lambda$**
    
- $c(\lambda) = -\lambda$
    
- $T(x) = x$


![[Pasted image 20260708010651.png]]

¿Por qué? Porque tu parámetro $p$ **no es continuo**. El enunciado te dice explícitamente que $p$ solo puede tomar dos valores concretos: $2/5$ o $4/5$.

Cuando el parámetro es discreto (un conjunto cerrado de opciones), el Método de Máxima Verosimilitud vuelve a su definición más básica: simplemente hay que evaluar la probabilidad de cada caso y **elegir el que dé el número más grande**.

Vamos a resolverlo en dos etapas muy claras:

### Paso 1: Encontrar el Estimador de Máxima Verosimilitud (EMV) de $p$

Primero tenemos que descubrir cuál de las dos monedas es la que estamos usando, basándonos en nuestra muestra (sacamos 3 caras en 10 tiros).

Nuestra variable $X$ (cantidad de caras) tiene una distribución Binomial con $n=10$.

La Función de Verosimilitud (que es la probabilidad de observar lo que observamos) es:

$$L(p) = P(X=3) = \binom{10}{3} p^3 (1-p)^{10-3} = 120 \cdot p^3 (1-p)^7$$

Ahora, simplemente evaluamos esta función para los dos candidatos que tenemos:

**Candidato A: $p = 2/5$**

$$L(2/5) = 120 \cdot \left(\frac{2}{5}\right)^3 \cdot \left(1 - \frac{2}{5}\right)^7 = 120 \cdot \left(\frac{2}{5}\right)^3 \cdot \left(\frac{3}{5}\right)^7$$

**Candidato B: $p = 4/5$**

$$L(4/5) = 120 \cdot \left(\frac{4}{5}\right)^3 \cdot \left(1 - \frac{4}{5}\right)^7 = 120 \cdot \left(\frac{4}{5}\right)^3 \cdot \left(\frac{1}{5}\right)^7$$

No hace falta calcular todo el número con decimales; podés ver visualmente o con la calculadora que la primera opción es muchísimo más grande (tiene un $(3/5)^7$ contra un $(1/5)^7$).

- _Intuición rápida:_ Sacamos 3 caras en 10 tiros, una proporción del $30\%$. Tiene todo el sentido del mundo que el parámetro real esté más cerca de $2/5$ ($40\%$) que de $4/5$ ($80\%$).
    

Como $L(2/5) > L(4/5)$, nuestro estimador de máxima verosimilitud para el parámetro es:

$$\hat{p} = \frac{2}{5}$$

### Paso 2: La Propiedad de Invarianza (El verdadero truco del ejercicio)

El problema no termina ahí. No te pide estimar $p$, te pide estimar **la probabilidad de un evento futuro** (sacar exactamente 1 cara en 3 nuevos tiros).

Llamemos $\tau(p)$ a esa probabilidad que queremos calcular. Como son 3 tiros nuevos, es otra Binomial:

$$\tau(p) = P(Y=1) = \binom{3}{1} p^1 (1-p)^{3-1} = 3p(1-p)^2$$

Acá es donde usás la **Propiedad de Invarianza de los EMV**. Esta propiedad te dice que si vos tenés el EMV de un parámetro ($\hat{p}$) y querés calcular el EMV de una función que depende de ese parámetro, **simplemente tenés que meter tu $\hat{p}$ adentro de esa función**.

Es decir:

$$\widehat{\tau(p)} = \tau(\hat{p})$$

Como ya descubrimos que $\hat{p} = 2/5$, lo reemplazamos en nuestra nueva ecuación:

$$\widehat{\tau(p)} = 3 \cdot \left(\frac{2}{5}\right) \cdot \left(1 - \frac{2}{5}\right)^2$$

$$\widehat{\tau(p)} = 3 \cdot \left(\frac{2}{5}\right) \cdot \left(\frac{3}{5}\right)^2$$

$$\widehat{\tau(p)} = \frac{6}{5} \cdot \frac{9}{25}$$

$$\widehat{\tau(p)} = \frac{54}{125} = 0.432$$

¡Y listo! El resultado final es $54/125$.

**Moraleja para el parcial:** Si te dan el parámetro entre llaves con números sueltos (ej: $p \in \{a, b\}$), guardá las derivadas en el cajón. Calculá las probabilidades a mano, agarrá la más grande, y si te piden estimar una función extra, mandale la propiedad de invarianza.

- **Buscás qué $p$ es más probable:** Mirás la realidad (lo que ya pasó, tu muestra) y te preguntás: _"¿Qué parámetro hace que este resultado sea el más lógico?"_. En tu caso, sacar 3 caras en 10 tiros es mucho más lógico para una moneda del **40%** ($2/5$) que para una del **80%** ($4/5$). Gana el $2/5$.
    
- **Calculás con ese $p$:** Una vez que coronás al ganador como tu estimador oficial ($\hat{p}$), lo usás como si fuera la verdad absoluta para calcular cualquier evento futuro o función que te pidan (esto es lo que formalmente se llama Propiedad de Invarianza).




![[Pasted image 20260708012546.png]]

### Parte (a): La Construcción Teórica

#### 1. Hallar el Estimador de Máxima Verosimilitud (EMV)

Nuestra muestra es $X_1, \dots, X_n \sim \text{Poisson}(\lambda)$. La función de probabilidad individual es $\frac{e^{-\lambda} \lambda^x}{x!}$.

**Paso 1: Armar la Función de Verosimilitud $L(\lambda)$**

Multiplicamos la función $n$ veces (acordate del truco de sumar exponentes para la $e$ y para la $\lambda$):

$$L(\lambda) = \prod_{i=1}^n \frac{e^{-\lambda} \lambda^{x_i}}{x_i!} = \frac{e^{-n\lambda} \lambda^{\sum x_i}}{\prod x_i!}$$

**Paso 2: Aplicar logaritmo natural ($\ln$)**

Esto baja los exponentes y convierte las multiplicaciones/divisiones en sumas y restas:

$$\ln(L(\lambda)) = -n\lambda + \left(\sum_{i=1}^n x_i\right) \ln(\lambda) - \ln\left(\prod_{i=1}^n x_i!\right)$$

**Paso 3: Derivar respecto a $\lambda$ e igualar a cero**

La derivada del último término es $0$ porque no tiene $\lambda$.

$$\frac{d}{d\lambda} \ln(L(\lambda)) = -n + \frac{\sum x_i}{\lambda}$$

Igualamos a cero para encontrar el máximo:

$$-n + \frac{\sum x_i}{\lambda} = 0$$

$$n = \frac{\sum x_i}{\lambda}$$

Despejamos $\lambda$ y le ponemos el "sombrerito" porque ya es nuestro estimador oficial:

$$\hat{\lambda} = \frac{\sum X_i}{n} = \bar{X}$$

_(¡Magia! El método matemático nos confirma que la mejor forma de estimar la media de una Poisson es, literalmente, calculando el promedio de la muestra)._

#### 2. Mostrar que es Insesgado

Un estimador es insesgado si su Esperanza es exactamente igual al parámetro real: $E[\hat{\lambda}] = \lambda$.

$$E[\hat{\lambda}] = E\left[ \frac{\sum X_i}{n} \right]$$

Sacamos la constante $1/n$ afuera:

$$E[\hat{\lambda}] = \frac{1}{n} \sum_{i=1}^n E[X_i]$$

Como cada $X_i$ es una Poisson($\lambda$), sabemos por tabla que su esperanza $E[X_i] = \lambda$. Si sumamos $\lambda$ un total de $n$ veces, tenemos $n\lambda$:

$$E[\hat{\lambda}] = \frac{1}{n} (n\lambda) = \lambda$$

**¡Queda demostrado que es insesgado!**

#### 3. Hallar el Error Cuadrático Medio (ECM)

La fórmula del ECM es: $\text{ECM} = \text{Varianza} + \text{Sesgo}^2$.

Como recién demostramos que es insesgado, el Sesgo es $0$. Por lo tanto, $\text{ECM} = V(\hat{\lambda})$.

$$V(\hat{\lambda}) = V\left[ \frac{\sum X_i}{n} \right]$$

Ojo acá: las constantes salen de la varianza **al cuadrado**:

$$V(\hat{\lambda}) = \frac{1}{n^2} \sum_{i=1}^n V(X_i)$$

En una distribución Poisson, la varianza también vale $\lambda$. Sumamos $\lambda$ un total de $n$ veces:

$$V(\hat{\lambda}) = \frac{1}{n^2} (n\lambda) = \frac{\lambda}{n}$$

Esa es tu expresión final del Error Cuadrático Medio.

### Parte (b): La Aplicación Práctica

Ahora pasamos a la realidad. Tenemos números.

#### 1. Calcular el estimador con la muestra

Nos piden aplicar la fórmula que descubrimos recién ($\hat{\lambda} = \bar{X}$) a la tabla de frecuencias de $n=100$ semanas.

Tenemos que calcular el promedio. Ojo, no sumes los números del 0 al 5 directamente. Tenés que multiplicar la cantidad de accidentes por la cantidad de semanas que ocurrió (Frecuencia):

- $\sum x_i = (0 \cdot 10) + (1 \cdot 29) + (2 \cdot 25) + (3 \cdot 17) + (4 \cdot 13) + (5 \cdot 6)$
    
- $\sum x_i = 0 + 29 + 50 + 51 + 52 + 30 = 212$ accidentes totales.
    

Ahora calculamos nuestro $\hat{\lambda}$ numérico (estimación puntual):

$$\hat{\lambda}_{obs} = \frac{212}{100} = 2.12$$

#### 2. Estimar la probabilidad de ningún accidente

Nos piden estimar la probabilidad de que $X=0$.

La fórmula teórica de la Poisson para $0$ accidentes es:

$$P(X=0) = \frac{e^{-\lambda} \lambda^0}{0!} = e^{-\lambda}$$

¿Te acordás del ejercicio de la moneda? ¡Acá entra la **Propiedad de Invarianza** para salvarte la vida! Si nos piden estimar una función del parámetro, simplemente agarramos la función e inyectamos nuestro $\hat{\lambda}$:

$$\widehat{P(X=0)} = e^{-\hat{\lambda}}$$

$$\widehat{P(X=0)} = e^{-2.12}$$

Y si lo pasás por la calculadora:

$$\widehat{P(X=0)} \approx 0.1199$$

¡Listo! Hay un **11.99%** de probabilidades estimadas de que pases una semana tranquila en Paseo Colón y Estados Unidos.


Todo el esfuerzo que hiciste en la **Parte (a)** despejando ecuaciones, aplicando logaritmos y derivando, tenía un único objetivo: **fabricar la receta perfecta** para calcular $\lambda$.

Esa receta (tu estimador) te dio como resultado final:

$$\hat{\lambda} = \frac{\sum x_i}{n}$$

Si mirás bien esa fórmula, $\frac{\text{suma de todos los valores}}{\text{cantidad de valores}}$ es la definición matemática literal del **promedio** (o media muestral, $\bar{X}$).

Entonces, cuando llegás a la **Parte (b)** y te dan datos reales, no tenés que adivinar o intuir qué hacer. Simplemente le hacés caso a la fórmula que vos mismo demostraste que era la mejor. Tu receta dice "calculá el promedio", así que vas a la tabla y calculás el promedio.

### El detalle de la tabla (¿Por qué multiplicamos?)

Quizás te hizo un poco de ruido cómo calculamos ese promedio. Como los datos te los dieron agrupados en una tabla de frecuencias, no podíamos simplemente sumar $0+1+2+3+4+5$ y dividir por $6$. ¡Estarías ignorando que son 100 semanas en total!

Tenías que sumar los 100 datos reales, que es lo mismo que sumar grupos:

- Hubo 10 semanas con $0$ accidentes: $(0+0+0...+0) \rightarrow 0 \cdot 10 = 0$
    
- Hubo 29 semanas con $1$ accidente: $(1+1+1...+1) \rightarrow 1 \cdot 29 = 29$
    
- ...y así sucesivamente.
    

Sumaste la cantidad **total** de accidentes que ocurrieron a lo largo de toda la historia ($212$ accidentes) y lo dividiste por la cantidad **total** de semanas observadas ($100$ semanas).

$$\hat{\lambda}_{obs} = \frac{212 \text{ accidentes}}{100 \text{ semanas}} = 2.12 \text{ accidentes por semana}$$

**En resumen:** Buscás el promedio única y exclusivamente porque el Método de Máxima Verosimilitud te gritó algebraicamente que esa era la forma correcta de estimar el parámetro para una distribución Poisson. ¡La matemática te dibujó el mapa y vos solo lo seguiste a la perfección!


![[Pasted image 20260708013254.png]]

### (a) Hallar un estadístico suficiente para $\theta$

Este es casi idéntico al de la segunda foto que me mandaste. Vamos a aplicar el **Teorema de Factorización**.

**1. Armamos la conjunta (Productoria):**

Nuestra función de densidad es $f(x; \theta) = \frac{1}{\theta} \mathbf{1}\{0 < x < \theta\}$.

$$f(\underline{x}; \theta) = \prod_{i=1}^n \left( \frac{1}{\theta} \mathbf{1}\{0 < x_i < \theta\} \right)$$

$$f(\underline{x}; \theta) = \frac{1}{\theta^n} \prod_{i=1}^n \mathbf{1}\{0 < x_i < \theta\}$$

**2. La magia de la Indicadora:**

Para que todas las $x_i$ sean menores a $\theta$, alcanza con que el **máximo** de la muestra sea menor a $\theta$.

Y para que todas las $x_i$ sean mayores a 0, alcanza con que el **mínimo** sea mayor a 0.

$$f(\underline{x}; \theta) = \frac{1}{\theta^n} \mathbf{1}\{\max(X_i) < \theta\} \cdot \mathbf{1}\{\min(X_i) > 0\}$$

**3. Aplicamos Factorización:**

Separamos en las dos "cajas":

- $g(T, \theta) = \frac{1}{\theta^n} \mathbf{1}\{\max(X_i) < \theta\}$
    
- $h(\underline{x}) = \mathbf{1}\{\min(X_i) > 0\}$
    

Como logramos aislar $\theta$ en una función que solo depende del máximo, **queda demostrado que $T = \max(X_1, \dots, X_n)$ es un estadístico suficiente.**

### (b) Hallar el estimador de Máxima Verosimilitud (EMV)

**¡Alerta de trampa gigante!** Veníamos de derivar e igualar a cero en la distribución Poisson. Acá **NO PODÉS DERIVAR**.

¿Por qué? Porque tu parámetro $\theta$ está metido adentro de la condición de la indicadora (es el límite del dominio). Si derivás, te da negativo y no llegás a nada.

Tenemos que usar la lógica visual:

La función de verosimilitud es $L(\theta) = \frac{1}{\theta^n} \mathbf{1}\{\theta > \max(X_i)\}$.

Queremos que el resultado de esa cuenta sea **lo más grande posible**.

Como $\theta$ está en el denominador ($\frac{1}{\theta^n}$), para que la fracción sea gigante, **$\theta$ tiene que ser lo más chico posible**.

Pero, ¡ojo! La indicadora nos pone un freno de mano: nos dice que obligatoriamente $\theta > \max(X_i)$. Si probás un número más chico que el máximo, la indicadora se apaga (vale 0) y te arruina la probabilidad.

Por lo tanto, el valor más chico que le podés dar a $\theta$ sin que todo explote y dé cero, es exactamente el máximo de la muestra.

$$\hat{\theta}_{EMV} = \max(X_1, \dots, X_n)$$

_(Ojo a la notación: a veces al máximo se lo escribe como $X_{(n)}$)._

### (c) Mostrar Esperanza, Varianza y Convergencia

Para calcular la Esperanza y Varianza de $\hat{\theta}_n$, necesitamos saber cuál es la función de densidad del máximo. Esto es una fórmula estándar de estadística de orden:

**1. Función de densidad del máximo ($f_{max}(x)$):**

La función de distribución acumulada del máximo es $(F(x))^n$.

Para la Uniforme, $F(x) = \frac{x}{\theta}$. Entonces $F_{max}(x) = (\frac{x}{\theta})^n = \frac{x^n}{\theta^n}$.

Derivamos para tener la densidad:

$$f_{max}(x) = \frac{n}{\theta^n} x^{n-1} \quad \text{para } 0 < x < \theta$$

**2. Mostrar la Esperanza ($E[\hat{\theta}_n]$):**

Por definición, $E[X] = \int x \cdot f(x) dx$.

$$E[\hat{\theta}_n] = \int_0^\theta x \cdot \left( \frac{n}{\theta^n} x^{n-1} \right) dx = \frac{n}{\theta^n} \int_0^\theta x^n dx$$

Integramos sumándole 1 al exponente:

$$E[\hat{\theta}_n] = \frac{n}{\theta^n} \left[ \frac{x^{n+1}}{n+1} \right]_0^\theta = \frac{n}{\theta^n} \cdot \frac{\theta^{n+1}}{n+1}$$

Simplificamos las $\theta$ y llegamos a lo que pedía el profe:

$$E[\hat{\theta}_n] = \frac{n}{n+1}\theta$$

**3. Mostrar la Varianza ($Var(\hat{\theta}_n)$):**

Primero calculamos $E[\hat{\theta}_n^2]$:

$$E[\hat{\theta}_n^2] = \int_0^\theta x^2 \cdot \left( \frac{n}{\theta^n} x^{n-1} \right) dx = \frac{n}{\theta^n} \int_0^\theta x^{n+1} dx = \frac{n}{\theta^n} \left[ \frac{x^{n+2}}{n+2} \right]_0^\theta = \frac{n}{n+2}\theta^2$$

Ahora sí, Varianza = $E[X^2] - (E[X])^2$:

$$Var(\hat{\theta}_n) = \frac{n}{n+2}\theta^2 - \left( \frac{n}{n+1}\theta \right)^2$$

$$Var(\hat{\theta}_n) = \theta^2 \left[ \frac{n}{n+2} - \frac{n^2}{(n+1)^2} \right]$$

Buscamos denominador común $(n+2)(n+1)^2$:

$$Var(\hat{\theta}_n) = \theta^2 \left[ \frac{n(n+1)^2 - n^2(n+2)}{(n+2)(n+1)^2} \right]$$

Desarrollamos el binomio $(n^2+2n+1)$ y distribuimos arriba:

$$Var(\hat{\theta}_n) = \theta^2 \left[ \frac{(n^3+2n^2+n) - (n^3+2n^2)}{(n+2)(n+1)^2} \right]$$

¡Se cancela casi todo! Solo sobrevive la $n$:

$$Var(\hat{\theta}_n) = \frac{n \theta^2}{(n+1)^2(n+2)}$$

**4. Convergencia en Media Cuadrática:**

Para que un estimador converja en media cuadrática, su **Error Cuadrático Medio (ECM) tiene que tender a 0 cuando $n \to \infty$.**

Sabemos que $ECM = Var(\hat{\theta}_n) + \text{Sesgo}^2$.

El Sesgo es $E[\hat{\theta}_n] - \theta$:

$$\text{Sesgo} = \frac{n}{n+1}\theta - \theta = \frac{n\theta - (n+1)\theta}{n+1} = \frac{-\theta}{n+1}$$

Armamos el ECM sumando la Varianza y el Sesgo al cuadrado:

$$ECM = \frac{n \theta^2}{(n+1)^2(n+2)} + \frac{\theta^2}{(n+1)^2}$$

Si le tomamos el límite cuando $n \to \infty$ a esa expresión:

- En el primer término, arriba tenés $n$ (grado 1) y abajo tenés $n^3$ (grado 3). El denominador crece mucho más rápido, así que tiende a 0.
    
- En el segundo término, tenés constante arriba y $n^2$ abajo. También tiende a 0.
    

Como $\lim_{n \to \infty} ECM(\hat{\theta}_n) = 0$, **queda demostrado que $\hat{\theta}_n$ converge en media cuadrática a $\theta$.**