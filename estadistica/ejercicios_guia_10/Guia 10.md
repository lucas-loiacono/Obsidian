![[Pasted image 20260714223938.png]]

### (a) ¿Cuál debe ser la hipótesis nula y cuál la alternativa?

Para definir las hipótesis, primero identificamos el parámetro a testear:

Sea $p$ la verdadera tasa de desocupación.

El enunciado indica que las políticas se aplican si la tasa supera el nivel aceptable del 4%. En estadística, la hipótesis alternativa ($H_1$) suele ser "lo que queremos probar" o la situación que requiere tomar acción. Por lo tanto, planteamos:

- **Hipótesis Nula ($H_0$):** $p \le 0.04$
    
    (La tasa de desocupación está en un nivel aceptable. Se mantiene el _status quo_ y no es urgente aplicar nuevas políticas).
    
- **Hipótesis Alternativa ($H_1$):** $p > 0.04$
    
    (La tasa de desocupación superó el límite aceptable. Hay evidencia para detonar las políticas de fomento del empleo).
    

### (b) ¿Qué significan los errores de tipo I y los errores de tipo II?

Llevando la teoría estadística a la realidad económica de este problema:

- **Error de Tipo I (Falso Positivo):** Ocurre cuando rechazamos $H_0$ siendo verdadera.
    
    - **En este contexto:** Significa concluir que la desocupación es alta (mayor al 4%) y decidir implementar costosas políticas de fomento del empleo, cuando en realidad la tasa estaba controlada.
        
    - **Consecuencia:** Gasto público innecesario o mala asignación de recursos del Estado.
        
- **Error de Tipo II (Falso Negativo):** Ocurre cuando no rechazamos $H_0$ siendo falsa.
    
    - **En este contexto:** Significa concluir que la desocupación está en niveles aceptables y decidir no hacer nada, cuando en realidad la tasa está por encima del 4%.
        
    - **Consecuencia:** No se interviene a tiempo en una crisis laboral, dejando a la población sin ayuda, lo que puede derivar en un problema social grave.
        

### (c) ¿Qué valores considera apropiados para el nivel de significación del test?

El nivel de significación ($\alpha$) es la probabilidad máxima permitida de cometer un Error de Tipo I. Al elegirlo, hay que balancearlo con el riesgo del Error de Tipo II ($\beta$).

En el diseño de políticas públicas, generalmente **el Error de Tipo II es mucho más grave que el Error de Tipo I**. Es preferible gastar dinero de más intentando fomentar el empleo (Error Tipo I) que ignorar una crisis de desempleo masivo que deje a familias en la calle (Error Tipo II).

Como $\alpha$ y $\beta$ se mueven en direcciones opuestas (si achicás uno, agrandás el otro), **no sería apropiado usar un $\alpha$ muy estricto o pequeño** (como 0.01), porque eso haría que el test sea muy conservador, elevando enormemente el riesgo de no detectar la crisis ($\beta$ alto).

**Valores apropiados:** Sería razonable utilizar niveles de significación más altos de lo habitual para darle mayor sensibilidad al test, como **0.05** o incluso **0.10**. Esto asegura que, ante la menor evidencia estadística de que el desempleo está subiendo, el test recomiende la intervención estatal, minimizando el riesgo de dejar a la población desprotegida.







![[Pasted image 20260714224928.png]]

Primero, ordenemos los datos del problema:

- **Población:** Urna con 4 bolas.
    
- **Parámetro ($\theta$):** Cantidad de bolas rojas. Las bolas verdes son $4 - \theta$. Los valores posibles para $\theta$ son **0, 1, 2, 3 o 4**.
    
- **Hipótesis:** $H_0: \theta = 2$ vs $H_1: \theta \neq 2$
    
- **Regla de decisión:** Rechazar $H_0$ si se extraen 2 bolas del **mismo color**. No rechazar si son de **distinto color**.
    

