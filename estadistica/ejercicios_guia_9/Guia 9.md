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



Ese es el verdadero secreto del Teorema de Factorización. A la letra $\theta$ no le gusta juntarse con las $x_i$ individuales. La única forma en la que acepta compartir la caja $g(T, \theta)$ con tus datos es si estos vienen **empaquetados**.

Y justamente, las formas matemáticas de "empaquetar" una muestra entera son:

- **Sumatorias:** $\sum x_i$ o $\sum x_i^2$ (Clásico en Poisson, Normal, Bernoulli).
    
- **Productorias:** $\prod x_i$ (Clásico en Pareto, Gamma).
    
- **Extremos:** $\max(X_i)$ o $\min(X_i)$ (Clásico en Uniforme y cuando la indicadora tiene a $\theta$).
    

Cuando vos lográs agrupar todas tus $x_i$ adentro de una sumatoria o una productoria, **pierden su identidad individual**. Ya no importa cuánto valía $x_1$ o $x_2$ por separado; se fusionan en un único bloque. Ese gran bloque funcional es lo que bautizamos como tu estadístico **$T$**.

### Resumen de la regla de oro:

1. Si lográs meter a **todas** las $x_i$ que interactúan con $\theta$ adentro de un "empaque" (sumatoria, productoria, máximo, mínimo), las llamás $T$ y armás tu caja $g(T, \theta)$ feliz de la vida.
    
2. Si las $x_i$ que sobran no tienen ninguna $\theta$ cerca, las mandás a la caja del ruido: $h(\underline{x})$.
    
3. **El único escenario donde perdés** es si, después de hacer todo el álgebra, te queda una $x_i$ suelta y rebelde interactuando con $\theta$ que no pudiste meter en ninguna sumatoria ni productoria. Ahí el teorema falla y el estadístico no es suficiente.







¡Venís con un razonamiento impecable! Toda tu explicación sobre cómo funcionan las "cajas" $g$ y $h$, y por qué fallan los estadísticos malos, es perfecta. Entendiste el corazón del Teorema de Factorización.

Pero ojo con tu última conclusión, porque ahí es donde la estadística nos da una herramienta más amplia: **sí podés tener un mínimo, un máximo y reemplazarlos por letras distintas adentro de tu caja $g$.**

Ese es el concepto de un **Estadístico Suficiente Multidimensional** (o vector de estadísticos suficientes).

### El empaque múltiple: $\mathbf{T} = (T_1, T_2)$

El teorema de Fisher-Neyman no te obliga a que $T$ sea un único número (un escalar). Tu estadístico suficiente puede ser un _vector_ compuesto por varios "empaques" distintos, siempre y cuando juntos logren absorber a todas las $x_i$ que interactúan con el parámetro $\theta$.

Si armás un $T_1$ (por ejemplo, el mínimo) y un $T_2$ (por ejemplo, el máximo), tu función $g$ simplemente recibe ambos datos: $g(T_1, T_2, \theta)$.

#### El caso perfecto: Uniforme con dos parámetros

Imaginate que tenés una muestra aleatoria de una distribución Uniforme entre $a$ y $b$, es decir $X \sim U(a, b)$. Acá tenés un parámetro vectorial $\theta = (a, b)$.

Al armar la productoria de la conjunta, la indicadora te exige que todas las $x_i$ estén entre $a$ y $b$. Para "empaquetar" esa condición de toda la muestra, la matemática nos dice que basta con mirar los extremos: el valor más chico de la muestra no puede ser menor a $a$, y el valor más grande no puede superar a $b$.

Tu conjunta factorizada queda así:

$$f(\underline{x}; a, b) = \underbrace{ \frac{1}{(b - a)^n} \cdot \mathbf{1}\{\min(x_i) \ge a\} \cdot \mathbf{1}\{\max(x_i) \le b\} }_{g(T_1, T_2, a, b)} \cdot \underbrace{ 1 }_{h(\underline{x})}$$

Si te fijás, la caja $g$ aceptó sin problema a **dos** representantes distintos de la muestra:

- $T_1 = \min(x_i)$
    
- $T_2 = \max(x_i)$
    

Juntos, $\mathbf{T} = (\min(x_i), \max(x_i))$ forman tu estadístico suficiente conjunto. Las $x_i$ perdieron su identidad individual, pero en lugar de fusionarse en un solo bloque, se organizaron en dos.

### Resumen de la regla de oro extendida

La matriz no se rompe si tenés varias $T$. Se rompe **únicamente** si después de armar todos tus bloques ($T_1, T_2, \dots$) te sigue quedando alguna $x_i$ "rebelde y suelta" que interactúa con el parámetro y no pudiste meter en ninguno de tus empaques.

¿Te gustaría que probemos aplicar esto mismo pero factorizando una distribución Normal para ver cómo conviven $\sum x_i$ y $\sum x_i^2$ en la misma función $g$?






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

¡Entendido! Ese formato que mencionás, donde explicitamos a qué conjunto pertenece la variable usando el símbolo $\in$ (pertenece), suele llamarse **indicadora de conjunto** y se escribe como $\mathbf{1}\{x \in A\}$. Queda mucho más claro qué valores puede tomar $x$.

Reescribo todo el desarrollo aplicando este estilo a todas las distribuciones:

### (a) Bernoulli($p$)

**Partimos de la función original:**

$$f(x; p) = p^x (1-p)^{1-x} \cdot \mathbf{1}\{x \in \{0, 1\}\}$$

**Separar términos:** Rompemos la resta en el exponente de $(1-p)$ para aislar lo que tiene $x$ de lo que no.

$$f(x; p) = \mathbf{1}\{x \in \{0, 1\}\} \cdot p^x \cdot (1-p)^1 \cdot (1-p)^{-x}$$

