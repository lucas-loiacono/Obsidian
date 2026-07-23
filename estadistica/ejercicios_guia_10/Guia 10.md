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


![[Pasted image 20260722150053.png]]


En el problema anterior queríamos probar algo sobre el promedio (el **centro** de la campana). En este ejercicio de la **image_1d63bc.png**, el problema no es cuánto llena la máquina en promedio, sino qué tan "desparejo" lo hace. Nos están pidiendo hacer un **Test de Hipótesis para la Varianza (o el desvío)**.

Para esto, la Normal o la $t$ de Student ya no nos sirven, porque la varianza no tiene forma de campana simétrica. Acá hace su entrada triunfal una distribución nueva que se llama **Chi-Cuadrado ($\chi^2$)**.

¡Vamos a armarlo paso a paso! Y cuidado, que este problema trae una trampa mortal con las unidades de medida.

### Paso 1: La trampa de las unidades y la muestra

El enunciado te da la regla de la máquina en **mililitros** (25 ml), pero los datos de la muestra están en **litros** (1.029, 0.943, etc.). Si metés eso así nomás en la fórmula, explota todo.

Vamos a multiplicar todos los datos de la muestra por 1000 para pasar todo a mililitros y trabajar cómodos:

- **Muestra en ml:** 1029, 943, 1071, 986, 962, 995, 991, 1002, 1003, 978.
    

Ahora necesitamos calcular la Varianza Muestral ($S^2$) de estos 10 números, igual que en el ejercicio de Aparicio (restando el promedio a cada uno, elevando al cuadrado y dividiendo por $n-1$).

- **Promedio ($\bar{x}$):** 996 ml.
    
- **Varianza Muestral ($S^2$):** Habiendo hecho la cuenta de las diferencias al cuadrado divididas por 9, nos da **$1246$**.
    

### Paso 2: Plantear las hipótesis

La máquina es eficaz si el desvío es menor o igual a 25. La pregunta nos pide comprobar _"que la máquina no es eficaz"_. Eso es lo que queremos demostrar, así que va a la alternativa ($H_1$).

Como la estadística para la dispersión trabaja con la varianza ($\sigma^2$), elevamos el desvío límite al cuadrado ($25^2 = 625$):

- $H_0: \sigma^2 = 625$ (Asumimos el límite aceptable).
    
- $H_1: \sigma^2 > 625$ (La máquina llena de forma muy despareja, no es eficaz).
    

### Paso 3: Armar la zona de rechazo (Chi-Cuadrado)

Queremos garantizar el resultado con un nivel de significación de 0.05. Al igual que antes, vamos a plantear nuestro condicional, pero usando el estadístico de Chi-Cuadrado ($\chi^2$):

$$P(\text{Rechazar } H_0 \mid H_0 \text{ es verdadera}) = 0.05$$

$$P(\chi^2_{obs} > k \mid \sigma^2 = 625) = 0.05$$

La tabla de la distribución $\chi^2$, al igual que la de Student, usa grados de libertad ($n - 1 = 9$).

Si buscás en tu tabla de $\chi^2$ con 9 grados de libertad el valor que deja un área de 0.05 a su derecha, vas a encontrar el valor crítico:

**$k = 16.919$**

**Regla de decisión:** Rechazar $H_0$ si nuestro estadístico observado resulta mayor a 16.919.

### Paso 4: Calcular el estadístico observado

Acá es donde aplicamos la fórmula mágica del Chi-Cuadrado para varianzas, que relaciona lo que vimos en la muestra ($S^2$) con lo que dictaba nuestra hipótesis teórica ($\sigma^2$):

$$\chi^2_{obs} = \frac{(n - 1) \cdot S^2}{\sigma^2_{H_0}}$$

Reemplazamos con nuestros datos (acordate que $n-1 = 9$):

$$\chi^2_{obs} = \frac{9 \cdot 1246}{625}$$

$$\chi^2_{obs} = \frac{11214}{625}$$

$$\chi^2_{obs} = 17.9424$$

### Paso 5: Conclusión

Miramos nuestra regla del Paso 3: teníamos que rechazar si superaba el límite de 16.919.

Como **$17.9424 > 16.919$**, caímos en la zona de rechazo.

**Respuesta al enunciado:**

Sí, se rechaza $H_0$. Con un nivel de significación de 0.05, **se puede asegurar que la máquina no es eficaz**.

Los sifones están saliendo demasiado desparejos (tuvimos un desvío muestral de casi 35 ml, lo cual fue suficiente evidencia estadística para probar que la máquina no está cumpliendo el estándar de 25 ml).









# CHI vs Student

