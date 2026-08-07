
![[Pasted image 20260805010847.png]]

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




![[Pasted image 20260731185801.png]]


¡Qué buen ejercicio! Este problema sube la vara y tiene una trampa matemática hermosa.

Hasta ahora, en los ejercicios anteriores, veníamos trabajando con lo que se llama "familias conjugadas": al multiplicar la muestra por la priori, mágicamente podíamos sumar los exponentes y nos quedaba otra distribución perfecta (otra Beta). ¡Acá esa magia se va a romper por culpa del "ruido" del canal!

Vamos a resolverlo paso a paso, remangándonos con las integrales, pero usando un súper truco para no hacer cuentas infinitas.

### Paso 1: Traducir el ruido del canal

El parámetro $p$ es la probabilidad de que se **emita** un 1. Pero la muestra que observamos son los números **recibidos**. Necesitamos calcular la probabilidad real de que el receptor lea un "1". Llamemos a esto $\theta$.

Por la Ley de Probabilidad Total, la probabilidad de recibir un 1 es:

$$\theta = P(\text{Recibir } 1 \vert{} \text{Emitir } 1) \cdot P(\text{Emitir } 1) + P(\text{Recibir } 1 \vert{} \text{Emitir } 0) \cdot P(\text{Emitir } 0)$$

Reemplazamos con los datos del enunciado:

- Si se envía un 1, lee 1 el $90\%$ de las veces ($9/10$ o $0.9$).
    
- Si se envía un 0, lee 0 el $100\%$ de las veces. Esto significa que **nunca** lee un 1 por error cuando se mandó un 0.
    
    $$\theta = (0.9 \cdot p) + (0 \cdot (1-p)) = \mathbf{0.9p}$$
    

Nuestra verdadera probabilidad de éxito al leer un dígito es $0.9p$.

### Paso 2: Armar el núcleo de la A Posteriori

Vamos a hacer nuestra clásica multiplicación: $\text{Posteriori} \propto \text{Verosimilitud} \cdot \text{Priori}$

**1. Verosimilitud (La muestra):**

Se recibieron 4 unos en 5 dígitos. Es una Binomial evaluada en $x=4$, usando nuestra probabilidad $\theta = 0.9p$:

$$L(p) \propto (0.9p)^4 (1 - 0.9p)^1 \propto \mathbf{p^4 (1 - 0.9p)}$$

_(Tiramos el $0.9^4$ y la combinatoria porque son constantes que se arreglan solas al final)._

**2. Priori:**

Nos dicen que $p \sim \text{Beta}(3, 3)$. El núcleo es $p^{\alpha-1}(1-p)^{\beta-1}$:

$$f(p) \propto \mathbf{p^2 (1 - p)^2}$$

**3. Multiplicamos (El núcleo $g(p)$):**

$$g(p) = p^4 (1 - 0.9p) \cdot p^2 (1 - p)^2$$

$$g(p) = \mathbf{p^6 (1 - 0.9p) (1 - p)^2}$$

**¡Acá está la trampa!** Ese término $(1 - 0.9p)$ arruina la estructura. Esto ya no es una distribución Beta de manual. Para poder usar esta distribución y hacer predicciones, vamos a tener que calcular obligatoriamente la constante del denominador de la fórmula de Bayes (llamémosla $D$).

### Paso 3: Calcular el denominador usando la función Beta

El denominador $D$ es la integral de nuestro núcleo entre 0 y 1. Si distribuimos el $(1 - 0.9p)$, podemos separar la integral en dos pedazos fáciles:

$$g(p) = p^6 (1-p)^2 - 0.9 p^7 (1-p)^2$$

$$D = \int_0^1 p^6 (1-p)^2 dp - 0.9 \int_0^1 p^7 (1-p)^2 dp$$

**El truco:** La integral $\int_0^1 p^{\alpha-1}(1-p)^{\beta-1} dp$ es literalmente la definición de la función matemática Beta $B(\alpha, \beta)$, que se resuelve fácil con factoriales: $B(\alpha, \beta) = \frac{(\alpha-1)! (\beta-1)!}{(\alpha+\beta-1)!}$.

Mirando los exponentes de nuestras integrales, reconocemos que:

- La primera integral es $B(7, 3) = \frac{6! 2!}{9!} = \frac{2}{504} = \mathbf{\frac{1}{252}}$
    
- La segunda integral es $B(8, 3) = \frac{7! 2!}{10!} = \frac{2}{720} = \mathbf{\frac{1}{360}}$
    

Reemplazamos:

$$D = \frac{1}{252} - 0.9 \left(\frac{1}{360}\right) = \frac{10}{2520} - \frac{9}{3600}$$

Buscamos denominador común y restamos:

$$\mathbf{D = \frac{37}{25200}}$$

Nuestra distribución a posteriori real y completa es: $f(p \vert{} \text{muestra}) = \frac{g(p)}{37/25200}$

### Paso 4: La Predicción del nuevo mensaje

Te piden la probabilidad de que, en un nuevo mensaje de 2 dígitos, recibas exactamente 2 unos.

Llamemos $Y$ a esta nueva variable predictiva. Sigue una $\text{Binomial}(n=2, \theta=0.9p)$.

La probabilidad condicionada a un $p$ exacto sería:

$$P(Y=2 \vert{} p) = \binom{2}{2} (0.9p)^2 (1 - 0.9p)^0 = \mathbf{0.81 p^2}$$

Como $p$ es una incógnita, usamos la Ley de Esperanza Total integrando esta probabilidad futura sobre nuestra distribución a posteriori:

$$P(Y=2 \vert{} \text{muestra}) = \int_0^1 0.81 p^2 \cdot f(p \vert{} \text{muestra}) dp$$

$$P(Y=2 \vert{} \text{muestra}) = \frac{0.81}{D} \int_0^1 p^2 \cdot \left[ p^6 (1-0.9p) (1-p)^2 \right] dp$$

Juntamos el $p^2$ con el $p^6$ para que nos quede un $p^8$ adentro de la integral. Llamemos $N$ a esa nueva integral a resolver:

$$N = \int_0^1 p^8 (1 - 0.9p) (1-p)^2 dp$$

$$N = \int_0^1 p^8 (1-p)^2 dp - 0.9 \int_0^1 p^9 (1-p)^2 dp$$

Aplicamos exactamente el mismo truco de las Betas que usamos en el Paso 3:

- La primera integral es $B(9, 3) = \frac{8! 2!}{11!} = \mathbf{\frac{1}{495}}$
    
- La segunda integral es $B(10, 3) = \frac{9! 2!}{12!} = \mathbf{\frac{1}{660}}$
    

Reemplazamos:

$$N = \frac{1}{495} - 0.9 \left(\frac{1}{660}\right) = \frac{40}{19800} - \frac{27}{19800} = \mathbf{\frac{13}{19800}}$$

### Resultado Final

Armamos la división completa:

$$P(Y=2 \vert{} \text{muestra}) = \frac{0.81 \cdot N}{D}$$

$$P(Y=2 \vert{} \text{muestra}) = 0.81 \cdot \frac{13 / 19800}{37 / 25200}$$

Si multiplicás todo y simplificás las fracciones:

$$P(Y=2 \vert{} \text{muestra}) = \mathbf{\frac{7371}{20350}} \approx \mathbf{0.3622}$$

La probabilidad de recibir exactamente dos "unos" en el próximo mensaje es del **36.22%**.









¡Vamos a reescribir todo el desarrollo de cero, dejando bien explícito cómo cada paso es una pieza fundamental del Teorema de Bayes!

  

### Paso 1: Definir la probabilidad real (El impacto del ruido)

El parámetro $p$ es la probabilidad teórica de emitir un 1. Sin embargo, debido a que el canal es defectuoso, lo que nosotros _recibimos_ y usamos para la muestra es distinto.

  

Definimos $\theta$ como la probabilidad de recibir efectivamente un 1. Usando la Ley de Probabilidad Total, combinamos las chances de aciertos y errores del canal:

  

$$\theta = P(\text{Recibir } 1 \mid \text{Emitir } 1) \cdot P(\text{Emitir } 1) + P(\text{Recibir } 1 \mid \text{Emitir } 0) \cdot P(\text{Emitir } 0)$$

Reemplazando con los datos del enunciado (el canal acierta el 90% de los unos, y el 100% de los ceros):

  

$$\theta = (0.9 \cdot p) + (0 \cdot (1-p)) = 0.9p$$

### Paso 2: El Numerador de Bayes (Priori $\times$ Verosimilitud)

El Teorema de Bayes nos pide multiplicar lo que creíamos antes (Priori) por la evidencia de la muestra (Verosimilitud).

  

1. **La Priori:** El enunciado nos dice que $p \sim \text{Beta}(3, 3)$. Tomamos solo la parte de la fórmula que contiene a la variable:
    
      
    
    $$f(p) \propto p^2(1-p)^2$$
    