### Escenario A: Con Reposición (Incisos a, b y c)

Como la extracción es con reposición, la probabilidad de sacar un color se mantiene constante en ambas extracciones.

- Probabilidad de sacar Roja: $P(R) = \frac{\theta}{4}$
    
- Probabilidad de sacar Verde: $P(V) = \frac{4-\theta}{4}$
    

**Probabilidad de Rechazar $H_0$ (mismo color):**

$$P(\text{Rechazar}) = P(R,R) + P(V,V) = \left(\frac{\theta}{4}\right)^2 + \left(\frac{4-\theta}{4}\right)^2$$

**Probabilidad de Aceptar $H_0$ (distinto color):**

$$P(\text{Aceptar}) = P(R,V) + P(V,R) = 2 \cdot \left(\frac{\theta}{4}\right) \cdot \left(\frac{4-\theta}{4}\right) = \frac{\theta(4-\theta)}{8}$$

#### (a) Nivel de significación del test ($\alpha$)

El nivel de significación es la probabilidad de rechazar $H_0$ cuando es verdadera (es decir, cuando $\theta = 2$).

Reemplazamos $\theta = 2$ en la probabilidad de rechazar:

$$\alpha = \left(\frac{2}{4}\right)^2 + \left(\frac{2}{4}\right)^2 = \left(\frac{1}{2}\right)^2 + \left(\frac{1}{2}\right)^2 = \frac{1}{4} + \frac{1}{4} = \frac{1}{2}$$

**$\alpha = 0.5$**

#### (b) Probabilidad de cometer error de tipo II ($\beta$)

El error de tipo II ocurre al aceptar $H_0$ cuando $H_1$ es verdadera ($\theta \neq 2$). Evaluamos la fórmula de $P(\text{Aceptar})$ para los valores donde $H_1$ es cierta:

- Si $\theta = 0$: $\beta(0) = \frac{0(4)}{8} = 0$
    
- Si $\theta = 1$: $\beta(1) = \frac{1(3)}{8} = \frac{3}{8} = 0.375$
    
- Si $\theta = 3$: $\beta(3) = \frac{3(1)}{8} = \frac{3}{8} = 0.375$
    
- Si $\theta = 4$: $\beta(4) = \frac{4(0)}{8} = 0$
    

**La máxima probabilidad de cometer un error de tipo II es $0.375$ (o 3/8)**, que ocurre cuando hay 1 o 3 bolas rojas.

#### (c) Tabular la función de potencia del test ($\pi(\theta)$)

La potencia es la probabilidad de rechazar $H_0$. Se calcula como $\pi(\theta) = 1 - \beta(\theta)$ para los valores de $H_1$, y $\pi(2) = \alpha$.

|**θ**|**β(θ)**|**π(θ) (Potencia)**|
|---|---|---|
|**0**|0|1|
|**1**|3/8|5/8 (0.625)|
|**2**|-|1/2 (0.500)|
|**3**|3/8|5/8 (0.625)|
|**4**|0|1|

_Gráficamente:_ Si dibujás estos 5 puntos en un eje cartesiano, vas a obtener una forma de "V" o parábola cóncava hacia arriba, cuyo punto más bajo (mínimo) se encuentra en $\theta = 2$ (el nivel de significación).

### Escenario B: Sin Reposición (Inciso d)

Al extraer sin reposición, las probabilidades cambian y dependemos de la distribución Hipergeométrica (casos favorables sobre casos posibles mediante combinatoria).

- Casos totales posibles: Elegir 2 bolas de 4 $\rightarrow \binom{4}{2} = 6$.
    

**Probabilidad de Aceptar $H_0$ (distinto color - 1 R y 1 V):**

$$P(\text{Aceptar}) = \frac{\binom{\theta}{1} \cdot \binom{4-\theta}{1}}{6} = \frac{\theta(4-\theta)}{6}$$

**Probabilidad de Rechazar $H_0$ (mismo color):**

