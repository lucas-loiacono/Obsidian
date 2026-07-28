
![[Pasted image 20260727204810.png]]



Aquí tienes la resolución del ejercicio 11.1 de la imagen **image_77713d.png**, aplicando estrictamente el método de la **sumatoria** para construir el intervalo de confianza, tal como lo establecimos.

### 1. Definición de la Variable y la Sumatoria

Sabemos que la señal recibida es $X = \mu + N$.

Como el ruido es $N \sim \mathcal{N}(0, 1)$, al sumarle una constante $\mu$, nuestra variable aleatoria original para cada transmisión individual distribuye de forma Normal con media $\mu$ y varianza 1:

$$X_i \sim \mathcal{N}(\mu, 1)$$

Se transmitieron $n = 9$ señales. En lugar de trabajar con el promedio, definimos nuestra variable de estudio como la **sumatoria total** de las señales recibidas:

$$S = \sum_{i=1}^{9} X_i$$

Por las propiedades de la distribución Normal (la suma de normales es normal), calculamos los parámetros para esta sumatoria:

- **Media de la suma:** $n \cdot \mu = 9\mu$
    
- **Varianza de la suma:** $n \cdot \sigma^2 = 9 \cdot 1 = 9$
    
- **Desvío estándar de la suma:** $\sqrt{9} = 3$
    

Entonces, nuestra sumatoria distribuye así:

$$S \sim \mathcal{N}(9\mu, 9)$$

### 2. Construcción del Pivote

Como conocemos la varianza real ($\sigma^2 = 1$), utilizamos la distribución Normal Estándar ($Z$) para armar nuestro pivote, pero usando la sumatoria en lugar del promedio:

$$Z = \frac{S - 9\mu}{3} \sim \mathcal{N}(0, 1)$$

Para un nivel de confianza del **95%** ($1 - \alpha = 0.95$), buscamos en la tabla Normal el valor $z_{1-\alpha/2} = z_{0.975}$:

- **Valor crítico:** $1.96$
    

### 3. Despeje de la Región de Confianza

Planteamos la probabilidad con nuestro pivote y despejamos la incógnita $\mu$:

$$P\left(-1.96 \leqslant \frac{S - 9\mu}{3} \leqslant 1.96\right) = 0.95$$

Pasamos el 3 multiplicando:

$$-5.88 \leqslant S - 9\mu \leqslant 5.88$$

Restamos $S$ en todos los miembros:

$$-S - 5.88 \leqslant -9\mu \leqslant -S + 5.88$$

Multiplicamos por $-1$ (¡cuidado, esto invierte los signos de desigualdad!) y ordenamos:

$$S - 5.88 \leqslant 9\mu \leqslant S + 5.88$$

Finalmente, dividimos todo por 9 para dejar a la $\mu$ sola en el centro. Esta es nuestra fórmula final del intervalo basado en la sumatoria:

$$\frac{S - 5.88}{9} \leqslant \mu \leqslant \frac{S + 5.88}{9}$$

### 4. Cálculo Final

Ahora, sumamos los 9 valores reales que recibió el receptor:

$$S_{obs} = 8.016 + 8.488 + 7.395 + 9.011 + 7.532 + 7.841 + 8.651 + 6.917 + 8.490$$

$$S_{obs} = 72.341$$

Reemplazamos este valor observado en nuestra fórmula despejada:

- **Límite Inferior:** $\frac{72.341 - 5.88}{9} = \frac{66.461}{9} \approx 7.3846$
    
- **Límite Superior:** $\frac{72.341 + 5.88}{9} = \frac{78.221}{9} \approx 8.6912$
    

**Conclusión final:**

Con un nivel de confianza del **95%**, el intervalo para el verdadero valor de la señal transmitida $\mu$ es **$[7.3846, 8.6912]$**.



![[Pasted image 20260728010511.png]]


Aquí tienes la resolución del ejercicio 11.2, manteniendo rigurosamente el planteo desde la **sumatoria** y conectándolo con el promedio que pide el enunciado.

### 1. Definición de la Variable y la Sumatoria

Sabemos que la señal recibida individualmente es $X_i = \mu + N$.

Como el ruido es $N \sim \mathcal{N}(0, 1/100)$, nuestra variable aleatoria para cada transmisión distribuye así:

$$X_i \sim \mathcal{N}\left(\mu, \frac{1}{100}\right)$$

El emisor transmite la señal $n$ veces. Definimos nuestra **sumatoria total** de señales recibidas:

$$S = \sum_{i=1}^{n} X_i$$

Calculamos los parámetros para esta sumatoria (la suma de Normales es Normal):

- **Media ($\mu_S$):** $n \cdot \mu$
    
- **Varianza ($\sigma_S^2$):** $n \cdot \frac{1}{100} = \frac{n}{100}$
    
- **Desvío estándar ($\sigma_S$):** $\sqrt{\frac{n}{100}} = \frac{\sqrt{n}}{10}$
    

Nuestra sumatoria distribuye:

$$S \sim \mathcal{N}\left(n\mu, \frac{n}{100}\right)$$

### 2. Construcción del Pivote

Utilizamos la distribución Normal Estándar ($Z$) para tipificar nuestra sumatoria:

$$Z = \frac{S - n\mu}{\frac{\sqrt{n}}{10}} = \frac{10(S - n\mu)}{\sqrt{n}} \sim \mathcal{N}(0, 1)$$

Para un nivel de confianza del **$99\%$** ($1 - \alpha = 0.99$), buscamos en la tabla Normal el valor crítico que deja un $0.5\%$ en cada cola ($z_{0.995}$):

- **Valor crítico:** $2.575$ (o $2.58$ dependiendo de la tabla que uses; usaremos $2.575$).
    

### 3. Del Pivote al Error del Promedio

Planteamos la probabilidad con nuestro pivote:

$$P\left(-2.575 \leqslant \frac{10(S - n\mu)}{\sqrt{n}} \leqslant 2.575\right) = 0.99$$

El enunciado indica que el receptor decodifica la señal **promediando** los valores, es decir, calcula $\frac{S}{n}$. Además, exige que el "error" (la distancia entre ese promedio y el verdadero $\mu$) sea $\leqslant 0.01$.

Vamos a manipular la inecuación del pivote para hacer aparecer ese promedio ($\frac{S}{n}$) en el centro:

Pasamos multiplicando el denominador:

$$-2.575 \frac{\sqrt{n}}{10} \leqslant S - n\mu \leqslant 2.575 \frac{\sqrt{n}}{10}$$

Dividimos todos los miembros por $n$ (esto convierte a la sumatoria $S$ en el promedio decodificado $\frac{S}{n}$):

$$-2.575 \frac{\sqrt{n}}{10n} \leqslant \frac{S}{n} - \mu \leqslant 2.575 \frac{\sqrt{n}}{10n}$$

Simplificamos la expresión $\frac{\sqrt{n}}{n}$ a $\frac{1}{\sqrt{n}}$:

$$-\frac{0.2575}{\sqrt{n}} \leqslant \frac{S}{n} - \mu \leqslant \frac{0.2575}{\sqrt{n}}$$

Lo que nos quedó en los extremos es exactamente el **margen de error**.

### 4. Cálculo del Tamaño de Muestra ($n$)

El comité/enunciado exige que este error sea menor o igual a $0.01$. Por lo tanto, forzamos esa condición:

$$\frac{0.2575}{\sqrt{n}} \leqslant 0.01$$

Despejamos $n$:

$$0.2575 \leqslant 0.01 \cdot \sqrt{n}$$

$$\frac{0.2575}{0.01} \leqslant \sqrt{n}$$

$$25.75 \leqslant \sqrt{n}$$

Elevamos al cuadrado ambos lados:

$$n \geqslant (25.75)^2$$

$$n \geqslant 663.0625$$

Dado que la cantidad de transmisiones no puede ser un número decimal, siempre debemos redondear al entero superior para garantizar que se cumpla el nivel de confianza del $99\%$.

**Conclusión final:**

El mínimo valor de transmisiones necesarias es **$n = 664$**.


![[Pasted image 20260728011544.png]]


Aquí tienes la resolución del ejercicio 11.3 de la imagen **image_35885a.png**, aplicando nuevamente el método de la **sumatoria** que acordamos, con la particularidad de que ahora la varianza poblacional ($\sigma^2$) es desconocida.

### 1. Definición de la Variable y la Sumatoria

El enunciado nos indica que las mediciones individuales tienen distribución normal: $X_i \sim \mathcal{N}(\mu, \sigma^2)$, donde tanto $\mu$ como $\sigma^2$ son desconocidos.

Se realizaron $n = 12$ mediciones. Definimos nuestra **sumatoria total** de las observaciones:

$$S_x = \sum_{i=1}^{12} X_i$$

Por las propiedades de la distribución Normal, sabemos que la sumatoria distribuye de la siguiente manera:

$$S_x \sim \mathcal{N}(n\mu, n\sigma^2)$$

### 2. Construcción del Pivote (con Varianza Desconocida)

Como no conocemos el verdadero desvío estándar ($\sigma$), debemos estimarlo usando el **desvío estándar muestral ($s$)**.

Al introducir $s$ en nuestra ecuación en lugar de $\sigma$, el estadístico ya no se comporta como una Normal estándar ($Z$), sino que pasa a tener una distribución **t de Student** con $n-1$ grados de libertad.

Adaptamos la fórmula del pivote clásico a nuestra sumatoria $S_x$:

$$T = \frac{S_x - n\mu}{\sqrt{n} \cdot s} \sim t_{n-1}$$

Para un nivel de confianza del **$95\%$** ($1 - \alpha = 0.95$), buscamos en la tabla de la t de Student el valor crítico para $n-1 = 11$ grados de libertad que deja un $0.025$ en cada cola ($t_{11, 0.975}$):

- **Valor crítico:** $2.201$
    

### 3. Despeje de la Región de Confianza

Planteamos la inecuación de probabilidad con nuestro pivote y procedemos a despejar $\mu$:

$$P\left(-2.201 \leqslant \frac{S_x - n\mu}{\sqrt{n} \cdot s} \leqslant 2.201\right) = 0.95$$

Pasamos multiplicando el denominador ($\sqrt{n} \cdot s$):

$$-2.201 \cdot \sqrt{n} \cdot s \leqslant S_x - n\mu \leqslant 2.201 \cdot \sqrt{n} \cdot s$$

Restamos la sumatoria $S_x$ en todos los miembros:

$$-S_x - 2.201 \cdot \sqrt{n} \cdot s \leqslant -n\mu \leqslant -S_x + 2.201 \cdot \sqrt{n} \cdot s$$