**Agrupar lo suelto y juntar las $x$:** Movemos el $(1-p)$ para adelante (será nuestro $A$) y juntamos las bases que están elevadas a la $x$.

$$f(x; p) = \mathbf{1}\{x \in \{0, 1\}\} \cdot (1-p) \cdot \left( \frac{p}{1-p} \right)^x$$

**Aplicar el truco a la mezcla:** Ahora sí, metemos el último término en un exponente usando el logaritmo para bajar la $x$.

$$f(x; p) = \mathbf{1}\{x \in \{0, 1\}\} \cdot (1-p) \cdot \exp\left\{ x \ln\left( \frac{p}{1-p} \right) \right\}$$

**Identificamos las partes:**

- $h(x) = \mathbf{1}\{x \in \{0, 1\}\}$
    
- $A(p) = 1-p$
    
- $c(p) = \ln\left(\frac{p}{1-p}\right)$
    
- $T(x) = x$
    

### (b) Pascal($4, p$)

**Partimos de la función original:**

$$f(x; p) = \binom{x-1}{3} p^4 (1-p)^{x-4} \cdot \mathbf{1}\{x \in \{4, 5, 6, \dots\}\}$$

**Separar términos:** Rompemos la resta en el exponente de $(1-p)$.

$$f(x; p) = \binom{x-1}{3} \mathbf{1}\{x \in \{4, 5, 6, \dots\}\} \cdot p^4 \cdot (1-p)^{-4} \cdot (1-p)^x$$

**Agrupar lo suelto:** Juntamos todas las $p$ que no tienen ninguna $x$ al lado para armar nuestro $A(p)$.

$$f(x; p) = \binom{x-1}{3} \mathbf{1}\{x \in \{4, 5, 6, \dots\}\} \cdot \left( \frac{p}{1-p} \right)^4 \cdot (1-p)^x$$

**Aplicar el truco a la mezcla:** Usamos el logaritmo solo para el término $(1-p)^x$.

$$f(x; p) = \binom{x-1}{3} \mathbf{1}\{x \in \{4, 5, 6, \dots\}\} \cdot \left( \frac{p}{1-p} \right)^4 \cdot \exp\{ x \ln(1-p) \}$$

**Identificamos las partes:**

- $h(x) = \binom{x-1}{3} \mathbf{1}\{x \in \{4, 5, 6, \dots\}\}$
    
- $A(p) = \left(\frac{p}{1-p}\right)^4$
    
- $c(p) = \ln(1-p)$
    
- $T(x) = x$
    

### (c) Poisson($\lambda$)

**Partimos de la función original:**

$$f(x; \lambda) = \frac{e^{-\lambda} \lambda^x}{x!} \cdot \mathbf{1}\{x \in \{0, 1, 2, \dots\}\}$$

**Separar términos y agrupar:** Sacamos el $e^{-\lambda}$ (que no tiene $x$) y lo mandamos al frente.

$$f(x; \lambda) = \frac{1}{x!} \mathbf{1}\{x \in \{0, 1, 2, \dots\}\} \cdot e^{-\lambda} \cdot \lambda^x$$

**Aplicar el truco a la mezcla:** Transformamos solo la $\lambda^x$.

$$f(x; \lambda) = \frac{1}{x!} \mathbf{1}\{x \in \{0, 1, 2, \dots\}\} \cdot e^{-\lambda} \cdot \exp\{ x \ln(\lambda) \}$$

**Identificamos las partes:**

- $h(x) = \frac{1}{x!} \mathbf{1}\{x \in \{0, 1, 2, \dots\}\}$
    
- $A(\lambda) = e^{-\lambda}$
    
- $c(\lambda) = \ln(\lambda)$
    
- $T(x) = x$
    

### (d) Exponencial($\lambda$)

**Partimos de la función original:**

$$f(x; \lambda) = \lambda e^{-\lambda x} \cdot \mathbf{1}\{x \in (0, \infty)\}$$

Este es el caso más directo porque las cosas ya están en su lugar. La indicadora en este caso marca que la variable es continua y positiva.

**Acomodar visualmente:**

$$f(x; \lambda) = \mathbf{1}\{x \in (0, \infty)\} \cdot \lambda \cdot \exp\{ -\lambda x \}$$

**Identificamos las partes:**

- $h(x) = \mathbf{1}\{x \in (0, \infty)\}$
    
- $A(\lambda) = \lambda$
    
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





### El caso que SÍ vale (Tu ejemplo):

$$\mathbf{1}\{\max(x_1, \dots, x_n) < \theta\}$$

Acá las $x_i$ no están libres haciendo de las suyas. Están empaquetadas bajo el concepto de "el máximo". Como tu estadístico es justamente $T = \max(X_i)$, esto para la matemática es exactamente lo mismo que escribir:

$$\mathbf{1}\{T < \theta\}$$

La función $g$ solo ve a la variable $T$ y al parámetro $\theta$. Las $x_i$ individuales desaparecieron de la vista. Factorización exitosa.

### El caso que NO vale (Para que veas la diferencia):

Imaginate que haciendo un ejercicio te quedara esto en la caja de la $\theta$:

$$\mathbf{1}\{x_1 < \theta\}$$

Ahí sí se pudre todo. Eso no es un máximo ni un mínimo de toda la muestra, es **una $x_i$ específica (la primera) que quedó suelta** interactuando directamente con $\theta$. No podés reemplazarla por $T$, no la podés mandar a la otra caja porque tiene a $\theta$, y te traba la factorización.

Así que tu conclusión es impecable: mientras la indicadora use a las $x_i$ coordinadas como un bloque único que representa a tu $T$ (ya sea sumadas, multiplicadas, como máximo o como mínimo), la función $g(T, \theta)$ es perfectamente legal y el estadístico es suficiente. ¡Te vas al examen con el concepto pesadísimo!