2. **La Verosimilitud:** Nuestra muestra es de 5 dígitos donde se recibieron 4 "unos". Es una distribución Binomial evaluada con nuestra nueva probabilidad $\theta = 0.9p$:
    
      
    
    $$L(p) \propto (0.9p)^4(1-0.9p)^1 \propto p^4(1-0.9p)$$
    
3. **El Numerador (El producto):** Multiplicamos ambas partes para obtener la base de nuestra distribución a posteriori (llamémosla $g(p)$):
    
      
    
    $$g(p) = p^4(1-0.9p) \cdot p^2(1-p)^2 = p^6(1-0.9p)(1-p)^2$$
    

### Paso 3: El Denominador de Bayes (La Constante de Integración)

Para que $g(p)$ se convierta en una función de probabilidad real (cuyo área total sea 1), necesitamos dividirla por la Probabilidad Total de la muestra. Como $p$ es continua, calculamos el denominador $D$ integrando el numerador entre 0 y 1.

  

$$D = \int_0^1 p^6(1-0.9p)(1-p)^2 dp$$

Para evitar una integración larguísima, distribuimos el bloque $(1-0.9p)$ para separarlo en dos integrales que tengan la forma exacta de la Función Beta Matemática:

  

$$D = \int_0^1 p^6(1-p)^2 dp - 0.9 \int_0^1 p^7(1-p)^2 dp$$

Aplicamos la definición de la función Beta $B(\alpha, \beta) = \frac{(\alpha-1)!(\beta-1)!}{(\alpha+\beta-1)!}$:

  

- **Primera integral:** Es $B(7, 3) = \frac{6!2!}{9!} = \frac{1}{252}$
    
      
    
- **Segunda integral:** Es $B(8, 3) = \frac{7!2!}{10!} = \frac{1}{360}$
    
      
    

Armamos la resta final para el denominador:

  

$$D = \frac{1}{252} - 0.9 \left(\frac{1}{360}\right) = \frac{10}{2520} - \frac{9}{3600} = \frac{37}{25200}$$

Con esto completamos el Teorema de Bayes. Nuestra función a posteriori definitiva es:

  

$$f(p \mid \text{muestra}) = \frac{p^6(1-0.9p)(1-p)^2}{37/25200}$$

### Paso 4: El Cálculo Predictivo (El Futuro)

Nos piden calcular la probabilidad de un evento futuro: recibir exactamente 2 "unos" en un nuevo mensaje de 2 dígitos. Llamemos $Y$ a esta nueva variable Binomial.

  

La probabilidad de este evento futuro, condicionada a un $p$ específico, sería:

  

$$P(Y=2 \mid p) = \binom{2}{2}(0.9p)^2(1-0.9p)^0 = 0.81p^2$$

Como no sabemos el valor exacto de $p$, integramos esta fórmula sobre toda nuestra nueva distribución a posteriori (Ley de Esperanza Total):

  

$$P(Y=2 \mid \text{muestra}) = \int_0^1 0.81p^2 \cdot f(p \mid \text{muestra}) dp$$

Reemplazamos $f(p \mid \text{muestra})$ con la fórmula completa del Paso 3 y sacamos las constantes afuera de la integral:

  

$$P(Y=2 \mid \text{muestra}) = \frac{0.81}{37/25200} \int_0^1 p^2 \cdot [p^6(1-0.9p)(1-p)^2] dp$$

Al multiplicar $p^2$ por $p^6$, nos queda un $p^8$ adentro. Llamemos $N$ a esta nueva integral y la resolvemos separándola igual que en el Paso 3:

  

$$N = \int_0^1 p^8(1-p)^2 dp - 0.9 \int_0^1 p^9(1-p)^2 dp$$

Aplicamos nuevamente las propiedades de la función Beta:

  

- **Primera integral:** Es $B(9, 3) = \frac{8!2!}{11!} = \frac{1}{495}$
    
      
    
- **Segunda integral:** Es $B(10, 3) = \frac{9!2!}{12!} = \frac{1}{660}$
    
      
    

Resolvemos el bloque $N$:

  

$$N = \frac{1}{495} - 0.9 \left(\frac{1}{660}\right) = \frac{40}{19800} - \frac{27}{19800} = \frac{13}{19800}$$

### Paso 5: Resultado Final

Finalmente, juntamos la fracción predictiva del Paso 4 ($0.81 \cdot N$) con el denominador de Bayes del Paso 3 ($D$):

  

$$P(Y=2 \mid \text{muestra}) = 0.81 \cdot \frac{13/19800}{37/25200}$$

Resolviendo las fracciones y simplificando:

$$P(Y=2 \mid \text{muestra}) = \frac{7371}{20350} \approx 0.3622$$





¡Es una pregunta teórica brillante! Estás tocando el engranaje principal que hace funcionar a toda la estadística predictiva.

  

Para responder de dónde sale esto, tenemos que unir dos conceptos fundamentales: la **Ley de Probabilidad Total** y la definición matemática de **Esperanza**.

  

### 1. ¿De qué ley sale? (La Ley de Probabilidad Total)

En probabilidad básica, cuando un evento futuro dependía de varios escenarios posibles, usabas la clásica sumatoria del **Teorema de Probabilidad Total**:

  

$$P(A) = \sum P(A \mid \text{Escenario}_i) \cdot P(\text{Escenario}_i)$$

En la estadística Bayesiana, tu "escenario" es el verdadero valor del parámetro $p$. Como $p$ es una variable continua y puede tomar infinitos valores decimales entre 0 y 1, la sumatoria se transforma en una integral. La ley sigue siendo exactamente la misma, pero adaptada al mundo continuo:

  

$$P(Y=2) = \int_0^1 P(Y=2 \mid p) \cdot f(p) dp$$

Como tu predicción ocurre _después_ de haber visto la muestra, usás tu creencia actualizada (la posteriori):

  

$$P(Y=2 \mid \text{muestra}) = \int_0^1 P(Y=2 \mid p) \cdot f(p \mid \text{muestra}) dp$$

### 2. ¿Por qué se le dice "sacar la Esperanza"?

Acá es donde la matemática se vuelve poética.

  

Recordemos la definición genérica de Esperanza (o Valor Esperado) para cualquier función $h(x)$ que dependa de una variable aleatoria:

  

$$E[h(x)] = \int h(x) \cdot f(x) dx$$

En nuestro problema predictivo:

  

- Nuestra variable aleatoria es el parámetro $p$.
    
      
    
- Nuestra función es la probabilidad futura: $h(p) = P(Y=2 \mid p)$.
    
      
    

Si metemos nuestra función adentro de la fórmula de la Esperanza, nos queda:

  

$$E[P(Y=2 \mid p)] = \int_0^1 P(Y=2 \mid p) \cdot f(p \mid \text{muestra}) dp$$

¡Es idéntica a la fórmula de Probabilidad Total! Por eso, calcular esa integral es, matemáticamente hablando, calcular **el Valor Esperado de la probabilidad**.

  

### El concepto intuitivo (¿Qué significa esto en la vida real?)

Imaginate que querés predecir si vas a recibir dos "unos" en el próximo mensaje.

  

- Si un oráculo te dijera "El parámetro $p$ vale exactamente 0.5", tu cuenta sería trivial. Reemplazás el 0.5 y listo.
    
      
    
- **Pero no conocés a tu variable.** Solo tenés una distribución a posteriori que te dice qué valores de $p$ son más creíbles y cuáles menos.
    
      
    

Como no podés jugártela por un solo número, la matemática te obliga a probarlos **todos**. La integral agarra cada valor posible de $p$ (0.01, 0.02, 0.5, 0.99...), calcula la probabilidad del futuro asumiendo ese número puntual, y luego multiplica ese resultado por el "peso" o la confianza que le tenés a ese $p$ (tu función a posteriori).

  

Al final del día, calcular una Esperanza no es otra cosa que calcular un **promedio ponderado**. Cuando resolvés esa integral doble, estás promediando todas las probabilidades futuras posibles, dándole más importancia a los valores de $p$ que tu muestra demostró que eran más probables.



![[Pasted image 20260731193528.png]]

¡Este es uno de los problemas más famosos de la historia de la estadística! Los datos de las patadas de caballo de Bortkiewicz son literalmente el ejemplo clásico con el que se enseña la distribución de Poisson en todo el mundo.

Acá volvemos a la zona de confort de las **familias conjugadas**. El combo **Poisson-Gamma** funciona exactamente igual de bien que el combo Binomial-Beta que venías manejando. Al multiplicar la muestra por la priori, los exponentes se suman y te devuelven otra Gamma perfecta.

Vamos a desarmarlo paso a paso:

### Paso 1: Resumir los datos de la muestra (Verosimilitud)

La distribución de Poisson evalúa conteos. Para armar la verosimilitud de toda la muestra junta, necesitamos dos datos clave de la tabla:

1. **Tamaño de la muestra ($n$):** Es la cantidad total de registros (cuerpos de caballería $\times$ años). El enunciado nos ahorra la suma y nos dice que son **200**.
    
