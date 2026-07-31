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




Habiendo aclarado esos detalles técnicos, **tu deducción de por qué se usa esa fórmula es 100% correcta.**

Tu incógnita (tu parámetro a estimar) es la cantidad de bolas blancas en la urna, a la que llamaste **$b$**. Como el enunciado te dice que en total hay 6 bolas fijas, por simple descarte lógico las bolas negras van a ser **$6-b$**.

La fórmula combinatoria de la Hipergeométrica simplemente traduce tus extracciones reales a matemática pura:

- **$\binom{b}{1}$:** Representa la parte blanca. Significa _"De las $b$ bolas blancas totales que hay escondidas, yo saqué exactamente **1**_".
    
- **$\binom{6-b}{1}$:** Representa la parte negra. Significa _"De las $6-b$ bolas negras totales que hay escondidas, yo saqué exactamente **1**_".
    
- **$\binom{6}{2}$:** Es el denominador que divide a todo. Representa los casos totales. Significa _"De las 6 bolas totales que hay en la urna, extraje **2** al azar"_.


![[Pasted image 20260730235001.png]]


¡Perfecto! Este ejercicio es el ejemplo definitivo de lo que veníamos hablando sobre la **"mezcla"**.

Tenés una variable de observación **continua** (la longitud de la varilla sigue una distribución Normal), pero tu parámetro desconocido $\mu$ es **discreto** (solo puede valer 10 o 14).

Vamos a resolverlo aplicando la lógica de las dos etapas (Inferencia y Predicción) usando el famoso diagrama de árbol.

### Etapa 1: Encontrar la distribución "A Posteriori" (Inferencia)

Nuestra primera tarea es actualizar las probabilidades de $\mu$ usando la muestra que observamos ($x = 12.1$).

La distribución base es $X\vert{}\mu \sim N(\mu, \sigma=2)$. La fórmula de densidad de la Normal es:

$$f(x\vert{}\mu) = \frac{1}{2\sqrt{2\pi}} e^{-\frac{1}{2} \left( \frac{x-\mu}{2} \right)^2}$$

Como en la fórmula de Bayes la constante $\frac{1}{2\sqrt{2\pi}}$ va a estar arriba y abajo, se va a cancelar. Podemos trabajar directamente con la parte exponencial (la proporcionalidad):

**1. Calculamos la verosimilitud (la rama) para cada $\mu$:**

- **Si $\mu = 10$:**
    
    $f(12.1 \vert{} \mu=10) \propto e^{-\frac{1}{2} \left( \frac{12.1-10}{2} \right)^2} = e^{-\frac{1}{2} (1.05)^2} = e^{-0.55125} \approx 0.5762$
    
- **Si $\mu = 14$:**
    
    $f(12.1 \vert{} \mu=14) \propto e^{-\frac{1}{2} \left( \frac{12.1-14}{2} \right)^2} = e^{-\frac{1}{2} (-0.95)^2} = e^{-0.45125} \approx 0.6368$
    

**2. Multiplicamos por la probabilidad A Priori (completamos la rama):**

- **Rama $\mu=10$:** $0.5762 \cdot 0.25 = 0.14405$
    
- **Rama $\mu=14$:** $0.6368 \cdot 0.75 = 0.4776$
    

**3. Sumamos para la Probabilidad Total y dividimos (A Posteriori):**

- **Prob. Total (Denominador):** $0.14405 + 0.4776 = 0.62165$
    
- $P(\mu=10 \vert{} X=12.1) = \frac{0.14405}{0.62165} \approx$ **$0.2317$**
    
- $P(\mu=14 \vert{} X=12.1) = \frac{0.4776}{0.62165} \approx$ **$0.7683$**
    

_Nota lógica:_ Viste una varilla de 12.1 cm. Como 12.1 está más cerca de 14 que de 10 (en términos relativos a cómo arrancó la a priori), la matemática ajustó tu creencia y ahora estás casi un 77% seguro de que el lote viene de $\mu=14$.

### Etapa 2: Probabilidad Predictiva (El futuro)

Ahora te piden predecir la probabilidad de que una **nueva varilla** ($X_{nueva}$) mida más de 13 cm.

Acá armamos el segundo árbol, usando las nuevas probabilidades "A Posteriori" como base de las ramas y calculando la probabilidad del evento $P(X_{nueva} > 13)$ estandarizando a la variable $Z$ clásica de la Normal.

**1. Calculamos el evento para cada escenario (usando tabla Normal):**

- **Si $\mu = 10$:**
    
    $P(X > 13 \vert{} \mu=10) = P\left(Z > \frac{13-10}{2}\right) = P(Z > 1.5) = 1 - \Phi(1.5) = 1 - 0.9332 = 0.0668$
    
- **Si $\mu = 14$:**
    
    $P(X > 13 \vert{} \mu=14) = P\left(Z > \frac{13-14}{2}\right) = P(Z > -0.5) = 1 - \Phi(-0.5) = \Phi(0.5) = 0.6915$
    

**2. Probabilidad Total (Sumamos el árbol):**

Multiplicamos la probabilidad del evento en cada rama por el "peso" (probabilidad a posteriori) de esa rama:

$$P(X_{nueva} > 13 \vert{} X=12.1) = (0.0668 \cdot 0.2317) + (0.6915 \cdot 0.7683)$$

$$P(X_{nueva} > 13 \vert{} X=12.1) = 0.01548 + 0.53127$$

$$P(X_{nueva} > 13 \vert{} X=12.1) \approx \mathbf{0.5467}$$

Hay aproximadamente un **54.67%** de probabilidad de que la próxima varilla que saques mida más de 13 cm.