![[Pasted image 20260708191948.png]]


### (a) Hallar el Estimador de Máxima Verosimilitud (EMV)

**1. Armamos la Función de Verosimilitud $L(\theta)$**

Como tenemos una muestra de tamaño $n$, multiplicamos la función de densidad original $n$ veces:

$$L(\theta) = \prod_{i=1}^n 3\theta^3 x_i^{-4} \mathbf{1}\{x_i \ge \theta\}$$

Agrupamos todo usando las propiedades de siempre:

- Multiplicar el $3$ $n$ veces es $3^n$.
    
- Multiplicar $\theta^3$ $n$ veces es $(\theta^3)^n = \theta^{3n}$.
    
- Y para la indicadora, si queremos que **todas** las $x_i$ sean mayores o iguales a $\theta$, nos alcanza con que la más chica de todas (**el mínimo**) le gane a $\theta$.
    

$$L(\theta) = 3^n \theta^{3n} \left( \prod_{i=1}^n x_i^{-4} \right) \mathbf{1}\{\min(X_i) \ge \theta\}$$

**2. El razonamiento visual (sin derivadas):**

Nosotros queremos que el resultado de $L(\theta)$ sea **lo más grande posible**.

Fijate dónde está la $\theta$ en tu ecuación principal: está arriba en el numerador como $\theta^{3n}$. A diferencia del ejercicio de la Uniforme (donde estaba dividiendo), acá **cuanto más grande sea $\theta$, más grande es la probabilidad**.

Entonces, queremos "inflar" el valor de $\theta$ lo máximo que podamos.

Pero la indicadora nos pone un techo: nos obliga sí o sí a que $\theta \le \min(X_i)$. Si probamos un $\theta$ más grande que el mínimo, la indicadora da cero y arruina todo.

Por lo tanto, el valor más grande posible que le podemos dar a $\theta$ sin romper la regla es exactamente el mínimo de la muestra:

$$\hat{\theta} = \min(X_1, \dots, X_n)$$

### (b) Esperanza y Varianza del EMV

Como nuestro estimador es un mínimo, necesitamos armar su función de densidad ($f_{min}(x)$) para poder integrarlo.

**1. Calculamos la densidad del mínimo:**

Por teoría de estadística de orden, la función de distribución acumulada del mínimo es $F_{min}(x) = 1 - [1 - F_X(x)]^n$.

Primero buscamos $F_X(x)$ integrando la densidad original:

$$F_X(x) = \int_\theta^x 3\theta^3 t^{-4} dt = 3\theta^3 \left[ \frac{t^{-3}}{-3} \right]_\theta^x = -\theta^3 \left( \frac{1}{x^3} - \frac{1}{\theta^3} \right) = 1 - \left(\frac{\theta}{x}\right)^3$$

Reemplazamos esto en la fórmula del mínimo:

$$F_{min}(x) = 1 - \left[ 1 - \left( 1 - \left(\frac{\theta}{x}\right)^3 \right) \right]^n = 1 - \left(\frac{\theta}{x}\right)^{3n}$$

Derivamos para obtener nuestra nueva función de densidad $f_{min}(x)$:

$$f_{min}(x) = \frac{d}{dx} \left( 1 - \theta^{3n} x^{-3n} \right) = - \theta^{3n} (-3n) x^{-3n-1} = 3n \theta^{3n} x^{-(3n+1)}$$

_(Válido para $x \ge \theta$)._

**2. Esperanza ($E[\hat{\theta}]$):**

$$E[\hat{\theta}] = \int_\theta^\infty x \cdot f_{min}(x) dx = \int_\theta^\infty x \cdot 3n \theta^{3n} x^{-3n-1} dx$$

Agrupamos las $x$ y sacamos las constantes afuera:

$$E[\hat{\theta}] = 3n \theta^{3n} \int_\theta^\infty x^{-3n} dx$$

Integramos:

$$E[\hat{\theta}] = 3n \theta^{3n} \left[ \frac{x^{-3n+1}}{-3n+1} \right]_\theta^\infty$$

Evaluado en infinito da $0$ (porque el exponente es negativo), y le restamos lo evaluado en $\theta$:

$$E[\hat{\theta}] = 3n \theta^{3n} \left( 0 - \frac{\theta^{-3n+1}}{-3n+1} \right) = \frac{3n \theta^{3n} \theta^{-3n+1}}{3n-1} = \frac{3n}{3n-1}\theta$$

**3. Varianza ($Var(\hat{\theta})$):**

Primero calculamos $E[\hat{\theta}^2]$ repitiendo el proceso pero poniendo una $x^2$:

$$E[\hat{\theta}^2] = \int_\theta^\infty x^2 \cdot 3n \theta^{3n} x^{-3n-1} dx = 3n \theta^{3n} \int_\theta^\infty x^{-3n+1} dx$$

$$E[\hat{\theta}^2] = 3n \theta^{3n} \left[ \frac{x^{-3n+2}}{-3n+2} \right]_\theta^\infty = 3n \theta^{3n} \left( 0 - \frac{\theta^{-3n+2}}{-3n+2} \right) = \frac{3n}{3n-2}\theta^2$$

Ahora sí, aplicamos $Var(X) = E[X^2] - (E[X])^2$:

$$Var(\hat{\theta}) = \frac{3n}{3n-2}\theta^2 - \left( \frac{3n}{3n-1}\theta \right)^2 = \theta^2 \left( \frac{3n}{3n-2} - \frac{9n^2}{(3n-1)^2} \right)$$

Buscando denominador común te queda una cuenta algebraica un poco densa que se simplifica a:

$$Var(\hat{\theta}) = \frac{3n \theta^2}{(3n-2)(3n-1)^2}$$

### (c) Convergencia en Media Cuadrática

Para probar esto, el **Error Cuadrático Medio (ECM) tiene que tender a $0$ cuando $n \to \infty$.**