$$P(\text{Rechazar}) = 1 - P(\text{Aceptar}) = 1 - \frac{\theta(4-\theta)}{6}$$

#### (a) Nivel de significación ($\alpha$) sin reposición

Evaluamos la probabilidad de rechazar cuando $\theta = 2$:

$$\alpha = 1 - \frac{2(4-2)}{6} = 1 - \frac{4}{6} = 1 - \frac{2}{3} = \frac{1}{3}$$

**$\alpha \approx 0.333$**

#### (b) Probabilidad de cometer error de tipo II ($\beta$) sin reposición

Usamos la nueva fórmula de $P(\text{Aceptar})$ para $\theta \neq 2$:

- Si $\theta = 0$: $\beta(0) = \frac{0(4)}{6} = 0$
    
- Si $\theta = 1$: $\beta(1) = \frac{1(3)}{6} = \frac{3}{6} = \frac{1}{2} = 0.5$
    
- Si $\theta = 3$: $\beta(3) = \frac{3(1)}{6} = \frac{3}{6} = \frac{1}{2} = 0.5$
    
- Si $\theta = 4$: $\beta(4) = \frac{4(0)}{6} = 0$
    

**La máxima probabilidad de cometer un error de tipo II ahora aumenta a $0.5$ (o 1/2)**.

#### (c) Tabular la función de potencia ($\pi(\theta)$) sin reposición

Nuevamente, $\pi(\theta) = 1 - \beta(\theta)$.

|**θ**|**β(θ)**|**π(θ) (Potencia)**|
|---|---|---|
|**0**|0|1|
|**1**|1/2|1/2 (0.500)|
|**2**|-|1/3 (0.333)|
|**3**|1/2|1/2 (0.500)|
|**4**|0|1|

Como verás, cambiar el método de muestreo afectó todo el test: sin reposición, el test se volvió más "conservador" (bajó el error Tipo I, $\alpha$), pero al costo de perder potencia para detectar diferencias (subió el error Tipo II, $\beta$).








![[Pasted image 20260714233159.png]]

### (a) Hallar todos los tests de nivel $\alpha = 0.05$

Un test de hipótesis se define por su **región de rechazo ($R$)**. El nivel de significación $\alpha$ es la probabilidad de rechazar $H_0$ cuando $H_0$ es verdadera.

Matemáticamente, buscamos combinaciones de valores de $X$ (nuestra región $R$) tales que la suma de sus probabilidades bajo $p_0(x)$ sea exactamente 0.05.

Miramos la fila de $p_0(x)$ en la tabla:

- $p_0(0) = 0.02$
    
- $p_0(1) = 0.03$
    
- $p_0(2) = 0.05$
    
- $p_0(3) = 0.05$
    
- $p_0(4) = 0.35$
    
- $p_0(5) = 0.50$
    

Buscamos qué valores suman exactamente 0.05. Hay tres formas posibles de lograrlo:

1. Tomar solo el valor $x = 2$ ($0.05$)
    
2. Tomar solo el valor $x = 3$ ($0.05$)
    
3. Tomar juntos los valores $x = 0$ y $x = 1$ ($0.02 + 0.03 = 0.05$)
    

Por lo tanto, **hay 3 tests posibles** de nivel exacto $\alpha = 0.05$:

- **Test 1:** Rechazar $H_0$ si $X = 2$ (Región de rechazo $R_1 = \{2\}$)
    
- **Test 2:** Rechazar $H_0$ si $X = 3$ (Región de rechazo $R_2 = \{3\}$)
    
- **Test 3:** Rechazar $H_0$ si $X \in \{0, 1\}$ (Región de rechazo $R_3 = \{0, 1\}$)



¡Son **tres regiones de rechazo completamente distintas**, lo que significa que son **tres tests diferentes**! No van todos juntos en una misma regla.