¿Ves cómo todo se reduce siempre al mismo esqueleto metodológico sin importar qué distribución fea te pongan?



¡Sí, totalmente! Y de hecho... **¡eso es exactamente lo que hicimos con esos números!**

Quizás al reemplazar directamente por los valores numéricos me salté el paso de escribirte la fórmula teórica completa con las letras y por eso no la reconociste, pero tu cabeza está razonando la estructura perfecta.

Vamos a ponerle "nombre y apellido" a esos números para que veas que es literalmente la fórmula que acabás de escribir (que es la misma del "machete" de la foto resumen que me pasaste antes).

La fórmula teórica de la probabilidad total (tu sumatoria de ramas) es:

$$P(X_{nueva} > 13 \vert{} X=12.1) = \sum_{\mu} P(X_{nueva} > 13 \vert{} \mu) \cdot P(\mu \vert{} X=12.1)$$

Si desarmamos esa sumatoria para las dos ramas de tu árbol, queda así:

- **Para la Rama $\mu=10$:**
    
    La estructura $P(X > \text{algo} \vert{} \mu) \cdot P(\mu \vert{} \text{muestra})$ se traduce en:
    
    $P(X_{nueva} > 13 \vert{} \mu=10) \cdot P(\mu=10 \vert{} X=12.1)$
    
    Que son exactamente los números que calculamos: **$(0.0668 \cdot 0.2317)$**
    
- **Para la Rama $\mu=14$:**
    
    La estructura $P(X > \text{algo} \vert{} \mu) \cdot P(\mu \vert{} \text{muestra})$ se traduce en:
    
    $P(X_{nueva} > 13 \vert{} \mu=14) \cdot P(\mu=14 \vert{} X=12.1)$
    
    Que son exactamente los números que calculamos: **$(0.6915 \cdot 0.7683)$**
    

Como ves, el primer factor de cada paréntesis es la probabilidad del evento futuro condicionado al parámetro (que lo sacamos estandarizando con la tabla $Z$ de la Normal). El segundo factor de cada paréntesis es el peso de la rama (tu distribución "a posteriori" que sacamos con Bayes en la Etapa 1).

¡Así que tu regla mental es 100% correcta! Siempre es esa misma estructura. Perdón si el salto directo a la cuenta te hizo dudar, pero el concepto lo tenés dominado a la perfección.








¡Te entiendo perfecto! Es súper común marearse cuando hay que hacer tantos cálculos intermedios antes de llegar a lo que realmente te pide el enunciado.

Vos querés ir directo al grano y responder la pregunta final: calcular la probabilidad predictiva **$P(X_{nueva} > 13 \vert{} X=12.1)$**.

Para entender por qué hicimos esos 3 pasos, volvé a mirar la fórmula de tu "diagrama de árbol" que vos mismo armaste espectacularmente en el mensaje anterior:

$$P(X_{nueva} > 13 \vert{} X=12.1) = \sum_{\mu} \underbrace{P(X_{nueva} > 13 \vert{} \mu)}_{\text{Ingrediente 1}} \cdot \underbrace{P(\mu \vert{} X=12.1)}_{\text{Ingrediente 2}}$$

Para poder resolver esa multiplicación final, necesitás dos ingredientes:

### El Ingrediente 1: $P(X_{nueva} > 13 \vert{} \mu)$

Esto es "fácil" de conseguir. Como sabés que las varillas siguen una distribución Normal, simplemente estandarizás (pasás a $Z$) y buscás en la tabla para cada valor de $\mu$.

### El Ingrediente 2: $P(\mu \vert{} X=12.1)$

¡Acá está el problema! El enunciado **no te da este dato**. El enunciado solo te da las probabilidades _viejas_ o "a priori" ($0.25$ para $\mu=10$ y $0.75$ para $\mu=14$).

Pero vos no podés usar las probabilidades viejas en tu fórmula final, tenés que usar las probabilidades **actualizadas** con el dato de la varilla de 12.1 cm que acabás de medir.

### ¿Qué son entonces esos 3 pasos que citaste?

Esos 3 pasos son simplemente la **"cocina"** (el Teorema de Bayes) necesaria para conseguir el Ingrediente 2.

1. **Paso 1:** Evalúa qué tan probable era ver una varilla de $12.1$ cm bajo cada escenario.
    
2. **Paso 2:** Cruza esa evaluación con tus creencias viejas ($0.25$ y $0.75$).
    
3. **Paso 3:** Ajusta los porcentajes para darte tus **nuevas creencias**.
    

El único objetivo de toda esa cuenta fea que citaste es obtener los valores **$0.2317$** y **$0.7683$**.

Una vez que Bayes te entrega esos dos números actualizados, la "Etapa 1" termina. Agarrás esos números, los enchufás en el Ingrediente 2 de tu fórmula del árbol, los multiplicás por los valores de la tabla Normal (Ingrediente 1), sumás todo y llegás a tu resultado final.

Es como en la programación de tus proyectos: antes de que la función principal pueda hacer el `return` final, a veces necesitás llamar a una función auxiliar para que procese y te prepare una de las variables. Acá, esos 3 pasos son tu función auxiliar.






¡Con todo gusto! Vamos a desarmar todo el proceso lógicamente para que te quede el esqueleto perfecto de cómo se encaran estos problemas de principio a fin.

Nuestra meta es armar y resolver esta sumatoria (el diagrama de árbol):

$$P(X_{nueva} > 13 \vert{} X=12.1) = \sum_{\mu} P(X_{nueva} > 13 \vert{} \mu) \cdot P(\mu \vert{} X=12.1)$$