Multiplicamos todo por $-1$ (lo que invierte los signos de desigualdad) y ordenamos:

$$S_x - 2.201 \cdot \sqrt{n} \cdot s \leqslant n\mu \leqslant S_x + 2.201 \cdot \sqrt{n} \cdot s$$

Dividimos todo por $n$ para despejar finalmente la media $\mu$:

$$\frac{S_x - 2.201 \cdot \sqrt{n} \cdot s}{n} \leqslant \mu \leqslant \frac{S_x + 2.201 \cdot \sqrt{n} \cdot s}{n}$$

### 4. Cálculos con los Datos de la Muestra

A partir de los 12 datos provistos por James Short, calculamos los valores necesarios:

- **Sumatoria observada ($S_{obs}$):** $9.11 + 8.66 + \dots + 9.25 = 103.17$
    
- **Desvío estándar muestral ($s$):** Calculando la varianza de la muestra (dividiendo por $n-1 = 11$) y aplicando raíz cuadrada, obtenemos $s \approx 0.5616$.
    
- **Tamaño de muestra ($n$):** $12$ (por lo tanto, $\sqrt{12} \approx 3.4641$)
    

Calculamos el término del margen de error de nuestra fórmula ($2.201 \cdot \sqrt{n} \cdot s$):

$$\text{Margen} = 2.201 \cdot 3.4641 \cdot 0.5616 \approx 4.2818$$

Reemplazamos en la fórmula despejada:

- **Límite Inferior:** $\frac{103.17 - 4.2818}{12} = \frac{98.8882}{12} \approx 8.2407$
    
- **Límite Superior:** $\frac{103.17 + 4.2818}{12} = \frac{107.4518}{12} \approx 8.9543$
    

**Conclusión final:**

Basado en las observaciones muestrales de James Short, el intervalo de confianza del **$95\%$** para la verdadera paralaje solar $\mu$ es **$[8.24, 8.95]$** segundos de grado.




![[Pasted image 20260728012234.png]]


Aquí tienes la resolución del ejercicio 11.4 de la imagen **image_351f7b.png**, utilizando nuestra metodología de la **sumatoria**.

Este ejercicio introduce una novedad importante: nos pide una **cota inferior** en lugar de un intervalo cerrado por ambos lados. Esto significa que todo nuestro nivel de riesgo ($\alpha$) irá a una sola cola de la distribución.

### 1. Definición de la Variable y la Sumatoria

Sabemos que el voltaje de ruptura tiene distribución Normal: $X_i \sim \mathcal{N}(\mu, \sigma^2)$, con varianza desconocida.

Se probaron $n = 10$ capacitores. Definimos nuestra **sumatoria total** de voltajes:

$$S_x = \sum_{i=1}^{10} X_i$$

La sumatoria distribuye de la siguiente manera:

$$S_x \sim \mathcal{N}(n\mu, n\sigma^2)$$

### 2. Construcción del Pivote Unilateral

Al no conocer la varianza real ($\sigma^2$), utilizamos el desvío estándar muestral ($s$) y la distribución **t de Student** con $n-1 = 9$ grados de libertad:

$$T = \frac{S_x - n\mu}{\sqrt{n} \cdot s} \sim t_9$$

El nivel de confianza exigido es del **$95\%$** ($1 - \alpha = 0.95$). Como buscamos exclusivamente una **cota inferior** para $\mu$, no dividimos el error en dos. Concentramos el $5\%$ de riesgo ($\alpha = 0.05$) en una sola cola.

Buscamos en la tabla t de Student el cuantil $t_{9, 0.95}$:

- **Valor crítico:** $1.833$
    

### 3. Despeje de la Cota Inferior

Planteamos la inecuación de probabilidad asegurándonos de que el pivote sea menor o igual al valor crítico, lo que nos permitirá despejar un límite inferior para $\mu$:

$$P\left( \frac{S_x - n\mu}{\sqrt{n} \cdot s} \leqslant 1.833 \right) = 0.95$$

Pasamos multiplicando el denominador:

$$S_x - n\mu \leqslant 1.833 \cdot \sqrt{n} \cdot s$$

Pasamos la sumatoria restando:

$$-n\mu \leqslant -S_x + 1.833 \cdot \sqrt{n} \cdot s$$

Multiplicamos todo por $-1$ (¡esto es clave porque invierte el signo de menor a mayor!) y ordenamos:

$$n\mu \geqslant S_x - 1.833 \cdot \sqrt{n} \cdot s$$

Dividimos por $n$ para despejar la media $\mu$:

$$\mu \geqslant \frac{S_x - 1.833 \cdot \sqrt{n} \cdot s}{n}$$

Lo que nos quedó a la derecha del signo mayor o igual es la fórmula exacta de nuestra cota inferior basada en la sumatoria.

### 4. Cálculos con los Datos de la Muestra

Con los 10 datos de voltajes obtenidos en la prueba, calculamos los valores observados:

- **Sumatoria observada ($S_{obs}$):** $196.73 + 204.37 + \dots + 202.27 = 2015.03$
    
- **Desvío estándar muestral ($s$):** Calculando la varianza muestral de estos 10 datos y aplicando raíz cuadrada, se obtiene $s \approx 3.3745$.
    
- **Tamaño de muestra ($n$):** $10$ (por lo tanto, $\sqrt{10} \approx 3.1623$)
    

Calculamos el margen que le restaremos a nuestra suma:

$$\text{Margen} = 1.833 \cdot 3.1623 \cdot 3.3745 \approx 19.5606$$

Reemplazamos en la fórmula despejada:

$$\mu \geqslant \frac{2015.03 - 19.5606}{10}$$

$$\mu \geqslant \frac{1995.4694}{10}$$

$$\mu \geqslant 199.5469$$

**Conclusión final:**

Con un nivel de confianza del **$95\%$**, la cota inferior para la media del voltaje de ruptura es **$199.55$**. Esto garantiza estadísticamente que el voltaje medio verdadero de estos capacitores es de 199.55 o superior.







![[Pasted image 20260728012753.png]]



Aquí tienes la resolución del ejercicio 11.5 de la imagen **image_351343.png**, manteniendo nuestra filosofía de trabajar todo desde la **sumatoria**.

Este ejercicio es excelente porque te obliga a tomar una decisión según el tamaño de la muestra ($n$):

- En el caso **(a)**, como $n=10$ es un tamaño de muestra pequeño, no podemos usar la aproximación Normal. Tenemos que usar la distribución "exacta".
    
- En el caso **(b)**, como $n=100$ es grande, podemos invocar al Teorema Central del Límite y usar nuestra querida Normal (intervalo asintótico).
    

Vamos a resolver ambos paso a paso.

### Caso (a): Muestra pequeña ($n = 10$) - Intervalo Exacto

**1. Definición de la Variable y la Sumatoria**

Sabemos que los tiempos individuales tienen distribución Exponencial: $T_i \sim \mathcal{E}(\lambda)$.

Nuestra variable de estudio es la sumatoria total:

$$S = \sum_{i=1}^{10} T_i$$

Por teoría de probabilidades, la suma de variables exponenciales independientes tiene una distribución Gamma. Y, específicamente, existe un "truco" o propiedad matemática para armar el pivote exacto: si multiplicamos esa suma por $2\lambda$, obtenemos una distribución **Chi-cuadrado ($\chi^2$)** con $2n$ grados de libertad.

**2. Construcción del Pivote Exacto**

Para $n=10$, los grados de libertad son $2 \cdot 10 = 20$.

$$U = 2\lambda S \sim \chi^2_{20}$$

El nivel de confianza es $0.90$ ($1 - \alpha = 0.90$). Esto significa que dejamos un $5\%$ ($\alpha/2 = 0.05$) de error en cada cola.

Buscamos en la tabla de la distribución Chi-cuadrado con 20 grados de libertad los dos valores críticos que encierran ese $90\%$:

- **Valor crítico inferior ($a$):** $\chi^2_{20, 0.05} \approx 10.851$
    
- **Valor crítico superior ($b$):** $\chi^2_{20, 0.95} \approx 31.410$
    

**3. Despeje de la Región de Confianza**

Planteamos la inecuación y despejamos la intensidad $\lambda$:

$$P(10.851 \leqslant 2\lambda S \leqslant 31.410) = 0.90$$

Dividimos todo por $2S$ para dejar la $\lambda$ sola en el centro:

$$\frac{10.851}{2S} \leqslant \lambda \leqslant \frac{31.410}{2S}$$

**4. Cálculo Final (a)**

El enunciado nos da el valor de la sumatoria observada: $S = 29.51$.

Reemplazamos en nuestra fórmula:

- **Límite Inferior:** $\frac{10.851}{2 \cdot 29.51} = \frac{10.851}{59.02} \approx 0.1838$
    
- **Límite Superior:** $\frac{31.410}{2 \cdot 29.51} = \frac{31.410}{59.02} \approx 0.5322$
    

**Respuesta (a):** El intervalo de confianza exacto al 90% para $\lambda$ es **$[0.1838, 0.5322]$**.

### Caso (b): Muestra grande ($n = 100$) - Intervalo Asintótico

**1. El Pivote Asintótico desde la Sumatoria**

Aquí $n=100$. Podríamos buscar una Chi-cuadrado con 200 grados de libertad, pero esas tablas no suelen existir. En su lugar, usamos el Teorema Central del Límite sobre nuestra sumatoria $S$.

Sabemos que en una Exponencial, la media es $1/\lambda$ y la varianza es $1/\lambda^2$.

Para la sumatoria $S$, la media será $n/\lambda$ y la varianza $n/\lambda^2$.

Armamos el pivote tipificando la sumatoria (restando su media y dividiendo por su desvío):

$$Z = \frac{S - n/\lambda}{\sqrt{n/\lambda^2}} = \frac{S - n/\lambda}{\sqrt{n}/\lambda} \sim \mathcal{N}(0,1)$$

Si resolvemos esa fracción (multiplicando numerador y denominador por $\lambda$), nos queda un pivote asintótico hermosamente simple:

$$Z = \frac{\lambda S - n}{\sqrt{n}} \sim \mathcal{N}(0,1)$$

**2. Despeje de la Región de Confianza**

Para un nivel de confianza del $0.90$, buscamos en la tabla Normal el valor crítico $z_{0.95}$:

- **Valor crítico:** $1.645$
    

Planteamos la inecuación:

$$-1.645 \leqslant \frac{\lambda S - n}{\sqrt{n}} \leqslant 1.645$$

Pasamos $\sqrt{n}$ multiplicando:

$$-1.645\sqrt{n} \leqslant \lambda S - n \leqslant 1.645\sqrt{n}$$