2. **Total de muertes observadas ($\sum x_i$):** Es la suma de todos los casos reales. Multiplicamos la cantidad de muertes por la frecuencia con la que ocurrieron:
    
    $$\sum x_i = (0 \cdot 109) + (1 \cdot 65) + (2 \cdot 22) + (3 \cdot 3) + (4 \cdot 1)$$
    
    $$\sum x_i = 0 + 65 + 44 + 9 + 4 = \mathbf{122}$$
    

El núcleo de la verosimilitud conjunta para una Poisson es proporcional a $\mu^{\sum x_i} e^{-n\mu}$.

Reemplazando nuestros datos:

$$\text{Verosimilitud} \propto \mu^{122} e^{-200\mu}$$

### Paso 2: Descubrir los parámetros de la "A Priori"

Nos dicen que la priori es una distribución Gamma, pero en lugar de darnos sus parámetros directos ($\alpha$ y $\lambda$), nos dan su media y su varianza. Tenemos que despejarlos usando las fórmulas teóricas de la Gamma:

- **Media:** $E[\mu] = \frac{\alpha}{\lambda} = \frac{1}{2}$
    
- **Varianza:** $V[\mu] = \frac{\alpha}{\lambda^2} = \frac{1}{8}$
    

Podemos resolver este sistema dividiendo la varianza por la media:

$$\frac{V[\mu]}{E[\mu]} = \frac{\alpha / \lambda^2}{\alpha / \lambda} = \frac{1}{\lambda}$$

$$\frac{1/8}{1/2} = \frac{2}{8} = \frac{1}{4}$$

Entonces, si $\frac{1}{\lambda} = \frac{1}{4}$, deducimos que **$\lambda = 4$**.

Reemplazamos este valor en la fórmula de la media para sacar $\alpha$:

$$\frac{\alpha}{4} = \frac{1}{2} \implies \mathbf{\alpha = 2}$$

Nuestra distribución a priori es una **$\text{Gamma}(\alpha=2, \lambda=4)$**.

El núcleo de una Gamma es $\mu^{\alpha-1} e^{-\lambda\mu}$, que en nuestro caso queda:

$$\text{Priori} \propto \mu^{2-1} e^{-4\mu} = \mu^1 e^{-4\mu}$$

### Paso 3: Armar la distribución "A Posteriori"

Multiplicamos el núcleo de la muestra por el núcleo de nuestra creencia inicial:

$$\text{Posteriori} \propto \text{Verosimilitud} \cdot \text{Priori}$$

$$\text{Posteriori} \propto \left( \mu^{122} e^{-200\mu} \right) \cdot \left( \mu^1 e^{-4\mu} \right)$$

Juntamos las bases iguales sumando los exponentes:

$$\text{Posteriori} \propto \mu^{122+1} e^{-(200+4)\mu}$$

$$\text{Posteriori} \propto \mu^{123} e^{-204\mu}$$

Este resultado tiene exactamente la forma del núcleo de una nueva distribución Gamma $\mu^{\alpha_{post}-1} e^{-\lambda_{post}\mu}$.

Dedudimos los parámetros actualizados:

- $\alpha_{post} - 1 = 123 \implies \mathbf{\alpha_{post} = 124}$
    
- $\mathbf{\lambda_{post} = 204}$
    

_Nota: La regla general para la actualización Poisson-Gamma es siempre $\alpha_{nueva} = \alpha_{vieja} + \sum x_i$ y $\lambda_{nueva} = \lambda_{vieja} + n$. ¡Coincide perfecto!_

### Paso 4: Calcular la Media a posteriori

El ejercicio te pide "calcular la media de la distribución a posteriori".

Como sabemos que nuestra nueva distribución es una $\text{Gamma}(124, 204)$, simplemente aplicamos la fórmula de la media para esta distribución ($\frac{\alpha}{\lambda}$):

$$E[\mu \vert{} \text{datos}] = \frac{124}{204}$$

Simplificando la fracción (dividiendo por 4 arriba y abajo), llegamos al resultado final:

$$\mathbf{E[\mu \vert{} \text{datos}] = \frac{31}{51} \approx 0.6078}$$


![[Pasted image 20260731193746.png]]

¡Este ejercicio es una combinación espectacular de todo lo que venís practicando! Vuelve el famoso combo **Poisson-Gamma**, pero le suma la predicción (como el canal de comunicación) y te pide un intervalo de confianza usando una aproximación clásica.

### Paso 1: Armar la "Cocina" (Distribución A Posteriori)

Primero definimos nuestras variables:

- **Verosimilitud (La muestra):** Es una distribución Poisson. Calculamos la muestra total ($n$) y la suma de todos los accidentes observados ($\sum x_i$):
    
    - $n = 100$ semanas.
        
    - $\sum x_i = (0 \cdot 10) + (1 \cdot 29) + (2 \cdot 25) + (3 \cdot 17) + (4 \cdot 13) + (5 \cdot 6)$
        
    - $\sum x_i = 0 + 29 + 50 + 51 + 52 + 30 = \mathbf{212}$
        
- **La Priori:** El enunciado dice que es una **Exponencial de media 2**. ¡Acá hay un truquito teórico! Una distribución Exponencial es simplemente un caso especial de la distribución Gamma donde el primer parámetro es $\alpha = 1$.
    
    Como la media teórica de una Exponencial es $1/\lambda$, si el enunciado te dice que la media es 2, entonces despejás $\lambda = 1/2 = 0.5$.
    
    Por lo tanto, tu priori es en realidad una **$\text{Gamma}(\alpha=1, \lambda=0.5)$**.
    

Como Poisson y Gamma son familia conjugada, sumamos los parámetros de la muestra a la priori para sacar la posteriori:

- $\alpha_{post} = \alpha + \sum x_i = 1 + 212 = \mathbf{213}$
    
- $\lambda_{post} = \lambda + n = 0.5 + 100 = \mathbf{100.5}$
    

Nuestra distribución actualizada final es: **$\mu \vert{} X \sim \text{Gamma}(213, 100.5)$**.

### (a) Estimar la probabilidad de ningún accidente (Predicción)

Te piden calcular la probabilidad de que una futura semana ($Y$) tenga 0 accidentes: $P(Y=0 \vert{} \text{muestra})$.

Acá aplicamos la **Ley de Esperanza Total** (nuestro "promedio de promedios" con integrales), usando la fórmula predictiva:

$$P(Y=0 \vert{} \text{muestra}) = \int_0^\infty P(Y=0 \vert{} \mu) \cdot f(\mu \vert{} \text{muestra}) d\mu$$

La probabilidad de $Y=0$ en una fórmula Poisson pura es simplemente $e^{-\mu}$. Lo multiplicamos por el núcleo de nuestra nueva Gamma:

$$P(Y=0 \vert{} \text{muestra}) \propto \int_0^\infty e^{-\mu} \cdot \mu^{213-1} e^{-100.5\mu} d\mu$$

Juntamos las bases de $e$:

$$\int_0^\infty \mu^{213-1} e^{-101.5\mu} d\mu$$

¡Esto que nos quedó adentro de la integral es el núcleo de una nueva Gamma (con $\lambda=101.5$)! En estadística bayesiana, esta estructura se resuelve sola por propiedades de las integrales de la función Gamma. Para la predicción exacta de $Y=0$ en el modelo Poisson-Gamma, el atajo matemático directo es:

$$P(Y=0 \vert{} \text{muestra}) = \left( \frac{\lambda_{post}}{\lambda_{post} + 1} \right)^{\alpha_{post}}$$

Reemplazamos con nuestros números:

$$P(Y=0 \vert{} \text{muestra}) = \left( \frac{100.5}{100.5 + 1} \right)^{213}$$

$$P(Y=0 \vert{} \text{muestra}) = \left( \frac{100.5}{101.5} \right)^{213}$$

$$P(Y=0 \vert{} \text{muestra}) \approx (0.990147)^{213} \approx \mathbf{0.1213}$$

Hay aproximadamente un **12.13%** de probabilidad de que en esa semana específica de diciembre no ocurra ningún accidente.

### (b) Intervalo de confianza al 95%

Acá tenemos que estimar un rango para nuestro parámetro $\mu$.

Como nuestra distribución a posteriori $\text{Gamma}(213, 100.5)$ tiene un $\alpha$ gigante (al ser mucho mayor a 30), podemos aplicar una de las propiedades más salvadoras: aproximarla a una **distribución Normal**.

Para armar la Normal, necesitamos la media y el desvío estándar de nuestra Gamma:

1. **Media:** $E[\mu] = \frac{\alpha_{post}}{\lambda_{post}} = \frac{213}{100.5} \approx \mathbf{2.1194}$
    
2. **Varianza:** $V[\mu] = \frac{\alpha_{post}}{\lambda_{post}^2} = \frac{213}{(100.5)^2} \approx \frac{213}{10100.25} \approx \mathbf{0.0211}$
    
