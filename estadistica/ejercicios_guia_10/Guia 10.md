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


Los profesores suelen escribir estos enunciados usando términos de la vida real ("comprar", "romperse", "curar", "explotar") justamente para que no sea tan obvio quién es $H_0$ y quién es $\alpha$.

Siempre que te den un ejercicio así, tu primer paso tiene que ser armar un "espejo" entre la fórmula estadística y la frase del enunciado usando la probabilidad condicional.

Funciona como un traductor automático de tres pasos:

### 1. Escribir el "Lado del Negocio" (El enunciado)

Leés el enunciado y traducís lo que pide a una notación condicional simple, sin pensar en hipótesis todavía.

- _Enunciado:_ "probabilidad de seguir comprando... cuando le hayan enviado de la variedad 1 sea 0.05".
    
- _Traducción:_ $P(\text{Seguir comprando} \mid \text{Variedad 1}) = 0.05$
    

### 2. Escribir el "Lado de la Estadística" (La teoría)

Anotás las dos definiciones inquebrantables de los errores en estadística:

- **Error Tipo I ($\alpha$):** $P(\text{Rechazar } H_0 \mid H_0 \text{ es verdadera})$
    
- **Error Tipo II ($\beta$):** $P(\text{No rechazar } H_0 \mid H_1 \text{ es verdadera})$
    

### 3. Hacer el cruce (El "Match")

Ahora simplemente alineás tu enunciado con la fórmula teórica que encaje perfecto. Como el enunciado te está exigiendo clavar una probabilidad desde el **diseño** del test, te está dando tu $\alpha$.

Entonces enfrentás las dos fórmulas:

$$P(\text{Seguir comprando} \mid \text{Variedad 1}) = 0.05$$

$$P(\text{Rechazar } H_0 \mid H_0 \text{ es verdadera}) = \alpha$$

Al mirarlas juntas, el problema se resuelve solo:

- **La Condición (Derecha):** Para que las fórmulas coincidan, el universo "Variedad 1" tiene que ser tu $H_0$. Por lo tanto, $H_0: \mu = 6.2$.
    
- **La Acción (Izquierda):** La acción de "Seguir comprando" equivale a "Rechazar $H_0$".
    
- **El Nivel de Significación:** $\alpha = 0.05$.
    

### ¿Por qué esto es tan poderoso?

Porque una vez que hiciste este cruce, el resto del ejercicio es totalmente mecánico.

Como ya sabés que $H_0: \mu = 6.2$ (Variedad 1) y que la alternativa lógica del problema es $H_1: \mu = 7$ (Variedad 2), al ver que $7 > 6.2$, sabés instantáneamente que tu test rechaza hacia la derecha.

Tu regla de decisión genérica queda armada: **"Voy a rechazar $H_0$ (y seguir comprando) si mi promedio muestral $\bar{X}$ es mayor a un valor crítico $k$"**.

Y para calcular ese valor $k$, adiviná qué usás: ¡la misma ecuación condicional que armaste al principio!

$$P(\bar{X} > k \mid \mu = 6.2) = 0.05$$

Estandarizás con la Normal $Z$, buscás en la tabla, despejás $k$, y el diseño del test está terminado sin dudar ni un segundo de tu planteo inicial. Si usás siempre este método de enfrentar el condicional del texto con el condicional de la fórmula, es matemáticamente imposible que definas mal las hipótesis.





_"Si Vivaldo compró la Variedad 2 y quiere confirmar que es la Variedad 2, ¡esa debería ser su hipótesis principal!"_.

Pero la estadística no funciona con la intuición humana de "qué es lo que espero que pase", sino con **cuál es el error que quiero controlar desde el diseño**.

Vamos a desarmar el enunciado de la **image_0255c4.png** usando el "machete" de probabilidades condicionadas que veníamos usando. Te prometo que con eso sale solo.

### 1. El diseño manda sobre $\alpha$

En todo test de hipótesis, el único valor que vos fijás "a dedo" desde el principio es el Nivel de Significación ($\alpha$). Es decir, vos armás tu región de rechazo específicamente para garantizar que la probabilidad de cometer el Error Tipo I sea ese número exacto.

El inciso **(a)** te dice: _"Diseñar un test... que garantice... que la probabilidad de seguir comprando... cuando le hayan enviado de la variedad 1 sea 0.05"_.

Como te están pidiendo _diseñar_ el test para clavar una probabilidad en $0.05$, ese $0.05$ tiene que ser obligatoriamente tu $\alpha$.

### 2. El cruce de variables

Escribamos la definición de $\alpha$ y abajo la frase del enunciado:

1. **Definición teórica:** $\alpha = P(\text{Rechazar } H_0 \mid H_0 \text{ es verdadera}) = 0.05$
    
2. **Frase del enunciado:** $P(\text{Seguir comprando} \mid \text{Enviaron Variedad 1}) = 0.05$
    

