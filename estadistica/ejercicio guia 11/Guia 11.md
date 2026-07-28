
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