3. **Desvío Estándar ($\sigma$):** $\sqrt{0.0211} \approx \mathbf{0.1452}$
    

Ahora armamos el intervalo de confianza clásico de la Normal al 95%, que usa el valor de tabla $Z_{0.975} = 1.96$:

$$IC = \text{Media} \pm (1.96 \cdot \sigma)$$

$$IC = 2.1194 \pm (1.96 \cdot 0.1452)$$

$$IC = 2.1194 \pm 0.2846$$

Calculamos los dos extremos:

- Límite Inferior: $2.1194 - 0.2846 = \mathbf{1.8348}$
    
- Límite Superior: $2.1194 + 0.2846 = \mathbf{2.4040}$
    

Tu intervalo de credibilidad al 95% para la media de accidentes es **$[1.835, 2.404]$**.








¡Es una pregunta excelente y da justo en el clavo del cambio de mentalidad que exige la estadística bayesiana!

  

Para responder a tu duda principal de forma directa: **Acá no hay una "X"**.

  

En la estadística clásica, vos estandarizabas el promedio de tu muestra ($\bar{X}$) porque esa era tu variable aleatoria. Pero en la estadística bayesiana, la muestra ya es un dato fijo (pasó a ser historia) y **tu parámetro $\mu$ es la nueva variable aleatoria**.

  

Por lo tanto, la "variable" que vas a poner en el numerador de tu estandarización es literalmente **$\mu$**.

  

Acá tenés el paso a paso visual armando el pivote y despejando, igual que hacías en la primera parte de la materia:

  

### 1. La Aproximación Normal

Sabemos que nuestra distribución a posteriori es $\mu \mid X \sim \text{Gamma}(213, 100.5)$. Como el $\alpha$ es altísimo, la aproximamos a una campana de Gauss (Normal) usando su media y desvío teórico:

  

- **Media ($E[\mu]$):** $2.1194$
    
      
    
- **Desvío ($\sigma_\mu$):** $0.1452$
    
      
    

Por lo tanto, asumimos que nuestra variable $\mu$ se comporta así:

  

$$\mu \sim \mathcal{N}(2.1194, 0.1452^2)$$

### 2. El Armado del Pivote ($Z$)

Para llevar esta distribución a una Normal Estándar $\mathcal{N}(0, 1)$ y poder usar la tabla, armamos la fórmula clásica de estandarización: $\frac{\text{Variable} - \text{Media}}{\text{Desvío}}$.

  

$$Z = \frac{\mu - E[\mu]}{\sigma_\mu}$$

$$Z = \frac{\mu - 2.1194}{0.1452}$$

### 3. Planteo de la Región de Confianza

El enunciado pide un intervalo del 95% de nivel de confianza. Esto significa que dejamos un 2.5% de error en cada cola. Buscando en la tabla normal, el valor crítico (el cuantil $0.975$) es $1.96$.

  

Planteamos que la probabilidad de que nuestro pivote caiga en esa zona central es del 95%:

  

$$P(-1.96 \leqslant Z \leqslant 1.96) = 0.95$$

### 4. Reemplazo y Despeje (Paso a paso visual)

Reemplazamos nuestra Z por la fórmula que armamos en el paso 2:

  

$$P\left(-1.96 \leqslant \frac{\mu - 2.1194}{0.1452} \leqslant 1.96\right) = 0.95$$

**Paso A:** Pasamos el desvío ($0.1452$) multiplicando hacia ambos lados para romper la fracción:

  

$$-1.96 \cdot 0.1452 \leqslant \mu - 2.1194 \leqslant 1.96 \cdot 0.1452$$

$$-0.2846 \leqslant \mu - 2.1194 \leqslant 0.2846$$

**Paso B:** Pasamos la media ($2.1194$) sumando hacia ambos lados para dejar a la variable $\mu$ completamente sola en el centro:

  

$$2.1194 - 0.2846 \leqslant \mu \leqslant 2.1194 + 0.2846$$

**Paso C:** Hacemos las sumas y restas finales:

  

$$1.8348 \leqslant \mu \leqslant 2.4040$$

### Conclusión

Como podés ver, la estructura matemática es exactamente idéntica a la que usabas para los intervalos de confianza clásicos para la media poblacional.

  

La única diferencia conceptual (y el motivo por el cual este intervalo bayesiano se suele llamar **"Intervalo de Credibilidad"**) es que ahora la que está atrapada en el medio del sándwich de inecuaciones es el parámetro real $\mu$, no un estimador muestral.












¡Exactamente! Acabás de dar en la tecla con la diferencia filosófica y matemática más importante entre los dos mundos de la estadística.

  

Te lo resumo en el gran "cambio de roles" que hace la estadística Bayesiana:

  

### 1. El Mundo Clásico (Frecuentista)

En los parciales anteriores, el verdadero promedio de la fábrica ($\mu$) era considerado un **número fijo, congelado y único** (que simplemente no conocías).

Lo que era considerado aleatorio era tu muestra, porque si ibas a la fábrica otra semana distinta, la $X$ te iba a dar otro número. Por eso, en tu fórmula de estandarización, la que variaba y ocupaba el lugar de la variable era tu $\bar{X}$.

  

### 2. El Mundo Bayesiano

Acá la lógica se invierte por completo:

  

- **La muestra es historia:** Ya fuiste a la fábrica, estuviste 100 semanas y contaste 212 accidentes. Eso ya pasó, es un hecho inamovible. Tu $X$ dejó de ser una variable y se transformó en una simple constante fija de tu pasado.
    
      
    
- **El parámetro es la variable:** Como no estás 100% seguro de cuál es el verdadero promedio de la fábrica, la matemática bayesiana dice _"tratemos a nuestra ignorancia como una probabilidad"_. Entonces, el parámetro $\mu$ se convierte en la **Variable Aleatoria**.
    
      
    

Por eso, cuando escribís $\mu \mid X$ (que se lee "la distribución de $\mu$ dado que ya observé mi muestra $X$"), la que tiene forma de campana, la que tiene varianza y la que ocupa el lugar de la "X" en tu fórmula de estandarización es, literalmente, la letra $\mu$.








¡Excelente pregunta! Es un detalle fundamental sobre cómo interpretar los datos cuando te los dan agrupados.

Usás esa suma de multiplicaciones simplemente para averiguar el **total real de accidentes** que ocurrieron a lo largo de esas 100 semanas.

Pensalo de esta forma: la planta industrial registró datos durante 100 semanas. En lugar de darte una lista inmensa y desordenada con 100 números sueltos (tipo: 0, 1, 1, 3, 2, 1, 0, 4...), te dieron un resumen en una **tabla de frecuencias**.

Esa multiplicación es el atajo matemático para desarmar el resumen:

- Hubo **10 semanas** donde ocurrieron **0 accidentes**. En total ahí tenés $0 \cdot 10 = 0$ accidentes.
    
- Hubo **29 semanas** donde ocurrió **1 accidente**. En vez de sumar $1+1+1+1...$ veintinueve veces en la calculadora, hacés el atajo: $1 \cdot 29 = 29$ accidentes.
    
- Hubo **25 semanas** donde ocurrieron **2 accidentes**. En vez de sumar $2+2+2+2...$ veinticinco veces, hacés $2 \cdot 25 = 50$ accidentes.
    

Al sumar todos esos subtotales ($0 + 29 + 50 + 51 + 52 + 30$), llegás al número **212**. Ese es el volumen total de accidentes que pasaron en tu muestra.

**¿Y por qué la fórmula necesita ese 212?**

Porque la distribución de Poisson se alimenta de conteos totales. Para actualizar tu parámetro $\alpha$ (y pasar de tu creencia _a priori_ a tu creencia _a posteriori_), la matemática bayesiana te exige que le ingreses toda la evidencia empírica junta. Necesita saber exactamente cuántos "éxitos" (o en este caso, accidentes) se acumularon en todo el período evaluado, que es precisamente tu $\sum x_i$.













![[Pasted image 20260731201102.png]]




¡Acá tenemos otro clásico de las familias conjugadas! En el archivo image_f73425.png vemos un problema que combina una distribución Gamma para la muestra y una Exponencial para la _a priori_.

Como ya venís viendo, la Exponencial es simplemente un "disfraz" de la familia Gamma, así que la matemática se va a resolver de forma muy elegante sumando exponentes.

Vamos a armar "la cocina" paso a paso:

### Paso 1: Definir la Verosimilitud (La muestra)

El enunciado nos dice que el tiempo de espera $X$ sigue una distribución $\text{Gamma}(2, \lambda)$.

La fórmula de densidad de una Gamma genérica es proporcional a $\lambda^\alpha x^{\alpha-1} e^{-\lambda x}$.

Para nuestro caso, sabemos que $\alpha = 2$ y que observamos un único dato muestral $x = 3/4$.

Reemplazamos estos valores para obtener el núcleo de nuestra verosimilitud (dejando solo lo que tiene a nuestra incógnita $\lambda$):

$$\text{Verosimilitud} \propto \lambda^2 e^{-\frac{3}{4}\lambda}$$