El secreto no está en qué datos "conocés", sino en **cuál es el parámetro protagonista de la pregunta del problema**.

Acá te dejo el resumen definitivo para saber qué distribución usar sin fallar nunca:

### 1. Test con "t de Student" (Tu deducción fue perfecta)

- **¿Cuál es la pregunta del problema?:** Querés evaluar el **promedio / media ($\mu$)** (Ej: "¿El camino es más rápido en promedio?").
    
- **¿Qué pasa con los datos?:** **NO conocés la varianza de la población ($\sigma^2$)**. Como no tenés ese dato, estás obligado a calcular el desvío de tu pequeña muestra ($S$).
    
- **Resumen:** Test sobre la media ($\mu$) con desvío poblacional ($\sigma$) desconocido.
    

### 2. Test con "Chi-Cuadrado ($\chi^2$)" (Acá corregimos la brújula)

- **¿Cuál es la pregunta del problema?:** No te importa el promedio. Querés evaluar la **varianza / desvío ($\sigma^2$ o $\sigma$)**. El protagonista del test es la dispersión (Ej: "¿La máquina es despareja para llenar los sifones?", "¿Las piezas tienen mucha variabilidad?").
    
- **¿Qué pasa con los datos?:** Tu hipótesis ($H_0$ y $H_1$) se plantea con $\sigma^2$ en lugar de $\mu$.
    
- **Resumen:** Test específico para evaluar la varianza ($\sigma^2$).
    

### Y para completar el cuadro...

### 3. Test con "Normal ($Z$)" (Los primeros que hicimos)

- **¿Cuál es la pregunta del problema?:** Querés evaluar el **promedio / media ($\mu$)** (Ej: "¿El rinde de la soja supera las 6.2 toneladas?").
    
- **¿Qué pasa con los datos?:** El enunciado **SÍ te regala la varianza de la población ($\sigma^2$)** ("se sabe que por historia el desvío es de 0.45").
    
- **Resumen:** Test sobre la media ($\mu$) con desvío poblacional ($\sigma$) conocido.
    

### El tip de oro:

Cuando leas el enunciado, tu primera pregunta mental tiene que ser: **_"¿Me están preguntando por el promedio de las cosas, o por qué tan desparejas son?"_**.

- Si es por lo desparejas (dispersión), vas ciego a **Chi-Cuadrado**.
    
- Si es por el promedio, te fijás si el enunciado te regaló el desvío de la población o si lo tenés que calcular vos a mano con la muestra. Si te lo regaló, usás **Normal**. Si te la tenés que arreglar vos con los datos sueltos, usás **Student**.





La $S$ (el desvío de tu muestra) y la $S^2$ (la varianza de tu muestra) **son siempre la misma**. Es un número que sale puramente de tus datos empíricos (restando el promedio, elevando al cuadrado y dividiendo por $n-1$). Tu muestra no sabe qué test vas a hacer después; la muestra es la muestra.

Lo que cambia es **dónde enchufás esa $S$** dependiendo de qué te esté preguntando el enunciado.

A esas "funciones" que me preguntás, en estadística las llamamos **Estadísticos de Prueba**. Son las fórmulas que transforman tus datos sueltos en un número que podés ir a buscar a las tablas. Acá tenés las dos fórmulas definitivas:

### 1. La Función para la $t$ de Student

Usás esta fórmula cuando tu test trata sobre descubrir si el **promedio** ($\mu$) cambió, pero no conocés el desvío original de la población.

Si trabajás con el **promedio de la muestra** ($\bar{X}$):

$$t_{obs} = \frac{\bar{X} - \mu_{H_0}}{S / \sqrt{n}}$$

Si trabajás con la **sumatoria total** ($T$) como veníamos haciendo:

$$t_{obs} = \frac{T_{obs} - n \cdot \mu_{H_0}}{\sqrt{n} \cdot S}$$

- **¿Qué hace la fórmula?:** Mide qué tan lejos quedó tu promedio real ($\bar{X}$) del promedio que asumías en tu hipótesis ($\mu_{H_0}$). Como no tenés el desvío perfecto ($\sigma$), usa tu $S$ como "parche" temporal para armar el error estándar.
    

### 2. La Función para Chi-Cuadrado ($\chi^2$)

Usás esta fórmula cuando tu test no trata sobre el promedio, sino puramente sobre la **varianza / dispersión** ($\sigma^2$). Querés saber si las cosas están saliendo muy desparejas o muy iguales.

La fórmula es única (acá no se usa la sumatoria total $T$):

$$\chi^2_{obs} = \frac{(n - 1) \cdot S^2}{\sigma^2_{H_0}}$$