Pensalo así: vos sos el investigador y tenés que elegir **una sola regla** antes de hacer el experimento. El ejercicio te está mostrando que, si querés un riesgo de equivocarte del 5% ($\alpha = 0.05$), la matemática te ofrece 3 "menús" u opciones diferentes para elegir:

- **Opción A (Test 1):** "Voy a rechazar $H_0$ únicamente si saco un 2".
    
- **Opción B (Test 2):** "Voy a rechazar $H_0$ únicamente si saco un 3".
    
- **Opción C (Test 3):** "Voy a rechazar $H_0$ si saco un 0 o un 1".
    

### ¿Por qué no pueden estar en la misma línea (todos juntos)?

Si vos decidieras juntarlos a todos en una sola "súper región" de rechazo, tu regla sería: _"Rechazo $H_0$ si saco 0, 1, 2 o 3"_.

Como vimos antes, en las variables discretas las probabilidades se suman. Si sumás las probabilidades de esa súper región bajo $H_0$, te daría:

$$0.02 + 0.03 + 0.05 + 0.05 = 0.15$$

Tu $\alpha$ pasaría a ser $0.15$ (un 15% de riesgo de error), ¡y el enunciado te pedía que fuera exactamente del $0.05$!



### (b) Calcular $\beta$ para cada test y elegir el mejor

El error de Tipo II ($\beta$) es la probabilidad de **no rechazar $H_0$ cuando $H_1$ es verdadera**.

Una forma más rápida de calcularlo es a través de la Potencia del test ($\pi$), que es la probabilidad de rechazar correctamente. Sabemos que $\beta = 1 - \pi$.

Para cada test, calculamos la Potencia sumando las probabilidades de la región de rechazo **usando la fila $p_1(x)$**, y luego sacamos $\beta$:

**Para el Test 1 ($R_1 = \{2\}$):**

- Potencia: $P(X=2 \mid H_1) = 0.08$
    
- $\beta_1 = 1 - 0.08 = \mathbf{0.92}$
    

**Para el Test 2 ($R_2 = \{3\}$):**

- Potencia: $P(X=3 \mid H_1) = 0.12$
    
- $\beta_2 = 1 - 0.12 = \mathbf{0.88}$
    

**Para el Test 3 ($R_3 = \{0, 1\}$):**

- Potencia: $P(X=0 \mid H_1) + P(X=1 \mid H_1) = 0.04 + 0.05 = 0.09$
    
- $\beta_3 = 1 - 0.09 = \mathbf{0.91}$
    

#### ¿Cuál es el mejor test de todos?

El mejor test es siempre aquel que, para un mismo nivel $\alpha$, **minimiza el error de Tipo II ($\beta$)** (o dicho de otra forma, maximiza la potencia).

Al comparar los resultados ($0.92$, $0.88$ y $0.91$), vemos que el valor más bajo es $0.88$.

Por lo tanto, **el mejor test es el Test 2** (Rechazar $H_0$ si $X = 3$).

> ### Bonus: ¿Por qué ganó el Test 2? (Lema de Neyman-Pearson)
> 
> Resolvimos el ejercicio por "fuerza bruta" probando todas las combinaciones. Pero el Lema de Neyman-Pearson nos dice que el test más potente se construye eligiendo los valores de $X$ que tengan el mayor cociente de verosimilitudes: $\frac{p_1(x)}{p_0(x)}$.
> 
> Si hacemos esa división para cada valor de $X$:
> 
> - $x=0 \implies 0.04 / 0.02 = 2.0$
>     
> - $x=1 \implies 0.05 / 0.03 = 1.66$
>     
> - $x=2 \implies 0.08 / 0.05 = 1.6$
>     
> - **$x=3 \implies 0.12 / 0.05 = 2.4$ (¡El cociente más alto!)**
>     
> - $x=4 \implies 0.41 / 0.35 = 1.17$
>     
> - $x=5 \implies 0.30 / 0.50 = 0.6$
>     
> 
> Como ves, $x=3$ es el valor que aporta "más evidencia proporcional" a favor de $H_1$ frente a $H_0$. Por eso, matemáticamente, el test que usa la región $R=\{3\}$ era el ganador indiscutido.