Si comparás las dos cosas como si fuera un espejo, el mapeo es directo y obligatorio:

- La acción **"Rechazar $H_0$"** equivale a la decisión de **"Seguir comprando"**.
    
- El universo **"$H_0$ es verdadera"** equivale al escenario **"Enviaron Variedad 1"**.
    

¡Ahí está la respuesta matemática! Para que la cuenta del diseño te cierre usando ese 0.05 como tu $\alpha$, no te queda otra opción que definir $H_0: \mu = 6.2$ (Variedad 1).

### ¿Qué pasaría si usás la Variedad 2 como $H_0$?

Hagamos el ejercicio mental de plantearlo al revés, como te dictaba tu intuición:

- $H_0: \mu = 7$ (Me enviaron la Variedad 2).
    
- $H_1: \mu = 6.2$ (Me enviaron la Variedad 1).
    

Si armás el test así, la acción lógica si decidís "No rechazar $H_0$" (te creés que tenés la buena) es **Seguir comprando**.

Ahora volvamos a leer la condición que te pide el problema: _"que la probabilidad de seguir comprando... cuando le hayan enviado de la variedad 1 sea 0.05"_.

En este test invertido, esa probabilidad se escribiría así:

$$P(\text{No rechazar } H_0 \mid H_1 \text{ es verdadera})$$

¿Te suena esa fórmula? ¡Esa es la definición de $\beta$ (Error Tipo II)!

Si plantearas la Variedad 2 como $H_0$, el enunciado te estaría dando el valor de $\beta = 0.05$ de entrada, pero no te estaría dando ningún $\alpha$ para que puedas diseñar la región de rechazo (y encima el inciso **b** te pide calcular $\beta$, así que no puede ser un dato).

### Resumen en términos de "Negocios"

La hipótesis nula ($H_0$) siempre se plantea como "el peor escenario" o "la presunción de inocencia" sobre la cual querés ser muy conservador antes de tomar una acción fuerte.

Vivaldo es desconfiado. Su posición por defecto ($H_0$) es: _"Me estafaron, me mandaron la Variedad 1"_. Él solamente va a tomar la acción fuerte de **Seguir comprando** (Rechazar $H_0$) si la muestra de su cosecha le da un rinde tan alto que le demuestra, con un 95% de seguridad, que la hipótesis de la estafa es insostenible.







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






### ¿Cómo funciona la dinámica de este ejercicio completo?

Si mirás la foto "image_0255c4.png" con todos los incisos, vas a notar cómo el autor del problema fue armando una trampa progresiva:

- **Inciso (a) y (b):** Te pide armar la regla del test y calcular el Error Tipo II ($\beta$). Como no tenés idea de cuántas hectáreas plantó, **estás obligado a dejar todo en función de $n$**. Las respuestas de estos dos incisos son fórmulas, no números finales.
    
- **Inciso (c):** Te pregunta explícitamente _"¿Cuántas hectáreas deben cultivarse para que $\beta \le 0.1$?"_. Acá es donde agarramos la fórmula que dejaste armada con la $n$ adentro, la igualamos a $0.1$, y usamos álgebra para despejar qué valor de $n$ necesitamos. ¡Para esto servía dejar la letra viva!
    
- **Inciso (d):** Recién acá, al final de todo, la historia avanza y te dice _"Vivaldo cultivó 10 hectáreas..."_. En este punto por fin te regalan el dato $n = 10$, y podés reemplazar ese número en tu regla para hacer las cuentas finales.
    

### La razón matemática (El Error Estándar)

Desde la teoría, cuando hacés un test sobre el promedio de una muestra ($\bar{X}$), la dispersión de ese promedio no es simplemente el desvío de la población ($\sigma$), sino el **Error Estándar**, que se calcula dividiendo por la raíz de la muestra:

$$\text{Error Estándar} = \frac{\sigma}{\sqrt{n}}$$

Como la cantidad de hectáreas ($n$) impacta directamente en qué tan "exacto" es tu promedio muestral, es un parámetro fundamental del test. A mayor muestra (más hectáreas), la curva se hace más finita y es más fácil detectar diferencias. Por eso, no podés ignorar la $n$ al estandarizar tu variable $Z$, y si el enunciado no te la da, la tenés que arrastrar como una incógnita.






### Paso 1: Definir la nueva variable y sus parámetros

Vamos a definir a nuestra variable $T$ como la **suma total** de los rindes de todas las hectáreas cultivadas:

$$T = \sum_{i=1}^n X_i$$

Como estamos diseñando el test ($\alpha = 0.05$), tenemos que plantarnos bajo el universo donde $H_0$ es verdadera ($\mu = 6.2$ y $\sigma = 0.45$).

Por las propiedades de la suma de variables aleatorias, calculamos la esperanza y el desvío de esta nueva variable $T$:

- **Esperanza total:** $E(T) = n \cdot \mu = n \cdot 6.2 = 6.2n$
    