Pasamos la $n$ sumando:

$$n - 1.645\sqrt{n} \leqslant \lambda S \leqslant n + 1.645\sqrt{n}$$

Dividimos todo por $S$:

$$\frac{n - 1.645\sqrt{n}}{S} \leqslant \lambda \leqslant \frac{n + 1.645\sqrt{n}}{S}$$

_(Nota curiosa: ¡Logramos despejar la $\lambda$ perfectamente sin necesidad de usar el teorema de Slutsky ni ecuaciones cuadráticas!)_

**3. Cálculo Final (b)**

El enunciado nos da $n = 100$ (por ende, $\sqrt{n} = 10$) y la nueva sumatoria $S = 223.21$.

Reemplazamos en nuestra fórmula:

- **Margen de error del numerador:** $1.645 \cdot 10 = 16.45$
    
- **Límite Inferior:** $\frac{100 - 16.45}{223.21} = \frac{83.55}{223.21} \approx 0.3743$
    
- **Límite Superior:** $\frac{100 + 16.45}{223.21} = \frac{116.45}{223.21} \approx 0.5217$
    

**Respuesta (b):** El intervalo de confianza asintótico al 90% para $\lambda$ es **$[0.3743, 0.5217]$**.


![[Pasted image 20260728012937.png]]

Aquí tienes la resolución del ejercicio 11.6 de la imagen **image_350818.png**.

Este ejercicio es una aplicación directa de lo que vimos en el punto 11.5(a), porque existe una relación fundamental en estadística: **en un proceso de Poisson, el tiempo que transcurre entre cada arribo distribuye de forma Exponencial**.

Siguiendo nuestra metodología, vamos a plantear todo en base a la sumatoria.

### 1. Definición de la Variable y la Sumatoria

Definimos $T_i$ como el tiempo (en minutos) que transcurre entre la llegada de un cliente y el siguiente. Como los clientes llegan según un proceso de Poisson de intensidad $\lambda$, sabemos que:

$$T_i \sim \mathcal{E}(\lambda)$$

Nuestra variable de estudio será la **sumatoria total** del tiempo esperado hasta que llega el cliente número $n=6$:

$$S = \sum_{i=1}^{6} T_i$$

Calcular esta sumatoria a partir de los datos es muy sencillo. No hace falta sumar las diferencias una por una; el tiempo total transcurrido es simplemente la hora a la que llegó el último cliente (10:16) menos la hora a la que abrió el banco (10:00).

$$S = 16 \text{ minutos}$$

### 2. Construcción del Pivote Exacto

Como nuestra muestra es pequeña ($n=6$) y es la suma de variables exponenciales, utilizamos exactamente el mismo pivote Chi-cuadrado ($\chi^2$) que aprendimos en el ejercicio anterior. Los grados de libertad serán $2n = 12$:

$$U = 2\lambda S \sim \chi^2_{12}$$

El enunciado nos pide una **cota inferior** de nivel $0.9$. Esto significa que queremos un nivel de confianza del **$90\%$** ($1 - \alpha = 0.90$) y que todo el $10\%$ de riesgo ($\alpha = 0.10$) lo vamos a dejar en la cola inferior de la distribución.

Buscamos en la tabla de Chi-cuadrado con 12 grados de libertad el valor que acumula un $0.10$ de probabilidad a su izquierda (a veces denotado como $\chi^2_{12, 0.10}$):

- **Valor crítico:** $6.304$
    

### 3. Despeje de la Cota Inferior

Planteamos la inecuación asegurándonos de que nuestro pivote sea mayor o igual al valor crítico. Esto nos garantizará el $90\%$ de probabilidad hacia la derecha y nos permitirá despejar un límite inferior para $\lambda$:

$$P(2\lambda S \geqslant 6.304) = 0.90$$

Despejamos la intensidad $\lambda$ dividiendo por $2S$:

$$\lambda \geqslant \frac{6.304}{2S}$$

Esta es la fórmula de nuestra cota inferior.

### 4. Cálculo Final

Reemplazamos nuestra sumatoria observada ($S = 16$) en la fórmula:

$$\lambda \geqslant \frac{6.304}{2 \cdot 16}$$

$$\lambda \geqslant \frac{6.304}{32}$$

$$\lambda \geqslant 0.197$$

**Conclusión final:**

Con un nivel de confianza del **$90\%$**, la cota inferior para la intensidad del proceso es **$0.197$**. Esto significa que podemos afirmar estadísticamente que los clientes llegan al banco a una tasa de al menos $0.197$ clientes por minuto.


![[Pasted image 20260728013242.png]]


¡Ojo con este ejercicio de la imagen **image_34b260.png**! Acá hay una trampa o "plot twist" importante respecto a los anteriores.

Hasta ahora veníamos armando todo en base a la **sumatoria** de los datos, pero si leés bien el enunciado, acá no te dan el total ni el promedio. Te dan la **duración mínima** observada entre las 5 lámparas.

Por lo tanto, no podemos usar la suma. Tenemos que usar la teoría de estadísticos de orden (específicamente, el mínimo).

Aquí te muestro cómo se adapta el método a esta situación:

### 1. Definición de la Variable y el Estadístico (El Mínimo)

La duración de una lámpara individual es $X_i \sim \mathcal{E}(\lambda)$.

Al poner a prueba $n = 5$ lámparas juntas y registrar la primera que se quema, lo que estamos observando es el estadístico del mínimo, al que llamaremos $Y_1$:

$$Y_1 = \min(X_1, X_2, X_3, X_4, X_5) = 200$$

Por propiedad de la distribución Exponencial (que se suele demostrar en la guía anterior), el mínimo de $n$ exponenciales independientes de parámetro $\lambda$ es también una variable exponencial, pero con parámetro $n\lambda$.

Como tenemos 5 lámparas, nuestro mínimo distribuye así:

$$Y_1 \sim \mathcal{E}(5\lambda)$$

### 2. Construcción del Pivote Exacto

Como nuestro estadístico $Y_1$ sigue teniendo una distribución exponencial, podemos aplicar exactamente el mismo truco de la **Chi-cuadrado ($\chi^2$)** que usamos en los ejercicios 11.5 y 11.6.

La regla estadística dice que si multiplicás cualquier variable exponencial por 2 veces su parámetro, obtenés una $\chi^2$ con 2 grados de libertad.

El parámetro de nuestra variable $Y_1$ es $5\lambda$. Entonces armamos el pivote:

$$U = 2 \cdot (5\lambda) \cdot Y_1 = 10\lambda Y_1 \sim \chi^2_2$$

Nos piden una **cota inferior** de nivel $0.95$. Esto significa que queremos dejar el $5\%$ de riesgo ($\alpha = 0.05$) concentrado en la cola izquierda de la distribución.

Buscamos en la tabla Chi-cuadrado con 2 grados de libertad el valor que acumula $0.05$ a su izquierda. _(Dato de color: como la $\chi^2_2$ es en realidad una exponencial, este valor exacto sale de calcular $-2\ln(0.95)$)_.

- **Valor crítico:** $\approx 0.1026$
    

### 3. Despeje de la Cota Inferior

Planteamos la inecuación asegurando que el pivote sea mayor o igual al valor crítico. Esto atrapa el $95\%$ de probabilidad hacia la derecha y nos deja despejar un límite inferior:

$$P(10\lambda Y_1 \geqslant 0.1026) = 0.95$$

Despejamos la intensidad $\lambda$ pasando el resto dividiendo:

$$\lambda \geqslant \frac{0.1026}{10 \cdot Y_1}$$

### 4. Cálculo Final

Reemplazamos el valor del mínimo que efectivamente se observó en la prueba ($Y_1 = 200$ horas):

$$\lambda \geqslant \frac{0.1026}{10 \cdot 200}$$

$$\lambda \geqslant \frac{0.1026}{2000}$$

$$\lambda \geqslant 0.0000513$$

**Conclusión final:**

Con un nivel de confianza del **$95\%$**, la cota inferior para la intensidad es **$\lambda \geqslant 0.0000513$** fallas por hora.



![[Pasted image 20260728014017.png]]


Aquí tienes la resolución del ejercicio 11.8 de la imagen **image_34a399.png**.

Al igual que en el ejercicio anterior donde tuvimos que usar el _mínimo_ porque nos daban ese dato, acá el enunciado nos da la **máxima longitud observada**. Cuando trabajamos con distribuciones Uniformes donde el parámetro desconocido está en el extremo del intervalo, usar el estadístico del máximo es el camino indicado.

Para que las cuentas sean mucho más amigables, vamos a aplicar un pequeño truco inicial: hacer un cambio de variable para "correr" la distribución hacia el cero.

### 1. Definición de la Variable y el Estadístico (El Máximo)

Sabemos que la longitud de cada rollo distribuye así: $X_i \sim \mathcal{U}(15, 15 + \theta)$.

Para simplificar, le restamos 15 metros a todos los rollos. Definimos una nueva variable $W_i = X_i - 15$.

Ahora nuestra variable arranca desde cero:

$$W_i \sim \mathcal{U}(0, \theta)$$

Se examinaron $n = 4$ rollos. El máximo observado de los rollos originales fue $\max(X_i) = 25$.

Por lo tanto, el máximo de nuestras variables restadas ($M$) será:

$$M = \max(W_1, W_2, W_3, W_4) = 25 - 15 = 10$$

Por teoría, la función de probabilidad acumulada del máximo de $n$ variables uniformes $\mathcal{U}(0, \theta)$ es:

$$F_M(m) = P(M \leqslant m) = \left(\frac{m}{\theta}\right)^n$$

### 2. Construcción del Pivote

Para armar un pivote $U$ cuya distribución no dependa de $\theta$, simplemente pasamos la $\theta$ dividiendo:

$$U = \frac{M}{\theta}$$

Si calculamos la probabilidad acumulada de este pivote, nos queda una fórmula facilísima que solo depende del tamaño de muestra $n$ (donde los valores posibles de $U$ van de 0 a 1):

$$P(U \leqslant u) = u^n$$

El enunciado pide una **cota superior** con nivel de confianza de **$0.99$** ($99\%$). Como queremos que $\theta$ nos quede acotada por _debajo_ de un número ($\theta \leqslant \dots$), necesitamos plantear que nuestro pivote sea _mayor o igual_ a un cierto valor crítico $a$:

$$P(U \geqslant a) = 0.99$$

Lo que es matemáticamente equivalente a decir que la probabilidad acumulada a su izquierda es del $1\%$:

$$P(U \leqslant a) = 0.01$$

### 3. Despeje del Valor Crítico

