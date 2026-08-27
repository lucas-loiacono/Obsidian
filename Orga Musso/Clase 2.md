![[Pasted image 20260825070057.png]]

**¡Exactamente!** Lo entendiste a la perfección.

  

Lo que nosotros llamamos un "número normal" en nuestro día a día es, en términos técnicos, un número expresado en **sistema decimal o base 10**.

  

Desglosando lo que acabás de decir:

  

- **"Por cómo está escrito":** Tal cual. Al estar en base 10, usamos 10 símbolos permitidos (0, 1, 2, 3, 4, 5, 6, 7, 8 y 9) y los ubicamos en distintas posiciones (unidades, decenas, centenas, etc.) para darle un peso a cada uno.
    
      
    
- **"Puede ser cualquier número":** Es la clave de todo. Usando esos 10 símbolos y moviéndolos de posición, podés representar **absolutamente cualquier magnitud que exista en el universo**. Podés escribir números enteros positivos, fracciones, decimales larguísimos, y números negativos (agregándole el símbolo `-` adelante, ya que nosotros sí podemos escribir ese símbolo, a diferencia de la memoria de la PC).
    
      
    

Le decimos "normal" pura y exclusivamente por costumbre biológica y cultural, pero es fundamental que en Organización del Computador tengas en mente que, matemáticamente, el sistema decimal es solo un idioma más. ¡Para tu computadora, el número "normal" es el binario!


![[Pasted image 20260825070121.png]]

![[Pasted image 20260825070151.png]]

Tomemos como ejemplo el número **107,25** en nuestro sistema decimal tradicional y veamos qué valor toma cada una de esas letras:

- $N$ **(Número válido):** Sería el número completo que estamos analizando, es decir, **107,25**.
    
- $b$ **(Base del sistema):** Es **10**, porque estamos en el sistema decimal y tenemos 10 símbolos permitidos para usar (del 0 al 9).
    
- $n$ **(Dígitos de la parte entera):** Vale **3**, porque la parte entera del número ("107") tiene exactamente tres dígitos.
    
- $,$ **(Coma fraccionaria):** Es, literalmente, la coma que separa el 107 del 25.
    
- $k$ **(Dígitos de la parte decimal):** Vale **2**, porque la parte después de la coma ("25") tiene exactamente dos dígitos.
    
- $d_i$ **(Símbolo en una posición):** Representa a cada dígito individual, donde la "i" indica su posición respecto a la coma (empezando a contar desde 0 hacia la izquierda, y en negativo hacia la derecha). En nuestro ejemplo:
    
    - $d_2$ es **1** (posición de las centenas)
        
    - $d_1$ es **0** (posición de las decenas)
        
    - $d_0$ es **7** (posición de las unidades)
        
    - $d_{-1}$ es **2** (primer decimal, décimas)
        
    - $d_{-2}$ es **5** (segundo decimal, centésimas)
        

El Teorema Fundamental de la Numeración básicamente usa todos estos elementos para decir que el valor total de $N$ se arma multiplicando cada dígito ($d_i$) por la base ($b$) elevada a su posición ($i$), y sumando todo.

En este caso: **107,25** = ($1 \times 10^2$) + ($0 \times 10^1$) + ($7 \times 10^0$) + ($2 \times 10^{-1}$) + ($5 \times 10^{-2}$)


![[Pasted image 20260825070207.png]]

Esta diapositiva es, ni más ni menos, la **fórmula matemática formal** de lo que acabamos de hacer en el ejemplo del 107,25. Te muestra de forma genérica cómo se construye un número en cualquier base.

Vamos a desglosar lo que estás viendo en la imagen `image_134c95.png`:

### 1. La Sumatoria (El símbolo $\Sigma$)

Esa especie de "E" gigante es el símbolo de sumatoria. La expresión:

$$\sum_{i=-k}^{n} d_i b^i$$

Es la forma matemática de decir: _"Empezá desde la posición del último decimal ($-k$) y andá sumando el valor de cada dígito multiplicado por su peso ($d_i \times b^i$), subiendo de posición hasta llegar al primer dígito de la parte entera ($n$)"_.

### 2. El desglose de la fórmula (Lo que está marcado en rojo y azul)

La diapositiva expande esa sumatoria para que veas todos los términos separados, dividiéndolos claramente por la coma:

- **Parte Entera (Corchete Rojo):**
    
    $$d_n b^n + \dots + d_1 b^1 + d_0 b^0$$
    
    Son todas las posiciones desde la coma hacia la izquierda. Acá los exponentes de la base ($b$) siempre son positivos o cero. El término $d_0 b^0$ es siempre la unidad (porque cualquier base elevada a la 0 da 1).
    
- **Parte Fraccionaria (Corchete Azul):**
    
    $$d_{-1} b^{-1} + \dots + d_{-k} b^{-k}$$
    
    Son todas las posiciones desde la coma hacia la derecha. Acá los exponentes de la base son negativos. Un exponente negativo es lo mismo que dividir (por ejemplo, $10^{-1}$ es $1/10$ o 0,1), por eso representan fracciones o decimales.
    

### 3. El texto del final

El párrafo de abajo te está adelantando la utilidad práctica de este teorema en Organización del Computador: te dice que si vos tenés un número que ya conocés (por ejemplo, en nuestro sistema decimal), podés usar esta lógica matemática a la inversa para **descubrir cómo se escribe en otra base** (como en binario para la PC).

Básicamente, averiguar cómo se escribe un número en otra base es jugar a descubrir cuáles son esos "coeficientes" ($d_i$) que, multiplicados por las potencias de la nueva base ($b$), te terminan sumando tu número original.



![[Pasted image 20260825070314.png]]



Esta diapositiva te da el "manual de instrucciones" o el algoritmo paso a paso para **convertir un número que está en decimal (base 10) a cualquier otra base** (por ejemplo, a binario o hexadecimal).

Como el método es distinto para lo que está a la izquierda de la coma y lo que está a la derecha, te lo separa en dos reglas. Vamos a explicarlo con un ejemplo práctico: supongamos que queremos convertir el número **13,375** (base 10) a **binario** (base 2).

### 1. Obtención de la Parte Entera (Divisiones sucesivas)

La regla dice que para convertir la parte entera (el **13**), tenés que dividir ese número por la base de destino (en nuestro ejemplo, 2) una y otra vez hasta que ya no puedas dividir más (cuando el cociente sea 0). **Los restos de esas divisiones van a ser tus nuevos dígitos ($d_i$).**

**Ejemplo con el 13:**

- $13 / 2 = 6$ y sobra **1** $\rightarrow$ (Este es tu primer dígito de derecha a izquierda, $d_0$)
    
- $6 / 2 = 3$ y sobra **0** $\rightarrow$ ($d_1$)
    
- $3 / 2 = 1$ y sobra **1** $\rightarrow$ ($d_2$)
    
- $1 / 2 = 0$ y sobra **1** $\rightarrow$ (Este es tu último dígito, $d_3$)
    

Para armar el número final, los restos se leen de abajo hacia arriba (o del último al primero). Entonces, el 13 en decimal es **1101** en binario.

### 2. Obtención de la Parte Fraccionaria (Multiplicaciones sucesivas)

Para lo que está después de la coma (el **0,375**), el proceso es inverso. En lugar de dividir, tenés que **multiplicar** por la base de destino (2). Lo que te quede a la izquierda de la coma en cada resultado será tu nuevo dígito, y seguís multiplicando solo la parte decimal restante hasta que llegues a 0 (o hasta que consigas la precisión deseada, ya que a veces es infinito).

**Ejemplo con el 0,375:**

- $0,375 \times 2 = \mathbf{0},75$ $\rightarrow$ Nos guardamos el **0** (primer decimal, $d_{-1}$) y seguimos multiplicando el resto (0,75).
    
- $0,75 \times 2 = \mathbf{1},50$ $\rightarrow$ Nos guardamos el **1** ($d_{-2}$) y seguimos multiplicando el resto (0,50).
    
- $0,50 \times 2 = \mathbf{1},00$ $\rightarrow$ Nos guardamos el **1** ($d_{-3}$). Como la parte decimal llegó a 0, terminamos.
    

En este caso, los números se leen en el orden normal (de arriba hacia abajo). Entonces, el 0,375 decimal es **011** en binario.

**Resultado final:**

Uniendo ambas partes, demostramos cómo aplicar las definiciones de tu diapositiva: el número decimal **13,375** equivale al **1101,011** en binario.


![[Pasted image 20260825070325.png]]