- **Desvío total:** $\sigma_T = \sqrt{n} \cdot \sigma = 0.45\sqrt{n}$
    

### Paso 2: Plantear la inecuación con el condicional

Como nuestra hipótesis alternativa sigue siendo $H_1: \mu = 7$, sabemos que rindes más altos nos hacen desconfiar de $H_0$. Por lo tanto, rechazaremos $H_0$ si nuestra cosecha total ($T$) supera un cierto límite (valor crítico $k_T$).

Usando el condicional para el $\alpha = 0.05$:

$$P(T > k_T \mid H_0 \text{ es verdadera}) = 0.05$$

### Paso 3: Estandarizar a $Z$ y despejar

Ahora estandarizamos esa inecuación usando los parámetros totales que calculamos en el Paso 1:

$$P\left( Z > \frac{k_T - E(T)}{\sigma_T} \right) = 0.05$$

Reemplazamos con nuestros datos:

$$P\left( Z > \frac{k_T - 6.2n}{0.45\sqrt{n}} \right) = 0.05$$

Como ya sabemos por la tabla Normal, el valor de $Z$ que deja un área de 0.05 hacia la derecha es $1.645$. Entonces igualamos:

$$\frac{k_T - 6.2n}{0.45\sqrt{n}} = 1.645$$

Y ahora simplemente despejamos nuestra incógnita ($k_T$):

$$k_T - 6.2n = 1.645 \cdot 0.45\sqrt{n}$$

$$k_T = 6.2n + 0.74025\sqrt{n}$$

### Regla de Decisión Final (Versión Sumatoria)

**Se rechazará $H_0$ (Vivaldo seguirá comprando) si la sumatoria de las toneladas cosechadas resulta:**

$$\sum X_i > 6.2n + 0.74025\sqrt{n}$$

**La comprobación mágica:** Si te fijás bien, si agarrás la regla de decisión final a la que llegaste vos antes con el promedio ($\bar{X} > 6.2 + \frac{0.74025}{\sqrt{n}}$) y **multiplicás ambos lados de esa inecuación por $n$**, vas a llegar exactamente a esta misma fórmula de la sumatoria. ¡Es la misma regla de rechazo vista con otra lupa!



### En resumen para los exámenes:

Aunque matemáticamente podés jugar con las escalas (usar el total, usar el promedio, etc.), la regla de oro para no complicarte la vida en los ejercicios es **usar el estadístico natural del parámetro que estás evaluando**:

- Si las hipótesis son sobre la media ($\mu$) $\implies$ Armá el test con el promedio muestral ($\bar{X}$).
    
- Si las hipótesis son sobre una proporción ($p$) $\implies$ Armá el test con la proporción muestral ($\hat{p}$).
    
- Si las hipótesis son sobre la varianza ($\sigma^2$) $\implies$ Armá el test con la varianza muestral ($S^2$).




## Punto b
### Paso 1: Traer la regla de decisión de la sumatoria

Antes habíamos calculado que, usando la sumatoria, la regla era **rechazar $H_0$ si:**

$$T > 6.2n + 0.74025\sqrt{n}$$

Por lo tanto, la condición de **No rechazar $H_0$** (que es lo que necesitamos para calcular $\beta$) es la contraria:

$$T \le 6.2n + 0.74025\sqrt{n}$$

### Paso 2: Plantear el nuevo universo ($H_1$) para la sumatoria

Como estamos calculando $\beta$, sabemos que $H_1$ es verdadera, es decir, el rinde real es $\mu = 7$.

¿Qué pasa con nuestra variable $T$ (la suma total) en este nuevo universo?

- Su nueva esperanza es: $E(T) = n \cdot 7 = \mathbf{7n}$
    
- Su desvío total sigue siendo: $\sigma_T = \mathbf{0.45\sqrt{n}}$
    

### Paso 3: Calcular $\beta$ y estandarizar

Planteamos la probabilidad del Error Tipo II:

$$\beta = P(T \le 6.2n + 0.74025\sqrt{n} \mid \mu = 7)$$

Ahora estandarizamos. La fórmula para estandarizar la sumatoria es $Z = \frac{T - E(T)}{\sigma_T}$. Reemplazamos $E(T)$ por el nuevo valor $7n$:

$$\beta = P\left( Z \le \frac{(6.2n + 0.74025\sqrt{n}) - 7n}{0.45\sqrt{n}} \right)$$

### Paso 4: Despeje algebraico

Fijate qué pasa en el numerador cuando juntamos las "$n$" con las "$n$":

$$6.2n - 7n = -0.8n$$

Reescribimos la fracción:

$$\beta = P\left( Z \le \frac{-0.8n + 0.74025\sqrt{n}}{0.45\sqrt{n}} \right)$$

Ahora repartimos el denominador ($0.45\sqrt{n}$) para los dos términos:

$$\beta = P\left( Z \le \frac{-0.8n}{0.45\sqrt{n}} + \frac{0.74025\sqrt{n}}{0.45\sqrt{n}} \right)$$