### Parte 1 (El Ingrediente 1): La probabilidad del evento futuro

Acá el objetivo es calcular **$P(X_{nueva} > 13 \vert{} \mu)$**.

Como el enunciado te dice que la longitud de las varillas sigue una distribución Normal y te da el desvío estándar ($\sigma = 2$), resolvemos esto usando la estandarización clásica de la estadística: pasamos nuestra variable $X$ a la variable $Z$ para poder buscarla en la tabla de probabilidades.

La fórmula de estandarización es: $Z = \frac{X - \mu}{\sigma}$

**1. Calculamos para el caso $\mu=10$:**

- Planteamos la probabilidad: $P\left(Z > \frac{13 - 10}{2}\right)$
    
- Resolvemos la fracción: $P(Z > 1.5)$
    
- Como la tabla Normal te da las áreas menores ($<$), aplicamos el complemento: $1 - \Phi(1.5)$
    
- Buscamos en la tabla y restamos: $1 - 0.9332 = \mathbf{0.0668}$
    

**2. Calculamos para el caso $\mu=14$:**

- Planteamos la probabilidad: $P\left(Z > \frac{13 - 14}{2}\right)$
    
- Resolvemos la fracción: $P(Z > -0.5)$
    
- Por propiedades de simetría de la Normal (y para sacar el negativo), sabemos que $P(Z > -0.5)$ es equivalente a $\Phi(0.5)$.
    
- Buscamos el valor directo en la tabla: $\mathbf{0.6915}$
    

### Parte 2 (El Ingrediente 2): La distribución A Posteriori

Acá el objetivo es conseguir **$P(\mu \vert{} X=12.1)$**.

No podemos usar los porcentajes iniciales (0.25 y 0.75) en la fórmula final. Tenemos que usar el Teorema de Bayes para calibrarlos basándonos en el hecho de que observamos una varilla que midió exactamente 12.1 cm.

**1. Evaluar la Verosimilitud (La fórmula de la distribución)**

Usamos la función de densidad de la Normal, evaluando nuestro dato real ($12.1$). Como las constantes de la fórmula se van a simplificar en la división de Bayes, podemos usar solo la parte proporcional: $e^{-\frac{1}{2} \left( \frac{X-\mu}{\sigma} \right)^2}$

- Para $\mu=10$: $e^{-\frac{1}{2} \left( \frac{12.1-10}{2} \right)^2} \approx 0.5762$
    
- Para $\mu=14$: $e^{-\frac{1}{2} \left( \frac{12.1-14}{2} \right)^2} \approx 0.6368$
    

**2. Multiplicar por las creencias "A Priori"**

A los resultados anteriores los multiplicamos por la probabilidad inicial que nos dio el enunciado para cada $\mu$.

- Rama $\mu=10$: $0.5762 \cdot 0.25 = 0.14405$
    
- Rama $\mu=14$: $0.6368 \cdot 0.75 = 0.4776$
    

**3. Sumar para sacar el Denominador (Probabilidad Total)**

Sumamos los dos resultados del paso anterior. Este número representa la probabilidad total de que una varilla mida 12.1 cm bajo cualquier escenario.

- Suma: $0.14405 + 0.4776 = 0.62165$
    

**4. Calcular el porcentaje final actualizado**

Dividimos lo que vale cada rama individual por el total que calculamos en el Paso 3.

- Para $\mu=10$: $\frac{0.14405}{0.62165} = \mathbf{0.2317}$
    
- Para $\mu=14$: $\frac{0.4776}{0.62165} = \mathbf{0.7683}$
    

### El Ensamblaje Final

¡Listo! Ya procesaste por separado las dos partes que pedía la sumatoria original. Ahora solo queda reemplazar los números, multiplicar las ramas y sumarlas para obtener la predicción total.

**Rama del 10:** (Ingrediente 1 $\cdot$ Ingrediente 2)

$$0.0668 \cdot 0.2317 = 0.01548$$

**Rama del 14:** (Ingrediente 1 $\cdot$ Ingrediente 2)

$$0.6915 \cdot 0.7683 = 0.53127$$

**Sumamos todo (Probabilidad Predictiva Final):**

$$0.01548 + 0.53127 \approx \mathbf{0.5467}$$



![[Pasted image 20260731015805.png]]

¡Este ejercicio es genial porque te hace aplicar todo lo que venimos charlando pero con un giro en la "Etapa 2" (la predicción)!

En lugar de pedirte una probabilidad pura (como "probabilidad de que sea mayor a 13"), te pide la **media** (la esperanza matemática) de una variable futura.

Vamos a resolverlo respetando nuestras dos etapas clásicas:

### Etapa 1: Encontrar la distribución "A Posteriori" de $p$

Primero, traducimos el enunciado a variables estadísticas:

- **El Parámetro ($p$):** La proporción de termos defectuosos. Es discreto: $p \in \{0.1, 0.9\}$.
    
- **La "A Priori":** $P(p=0.1) = 0.5$ y $P(p=0.9) = 0.5$.
    
- **La Muestra ($X$):** Se extraen termos hasta encontrar el primer defectuoso en la **tercera** extracción ($X=3$).
    
    - _Dato estadístico:_ Esto se modela con una distribución **Geométrica**, cuya fórmula para la extracción $x$ es: $(1-p)^{x-1} \cdot p$. (Básicamente: dos termos sanos y el tercero roto).
        

Ahora, hacemos nuestra "cocina" (el Teorema de Bayes) para actualizar las probabilidades del parámetro $p$:

**1. Calculamos la verosimilitud (la rama) para cada $p$:**