### 1. De Cualquier Base a Base 10 (Primer párrafo)

Te dice que si tenés un número "raro" (por ejemplo, en binario, octal o hexadecimal) y querés saber qué número es para nosotros en la vida real (base 10), simplemente tenés que resolver la cuenta. Agarrás cada dígito, lo multiplicás por su peso (la base elevada a su posición) y sumás todo.

**Ejemplo rápido:** Pasar el binario **101,1** a decimal (base 10).

- $(1 \times 2^2) + (0 \times 2^1) + (1 \times 2^0) + (1 \times 2^{-1})$
    
- $4 + 0 + 1 + 0,5 = \mathbf{5,5}$ en base 10.
    

### 2. De Base 10 a Cualquier Base (Segundo párrafo)

Es exactamente lo que vimos en la diapositiva anterior. Si tenés el número en base 10 y querés pasarlo a otra base, tu objetivo es "desarmarlo" (descomponerlo) para encontrar cuáles son esos dígitos de la nueva base. ¿Cómo encontrás esos coeficientes? Usando las divisiones (para la parte entera) y las multiplicaciones (para la parte fraccionaria) que vimos antes.

### La Fórmula (Verde y Roja)

La ecuación que ves ahí abajo es exactamente el mismo **Teorema Fundamental de la Numeración** que viste hace dos diapositivas, pero le cambiaron un poco los nombres a las letras para que sea más visual:

- En lugar de $d$, usan **$M$** para los dígitos (coeficientes).
    
- En lugar de $b$, usan **$B$** para la base.
    
- En lugar de $k$, usan **$m$** para la cantidad de decimales.
    

El **color verde** representa la suma de los pesos de la **Parte Entera (PE)**, donde los exponentes de $B$ van desde $n$ bajando hasta llegar a $0$.

El **color rojo** representa la suma de los pesos de la **Parte Fraccionaria (PF)**, donde los exponentes de $B$ son negativos (desde $-1$ bajando hasta $-m$).

El resultado de sumar todo ese choclazo matemático te da el número expresado en base 10 (eso significa el $N^\circ\vert{}_{10}$ del final). Básicamente, esta diapositiva formaliza matemáticamente por qué funcionan las cuentas que hacemos para convertir de una base a otra.



El punto 2 dice que si tenés un número en base 10, lo podés representar en otra base encontrando su descomposición. Supongamos que tenemos el número decimal **25,5** (Base 10) y queremos desarmarlo para representarlo en **binario (Base $B = 2$)**.

Si hacemos las divisiones y multiplicaciones que vimos en la imagen anterior, descubrimos que los dígitos (los coeficientes **$M$**) que necesitamos son **11001,1**.

Vamos a meter esos coeficientes $M$ y la base $B=2$ en la fórmula de la diapositiva para comprobar cómo se reconstruye el 25,5:

**Parte Entera (Lo verde en tu diapositiva - exponentes de $n$ hasta $0$):**

Agarramos la parte entera del binario (**11001**) y multiplicamos cada dígito por la base 2 elevada a su posición:

- $M_4 \cdot B^4 \rightarrow \mathbf{1} \times 2^4 = 16$
    
- $M_3 \cdot B^3 \rightarrow \mathbf{1} \times 2^3 = 8$
    
- $M_2 \cdot B^2 \rightarrow \mathbf{0} \times 2^2 = 0$
    
- $M_1 \cdot B^1 \rightarrow \mathbf{0} \times 2^1 = 0$
    
- $M_0 \cdot B^0 \rightarrow \mathbf{1} \times 2^0 = 1$
    
    _(Si sumás los resultados de la parte verde: $16 + 8 + 0 + 0 + 1 = \mathbf{25}$)_
    

**Parte Fraccionaria (Lo rojo en tu diapositiva - exponentes negativos):**

Agarramos la parte decimal del binario (**,1**) y la multiplicamos por la base con exponente negativo:

- $M_{-1} \cdot B^{-1} \rightarrow \mathbf{1} \times 2^{-1} = 0,5$
    
    _(Acá solo tenemos un término en rojo, que equivale a **0,5**)_
    

**El resultado final (la ecuación completa de la diapositiva):**

Si escribimos toda la suma de corrido, queda exactamente la estructura que te muestra el profesor:

$$(\mathbf{1} \times 2^4) + (\mathbf{1} \times 2^3) + (\mathbf{0} \times 2^2) + (\mathbf{0} \times 2^1) + (\mathbf{1} \times 2^0) + (\mathbf{1} \times 2^{-1}) = 25,5\vert{}_{10}$$

En resumen: el punto 2 te demuestra que convertir de base 10 a otra base es simplemente el desafío de encontrar esos coeficientes específicos ($M$) que hacen que la suma matemática funcione.




Asumo que te referís a ver el **paso a paso completo** de cómo obtuve ese número binario (`11001,1`) a partir del **25,5** decimal, haciendo las divisiones y multiplicaciones que se explican en la teoría.

  

Acá tenés el desarrollo para encontrar esos coeficientes $M$:

  

### 1. Descomposición de la Parte Entera (25)

Aplicamos divisiones sucesivas por la base a la que queremos llegar ($B = 2$):

  

- $25 \div 2 = 12$ y sobra **1** $\rightarrow$ Este es tu primer dígito de derecha a izquierda ($M_0$)
    
      
    
- $12 \div 2 = 6$ y sobra **0** $\rightarrow$ ($M_1$)
    
      
    
- $6 \div 2 = 3$ y sobra **0** $\rightarrow$ ($M_2$)
    
      
    
- $3 \div 2 = 1$ y sobra **1** $\rightarrow$ ($M_3$)
    
      
    
- $1 \div 2 = 0$ y sobra **1** $\rightarrow$ Al llegar al cociente cero, este es tu último dígito ($M_4$)
    
      
    

Para armar el número, los restos se leen desde el último que calculaste hasta el primero (de abajo hacia arriba). Entonces, el 25 decimal equivale a **11001** en binario.

  

### 2. Descomposición de la Parte Fraccionaria (0,5)

Aplicamos multiplicaciones sucesivas por la base ($B = 2$) solo a la parte decimal:

  

- $0,5 \times 2 = \mathbf{1},0$ $\rightarrow$ Nos guardamos el número que queda a la izquierda de la coma, que es el **1** ($M_{-1}$).
    
      
    

Como la parte que quedó a la derecha de la coma llegó a cero (es decir, ya no hay más decimales para seguir multiplicando), el proceso termina en este primer paso.

  

### Resultado Final

Al unir la parte entera obtenida en el Paso 1 con la parte fraccionaria obtenida en el Paso 2, comprobamos de dónde salió el coeficiente completo:

**$25,5\vert{}_{10} = 11001,1\vert{}_2$**

  

¿Querés que hagamos este mismo procedimiento de conversión completo con algún otro número para seguir practicando?




![[Pasted image 20260825070344.png]]

![[Pasted image 20260825070355.png]]



Esta diapositiva, la `image_143997.png`, responde a una pregunta muy práctica en la arquitectura de computadoras: **"Si tengo un número que ocupa cierta cantidad de dígitos en una base, ¿cuánto espacio (cuántos dígitos) voy a necesitar para guardar ese mismo número en otra base?"**

Por ejemplo, si tenés un número decimal grande y querés saber cuántos bits vas a necesitar para guardarlo en la memoria de la PC, esta es la matemática que te da la respuesta.

Vamos a desglosar el razonamiento matemático que hace el profesor:

### 1. El Concepto Central (La Inecuación)

Para que no se pierda información al pasar de una Base 1 ($B_1$) a una Base 2 ($B_2$), la cantidad máxima de combinaciones que podés armar en la nueva base tiene que ser **mayor o igual** a la cantidad de combinaciones de la base original.

Eso se expresa con esta inecuación:

$$B_2^{n_2} \ge B_1^{n_1}$$

- $B_1$: Es tu base original.
    
- $n_1$: Son los dígitos que usás en esa base original.
    
- $B_2$: Es tu nueva base (la de destino).
    
- $n_2$: Es tu incógnita, la cantidad de dígitos que vas a necesitar en la nueva base.
    

### 2. Despejando la incógnita con Logaritmos

Como la incógnita ($n_2$) está en el exponente, la única forma matemática de "bajarla" para poder calcularla es aplicando logaritmos en ambos lados de la inecuación.

El profesor aplica logaritmo en base $B_2$:

$$\log_{B_2}(B_2^{n_2}) \ge \log_{B_2}(B_1^{n_1})$$