Simplificamos cada término:

1. En el primer término: $\frac{n}{\sqrt{n}} = \sqrt{n}$. Y la división $-0.8 / 0.45 = -1.778$. Nos queda **$-1.778\sqrt{n}$**.
    
2. En el segundo término: Las $\sqrt{n}$ se tachan y $0.74025 / 0.45 = 1.645$. Nos queda **$1.645$**.
    

Volvemos a armar la inecuación:

$$\beta = P( Z \le -1.778\sqrt{n} + 1.645 )$$

### Conclusión

¡Llegaste a la misma fórmula!

$$\beta = \Phi(1.645 - 1.778\sqrt{n})$$

Podés estandarizar con el estadístico que más te guste ($\bar{X}$ o la sumatoria $T$). Como representan el mismo experimento físico (la cosecha de Vivaldo), la probabilidad de equivocarte ($\beta$) tiene que ser idéntica sin importar con qué lupa matemática mires el problema.







Vamos a resolverlo calculando el **p-valor** (o valor $p$).

### Paso 1: Recolectar la información de la muestra empírica

El enunciado nos da los rindes de $n = 10$ hectáreas.

Lo primero que tenemos que hacer es resumir esa muestra. Como en los incisos anteriores vimos que podíamos usar el Promedio ($\bar{X}$) o la Sumatoria ($T$), podemos elegir el que más nos guste. Vamos con el promedio que es el más clásico.

Sumamos los 10 valores:

$$7.36 + 7.62 + 7.02 + 6.99 + 6.66 + 6.74 + 6.25 + 6.41 + 6.91 + 7.11 = 69.07 \text{ toneladas totales}$$

Calculamos el promedio de la muestra ($\bar{x}_{obs}$):

$$\bar{x}_{obs} = \frac{69.07}{10} = \mathbf{6.907 \text{ toneladas/hectárea}}$$

### Paso 2: ¿Qué es el p-valor?

El p-valor es, conceptualmente, hacerle una pregunta al universo de $H_0$:

_"Asumiendo que me mandaste la Variedad 1 ($H_0$ es verdad), ¿cuál era la probabilidad de que, por pura casualidad, yo consiguiera una cosecha tan buena como la que acabo de tener (6.907) o incluso mejor?"_

Matemáticamente, como nuestro test rechaza hacia la derecha (valores grandes nos hacen sospechar de $H_0$), el p-valor se calcula así:

$$\text{p-valor} = P(\bar{X} > 6.907 \mid \mu = 6.2)$$

### Paso 3: Calcular el p-valor

Para resolver esa probabilidad, tenemos que estandarizar nuestro resultado empírico ($6.907$) usando los parámetros de $H_0$:

$$Z_{obs} = \frac{\bar{x}_{obs} - \mu}{\sigma / \sqrt{n}}$$

$$Z_{obs} = \frac{6.907 - 6.2}{0.45 / \sqrt{10}}$$

$$Z_{obs} = \frac{0.707}{0.1423}$$

$$Z_{obs} \approx 4.968$$

Ahora buscamos la probabilidad:

$$\text{p-valor} = P(Z > 4.968)$$

Si vas a la tabla de la Normal Estándar, vas a ver que el gráfico suele terminar en $Z = 3.49$. Un valor de $Z = 4.968$ está exageradamente lejos hacia la derecha en la cola de la campana.

Esto significa que el área a su derecha es prácticamente nula.

$$\text{p-valor} \approx 0$$

### Paso 4: Tomar la decisión

La regla universal del p-valor para decidir en un test de hipótesis es:

- Si $\text{p-valor} < \alpha \implies$ **Rechazo $H_0$**
    
- Si $\text{p-valor} \ge \alpha \implies$ **No rechazo $H_0$**
    

En nuestro diseño (inciso a), Vivaldo había fijado un nivel de exigencia de $\alpha = 0.05$.

Como $0 < 0.05$, la decisión estadística es **Rechazar $H_0$**.

**Conclusión para Vivaldo ("¿Qué debe hacerse?"):**

La evidencia en contra de $H_0$ (Variedad 1) es abrumadora. Las chances de conseguir casi 7 toneladas por hectárea si las semillas fueran malas eran prácticamente de cero. Por lo tanto, Vivaldo debe descartar su sospecha de que lo estafaron y **debe tomar la decisión de seguir comprando** sem



![[Pasted image 20260720193547.png]]



### 1. Datos y la Nueva Variable (Sumatoria)

Nuestra muestra es de $n = 10$ capacitores. En lugar de mirar el promedio, vamos a mirar el **voltaje total** si sumáramos las rupturas de los 10 capacitores juntos.

Definimos $T = \sum_{i=1}^{10} X_i$

Las hipótesis siguen siendo sobre la media original:

- $H_0: \mu = 200$
    
- $H_1: \mu > 200$
    