- **¿Qué hace la fórmula?:** Compara directamente la variabilidad de tu muestra real ($S^2$) contra la variabilidad teórica que te exige el problema en la hipótesis ($\sigma^2_{H_0}$). Si tu muestra es mucho más despareja que lo permitido, la división da un número gigante y rechazás la hipótesis.


![[Pasted image 20260722175410.png]]




Fijate que el inciso (a) te pide evaluar a la media ($\mu$), y el inciso (b) te pide evaluar el desvío ($\sigma$). ¡Es el combo completo!

Antes de arrancar, tenemos que superar el primer obstáculo: **no nos dieron los 75 datos sueltos, ni nos dieron el desvío muestral ($S$) ya calculado**. En su lugar, nos dieron dos sumatorias extrañas: $\sum w_i = 74.4$ y $\sum w_i^2 = 73.81$.

Para sacar la Varianza Muestral ($S^2$) a partir de esos datos, existe una "fórmula salvavidas" (o fórmula de trabajo) que los profesores adoran poner en los parciales:

$$S^2 = \frac{ \sum w_i^2 - \frac{(\sum w_i)^2}{n} }{n - 1}$$

Reemplazando con nuestros datos ($n = 75$):

$$S^2 = \frac{ 73.81 - \frac{(74.4)^2}{75} }{74}$$

$$S^2 = \frac{ 73.81 - 73.8048 }{74}$$

$$S^2 = \frac{ 0.0052 }{74}$$

$$S^2 \approx 0.00007027$$

_(Esta es la varianza muestral)_

$$S \approx 0.00838$$

_(Este es el desvío muestral, aplicando la raíz cuadrada)_

¡Con estos números en la mano, ya podemos destrozar los dos incisos!

### Inciso (a): Test para la media ($\mu$)

- **La pregunta:** ¿Es el promedio menor a 1 kg? ($H_0: \mu = 1$ contra $H_1: \mu < 1$).
    
- **¿Qué usamos?:** Como evaluamos el promedio ($\mu$) y no conocemos el desvío de la población entera, **usamos $t$ de Student**.
    

Como te gusta usar la **sumatoria total**, vamos a hacerlo así (nuestra suma real observada la da el enunciado: $T_{obs} = 74.4$).

Planteamos el estadístico para la sumatoria:

$$t_{obs} = \frac{T_{obs} - n \cdot \mu_0}{\sqrt{n} \cdot S}$$

$$t_{obs} = \frac{74.4 - (75 \cdot 1)}{\sqrt{75} \cdot 0.00838}$$

$$t_{obs} = \frac{74.4 - 75}{8.66 \cdot 0.00838}$$

$$t_{obs} = \frac{-0.6}{0.07257}$$

$$t_{obs} \approx -8.26$$

**Conclusión del (a):**

El enunciado no te dio un nivel de significación ($\alpha$), pero no hace falta. Un valor de $t = -8.26$ está tan absurdamente a la izquierda en la campana que el p-valor es prácticamente cero.

**Se rechaza $H_0$**. Hay evidencia abrumadora de que la media real es menor a 1 kilo (¡la marca Spiky Milk le está poniendo menos leche a las cajas!).

### Inciso (b): Test para el desvío ($\sigma$)

- **La pregunta:** ¿El desvío es menor a 0.14? ($H_0: \sigma = 0.14$ contra $H_1: \sigma < 0.14$).
    
- **¿Qué usamos?:** Como evaluamos la dispersión ($\sigma$), vamos ciegos a **Chi-Cuadrado ($\chi^2$)**.
    

Acá recordamos que el Chi-Cuadrado trabaja siempre con la varianza (al cuadrado). Así que nuestra hipótesis nula asume que $\sigma^2 = 0.14^2 = 0.0196$.

Planteamos el estadístico de Chi-Cuadrado:

$$\chi^2_{obs} = \frac{(n - 1) \cdot S^2}{\sigma^2_{H_0}}$$

Recordá que $(n-1) \cdot S^2$ es justamente el numerador de la fórmula salvavidas que calculamos al principio (que nos dio $0.0052$):

$$\chi^2_{obs} = \frac{0.0052}{0.0196}$$

$$\chi^2_{obs} \approx 0.2653$$

**Conclusión del (b):**

Si buscás en una tabla Chi-Cuadrado con 74 grados de libertad ($n-1$), lo "normal" es que el resultado dé cerca de 74. Un resultado de $0.2653$ significa que la varianza de la muestra fue ridículamente más chica que lo que proponía $H_0$. El p-valor vuelve a ser prácticamente cero.

**Se rechaza $H_0$**. Hay evidencia suficiente para asegurar que el desvío estándar de las cajas es muchísimo menor a 0.14.