Vamos a aplicarle esta lógica de probabilidades condicionadas leyendo estrictamente la tabla del ejercicio 10.3 para calcular todo.

### 1. Nivel de Significación ($\alpha$) / Error de Tipo I

- **La pregunta:** ¿Cuál es la probabilidad de rechazar $H_0$, asumiendo que $H_0$ es la realidad?
    
- **Planteo condicionado:** $P(X = 3 \mid H_0)$
    
- **Cómo se usa en el ejercicio:**
    
    - El condicional (derecha de la barra) te indica: _"Como $H_0$ es verdad, tapá el resto de la tabla y mirá únicamente la fila $p_0(x)$"_.
        
    - La acción (izquierda de la barra) te indica: _"Buscá la probabilidad de caer en tu zona de rechazo (sacar el valor 3)"_.
        
    - Vas a la fila $p_0$, buscás la columna de $x=3$, y el valor es **0.05**. Por lo tanto, tu $\alpha = 0.05$.
        

### 2. Potencia del Test ($1 - \beta$)

_(Suele ser más intuitivo calcular esto primero antes que el Error Tipo II)_

- **La pregunta:** ¿Cuál es la probabilidad de rechazar correctamente $H_0$, sabiendo que $H_1$ es la verdadera realidad?
    
- **Planteo condicionado:** $P(X = 3 \mid H_1)$
    
- **Cómo se usa en el ejercicio:**
    
    - El condicional te indica: _"Las reglas del juego cambiaron. Ahora $H_1$ es verdad. Tapá todo y mirá únicamente la fila $p_1(x)$"_.
        
    - La acción te indica: _"Seguimos evaluando si el test rechaza, así que buscá la probabilidad de sacar el valor 3 en este nuevo universo"_.
        
    - Vas a la fila $p_1$, buscás la columna de $x=3$, y el valor es **0.12**. Esa es la Potencia de este test (hay un **12%** de chances de que el test funcione y descubra que $H_1$ es cierta).
        

### 3. Error de Tipo II ($\beta$)

- **La pregunta:** ¿Cuál es la probabilidad de NO rechazar $H_0$, a pesar de que $H_1$ es la realidad?
    
- **Planteo condicionado:** $P(X \neq 3 \mid H_1)$
    
- **Cómo se usa en el ejercicio:**
    
    - El condicional te indica: _"Seguimos parados en el universo donde $H_1$ es la verdad absoluta. Tu única referencia es la fila $p_1(x)$"_.
        
    - La acción te indica: _"Acá NO tenés que rechazar. Es decir, tenés que calcular la probabilidad de que te salga cualquier valor que quede fuera de tu zona de rechazo (que $X$ sea 0, 1, 2, 4 o 5)"_.
        
    - Podés resolverlo de dos maneras:
        
        1. Sumando todos esos valores directamente en la fila de $p_1$: **0.04 + 0.05 + 0.08 + 0.41 + 0.30 = 0.88**
            
        2. Usando la propiedad matemática del complemento (como ya habías calculado la Potencia): si la probabilidad de rechazar bajo $H_1$ era **0.12**, la probabilidad de equivocarte y no rechazar es **1 - 0.12 = 0.88**.
            

Como podés ver, la notación del condicional te va guiando como si fuera un GPS: te dice exactamente en qué fila de la tabla pararte y qué columnas de esa fila sumar.




Cuando el enunciado te pide "hallar todos los tests de nivel $\alpha = 0.05$", te está pidiendo que resuelvas una ecuación usando la probabilidad condicionada.

Traducido a nuestro "machete de condicionales", el ejercicio te dio el resultado y te pidió que averigües la incógnita de esta fórmula:

$$P(X \in \text{Región de Rechazo} \mid H_0 \text{ es verdadera}) = 0.05$$