- **Si $p = 0.1$:**
    
    $P(X=3 \vert{} p=0.1) = (1 - 0.1)^2 \cdot 0.1 = 0.9^2 \cdot 0.1 = 0.81 \cdot 0.1 = 0.081$
    
- **Si $p = 0.9$:**
    
    $P(X=3 \vert{} p=0.9) = (1 - 0.9)^2 \cdot 0.9 = 0.1^2 \cdot 0.9 = 0.01 \cdot 0.9 = 0.009$
    

**2. Multiplicamos por la probabilidad A Priori:**

- Rama $p=0.1$: $0.081 \cdot 0.5 = 0.0405$
    
- Rama $p=0.9$: $0.009 \cdot 0.5 = 0.0045$
    

**3. Sumamos para la Probabilidad Total (Denominador):**

- $P(X=3) = 0.0405 + 0.0045 = 0.045$
    

**4. Dividimos para sacar la "A Posteriori":**

- $P(p=0.1 \vert{} X=3) = \frac{0.0405}{0.045} =$ **$0.9$**
    
- $P(p=0.9 \vert{} X=3) = \frac{0.0045}{0.045} =$ **$0.1$**
    

_(Pausa lógica: Tiene todo el sentido del mundo. Si tuviste que esperar hasta el tercer intento para encontrar un defecto, es porque los defectos son raros. Por eso la matemática te dice que ahora estás 90% seguro de que la proporción real de defectuosos es baja)._

### Etapa 2: Predecir el futuro (La Esperanza Muestral)

El enunciado te pide "estimar la media de la cantidad de termos defectuosos que se encontrarán en otros 100000 termos".

- **Tu variable futura ($Y$):** Cantidad de defectuosos en una muestra de tamaño $n = 100000$.
    
- Esta variable sigue una distribución **Binomial**: $Y \sim \text{Binomial}(n, p)$.
    
- La "media" (esperanza) de una Binomial es la fórmula clásica: $E[Y] = n \cdot p$.
    

Como el parámetro $p$ sigue siendo una incógnita (no es un número fijo, sino que tiene su propia distribución de probabilidades que calculamos en la Etapa 1), aplicamos la ley de esperanza total:

$$E[Y \vert{} X=3] = n \cdot E[p \vert{} X=3]$$

Para resolver esto, primero calculamos $E[p \vert{} X=3]$ (que no es otra cosa que el estimador de Bayes bajo pérdida cuadrática que vimos en ejercicios anteriores):

**1. Calculamos la Esperanza de $p$ a posteriori:**

$$E[p \vert{} X=3] = (0.1 \cdot 0.9) + (0.9 \cdot 0.1)$$

$$E[p \vert{} X=3] = 0.09 + 0.09 = 0.18$$

**2. Multiplicamos por la muestra futura ($n$):**

$$E[Y \vert{} X=3] = 100000 \cdot 0.18$$

$$E[Y \vert{} X=3] = \mathbf{18000}$$

La estimación final es que encontrarás **18000** termos defectuosos en el próximo lote.





¡Es una duda excelente! Es uno de los conceptos más abstractos de la materia, así que es súper normal que haga ruido.

Para responder a tu pregunta rápido: **No es que "reemplazás a $Y$", sino que la Ley de Esperanza Total te permite calcular un problema imposible dividiéndolo en varios problemas fáciles.**

Pensalo con esta lógica intuitiva, olvidándonos por un segundo de las fórmulas raras:

Vos querés saber cuántos termos rotos vas a tener en un lote de 100.000 (esa es tu $Y$).

Como no tenés idea de cuál es la verdadera proporción de rotos (tu parámetro $p$ es una incógnita), estás trabado. No podés calcular el futuro si no conocés la regla del juego.

La Ley de Esperanza Total te dice: _"No te bloquees. Hacé de cuenta que SÍ sabés cuánto vale $p$, calculá el resultado para cada caso, y después promediá todos esos resultados"_.

Fijate cómo funciona esto con los números de tu ejercicio:

### Paso 1: Imaginar que conocemos el parámetro (El núcleo)

Vamos a calcular la esperanza de $Y$ asumiendo que conocemos $p$ (esto es $E[Y\vert{}p]$):

- **Escenario A (Si $p=0.1$):** Si la fábrica tiene un 10% de fallas, en 100.000 termos vos _esperarías_ encontrar **10.000** rotos.
    
- **Escenario B (Si $p=0.9$):** Si la fábrica tiene un 90% de fallas, en 100.000 termos vos _esperarías_ encontrar **90.000** rotos.
    

¡Esa cuenta fácil que hiciste mentalmente ($100000 \cdot 0.1$ y $100000 \cdot 0.9$) es exactamente reemplazar por $n \cdot p$! Es la esperanza de la Binomial.

### Paso 2: Promediar usando tus probabilidades "A Posteriori"

Ahora tenés dos futuros posibles (10.000 rotos o 90.000 rotos). ¿Cuál elegís? Ninguno. La Ley de Esperanza Total te hace **promediar** esos futuros usando la confianza que le tenés a cada escenario (los porcentajes que calculaste con Bayes):

- Estás un **90%** seguro de que el Escenario A es el real ($P=0.9$).
    
- Estás un **10%** seguro de que el Escenario B es el real ($P=0.1$).
    

Entonces, multiplicás cada futuro por su probabilidad:

$$Esperanza Total = (10.000 \cdot 0.90) + (90.000 \cdot 0.10)$$

$$Esperanza Total = 9.000 + 9.000 = \mathbf{18.000}$$

### ¿Qué dice matemáticamente la Ley?