# Graficos de las variables


Para entender por qué rechazamos tan rápido en el último ejercicio, hay que imaginarse cómo es la "geografía" de cada una de estas distribuciones. Cada distribución tiene un "centro" (lo que es esperable que pase si $H_0$ es verdad) y "colas" (los valores raros).

Vamos a ver cómo funciona el mapa de cada una:

### 1. El mapa de la $t$ de Student (El ejercicio de la media)

La distribución $t$ de Student tiene exactamente la misma forma que la campana de Gauss (la Normal): es perfectamente simétrica.

- **El Centro:** Su centro exacto es **0**. Si tu muestra empírica diera exactamente el mismo promedio que asume tu hipótesis nula ($H_0$), la fórmula te daría $t_{obs} = 0$.
    
- **Lo "Normal":** Casi todo lo que pasa por simple casualidad cae entre los valores **-2 y 2**. Si te da 1.5 o -1.8, estás dentro del ruido estadístico aceptable.
    
- **Las Fronteras:** Las tablas de los libros de estadística suelen terminar en el número **3** o **4**. Un valor de 3 significa que ya estás en el 0.1% de los casos más raros del universo.
    
- **¿Qué pasó en nuestro ejercicio?** Nos dio **-8.26**. ¡Ese número rompió la escala! Imaginate que estás tirando dardos al centro de un tablero (el 0), y de repente un dardo cae a 8 cuadras de distancia. Ya no es casualidad; es evidente que estás apuntando a otro lado (es decir, la media real es otra). Por eso rechazamos directamente sin siquiera mirar la tabla.
    

### 2. El mapa del Chi-Cuadrado $\chi^2$ (El ejercicio del desvío)

Acá la intuición cambia por completo, porque la distribución Chi-Cuadrado **no es simétrica y no tiene números negativos** (porque estamos hablando de varianzas, que son desvíos elevados al cuadrado, y todo número al cuadrado es positivo).

- **El Inicio:** Arranca en **0** como una pared de ladrillos y se extiende hacia la derecha infinitamente.
    
- **El Centro (La clave de todo):** A diferencia de la Student que siempre se centra en 0, la "montaña" de la Chi-Cuadrado se va moviendo dependiendo de la cantidad de datos que tengas. **Su centro esperado es aproximadamente igual a sus grados de libertad ($n - 1$).**
    
- **¿Qué pasó en nuestro ejercicio?** Teníamos 75 cajas de leche, por lo tanto nuestros grados de libertad eran **74**. Si la hipótesis de Spiky Milk ($H_0$) hubiera sido cierta, nuestro resultado tendría que haber caído cerquita de la cima de la montaña, es decir, ¡cerca del 74!
    
- **El resultado absurdo:** A nosotros la fórmula nos dio **0.26**. Esperábamos un 74 y nos dio un número microscópico casi pegado al cero. Es como si esperaras que un árbol mida 74 metros y de repente mide 26 centímetros. Esa diferencia abismal te grita que la variabilidad de tu muestra es ridículamente más baja que lo que proponía la hipótesis, y por eso se rechaza de inmediato.
    

### En resumen:

Las tablas que usás (Normal, Student, Chi-Cuadrado) son simplemente mapas geográficos que cubren el "área normal" donde suceden las cosas por casualidad.

Cuando tu fórmula arroja un número que se cae de los bordes de la página de ese mapa (un -8 en Student, o un 0.26 cuando esperabas un 74 en Chi-Cuadrado), significa que la probabilidad de que $H_0$ sea cierta es prácticamente cero. ¡La matemática te está avisando a gritos que tu hipótesis original estaba equivocada!




![[Pasted image 20260722232129.png]]


Aquí tienes la resolución paso a paso del ejercicio presentado en la imagen "image_a7fd39.png".

### 1. Planteo de Hipótesis

Definimos nuestras hipótesis nula ($H_0$) y alternativa ($H_1$) respecto a la intensidad (tasa) de la distribución exponencial $\lambda$:

- **Hipótesis nula ($H_0$):** $\lambda \leqslant 0.0005$
    
- **Hipótesis alternativa ($H_1$):** $\lambda > 0.0005$
    

### 2. Datos y Estadístico de Prueba

Contamos con una muestra de **6** observaciones ($n = 6$).

Primero, calculamos la suma total de las duraciones observadas:

$$S = \sum_{i=1}^{n} X_i = 61 + 1905 + 1076 + 623 + 33 + 167 = 3865$$

Sabemos que si $X_i \sim \text{Exp}(\lambda)$, entonces la variable transformada $T = 2\lambda \sum X_i$ sigue una distribución Chi-cuadrado con $2n$ grados de libertad ($\chi^2_{2n}$).

