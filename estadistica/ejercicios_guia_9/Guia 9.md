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