La fórmula que escribimos antes ($E[Y \vert{} X] = n \cdot E[p \vert{} X]$) es literalmente un atajo algebraico para hacer esta misma cuenta que te acabo de mostrar.

La Ley de Esperanza Total afirma que **el promedio de los promedios es el promedio total**. Como $p$ es una incógnita aleatoria, vos no podés calcular $E[Y]$ de una sola vez. Lo que hacés es calcular la esperanza de $Y$ condicionada a cada valor de $p$ ($E[Y\vert{}p]$), y luego le calculás la esperanza a eso.

Por eso el núcleo de la fórmula se transformó en $n \cdot p$. Porque al condicionar sobre $p$, $p$ deja de ser una incógnita por un segundo y se comporta como una constante para que puedas resolver la Binomial.




¡Exactamente! Lo escribiste a la perfección.

Esa es la notación matemática rigurosa y formal de todo lo que acabamos de charlar.

Fijate cómo cada parte de tu fórmula se traduce literalmente a los pasos que hicimos recién:

1. **El núcleo interno $E[Y\vert{}p]$:** Es el "Paso 1", donde hacés de cuenta que conocés la proporción $p$ y resolvés el problema fácil. Como la variable $Y$ es una Binomial, esta esperanza interna se resuelve simplemente como $n \cdot p$.
    
2. **La capa externa $E[\dots \vert{} X=3]$:** Es el "Paso 2". Le estás diciendo a la fórmula _"ahora agarrá eso que resolviste adentro y promediámelo usando las probabilidades reales que descubrimos cuando observamos que $X=3$"_.
    

Si unís todo, la cadena lógica y algebraica que tu cabeza acaba de deducir es esta:

$$E[Y \vert{} X=3] = E \big[ E[Y\vert{}p] \big\vert{} X=3 \big]$$

Reemplazás la parte de adentro por su resultado de la Binomial:

$$E[Y \vert{} X=3] = E \big[ n \cdot p \big\vert{} X=3 \big]$$

Y como la $n$ es una constante (los 100.000 termos fijos), la matemática te permite sacarla afuera de la esperanza, dejándote exactamente la fórmula que usamos para resolver el ejercicio:

$$E[Y \vert{} X=3] = n \cdot E[p \vert{} X=3]$$

¡Es brillante! Pasaste de tener una duda conceptual a escribir vos mismo la demostración formal del teorema. Entender la estadística así, desde la lógica y no desde la memoria, es lo que te asegura aprobar el parcial.





![[Pasted image 20260731152118.png]]


¡Me encanta la idea! Vamos a hacer el ejercicio completo desde cero, armando cada pieza del rompecabezas como si estuviéramos escribiendo la demostración paso a paso en la hoja del parcial, sin guardarnos ningún truco algebraico.

### Paso Cero: La "Cocina" (Armar la distribución A Posteriori)

Antes de responder cualquier inciso, necesitamos saber cuál es nuestra nueva distribución de probabilidad para el parámetro $p$. Arrancamos con el Teorema de Bayes para variables continuas:

$$f(p \vert{} x) = \frac{P(x \vert{} p) \cdot f(p)}{\text{Constante del denominador}}$$

Como el denominador es solo un número para que todo sume 1, trabajamos con proporciones:

$$\text{Posteriori} \propto \text{Verosimilitud} \cdot \text{Priori}$$

**1. Desarrollamos la Verosimilitud (Binomial):**

Observar $x$ caras en $n$ tiros sigue una Binomial. Separamos la parte constante de la parte que tiene $p$ (el núcleo):

$$P(x \vert{} p) = \left[ \binom{n}{x} \right] \cdot \left[ p^x (1-p)^{n-x} \right]$$

**2. Desarrollamos la Priori (Beta):**

El enunciado nos dice que $p \sim \text{Beta}(\nu_1, \nu_2)$. Separamos su constante de su núcleo:

$$f(p) = \left[ \frac{1}{B(\nu_1, \nu_2)} \right] \cdot \left[ p^{\nu_1 - 1} (1-p)^{\nu_2 - 1} \right]$$

**3. Multiplicamos (Bayes) y aplicamos álgebra:**

Metemos todo en la multiplicación y juntamos las bases iguales ($p$ con $p$, y $1-p$ con $1-p$). Al multiplicar bases iguales, los exponentes se suman:

$$\text{Posteriori} \propto \left( \text{Constantes gigantes} \right) \cdot \left( p^x \cdot p^{\nu_1 - 1} \right) \cdot \left( (1-p)^{n-x} \cdot (1-p)^{\nu_2 - 1} \right)$$

$$\text{Posteriori} \propto p^{x + \nu_1 - 1} (1-p)^{n - x + \nu_2 - 1}$$

Al ver este núcleo, reconocemos matemáticamente que la nueva distribución es una **Beta** con parámetros actualizados:

- $\alpha_{nueva} = x + \nu_1$
    
- $\beta_{nueva} = n - x + \nu_2$
    

### (a) Hallar la media a posteriori y mostrar dónde está comprendida

La fórmula teórica de la esperanza (media) para cualquier distribución Beta$(\alpha, \beta)$ es:

$$E[p] = \frac{\alpha}{\alpha + \beta}$$

**1. Calculamos nuestra media:**

Reemplazamos con nuestros parámetros nuevos:

$$\hat{p}_{post} = \frac{x + \nu_1}{(x + \nu_1) + (n - x + \nu_2)}$$

Las $x$ del denominador se cancelan ($x - x = 0$), dejándonos nuestra respuesta:

$$\mathbf{\hat{p}_{post} = \frac{x + \nu_1}{n + \nu_1 + \nu_2}}$$