- **Grados de libertad:** $2n = 2 \cdot 6 = 12$
    

Calculamos el estadístico de prueba observado asumiendo el valor límite de la hipótesis nula ($\lambda_0 = 0.0005$):

$$T_{obs} = 2 \cdot 0.0005 \cdot 3865$$

$$T_{obs} = 3.865$$

### 3. Regla de Decisión y Conclusión

Como la hipótesis alternativa plantea que $\lambda > 0.0005$ (lo que implica un menor tiempo de duración esperado, ya que la media es $1/\lambda$), la región de rechazo se encuentra en la **cola inferior** de la distribución Chi-cuadrado.

Rechazaremos $H_0$ si nuestro estadístico es menor al valor crítico de la tabla Chi-cuadrado para un nivel de significación $\alpha = 0.05$ y **12** grados de libertad.

- **Valor crítico:** $\chi^2_{0.05; 12} = 5.226$
    

**Conclusión:**

Como el estadístico observado ($3.865$) es menor que el valor crítico ($5.226$), el valor cae dentro de la región de rechazo. Por lo tanto, **sí, los datos permiten refutar la hipótesis nula** con un nivel de significación del **5%**. Existe evidencia estadística para afirmar que $\lambda > 0.0005$.

### 4. Cálculo del _p-valor_

El _p-valor_ es la probabilidad de obtener un estadístico tan o más extremo (más pequeño, en este caso) que el observado, asumiendo que la hipótesis nula es cierta.

$$p\text{-valor} = P(\chi^2_{12} < 3.865)$$

Calculando la función de distribución acumulada para la Chi-cuadrado con **12** grados de libertad en el punto **3.865**:

$$p\text{-valor} \approx 0.0142$$

Como el _p-valor_ (**0.0142**) es menor que el nivel de significación $\alpha$ (**0.05**), esto confirma nuestra decisión de rechazar la hipótesis nula.


### 1. El multiplicador siempre será $2\lambda$

El **$2$** es una constante matemática inamovible en este procedimiento. Su única función es actuar como un "factor de ajuste" para transformar el parámetro de la distribución original y forzarlo a que valga $1/2$ (que es el requisito obligatorio para que se convierta en una tabla Chi-cuadrado).

**Una pequeña advertencia de notación:**

Esto se cumple siempre y cuando estés trabajando con la intensidad o tasa **$\lambda$**. Algunos libros de estadística plantean el ejercicio usando la media de vida útil, usualmente llamada **$\mu$** o **$\theta$**.

Como la media es la inversa de la intensidad ($\mu = \frac{1}{\lambda}$), si el ejercicio te da la media, la fórmula equivalente sería:

$$\chi^2_{obs} = \frac{2}{\mu} \sum_{i=1}^{n} X_i$$

Como ves, el **2** sigue estando ahí multiplicando a la sumatoria, solo cambia cómo expresas el parámetro.

### 2. Los grados de libertad $\nu$ siempre serán $2n$

Los grados de libertad (que a veces se escriben como $\nu$ o $gl$) **siempre serán exactamente el doble del tamaño de tu muestra**.

- Si tu muestra es de $n = 6$ lámparas, entras a la tabla con $12$.
    
- Si tu muestra fuera de $n = 50$ lámparas, entrarías a la tabla con $100$.
    

Esto es una regla universal para la suma de variables exponenciales transformadas a Chi-cuadrado, porque cada observación $X_i$ individual aporta el equivalente a "2" grados de libertad a esa distribución final.







# La Relación entre Sumatoria y Promedio

Sabemos que el promedio muestral se calcula dividiendo la sumatoria de todos los valores por la cantidad de datos ($n$):

$$\bar{X} = \frac{\sum_{i=1}^{n} X_i}{n}$$

Si de ahí despejamos la sumatoria, nos queda:

$$\sum_{i=1}^{n} X_i = n \cdot \bar{X}$$

### La Fórmula Adaptada

Si tomamos nuestra fórmula original del estadístico de prueba y reemplazamos la sumatoria por su equivalente ($n \cdot \bar{X}$), obtenemos la versión para el promedio:

$$\chi^2_{obs} = 2\lambda_0 (n \cdot \bar{X})$$

Que, reordenando los factores, suele escribirse así:

$$\chi^2_{obs} = 2n\lambda_0 \bar{X}$$

### Conclusión Práctica

- **El resultado final:** El valor numérico de $\chi^2_{obs}$ te va a dar exactamente igual uses la fórmula que uses. Es solo un camino distinto para llegar al mismo número.
    