### Paso 2: Definir la A Priori

Nos dicen que $\lambda$ tiene una distribución **Exponencial de media 1**.

La distribución Exponencial es un caso especial de la Gamma donde el primer parámetro es $\alpha = 1$.

Como la media teórica de una Exponencial es $\frac{1}{\beta}$, si la media es $1$, entonces nuestro parámetro de tasa $\beta$ también vale $1$.

Por lo tanto, nuestra _a priori_ es en realidad una **$\text{Gamma}(\alpha=1, \beta=1)$**.

El núcleo de esta distribución es:

$$\text{Priori} \propto \lambda^{1-1} e^{-1\lambda} = \mathbf{e^{-\lambda}}$$

### Paso 3: Hallar la Distribución A Posteriori

Multiplicamos la Verosimilitud por la A Priori para actualizar nuestras creencias:

$$\text{Posteriori} \propto \text{Verosimilitud} \cdot \text{Priori}$$

$$\text{Posteriori} \propto \left( \lambda^2 e^{-\frac{3}{4}\lambda} \right) \cdot \left( e^{-\lambda} \right)$$

Juntamos las bases iguales sumando los exponentes de $e$:

$$\text{Posteriori} \propto \lambda^2 e^{-\left(\frac{3}{4} + 1\right)\lambda}$$

$$\text{Posteriori} \propto \mathbf{\lambda^2 e^{-\frac{7}{4}\lambda}}$$

Si miramos la estructura matemática $\lambda^{\alpha_{post}-1} e^{-\beta_{post}\lambda}$, reconocemos inmediatamente que esto es una nueva distribución Gamma. Despejamos sus parámetros:

- $\alpha_{post} - 1 = 2 \implies \mathbf{\alpha_{post} = 3}$
    
- $\mathbf{\beta_{post} = \frac{7}{4}}$
    

**Respuesta a la primera pregunta:** La distribución _a posteriori_ de $\lambda$ es una **$\text{Gamma}(3, 7/4)$**.

### Paso 4: Calcular la Media y la Moda

Ahora que ya sabemos que $\lambda \vert{} X \sim \text{Gamma}(3, 7/4)$, simplemente aplicamos las fórmulas teóricas de la distribución Gamma para responder las últimas dos cosas que nos piden.

**1. La Media:**

La esperanza matemática de una Gamma se calcula como $\frac{\alpha}{\beta}$.

$$\text{Media} = \frac{3}{7/4} = 3 \cdot \frac{4}{7} = \mathbf{\frac{12}{7}} \approx 1.714$$

**2. La Moda:**

La moda (el punto más alto o más probable de la distribución) para una Gamma se calcula como $\frac{\alpha - 1}{\beta}$ (siempre que $\alpha \ge 1$).

$$\text{Moda} = \frac{3 - 1}{7/4} = \frac{2}{7/4} = 2 \cdot \frac{4}{7} = \mathbf{\frac{8}{7}} \approx 1.143$$


# Familias conjugadas


¡Las **familias conjugadas** son literalmente el mejor "truco" de toda la estadística bayesiana! Es el concepto que te salva la vida en los parciales porque te permite saltearte la parte más difícil de las matemáticas.

Te lo explico primero desde el concepto y después te muestro cuáles son.

### ¿Qué son exactamente?

En estadística bayesiana, siempre armamos nuestra "cocina" multiplicando dos cosas:

$$\text{Posteriori} \propto \text{Verosimilitud (Muestra)} \cdot \text{Priori}$$

Decimos que una distribución _a priori_ es **conjugada** de la verosimilitud si, al multiplicarlas, el resultado (la _a posteriori_) pertenece **a la misma familia matemática** que la _a priori_.

Es decir, la muestra solo actualiza los parámetros, pero no rompe la forma de la función original. Si entraste con una distribución de un tipo, salís con una distribución de ese mismo tipo.

### ¿Por qué son tan importantes?

Por el infame denominador del Teorema de Bayes.

Para conseguir una distribución _a posteriori_ exacta, la teoría dice que tenés que calcular una integral dificilísima en el denominador para que todas las probabilidades sumen 1.

Cuando usás familias conjugadas, **la integral desaparece**. Como ya sabés de antemano qué forma va a tener el resultado (porque hereda la forma de la priori), lo único que tenés que hacer es sumar los exponentes con álgebra básica, mirar cómo quedaron los parámetros nuevos, y listo. Te ahorraste hojas y hojas de cálculos.

### Las parejas famosas (Cómo son)

Hay combinaciones clásicas que siempre encastran perfecto. Estas son las que más vas a usar:

**1. El combo Beta - Binomial (Para proporciones)**

- **Verosimilitud:** $\text{Binomial}$ (Ej: contar cuántas caras salen en $n$ tiros de moneda, o cuántos termos defectuosos hay).
    
- **Priori Conjugada:** $\text{Beta}(\alpha, \beta)$
    
- **Posteriori:** ¡Otra $\text{Beta}$!
    
- **La magia:** Al multiplicar, simplemente actualizás sumando los éxitos de la muestra al parámetro $\alpha$, y los fracasos al parámetro $\beta$.
    

**2. El combo Gamma - Poisson (Para conteos o tasas)**

- **Verosimilitud:** $\text{Poisson}$ (Ej: cantidad de accidentes por semana, o muertes por patadas de caballo en un año).
    
- **Priori Conjugada:** $\text{Gamma}(\alpha, \lambda)$
    
- **Posteriori:** ¡Otra $\text{Gamma}$!
    
- **La magia:** Actualizás sumando el total de casos observados al parámetro $\alpha$, y el tamaño total de la muestra (ej: cantidad de semanas) al parámetro $\lambda$.
    

**3. El combo Gamma - Exponencial (Para tiempos de espera)**

- **Verosimilitud:** $\text{Exponencial}$ o $\text{Gamma}$ (Ej: tiempo en horas hasta que falla un sistema).
    
- **Priori Conjugada:** $\text{Gamma}(\alpha, \beta)$
    
- _(Recordá que la Exponencial es solo una Gamma con $\alpha=1$)._
    
- **Posteriori:** ¡Otra $\text{Gamma}$!
    
- **La magia:** Actualizás sumando la cantidad de datos u observaciones a $\alpha$, y sumando el tiempo total transcurrido a $\beta$.
    

**4. El combo Normal - Normal (Para promedios continuos)**

- **Verosimilitud:** $\text{Normal}$ (Ej: medir la altura de las personas o la longitud de una varilla).
    
- **Priori Conjugada:** $\text{Normal}$ (para la media $\mu$).
    
- **Posteriori:** ¡Otra $\text{Normal}$!
    
- **La magia:** La media _a posteriori_ termina siendo un "promedio ponderado" perfecto entre la media de tu creencia original y la media de tu muestra empírica.
    

En resumen: las conjugadas son parejas predeterminadas de distribuciones que se llevan tan bien matemáticamente que, al juntarlas, te devuelven una versión actualizada y más precisa de sí mismas.



![[Pasted image 20260731201518.png]]

Este ejercicio tiene una trampa excelente que es súper común en la estadística bayesiana: **los parámetros que definen el límite del dominio**.

Cuando trabajamos con distribuciones Uniformes donde la incógnita está en el límite (en este caso el límite superior es $1+\theta$), la clave de la Verosimilitud no está solo en la fórmula, sino en las **funciones indicadoras** (las restricciones lógicas).

Vamos a resolverlo paso a paso.

### Paso 1: La Verosimilitud (El problema de los límites)

El tiempo $X$ sigue una distribución Uniforme en el intervalo $[1, 1+\theta]$.

La función de densidad de una Uniforme $[a, b]$ es $\frac{1}{b-a}$. En nuestro caso:

$$f(x \vert{} \theta) = \frac{1}{(1+\theta) - 1} = \frac{1}{\theta}$$

Pero esto solo vale si $1 \le x \le 1+\theta$. Si la muestra se sale de ese rango, la probabilidad es cero. Observamos tres tiempos: $x_1=3$, $x_2=5$ y $x_3=8$.

La verosimilitud conjunta para los tres datos es la multiplicación de las densidades:

$$L(\theta \vert{} \mathbf{x}) = \frac{1}{\theta} \cdot \frac{1}{\theta} \cdot \frac{1}{\theta} = \frac{1}{\theta^3}$$

**¡La restricción fundamental!**

Para que este modelo sea posible, todos los datos observados deben obligatoriamente ser menores o iguales al límite superior del intervalo ($1+\theta$). El dato más restrictivo es el valor máximo que observaste (el 8).

$$8 \le 1+\theta \implies \mathbf{7 \le \theta}$$

Entonces, el núcleo de nuestra Verosimilitud, incluyendo su restricción, se escribe así:

$$L(\theta \vert{} \mathbf{x}) \propto \frac{1}{\theta^3} \mathbf{1}\{\theta \ge 7\}$$

### Paso 2: La Distribución A Posteriori