Usamos la fórmula de la probabilidad acumulada del pivote ($u^n$) que definimos arriba, sabiendo que $n=4$:

$$a^4 = 0.01$$

$$a = \sqrt[4]{0.01} \approx 0.3162$$

### 4. Despeje de la Cota Superior y Cálculo

Planteamos la inecuación original del pivote con el valor crítico que encontramos:

$$P\left( \frac{M}{\theta} \geqslant 0.3162 \right) = 0.99$$

Despejamos la $\theta$. Primero la pasamos multiplicando:

$$M \geqslant 0.3162 \cdot \theta$$

Y pasamos el número dividiendo:

$$\frac{M}{0.3162} \geqslant \theta$$

$$\theta \leqslant \frac{M}{0.3162}$$

Finalmente, reemplazamos el valor del máximo observado que calculamos en el primer paso ($M = 10$):

$$\theta \leqslant \frac{10}{0.3162}$$

$$\theta \leqslant 31.6227$$

_(Nota: Como el máximo observado $M$ fue 10, lógicamente sabemos que $\theta$ jamás podría ser menor que 10. Por lo que el intervalo real de $\theta$ siempre estará entre $M$ y tu cota)._

**Conclusión final:**

Con un nivel de confianza del **$99\%$**, la cota superior para el parámetro es **$\theta \leqslant 31.62$**.






¡Excelente pregunta! No sale de una galera mágica, sino de mirar con mucha atención la fórmula de la probabilidad acumulada que calculamos un renglón antes.

El objetivo del **Método del Pivote** es inventar una variable matemática que mezcle tu dato (el estadístico $M$) con tu incógnita ($\theta$), pero con la condición obligatoria de que **su distribución final de probabilidades no dependa de $\theta$**.

¿Cómo nos damos cuenta de que $U = \frac{M}{\theta}$ es el candidato perfecto? Por la forma estructural que tiene la función.

Fijate en el paso 1 del ejercicio 11.9. Habíamos llegado a que la probabilidad acumulada del máximo era:

$$F_M(m) = P(M \leqslant m) = \left( \frac{m}{\theta} \right)^6$$

La variable $m$ y el parámetro $\theta$ están "atados" como una fracción. Para deshacernos de la $\theta$ en el resultado final, la estrategia algebraica natural es proponer un cambio de variable que fuerce esa cancelación.

Vamos a demostrar paso a paso por qué funciona inventar $U = \frac{M}{\theta}$:

1. Buscamos la función de distribución de esta nueva variable $U$:
    
    $$P(U \leqslant u)$$
    
2. Reemplazamos la $U$ por el invento que propusimos:
    
    $$P\left( \frac{M}{\theta} \leqslant u \right)$$
    
3. Despejamos la $M$ pasando la $\theta$ multiplicando (como es una longitud/parámetro positivo, el signo de la inecuación no se altera):
    
    $$P(M \leqslant u \cdot \theta)$$
    
4. ¡Acá está la magia! Eso que nos quedó adentro del paréntesis es exactamente la definición de la función de probabilidad acumulada $F_M$, pero en lugar de evaluarla en $m$, la evaluamos en $u \cdot \theta$. Reemplazamos eso en nuestra fórmula original $\left( \frac{m}{\theta} \right)^6$:
    
    $$P(U \leqslant u) = \left( \frac{u \cdot \theta}{\theta} \right)^6$$
    
5. Las $\theta$ del numerador y denominador se cancelan perfectamente:
    
    $$P(U \leqslant u) = u^6$$
    

### En resumen

Ese pivote sale de un análisis de conveniencia algebraica. Al proponer $U = \frac{M}{\theta}$, logramos que su distribución ($u^6$) dependa puramente de un número, sin ninguna incógnita.

Como regla general: en todas las distribuciones donde el parámetro $\theta$ funciona como el "techo" o límite superior del dominio (como la distribución Uniforme de la imagen anterior o esta función triangular), el pivote de turno casi siempre se va a construir dividiendo el máximo de la muestra por el parámetro.









¡Excelente elección! Resolver el ejercicio 11.8 de **image_33c547.png** con el método directo y asimétrico es el camino más elegante, porque llegás al mismo resultado sin tener que inventar el pivote $U$.

Aquí te muestro cómo queda aplicando la misma lógica del ejercicio anterior.

### 1. Definición del Estadístico y su Probabilidad

Para que el álgebra sea mucho más sencilla, vamos a aplicar el mismo truco inicial: restarle **15** metros a la variable original para que arranque desde cero.

Definimos $W_i = X_i - 15$, por lo que ahora $W_i \sim \mathcal{U}(0, \theta)$.

Se examinaron $n = 4$ rollos. Nuestro estadístico será el máximo de estas nuevas variables:

$$T = \max(W_1, W_2, W_3, W_4)$$

La probabilidad acumulada de este estadístico máximo, sabiendo que el tamaño de muestra es 4, es:

$$P(T \leqslant t) = \left( \frac{t}{\theta} \right)^4$$

### 2. Planteo Asimétrico (Cota Superior)

El enunciado pide una **cota superior** con un nivel de confianza de **0.99** (es decir, el **99%**). Esto nos deja un **1%** de riesgo (**0.01**).

Como queremos construir una cota superior, nuestro objetivo final es llegar a una expresión del tipo $\theta \leqslant \text{algo}$. Para lograr esto manipulando directamente a $T$, necesitamos asegurar que $T$ sea _mayor o igual_ a un cierto valor de corte $K$ el **99%** de las veces:

$$P(T \geqslant K) = 0.99$$

Por regla del complemento, esto significa que todo nuestro **1%** de riesgo queda arrinconado en la probabilidad de que $T$ sea más chico que $K$:

$$P(T \leqslant K) = 0.01$$

### 3. Despeje del Valor de Corte $K$

Tomamos la ecuación de nuestro riesgo y la reemplazamos en la fórmula de probabilidad acumulada que definimos en el primer paso:

$$\left( \frac{K}{\theta} \right)^4 = 0.01$$

Despejamos $K$:

$$\frac{K}{\theta} = \sqrt[4]{0.01}$$

$$\frac{K}{\theta} \approx 0.3162$$

$$K = \theta \cdot 0.3162$$

### 4. Despeje de la Cota Superior

Volvemos a nuestra inecuación de confianza del paso 2 ($T \geqslant K$) y reemplazamos la $K$ que acabamos de encontrar:

$$P(T \geqslant \theta \cdot 0.3162) = 0.99$$

Ahora simplemente despejamos la $\theta$ pasando el número dividiendo. Al leer la inecuación de derecha a izquierda, vas a ver que la $\theta$ ya nos quedó acotada por arriba:

$$\frac{T}{0.3162} \geqslant \theta$$

$$\theta \leqslant \frac{T}{0.3162}$$

¡Esa es nuestra fórmula directa para la cota superior!

### 5. Cálculos Finales con la Muestra

El enunciado indica que el máximo observado de los rollos originales fue **25** metros. Como al principio del ejercicio decidimos restarle **15** a todo para simplificar, nuestro estadístico observado es:

$$T = 25 - 15 = 10$$

Reemplazamos $T$ en la fórmula que despejamos:

$$\theta \leqslant \frac{10}{0.3162}$$

$$\theta \leqslant 31.6255$$

**Conclusión final:**

Con un nivel de confianza del **99%**, la cota superior para el parámetro es **$\theta \leqslant 31.62$**.

Como ves, la lógica de manipular la $T$ directamente funciona a la perfección y te ahorra tener que justificar de dónde salió la fracción $M/\theta$.


![[Pasted image 20260728014430.png]]


Acá tenés la resolución del ejercicio 11.9 de la imagen **image_349c36.png**.

Este ejercicio es un "primo hermano" del 11.8. Como el parámetro $\theta$ está limitando el dominio de la función ($0 \leqslant x \leqslant \theta$), el estadístico estrella que tenemos que usar vuelve a ser el **máximo** de la muestra.

La única diferencia es que la distribución ya no es Uniforme, sino que tiene una forma triangular o cuadrática. Así que tenemos que arremangarnos y calcular su probabilidad acumulada desde cero usando integrales.

### 1. Definición del Estadístico y su Probabilidad

Primero, necesitamos la función de probabilidad acumulada $F(x)$ para una sola variable $X_i$. Integramos la función de densidad que nos da el enunciado:

$$F(x) = \int_{0}^{x} \frac{2t}{\theta^2} dt = \left[ \frac{t^2}{\theta^2} \right]_{0}^{x} = \frac{x^2}{\theta^2}$$

El tamaño de nuestra muestra es $n = 3$. El estadístico que vamos a usar es el máximo: $M = \max(X_1, X_2, X_3)$.

Por teoría, la probabilidad acumulada del máximo de $n$ variables es elevar la $F(x)$ original a la $n$:

$$F_M(m) = P(M \leqslant m) = [F(m)]^n = \left( \frac{m^2}{\theta^2} \right)^3 = \left( \frac{m}{\theta} \right)^6$$

### 2. Construcción del Pivote

Igual que en el ejercicio anterior, para "limpiar" la $\theta$ y armar un pivote $U$ cuya distribución sea independiente de parámetros desconocidos, pasamos la $\theta$ dividiendo:

$$U = \frac{M}{\theta}$$

Calculamos la probabilidad acumulada de este pivote reemplazando en la fórmula de arriba:

$$P(U \leqslant u) = P\left(\frac{M}{\theta} \leqslant u\right) = P(M \leqslant u\theta) = F_M(u\theta) = \left( \frac{u\theta}{\theta} \right)^6 = u^6$$

_(Nota: Esto vale para $0 \leqslant u \leqslant 1$, ya que el máximo de la muestra $M$ jamás puede ser más grande que el límite $\theta$)._

### 3. Definición del Valor Crítico (El truco del intervalo más corto)

Nos piden un intervalo de confianza del **$90\%$** ($0.9$).

Acá hay un detalle estadístico clave: podríamos dejar un $5\%$ de riesgo en cada cola (colas simétricas). Pero como sabemos con total certeza que $M \leqslant \theta$, nuestro pivote $U = M/\theta$ tiene un tope inamovible en $1$.

Para conseguir el intervalo más corto y preciso posible, lo mejor es anclar el límite superior del pivote en $1$, y dejar todo el $10\%$ de riesgo en la cola inferior:

$$P(a \leqslant U \leqslant 1) = 0.90$$

Usando nuestra fórmula acumulada $u^6$, esto significa que:

$$P(U \leqslant 1) - P(U \leqslant a) = 0.90$$

$$1^6 - a^6 = 0.90$$

$$1 - a^6 = 0.90$$