- **Los grados de libertad:** Tampoco cambian en absoluto. Entras a la tabla de Chi-cuadrado con **$2n$** grados de libertad, igual que antes.
    
- **¿Cuál conviene usar?** Depende exclusivamente de cómo te presenten el enunciado:
    
    - Si te dan la lista cruda de números (como en la imagen), usas la **sumatoria** porque es más rápido sumar y listo.
        
    - Si el enunciado te dice algo como _"se analizó una muestra de 6 lámparas y su duración promedio fue de 644.16 horas"_, usas la fórmula del **promedio** ($\bar{X}$) directamente.






![[Pasted image 20260723005523.png]]


Aquí tienes la resolución paso a paso del ejercicio presentado en el archivo "image_c1ed46.png".

A diferencia del ejercicio anterior, aquí no tenemos los tiempos exactos de duración, sino datos "censurados" (sabemos que superaron un umbral, pero no por cuánto). Por lo tanto, lo abordaremos a través de la probabilidad del evento observado.

### 1. Planteo de Hipótesis

Queremos poner a prueba la duración media ($\mu$). Sabemos que en una distribución exponencial, la intensidad es la inversa de la media ($\lambda = 1/\mu$).

- **Hipótesis nula ($H_0$):** $\mu \leqslant 55$ horas (lo que implica que $\lambda \geqslant 1/55$)
    
- **Hipótesis alternativa ($H_1$):** $\mu > 55$ horas (lo que implica que $\lambda < 1/55$)
    

### 2. El Evento Observado bajo $H_0$

El experimento consistió en probar 10 lámparas y el evento observado fue que **las 10 superaron las 50 horas**.

Primero, calculamos la probabilidad de que **una sola** lámpara dure más de 50 horas. Esto nos lo da la función de supervivencia de la distribución exponencial:

$$P(X > x) = e^{-\lambda x}$$

$$P(X > 50) = e^{-50\lambda}$$

Para hacer el contraste de hipótesis, evaluamos esta probabilidad en el "peor de los casos" de la hipótesis nula, es decir, el valor límite $\mu = 55$ (o $\lambda = 1/55$):

$$P(X > 50 \mid H_0) = e^{-50 \cdot (1/55)} = e^{-50/55} = e^{-10/11}$$

Como las 10 lámparas son variables independientes, la probabilidad conjunta de que **todas** duren más de 50 horas bajo la hipótesis nula se calcula multiplicando esa probabilidad 10 veces (o elevándola a la 10):

$$P(\text{10 lámparas } > 50 \mid H_0) = \left(e^{-10/11}\right)^{10} = e^{-100/11}$$

### 3. Cálculo del _p-valor_

El _p-valor_ es la probabilidad de observar un resultado tan o más extremo a favor de $H_1$, asumiendo que $H_0$ es cierta. En este diseño, el evento observado (las 10 lámparas aguantando más de 50 horas) concentra toda la probabilidad de la región de rechazo para nuestros datos censurados.

Calculamos el valor numérico:

$$p\text{-valor} = e^{-100/11} \approx 0.0001128$$

### 4. Regla de Decisión y Conclusión

El enunciado nos da un nivel de significación de **$\alpha = 0.05$**.

Comparamos nuestro _p-valor_ con $\alpha$:

$$0.0001128 < 0.05$$

**Conclusión:**

Como el _p-valor_ es estrictamente menor al nivel de significación, **rechazamos la hipótesis nula**. Por lo tanto, con un nivel de significación del 5%, **sí se puede afirmar** que la duración media de cada lámpara del lote es mayor que 55 horas, ya que sería extremadamente improbable ($0.011\%$) obtener una muestra de 10 lámparas que duren tanto si la media real fuera de 55 horas o menos.





![[Pasted image 20260723005758.png]]


Aquí tienes la resolución paso a paso para diseñar el test de hipótesis planteado en la imagen "image_c3b73d.png".

### 1. Elección del Estadístico de Prueba

Para una muestra aleatoria $X_1, X_2, \dots, X_n$ proveniente de una distribución uniforme $U(0, \theta)$, el mejor estimador (y estadístico suficiente) para el parámetro $\theta$ es el máximo de la muestra, conocido como el mayor estadístico de orden:

$$Y = X_{(n)} = \max(X_1, X_2, \dots, X_n)$$

La función de distribución acumulada de $Y$ es:

$$F_Y(y) = P(Y \leqslant y) = \left( \frac{y}{\theta} \right)^n \quad \text{para } 0 \leqslant y \leqslant \theta$$

### 2. Definición de la Región de Rechazo

Nuestras hipótesis son:

- **$H_0$:** $\theta \leqslant 1$
    
- **$H_1$:** $\theta > 1$
    