Pero ahora necesitamos saber cómo se comporta nuestra variable $T$ bajo el universo de $H_0$:

- **Esperanza Total:** $E(T) = n \cdot \mu = 10 \cdot 200 = \mathbf{2000}$
    
- **Varianza Total:** $Var(T) = n \cdot \sigma^2 = 10 \cdot 25 = \mathbf{250}$
    
- **Desvío Total:** $\sigma_T = \sqrt{250} = \mathbf{15.811}$
    

### 2. Diseño del Test de Hipótesis

Queremos un Nivel de Significación $\alpha = 0.05$.

Como $H_1$ afirma que la media es _mayor_, un voltaje total sospechosamente grande nos hará rechazar $H_0$. Planteamos el condicional:

$$P(\text{Rechazar } H_0 \mid H_0 \text{ es verdadera}) = 0.05$$

$$P(T > k_T \mid \mu = 200) = 0.05$$

Estandarizamos usando los parámetros totales que calculamos arriba:

$$P\left(Z > \frac{k_T - 2000}{15.811}\right) = 0.05$$

Buscamos en la tabla Normal el valor de $Z$ que deja un área de 0.05 a la derecha, que es **$1.645$**. Igualamos y despejamos nuestro límite $k_T$:

$$\frac{k_T - 2000}{15.811} = 1.645$$

$$k_T - 2000 = 1.645 \cdot 15.811$$

$$k_T = 2000 + 26.01$$

$$k_T = 2026.01$$

**Regla de decisión diseñada:** Se rechazará $H_0$ si la suma de los voltajes de los 10 capacitores resulta $T > 2026.01$.

_(Nota de color: fíjate que 2026.01 es exactamente 10 veces el 202.60 que nos había dado con el promedio. ¡Todo cierra!)_

### 3. Calcular la probabilidad de decidir erróneamente

Ahora el enunciado cambia las reglas: _"cuando el verdadero valor de la media... es 210"_.

Si $\mu = 210$, $H_1$ es verdad. El error (Tipo II, $\beta$) ocurre si nuestra muestra no logra superar el límite y, por ende, **No rechazamos $H_0$**.

Planteamos el condicional:

$$\beta = P(\text{No rechazar } H_0 \mid \mu = 210)$$

Traducido a nuestra regla de la sumatoria (no superar el límite de 2026.01):

$$\beta = P(T \le 2026.01 \mid \mu = 210)$$

Para estandarizar ahora, necesitamos la **nueva esperanza** de $T$ en este universo donde $\mu = 210$:

- **Nueva Esperanza Total:** $E(T) = 10 \cdot 210 = \mathbf{2100}$
    
    _(El desvío total sigue siendo 15.811 porque la varianza no cambia)._
    

Estandarizamos:

$$\beta = P\left(Z \le \frac{2026.01 - 2100}{15.811}\right)$$

$$\beta = P\left(Z \le \frac{-73.99}{15.811}\right)$$

$$\beta = P(Z \le -4.68)$$

Buscamos $-4.68$ en la tabla de la Normal (o recordamos que a partir de -3.5 el área es minúscula).

**Respuesta final:** $\beta \approx 0$.

Al mirarlo con la sumatoria, es incluso más gráfico: si tu barrera para rechazar era conseguir 2026 puntos, y la realidad es que el sistema te tira 2100 puntos en promedio, la probabilidad de que justo tengas tan mala suerte de sumar menos de 2026 es nula



![[Pasted image 20260720203706.png]]



¡Vamos a resolver el ejercicio **10.6** de la **image_72fe8b.png**!

Como me comentaste que te resulta más fácil de ver usando la **sumatoria** ($T$), vamos a encararlo directamente por ese camino. ¡Vas a ver que sale rapidísimo aplicando la misma lógica de condicionales!

### Paso 1: Ordenar los datos y armar la sumatoria empírica

- **Población:** Distribución normal con varianza $\sigma^2 = 25 \implies \sigma = 5$.
    
- **Muestra:** $n = 36$ varillas.
    
- **Nivel de Significación:** $\alpha = 0.05$.
    

Acá hay un detalle: el enunciado te da como dato empírico el **promedio** de la muestra ($\bar{x}_{obs} = 51.74$). Como nosotros queremos usar la sumatoria total, simplemente lo multiplicamos por la cantidad de varillas:

$$T_{obs} = n \cdot \bar{x}_{obs} = 36 \cdot 51.74 = \mathbf{1862.64 \text{ cm totales}}$$

_(Esa es la longitud real de todas las varillas puestas una al lado de la otra)._

### Paso 2: Plantear las hipótesis

La pregunta del problema es: _"¿se puede garantizar que la longitud media... supera los 50 cm?"_.

Como eso es lo que queremos demostrar, va a nuestra hipótesis alternativa ($H_1$).

- $H_0: \mu = 50$
    
- $H_1: \mu > 50$ (Es un test unilateral derecho).
    