Por propiedades de los logaritmos, el exponente pasa multiplicando adelante, y como el logaritmo de una base sobre sí misma da 1 ($\log_{B_2}(B_2) = 1$), la fórmula se simplifica a:

$$n_2 \ge n_1 \cdot \log_{B_2}(B_1)$$

### 3. El problema de la calculadora (Cambio de Base)

La parte final de la diapositiva aborda un problema práctico: las calculadoras normales no calculan logaritmos en cualquier base, solo calculan logaritmo natural o logaritmo en base 10 (decimal).

Por lo tanto, hace una demostración matemática (el bloque del medio con la $y$ y la $x$) para aplicar la regla de "Cambio de Base". Esto transforma ese logaritmo raro en una división de logaritmos decimales que sí podés poner en la calculadora.

### La Fórmula Final

La conclusión de toda esta diapositiva es la fórmula de la última línea, que es la que vas a usar en la práctica:

$$n_2 \ge n_1 \cdot \frac{\log(B_1)}{\log(B_2)}$$

### Un ejemplo práctico para entenderlo mejor:

Supongamos que tenés números decimales de **3 dígitos** (van del 000 al 999). Querés saber **cuántos bits (dígitos binarios)** necesitás como mínimo para representar cualquiera de esos números.

- $B_1 = 10$ (Base decimal)
    
- $n_1 = 3$ (Cantidad de dígitos decimales)
    
- $B_2 = 2$ (Base binaria)
    

Aplicamos la fórmula final:

$$n_2 \ge 3 \cdot \frac{\log(10)}{\log(2)}$$

$$n_2 \ge 3 \cdot \frac{1}{0,30103}$$

$$n_2 \ge 3 \cdot 3,3219$$

$$n_2 \ge 9,96$$

Como no podés tener "9,96 bits", siempre redondeás hacia arriba. Esto significa que **necesitás al menos 10 bits** para poder representar cualquier número decimal de 3 dígitos en binario. (Y tiene sentido, porque con 9 bits llegás hasta el 511, pero con 10 bits llegás hasta el 1023, cubriendo así el 999).


![[Pasted image 20260825070406.png]]

![[Pasted image 20260825070418.png]]

![[Pasted image 20260825070458.png]]

![[Pasted image 20260825070510.png]]

![[Pasted image 20260825070521.png]]

![[Pasted image 20260825070532.png]]



Esta diapositiva (`image_21e43b.png`) muestra un ejemplo práctico de cómo convertir la parte decimal de un número de base 10 a base 2, pero introduce un problema muy común en la informática: **¿Qué pasa cuando la cuenta no termina nunca?**

Vamos a dividir la explicación en las dos partes que muestra la imagen.

### 1. El cálculo paso a paso

El ejemplo quiere pasar el número decimal **0,35** a binario. Como vimos antes, para la parte fraccionaria se multiplica por la base destino (2) y nos vamos guardando lo que queda a la izquierda de la coma:

1. $0,35 \times 2 = \mathbf{0},7$ $\rightarrow$ Nos guardamos el **0**. Nos queda $0,7$ para seguir.
    
2. $0,7 \times 2 = \mathbf{1},4$ $\rightarrow$ Nos guardamos el **1**. Nos queda $0,4$ para seguir.
    
3. $0,4 \times 2 = \mathbf{0},8$ $\rightarrow$ Nos guardamos el **0**. Nos queda $0,8$ para seguir.
    

Hasta acá, el número binario armado es **0,010...**

Si siguieras multiplicando ($0,8 \times 2 = \mathbf{1},6$; luego $0,6 \times 2 = \mathbf{1},2$; luego $0,2 \times 2 = \mathbf{0},4$; y de nuevo $0,4 \times 2 = \mathbf{0},8$), entrarías en un bucle infinito. La parte fraccionaria jamás va a llegar a ser "cero exacto".

### 2. El Truncamiento y el Error (El texto de abajo)

Como la memoria de una computadora es limitada (no tenés infinitos bits para guardar infinitos decimales), en algún momento vas a tener que decir "basta, corto acá" (truncar el número). Al cortar la cuenta, **estás perdiendo información y generando un error de precisión**, porque el número binario que armaste no es exactamente igual al 0,35 original.

El profesor te da una fórmula para calcular **cuál es el error máximo** que estás cometiendo al cortar ahí. La fórmula es:

$$Error < B^{-K}$$