Como la hipótesis alternativa plantea valores de $\theta$ mayores a 1, esperaremos observar valores grandes en nuestra muestra. Por lo tanto, rechazaremos $H_0$ si nuestro estadístico máximo supera un cierto valor crítico $c$:

$$\text{Región de Rechazo (RR)} = \{ Y > c \}$$

### 3. Uso del Nivel de Significación ($\alpha$)

El nivel de significación es la máxima probabilidad de cometer un error de Tipo I (rechazar $H_0$ siendo cierta). Este máximo se alcanza en el límite de $H_0$, es decir, asumiendo $\theta = 1$.

$$\alpha = P(Y > c \mid \theta = 1) = 0.05$$

Expresamos esta probabilidad usando la función de distribución:

$$P(Y > c \mid \theta = 1) = 1 - P(Y \leqslant c \mid \theta = 1) = 1 - \left( \frac{c}{1} \right)^n = 1 - c^n$$

Igualamos a $0.05$ y obtenemos nuestra primera ecuación clave:

$$1 - c^n = 0.05 \implies c^n = 0.95$$

### 4. Uso de la Función de Potencia

El enunciado exige que la potencia del test evaluada en $\theta = 1.1$ sea igual a $0.9$. La potencia es la probabilidad de rechazar $H_0$ cuando $H_1$ es cierta:

$$\pi(1.1) = P(Y > c \mid \theta = 1.1) = 0.9$$

Aplicamos nuevamente la función de distribución, pero ahora con $\theta = 1.1$:

$$1 - P(Y \leqslant c \mid \theta = 1.1) = 1 - \left( \frac{c}{1.1} \right)^n = 0.9$$

Sabiendo por el paso anterior que $c^n = 0.95$, sustituimos ese valor en la ecuación:

$$1 - \frac{0.95}{1.1^n} = 0.9$$

### 5. Cálculo del Tamaño de Muestra ($n$) y Valor Crítico ($c$)

Despejamos $1.1^n$:

$$1 - 0.9 = \frac{0.95}{1.1^n}$$

$$0.1 = \frac{0.95}{1.1^n} \implies 1.1^n = \frac{0.95}{0.1}$$

$$1.1^n = 9.5$$

Aplicamos logaritmo natural para despejar $n$:

$$n \ln(1.1) = \ln(9.5)$$

$$n = \frac{\ln(9.5)}{\ln(1.1)} \approx \frac{2.25129}{0.09531} \approx 23.62$$

Dado que el tamaño de muestra $n$ debe ser un número entero, **redondeamos hacia arriba** a $n = 24$ para garantizar que la potencia cumpla con ser _al menos_ $0.9$.

Ahora, calculamos el valor crítico $c$ usando $n = 24$:

$$c^{24} = 0.95$$

$$c = \sqrt[24]{0.95} \approx 0.99787$$

### Diseño Final del Test

Para cumplir con las condiciones solicitadas en el problema, el test de hipótesis debe diseñarse de la siguiente manera:

1. Tomar una muestra aleatoria de tamaño **$n = 24$**.
    
2. Buscar el valor máximo de esa muestra, $X_{(24)}$.
    
3. **Rechazar $H_0$** si el valor máximo observado es mayor a **$0.99787$**.








![[Pasted image 20260723012442.png]]




Aquí tienes la resolución del ejercicio presentado en la imagen "image_c4985d.png".

Este es un problema muy interesante porque se puede resolver tanto desde la formalidad del test de hipótesis como desde la lógica pura del dominio de la variable.

### 1. Parámetros e Hipótesis

Primero, definimos la distribución y relacionamos el parámetro $\theta$ con la media poblacional ($\mu$), que es sobre lo que recae la pregunta.

- **Variable aleatoria:** $X \sim U(15, 15 + \theta)$
    
- **Media de una Uniforme:** $\mu = E(X) = \frac{\text{límite inferior} + \text{límite superior}}{2}$
    
    $$\mu = \frac{15 + (15 + \theta)}{2} = 15 + \frac{\theta}{2}$$
    

El enunciado pregunta si _se puede afirmar_ que la longitud media es menor que 20 metros. Lo que queremos probar siempre va en la hipótesis alternativa ($H_1$).

Planteamos las hipótesis en función de $\mu$ y luego las traducimos a $\theta$:

- **Hipótesis alternativa ($H_1$):** $\mu < 20$
    
    $$15 + \frac{\theta}{2} < 20 \implies \frac{\theta}{2} < 5 \implies \theta < 10$$
    
- **Hipótesis nula ($H_0$):** $\mu \geqslant 20$
    
    $$\theta \geqslant 10$$
    