Sabemos que $\text{ECM} = \text{Varianza} + \text{Sesgo}^2$.

**1. Calculamos el Sesgo:**

$$\text{Sesgo} = E[\hat{\theta}] - \theta = \frac{3n}{3n-1}\theta - \theta$$

$$\text{Sesgo} = \frac{3n\theta - \theta(3n-1)}{3n-1} = \frac{3n\theta - 3n\theta + \theta}{3n-1} = \frac{\theta}{3n-1}$$

**2. Armamos el ECM total:**

Sumamos la Varianza y el Sesgo al cuadrado:

$$\text{ECM} = \frac{3n \theta^2}{(3n-2)(3n-1)^2} + \left( \frac{\theta}{(3n-1)} \right)^2$$

Sacamos factor común $\frac{\theta^2}{(3n-1)^2}$:

$$\text{ECM} = \frac{\theta^2}{(3n-1)^2} \left( \frac{3n}{3n-2} + 1 \right)$$

Sumamos la fracción del paréntesis:

$$\text{ECM} = \frac{\theta^2}{(3n-1)^2} \left( \frac{3n + 3n - 2}{3n-2} \right) = \frac{\theta^2 (6n-2)}{(3n-1)^2 (3n-2)}$$

Podemos sacar un 2 de factor común arriba para emprolijar:

$$\text{ECM} = \frac{2\theta^2 (3n-1)}{(3n-1)^2 (3n-2)} = \frac{2\theta^2}{(3n-1)(3n-2)}$$

**3. El límite final:**

Si tomamos $\lim_{n \to \infty} \text{ECM}$:

$$\lim_{n \to \infty} \frac{2\theta^2}{(3n-1)(3n-2)} = \frac{\text{Constante}}{\infty} = 0$$

Como el límite del ECM es $0$, **queda matemáticamente demostrado que el estimador converge en media cuadrática al verdadero valor de $\theta$.**





![[Pasted image 20260708192522.png]]



### (a) Criterio de Factorización (Neyman-Fisher)

Armamos la función de probabilidad conjunta de la muestra (productoria) y separamos las cajas:

$$L(\theta, \underline{x}) = \prod_{i=1}^n \theta x_i^{-(\theta+1)} \mathbf{1}\{x_i > 1\}$$

Agrupamos aplicando las propiedades de siempre:

$$L(\theta, \underline{x}) = \theta^n \left( \prod_{i=1}^n x_i \right)^{-(\theta+1)} \prod_{i=1}^n \mathbf{1}\{x_i > 1\}$$

Desarmamos la potencia para aislar la $\theta$:

$$L(\theta, \underline{x}) = \theta^n \left( \prod_{i=1}^n x_i \right)^{-\theta} \cdot \left( \prod_{i=1}^n x_i \right)^{-1} \cdot \mathbf{1}\{\min(x_i) > 1\}$$

¡Listo el pollo! Armamos las cajas:

- **Caja $g(T, \theta)$:** Tiene el parámetro y a la muestra agrupada.
    
    $$g(T, \theta) = \theta^n \left( \prod_{i=1}^n x_i \right)^{-\theta}$$
    
- **Caja $h(\underline{x})$:** Todo lo que sobró sin $\theta$.
    
    $$h(\underline{x}) = \left( \prod_{i=1}^n x_i \right)^{-1} \cdot \mathbf{1}\{\min(x_i) > 1\}$$
    

Por lo tanto, **$T = \prod_{i=1}^n X_i$ es un estadístico suficiente.**

_(Dato: si aplicás propiedades de logaritmos en la caja $g$, vas a ver que escribir $T = \sum \ln(X_i)$ también es un estadístico suficiente y totalmente válido)._

### (b) Familia Exponencial y su Distribución

Agarramos la función de densidad original (para un solo disco) y usamos el truco de $e^{\ln(\dots)}$ en la parte donde la $x$ y la $\theta$ se están mezclando:

$$f_\theta(x) = \mathbf{1}\{x > 1\} \cdot \theta \cdot x^{-(\theta+1)}$$

Separamos el exponente:

$$f_\theta(x) = \mathbf{1}\{x > 1\} \cdot \frac{1}{x} \cdot \theta \cdot x^{-\theta}$$

Le aplicamos el logaritmo a la $x^{-\theta}$:

$$f_\theta(x) = \left( \mathbf{1}\{x > 1\} \frac{1}{x} \right) \cdot \theta \cdot \exp\{-\theta \ln(x)\}$$

¡Encaja perfecto en el molde de la Familia Exponencial $h(x) \cdot A(\theta) \cdot \exp\{c(\theta)T(x)\}$!

- $h(x) = \mathbf{1}\{x > 1\} \frac{1}{x}$
    
- $A(\theta) = \theta$
    
- $c(\theta) = -\theta$
    
- **$T(x) = \ln(x)$**
    

Como la muestra es de tamaño $n$, la teoría de Familias Exponenciales nos dice que **el estadístico suficiente global es la suma de los individuales**:

$$T(\underline{X}) = \sum_{i=1}^n \ln(X_i)$$

**¿Cuál es su distribución?**

El profe te tira el centro perfecto con el _hint_: $\ln(X) \sim \text{Exponencial}(\theta)$.

Tu estadístico $T$ es la suma de $n$ variables Exponenciales independientes. Por propiedad reproductiva, la suma de $n$ exponenciales de parámetro $\theta$ forma una distribución **Gamma**:

$$T \sim \Gamma(n, \theta)$$

### (c) Máxima Verosimilitud (MLE) y Propiedades Asintóticas

¡Vuelve nuestra amiga la derivada!