### Paso 3: Preparar el universo de $H_0$ para la sumatoria

Como vamos a calcular el p-valor, necesitamos saber cuáles son las reglas del juego si $H_0$ fuera verdadera ($\mu = 50$).

Calculamos la esperanza y el desvío para nuestra variable $T$ (la suma de 36 varillas):

- **Esperanza Total:** $E(T) = n \cdot \mu = 36 \cdot 50 = \mathbf{1800}$
    
- **Desvío Total:** $\sigma_T = \sqrt{n} \cdot \sigma = \sqrt{36} \cdot 5 = 6 \cdot 5 = \mathbf{30}$
    

### Paso 4: Calcular el p-valor

El p-valor es la probabilidad de que, asumiendo que $H_0$ es cierta, obtengamos de casualidad una sumatoria tan grande o peor que la que observamos en la realidad ($1862.64$).

Planteamos nuestro condicional:

$$\text{p-valor} = P(T > 1862.64 \mid \mu = 50)$$

Estandarizamos usando los parámetros de $H_0$ que calculamos en el Paso 3:

$$\text{p-valor} = P\left(Z > \frac{1862.64 - 1800}{30}\right)$$

$$\text{p-valor} = P\left(Z > \frac{62.64}{30}\right)$$

$$\text{p-valor} = P(Z > 2.088)$$

Buscamos en la tabla Normal el área a la derecha de $2.088$ (podés redondear a $2.09$). El área acumulada a izquierda para $2.09$ es aproximadamente $0.9817$.

Por lo tanto, el área a la derecha es $1 - 0.9817 = 0.0183$.

$$\text{p-valor} = \mathbf{0.0183}$$

### Paso 5: Conclusión y decisión

Ahora comparamos nuestro p-valor con el nivel de significación que nos exigía el problema:

- $\text{p-valor} = 0.0183$
    
- $\alpha = 0.05$
    

Como **$\text{p-valor} < \alpha$**, la decisión estadística es **Rechazar $H_0$**.

**Respuesta a la pregunta del enunciado:**

Sí, se puede garantizar (con un nivel de significación del 0.05) que la longitud media de las varillas supera los 50 cm. La probabilidad de haber conseguido una muestra con varillas tan largas si la máquina estuviera calibrada en 50 cm era de apenas 1.83%, lo cual es evidencia suficiente para afirmar que la media real es mayor.


![[Pasted image 20260721204041.png]]


¡Excelente! Vamos a resolver el ejercicio **10.7** de la **image_0e71a5.png** siguiendo el método que te resulta más cómodo: usando la **sumatoria total** ($T$) y planteando las probabilidades condicionadas.

Este ejercicio tiene una pequeña "trampa" conceptual respecto a los anteriores, ¡así que viene bárbaro para seguir sumando herramientas!

### Paso 1: Ordenar los datos y armar la sumatoria empírica

- **Población:** Distribución normal con desvío $\sigma = 0.75$.
    
- **Muestra:** $n = 53$ mediciones.
    
- **Nivel de Significación:** $\alpha = 0.05$.
    

El enunciado nos da el promedio observado ($\bar{x}_{obs} = 8.616$). Para trabajar con tu método, lo pasamos a la sumatoria total multiplicando por $n$:

$$T_{obs} = n \cdot \bar{x}_{obs} = 53 \cdot 8.616 = \mathbf{456.648}$$

### Paso 2: Plantear las hipótesis (¡Atención acá!)

Fijate cómo está redactado el problema: _"decidir... si hay suficiente evidencia para rechazar la hipótesis $\mu = 8.789$"_.

A diferencia de los ejercicios anteriores donde te decían explícitamente "el productor afirma que es **mayor** a 200" o "¿se puede garantizar que **supera** los 50?", acá **no te dan una dirección**. Solo te preguntan si podés rechazar ese valor exacto.

Cuando pasa esto, estamos frente a un **test bilateral** (o de dos colas). Nos va a parecer sospechoso tanto si la sumatoria da excesivamente grande, como si da excesivamente chica.

- $H_0: \mu = 8.789$
    
- $H_1: \mu \neq 8.789$
    

### Paso 3: Preparar el universo de $H_0$ para la sumatoria

Asumiendo que $H_0$ es verdad ($\mu = 8.789$), calculamos cómo debería comportarse nuestra variable $T$:

- **Esperanza Total:** $E(T) = n \cdot \mu = 53 \cdot 8.789 = \mathbf{465.817}$
    
- **Desvío Total:** $\sigma_T = \sqrt{n} \cdot \sigma = \sqrt{53} \cdot 0.75 \approx 7.2801 \cdot 0.75 \approx \mathbf{5.46}$
    

### Paso 4: Calcular el p-valor

Como nuestro test es bilateral, el p-valor se calcula buscando la probabilidad de caer en el extremo de nuestra muestra observada, y **multiplicándola por 2** (porque tenemos que contemplar la misma probabilidad de error hacia el otro lado de la campana).