$$a^6 = 0.10$$

$$a = \sqrt[6]{0.10} \approx 0.68129$$

### 4. Despeje de la Región de Confianza

Planteamos la inecuación de nuestro pivote con el valor $a$ que encontramos:

$$0.68129 \leqslant \frac{M}{\theta} \leqslant 1$$

Invertimos las fracciones en los tres miembros (¡recordá que esto da vuelta los signos de desigualdad!):

$$\frac{1}{0.68129} \geqslant \frac{\theta}{M} \geqslant 1$$

Multiplicamos todo por $M$ y lo ordenamos de menor a mayor para que se lea mejor:

$$M \leqslant \theta \leqslant \frac{M}{0.68129}$$

¡Esa es nuestra fórmula final del intervalo!

### 5. Cálculo con los Datos de la Muestra

El enunciado nos da los tres valores observados: $0.8$, $0.1$ y $0.3$.

El máximo de esos valores es:

$$M = \max(0.8, 0.1, 0.3) = 0.8$$

Reemplazamos $M$ en nuestra fórmula:

- **Límite Inferior:** $0.8$
    
- **Límite Superior:** $\frac{0.8}{0.68129} \approx 1.1742$
    

**Conclusión final:**

Basado en la muestra, el intervalo de confianza del **$90\%$** para el parámetro $\theta$ es **$[0.8, 1.1742]$**.






o sino

Aquí tienes la resolución completa del **Ejercicio 11.9** siguiendo exactamente la lógica de "colas simétricas" y el método directo (sin el pivote $U$) que aplicó el alumno en la hoja.

### 1. Definición del Estadístico y su Probabilidad

El tamaño de la muestra es $n = 3$. Primero calculamos la función de distribución acumulada para una sola variable $X_i$ integrando la densidad:

$$F(x) = \int_{0}^{x} \frac{2t}{\theta^2} dt = \frac{x^2}{\theta^2}$$

El estadístico suficiente para este tipo de distribución es el máximo, al que llamaremos $T$:

$$T = \max(X_1, X_2, X_3)$$

La probabilidad acumulada de este estadístico máximo es la original elevada a la $n$:

$$P(T \leqslant t) = [F(t)]^3 = \left( \frac{t^2}{\theta^2} \right)^3 = \left( \frac{t}{\theta} \right)^6$$

### 2. Planteo de las Colas Simétricas

El enunciado pide un nivel de confianza del **$90\%$** ($0.90$). Esto deja un $10\%$ de margen de error.

En lugar de mandar todo el error a un lado, este método lo divide exactamente a la mitad:

- Un **$5\%$** ($0.05$) para la cola inferior.
    
- Un **$5\%$** ($0.05$) para la cola superior.
    

### 3. Despeje de la Cota Superior (Cola Inferior)

Buscamos un valor $K_1$ tal que la probabilidad de que el estadístico sea menor a ese valor sea del $5\%$:

$$P(T \leqslant K_1) = 0.05$$

Reemplazamos en nuestra fórmula de probabilidad:

$$\left( \frac{K_1}{\theta} \right)^6 = 0.05$$

Despejamos $K_1$:

$$\frac{K_1}{\theta} = 0.05^{1/6}$$

$$K_1 = \theta \cdot 0.05^{1/6}$$

Ahora, volvemos a meter esto en la probabilidad original para despejar la $\theta$:

$$P(T \leqslant \theta \cdot 0.05^{1/6}) = 0.05$$

Pasamos el número dividiendo:

$$P\left( \frac{T}{0.05^{1/6}} \leqslant \theta \right) = 0.05$$

Esta expresión nos define la **cota superior** de nuestro intervalo.

### 4. Despeje de la Cota Inferior (Cola Superior)

Ahora buscamos un valor $K_2$ para el otro $5\%$ de riesgo en el extremo opuesto (la probabilidad de que el estadístico sea mayor a $K_2$):

$$P(T > K_2) = 0.05$$

Por complemento, esto significa que la probabilidad acumulada hasta $K_2$ es del $95\%$:

$$P(T \leqslant K_2) = 0.95$$

Reemplazamos en la fórmula:

$$\left( \frac{K_2}{\theta} \right)^6 = 0.95$$

Despejamos $K_2$:

$$K_2 = \theta \cdot 0.95^{1/6}$$

Volvemos a armar la probabilidad original para despejar $\theta$:

$$P(T > \theta \cdot 0.95^{1/6}) = 0.05$$

Pasamos el número dividiendo:

$$P\left( \frac{T}{0.95^{1/6}} > \theta \right) = 0.05$$

Esta expresión nos define la **cota inferior**.

### 5. Fórmula General del Intervalo

Juntando las dos cotas que despejamos en los pasos 3 y 4, la estructura del intervalo de confianza para $\theta$ queda así:

$$IC(\theta) = \left[ \frac{T}{0.95^{1/6}} ; \frac{T}{0.05^{1/6}} \right]$$

### 6. Cálculos Finales con la Muestra

A partir de la muestra del enunciado ($0.8, 0.1, 0.3$), obtenemos nuestro estadístico máximo:

$$T = \max(0.8, 0.1, 0.3) = 0.8$$

Resolvemos los denominadores con calculadora:

- $0.95^{1/6} \approx 0.9914$
    
- $0.05^{1/6} \approx 0.6069$
    

Reemplazamos en la fórmula del intervalo:

- **Límite Inferior:** $\frac{0.8}{0.9914} \approx 0.8069$
    
- **Límite Superior:** $\frac{0.8}{0.6069} \approx 1.3181$
    

**Conclusión final del método simétrico:**

El intervalo de confianza al $90\%$ es **$[0.8069, 1.3181]$**.

> **Nota teórica:** Como charlamos antes, aunque el procedimiento matemático es perfecto, fijate que el límite inferior dio $0.8069$, dejando afuera el valor real $0.8$ que efectivamente midieron. Por eso se suele preferir el otro método.











¡Esta es la mejor combinación posible! Vamos a usar el **método directo** (manipulando la variable $T$ como hizo el alumno de la hoja, sin inventar la letra $U$), pero aplicando la **lógica asimétrica** para no cometer el error de dejar afuera al máximo observado.

Así es como se resuelve para conseguir el intervalo más corto y exacto:

### 1. Definición del Estadístico y su Probabilidad

Igual que antes, para una muestra de tamaño $n = 3$, usamos el estadístico máximo:

$$T = \max(X_1, X_2, X_3)$$

Ya sabemos que su probabilidad acumulada es:

$$P(T \leqslant t) = \left( \frac{t}{\theta} \right)^6$$

### 2. Planteo Asimétrico (La lógica del dominio)

Sabemos por definición de la función que cualquier valor observado jamás puede ser mayor que el parámetro $\theta$. Por lo tanto, es una certeza absoluta que nuestro máximo cumplirá siempre que $T \leqslant \theta$.

En términos de probabilidad, esto significa que:

$$P(T \leqslant \theta) = 1$$

Como nos piden un nivel de confianza del **$90\%$** ($0.90$), tenemos un $10\%$ de riesgo ($0.10$). En lugar de dividirlo, vamos a concentrar todo ese riesgo en los valores más chicos de $T$, anclando el extremo superior en $\theta$.

Planteamos que la probabilidad de que $T$ caiga entre un valor de corte $K$ y su tope máximo $\theta$ es del $90\%$:

$$P(K \leqslant T \leqslant \theta) = 0.90$$

### 3. Despeje del Valor $K$

Para que esa inecuación funcione, la probabilidad de que $T$ sea más chico que $K$ tiene que ser exactamente ese $10\%$ sobrante:

$$P(T \leqslant K) = 0.10$$

Reemplazamos esto en nuestra fórmula de probabilidad acumulada:

$$\left( \frac{K}{\theta} \right)^6 = 0.10$$

Despejamos $K$:

$$\frac{K}{\theta} = 0.10^{1/6}$$

$$K = \theta \cdot 0.10^{1/6}$$

### 4. Despeje del Intervalo de Confianza

Volvemos a nuestra inecuación doble del paso 2 y reemplazamos la $K$ que acabamos de despejar:

$$P(\theta \cdot 0.10^{1/6} \leqslant T \leqslant \theta) = 0.90$$

Ahora nuestro objetivo es dejar a la $\theta$ sola en el medio. Para que sea fácil de ver, analizamos la inecuación en dos partes:

- **Lado derecho:** $T \leqslant \theta$
    
    ¡Esta ya está despejada! Nos dice que la $\theta$ siempre es mayor o igual a $T$. Esa es nuestra **cota inferior**.
    
- **Lado izquierdo:** $\theta \cdot 0.10^{1/6} \leqslant T$
    
    Pasamos el número dividiendo para dejar la $\theta$ sola:
    
    $$\theta \leqslant \frac{T}{0.10^{1/6}}$$
    
    Esa es nuestra **cota superior**.
    

Juntando ambas partes, la fórmula general de nuestro intervalo nos queda perfecta:

$$IC(\theta) = \left[ T ; \frac{T}{0.10^{1/6}} \right]$$

### 5. Cálculos Finales con la Muestra

El enunciado nos da los valores $0.8, 0.1, 0.3$.

Nuestro estadístico máximo es:

$$T = \max(0.8, 0.1, 0.3) = 0.8$$

Resolvemos el denominador en la calculadora:

$$0.10^{1/6} \approx 0.68129$$

Reemplazamos en nuestra fórmula del intervalo:

- **Límite Inferior:** $0.8$
    
- **Límite Superior:** $\frac{0.8}{0.68129} \approx 1.1742$
    

**Conclusión final:**

El intervalo de confianza al $90\%$ es **$[0.8, 1.1742]$**.

Fijate cómo usando el método directo de la hoja, pero aplicando la lógica correcta de no dividir el error, llegamos exactamente al mismo resultado óptimo de $[0.8, 1.17]$ que habíamos calculado la primera vez.



![[Pasted image 20260728022115.png]]


¡Perfecto! Vamos a aplicar exactamente la misma filosofía de la **sumatoria** para este ejercicio 11.10 de la imagen **image_33be05.png**.

Aunque sea un ejercicio de proporciones (porcentajes), vas a ver que el método de sumar todo funciona de maravilla y nos evita trabajar con números decimales minúsculos desde el principio.

### 1. Definición de la Variable y la Sumatoria

Definimos $X_i$ como el estado de un artículo, donde $X_i = 1$ si es defectuoso y $X_i = 0$ si no lo es. Esto es una variable Bernoulli con una probabilidad $p$ desconocida.

Se tomó una muestra de $n = 200$ artículos. Nuestra **sumatoria total** es la cantidad de artículos defectuosos encontrados:

$$S = \sum_{i=1}^{200} X_i = 11$$

La suma de variables Bernoulli nos da una distribución Binomial, pero como $n$ es un número grande ($200$), invocamos al Teorema Central del Límite para usar una aproximación Normal (intervalo asintótico):

$$S \sim \mathcal{N}(np, np(1-p))$$

**El detalle técnico para proporciones:** Para armar el pivote, necesitamos calcular el desvío estándar ($\sqrt{np(1-p)}$). Como no conocemos la verdadera $p$, la estadística nos permite estimarla usando la proporción observada en la muestra $\hat{p} = \frac{S}{n} = \frac{11}{200} = 0.055$.

### Parte (a): Intervalo de Confianza del 90%

**1. Construcción del Pivote**

Armamos nuestro pivote tipificando la sumatoria:

$$Z = \frac{S - np}{\sqrt{n \hat{p}(1-\hat{p})}} \sim \mathcal{N}(0, 1)$$

Para un nivel de confianza del **$90\%$** ($1 - \alpha = 0.90$), dejamos un $5\%$ de error en cada cola. Buscamos en la tabla Normal el valor crítico $z_{0.95}$:

- **Valor crítico:** $1.645$
    

**2. Despeje de la Región de Confianza**

Planteamos la inecuación:

$$-1.645 \leqslant \frac{S - np}{\sqrt{n \hat{p}(1-\hat{p})}} \leqslant 1.645$$

Pasamos multiplicando la raíz (el desvío de la suma):

$$-1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})} \leqslant S - np \leqslant 1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})}$$

Restamos la sumatoria $S$ en todos los lados, multiplicamos por $-1$ (dando vuelta los signos) y nos queda el término central positivo:

$$S - 1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})} \leqslant np \leqslant S + 1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})}$$

Finalmente, dividimos todo por $n$ para despejar nuestra proporción $p$:

$$\frac{S - 1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})}}{n} \leqslant p \leqslant \frac{S + 1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})}}{n}$$

**3. Cálculos Finales (a)**

Calculamos el desvío estándar de nuestra suma observada:

$$\text{Desvío} = \sqrt{200 \cdot 0.055 \cdot (1 - 0.055)} = \sqrt{200 \cdot 0.055 \cdot 0.945} = \sqrt{10.395} \approx 3.2241$$

Calculamos el margen de error para la sumatoria:

$$\text{Margen} = 1.645 \cdot 3.2241 \approx 5.3036$$

Reemplazamos en la fórmula despejada (con $S = 11$):

- **Límite Inferior:** $\frac{11 - 5.3036}{200} = \frac{5.6964}{200} \approx 0.0285$
    
- **Límite Superior:** $\frac{11 + 5.3036}{200} = \frac{16.3036}{200} \approx 0.0815$
    

**Respuesta (a):** El intervalo de confianza asintótico al 90% para la proporción de defectuosos es **$[0.0285, 0.0815]$** (o entre 2.85% y 8.15%).

### Parte (b): Cota Inferior del 95% y Evaluación

**1. Planteo de la Cota Inferior**

Nos piden una cota inferior de nivel **$0.95$**. Al ser un intervalo unilateral (de un solo lado), no dividimos el error de $\alpha = 0.05$ en dos. Casualmente, el valor en la tabla Normal que deja un $5\%$ en una sola cola es exactamente el mismo que usamos antes para el 90% bilateral:

- **Valor crítico unilateral:** $1.645$
    

Como queremos una cota inferior para $p$ (es decir, $p \geqslant \dots$), forzamos al pivote a ser menor o igual al valor crítico:

$$P\left( \frac{S - np}{\sqrt{n \hat{p}(1-\hat{p})}} \leqslant 1.645 \right) = 0.95$$

**2. Despeje y Cálculo (b)**

El despeje algebraico es idéntico al límite inferior del paso anterior. Llegamos directamente a:

$$np \geqslant S - 1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})}$$

$$p \geqslant \frac{11 - 5.3036}{200}$$

$$p \geqslant 0.0285$$

**Respuesta (b) - La Cota:** Con un nivel de confianza del 95%, la cota inferior es **$0.0285$**.

**3. Evaluación de la afirmación del fabricante:**

El fabricante asegura que el porcentaje de defectuosos es **como máximo un $2\%$** ($p \leqslant 0.02$).

Sin embargo, nuestra estadística demuestra con un $95\%$ de seguridad que el porcentaje de defectuosos es **como mínimo un $2.85\%$** ($p \geqslant 0.0285$).

**Conclusión:** Como la cota inferior calculada es estrictamente mayor al límite que promete el fabricante, **la afirmación del fabricante es falsa (se rechaza)**. La cantidad de artículos defectuosos que recibimos es innegablemente superior a lo prometido.


![[Pasted image 20260728022433.png]]


Aquí tienes la resolución del ejercicio 11.12 de la imagen **image_3351e0.png**, aplicando nuestra metodología de la **sumatoria** paso a paso.

Como es un problema de proporciones con una muestra grande ($n=100$), la lógica es idéntica a la que usamos en el ejercicio del fabricante de artículos.

### 1. Definición de la Variable y la Sumatoria

Definimos $X_i$ como el voto de un ciudadano encuestado, donde $X_i = 1$ si vota al candidato azul y $X_i = 0$ si vota al amarillo (o a otro). Esta es una variable Bernoulli con una probabilidad $p$ desconocida.

Se encuestaron $n = 100$ ciudadanos. Nuestra **sumatoria total** es la cantidad de personas que afirmaron que votarán al candidato azul:

$$S = \sum_{i=1}^{100} X_i = 44$$

Por el Teorema Central del Límite, como la muestra es grande, la sumatoria se aproxima a una distribución Normal:

$$S \sim \mathcal{N}(np, np(1-p))$$

Para calcular la varianza de nuestro pivote, estimamos la $p$ desconocida usando la proporción que observamos en la muestra: $\hat{p} = \frac{S}{n} = \frac{44}{100} = 0.44$.

### 2. Construcción del Pivote Unilateral

Armamos el pivote tipificando nuestra sumatoria:

$$Z = \frac{S - np}{\sqrt{n \hat{p}(1-\hat{p})}} \sim \mathcal{N}(0, 1)$$

El enunciado pide una **cota inferior** de nivel asintótico **$0.95$**. Al igual que en el ejercicio anterior, al ser un límite de un solo lado, no dividimos el error en dos colas. Todo el $5\%$ de riesgo ($\alpha = 0.05$) va a un solo extremo.

Buscamos en la tabla Normal estándar el valor que acumula $0.95$ de probabilidad a su izquierda ($z_{0.95}$):

- **Valor crítico:** $1.645$
    

Para que la $p$ nos quede acotada por debajo ($p \geqslant \dots$), forzamos al pivote a ser menor o igual a nuestro valor crítico:

$$P\left( \frac{S - np}{\sqrt{n \hat{p}(1-\hat{p})}} \leqslant 1.645 \right) = 0.95$$

### 3. Despeje de la Cota Inferior

El despeje es exactamente el mismo que venimos practicando:

Pasamos multiplicando el denominador (el desvío):

$$S - np \leqslant 1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})}$$

Restamos $S$ y luego multiplicamos todo por $-1$ (lo que invierte el signo de la inecuación a $\geqslant$):

$$np \geqslant S - 1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})}$$

Dividimos todo por $n$ para despejar nuestra proporción poblacional $p$:

$$p \geqslant \frac{S - 1.645 \cdot \sqrt{n \hat{p}(1-\hat{p})}}{n}$$

### 4. Cálculos Finales con los Datos de la Encuesta

Calculamos primero el desvío estándar de nuestra sumatoria con los datos ($n=100$, $\hat{p}=0.44$, y por ende $1-\hat{p}=0.56$):

$$\text{Desvío} = \sqrt{100 \cdot 0.44 \cdot 0.56} = \sqrt{24.64} \approx 4.9639$$

Calculamos el margen de error para la sumatoria multiplicando por el valor crítico:

$$\text{Margen} = 1.645 \cdot 4.9639 \approx 8.1656$$

Reemplazamos en la fórmula despejada, sabiendo que el total de votos a favor en la muestra fue $S = 44$:

$$p \geqslant \frac{44 - 8.1656}{100}$$

$$p \geqslant \frac{35.8344}{100}$$

$$p \geqslant 0.3583$$

**Conclusión final:**

Con un nivel de confianza asintótico del **$95\%$**, la cota inferior para la proporción de votantes a favor del candidato azul es **$0.3583$** (o un $35.83\%$).



![[Pasted image 20260728022725.png]]

Aquí tienes la resolución del ejercicio 11.13 de la imagen **image_334d05.png**.

Este ejercicio tiene una trampa clásica de parcial en la que caen muchos: **las unidades de tiempo**. La intensidad $\lambda$ está definida "por segundo", pero la observación duró "4 horas". Lo primero que tenemos que hacer es unificar eso.

### 1. Definición de la Variable y la Sumatoria (y la trampa del tiempo)

Definimos $X_i$ como el número de partículas emitidas en el segundo $i$. Como es un proceso de Poisson, $X_i \sim \mathcal{P}(\lambda)$.

El tiempo total de observación en segundos es $n = 4 \text{ horas} \cdot 60 \text{ min} \cdot 60 \text{ seg} = 14400 \text{ segundos}$.

Nuestra **sumatoria total** es la cantidad de emisiones registradas en esos 14400 segundos:

$$S = \sum_{i=1}^{14400} X_i = 11150$$

Sabemos que la suma de variables de Poisson también es Poisson. Pero como $n$ es un número gigante, usamos el Teorema Central del Límite para aproximarlo a una Normal (intervalo asintótico):

$$S \sim \mathcal{N}(n\lambda, n\lambda)$$

_(Recordatorio teórico: en la distribución de Poisson, la esperanza y la varianza son iguales, ambas valen $n\lambda$ para la sumatoria)._

### 2. Construcción del Pivote

Para tipificar la variable y armar el pivote $Z$, deberíamos dividir por el desvío estándar ($\sqrt{n\lambda}$). Como la $\lambda$ es nuestra incógnita, la estadística nos permite estimar esa varianza usando el valor total que efectivamente observamos ($S$). Es decir, reemplazamos la varianza desconocida $n\lambda$ por la suma observada $S$.

Armamos el pivote:

$$Z = \frac{S - n\lambda}{\sqrt{S}} \sim \mathcal{N}(0, 1)$$

El enunciado pide un nivel de confianza del **$99\%$** ($1 - \alpha = 0.99$). Dejamos un $0.5\%$ en cada cola ($\alpha/2 = 0.005$).