**2. Demostración del "Promedio Ponderado":**

Nos piden demostrar que este resultado es un punto medio entre la frecuencia de la muestra ($x/n$) y la media a priori ($\nu_1 / (\nu_1 + \nu_2)$).

Para eso, reescribimos nuestra fracción separándola estratégicamente en dos bloques, multiplicando y dividiendo por $n$ y por $(\nu_1+\nu_2)$ para forzar que aparezcan esos términos:

$$\hat{p}_{post} = \left( \frac{n}{n + \nu_1 + \nu_2} \right) \cdot \left( \frac{x}{n} \right) + \left( \frac{\nu_1 + \nu_2}{n + \nu_1 + \nu_2} \right) \cdot \left( \frac{\nu_1}{\nu_1 + \nu_2} \right)$$

Fijate la magia de esa separación:

- El término $(x/n)$ es tu **muestra**.
    
- El término $(\nu_1 / (\nu_1+\nu_2))$ es tu **priori**.
    
- Los paréntesis grandes que los multiplican son sus **pesos**. Si sumás esos dos pesos, dan exactamente $1$.
    

Matemáticamente, esto se llama "combinación convexa". Cualquier cosa que sea una combinación convexa de $A$ y $B$ siempre, obligatoriamente, da un número que está metido entre $A$ y $B$. ¡Demostrado!

### (b) Comportamiento asintótico de la varianza

La fórmula teórica de la varianza para una Beta$(\alpha, \beta)$ es:

$$V[p] = \frac{\alpha \cdot \beta}{(\alpha + \beta)^2 (\alpha + \beta + 1)}$$

**1. Reemplazamos con nuestros parámetros:**

$$V_{post} = \frac{(x + \nu_1)(n - x + \nu_2)}{(n + \nu_1 + \nu_2)^2 (n + \nu_1 + \nu_2 + 1)}$$

**2. Aplicamos el límite asintótico ($n \to \infty$):**

Asintótico significa "qué pasa cuando los tiros ($n$) y los éxitos ($x$) son gigantes".

Imaginate que $n$ es $1.000.000$. Sumarle un número chiquitito como $\nu_1$, $\nu_2$ o $1$ no cambia matemáticamente la escala del número. Entonces, para ver la estructura, "tachamos" esas constantes despreciables:

$$V_{asintotica} \approx \frac{(x)(n - x)}{(n)^2 (n)}$$

$$V_{asintotica} \approx \frac{x(n - x)}{n^3}$$

**3. Acomodamos el álgebra:**

Desarmamos el $n^3$ del denominador en tres pedazos ($n \cdot n \cdot n$) y los repartimos para que quede idéntico a lo que pide el enunciado:

$$V_{asintotica} \approx \frac{x}{n} \cdot \frac{n - x}{n} \cdot \frac{1}{n}$$

Separamos la fracción del medio: $\frac{n-x}{n} = \frac{n}{n} - \frac{x}{n} = 1 - \frac{x}{n}$

$$\mathbf{V_{asintotica} \approx \frac{(x/n) (1 - x/n)}{n}}$$

¡Demostrado exactamente igual a la foto!

### (c) Estimar la probabilidad del siguiente tiro

Acá usamos la **Ley de Esperanza Total** (la misma que usamos para los termos).

Como el siguiente tiro es una variable Bernoulli (cara o ceca) y la probabilidad de sacar cara es $p$, la probabilidad predictiva es simplemente la esperanza matemática de $p$ condicionada a la muestra:

$$P(\text{Próxima es Cara} \vert{} \text{muestra}) = E[p \vert{} \text{muestra}]$$

Como a esa esperanza a posteriori ya la calculamos en el inciso (a), la respuesta es directa y no hay que hacer ninguna cuenta nueva:

$$\mathbf{P(\text{Cara}) = \frac{x + \nu_1}{n + \nu_1 + \nu_2}}$$

### (d) El acertijo final

Acá el ejercicio nos da condiciones y nos pide despejar $n$. Traducimos el texto a matemáticas puras usando la fórmula que sacamos en (c):

- **"Moneda equilibrada a priori":** Esto significa que la priori es simétrica. Entonces $\nu_1 = \nu_2$. Para no marearnos, llamémoslas a ambas simplemente $\nu$.
    
- **"Se observaron $n - 1$ caras":** Nuestra $x$ observable ahora vale exactamente $n - 1$.
    
- **"Probabilidades 2 a 1 a favor de cara":** Significa que el suceso cara tiene probabilidad doble. Matemáticamente, eso es un $2/3$ (y un $1/3$ para ceca).
    

**1. Armamos la ecuación reemplazando en nuestra fórmula:**

$$\frac{(n - 1) + \nu}{n + \nu + \nu} = \frac{2}{3}$$

$$\frac{n - 1 + \nu}{n + 2\nu} = \frac{2}{3}$$

**2. Despejamos la $n$:**

Pasamos los denominadores multiplicando cruzado:

$$3 \cdot (n - 1 + \nu) = 2 \cdot (n + 2\nu)$$

Hacemos distributiva:

$$3n - 3 + 3\nu = 2n + 4\nu$$

Juntamos las $n$ de un lado y el resto del otro:

$$3n - 2n = 4\nu - 3\nu + 3$$

$$\mathbf{n = \nu + 3}$$

Ese es tu resultado final. Dependiendo del valor exacto que tenga la priori ($\nu$), vas a necesitar esa cantidad de tiros más 3. Si asumiéramos el clásico valor de ignorancia total ($\nu = 1$), necesitarías $n = 4$ tiros.