El enunciado nos da la densidad _a priori_ de $\theta$:

$$f(\theta) = \frac{192}{\theta^4} \mathbf{1}\{\theta \ge 4\}$$

Aplicamos el Teorema de Bayes multiplicando ambas partes:

$$\text{Posteriori} \propto L(\theta \vert{} \mathbf{x}) \cdot f(\theta)$$

$$\text{Posteriori} \propto \left( \frac{1}{\theta^3} \mathbf{1}\{\theta \ge 7\} \right) \cdot \left( \frac{192}{\theta^4} \mathbf{1}\{\theta \ge 4\} \right)$$

Juntamos las $\theta$ sumando los exponentes del denominador ($\theta^3 \cdot \theta^4 = \theta^7$).

¿Y qué pasa con las restricciones? Tenemos dos condiciones que se deben cumplir en simultáneo: $\theta \ge 7$ y $\theta \ge 4$. La condición más fuerte (la que "gana" la intersección) es $\theta \ge 7$.

El núcleo de nuestra _a posteriori_ queda:

$$f(\theta \vert{} \mathbf{x}) \propto \frac{1}{\theta^7} \mathbf{1}\{\theta \ge 7\}$$

**Encontrar la constante:**

Para que esto sea una distribución de probabilidad real, la integral desde 7 hasta infinito debe dar 1. Agregamos una constante $C$:

$$\int_7^\infty \frac{C}{\theta^7} d\theta = 1$$

$$C \left[ \frac{\theta^{-6}}{-6} \right]_7^\infty = 1$$

$$C \left( 0 - \frac{7^{-6}}{-6} \right) = 1 \implies C \cdot \frac{1}{6 \cdot 7^6} = 1 \implies \mathbf{C = 6 \cdot 7^6}$$

La distribución _a posteriori_ exacta es:

$$f(\theta \vert{} \mathbf{x}) = \frac{6 \cdot 7^6}{\theta^7} \mathbf{1}\{\theta \ge 7\}$$

_(Dato de color teórico: Esta estructura matemática se conoce como **Distribución de Pareto**)._

### Paso 3: Estimar la media del tiempo de realización

Acá te piden estimar un valor futuro (predictivo) del tiempo de tarea, al que llamaremos $X_{nuevo}$. Por la **Ley de Esperanza Total**, la esperanza del tiempo depende de la esperanza de $\theta$:

$$E[X_{nuevo} \vert{} \mathbf{x}] = E \big[ E[X_{nuevo} \vert{} \theta] \big\vert{} \mathbf{x} \big]$$

**1. El núcleo (La media si conociéramos $\theta$):**

Como $X \sim \text{Uniforme}[1, 1+\theta]$, la media teórica de una Uniforme es el punto medio del intervalo: $\frac{a+b}{2}$.

$$E[X \vert{} \theta] = \frac{1 + (1+\theta)}{2} = \frac{2 + \theta}{2} = \mathbf{1 + \frac{\theta}{2}}$$

**2. La esperanza de $\theta$ a posteriori:**

Tenemos que promediar ese resultado usando nuestra nueva distribución de Pareto calculando la integral de $\theta \cdot f(\theta\vert{}\mathbf{x})$:

$$E[\theta \vert{} \mathbf{x}] = \int_7^\infty \theta \cdot \frac{6 \cdot 7^6}{\theta^7} d\theta$$

$$E[\theta \vert{} \mathbf{x}] = \int_7^\infty \frac{6 \cdot 7^6}{\theta^6} d\theta = 6 \cdot 7^6 \left[ \frac{\theta^{-5}}{-5} \right]_7^\infty$$

$$E[\theta \vert{} \mathbf{x}] = 6 \cdot 7^6 \left( 0 - \frac{7^{-5}}{-5} \right) = \frac{6 \cdot 7^6}{5 \cdot 7^5} = \frac{6 \cdot 7}{5} = \mathbf{\frac{42}{5}} = \mathbf{8.4}$$

**3. El Ensamblaje Final:**

Reemplazamos el valor que acabamos de conseguir en la fórmula del núcleo del paso 1:

$$E[X_{nuevo} \vert{} \mathbf{x}] = 1 + \frac{E[\theta \vert{} \mathbf{x}]}{2}$$

$$E[X_{nuevo} \vert{} \mathbf{x}] = 1 + \frac{8.4}{2}$$

$$E[X_{nuevo} \vert{} \mathbf{x}] = 1 + 4.2 = \mathbf{5.2}$$

La estimación final para la media del tiempo de realización de la tarea es de **5.2 minutos**.




¡Es una duda excelente! La clave matemática acá está en la diferencia entre un **núcleo** (que usamos con el símbolo $\propto$) y una **distribución de probabilidad real** (que usamos con el símbolo $=$).

Cuando aplicamos el Teorema de Bayes en el paso anterior, nosotros ignoramos todas las constantes numéricas que no tenían la letra $\theta$ para hacer las cuentas más rápido. Por eso llegamos a este resultado:

$$f(\theta \vert{} \mathbf{x}) \propto \frac{1}{\theta^7}$$

El símbolo $\propto$ significa "es proporcional a". Nos dice que la curva gráfica tiene _la forma_ de la función $1/\theta^7$, pero **le falta su escala original**.

Para que una función sea considerada una distribución de probabilidad válida, tiene una regla de oro irrompible: **el área total debajo de su curva tiene que sumar exactamente 1** (que representa el 100% de la probabilidad).

### ¿Qué pasa si integramos sin la C?

Si vos calculás la integral de la función "pelada" $1/\theta^7$ desde 7 hasta infinito, fijate lo que da:

$$\int_7^\infty \frac{1}{\theta^7} d\theta = \left[ \frac{\theta^{-6}}{-6} \right]_7^\infty = 0 - \left( \frac{7^{-6}}{-6} \right) = \mathbf{\frac{1}{6 \cdot 7^6}}$$

Ese resultado es un número minúsculo, lejísimos de ser un 1. Si dejaras la función así, estarías diciendo que la suma de todas las probabilidades posibles da $0.0000014...$, lo cual matemáticamente es un error.

### El rol de la C (Constante de Normalización)

Como sabemos que nuestra función tiene la "forma" correcta pero le falta "volumen" para llegar al 1, le multiplicamos una constante genérica $C$ para corregirla.

Planteamos la ecuación forzando a que el resultado sea 1:

"La integral de mi función multiplicada por $C$ **tiene que ser igual a 1**".

$$\int_7^\infty C \cdot \frac{1}{\theta^7} d\theta = 1$$

Al resolver esa ecuación y despejar la letra $C$, lo que estamos descubriendo es el número exacto por el que hay que multiplicar a $1/\theta^7$ para que su área se estire hasta valer exactamente el 100%. A ese proceso en estadística se lo llama **"encontrar la constante de normalización"**.





![[Pasted image 20260731202318.png]]


¡Este ejercicio es la secuela perfecta del anterior! Vuelve a aparecer la trampa de los límites con la distribución Uniforme, pero esta vez, en lugar de pedirte estimar una media predictiva, te pide estimar una **probabilidad predictiva**.

Vamos a resolverlo respetando nuestra clásica "cocina" paso a paso.

### Paso 1: La Verosimilitud y el límite oculto

Sabemos que el tamaño de cada archivo $X$ sigue una distribución Uniforme en el intervalo $(0, \theta]$.

La función de densidad para un solo archivo es:

$$f(x \vert{} \theta) = \frac{1}{\theta}$$

Como tenemos una muestra de **10 archivos** ($n=10$), la verosimilitud conjunta es multiplicar esa densidad 10 veces:

$$L(\theta \vert{} \mathbf{x}) = \left( \frac{1}{\theta} \right)^{10} = \theta^{-10}$$

**La restricción lógica:**

Al igual que en el ejercicio anterior, para que esta distribución exista, absolutamente todos los archivos de la muestra deben ser menores o iguales al techo $\theta$.

Buscamos el archivo más pesado de todos los que observamos: es el de **3.00 GB**.

Por lo tanto, la matemática nos obliga a que $\theta \ge 3$.

El núcleo de nuestra Verosimilitud queda:

$$L(\theta \vert{} \mathbf{x}) \propto \theta^{-10} \mathbf{1}\{\theta \ge 3\}$$

### Paso 2: La Distribución A Posteriori

El enunciado nos da la densidad _a priori_ de $\theta$:

$$f(\theta) = \frac{3}{2} \theta^{-5/2} \mathbf{1}\{\theta > 1\}$$

_(Nota: Tiramos a la basura la constante $3/2$ para armar el núcleo, total la recuperamos al final)._

Multiplicamos Verosimilitud por Priori:

$$\text{Posteriori} \propto \left( \theta^{-10} \mathbf{1}\{\theta \ge 3\} \right) \cdot \left( \theta^{-5/2} \mathbf{1}\{\theta > 1\} \right)$$

1. **Juntamos las $\theta$:** Sumamos exponentes $-10 - 2.5 = -12.5 = \mathbf{-25/2}$.
    