Buscamos en la tabla Normal el valor crítico $z_{0.995}$:

- **Valor crítico:** $2.575$
    

### 3. Despeje de la Región de Confianza

Planteamos la inecuación doble para encerrar a la $\lambda$:

$$-2.575 \leqslant \frac{S - n\lambda}{\sqrt{S}} \leqslant 2.575$$

Pasamos multiplicando el desvío estimado ($\sqrt{S}$):

$$-2.575 \cdot \sqrt{S} \leqslant S - n\lambda \leqslant 2.575 \cdot \sqrt{S}$$

Restamos $S$ en todos los miembros, multiplicamos por $-1$ (dando vuelta los signos de la inecuación) y ordenamos:

$$S - 2.575 \cdot \sqrt{S} \leqslant n\lambda \leqslant S + 2.575 \cdot \sqrt{S}$$

Dividimos todo por $n$ para despejar definitivamente la intensidad $\lambda$:

$$\frac{S - 2.575 \cdot \sqrt{S}}{n} \leqslant \lambda \leqslant \frac{S + 2.575 \cdot \sqrt{S}}{n}$$

### 4. Cálculos Finales con los Datos de la Muestra

Tenemos nuestros datos procesados:

- $n = 14400$
    
- $S = 11150$
    

Calculamos la raíz de $S$ (nuestro desvío estimado):

$$\sqrt{11150} \approx 105.5936$$

Calculamos el margen de error que le sumaremos y restaremos a $S$:

$$\text{Margen} = 2.575 \cdot 105.5936 \approx 271.9035$$

Reemplazamos en la fórmula despejada:

- **Límite Inferior:** $\frac{11150 - 271.9035}{14400} = \frac{10878.0965}{14400} \approx 0.7554$
    
- **Límite Superior:** $\frac{11150 + 271.9035}{14400} = \frac{11421.9035}{14400} \approx 0.7932$
    

**Conclusión final:**

Con un nivel de confianza asintótico del **$99\%$**, el intervalo para la intensidad del proceso de emisión es **$[0.755, 0.793]$** partículas por segundo.




¡Es una pregunta excelente! Toca el corazón de cómo funcionan los pivotes y las estimaciones en estadística.

Para entender el porqué de esta decisión, analicemos cómo es el pivote original (el verdadero) antes de hacerle ninguna modificación:

$$Z = \frac{S - n\lambda}{\sqrt{n\lambda}}$$

Aquí te explico el rol de cada parte y por qué tomamos decisiones distintas arriba y abajo:

### 1. El numerador: La obligación de mantener la incógnita

El numerador ($S - n\lambda$) representa el error o la distancia entre tu dato observado ($S$) y la realidad teórica ($n\lambda$).

Si hiciéramos el reemplazo de $n\lambda$ por $S$ en el numerador, la ecuación quedaría así:

$$S - S = 0$$

El pivote daría cero y la letra $\lambda$ desaparecería por completo. Al no haber incógnita, se vuelve matemáticamente imposible despejar un intervalo. El numerador **tiene que conservar obligatoriamente** al parámetro desconocido para que el despeje exista.

### 2. El denominador: La regla de medir (estimable)

El denominador ($\sqrt{n\lambda}$) es el desvío estándar, y su única función matemática es actuar como una "regla" para escalar ese error del numerador.

Como no conocemos la verdadera $\lambda$, no sabemos qué tamaño tiene esa regla. Pero la estadística (mediante el Teorema de Slutsky) demuestra que si la muestra es grande, reemplazar esa regla teórica desconocida por una regla aproximada usando tus datos ($\sqrt{S}$) no rompe la distribución Normal. Funciona casi igual de bien.

### ¿Se podría dejar $n\lambda$ en el denominador?

Sí, **es estadísticamente válido y de hecho es más preciso** (se lo conoce como "Intervalo de Score").

Si armás la inecuación usando el pivote original:

$$-2.575 \leqslant \frac{S - n\lambda}{\sqrt{n\lambda}} \leqslant 2.575$$

El problema es estrictamente algebraico. Para despejar esa $\lambda$ que está atrapada adentro de una raíz abajo y restando arriba, estás obligado a elevar todos los términos al cuadrado y resolver una **ecuación cuadrática completa (usando la fórmula resolvente o de Bhaskara)**.

Reemplazar $n\lambda$ por $S$ exclusivamente en el denominador es un "atajo" universalmente aceptado (llamado "Intervalo de Wald") para poder despejar la $\lambda$ de forma lineal, rápida y sin hacer cuentas gigantescas en medio de un examen.






o sino


¡Es una excelente pregunta! Todo se reduce a una de las propiedades más famosas y únicas que tiene la **distribución de Poisson**.

En la gran mayoría de las distribuciones, la media y la varianza son dos cosas totalmente distintas. Pero en un proceso de Poisson regido por un parámetro $\lambda$, ocurre algo mágico: **su media y su varianza valen exactamente lo mismo**.

- Esperanza: $E(X) = \lambda$
    
- Varianza: $V(X) = \lambda$
    

Sabiendo esto, te explico de dónde sale ese $\sqrt{\bar{X}/n}$ que usó el alumno en el denominador, paso a paso:

### 1. La varianza del promedio

Cuando vos trabajás con el promedio de una muestra ($\bar{X}$), la estadística dicta que la varianza de ese promedio es igual a la varianza original de la variable dividida por el tamaño de la muestra ($n$).

Como nuestra variable es Poisson:

$$V(\bar{X}) = \frac{V(X)}{n} = \frac{\lambda}{n}$$

### 2. El verdadero desvío estándar

El denominador de cualquier pivote Normal ($Z$) siempre tiene que ser el desvío estándar (es decir, la raíz cuadrada de la varianza que calculamos recién).

Por lo tanto, el denominador "teórico y perfecto" para armar el pivote de la media muestral es:

$$\text{Desvío} = \sqrt{\frac{\lambda}{n}}$$

### 3. La estimación (El truco para poder despejar)

Acá entra en juego el mismo dilema que charlamos hace un rato. Si ponemos esa raíz con la $\lambda$ en el denominador del pivote, nos queda una $\lambda$ arriba y una $\lambda$ adentro de una raíz abajo:

$$Z = \frac{\bar{X} - \lambda}{\sqrt{\frac{\lambda}{n}}}$$

Despejar eso a mano implica elevar todo al cuadrado y hacer la fórmula resolvente de Bhaskara. Es un infierno algebraico.

Para evitarlo, aplicamos el **Teorema de Slutsky**. Como la muestra es grande, podemos "estimar" esa varianza desconocida del denominador usando nuestros datos.

Y como dijimos al principio que en Poisson la media y la varianza son lo mismo, ¿cuál es nuestro mejor estimador para la varianza $\lambda$? **¡Nuestra media observada $\bar{X}$!**

Por lo tanto, reemplazamos la $\lambda$ del denominador por nuestra $\bar{X}$:

$$\sqrt{\frac{\bar{X}}{n}}$$

**En resumen:** Usan $\bar{X}$ en el denominador porque, exclusivamente en la distribución de Poisson, el promedio de tu muestra es numéricamente la mejor estimación que tenés para la varianza. Todo ese denominador ($\sqrt{\bar{X}/n}$) es simplemente el desvío estándar estimado de tu promedio.





# Por que puedo reemplazar la varianza?

**¡Exactamente! Entendiste la regla de oro de los intervalos asintóticos.**

Esa es la conclusión perfecta. Cuando el tamaño de tu muestra ($n$) es "lo suficientemente grande" (por convención, la mayoría de los profesores aceptan $n \geqslant 30$), la estadística te da permiso legal para hacer ese reemplazo exclusivamente en el denominador.

El justificativo teórico detrás de esto es la combinación de la **Ley de los Grandes Números** y el **Teorema de Slutsky**. Estos teoremas garantizan que cuando $n$ es gigante, tu estimador de la varianza se parece tanto, pero tanto a la varianza real, que podés intercambiarlos sin que la curva de la distribución Normal se deforme.

Fijate que es exactamente el mismo "truco" que aplicamos en los últimos tres ejercicios de la guía:

- **En Proporciones (los artículos defectuosos y los votos):** La varianza real era $p(1-p)$. Como no teníamos la $p$ real pero el $n$ era grande (200 y 100), metimos sin culpa nuestro estimador $\hat{p}(1-\hat{p})$ adentro de la raíz.
    
- **En Poisson (las partículas):** La varianza real era $\lambda$. Como el $n$ era enorme (14400), metimos nuestra media muestral $\bar{X}$ adentro de la raíz.
    
- **En cualquier otra distribución (Media general):** La varianza real es $\sigma^2$. Si no la conocés pero tenés un $n$ grande, la reemplazás por la varianza de tu muestra ($S^2$) y usás la Normal en vez de la t de Student.
    

¡Si lograste ver ese patrón, ya tenés dominada la lógica principal de todos los intervalos de confianza asintóticos!




¡Le diste en el clavo! Exactamente, **tiene que haber coherencia total entre el numerador y el denominador**.

No podés mezclar un estimador con otro porque estarías midiendo manzanas con la regla de medir peras. El denominador no es una fórmula suelta, es literalmente **el desvío estándar de lo que sea que hayas puesto en el numerador**.

Aquí te muestro cómo funciona esa regla de coherencia dependiendo de si elegís trabajar con la sumatoria o con el promedio:

### 1. Si decidís trabajar con la Sumatoria ($S$)

- **Numerador:** Ponés la distancia de la sumatoria a su media teórica: $S - n\lambda$.
    
- **Denominador (La regla):** Tenés que usar obligatoriamente la varianza estimada **de la sumatoria**. Sabemos que la varianza teórica de $S$ es $n\lambda$. Como no tenés $\lambda$, el mejor estimador para $n\lambda$ es tu propia suma observada $S$.
    
- **Pivote resultante:**
    
    $$Z = \frac{S - n\lambda}{\sqrt{S}}$$
    

### 2. Si decidís trabajar con el Promedio ($\bar{X}$)

- **Numerador:** Ponés la distancia del promedio a su media teórica: $\bar{X} - \lambda$.
    
- **Denominador (La regla):** Tenés que usar obligatoriamente la varianza estimada **del promedio**. Sabemos que la varianza teórica de $\bar{X}$ es $\lambda/n$. Como no tenés $\lambda$, usás tu promedio observado $\bar{X}$.
    
- **Pivote resultante:**
    
    $$Z = \frac{\bar{X} - \lambda}{\sqrt{\bar{X}/n}}$$
    

### En conclusión