### 2. Análisis Directo por Dominio (La forma rápida)

Antes de hacer cuentas complejas, miremos los datos muestrales: la muestra de $n = 4$ arrojó un valor máximo observado de **25 metros** ($X_{(4)} = 25$).

Por definición de la distribución uniforme $U(15, 15 + \theta)$, **ningún** valor de la variable puede superar el límite superior. Es decir, para cualquier observación $x$, se debe cumplir:

$$x \leqslant 15 + \theta$$

Si observamos un rollo de 25 metros, entonces es físicamente imposible que el límite superior sea menor a 25:

$$25 \leqslant 15 + \theta \implies 10 \leqslant \theta$$

Como la muestra nos demuestra irrefutablemente que **$\theta \geqslant 10$**, la hipótesis alternativa ($H_1: \theta < 10$) queda descartada de inmediato. La probabilidad de que $\theta < 10$ dado un dato de 25 metros es cero.

### 3. Resolución Formal del Test de Hipótesis

Para demostrarlo con el procedimiento estadístico formal requerido:

Como queremos probar que $\theta < 10$, esperaremos valores pequeños en nuestra muestra para rechazar $H_0$. Por ende, la región de rechazo (RR) estará en la cola inferior del estadístico máximo $X_{(n)}$:

$$\text{RR} = \{ X_{(4)} < c \}$$

Calculamos el valor crítico $c$ usando el nivel de significación $\alpha = 0.01$ y evaluando en el peor caso de $H_0$ ($\theta = 10$). Si $\theta = 10$, la distribución es $U(15, 25)$.

$$\alpha = P(X_{(4)} < c \mid \theta = 10) = 0.01$$

Utilizamos la función de distribución acumulada para el máximo estadístico de orden en una uniforme $[A, B]$, que es $F(x) = \left(\frac{x - A}{B - A}\right)^n$:

$$\left( \frac{c - 15}{25 - 15} \right)^4 = 0.01$$

$$\left( \frac{c - 15}{10} \right)^4 = 0.01$$

Despejamos $c$:

$$\frac{c - 15}{10} = \sqrt[4]{0.01} \approx 0.3162$$

$$c - 15 = 3.162 \implies c = 18.162$$

**Región de Rechazo:** $\{ X_{(4)} < 18.162 \}$

Nuestro estadístico observado fue **25**. Como $25 \nless 18.162$, no cae en la región de rechazo.

### Conclusión

**No**, no se puede afirmar que la longitud media de los rollos del lote sea menor a 20 metros. De hecho, la evidencia de haber encontrado un rollo de 25 metros hace que sea teóricamente imposible que la media poblacional sea menor a 20 bajo este modelo uniforme.





## Por que no uso a $\mu$

Es una excelente pregunta conceptual. La razón principal es que **$\theta$ es el parámetro que define la estructura matemática de la distribución**, mientras que **$\mu$ (la media) es solo una consecuencia** de ese parámetro.

Aquí te detallo por qué es necesario hacer ese cambio:

### 1. Las fórmulas necesitan los límites

Todas las fórmulas de probabilidad que usamos para este ejercicio (como la función de distribución acumulada del máximo que vimos recién) funcionan usando los extremos de la distribución Uniforme: el límite inferior ($A$) y el límite superior ($B$).

En el modelo que plantea este problema:

- $A = 15$
    
- $B = 15 + \theta$
    

La media ($\mu$) te indica dónde está el "centro" geométrico de los datos, pero no podés enchufarla directamente en la fórmula de la función de distribución $F(x)$. Para poder hacer las cuentas probabilísticas y hallar la región de rechazo, **necesitamos obligatoriamente usar $\theta$** para saber dónde termina exactamente la curva.

### 2. La "traducción" de la hipótesis

El enunciado, para plantear el problema en términos prácticos, te pregunta sobre la media ($\mu < 20$). Pero como nosotros operamos con la estructura de la distribución, hacemos una equivalencia o "traducción matemática".

Dado que la relación entre ambas está fija por la geometría de la distribución uniforme:

$$\mu = 15 + \frac{\theta}{2}$$

Cualquier afirmación sobre $\mu$ repercute automáticamente sobre $\theta$. Decir "la media poblacional es menor a 20" ($\mu < 20$) es exactamente lo mismo que decir "el límite superior de mi distribución se extiende menos de 10 unidades desde el 15" ($\theta < 10$).

**En resumen:**

Pasamos todo a $\theta$ porque es el engranaje que hace funcionar las fórmulas de la distribución Uniforme. La $\mu$ es simplemente la forma en la que el enunciado te planteó la pregunta, pero no nos sirve operativamente para calcular el estadístico.