Como nuestra sumatoria real ($456.648$) dio menor que la esperanza teórica ($465.817$), miramos hacia la izquierda:

$$\text{p-valor} = 2 \cdot P(T \le 456.648 \mid \mu = 8.789)$$

Estandarizamos usando los parámetros de $H_0$ del Paso 3:

$$\text{p-valor} = 2 \cdot P\left(Z \le \frac{456.648 - 465.817}{5.46}\right)$$

$$\text{p-valor} = 2 \cdot P\left(Z \le \frac{-9.169}{5.46}\right)$$

$$\text{p-valor} = 2 \cdot P(Z \le -1.679)$$

Buscamos el valor de $-1.68$ en la tabla de la Normal Estándar, lo cual nos da un área de **$0.0465$**.

$$\text{p-valor} = 2 \cdot 0.0465$$

$$\text{p-valor} = \mathbf{0.093}$$

### Paso 5: Conclusión y decisión

Regla de oro del p-valor:

- Comparamos nuestro $\text{p-valor}$ ($0.093$) con el $\alpha$ ($0.05$).
    

Como **$0.093 > 0.05$**, la decisión estadística es **No rechazar $H_0$**.

**Respuesta final:**

El p-valor es $0.093$. Por lo tanto, con un nivel de significación del 0.05, **no hay suficiente evidencia estadística para rechazar la hipótesis** de que la media poblacional es 8.789. La diferencia entre lo que midió James Short y el valor teórico podría deberse simplemente a la fluctuación natural (casualidad) de las 53 mediciones.



![[Pasted image 20260721234132.png]]



Lo vamos a plantear directamente usando la **sumatoria total ($T$)** que veníamos usando, pero te aviso desde ya que este problema trae una "trampa" nueva (y muy importante) respecto a los anteriores.

### La trampa: ¿Dónde está $\sigma$?

Si leés el enunciado de nuevo, te dice que la distribución es normal, pero **nunca te da la varianza o el desvío poblacional ($\sigma$)**. En los problemas anteriores te decían "varianza 25" o "desvío 0.45", pero acá te dan solo los 10 tiempos sueltos y arreglate.

Cuando no conocemos el desvío de la población y tenemos que calcularlo a partir de nuestra muestra ($S$), **ya no podemos usar la tabla Normal ($Z$)**. Entra a jugar una tabla nueva que se llama **$t$ de Student**. Funciona igual que la Normal, pero sus colas son un poco más "gordas" para compensar la incertidumbre de no conocer el verdadero desvío.

¡Aclarado esto, vamos a los pasos!

### Paso 1: Recopilar y procesar la muestra empírica

- **Muestra ($n$):** 10 viajes.
    
- **Nivel de Significación ($\alpha$):** 0.1
    

Calculamos nuestra sumatoria real observada sumando los 10 tiempos:

$$T_{obs} = 41.1 + 42.2 + 40.5 + 39.9 + 40.3 + 36.6 + 39.3 + 42.5 + 37.8 + 40.5 = \mathbf{400.7 \text{ minutos}}$$

Como te comentaba antes, necesitamos calcular el desvío estándar de esta muestra ($S$). Para eso calculamos el promedio ($\bar{x} = 40.07$) y aplicamos la fórmula de varianza muestral. Para no aburrirte con las cuentas, el resultado del desvío de esta muestra da:

$$S \approx 1.818$$

### Paso 2: Plantear las hipótesis

Juan sugiere un camino para **reducir** el tiempo. Aparicio por defecto tarda 40 minutos.

- $H_0: \mu = 40$ (El camino nuevo no cambia nada, se tarda lo mismo).
    
- $H_1: \mu < 40$ (El camino nuevo sí reduce el tiempo, es un **test unilateral izquierdo**).
    

### Paso 3: Preparar el universo de $H_0$ para la sumatoria

Bajo el universo de $H_0$ ($\mu = 40$), veamos cómo se debería comportar nuestra suma total de los 10 viajes:

- **Esperanza Total:** $E(T) = n \cdot \mu = 10 \cdot 40 = \mathbf{400 \text{ minutos}}$.
    
- **Desvío Total Estimado:** Como no tenemos $\sigma$, usamos nuestro $S$ multiplicado por $\sqrt{n}$:
    
    $$S_T = \sqrt{n} \cdot S = \sqrt{10} \cdot 1.818 \approx \mathbf{5.749}$$
    

### Paso 4: Diseñar la zona de rechazo (con $t$ de Student)

Queremos que nuestro riesgo de error sea del 10%. Como la hipótesis $H_1$ apunta hacia la izquierda (tiempos menores), vamos a rechazar $H_0$ si nuestra suma total da _sospechosamente baja_.

$$P(T < k_T \mid \mu = 40) = 0.1$$

Estandarizamos, pero esta vez a la variable $t$ de Student:

$$P\left(t_{n-1} < \frac{k_T - 400}{5.749}\right) = 0.1$$

La tabla $t$ de Student requiere que le pases los "grados de libertad", que siempre son $n - 1$. En este caso: $10 - 1 = \mathbf{9}$ grados de libertad.

Buscamos en la tabla $t$ con 9 grados de libertad, el valor que deja un área de 0.1 a la izquierda. Ese valor crítico es **$-1.383$**.

Igualamos y despejamos nuestra barrera:

$$\frac{k_T - 400}{5.749} = -1.383$$

$$k_T = 400 - 1.383 \cdot 5.749$$

$$k_T = 400 - 7.95$$

$$k_T = \mathbf{392.05}$$

**Regla de decisión:** Rechazar $H_0$ (confirmar que es más rápido) si la sumatoria de los 10 viajes da menor a 392.05 minutos.

### Paso 5: Conclusión

Miramos nuestro dato empírico del Paso 1: la sumatoria real dio **$400.7$ minutos**.

Como $400.7$ no cae en nuestra zona de rechazo (no es menor a $392.05$), la decisión es **No rechazar $H_0$**.

**Respuesta al enunciado:**

No, con un nivel de significación de 0.1 **no se puede asegurar** que el camino sugerido por Juan sea más rápido. De hecho, si mirás la sumatoria real, en esos 10 viajes Aparicio terminó sumando más minutos (400.7) que lo que hubiese esperado sumar por su camino tradicional (400). ¡La recomendación de Juan no fue estadísticamente buena!



## como sacar mi *S*
Como no conocemos el desvío poblacional de todos los viajes posibles de Aparicio, tenemos que "estimarlo" usando únicamente los 10 viajes que tenemos anotados. Eso se llama **Desvío Estándar Muestral ($S$)**.

La fórmula del desvío muestral es:

$$S = \sqrt{ \frac{\sum (x_i - \bar{x})^2}{n - 1} }$$

El detalle más importante acá es que **se divide por $n - 1$** (en este caso por 9) y no por $n$ (10). En estadística esto se hace para corregir un pequeño sesgo al estimar parámetros a partir de muestras chicas.

Veamos el paso a paso de la cuenta con los datos del ejercicio:

### Paso 1: El Promedio ($\bar{x}$)

Ya lo habíamos calculado dividiendo la suma total por 10:

$$\bar{x} = \frac{400.7}{10} = \mathbf{40.07}$$

### Paso 2: Las diferencias al cuadrado

A cada uno de los 10 tiempos le restás el promedio y elevás ese resultado al cuadrado. Esto mide qué tan "lejos" estuvo cada viaje del promedio.

- Viaje 1: $(41.1 - 40.07)^2 = (1.03)^2 = 1.0609$
    
- Viaje 2: $(42.2 - 40.07)^2 = (2.13)^2 = 4.5369$
    
- Viaje 3: $(40.5 - 40.07)^2 = (0.43)^2 = 0.1849$
    
- Viaje 4: $(39.9 - 40.07)^2 = (-0.17)^2 = 0.0289$
    
- Viaje 5: $(40.3 - 40.07)^2 = (0.23)^2 = 0.0529$
    
- Viaje 6: $(36.6 - 40.07)^2 = (-3.47)^2 = 12.0409$ _(Acá se apuró bastante)_
    
- Viaje 7: $(39.3 - 40.07)^2 = (-0.77)^2 = 0.5929$
    
- Viaje 8: $(42.5 - 40.07)^2 = (2.43)^2 = 5.9049$
    
- Viaje 9: $(37.8 - 40.07)^2 = (-2.27)^2 = 5.1529$
    
- Viaje 10: $(40.5 - 40.07)^2 = (0.43)^2 = 0.1849$
    

Ahora, sumamos todos esos resultados:

$$1.0609 + 4.5369 + ... + 0.1849 = \mathbf{29.741}$$

### Paso 3: Dividir por $n - 1$ (Varianza Muestral)

Agarramos la suma total de las diferencias y la dividimos por $10 - 1 = 9$:

$$S^2 = \frac{29.741}{9} \approx \mathbf{3.3045}$$

### Paso 4: La raíz cuadrada (Desvío Estándar)

Le aplicamos la raíz cuadrada a la varianza para que vuelva a estar en la misma unidad de medida (minutos):

$$S = \sqrt{3.3045} \approx \mathbf{1.8178}$$

¡Ahí lo tenés! Redondeando a tres decimales, llegamos al **$1.818$**.

**Un consejo práctico:** En los parciales nadie te pide que hagas las 10 restas y potencias a mano. Si tu calculadora científica tiene un "Modo Estadístico" (suele llamarse `STAT` o `SD`), podés cargarle la lista de los 10 números y tocando un botón (suele ser `sx` o `xσn-1`) te devuelve directamente este $1.818$. ¡Ahorra muchísimo tiempo y evita errores de tipeo!