- $B$: Es la base a la que estás convirtiendo (en este caso, 2).
    
- $K$: Es la cantidad de multiplicaciones que hiciste (o cuántos "lugares después de la coma" calculaste).
    

En el ejemplo de la diapositiva, como solo hicieron 3 multiplicaciones (es decir, $K = 3$), el error de precisión que tiene ese número es menor a:

$$Error < 2^{-3}$$

$$2^{-3} = \frac{1}{2^3} = \frac{1}{8} = 0,125$$

**¿Qué significa esto en la práctica?**

Significa que el binario `0,010` que acabamos de armar, si lo pasáramos de nuevo a decimal para comprobarlo, nos daría $0,25$. La diferencia (el error) entre el $0,35$ que queríamos guardar y el $0,25$ real que logramos armar es de $0,10$. Como predijo la fórmula del profesor, el error que cometimos ($0,10$) efectivamente es menor al límite máximo de $0,125$.

Si quisieras que el error fuera más chico (tener un número más preciso), tendrías que hacer más multiplicaciones y usar más bits (aumentar el valor de $K$).


![[Pasted image 20260825070542.png]]




Esta diapositiva marca un punto de inflexión en el tema. Hasta ahora, todas las conversiones que venías viendo asumían que los números eran positivos. Esta imagen introduce el problema de **cómo hace la computadora para representar números negativos**.

  

Como la PC solo entiende de ceros y unos, no le podés poner un símbolo de menos (`-`) adelante al número. Hay que usar esos mismos ceros y unos para indicar el signo. La diapositiva te presenta las dos convenciones principales teóricas para lograr esto:

  

### 1. Valor Absoluto + Bit de Signo (Signo y Magnitud)

Es el método más humano e intuitivo. Consiste en agarrar tu número binario normal (el valor absoluto) y **agregarle un bit extra a la izquierda del todo** (lo que se llama la posición "más significativa").

  

- Si ese bit extra es un **`0`**, la PC entiende que el número es **positivo (+)**.
    
      
    
- Si ese bit extra es un **`1`**, la PC entiende que el número es **negativo (-)**.
    
      
    

**Ejemplo rápido (asumiendo que usamos 4 bits en total):**

  

- El número 5 en binario es `101`.
    
      
    
- Para guardar el **+5**, le agregás un 0 adelante: **`0`**`101`.
    
      
    
- Para guardar el **-5**, le agregás un 1 adelante: **`1`**`101`.
    
      
    

### 2. Complemento al Módulo + Bit de Signo ($C_M$)

Aunque el primer método es fácil de entender para nosotros, a la hora de diseñar el procesador de una computadora, hacer sumas y restas con el método de "Bit de Signo" es muy ineficiente y complicado a nivel hardware.

  

Por eso se inventó el **Complemento al Módulo** (que en el sistema binario vas a terminar conociendo en la práctica como _Complemento a 2_). Es un truco matemático espectacular para representar números negativos de forma tal que **restar sea exactamente lo mismo que sumar un número negativo**.

  

La definición que da el profesor es la regla matemática general: el complemento de un número $N$ (que se escribe $C_M(N)$) es la cantidad exacta que le tenés que sumar a tu número original para alcanzar el límite máximo de combinaciones que permite esa base con esa cantidad de dígitos.

  

Por eso te muestra la fórmula:

  

$$N\vert{}_B + C_M(N)\vert{}_B = B^n\vert{}_B$$

- **$N$**: Es tu número original.
    
      
    
- **$C_M(N)$**: Es el "complemento" de tu número (la versión negativa de tu número en este sistema).
    
      
    
- **$B^n$**: Es el total de combinaciones posibles (Base elevada a la cantidad de dígitos $n$).
    
      
    

_En criollo:_ El complemento es lo que le falta a tu número para "dar toda la vuelta" al cuentakilómetros y volver a quedar en cero dentro de la memoria de la computadora.




¡Excelente idea! Vamos a poner en práctica esa fórmula paso a paso para que veas cómo ocurre la "magia" en la memoria de una computadora.

  

Para que el ejemplo funcione, tenemos que definir un límite físico, una "cantidad de casilleros" fijos. Vamos a suponer que nuestra memoria trabaja con **$n = 4$ bits**.

  