![[Pasted image 20260731171759.png]]



¡Este ejercicio es un clásico espectacular! Es la demostración matemática perfecta de lo que pasa en la vida real cuando dos personas tienen sesgos iniciales muy fuertes ("la grieta") y miran los mismos datos.

Vamos a resolverlo paso a paso, armando primero la "cocina" de las distribuciones como hicimos en el ejercicio anterior.

### Paso Cero: Identificar los modelos (La "Cocina")

Tenemos que estimar la proporción $p$ (un parámetro continuo entre 0 y 1).

**1. La Verosimilitud (La muestra):**

Si encuestamos a $n$ vecinos y $x$ están irritados, esto es un experimento de éxitos y fracasos. Es decir, sigue una distribución **Binomial**, cuyo núcleo ya conocemos:

$$\text{Verosimilitud} \propto p^x(1-p)^{n-x}$$

**2. Identificar las Priori de los especialistas:**

Las fórmulas que nos dan para los especialistas son funciones de densidad. Si recordamos que el núcleo de una distribución $\text{Beta}(\alpha, \beta)$ es $p^{\alpha-1}(1-p)^{\beta-1}$, podemos deducir qué distribución eligió cada uno:

- **Especialista 1:** $f_1(p) = 10(1-p)^9$. Si acomodamos los exponentes, esto es $p^0(1-p)^9$. Por lo tanto, $\alpha-1=0$ y $\beta-1=9$.
    
    Este especialista está usando una priori **$\text{Beta}(1, 10)$**.
    
- **Especialista 2:** $f_2(p) = 10p^9$. Acomodando, es $p^9(1-p)^0$.
    
    Este especialista está usando una priori **$\text{Beta}(10, 1)$**.
    

**3. Armar las distribuciones A Posteriori:**

Como la Binomial y la Beta son "familias conjugadas", al multiplicar la verosimilitud por cada priori (sumando los exponentes de las bases $p$ y $1-p$), sabemos que ambas posteriores también serán distribuciones Beta, con parámetros actualizados $\alpha_{post} = \alpha + x$ y $\beta_{post} = \beta + n - x$.

- **Posteriori 1:** $\text{Beta}(1 + x, 10 + n - x)$
    
- **Posteriori 2:** $\text{Beta}(10 + x, 1 + n - x)$
    

### (a) Análisis de las opiniones y consecuencias con $n=10$

**¿Qué significado tienen las opiniones?**

Podemos ver el sesgo de cada especialista calculando la media _a priori_ (la fórmula de la media de la Beta es $\frac{\alpha}{\alpha+\beta}$):

- Media Especialista 1: $\frac{1}{1+10} = \mathbf{1/11} \approx \mathbf{0.09}$ (Cree que casi **nadie** está irritado).
    
- Media Especialista 2: $\frac{10}{10+1} = \mathbf{10/11} \approx \mathbf{0.91}$ (Cree que casi **todos** están irritados).
    

**Consecuencias de encuestar solo a 10 vecinos ($n=10$):**

Veamos qué estimador (la media a posteriori) entregaría cada uno a la Ciudad si hicieran una encuesta chica de 10 personas donde observan $x$ cantidad de enojados.

Reemplazamos $n=10$ en las posteriores que armamos en el paso cero y calculamos sus medias:

- **Estimador 1:** $\frac{\alpha_{post}}{\alpha_{post} + \beta_{post}} = \frac{1+x}{(1+x) + (10+10-x)} = \mathbf{\frac{x+1}{21}}$
    
- **Estimador 2:** $\frac{\alpha_{post}}{\alpha_{post} + \beta_{post}} = \frac{10+x}{(10+x) + (1+10-x)} = \mathbf{\frac{x+10}{21}}$
    

**La consecuencia analítica:**

Si calculamos la diferencia entre ambos estimadores, las $x$ se cancelan:

$$\frac{x+10}{21} - \frac{x+1}{21} = \frac{9}{21} \approx \mathbf{0.428}$$

**Conclusión:** La consecuencia es gravísima para el Gobierno. Como la muestra ($n=10$) es muy chica frente a la terquedad de los especialistas (que pusieron "pesos" iniciales fuertes en sus parámetros), sin importar qué resultado dé la encuesta, los especialistas **siempre van a diferir en casi un 43%** en sus conclusiones. La muestra no tiene fuerza suficiente para corregir el sesgo inicial.

### (b) Cantidad de encuestados para lograr consenso

Acá el Gobierno se cansó de que los especialistas se peleen y quiere saber a cuánta gente (n) tiene que encuestar obligatoriamente para que los dos análisis matemáticos terminen dando casi lo mismo (una diferencia menor a **0.001**).

**1. Planteamos la diferencia de las medias a posteriori en base a $n$:**

En lugar de fijar $n=10$, lo dejamos como variable.

- Media Post 1: $\frac{x+1}{(1+x) + (10+n-x)} = \frac{x+1}{n+11}$
    
- Media Post 2: $\frac{x+10}{(10+x) + (1+n-x)} = \frac{x+10}{n+11}$
    

**2. Restamos ambas medias:**

$$\text{Diferencia} = \frac{x+10}{n+11} - \frac{x+1}{n+11}$$

$$\text{Diferencia} = \frac{x + 10 - x - 1}{n+11} = \mathbf{\frac{9}{n+11}}$$

**3. Resolvemos la inecuación del enunciado:**

Queremos que esa diferencia sea menor a 0.001:

$$\frac{9}{n+11} < 0.001$$

Pasamos el denominador multiplicando:

$$9 < 0.001(n+11)$$

Pasamos el 0.001 dividiendo (que es lo mismo que multiplicar por 1000):