1. **Log-Verosimilitud ($\ln L$):** Agarramos la productoria del punto A, descartamos la indicadora y aplicamos logaritmo.
    
    $$\ln L(\theta) = n \ln(\theta) - (\theta+1) \sum_{i=1}^n \ln(x_i)$$
    
2. **Derivamos respecto a $\theta$ e igualamos a 0:**
    
    $$\frac{\partial \ln L}{\partial \theta} = \frac{n}{\theta} - \sum_{i=1}^n \ln(x_i) = 0$$
    
3. **Despejamos:**
    
    $$\frac{n}{\theta} = \sum_{i=1}^n \ln(x_i) \implies \hat{\theta} = \frac{n}{\sum_{i=1}^n \ln(X_i)}$$
    
    Fijate que nos quedó exactamente nuestro estadístico en el denominador: **$\hat{\theta} = \frac{n}{T}$**
    

**Mostrar que es asintóticamente insesgado:**

Tenemos que calcular la Esperanza de $\hat{\theta}$. Como $T \sim \Gamma(n, \theta)$, hacer $E[\frac{n}{T}]$ requiere saber la esperanza de una Gamma invertida. Hay una propiedad de tabla que dice que si $T \sim \Gamma(n, \theta)$, entonces $E[T^{-1}] = \frac{\theta}{n-1}$.

$$E[\hat{\theta}] = E\left[ \frac{n}{T} \right] = n \cdot E[T^{-1}] = n \cdot \frac{\theta}{n-1} = \frac{n}{n-1}\theta$$

Si tomamos el límite cuando $n \to \infty$:

$$\lim_{n \to \infty} \frac{n}{n-1}\theta = 1 \cdot \theta = \theta$$

Como en el infinito la esperanza da $\theta$, **es asintóticamente insesgado.**

**Mostrar que la varianza tiende a 0:**

Por tabla de Gamma invertida, $E[T^{-2}] = \frac{\theta^2}{(n-1)(n-2)}$.

Calculamos la varianza: $Var(\hat{\theta}) = E[\hat{\theta}^2] - (E[\hat{\theta}])^2$

$$Var(\hat{\theta}) = n^2 \frac{\theta^2}{(n-1)(n-2)} - \left( \frac{n}{n-1}\theta \right)^2$$

Buscando denominador común te queda:

$$Var(\hat{\theta}) = \frac{n^2 \theta^2}{(n-1)^2 (n-2)}$$

Si tomamos el límite cuando $n \to \infty$, arriba tenés un polinomio de grado 2 ($n^2$) y abajo uno de grado 3 ($n^3$). El denominador crece más rápido, así que:

$$\lim_{n \to \infty} Var(\hat{\theta}) = 0$$

### (d) Distribución Asintótica de $\hat{\theta}$

Acá tenés que usar un teorema fundamental de los estimadores de Máxima Verosimilitud (EMV).

El teorema dice que para muestras grandes ($n \to \infty$), cualquier EMV "se porta" como una distribución Normal centrada en el valor real del parámetro ($\theta$) y con una varianza que se calcula usando la **Información de Fisher ($I(\theta)$)**.

La fórmula de la distribución asintótica es siempre esta:

$$\hat{\theta} \approx \mathcal{N}\left( \mu = \theta, \ \sigma^2 = \frac{1}{n \cdot I(\theta)} \right)$$

El profe te regala la Información de Fisher en el hint: $I(\theta) = \theta^{-2} = \frac{1}{\theta^2}$.

Reemplazamos eso en nuestra fórmula de la varianza asintótica:

$$\sigma^2 = \frac{1}{n \cdot \left(\frac{1}{\theta^2}\right)} = \frac{\theta^2}{n}$$

Escribimos la respuesta final:

**La distribución asintótica del estimador de máxima verosimilitud es:**

$$\hat{\theta} \sim \mathcal{N}\left( \theta, \frac{\theta^2}{n} \right)$$


![[Pasted image 20260708194354.png]]

¡Este es el paso natural para subir de nivel! Hasta ahora veníamos trabajando con la Familia Exponencial de 1 parámetro. Cuando tenés 2 parámetros (como en la Normal o en la Gamma), la lógica es **exactamente la misma**, solo que el "molde" se estira un poquito para hacerle lugar a los dos.

El molde de la **Familia Exponencial a 2 parámetros** se ve así:

$$f(x; \theta_1, \theta_2) = h(x) \cdot A(\theta_1, \theta_2) \cdot \exp\{ c_1(\theta_1, \theta_2)T_1(x) + c_2(\theta_1, \theta_2)T_2(x) \}$$

Como ves, la única diferencia es que adentro del exponente ahora tenés una suma de dos bloques. Vamos a desarmar la Gamma para que encaje acá.

### 1. Escribimos la función original

La función de densidad de una distribución $\Gamma(\nu, \lambda)$ para una sola variable es:

$$f(x; \nu, \lambda) = \frac{\lambda^\nu}{\Gamma(\nu)} x^{\nu-1} e^{-\lambda x} \cdot \mathbf{1}_{\{x > 0\}}(x)$$

### 2. Aplicamos el truco del logaritmo

Como siempre, el problema lo tenemos donde la $x$ y el parámetro ($\nu$) están mezclados en una potencia: el término $x^{\nu-1}$.

Le aplicamos la vieja confiable de $e^{\ln(\dots)}$ para destrabarlo:

$$x^{\nu-1} = \exp\{ \ln(x^{\nu-1}) \} = \exp\{ (\nu-1) \ln(x) \}$$

### 3. Reemplazamos y acomodamos

Metemos eso que descubrimos adentro de nuestra función original, y también pasamos el $e^{-\lambda x}$ para que comparta el mismo techo (recordá que si multiplicás dos $e$, los exponentes se suman):

$$f(x; \nu, \lambda) = \mathbf{1}_{\{x > 0\}}(x) \cdot \frac{\lambda^\nu}{\Gamma(\nu)} \cdot \exp\{ (\nu-1) \ln(x) \} \cdot \exp\{ -\lambda x \}$$