No es que usás "cualquier" estimador. Usás el estimador que le corresponde al estadístico con el que decidiste armar la fórmula.

Si armás el numerador con $S$, abajo va la raíz de $S$. Si armás el numerador con $\bar{X}$, abajo va la raíz de $\bar{X}/n$.

Ambos caminos son matemáticamente perfectos y te van a llevar al mismo intervalo exacto, pero no podés cruzarlos en el medio.


![[Pasted image 20260728023834.png]]


Acá tenés la resolución del ejercicio 11.14 de la imagen **image_32e06a.png**.

Como el enunciado pide explícitamente un nivel **asintótico**, vamos a aplicar exactamente el mismo método de la sumatoria y la aproximación Normal que usamos en el ejercicio de las partículas, manteniendo la regla de coherencia entre nuestro numerador y denominador.

_(Pequeño comentario teórico: En la vida real, un estadístico dudaría en usar una aproximación Normal con solo 7 terremotos observados, pero como el examen te da la orden directa de usar el método "asintótico", avanzamos con total seguridad por este camino)._

### 1. Definición de la Variable y la Sumatoria

Definimos $X_i$ como el número de terremotos en el año $i$. Sabemos que es un proceso de Poisson: $X_i \sim \mathcal{P}(\lambda)$.

El tiempo de observación es $n = 200$ años. Nuestra sumatoria total de terremotos observados es:

$$S = \sum_{i=1}^{200} X_i = 7$$

Por el Teorema Central del Límite, aproximamos la distribución de la suma a una Normal:

$$S \sim \mathcal{N}(n\lambda, n\lambda)$$

### 2. Construcción del Pivote Unilateral

Al igual que en el ejercicio 11.13, para poder despejar la $\lambda$ linealmente, estimamos la varianza desconocida del denominador usando nuestra propia sumatoria observada $S$ (Teorema de Slutsky).

El pivote nos queda:

$$Z = \frac{S - n\lambda}{\sqrt{S}} \sim \mathcal{N}(0, 1)$$

El enunciado nos pide una **cota inferior** con nivel asintótico de **$0.95$**. Al ser de un solo lado, todo el riesgo del $5\%$ ($\alpha = 0.05$) va a una sola cola.

Buscamos en la tabla Normal el valor crítico que deja un $0.95$ de área a su izquierda ($z_{0.95}$):

- **Valor crítico:** $1.645$
    

Como queremos una cota inferior para el parámetro (queremos llegar a $\lambda \geqslant \dots$), forzamos al pivote a ser menor o igual al valor crítico:

$$P\left( \frac{S - n\lambda}{\sqrt{S}} \leqslant 1.645 \right) = 0.95$$

### 3. Despeje de la Cota Inferior

El despeje es idéntico a los que venimos practicando:

Pasamos multiplicando la raíz (el desvío estimado):

$$S - n\lambda \leqslant 1.645 \cdot \sqrt{S}$$

Restamos $S$ en ambos lados y multiplicamos por $-1$ (¡recordá que esto da vuelta el signo de la inecuación!):

$$n\lambda \geqslant S - 1.645 \cdot \sqrt{S}$$

Dividimos todo por $n$ para despejar nuestra incógnita $\lambda$:

$$\lambda \geqslant \frac{S - 1.645 \cdot \sqrt{S}}{n}$$

### 4. Cálculos Finales

Tenemos nuestros datos extraídos del enunciado:

- $n = 200$
    
- $S = 7$
    

Calculamos la raíz de nuestra sumatoria:

$$\sqrt{7} \approx 2.6457$$

Calculamos el margen de error del numerador:

$$1.645 \cdot 2.6457 \approx 4.3522$$

Reemplazamos todo en nuestra fórmula final:

$$\lambda \geqslant \frac{7 - 4.3522}{200}$$

$$\lambda \geqslant \frac{2.6478}{200}$$

$$\lambda \geqslant 0.013239$$

**Conclusión final:**

En base a la información muestral y con un nivel asintótico del **$95\%$**, la cota inferior para la intensidad del proceso sísmico es **$\lambda \geqslant 0.0132$** terremotos por año.






![[Pasted image 20260728024109.png]]



Acá tenés la resolución del ejercicio 11.15 de la imagen **image_32dcaa.png**.

Este ejercicio es una genialidad teórica porque te hace calcular la misma situación desde dos perspectivas distintas de un proceso de Poisson para demostrarte que **llegan al mismo resultado algebraico y numérico**.

Vamos a desglosarlo parte por parte, manteniendo la coherencia de nuestro método.

### Parte (a): El enfoque Poisson (Tiempo fijo, Eventos aleatorios)

En esta primera parte, el investigador fija su cronómetro en $10$ segundos y cuenta cuántas partículas salen. El tiempo es una constante y la cantidad de emisiones es la variable aleatoria.

**1. Definición de la Sumatoria**

Como vimos en los ejercicios anteriores, dividimos la observación en $n = 10$ intervalos de 1 segundo.

Nuestra variable $S$ es el total de emisiones en esos 10 segundos:

$$S \sim \mathcal{P}(n\lambda)$$

Por Teorema Central del Límite, aproximamos a la Normal:

$$S \sim \mathcal{N}(n\lambda, n\lambda)$$

**2. Construcción del Pivote y Despeje**

Aplicamos exactamente el mismo pivote asintótico con la varianza estimada por Slutsky (reemplazando el desvío teórico $\sqrt{n\lambda}$ por nuestro dato $\sqrt{S}$):

$$Z = \frac{S - n\lambda}{\sqrt{S}} \sim \mathcal{N}(0, 1)$$

Para un nivel de confianza del **$95\%$** (bilateral), el valor crítico en la tabla Normal es $z = 1.96$.

El despeje es el que ya conocemos de memoria:

$$-1.96 \leqslant \frac{S - n\lambda}{\sqrt{S}} \leqslant 1.96$$

$$S - 1.96 \cdot \sqrt{S} \leqslant n\lambda \leqslant S + 1.96 \cdot \sqrt{S}$$

$$\frac{S - 1.96 \cdot \sqrt{S}}{n} \leqslant \lambda \leqslant \frac{S + 1.96 \cdot \sqrt{S}}{n}$$

**3. Cálculos Finales (a)**

Tenemos los datos: $n = 10$ y $S = 4$.

- Raíz de $S$: $\sqrt{4} = 2$
    
- Margen de error: $1.96 \cdot 2 = 3.92$
    

Reemplazamos en la fórmula:

- **Límite Inferior:** $\frac{4 - 3.92}{10} = \frac{0.08}{10} = 0.008$
    
- **Límite Superior:** $\frac{4 + 3.92}{10} = \frac{7.92}{10} = 0.792$
    

**Respuesta (a):** El intervalo de confianza asintótico al $95\%$ para $\lambda$ es **$[0.008, 0.792]$**.

### Parte (b): El enfoque Exponencial/Gamma (Eventos fijos, Tiempo aleatorio)

Acá cambia totalmente la lógica del experimento. El investigador decide esperar hasta ver exactamente $r = 4$ emisiones, sin importar cuánto tarde. Ahora los eventos son una constante y el tiempo que tarda es la variable aleatoria.

**1. Definición de la Variable**

El tiempo que pasa entre emisión y emisión tiene una distribución Exponencial $\mathcal{E}(\lambda)$.

El tiempo total hasta observar la emisión número $r$ lo llamamos $T_r$, y es la suma de $r$ variables Exponenciales. Esa suma tiene una distribución Gamma:

$$T_r \sim \Gamma(r, \lambda)$$

Sabemos por teoría que $E(T_r) = \frac{r}{\lambda}$ y $V(T_r) = \frac{r}{\lambda^2}$.

**2. Construcción del Pivote (¡Acá está la magia!)**

Como $r=4$, podemos usar el Teorema Central del Límite para aproximar $T_r$ a una Normal (el enunciado nos fuerza a hacerlo al pedir nivel "asintótico").

$$T_r \sim \mathcal{N}\left(\frac{r}{\lambda}, \frac{r}{\lambda^2}\right)$$

Armamos el pivote tipificando (restamos la esperanza y dividimos por el desvío teórico $\frac{\sqrt{r}}{\lambda}$):

$$Z = \frac{T_r - \frac{r}{\lambda}}{\frac{\sqrt{r}}{\lambda}} \sim \mathcal{N}(0, 1)$$

Si multiplicamos el numerador y el denominador por $\lambda$ para "limpiar" las fracciones, nos queda un pivote hermoso donde la $\lambda$ no está en el denominador, **por lo que no necesitamos usar el Teorema de Slutsky ni inventar estimadores**:

$$Z = \frac{\lambda T_r - r}{\sqrt{r}} \sim \mathcal{N}(0, 1)$$

**3. Despeje**

Usamos el mismo valor crítico $1.96$:

$$-1.96 \leqslant \frac{\lambda T_r - r}{\sqrt{r}} \leqslant 1.96$$

Pasamos la raíz multiplicando:

$$-1.96 \cdot \sqrt{r} \leqslant \lambda T_r - r \leqslant 1.96 \cdot \sqrt{r}$$

Sumamos $r$ en todos lados:

$$r - 1.96 \cdot \sqrt{r} \leqslant \lambda T_r \leqslant r + 1.96 \cdot \sqrt{r}$$

Pasamos el tiempo observado $T_r$ dividiendo:

$$\frac{r - 1.96 \cdot \sqrt{r}}{T_r} \leqslant \lambda \leqslant \frac{r + 1.96 \cdot \sqrt{r}}{T_r}$$

**4. Cálculos Finales (b)**

Fijate qué maravilla matemática nos quedó. Los datos ahora son: $r = 4$ eventos fijos, y el tiempo aleatorio resultó ser $T_r = 10$.

Al reemplazar, los números son idénticos a los del inciso anterior, solo que intercambiaron posiciones:

- $\sqrt{r} = \sqrt{4} = 2$
    
- Margen: $1.96 \cdot 2 = 3.92$
    
- **Límite Inferior:** $\frac{4 - 3.92}{10} = 0.008$
    
- **Límite Superior:** $\frac{4 + 3.92}{10} = 0.792$
    

**Respuesta (b):** El intervalo de confianza asintótico al $95\%$ para $\lambda$ vuelve a ser **$[0.008, 0.792]$**.

> **Conclusión del ejercicio:** No importa si estructurás tu experimento midiendo cantidad de eventos en un tiempo fijo (Poisson) o midiendo el tiempo transcurrido para una cantidad fija de eventos (Gamma), si los números observados coinciden, el intervalo de confianza asintótico que respalda a $\lambda$ es exactamente el mismo.