**El objetivo:** Queremos averiguar cuál es el código binario para guardar el número **-3** utilizando este método $C_M$ (que en binario se llama Complemento a 2).

  

### Paso 1: Identificar los elementos de la fórmula

Nuestra fórmula es:

  

$$N\vert{}_B + C_M(N)\vert{}_B = B^n\vert{}_B$$

- **$N$ (El número original en positivo):** Queremos el negativo de 3, así que nuestro número base es 3. En binario de 4 bits se escribe **0011**.
    
      
    
- **$B$ (La base):** Es 2 (sistema binario).
    
      
    
- **$n$ (Cantidad de dígitos):** Es 4.
    
      
    
- **$B^n$ (El límite máximo):** $2^4 = 16$. Si pasamos el 16 a binario, se escribe con un 1 seguido de cuatro ceros: **10000**.
    
      
    

### Paso 2: Aplicar la matemática

Para que sea súper intuitivo, vamos a resolver la fórmula pensando en nuestros números decimales:

  

$$3 + C_M(3) = 16$$

Despejamos el complemento (que será la versión negativa de nuestro número):

  

$$C_M(3) = 16 - 3$$

$$C_M(3) = \mathbf{13}$$

### Paso 3: El resultado en binario

Ahora simplemente escribimos ese 13 en nuestro sistema binario de 4 bits. El 13 decimal equivale a **1101**.

¡Listo! Para tu computadora, si está usando el sistema de Complemento al Módulo, leer **1101** significa exactamente **-3**.

  

### La prueba de fuego (El efecto "Cuentakilómetros")

Acá es donde ves por qué los ingenieros que diseñan procesadores aman este sistema. Te dije antes que el objetivo era lograr que la computadora pudiera "restar" haciendo simplemente una suma, y que el número diera la vuelta completa para volver a cero.

  

En la vida real, $3 + (-3) = 0$. Veamos qué pasa si la computadora suma los dos números binarios que acabamos de usar:

  

`0011`    _(Este es el +3)_

  

- `1101`    _(Este es el -3 que calculamos)_
    
    ----------
    
     **`10000`**
    
      
    

El resultado de la suma binaria da **10000**.

Pero acá viene el truco físico: **nuestra computadora solo tiene espacio para 4 bits**. Como el resultado tiene 5 bits, el "1" que sobra a la izquierda literalmente no entra en la memoria. Se rebalsa, se ignora y se pierde (a este fenómeno se lo llama _overflow_ o desbordamiento).

  

Al borrarse ese quinto bit, ¿qué le quedó guardado a la computadora en sus 4 casilleros disponibles?

Exactamente: **`0000`**.

  

El cuentakilómetros dio la vuelta perfecta. La máquina logró resolver una resta ($3 - 3 = 0$) utilizando únicamente el hardware diseñado para sumar, todo gracias a este truco matemático de los complementos.


![[Pasted image 20260825070718.png]]


Esta diapositiva (`image_22507b.png`) te presenta una **tercera forma** de representar números negativos en la computadora. Matemáticamente se la llama **Complemento al Módulo menos uno ($C_M-1$)**, pero en la práctica y en el sistema binario se la conoce famosamente como **Complemento a 1**.

Viene a plantear una alternativa al método de la diapositiva anterior ($C_M$ o Complemento a 2) y destaca por un "truco" que a los circuitos electrónicos les encanta. Vamos a desarmarlo:

### 1. La Matemática detrás del nombre

La diapositiva empieza mostrándote una tabla de 3 bits.

Primero te muestra cómo se representan los números en el sistema $C_M$ (van del -4 al +3). Luego, aplica la regla matemática que le da nombre a este nuevo método: literalmente le **resta una unidad** a la magnitud de los complementos.

Si te fijás, el binario `100` que antes valía -4, ahora en la fila de $C_M-1$ vale -3. El `101` que valía -3, ahora vale -2, y así sucesivamente.

### 2. La Magia Práctica (Inversión de bits)

El último párrafo es la verdadera lección de la diapositiva. Te dice que si dejás de lado la resta matemática y simplemente mirás cómo quedaron formados los números, vas a notar un patrón espectacular: **para conseguir la versión negativa de cualquier número, simplemente tenés que invertir todos sus bits (cambiar los 0 por 1, y los 1 por 0).**

**Ejemplo en la tabla:**

- Buscá el **+2**. Su código binario es `010`.
    