Fijate cómo se lee cada parte:

1. **El condicional ($\mid H_0 \text{ es verdadera}$):** Te dice _"plantate únicamente en la fila de $p_0(x)$"_.
    
2. **El resultado matemático ($= 0.05$):** Es tu restricción. La suma total te tiene que dar ese número exacto.
    
3. **La incógnita ($X \in \text{Región de Rechazo}$):** Es lo que vos tenías que adivinar. La pregunta que te estabas haciendo era: _"¿Qué valores de $X$ (qué columnas) tengo que elegir para cumplir con esa condición y llegar a ese número?"_.
    

Ahí fue cuando empezaste a buscar combinaciones y, usando esta misma lógica, armaste tus tres opciones:

- Descubriste que $P(X = 2 \mid H_0) = 0.05$. ¡Ese fue tu **Test 1**!
    
- Descubriste que $P(X = 3 \mid H_0) = 0.05$. ¡Ese fue tu **Test 2**!
    
- Descubriste que sumar $P(X = 0 \mid H_0) + P(X = 1 \mid H_0) = 0.02 + 0.03 = 0.05$. Lo que matemáticamente se escribe como $P(X \in \{0, 1\} \mid H_0) = 0.05$. ¡Y ese fue tu **Test 3**!
    

Entonces, buscar a mano qué números suman $0.05$ en la fila de $p_0$ no es otra cosa que resolver una ecuación de probabilidad condicionada "al revés", donde tu objetivo es encontrar la región de rechazo.


![[Pasted image 20260714233749.png]]


El primer desafío (y el más importante) es definir quién es nuestra Hipótesis Nula ($H_0$).

El enunciado dice: _"garantice... que la probabilidad de seguir comprando... cuando le hayan enviado variedad 1 sea 0.05"_.

En el mundo de los negocios, "seguir comprando" es tomar una acción (rechazar el _status quo_). Si nos enviaron la Variedad 1 (la mala), seguir comprando sería un **Error de Tipo I**. Como queremos clavar ese error exactamente en $0.05$, obligatoriamente la Variedad 1 debe ser nuestra $H_0$.

- **$H_0: \mu = 6.2$** (Me enviaron la Variedad 1).
    
- **$H_1: \mu = 7$** (Me enviaron la Variedad 2).
    
- Desvío conocido: $\sigma = 0.45$.
    

### (a) Diseñar el test de hipótesis ($\alpha = 0.05$)

Como $H_1$ plantea una media mayor ($7 > 6.2$), nuestra zona de rechazo estará en la cola derecha. Rechazaremos $H_0$ (es decir, Vivaldo seguirá comprando) si el promedio de su cosecha ($\bar{X}$) es mayor a un valor crítico $k_\alpha$.

Como en este punto aún no sabemos cuántas hectáreas ($n$) va a cultivar, armamos la regla de decisión (la "primera estandarización") de forma general, dejándola en función de $n$:

$$P_{\mu=6.2}(\bar{X} > k_\alpha) = 0.05$$

Estandarizamos usando la media de $H_0$:

$$P\left( Z > \frac{k_\alpha - 6.2}{0.45 / \sqrt{n}} \right) = 0.05$$

Buscamos en la tabla Normal el valor $Z_{0.95}$ (el que deja $0.05$ a la derecha), que sabemos que es **$1.645$**. Igualamos y despejamos $k_\alpha$:

$$\frac{k_\alpha - 6.2}{0.45 / \sqrt{n}} = 1.645 \implies k_\alpha = 6.2 + 1.645 \cdot \frac{0.45}{\sqrt{n}}$$

**Test diseñado:** Rechazar $H_0$ (seguir comprando) si $\bar{X} > 6.2 + \frac{0.74025}{\sqrt{n}}$.

### (b) Calcular $\beta$

