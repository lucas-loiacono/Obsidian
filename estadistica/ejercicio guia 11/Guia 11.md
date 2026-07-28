
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