$$9000 < n + 11$$

Despejamos $n$:

$$n > 9000 - 11$$

$$\mathbf{n > 8989}$$

Para lograr que dos especialistas con opiniones previas tan extremas y polarizadas lleguen a una diferencia menor a 0.001, **se deben encuestar como mínimo a 8990 vecinos de la Ciudad**. ¡Los datos reales finalmente aplastan a la opinión si recolectás los suficientes!





¡Ningún problema! Es la parte más conceptual del ejercicio y es súper normal que haga ruido, porque mezcla la matemática pura con la interpretación política/estadística de los datos.

Vamos a desarmar los dos incisos sin saltearnos un solo detalle para que veas qué significa cada fracción.

### (a) ¿Qué está pasando con los 10 vecinos ($n=10$)?

Imaginemos el escenario real del problema: el Gobierno de la Ciudad quiere saber qué porcentaje ($p$) de la gente está enojada con el ministro.

#### 1. Las dos opiniones antes de encuestar a nadie (La Priori)

Los especialistas tienen dos sesgos opuestos:

- **Especialista 1:** Usa una $\text{Beta}(1, 10)$. Su estimación inicial (la media de la Beta) es $\frac{1}{1+10} = \mathbf{0.09}$. Es decir, antes de salir a la calle, él opina que **solo el 9%** está enojado.
    
- **Especialista 2:** Usa una $\text{Beta}(10, 1)$. Su estimación inicial es $\frac{10}{10+1} = \mathbf{0.91}$. Él opina que **el 91%** está enojado.
    

#### 2. La encuesta chica y la terquedad de los modelos ($n=10$)

Salen a la calle y le preguntan a **10 vecinos** ($n=10$). Supongamos que encuentran $x$ vecinos enojados.

Cada especialista actualiza su modelo combinando lo que él creía con lo que vio en la calle:

- El **Especialista 1** entrega como resultado: $\frac{x+1}{21}$
    
- El **Especialista 2** entrega como resultado: $\frac{x+10}{21}$
    

#### 3. El problema (La conclusión del inciso A)

Fijate qué pasa si restamos el resultado del Especialista 2 menos el del Especialista 1 para ver qué tan de acuerdo están:

$$\text{Diferencia} = \frac{x+10}{21} - \frac{x+1}{21} = \frac{x + 10 - x - 1}{21} = \mathbf{\frac{9}{21}} \approx \mathbf{0.43}$$

**¿Por qué desapareció la $x$?** ¡Esa es la clave de la conclusión!

Desapareció porque **no importa en absoluto qué resultado dio la encuesta**.

- Si de los 10 vecinos los 10 estaban enojados ($x=10$), el Especialista 1 dirá _"52% enojados"_ y el Especialista 2 dirá _"95% enojados"_. Diferencia: **43%**.
    
- Si de los 10 vecinos ninguno estaba enojado ($x=0$), el Especialista 1 dirá _"5% enojados"_ y el Especialista 2 dirá _"48% enojados"_. Diferencia: **43%**.
    

**La conclusión analítica:** Como $n=10$ es una muestra demasiado chica, no tiene la fuerza matemática suficiente para torcer la opinión previa de los analistas. El Gobierno gastó plata en una encuesta de 10 personas y los dos analistas le siguen dando informes que contradicen al otro por un 43%.

### (b) ¿A cuánta gente hay que encuestar para que se pongan de acuerdo?

El Gobierno se da cuenta de que 10 personas no alcanzan. Ahora nos preguntan: **_"¿Cuánto tiene que valer $n$ para que la diferencia entre el Especialista 2 y el Especialista 1 sea minúscula (menor a 0.001)?"_**

#### 1. Armamos la fórmula de la diferencia con $n$ libre

Hacemos la misma resta de recién, pero en vez de poner un $21$ abajo (que salía de hacer $11 + 10$), dejamos el tamaño de la muestra como una incógnita ($11 + n$):

$$\text{Diferencia} = \text{Media 2} - \text{Media 1}$$

$$\text{Diferencia} = \left( \frac{x + 10}{n + 11} \right) - \left( \frac{x + 1}{n + 11} \right)$$

$$\text{Diferencia} = \frac{x + 10 - x - 1}{n + 11} = \mathbf{\frac{9}{n + 11}}$$

#### 2. Planteamos la inecuación

El enunciado nos exige que esa diferencia sea menor a $0.001$:

$$\frac{9}{n + 11} < 0.001$$

#### 3. Despejamos la $n$ paso a paso

- El término $(n + 11)$ está dividiendo, lo pasamos multiplicando al otro lado:
    
    $$9 < 0.001 \cdot (n + 11)$$
    
- El número $0.001$ está multiplicando, lo pasamos dividiendo:
    
    $$\frac{9}{0.001} < n + 11$$
    
    _(Dividir por $0.001$ es exactamente lo mismo que hacer $9 \times 1000$)_:
    
    $$9000 < n + 11$$
    
- El $11$ está sumando, pasa restando:
    
    $$9000 - 11 < n$$
    
    $$\mathbf{8989 < n}$$
    

**¿Qué significa este resultado?**

Significa que si el Gobierno quiere que los dos analistas le entreguen prácticamente el **mismo número** (con una diferencia menor al $0.1\%$), tiene que salir a encuestar a **por lo menos 8990 vecinos**.

Es una hermosa moraleja de la estadística bayesiana: _cuando dos personas tienen prejuicios muy fuertes y opuestos, la única forma de que lleguen a un consenso es abrumándolos con una cantidad gigante de evidencia empírica ($n > 8989$)._