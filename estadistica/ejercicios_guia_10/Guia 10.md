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