El error $\beta$ es la probabilidad de no rechazar $H_0$ cuando en realidad $H_1$ es cierta (es decir, dejar de comprar cuando en realidad sí le habían mandado la buena).

Acá entra la "segunda estandarización". Asumimos que la media real es $\mu = 7$ y evaluamos la regla fija que armamos arriba:

$$\beta = P_{\mu=7}(\bar{X} \le k_\alpha)$$

$$\beta = P_{\mu=7}\left( \bar{X} \le 6.2 + 1.645 \cdot \frac{0.45}{\sqrt{n}} \right)$$

Estandarizamos restando la media real ($7$) y dividiendo por el error estándar ($0.45/\sqrt{n}$):

$$\beta = P\left( Z \le \frac{6.2 + 1.645 \cdot \frac{0.45}{\sqrt{n}} - 7}{0.45 / \sqrt{n}} \right)$$

Haciendo álgebra en el numerador:

$$\beta = P\left( Z \le \frac{-0.8 + 1.645 \cdot \frac{0.45}{\sqrt{n}}}{0.45 / \sqrt{n}} \right)$$

$$\beta = P\left( Z \le -\frac{0.8 \cdot \sqrt{n}}{0.45} + 1.645 \right)$$

$$\beta = \Phi(1.645 - 1.777\sqrt{n})$$

Esta es la probabilidad $\beta$ en función de cualquier cantidad de hectáreas $n$.

### (c) ¿Cuántas hectáreas deben cultivarse para que $\beta \le 0.1$?

Tomamos la fórmula de $\beta$ que acabamos de armar y la forzamos a ser menor o igual a $0.1$:

$$\Phi(1.645 - 1.777\sqrt{n}) \le 0.1$$

Buscamos en la tabla de la Normal el cuantil que acumula $0.10$ a su izquierda. Ese valor es **$-1.28$**.

Entonces, el contenido del paréntesis debe ser menor o igual a $-1.28$:

$$1.645 - 1.777\sqrt{n} \le -1.28$$

$$1.645 + 1.28 \le 1.777\sqrt{n}$$

$$2.925 \le 1.777\sqrt{n}$$

$$1.646 \le \sqrt{n}$$

$$n \ge 2.71$$

Para garantizar que el error $\beta$ sea del $10\%$ o menos, Vivaldo debe cultivar al menos **2.71 hectáreas** (si solo puede cultivar hectáreas enteras, deberá cultivar **3**).

### (d) Análisis de datos reales ($n=10$) y p-valor

Vivaldo plantó $10$ hectáreas (lo cual es genial, porque $10 > 2.71$, así que su error $\beta$ será minúsculo).

Primero, calculamos el promedio real de sus rindes ($\bar{X}$):

Suma total = $7.36 + 7.62 + 7.02 + 6.99 + 6.66 + 6.74 + 6.25 + 6.41 + 6.91 + 7.11 = 69.07$

**$\bar{X} = \frac{69.07}{10} = 6.907$**

Ahora calculamos el **p-valor**. Es la probabilidad de obtener un promedio de $6.907$ (o uno aún más extremo) asumiendo que le hubieran mandado la variedad mala ($H_0$):

$$p\text{-valor} = P_{\mu=6.2}(\bar{X} > 6.907)$$

Estandarizamos (esta vez usamos $n=10$):

$$Z_{obs} = \frac{6.907 - 6.2}{0.45 / \sqrt{10}} = \frac{0.707}{0.1423} \approx 4.968$$

$$p\text{-valor} = P(Z > 4.968)$$

**Conclusión:** Un valor $Z$ de casi $5$ es absurdamente grande (la tabla suele cortar en $3.5$). El p-valor es prácticamente **$0$** ($0.000000...$).

Como el p-valor es muchísimo menor que nuestro $\alpha$ ($0.05$), rechazamos categóricamente $H_0$.

**Vivaldo debe quedarse tranquilo, confirmar que le enviaron la Variedad 2, y seguir comprándole a _La porota_.**