- Si invertimos todos sus números (donde hay 0 ponemos 1, y viceversa), nos queda `101`.
    
- Si mirás qué valor tiene el `101` en la fila de $C_M-1$, vas a ver que es exactamente el **-2**.
    

### 3. ¿Por qué es importante esto?

Como dice la última oración del profesor: _"Esta operación suele ser más sencilla de realizar en los circuitos digitales"_.

A nivel físico/hardware, construir un circuito que haga sumas y restas complejas es caro y lento. Pero construir una compuerta lógica que simplemente invierta la corriente (si entra señal que no salga, y si no entra que salga) es facilísimo y súper rápido.

### El pequeño gran problema (El doble cero)

Si prestás mucha atención a la tabla, vas a notar algo raro que pasa con este sistema $C_M-1$:

- Tenés el binario `000` que equivale al **+0**.
    
- Si invertís sus bits te queda `111`, que equivale al **-0**.
    

Este sistema crea **dos representaciones distintas para el número cero**. En matemática el cero no tiene signo, y para una computadora, tener que lidiar con dos "ceros" distintos a la hora de hacer cálculos es un dolor de cabeza. Por este motivo, aunque el Complemento a 1 ($C_M-1$) es facilísimo de calcular, las computadoras modernas terminan usando el sistema anterior ($C_M$ o Complemento a 2) para trabajar.



¡Dale! Vamos a armar ese cuadro comparativo.

Para que quede bien claro, vamos a usar **4 bits** de memoria y vamos a ver cómo se escriben el **+6** y el **-6** en los tres sistemas que vimos en tus diapositivas.

Lo primero que tenés que saber es que el número **+6** en binario puro (sin signo) es `110`. Como tenemos 4 bits, lo rellenamos con un cero a la izquierda, quedando **`0110`**.

Fijate lo que pasa en cada sistema:

| **Sistema de Representación**     | **Cómo se escribe el +6** | **Cómo se escribe el -6** |
| --------------------------------- | ------------------------- | ------------------------- |
| **Valor Absoluto + Bit de Signo** | `0110`                    | `1110`                    |
| **Complemento a 1 ($C_M-1$)**     | `0110`                    | `1001`                    |
| **Complemento a 2 ($C_M$)**       | `0110`                    | `1010`                    |

### ¿De dónde salió el -6 en cada caso?

La clave para entender esta tabla es mirar qué le hicimos al `0110` original para convertirlo en negativo:

1. **En Valor Absoluto + Bit de Signo:**
    
    Simplemente agarramos el bit de más a la izquierda (el que marca el signo) y lo cambiamos de `0` (positivo) a `1` (negativo). El resto del número (`110`) quedó intacto.
    
2. **En Complemento a 1 ($C_M-1$):**
    
    Aplicamos el "truco de la inversión" que vimos en la última diapositiva. Agarramos el `0110` e invertimos absolutamente todos sus bits: los ceros pasaron a unos, y los unos a ceros. Por eso quedó `1001`.
    
3. **En Complemento a 2 ($C_M$):**
    
    Este es el método que usan las computadoras hoy en día. Para calcularlo rápido en la práctica, se hace el Complemento a 1 (invertir los bits) y **se le suma un 1 matemático al final**.
    
    Si al `1001` de arriba le sumamos `1` bit, nos da `1010`.
    

**La regla de oro:** Notá que los números positivos (`0110`) **se escriben exactamente igual en los tres sistemas**. La diferencia entre estos métodos existe única y exclusivamente en cómo manejan los números negativos.

¿Quedó un poco más claro cómo conviven los tres sistemas con este ejemplo?


![[Pasted image 20260825070729.png]]

![[Pasted image 20260825070742.png]]

![[Pasted image 20260825070757.png]]

![[Pasted image 20260825070812.png]]

![[Pasted image 20260825070823.png]]

![[Pasted image 20260826210051.png]]

![[Pasted image 20260826210101.png]]

![[Pasted image 20260826210113.png]]

![[Pasted image 20260826210124.png]]

![[Pasted image 20260826210135.png]]

![[Pasted image 20260826210152.png]]

![[Pasted image 20260826210204.png]]

![[Pasted image 20260826210213.png]]

![[Pasted image 20260826210224.png]]

![[Pasted image 20260826210234.png]]

![[Pasted image 20260826210243.png]]