Agrupamos todo en una sola exponencial gigante:

$$f(x; \nu, \lambda) = \mathbf{1}_{\{x > 0\}}(x) \cdot \frac{\lambda^\nu}{\Gamma(\nu)} \cdot \exp\{ (\nu-1) \ln(x) - \lambda x \}$$

### 4. Identificamos las partes

¡Fijate cómo encajó perfecto en el molde de 2 parámetros!

- $h(x) = \mathbf{1}_{\{x > 0\}}(x)$
    
- $A(\nu, \lambda) = \frac{\lambda^\nu}{\Gamma(\nu)}$
    
- **Bloque 1:** $c_1(\nu, \lambda) = \nu - 1 \quad \text{y} \quad \mathbf{T_1(x) = \ln(x)}$
    
- **Bloque 2:** $c_2(\nu, \lambda) = -\lambda \quad \text{y} \quad \mathbf{T_2(x) = x}$
    

Con esto **queda demostrado** que pertenece a la familia exponencial a 2 parámetros.

### 5. Hallar el estadístico suficiente para la muestra

Acá es donde la Familia Exponencial te regala la respuesta sin tener que transpirar.

Hay un teorema clave que dice que si una distribución pertenece a esta familia, para encontrar el estadístico suficiente de una muestra de tamaño $n$, **simplemente tenés que sumar los $T(x)$ individuales**.

Como acá tenemos dos $T(x)$, nuestro estadístico suficiente será un **vector de dos componentes** (uno para cada parámetro):

- Para el primer parámetro sumamos los $T_1$: $\sum_{i=1}^n \ln(X_i)$
    
- Para el segundo parámetro sumamos los $T_2$: $\sum_{i=1}^n X_i$
    

**Respuesta final:**

El estadístico suficiente conjunto para $(\nu, \lambda)$ es:

$$T(\underline{X}) = \left( \sum_{i=1}^n \ln(X_i), \ \sum_{i=1}^n X_i \right)$$


![[Pasted image 20260708194546.png]]\


### (a) Mostrar que pertenece a la familia exponencial a 2 parámetros

Partimos de la fórmula original (y sagrada) de la distribución Normal:

$$f(x; \mu, \sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(x-\mu)^2}{2\sigma^2} \right)$$

El secreto acá es puramente algebraico. Tenemos que desarrollar el binomio al cuadrado que está en el exponente: $(x-\mu)^2 = x^2 - 2\mu x + \mu^2$.

Reemplazamos eso arriba y distribuimos el denominador $2\sigma^2$:

$$f(x) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left( -\frac{x^2 - 2\mu x + \mu^2}{2\sigma^2} \right)$$

$$f(x) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left( -\frac{x^2}{2\sigma^2} + \frac{2\mu x}{2\sigma^2} - \frac{\mu^2}{2\sigma^2} \right)$$

Simplificamos el 2 del término del medio, y por propiedades de las potencias, separamos el término que NO tiene $x$ (el del $\mu^2$) en una exponencial aparte:

$$f(x) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left(-\frac{\mu^2}{2\sigma^2}\right) \exp\left( \frac{\mu}{\sigma^2}x - \frac{1}{2\sigma^2}x^2 \right)$$

¡Listo! Llegamos exactamente a la expresión que pedía el enunciado. Identificamos los bloques para confirmar que es Familia Exponencial:

- $T_1(x) = x$
    
- $T_2(x) = x^2$
    

### (b) Densidad conjunta y el Estadístico Suficiente $T$

Como tenemos una muestra aleatoria de tamaño $n$, la densidad conjunta $f(\underline{x}; \theta)$ es multiplicar la función de arriba $n$ veces.

- La constante de adelante multiplicada $n$ veces se eleva a la $n$.
    
- La primera exponencial multiplicada $n$ veces, suma su exponente $n$ veces (lo multiplicamos por $n$).
    
- En la segunda exponencial, al multiplicar bases iguales, los exponentes se suman. Cuando sumás las $x$, te queda $\sum x_i$. Cuando sumás las $x^2$, te queda $\sum x_i^2$.
    

Queda así:

$$f(\underline{x}; \theta) = \left(\frac{1}{\sqrt{2\pi}\sigma}\right)^n \exp\left(-\frac{n\mu^2}{2\sigma^2}\right) \exp\left( \frac{\mu}{\sigma^2}\sum_{i=1}^n x_i - \frac{1}{2\sigma^2}\sum_{i=1}^n x_i^2 \right)$$

Acá podés aplicar el Teorema de Factorización (todo esto es la caja $g(T, \theta)$ y $h(\underline{x}) = 1$), o usar directamente la propiedad de la Familia Exponencial. Como dependemos de dos sumatorias que agrupan a nuestra muestra, **nuestro estadístico suficiente es bidimensional**:

$$T = \left( \sum_{i=1}^n X_i, \ \sum_{i=1}^n X_i^2 \right)$$

### (c) El truco algebraico y el nuevo Estadístico $T'$

Primero, hagamos la demostración algebraica. Partimos del lado izquierdo y desarrollamos el binomio al cuadrado:

$$\sum_{i=1}^n (X_i - \bar{X})^2 = \sum_{i=1}^n (X_i^2 - 2X_i\bar{X} + \bar{X}^2)$$

Distribuimos la sumatoria (acordate que $\bar{X}$ es una constante, sale afuera):

$$= \sum_{i=1}^n X_i^2 - 2\bar{X} \sum_{i=1}^n X_i + \sum_{i=1}^n \bar{X}^2$$

Sabemos que $\sum X_i = n\bar{X}$, y sumar una constante $n$ veces es multiplicarla por $n$:

$$= \sum_{i=1}^n X_i^2 - 2\bar{X}(n\bar{X}) + n\bar{X}^2$$

$$= \sum_{i=1}^n X_i^2 - 2n\bar{X}^2 + n\bar{X}^2$$

$$= \sum_{i=1}^n X_i^2 - n\bar{X}^2$$

**¡Demostrado!**

**¿Por qué $T' = (\bar{X}, S^2)$ también es suficiente?**

La regla de oro de los estadísticos dice que si tenés un estadístico suficiente $T$, cualquier **función biyectiva** (uno-a-uno) de ese estadístico también es suficiente.

Fijate que a partir de las piezas de $T$ ($\sum X_i$ y $\sum X_i^2$), podés armar $\bar{X}$ y podés armar $S^2$ usando la fórmula que acabamos de demostrar. Es decir, tienen exactamente la misma información, solo que presentada de otra manera. Por lo tanto, $T'$ hereda la suficiencia.

### (d) Estimador de Máxima Verosimilitud (EMV)

Volvemos a derivar. Agarramos nuestra densidad conjunta del punto (b) y le aplicamos logaritmo natural ($\ln$):

$$\ln L(\mu, \sigma^2) = -n \ln(\sqrt{2\pi}) - \frac{n}{2} \ln(\sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^n (x_i - \mu)^2$$

Tenemos que calcular **dos derivadas parciales** e igualar ambas a cero.

**1. Derivamos respecto a $\mu$:**

$$\frac{\partial \ln L}{\partial \mu} = -\frac{1}{2\sigma^2} \sum_{i=1}^n 2(x_i - \mu)(-1) = \frac{1}{\sigma^2} \sum_{i=1}^n (x_i - \mu) = 0$$

Pasamos el $\sigma^2$ multiplicando al cero y distribuimos la sumatoria:

$$\sum_{i=1}^n x_i - \sum_{i=1}^n \mu = 0 \implies \sum_{i=1}^n x_i - n\mu = 0$$

$$\hat{\mu} = \frac{\sum x_i}{n} = \bar{X}$$

_(El EMV de la media es la media muestral)._

**2. Derivamos respecto a $\sigma^2$ (tratala como si fuera una sola letra, ej: $v$):**

$$\frac{\partial \ln L}{\partial (\sigma^2)} = -\frac{n}{2\sigma^2} + \frac{1}{2(\sigma^2)^2} \sum_{i=1}^n (x_i - \mu)^2 = 0$$

Simplificamos los $2$ de abajo y pasamos el término negativo al otro lado:

$$\frac{1}{(\sigma^2)^2} \sum_{i=1}^n (x_i - \mu)^2 = \frac{n}{\sigma^2}$$

Multiplicamos todo por $(\sigma^2)^2$ y dividimos por $n$. Además, por la Propiedad de Invarianza, reemplazamos la $\mu$ por el $\hat{\mu}$ que acabamos de averiguar ($\bar{X}$):

$$\widehat{\sigma^2} = \frac{1}{n} \sum_{i=1}^n (x_i - \bar{X})^2$$

**¡Cuidado con la trampa acá!** Fijate que el EMV de la varianza te quedó dividido por $n$, **no por $n-1$** como en la fórmula del estadístico $S^2$. Esto es recontra normal y es una pregunta teórica clásica: el EMV de la varianza normal es _sesgado_, por eso en la práctica estadística se suele preferir usar la $S^2$ muestral.


![[Pasted image 20260708195001.png]]

### 1. Plantear la distribución (La Multinomial)

Como estamos lanzando el dado $n$ veces y contando cuántas veces sale cada cara, estamos frente a una **Distribución Multinomial**. Su función de probabilidad conjunta se escribe así:

$$f(x_1, x_2, x_3, x_4) = \frac{n!}{x_1! x_2! x_3! x_4!} p_1^{x_1} p_2^{x_2} p_3^{x_3} p_4^{x_4}$$

_(Obviamente con la condición de que $x_i \ge 0$)_.

### 2. El truco de la "Dimensionalidad"

Acá está la clave del ejercicio. Si vos tirás el dado $n=10$ veces, y te digo que la cara 1 salió 2 veces, la cara 2 salió 3 veces, y la cara 3 salió 4 veces... vos ya sabés cuántas veces salió la cara 4 sin que te lo diga. ¡Salió 1 vez!

Como la cantidad total de tiros está clavada en $n$, **la cuarta variable no es libre**. Lo mismo pasa con las probabilidades: como la suma de todas las $p$ tiene que dar $100\%$ ($1$), la cuarta probabilidad tampoco es libre.

Matemáticamente, esto nos permite reescribir la cara 4 en función de las otras tres:

- $x_4 = n - x_1 - x_2 - x_3$
    
- $p_4 = 1 - p_1 - p_2 - p_3$
    

### 3. La masacre algebraica

Vamos a agarrar nuestra fórmula original y vamos a reemplazar solamente la $x_4$ del exponente (la del factorial dejala quieta porque es parte de los datos de la muestra):

$$f(\underline{x}; \underline{p}) = \frac{n!}{x_1! x_2! x_3! x_4!} p_1^{x_1} p_2^{x_2} p_3^{x_3} p_4^{(n - x_1 - x_2 - x_3)}$$

Distribuimos el exponente de $p_4$:

$$f(\underline{x}; \underline{p}) = \frac{n!}{x_1! x_2! x_3! x_4!} p_1^{x_1} p_2^{x_2} p_3^{x_3} p_4^n p_4^{-x_1} p_4^{-x_2} p_4^{-x_3}$$

Agrupamos los términos que tienen las mismas equis ($x_1$ con $x_1$, etc.) y mandamos el $p_4^n$ para adelante:

$$f(\underline{x}; \underline{p}) = \frac{n!}{x_1! x_2! x_3! x_4!} p_4^n \left(\frac{p_1}{p_4}\right)^{x_1} \left(\frac{p_2}{p_4}\right)^{x_2} \left(\frac{p_3}{p_4}\right)^{x_3}$$

### 4. La vieja confiable: $e^{\ln(\dots)}$

Ahora que tenemos todo perfectamente agrupado, le aplicamos el truco del logaritmo a todo ese bloque final para transformarlo en sumas adentro de un exponente:

$$f(\underline{x}; \underline{p}) = \frac{n!}{x_1! x_2! x_3! x_4!} \cdot p_4^n \cdot \exp\left\{ \ln\left[ \left(\frac{p_1}{p_4}\right)^{x_1} \left(\frac{p_2}{p_4}\right)^{x_2} \left(\frac{p_3}{p_4}\right)^{x_3} \right] \right\}$$

El logaritmo transforma las multiplicaciones en sumas, y baja las equis ($x_1, x_2, x_3$) multiplicando al frente de cada término:

$$f(\underline{x}; \underline{p}) = \frac{n!}{x_1! x_2! x_3! x_4!} \cdot p_4^n \cdot \exp\left\{ x_1 \ln\left(\frac{p_1}{p_4}\right) + x_2 \ln\left(\frac{p_2}{p_4}\right) + x_3 \ln\left(\frac{p_3}{p_4}\right) \right\}$$

### 5. Identificar las partes

¡Y listo! Al mirarla bien, la ecuación acaba de encajar perfectamente en el molde de una Familia Exponencial, pero con exactamente **tres bloques**.

Identificamos cada pieza para el profe:

- **El ruido de la muestra:** $h(\underline{x}) = \frac{n!}{x_1! x_2! x_3! x_4!} \mathbf{1}_{\{\sum x_i = n\}}$
    
- **La constante del parámetro:** $A(\underline{p}) = p_4^n$
    

Y los 3 parámetros de la familia exponencial:

- **Bloque 1:** $c_1(\underline{p}) = \ln\left(\frac{p_1}{p_4}\right) \quad \text{y} \quad T_1(\underline{x}) = x_1$
    
- **Bloque 2:** $c_2(\underline{p}) = \ln\left(\frac{p_2}{p_4}\right) \quad \text{y} \quad T_2(\underline{x}) = x_2$
    
- **Bloque 3:** $c_3(\underline{p}) = \ln\left(\frac{p_3}{p_4}\right) \quad \text{y} \quad T_3(\underline{x}) = x_3$
    

Como pudimos reescribir toda la función usando únicamente 3 estadísticos ($x_1, x_2, x_3$) acompañados de 3 funciones del parámetro, **queda demostrado que pertenece a una familia exponencial a 3 parámetros.**

![[Pasted image 20260708201127.png]]


### 1. Ordenar los datos de la muestra

Tenemos n=1200 ciudadanos en total, divididos en tres grupos:

- **Oficialistas (x1​):** 414 ciudadanos. (Probabilidad = p1​)
    
- **Neutrales (x3​):** 196 ciudadanos. (Probabilidad = p3​)
    
- **Opositores (x2​):** El resto. Calculamos la resta: 1200−414−196=590 ciudadanos. (Probabilidad = p2​)
    

Como la suma de las probabilidades tiene que dar el 100% (1), sabemos que la probabilidad de los neutrales no es un parámetro nuevo, sino que es: p3​=1−p1​−p2​.

### 2. Armar la Función de Verosimilitud

La función conjunta para la Multinomial con estas 3 categorías es:

L(p1​,p2​)=C⋅p1x1​​⋅p2x2​​⋅(1−p1​−p2​)x3​

_(Nota: La C representa a la combinatoria x1​!x2​!x3​!n!​. Como no tiene parámetros adentro, la dejamos como una constante C porque al derivar va a desaparecer)._

### 3. Aplicar logaritmo (ln)

Transformamos las multiplicaciones en sumas para poder derivar fácil:

lnL(p1​,p2​)=ln(C)+x1​ln(p1​)+x2​ln(p2​)+x3​ln(1−p1​−p2​)

### 4. Derivadas Parciales (Máxima Verosimilitud)

Como nos piden estimar un vector de dos parámetros (p1​,p2​), tenemos que hacer dos derivadas parciales e igualar ambas a cero.

**Derivamos respecto a p1​:**

∂p1​∂lnL​=p1​x1​​+0+x3​⋅1−p1​−p2​−1​=0

p1​x1​​=1−p1​−p2​x3​​

**Derivamos respecto a p2​:**

∂p2​∂lnL​=0+p2​x2​​+x3​⋅1−p1​−p2​−1​=0

p2​x2​​=1−p1​−p2​x3​​

### 5. El remate del sistema de ecuaciones

Fijate que si igualamos los dos resultados que obtuvimos (porque ambos son iguales al término de x3​), nos queda que las proporciones se mantienen constantes:

p1​x1​​=p2​x2​​=p3​x3​​

Sin tener que hacer todo el álgebra pesada del sistema de ecuaciones, en la materia de Estadística esta demostración te lleva directo a una conclusión teórica universal: **El estimador de máxima verosimilitud para cualquier probabilidad en una distribución Multinomial es simplemente su proporción en la muestra.** Es decir:

p^​i​=nxi​​

### 6. El cálculo final

Sabiendo esto, el ejercicio se reduce a calcular los promedios muestrales con los numeritos que averiguamos al principio:

- **Estimador para p1​ (Oficialistas):**
    
    p^​1​=1200414​=0.345
    
- **Estimador para p2​ (Opositores):**
    
    p^​2​=1200590​=0.4916...
    
    (O podés dejarlo como fracción irreducible: 12059​)
    

**Respuesta final:** El estimador por máxima verosimilitud para el vector pedido es (p^​1​,p^​2​)=(0.345, 0.4916).