2. **Juntamos los límites:** Tenemos $\theta \ge 3$ y $\theta > 1$. El más restrictivo "gana", así que nos quedamos con $\mathbf{\theta \ge 3}$.
    

El núcleo _a posteriori_ es:

$$f(\theta \vert{} \mathbf{x}) \propto \theta^{-25/2} \mathbf{1}\{\theta \ge 3\}$$

**Encontramos la constante (C):**

Forzamos a que la integral dé 1 para que sea una distribución real:

$$\int_3^\infty C \cdot \theta^{-25/2} d\theta = 1$$

$$C \left[ \frac{\theta^{-23/2}}{-23/2} \right]_3^\infty = 1$$

$$C \left( 0 - \frac{3^{-23/2}}{-23/2} \right) = 1 \implies C \cdot \frac{2}{23 \cdot 3^{23/2}} = 1 \implies \mathbf{C = \frac{23}{2} 3^{23/2}}$$

La distribución _a posteriori_ exacta (¡Otra Pareto!) es:

$$f(\theta \vert{} \mathbf{x}) = \frac{23}{2} 3^{23/2} \cdot \theta^{-25/2} \mathbf{1}\{\theta \ge 3\}$$

### Paso 3: Estimar la probabilidad predictiva

Nos piden la probabilidad de que un nuevo archivo supere los 2 GB: $P(X_{nuevo} > 2 \vert{} \mathbf{x})$.

Aplicamos la **Ley de Esperanza Total** (nuestra integral predictiva):

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \int_3^\infty P(X_{nuevo} > 2 \vert{} \theta) \cdot f(\theta \vert{} \mathbf{x}) d\theta$$

**1. Calculamos el núcleo interno $P(X_{nuevo} > 2 \vert{} \theta)$:**

Si el archivo sigue una Uniforme entre $0$ y $\theta$, la probabilidad de que sea mayor a 2 es calcular qué porcentaje del intervalo cae después del número 2.

Como sabemos con total seguridad que $\theta \ge 3$, el límite siempre es más grande que 2. La fórmula geométrica para esa probabilidad es simplemente:

$$P(X > 2 \vert{} \theta) = \frac{\theta - 2}{\theta} = \mathbf{1 - \frac{2}{\theta}}$$

**2. Resolvemos la integral completa:**

Reemplazamos eso en nuestra gran integral:

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \int_3^\infty \left(1 - \frac{2}{\theta}\right) \cdot f(\theta \vert{} \mathbf{x}) d\theta$$

Podemos separar esto en dos integrales por la resta:

$$= \int_3^\infty 1 \cdot f(\theta \vert{} \mathbf{x}) d\theta - \int_3^\infty \frac{2}{\theta} \cdot f(\theta \vert{} \mathbf{x}) d\theta$$

- **La primera integral:** ¡Da **1** directo! (Es la integral de una distribución de probabilidad en todo su dominio).
    
- **La segunda integral:** Sacamos el 2 afuera e integramos lo que queda:
    
    $$\int_3^\infty \frac{2}{\theta} \left( \frac{23}{2} 3^{23/2} \theta^{-25/2} \right) d\theta$$
    
    Juntamos la $\theta$ del denominador con la otra potencia:
    
    $$2 \cdot \frac{23}{2} 3^{23/2} \int_3^\infty \theta^{-27/2} d\theta$$
    
    $$23 \cdot 3^{23/2} \left[ \frac{\theta^{-25/2}}{-25/2} \right]_3^\infty$$
    
    $$23 \cdot 3^{23/2} \left( 0 - \frac{3^{-25/2}}{-25/2} \right)$$
    
    Multiplicamos todo: $23 \cdot 3^{23/2} \cdot \frac{2}{25} \cdot 3^{-25/2}$.
    
    Restamos los exponentes del 3 ($23/2 - 25/2 = -2/2 = -1$).
    
    $$23 \cdot \frac{2}{25} \cdot 3^{-1} = \frac{46}{25 \cdot 3} = \mathbf{\frac{46}{75}}$$
    

**3. Resultado final:**

Volvemos a nuestra resta original:

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = 1 - \frac{46}{75}$$

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \mathbf{\frac{29}{75}} \approx \mathbf{0.3866}$$

La probabilidad predictiva estimada es de aproximadamente un **38.66%**.





![[Pasted image 20260731202616.png]]


¡Otro problema excelente! Acá seguimos con la misma familia de trampas: los límites y las funciones indicadoras. Pero esta vez, en lugar de que el parámetro $\theta$ nos ponga un "techo" (límite superior), nos pone un **"piso"** (límite inferior).

Vamos a desarmar "la cocina" paso a paso.

### Paso 1: La Verosimilitud y el límite

La función de densidad para un archivo es:

$$f(x \vert{} \theta) = \theta x^{-2} \mathbf{1}\{x \ge \theta\}$$

Tenemos una muestra de $n=2$ archivos, con tamaños $x_1 = 1.75$ y $x_2 = 2.35$.

Para armar la verosimilitud conjunta, multiplicamos la densidad evaluada en ambos archivos:

$$L(\theta \vert{} \mathbf{x}) = (\theta \cdot 1.75^{-2}) \cdot (\theta \cdot 2.35^{-2}) \cdot \mathbf{1}\{1.75 \ge \theta\} \cdot \mathbf{1}\{2.35 \ge \theta\}$$

Como los números $1.75$ y $2.35$ son constantes fijas, las descartamos para quedarnos solo con el núcleo que depende de $\theta$.

Juntamos las $\theta$ y nos queda $\theta^2$.

**La restricción lógica:**

Tenemos dos condiciones simultáneas: $\theta \le 1.75$ y $\theta \le 2.35$.

Para que el modelo sea válido, $\theta$ debe ser obligatoriamente menor o igual al archivo _más chico_ de nuestra muestra (sino, ese archivo sería imposible de observar). El más restrictivo es el 1.75.

Nuestro núcleo de verosimilitud es:

$$L(\theta \vert{} \mathbf{x}) \propto \theta^2 \mathbf{1}\{\theta \le 1.75\}$$

### Paso 2: La Distribución A Posteriori

El enunciado dice que la _a priori_ es una distribución Uniforme en el intervalo $(1, 2)$. El núcleo de una Uniforme es simplemente $1$ dentro de su intervalo:

$$f(\theta) \propto 1 \cdot \mathbf{1}\{1 < \theta < 2\}$$

Multiplicamos Verosimilitud por Priori:

$$\text{Posteriori} \propto \left( \theta^2 \mathbf{1}\{\theta \le 1.75\} \right) \cdot \mathbf{1}\{1 < \theta < 2\}$$

Al cruzar los intervalos de ambas funciones indicadoras ($\theta \le 1.75$ y $1 < \theta < 2$), el dominio final donde ambas cosas son verdad al mismo tiempo se "achica":

$$f(\theta \vert{} \mathbf{x}) \propto \theta^2 \mathbf{1}\{1 < \theta \le 1.75\}$$

**Encontramos la constante (C):**

Para que la integral dé 1, resolvemos:

$$\int_1^{1.75} C \cdot \theta^2 d\theta = 1$$

Pasamos a fracciones para no perder decimales ($1.75 = 7/4$):

$$C \left[ \frac{\theta^3}{3} \right]_1^{7/4} = 1$$

$$C \left( \frac{(7/4)^3}{3} - \frac{1^3}{3} \right) = 1$$

$$C \left( \frac{343/64}{3} - \frac{1}{3} \right) = 1$$

$$C \left( \frac{343}{192} - \frac{64}{192} \right) = 1 \implies C \left( \frac{279}{192} \right) = 1$$

Simplificamos la fracción dividiendo por 3 (queda $93/64$), y despejamos $C$:

$$\mathbf{C = \frac{64}{93}}$$

Nuestra distribución _a posteriori_ exacta es:

$$f(\theta \vert{} \mathbf{x}) = \frac{64}{93} \theta^2 \mathbf{1}\{1 < \theta \le 1.75\}$$

### Paso 3: Probabilidad Predictiva

Nos piden la probabilidad de que un nuevo archivo supere los 2 GB: $P(X_{nuevo} > 2 \vert{} \mathbf{x})$.

Aplicamos la **Ley de Esperanza Total**:

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \int_1^{1.75} P(X_{nuevo} > 2 \vert{} \theta) \cdot f(\theta \vert{} \mathbf{x}) d\theta$$

**1. Calculamos el núcleo interno $P(X_{nuevo} > 2 \vert{} \theta)$:**

Sabemos que la densidad del archivo es $\theta x^{-2}$ (solo si $x \ge \theta$).

Como en nuestra posteriori sabemos con total seguridad que nuestro parámetro $\theta$ jamás va a superar $1.75$, entonces para el valor $x=2$ la condición siempre se cumple perfecto ($2 \ge 1.75$). Integramos la densidad del archivo desde 2 hasta infinito:

$$P(X > 2 \vert{} \theta) = \int_2^\infty \theta x^{-2} dx = \theta \left[ \frac{x^{-1}}{-1} \right]_2^\infty = \theta \left[ -\frac{1}{x} \right]_2^\infty$$

$$P(X > 2 \vert{} \theta) = \theta \left( 0 - \left(-\frac{1}{2}\right) \right) = \mathbf{\frac{\theta}{2}}$$

**2. Resolvemos la integral final:**

Reemplazamos este resultado y nuestra posteriori en la gran integral:

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \int_1^{1.75} \left( \frac{\theta}{2} \right) \cdot \left( \frac{64}{93} \theta^2 \right) d\theta$$

Sacamos las constantes afuera ($1/2 \cdot 64/93 = 32/93$):

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \frac{32}{93} \int_1^{1.75} \theta^3 d\theta$$

Integramos:

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \frac{32}{93} \left[ \frac{\theta^4}{4} \right]_1^{7/4}$$

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \frac{32}{93 \cdot 4} \left[ \left(\frac{7}{4}\right)^4 - 1^4 \right]$$

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \frac{8}{93} \left[ \frac{2401}{256} - 1 \right]$$

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \frac{8}{93} \left[ \frac{2401 - 256}{256} \right] = \frac{8}{93} \left( \frac{2145}{256} \right)$$

Simplificamos cruzado (el 8 con el 256 queda 32 abajo):

$$P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \frac{2145}{93 \cdot 32} = \frac{2145}{2976}$$

Si dividimos numerador y denominador por 3 para la mínima expresión:

$$\mathbf{P(X_{nuevo} > 2 \vert{} \mathbf{x}) = \frac{715}{992} \approx 0.7208}$$

Hay aproximadamente un **72.08%** de probabilidad de que el próximo archivo supere los 2 GB.





![[Pasted image 20260731202753.png]]


¡Llegamos al último gran combo de las familias conjugadas! El modelo **Normal-Normal**.

Este es uno de los modelos más usados en la práctica porque te permite actualizar promedios de variables continuas. Cuando tanto la verosimilitud (los datos) como la _a priori_ son distribuciones Normales, la matemática tiene fórmulas directas para actualizar la media y la varianza sin tener que integrar a mano.

Vamos a definir los datos iniciales que nos da el problema:

- **Datos (Verosimilitud):** Desvío $\sigma = 2 \implies$ Varianza $\sigma^2 = 4$. Promedio muestral $\bar{x} = 12.1$.
    
- **A Priori:** Media $\mu_0 = 13$. Desvío $\tau_0 = 1 \implies$ Varianza $\tau_0^2 = 1$.
    

### (a) Hallar la distribución _a posteriori_ de $\mu$

Para la familia Normal-Normal, las fórmulas teóricas de actualización (basadas en la suma de las "precisiones", que son las inversas de las varianzas) son:

1. **Varianza a posteriori ($\tau_n^2$):**
    
    $$\frac{1}{\tau_n^2} = \frac{1}{\tau_0^2} + \frac{n}{\sigma^2}$$
    
    $$\frac{1}{\tau_n^2} = \frac{1}{1} + \frac{n}{4} = \frac{4 + n}{4} \implies \mathbf{\tau_n^2 = \frac{4}{n + 4}}$$
    
2. **Media a posteriori ($\mu_n$):**
    
    $$\mu_n = \tau_n^2 \left( \frac{\mu_0}{\tau_0^2} + \frac{n\bar{x}}{\sigma^2} \right)$$
    
    $$\mu_n = \left(\frac{4}{n + 4}\right) \left( \frac{13}{1} + \frac{n(12.1)}{4} \right)$$
    
    $$\mu_n = \frac{4(13) + n(12.1)}{n + 4} = \mathbf{\frac{52 + 12.1n}{n + 4}}$$
    

La distribución _a posteriori_ es **$\text{Normal}\left(\frac{52 + 12.1n}{n + 4}, \frac{4}{n + 4}\right)$**.

### (b) El promedio ponderado y el límite asintótico

Nos piden demostrar que la media _a posteriori_ es un promedio ponderado entre la creencia original ($13$) y el dato de la muestra ($12.1$).

Reescribimos la fórmula de $\mu_n$ separando la fracción en dos términos:

$$\mu_n = \left( \frac{4}{n + 4} \right) \cdot 13 + \left( \frac{n}{n + 4} \right) \cdot 12.1$$

Vemos claramente que tiene la forma $\gamma_n 13 + (1 - \gamma_n)12.1$, donde **$\gamma_n = \frac{4}{n + 4}$**.

**Comportamiento cuando $n \to \infty$:**

Calculamos el límite de nuestro peso $\gamma_n$ cuando el tamaño de la muestra crece infinitamente:

$$\lim_{n \to \infty} \frac{4}{n + 4} = \mathbf{0}$$

**Análisis:** Esto significa que a medida que juntamos más y más datos empíricos ($n \to \infty$), el peso de nuestra creencia _a priori_ ($\gamma_n$) desaparece y tiende a 0, haciendo que la estimación final dependa exclusivamente de lo que observamos en la realidad (la media de la muestra).

### (c) Distribución Predictiva

Queremos la distribución para una nueva varilla $X$. En el modelo Normal-Normal, la distribución predictiva también es **Normal**.

Por la Ley de Esperanza Total y Varianza Total, sus parámetros son:

- **Media Predictiva:** Es igual a la media _a posteriori_ de $\mu$.
    
    $$E[X \vert{} \text{datos}] = \mu_n = \mathbf{\frac{52 + 12.1n}{n + 4}}$$
    
- **Varianza Predictiva:** Es la varianza natural de la población ($\sigma^2$) más la incertidumbre que nos queda sobre la media ($\tau_n^2$).
    
    $$V[X \vert{} \text{datos}] = \sigma^2 + \tau_n^2 = 4 + \frac{4}{n+4} = \frac{4n + 16 + 4}{n+4} = \mathbf{\frac{4n + 20}{n + 4}}$$
    

### (d) Intervalos para $n=10$

Reemplazamos $n=10$ en todas nuestras fórmulas.

- **Media $\mu_{10}$:** $\frac{52 + 121}{14} = \frac{173}{14} \approx \mathbf{12.357}$
    
- **Varianza $\tau_{10}^2$:** $\frac{4}{14} = \frac{2}{7} \approx 0.2857 \implies$ Desvío $\tau_{10} = \sqrt{2/7} \approx \mathbf{0.5345}$
    
- **Varianza predictiva $V_X$:** $4 + \frac{2}{7} = \frac{30}{7} \approx 4.2857 \implies$ Desvío $\sigma_{pred} = \sqrt{30/7} \approx \mathbf{2.0702}$
    

Usamos el valor $Z = 1.96$ para el 95% de confianza.

**1. Intervalo para $\mu$:**

$$IC = \mu_{10} \pm 1.96 \cdot \tau_{10}$$

$$IC = 12.357 \pm 1.96 \cdot 0.5345 \implies 12.357 \pm 1.047$$

**$IC_{0.95}(\mu) = [11.310, 13.404]$**

**2. Intervalo predictivo para $X$:**

$$IC = \mu_{10} \pm 1.96 \cdot \sigma_{pred}$$

$$IC = 12.357 \pm 1.96 \cdot 2.0702 \implies 12.357 \pm 4.057$$

**$IC_{0.95}(X) = [8.300, 16.414]$**

### (e) Intervalos para $n=100$

Repetimos el proceso con $n=100$.

- **Media $\mu_{100}$:** $\frac{52 + 1210}{104} = \frac{1262}{104} \approx \mathbf{12.1346}$
    
- **Varianza $\tau_{100}^2$:** $\frac{4}{104} = \frac{1}{26} \approx 0.0384 \implies$ Desvío $\tau_{100} = \sqrt{1/26} \approx \mathbf{0.1961}$
    
- **Varianza predictiva $V_X$:** $4 + \frac{1}{26} = \frac{105}{26} \approx 4.0384 \implies$ Desvío $\sigma_{pred} = \sqrt{105/26} \approx \mathbf{2.0096}$
    

**1. Intervalo para $\mu$:**

$$IC = \mu_{100} \pm 1.96 \cdot \tau_{100}$$

$$IC = 12.1346 \pm 1.96 \cdot 0.1961 \implies 12.1346 \pm 0.3843$$

**$IC_{0.95}(\mu) = [11.750, 12.519]$**

**2. Intervalo predictivo para $X$:**

$$IC = \mu_{100} \pm 1.96 \cdot \sigma_{pred}$$

$$IC = 12.1346 \pm 1.96 \cdot 2.0096 \implies 12.1346 \pm 3.9388$$

**$IC_{0.95}(X) = [8.196, 16.073]$**

_(Nota conceptual final: Fijate cómo en el inciso E, al tener 100 datos en vez de 10, la media saltó casi por completo al 12.1 de la muestra, y el ancho del intervalo para descubrir $\mu$ se encogió muchísimo gracias a la nueva certeza)._