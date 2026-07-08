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

La función de probabilidad es:

$$f(x; p) = p^x (1-p)^{1-x} \cdot \mathbf{1}_{\{0, 1\}}(x)$$

Aplicamos el truco de $e^{\ln(\dots)}$ a la parte que tiene el parámetro:

$$f(x; p) = \mathbf{1}_{\{0, 1\}}(x) \cdot \exp\{ \ln\left( p^x (1-p)^{1-x} \right) \}$$

El logaritmo separa la multiplicación en suma y baja las $x$:

$$f(x; p) = \mathbf{1}_{\{0, 1\}}(x) \cdot \exp\{ x \ln(p) + (1-x) \ln(1-p) \}$$

Distribuimos y agrupamos todo lo que tiene $x$:

$$f(x; p) = \mathbf{1}_{\{0, 1\}}(x) \cdot \exp\{ x \ln(p) + \ln(1-p) - x \ln(1-p) \}$$

$$f(x; p) = \mathbf{1}_{\{0, 1\}}(x) \cdot \exp\left\{ x \left[ \ln(p) - \ln(1-p) \right] + \ln(1-p) \right\}$$

Por propiedad de logaritmos, la resta es una división. Identificamos las partes:

- $h(x) = \mathbf{1}_{\{0, 1\}}(x)$
    
- $c(p) = \ln\left(\frac{p}{1-p}\right)$
    
- $T(x) = x$
    
- $d(p) = \ln(1-p)$
    

¡Pertenece a la familia exponencial!

### (b) Pascal($4, p$)

La distribución de Pascal (también conocida como Binomial Negativa) nos dice la probabilidad de necesitar $x$ intentos para lograr $4$ éxitos:

$$f(x; p) = \binom{x-1}{4-1} p^4 (1-p)^{x-4} \cdot \mathbf{1}_{\{x \ge 4\}}(x)$$

Dejamos la combinatoria afuera y le aplicamos el truco a la parte de la probabilidad:

$$f(x; p) = \binom{x-1}{3} \mathbf{1}_{\{x \ge 4\}}(x) \cdot \exp\{ \ln\left( p^4 (1-p)^{x-4} \right) \}$$

$$f(x; p) = \binom{x-1}{3} \mathbf{1}_{\{x \ge 4\}}(x) \cdot \exp\{ 4 \ln(p) + (x-4) \ln(1-p) \}$$

$$f(x; p) = \binom{x-1}{3} \mathbf{1}_{\{x \ge 4\}}(x) \cdot \exp\{ x \ln(1-p) + 4 \ln(p) - 4 \ln(1-p) \}$$

Identificamos las partes:

- $h(x) = \binom{x-1}{3} \mathbf{1}_{\{x \ge 4\}}(x)$
    
- $c(p) = \ln(1-p)$
    
- $T(x) = x$
    
- $d(p) = 4 \ln(p) - 4 \ln(1-p)$
    

¡Pertenece a la familia exponencial!

### (c) Poisson($\lambda$)

La función de probabilidad es:

$$f(x; \lambda) = \frac{e^{-\lambda} \lambda^x}{x!} \cdot \mathbf{1}_{\{x \ge 0\}}(x)$$

Separamos el denominador y aplicamos el truco arriba:

$$f(x; \lambda) = \frac{1}{x!} \mathbf{1}_{\{x \ge 0\}}(x) \cdot \exp\{ \ln\left( e^{-\lambda} \lambda^x \right) \}$$

$$f(x; \lambda) = \frac{1}{x!} \mathbf{1}_{\{x \ge 0\}}(x) \cdot \exp\{ -\lambda + x \ln(\lambda) \}$$

Identificamos las partes:

- $h(x) = \frac{1}{x!} \mathbf{1}_{\{x \ge 0\}}(x)$
    
- $c(\lambda) = \ln(\lambda)$
    
- $T(x) = x$
    
- $d(\lambda) = -\lambda$
    

¡Pertenece a la familia exponencial!

### (d) Exponencial($\lambda$)

Acá la función ya es una exponencial por naturaleza, así que el trabajo es casi nulo:

$$f(x; \lambda) = \lambda e^{-\lambda x} \cdot \mathbf{1}_{\{x > 0\}}(x)$$

Aplicamos el truco para meter esa $\lambda$ inicial adentro del exponente general:

$$f(x; \lambda) = \mathbf{1}_{\{x > 0\}}(x) \cdot \exp\{ \ln\left( \lambda e^{-\lambda x} \right) \}$$

$$f(x; \lambda) = \mathbf{1}_{\{x > 0\}}(x) \cdot \exp\{ \ln(\lambda) - \lambda x \}$$

Identificamos las partes:

- $h(x) = \mathbf{1}_{\{x > 0\}}(x)$
    
- $c(\lambda) = -\lambda$
    
- $T(x) = x$
    
- $d(\lambda) = \ln(\lambda)$