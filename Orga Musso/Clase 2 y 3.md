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



**¡Exactamente! Lo resumiste a la perfección.**

  

Ese 0,125 no es el error exacto que estás cometiendo, sino tu **"peor escenario posible"** (o límite de riesgo, como muy bien lo llamaste). Te garantiza matemáticamente que, si cortás la cuenta en 3 multiplicaciones ($K = 3$), es absolutamente imposible que le pifies al número original por más de 0,125.

  

Y tu segunda deducción es brillante: **a mayor cantidad de números calculados (mayor $K$), el margen de error se desploma rapidísimo.**

  

Vamos a comprobar tu teoría matemáticamente para que veas qué rápido se achica el error:

  

- **Con $K = 4$ (4 decimales):**
    
    El error máximo garantizado por la fórmula baja a:
    
      
    
    $$2^{-4} = \frac{1}{16} = 0,0625$$
    
- **Con $K = 8$ (8 decimales):**
    
      
    
    $$2^{-8} = \frac{1}{256} \approx 0,0039$$
    
- **Con $K = 16$ (16 decimales):**
    
      
    
    $$2^{-16} = \frac{1}{65536} \approx 0,000015$$
    

Fijate que con solo calcular 16 lugares después de la coma, el margen de error ya es prácticamente invisible (estamos hablando de millonésimas).

  

### El impacto en el mundo real

Esto que acabás de deducir es el corazón de cómo las computadoras modernas (incluyendo tu PC) manejan los números con coma.

  

Como los bits son limitados y ocupan espacio en la memoria, los creadores de lenguajes de programación y procesadores tienen que elegir un equilibrio:

  

1. **Velocidad vs. Precisión:** Si deciden usar poquitos bits para guardar la parte fraccionaria (un $K$ chico), el programa es súper ligero y rápido, pero en cálculos muy finos (como mandar un cohete al espacio o hacer transacciones bancarias) ese pequeño error de truncamiento se puede ir acumulando y generar un desastre.
    
      
    
2. **El estándar de hoy:** Para evitar eso, la mayoría de los lenguajes de programación (como C o Python) usan formatos gigantes de memoria para los decimales (llamados de "Doble Precisión" o _Double_ de 64 bits), donde el valor de $K$ es de 52. ¡Imaginate lo microscópico que es el error con un $K = 52$!
    
      
    

En conclusión, la cazaste al vuelo. Es exactamente una balanza entre cuántos recursos querés gastar y cuánta precisión estás dispuesto a perder.

  

¿Se entiende bien la lógica o querés que probemos calcular un decimal más en ese mismo ejemplo para ver cómo se acerca al 0,35 real?


![[Pasted image 20260825070542.png]]

	001 -> +1
	+111 -> -1
	1000 con 3 bits puedo representar 8 en binario, ya que es 2^n, ese es el modulo en binomial, si yo paso 1000 a decimal es el 8


como representar numeros con signo


hay varios tipos de representacion:

valor absoluto + bit de signo, le agrego un 0 o un 1 si es positivo o negativo

complemento al modulo +bit de signo

$$N\vert{}_B + C_M(N)\vert{}_B = B^n\vert{}_B$$



$$N\vert{}_B $$
este es un numero dado una base, si yo le sumo mi complemento de ese numero osea mi: 

$$C_M(N)\vert{}_B$$

llego a la cantidad de resultados que puedo representar con esa base y la cantidad de numeros que tengo, osea mi 


$$B^n\vert{}_B$$





(complemento al modulo -1) + bit de signo

donde 
(complemento al modulo -1) + 1= complemento al modulo

   001   = +1
+
   111   = -1             -> le tengo que sumar su negativo, ya que es el modulo
= 1000

con 3 bits, puedo representar 8 números, esto es por

$$B^n\vert{}_B$$
que es 2^3 = 8 que en binario es 1000, es la cantidad de números que podes representar con 3 dígitos en base 2




En la arquitectura de las computadoras, el "complemento" de un número es literalmente la forma en la que la máquina escribe su versión negativa.

Si vos agarrás el código binario del **+5** y le calculás el complemento a 2 (invertir los bits y sumarle 1), el resultado que obtenés es el código binario exacto del **-5**.

Y funciona para los dos lados: si le calculás el complemento al -5, volvés a obtener el +5. Es el método que usa el hardware para cambiarle el signo a cualquier número.

osea el complemento al modulo es mi numero pero en el otro signo


**Complemento a 1 ($C_M-1$)**

- **Mecanismo:** Se calcula únicamente invirtiendo todos los bits del número binario original. Los `0` se transforman en `1`, y los `1` se transforman en `0`.
    
- **Ventaja física:** Es la operación más sencilla y rápida de construir en un circuito electrónico, ya que solo requiere pasar la señal por compuertas lógicas inversoras (NOT).
    
- **Desventaja (El doble cero):** Al invertir los bits, se crean dos representaciones distintas para el número cero: un $+0$ (ej: `000`) y un $-0$ (ej: `111`). Esto entorpece las validaciones matemáticas internas del procesador.
    

**Complemento a 2 ($C_M$)**

- **Mecanismo:** Se ejecuta en dos pasos. Primero se aplica el Complemento a 1 (invertir todos los bits) y, al resultado obtenido, se le suma un `1` en la columna de la extrema derecha.
    
- **Ventaja física:** Elimina la redundancia del doble cero, dejando una única combinación universal para el cero absoluto (`000...`). Por este motivo, es el estándar que usan todos los procesadores modernos.
    
- **Lógica subyacente:** El número negativo calculado es matemáticamente la distancia exacta que falta para alcanzar el total de combinaciones del sistema (el Módulo). Esto garantiza que al sumar un número con su negativo ($n + (-n)$), el sistema genere un desborde perfecto por la izquierda que se descarta, reiniciando los casilleros útiles a cero puro sin necesidad de circuitos de resta.


para conseguir el numero negativo con complemento al modulo -1 lo que hago es

.invierto los 1 y los 0 y le sumo 1 bit





Básicamente, la historia de la arquitectura de computadoras pasó por estos tres sistemas:

- **Signo y Magnitud:** Es el método que dedujiste vos recién (usar el primer bit para el signo y dejar el número original intacto). Es el más fácil de leer para la cabeza humana, pero pésimo para procesar cuentas. Curiosamente, aunque ya no se usa para enteros, **es la lógica exacta que usa la Norma IEEE 754** (Punto Flotante) que vimos al principio, donde el bit de signo está totalmente separado del resto de la fórmula.
    
- **Complemento a 1 ($C_M-1$):** El primer intento de los ingenieros por lograr que la máquina pueda restar sumando (invertir los bits). Era rapidísimo a nivel electrónico, pero el fallo técnico de tener un $+0$ y un $-0$ lo terminó dejando en el pasado.
    
- **Complemento al Módulo ($C_M$ / Complemento a 2):** El campeón indiscutido. Es el estándar absoluto que usa tu computadora y cualquier procesador moderno para manejar los números enteros (como el tipo de dato `int` cuando programás). Costó un paso extra (sumarle 1), pero es el único que logra que toda la matemática binaria fluya sola por los circuitos y que el $n + (-n) = 0$ se cumpla a la perfección forzando el reinicio de los casilleros.



como mi idioma principal para esto es complemento al modulo +bit de signo lo que hago es 

(complemento al modulo -1) + 1 = complemento al modulo


Para obtener el negativo de un número bajo el sistema actual (Complemento a 2 / Complemento al Módulo), existen efectivamente dos caminos lógicos paralelos.

**Camino Matemático (El concepto teórico)**

1. Se calcula el Módulo del sistema (el total de combinaciones posibles elevando $2^n$, donde $n$ es la cantidad de casilleros físicos).
    
2. Se ejecuta la resta de ese Módulo menos el número positivo original ($M - n$).
    

**Camino Mecánico (La receta del hardware)**

1. Se aplica primero la regla del Complemento a 1, que consiste en invertir todos los ceros y unos de forma directa.
    
2. Al resultado invertido, se le suma una unidad (`1`) en la columna de la extrema **derecha**.















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








Esta diapositiva te está presentando al "hermano menor" del método que vimos recién. El que calculamos antes era el **Complemento al Módulo ($C_M$)**, también conocido en la práctica como Complemento a 2.

Este nuevo método de la imagen se llama **Complemento al Módulo menos uno ($C_M - 1$)**, que vas a escuchar habitualmente como **Complemento a 1**.

Vamos a desarmar la diapositiva en dos partes clave para que la tabla no te maree:

**1. El atajo principal (El párrafo final de la imagen)**

Olvidate un segundo de las restas y enfocáte en el último párrafo, porque ahí está el verdadero motivo por el que existe este método. Los ingenieros se dieron cuenta de que calcular el $C_M$ con la fórmula matemática que usamos antes llevaba algunas fracciones de segundo extra en el hardware.

En cambio, hacer el $C_M-1$ es absurdamente fácil para los circuitos de una máquina: **para conseguir el negativo de un número, solo tenés que agarrar su versión positiva e invertir absolutamente todos sus ceros y unos**.

Comprobalo mirando la tabla:

- El $+3$ en binario es `011`.
    
- Si invertís todos sus bits, te queda `100`.
    
- Si mirás la última fila de la tabla ($C_M-1$), vas a ver que el `100` corresponde exactamente al **$-3$**. Conseguiste el negativo al instante y sin hacer ninguna cuenta matemática.
    

**2. Qué significa la tabla del medio**

La tabla te está mostrando visualmente qué pasó con el sistema viejo ($C_M$) para llegar al nuevo. Al "restarle uno" a la lógica matemática, todo el bloque de los números negativos se desplazó un lugar hacia la derecha.

- En el sistema viejo que calculaste antes, el código `100` se usaba para representar al $-4$.
    
- En este nuevo sistema, el código `100` se corre y pasa a representar al $-3$.
    

**El "defecto" del sistema (y por qué ves un -0)**

Si mirás la tabla con muchísima atención, vas a notar la consecuencia de haber desplazado todos los números negativos un lugar: **aparecen dos ceros distintos**.

- Tenés un **$+0$** lógico (`000`).
    
- Tenés un bizarro **$-0$** (`111`), que nace justamente de invertir todos los bits del +0.
    

Tener dos formas distintas de escribir el cero es un dolor de cabeza enorme para diseñar el procesador de la computadora. Por eso, aunque este método del Complemento a 1 era facilísimo para los circuitos porque solo invertía bits, la industria lo terminó descartando.

Hoy en día, tu computadora (y casi todos los ejercicios de parcial) usan el método del **Complemento a 2 ($C_M$)**, porque soluciona el problema del doble cero y aprovecha ese espacio extra para poder contar un número negativo más (el -4 que ves en la primera fila).

¿Queda más claro ahora cómo funciona la inversión de bits en esta convención?






¡Entiendo perfecto por qué te hace ruido al mirar la tabla! Pero la respuesta es que **no conviven al mismo tiempo**. El código `100` nunca va a significar dos cosas a la vez en una misma máquina.

Lo que la diapositiva te está mostrando son dos "idiomas" o convenciones totalmente distintas para leer exactamente el mismo código binario.

Pensalo como la palabra "pie": en inglés significa una tarta dulce, y en español significa una parte del cuerpo. El significado cambia por completo dependiendo del idioma que estés hablando. Acá pasa lo mismo:

- Si tu computadora está fabricada para usar el sistema **$C_M$** (Complemento a 2, el de la primera fila), cuando el procesador lea `100` va a entender que es un **-4**.
    
- Si tu computadora está fabricada para usar el sistema **$C_M-1$** (Complemento a 1, el de la última fila), cuando el procesador lea `100` va a entender que es un **-3**.
    

Una computadora real opera utilizando **solo uno** de estos dos sistemas. Por lo tanto, la máquina jamás duda sobre qué número es.

El profesor simplemente los apiló uno arriba del otro en la diapositiva para que puedas comparar de forma visual cómo un mismo patrón de ceros y unos (`100`) cambia de valor matemático cuando los ingenieros deciden cambiar la regla del juego.














La regla de **invertir directamente los ceros y unos** pertenece exclusivamente al **$C_M-1$** (Complemento al Módulo menos uno, que en la práctica se llama Complemento a 1).

Como viste en la diapositiva, si tenés el $+3$ (`011`) y simplemente invertís todos sus bits (`100`), ya conseguiste automáticamente el código del $-3$ para el sistema $C_M-1$. No hay que hacer absolutamente nada más.

Para que veas cómo se relacionan los dos métodos a la hora de hacer un ejercicio en papel, acá tenés el "truco definitivo" que usan todos los programadores. Si a vos te dan un número positivo y te piden pasarlo a negativo, los pasos son estos:

- **Para conseguir el $C_M-1$ (Complemento a 1):** Invertís todos los ceros y unos. (Ejemplo: el $+3$ es `011` $\rightarrow$ invertido te da **`100`**).
    
- **Para conseguir el $C_M$ (Complemento a 2):** Hacés la inversión de bits (el paso anterior) y a ese resultado **le sumás 1**. (Ejemplo: invertiste el `011` y te dio `100` $\rightarrow$ le sumás 1 y te da **`101`**).
    

Así te ahorrás tener que usar la fórmula matemática con restas y potencias que vimos antes. Invertir y sumar 1 es el camino más rápido para calcular el $C_M$ en cualquier examen.


![[Pasted image 20260825070729.png]]

![[Pasted image 20260825070742.png]]

![[Pasted image 20260825070757.png]]

![[Pasted image 20260825070812.png]]

![[Pasted image 20260825070823.png]]




yo aca para encontrar el -25 lo que tendria que hacer es pasar el 25 con complemento a -1 y lo consigo rapido




Esta diapositiva es el "gran final" de la historia de los sistemas binarios. Te muestra en la práctica **por qué la industria informática eligió el sistema $C_M$ (Complemento a 2) como el ganador indiscutido**, descartando al resto.

La idea central que te quiere transmitir el profesor es que **este sistema permite que la computadora no tenga que saber restar**. Para la máquina, restar 25 es exactamente lo mismo que "sumar un -25". Al usar solo circuitos sumadores, el procesador es mucho más barato y eficiente.

Vamos a analizar el primer ejemplo de la izquierda (`28 - 25`), que es donde ocurre la verdadera magia matemática:

1. **La suma:** El profesor agarra el código binario del 28 positivo y le suma directamente el código binario del 25 negativo.
    
2. **El desborde (Carry):** Si aplicás las reglas de sumar que vimos en la diapositiva anterior y sumás columna por columna, el resultado final que te da es **`100000011`**.
    
3. **El truco del $C_M$:** Si contás los dígitos de ese resultado, vas a notar que tiene **9 bits**, pero tu sistema era de 8 bits. Ese `1` extra que quedó colgando a la izquierda del todo se llama "carry" de desborde. La gran ventaja del sistema $C_M$ es que te permite agarrar ese `1` sobrante, **tirarlo a la basura e ignorarlo por completo**.
    
4. **El resultado perfecto:** Al tachar ese uno de la izquierda, te queda el código `00000011`, ¡que es exactamente el número 3 positivo! La cuenta da perfecto.
    

### El resumen de ventajas y desventajas (Texto inferior)

El texto de abajo simplemente pone en palabras por qué este sistema es mejor que el $C_{M-1}$ que vimos un par de diapositivas atrás:

- **Ventaja 1 (Única representación para el cero):** ¿Te acordás del bizarro "-0" (`11111111`) que nos generaba problemas en el sistema anterior? Acá eso no pasa. El cero es de puros ceros y no hay confusión posible.
    
- **Ventaja 2 (No es necesario sumar el carry):** Es justamente lo que hicimos recién con el `1` que sobró. Lo ignoramos y listo. Si estuvieras usando el sistema viejo ($C_{M-1}$), los circuitos tendrían que agarrar ese `1` sobrante, llevarlo hasta la otra punta del número y volver a sumarlo, perdiendo tiempo de procesamiento.
    
- **El único inconveniente:** Para armar el número negativo original te lleva un pasito matemático más. En el sistema viejo solo invertías ceros y unos; acá estás obligado a invertir los bits y **sumarle 1** al final.


![[Pasted image 20260826210051.png]]

Pensá en las **Banderas (Flags)** como si fueran las luces del tablero de un auto. Cada vez que el procesador termina de hacer una cuenta matemática (como las sumas que estuviste practicando recién), prende o apaga de forma automática una serie de "lucecitas" de advertencia para resumir qué pasó con ese resultado.

Estas luces son fundamentales porque la computadora las usa para tomar decisiones lógicas súper rápidas (por ejemplo: "si la luz de cero se prende, terminá el programa").

Acá te traduzco qué significa cada luz del tablero que muestra la diapositiva:

- **Carry (Acarreo):** ¡A esta ya la conocés! Es exactamente ese `1` que desbordaba a la izquierda del todo en la diapositiva anterior y que terminábamos descartando. La bandera se prende para avisar "che, me sobró un bit que no entró en el registro".
    
- **Overflow (Desbordamiento):** Es la luz de alerta de catástrofe matemática. Se prende exclusivamente cuando sumás dos números del mismo signo (ejemplo: dos positivos muy grandes) y por falta de espacio el resultado te da con el signo opuesto (negativo). Significa que el número que quedó guardado es incoherente y no sirve.
    
- **Zero (Cero):** Súper simple. Si el resultado final de toda tu cuenta dio `00000000`, esta bandera se prende en `1` para confirmarlo.
    
- **Negative (Negativo):** Mira directamente el último bit de la izquierda (el bit de signo) del resultado. Si quedó en `1`, esta bandera se prende para reportar que el resultado es negativo.
    
- **Half-Carry (Acarreo de primer nibble):** Es como un Carry interno. Se prende si cuando estabas sumando columna por columna, pasaste un "me llevo uno" desde la primera mitad del número hacia la segunda mitad (del bit 4 al bit 5).
    
- **Paridad (P):** Literalmente se pone a contar cuántos `1` sueltos quedaron prendidos en tu resultado final para avisar si esa cantidad es par o impar. Es una herramienta que se usa mucho a nivel de hardware para detectar si un dato se corrompió al enviarlo por una red.
    

Las banderas le ahorran al procesador tener que analizar el número binario completo de nuevo cada vez que necesita saber si una cuenta dio negativo, si dio cero o si hubo un error de espacio.







¡Ojo acá! Se te están mezclando dos momentos distintos de la suma. Vamos a separar las aguas para que quede súper claro.

  

Primero: el acarreo interno ("me llevo uno") **siempre viaja hacia la izquierda**, no hacia la derecha. Pensá en la suma que hacés en papel desde que sos chico: si sumás la columna de la derecha (las unidades) y te pasás de 9, te llevás el 1 hacia la izquierda (a la columna de las decenas). En binario es exactamente igual; los unos viajan como una cascada hacia las columnas de la izquierda.

  

Lo de "eliminar un número" ocurre exclusivamente **al final de toda la cuenta**, cuando te chocás contra la pared física de la memoria.

  

Imaginate la memoria de la PC como una cubetera de hielo que tiene exactamente 8 huecos.

  

1. Venís sumando columna por columna, pasando los acarreos hacia la izquierda lo más bien.
    
      
    
2. Llegás a sumar la última columna de todas (el bit número 8, el de la extrema izquierda).
    
      
    
3. Si justo esa última suma genera un acarreo extra ("me llevo uno"), ese `1` debería ocupar un noveno casillero.
    
      
    
4. Como tu cubetera solo tiene 8 huecos, **ese noveno bit se cae por el borde y no entra en el resultado principal.**
    
      
    

Acá es donde entra en juego la **Bandera de Carry** (la luz del tablero). Ese `1` que se cayó por el borde izquierdo no desaparece en la nada, sino que va a chocar contra la luz de Carry y la prende, avisándole al procesador: _"Che, me sobró un bit que no entró en los 8 casilleros"_.

  

La genialidad matemática del sistema **$C_M$ (Complemento a 2)** que vimos en el ejemplo de `28 - 25`, es que está diseñado a propósito para que ese bit que se cae por la izquierda no te importe. Al "eliminarlo" o ignorarlo, los 8 bits que sí lograron quedarse adentro de la cubetera forman el resultado perfecto de tu resta.





Son dos alertas totalmente independientes que vigilan problemas distintos. Aunque las dos avisan que el número "se pasó de un límite", lo hacen mirando cosas separadas.

  

**Carry (Falta de espacio físico)**

Vigila si la cuenta generó un noveno bit que se cayó de tu registro de 8 casilleros. Como vimos antes, si estás usando números con signo en el sistema $C_M$, que se prenda esta luz es normal y ese bit que se cae por el borde simplemente se ignora.

  

**Overflow (Incoherencia lógica de signo)**

Vigila exclusivamente el comportamiento del bit de signo (el primero de la izquierda). Solo se prende si sumás dos números positivos y el espacio te queda tan chico que invadís el bit de signo, haciendo que el resultado parezca negativo. También pasa al revés (sumar dos negativos y que dé positivo). Te avisa que corrompiste la regla de los signos.

  

Para demostrar que evalúan cosas separadas, mirá cómo pueden saltar de forma independiente:

  

- **Podés tener Overflow sin Carry:** Si sumás $+127$ (`01111111`) y $+2$ (`00000010`) en un sistema de 8 bits, el resultado encaja perfecto en los 8 casilleros dando `10000001`. Como no sobró ningún bit, la luz de Carry **no se prende**. Sin embargo, la máquina ahora lee ese `1` de la izquierda y asume que el resultado es negativo ($-127$). Como sumar dos positivos te dio un negativo, la luz de Overflow **sí se prende** gritando que hay un error lógico.
    
      
    
- **Podés tener Carry sin Overflow:** Si sumás $-1$ (`11111111`) y $-1$ (`11111111`), la cuenta te da `111111110`. Como tiene 9 bits, el `1` de la izquierda se cae del registro y prende la luz de **Carry**. Pero los 8 bits que se lograron quedar adentro (`11111110`) equivalen al número $-2$. Como la suma de dos negativos dio como resultado otro negativo, la lógica de signos se mantuvo intacta y la luz de Overflow **no se prende**.
    
      
    

El Overflow no es un subcaso del Carry; son dos circuitos de vigilancia que tu procesador revisa en paralelo cada vez que hace una cuenta.






Tu intuición matemática dio en el clavo. De hecho, a nivel de los circuitos físicos del procesador, el Overflow se calcula observando **exclusivamente** el comportamiento de los acarreos alrededor del último casillero.

  

El secreto está en que el procesador compara dos movimientos en el último paso de la suma (la columna del bit de signo):

  

1. El acarreo que **ENTRA** a esa columna (el "me llevo uno" interno que viaja desde la derecha).
    
      
    
2. El acarreo que **SALE** de esa columna (el bit que se cae al vacío y prende la bandera de Carry general).
    
      
    

La regla de oro de la computadora es esta: **Si el acarreo que entra es distinto al acarreo que sale, se produce un Overflow.**

  

Mirá cómo esos acarreos generan los problemas lógicos de los que hablábamos antes:

  

- **Entra un `1` pero sale un `0`:** Venías sumando dos números positivos muy grandes. El "me llevo uno" interno invadió la columna del signo, transformándolo a la fuerza en un `1` (haciendo que parezca negativo). Como la cuenta terminó ahí, no sobró ningún bit para caerse afuera. **Resultado:** Se prende el Overflow (por la invasión interna) pero no el Carry.
    
      
    
- **Entra un `0` pero sale un `1`:** Sumaste dos números negativos muy grandes. La columna del signo original tenía la cuenta `1 + 1`. Eso da como resultado `0` (haciendo que el número parezca positivo), y genera un `1` extra que se cae del registro. **Resultado:** Se prende el Overflow y también el Carry.
    
      
    
- **Entran y salen iguales (`1` y `1`, o `0` y `0`):** La lógica de signos fluyó sin interrupciones y el número mantuvo su coherencia. **Resultado:** No hay Overflow.
    
      
    

Así que tu conclusión es 100% correcta. El Overflow no es magia; es literalmente el síntoma físico de que un acarreo interno chocó contra el bit de signo y arruinó la coherencia matemática de la suma.





El Half-Carry (o acarreo de primer _nibble_) es un "me llevo uno" que cruza exactamente por la frontera central de tu registro.

  

Imaginate que agarrás tu registro de 8 bits y le trazás una línea vertical por el medio, dividiéndolo en dos bloques cerrados de 4 bits: una mitad derecha (el _nibble_ inferior) y una mitad izquierda (el _nibble_ superior).

  

La luz del Half-Carry se prende **exclusivamente** si, al sumar la cuarta columna (el último casillero de la mitad derecha), se genera un acarreo que salta esa pared divisoria y aterriza en la quinta columna (el primer casillero de la mitad izquierda).

  

Para visualizarlo, sumemos `0000 1000` (8) y `0000 1000` (8):

  

- Las primeras tres columnas de la derecha suman puros ceros.
    
      
    
- Llegás a la cuarta columna y sumás: `1 + 1 = 10`.
    
      
    
- Anotás el `0` abajo y te pasás un `1` de acarreo hacia la quinta columna.
    
      
    
- Ese cruce de frontera entre el cuarto y el quinto bit es el que hace saltar la bandera de Half-Carry.
    
      
    

**El motivo de su existencia**

Mientras el Carry general cuida el límite físico de la memoria y el Overflow vigila la coherencia de los signos, el Half-Carry tiene un propósito hiperespecífico: el formato BCD (Decimal Codificado en Binario).

  

En ciertos procesos (como los relojes digitales o calculadoras financieras), la computadora no usa binario puro, sino que guarda cada dígito decimal del 0 al 9 en pequeños paquetes de 4 bits. Si una suma genera un acarreo que rompe ese paquete de 4 bits e invade el paquete de al lado, la luz de Half-Carry le avisa al procesador que los paquetes se desfasaron y que tiene que inyectar una corrección matemática extra para arreglar el número.



Solo con que **cruce la frontera** ya cuenta. Lo que pase de ahí en adelante no le importa en lo más mínimo a esta bandera.

  

Volviendo a la analogía del peaje: el sensor de esta luz está instalado únicamente en la línea exacta que divide la cuarta y la quinta columna. Si el sensor detecta que un acarreo atravesó esa línea, prende la luz del Half-Carry automáticamente.

  

Si después de cruzar esa frontera el acarreo se asienta tranquilamente en la quinta columna, o si choca con otro `1` y genera un nuevo efecto dominó que viaja hacia la sexta, séptima u octava columna, es un problema que pasará a ser jurisdicción de otras banderas (como el Carry general o el Overflow).

  

El único trabajo del Half-Carry en el universo del procesador es gritar _"¡Alguien cruzó al nibble superior!"_ y dejar la luz prendida.

![[Pasted image 20260826210101.png]]


Esta diapositiva es la práctica integradora de todo lo que charlamos sobre el sistema de Complemento a 2 ($C_M$) y cómo reaccionan las "luces del tablero" (las Banderas) ante distintos escenarios.

  

El profesor te armó cuatro ejemplos distintos. Vamos a leerlos uno por uno mirando la columna de la derecha de cada cuadro, que te indica cómo quedaron las banderas al final (C=Carry, V=Overflow, N=Negativo, Z=Cero).

  

**1. Arriba a la Izquierda (La suma perfecta)**

  

- **La cuenta:** Sumás $+26$ y $+19$. El resultado entra perfecto en los 8 bits.
    
      
    
- **Las banderas:** Todo está en `0`. No sobró ningún bit (C='0'), la coherencia matemática está intacta porque positivo más positivo dio positivo (V='0'), el resultado empieza con cero así que no es negativo (N='0'), y la cuenta no dio cero (Z='0').
    
      
    

**2. Arriba a la Derecha (El Cero y el Carry descartado)**

  

- **La cuenta:** Sumás $+26$ y $-26$. Físicamente, la suma binaria genera ese noveno `1` que el profesor marcó en rojo.
    
      
    
- **Las banderas:** Como ese `1` rojo se cayó del registro de 8 bits, se prende la luz de Carry (**C='1'**). Los 8 bits que sí quedaron adentro son todos ceros, así que se prende la luz de Cero (**Z='1'**). No hay Overflow (V='0') porque sumar números de distinto signo jamás puede generar una incoherencia lógica.
    
      
    

**3. Abajo a la Izquierda (Suma de negativos)**

  

- **La cuenta:** Sumás $-19$ y $-32$. Al igual que arriba, se genera un noveno bit rojo que se cae al vacío.
    
      
    
- **Las banderas:** Ese bit caído prende el Carry (**C='1'**). El resultado final de los 8 bits empieza con un `1`, lo que indica que es negativo, así que se prende esa bandera (**N='1'**). ¡Y fijate el Overflow! Sigue apagado (V='0') porque la regla lógica se cumplió a la perfección: sumaste dos negativos y el resultado fue efectivamente negativo.
    
      
    

**4. Abajo a la Derecha (¡El desastre del Overflow!)**

  

- **La cuenta:** Acá el profesor cambió las reglas y usó registros chiquitos de solo **6 bits**. Suma $+26$ (`011010`) y $+21$ (`010101`).
    
      
    
- **El problema:** En la vida real eso da 47, pero el número máximo que entra en un sistema de 6 bits con signo es el $+31$. Físicamente, los bits no entraron y el acarreo interno invadió la columna del signo, dejando un `1` a la izquierda del todo (`101111`).
    
      
    
- **Las banderas:** Como no cayó ningún bit por el borde izquierdo, el Carry está apagado (C='0'). Pero la máquina lee ese `1` inicial y prende la luz de Negativo (**N='1'**). Como sumaste dos números positivos y mágicamente apareció un resultado negativo ($-17$), el procesador detecta la incoherencia lógica y prende la sirena de Overflow (**V='1'**), avisando que ese resultado es basura y no sirve.
    
      
    

¿Ves cómo en este último cuadro, con solo mirar que se prendió la bandera `V`, la computadora ya sabe que tiene que descartar toda esa cuenta sin siquiera entender qué números estaba sumando?



![[Pasted image 20260826210113.png]]




Esta diapositiva es literalmente el "machete" definitivo para el parcial. Viene a resumir en reglas universales todo lo que venimos deduciendo en los ejemplos anteriores con las banderas.

  

El gráfico de arriba te muestra visualmente los límites de la computadora. Los paréntesis negros de los extremos son "la pared" (la capacidad máxima de tu sistema). Adentro tenés tu zona segura de números negativos (verde) y positivos (marrón).

  

Acá te traduzco las conclusiones del texto a la lógica práctica:

  

**Reglas de oro del Overflow (Desbordamiento)**

  

- **Positivo + Positivo = Peligro:** Si estás en la burbuja marrón y sumás otro número marrón, te podés pasar de largo de la pared derecha. (Puede haber Overflow).
    
      
    
- **Negativo + Negativo = Peligro:** Si estás en la burbuja verde y sumás otro número verde, te podés caer por la pared izquierda. (Puede haber Overflow).
    
      
    
- **Positivo + Negativo = Imposible desbordar:** Si das 10 pasos para adelante y 5 para atrás, es imposible que te alejes más de tu punto de partida. Como "tiran para lados contrarios", el resultado siempre va a caer adentro de la zona segura. **Nunca** hay Overflow.
    
      
    

**Reglas de oro del Carry (Acarreo del bit extra)**

  

- **Negativo + Negativo = Siempre hay Carry:** Como estás usando el sistema $C_M$, todos los números negativos empiezan con un `1` a la izquierda. Cuando llegás a sumar la última columna, vas a hacer obligatoriamente `1 + 1`. Eso da `10`, lo que garantiza al 100% que un bit se va a caer del registro.
    
      
    
- **Positivo + Negativo dando Cero = Siempre hay Carry:** Es exactamente lo que viste en la diapositiva anterior con $+26 - 26$. Para que la matemática del complemento a 2 logre que todos los casilleros queden en cero, necesita generar una cascada de acarreos que termina empujando un `1` por el borde izquierdo.
    
      
    
- **Positivo + Positivo = Nunca hay Carry:** Como los dos números son positivos, sus bits de signo (el de la extrema izquierda) son `0`. Al sumar la última columna vas a hacer `0 + 0`. Aunque arrastres un "me llevo uno" de la columna anterior (`0 + 0 + 1 = 1`), jamás vas a lograr generar un número lo suficientemente grande como para que se caiga un bit afuera del registro.
    
      
    

En los exámenes de Organización del Computador, a veces te dan sumas gigantes y te preguntan "sin hacer la cuenta, ¿puede haber Overflow?". Con solo mirar los signos de los números que te dieron usando estas reglas, ya tenés la respuesta.



![[Pasted image 20260826210124.png]]

¡Bienvenido al mundo del **Punto Flotante**! Con esta diapositiva dejás atrás los números enteros y empezás a ver cómo hace realmente la computadora para guardar números gigantescos (como la distancia a otra galaxia) o microscópicos (como el tamaño de un átomo) sin quedarse sin memoria.

  

Vamos a dividir la imagen en dos para entender el salto lógico que da el profesor:

  

**1. El problema del modelo viejo (El dibujito de arriba)**

Los casilleros de arriba muestran cómo se guardaban los números con coma antes. Se llamaba "Punto Fijo". Era un sistema rígido donde la memoria se partía a la mitad: una cantidad fija de casilleros para la parte entera, y otra fija para la parte fraccionaria.

El problema es que si querías guardar el número `241506800` (que no tiene decimales pero es larguísimo), desperdiciabas toda la mitad de la memoria destinada a las fracciones, y capaz no te alcanzaban los casilleros de la parte entera. Era súper ineficiente.

  

**2. La solución: El Punto Flotante (La fórmula y el ejemplo)**

Para arreglar esto, los ingenieros le robaron una idea a la matemática: la **Notación Científica**.

  

La magia de esta fórmula (`+/- Mantisa x Base^exponente`) es que la coma "flota". Ya no está clavada en el medio del registro, sino que la podés mover hasta donde te convenga, y usás un exponente para recordar cuántos lugares la moviste.

  

Vamos a desarmar el ejemplo de la diapositiva paso a paso (aclaración: el profesor usa un apóstrofe `0'24` para representar la coma decimal `0,24`):

  

- **El número original:** Tenés el `241506800`. La coma imaginaria está al final del todo (a la derecha de los ceros).
    
      
    
- **Flotando la coma:** El profesor decide empujar esa coma hacia la izquierda hasta que el número quede convertido en `0,2415068` (los ceros del final ya no importan).
    
      
    
- **El exponente:** Para que `0,2415068` vuelva a ser el número gigante original, lo tenés que multiplicar por 10 (la base) elevada a la cantidad de lugares que moviste la coma. Como la moviste 9 lugares a la izquierda, el exponente es **9**.
    
      
    

**¿Qué es lo que realmente se guarda en la memoria?**

La computadora no guarda los ceros inútiles, ni la base (porque ya sabe que está trabajando en base 10 para este ejemplo, o base 2 en la vida real), ni el símbolo de multiplicar. Solo guarda tres "ingredientes" empaquetados:

  

1. **El signo:** `+` (Ocupa 1 bit).
    
      
    
2. **La mantisa:** `2415068` (Son los "dígitos significativos", el corazón del número sin ceros de relleno).
    
      
    
3. **El exponente:** `9` (Es el mapa que le dice a la computadora cuántos lugares tiene que volver a mover la coma cuando quiera leer el número original).
    
      
    

Con este truco, en vez de gastar millones de casilleros de memoria escribiendo ceros, la máquina guarda números enormes en un espacio chiquitito. En las próximas diapositivas seguro vas a ver cómo se aplica esta misma lógica pero usando Base 2.



![[Pasted image 20260826210135.png]]


Esta diapositiva te muestra la **Norma IEEE 754**, que es la regla universal que usan todas las computadoras y procesadores modernos para guardar los números de punto flotante en binario. Es la aplicación en la vida real de la fórmula matemática que viste en la diapositiva anterior.

  

En lugar de que cada fabricante invente su propio método de almacenamiento, este estándar dictamina exactamente cómo se deben repartir los "casilleros" físicos de la memoria para empaquetar los tres ingredientes: el signo, el exponente y la mantisa.

  

El estándar define dos "tamaños de caja" principales:

  

- **Simple Precisión (32 bits):** Reparte la memoria en 1 bit para el signo, 8 para el exponente y 23 para la mantisa. Cuando escribís código en C y declarás una variable tipo `float`, estás creando exactamente esta estructura de 32 bits. También es el formato rey en el mundo del gaming; cuando una placa de video renderiza los modelos 3D y las trayectorias en juegos tácticos o _shooters_, procesa casi todo usando Simple Precisión porque ofrece el equilibrio perfecto entre velocidad de cálculo y calidad visual sin saturar la memoria.
    
      
    
- **Doble Precisión (64 bits):** Duplica el tamaño total, asignando 1 bit de signo, 11 de exponente y una mantisa gigante de 52 bits. En la programación, este es el clásico tipo de dato `double`. Al tener 52 casilleros solo para la mantisa, podés retener muchísimos más "dígitos significativos", lo cual es vital si programás una base de datos financiera o un motor de físicas donde un mínimo error de redondeo te arruina todo el cálculo.
    
      
    

Finalmente, el texto de abajo te confirma que la regla para identificar si el paquete completo representa un número positivo o negativo es la convención más directa y simple posible: **`0` significa positivo y `1` significa negativo**.


![[Pasted image 20260826210152.png]]

Esta diapositiva resuelve un problema clave de los **8 bits del exponente** en el formato de Simple Precisión (la estructura física exacta que hay detrás de una variable `float` cuando programás en C).

  

El problema que plantea el profesor es el siguiente: tu exponente puede ser negativo (si querés guardar un número microscópico como $2^{-50}$) o positivo (para un número gigante). Sin embargo, ya gastaste el único "bit de signo" que tenías para definir si el número completo era positivo o negativo. ¿Cómo hacés para guardar un exponente negativo en esos 8 casilleros sin complicarte la vida con el sistema de Complemento a 2?

  

La norma IEEE 754 lo solucionó inventando el sistema de **Exceso 127** (también conocido como desplazamiento o _bias_).

  

La matemática que explica el párrafo central es súper mecánica:

  

1. Con 8 bits podés armar 256 combinaciones (del 0 al 255).
    
      
    
2. Los ingenieros agarraron el número que está justo en la mitad: el **127**.
    
      
    
3. **La regla de oro:** Al exponente real que vos necesites guardar, le vas a sumar 127, y recién ahí vas a pasar ese resultado a binario para guardarlo en la memoria.
    
      
    

Fijate cómo funciona en la lista de ejemplos:

  

- Si tu exponente real es **0**: Hacés la suma (0 + 127 = 127). El procesador guarda el binario `01111111`.
    
      
    
- Si tu exponente es recontra negativo, por ejemplo **-126**: Hacés la suma (-126 + 127 = 1). El procesador simplemente guarda un `00000001`.
    
      
    
- Si tu exponente es positivo y gigante, como **127**: Hacés la suma (127 + 127 = 254). El procesador guarda `11111110`.
    
      
    

**¿Cuál es la gran ventaja de hacer este "corrimiento"?**

Hace que el procesador sea rapidísimo para comparar qué número es más grande. Al sumarle 127 a todo, la máquina percibe que todos los exponentes son números positivos convencionales. Si tiene que comparar, sabe al instante que un `00000001` (que es el -126 real) es menor que un `01111111` (que es el 0 real), sin tener que analizar bits de signos extraños.

  

El recuadrito negro de abajo a la derecha resume el proceso a la inversa (el desempaquetado). Cuando la máquina tiene que leer de la memoria el número que guardaste, lee el exponente en binario (E) y **le resta 127** para deshacer el truco y recuperar el exponente original. Ese "1,Mantisa" que aparece en la fórmula te está spoileando el próximo gran truco de la norma: el bit implícito.



![[Pasted image 20260826210204.png]]


Esta diapositiva es el mapa completo de los límites físicos de tu computadora cuando usa el formato de Simple Precisión (los famosos 32 bits). Básicamente, te muestra qué pasa cuando intentás guardar números que se salen de los márgenes.

  

Vamos a desglosarla en las tres partes clave que te muestra:

  

**1. El límite máximo (El número más gigante posible)**

La fórmula de arriba te muestra el tope absoluto del sistema. Se logra cuando ponés todos los casilleros de la mantisa en `1` y usás el exponente máximo permitido (que es el 127 que charlamos recién).

Al pasarlo a decimal, da ese $3.4028... \times 10^{38}$. Para que te des una idea, es un número tan grande que si intentás guardar algo mayor a eso (por ejemplo, el resultado de una multiplicación bestial o ese exponente de 254 que hablábamos antes), la computadora directamente tira la toalla y caes en las zonas de los costados llamadas **Overflow** (positivo o negativo).

  

**2. La Precisión**

Ese $2^{-23}$ viene del hecho de que tenés exactamente 23 casilleros para la mantisa. Representa el "escalón" más chiquitito que la computadora puede notar entre dos números distintos. Si la diferencia entre dos números es menor a eso, para la computadora son exactamente el mismo número porque no tiene suficientes casilleros para escribir el detalle fino.

  

**3. El gráfico y el "Agujero Negro" del Underflow**

El eje horizontal es una recta numérica. Las zonas rayadas son tu **zona segura** (los números que caben perfecto en los 32 bits).

Pero lo más importante de este gráfico es el espacio en blanco que está en el medio, rodeando al cero: el **Underflow**.

  

Pensalo así: si intentás guardar un número que es microscópico, como por ejemplo la masa de un electrón (que tiene como 30 ceros después de la coma), vas a necesitar un exponente recontra negativo. Como tu límite para exponentes negativos es -126 (físicamente guardado como `00000001`), si tu número es todavía más chiquito que ese límite, te caes en la zona de Underflow.

  

Cuando hay un Underflow, el número es tan microscópicamente cercano a cero que la computadora se queda sin capacidad para representarlo y, en general, lo redondea directamente a un `0` absoluto.



![[Pasted image 20260826210213.png]]

Acá tenés el desglose exacto de las cinco filas de la tabla, explicando qué significa cada combinación física para el procesador:

  

1. **Exponente = 0 y Mantisa = 0 (El Cero absoluto):**
    
    Cuando todos los bits del exponente y de la mantisa están apagados, el sistema representa el valor matemático cero. Como el bit de signo viaja por un carril separado, la computadora puede registrar físicamente un $+0$ (`0` en el signo) y un $-0$ (`1` en el signo).
    
      
    
2. **Exponente = 0 y Mantisa = <>0 (Números no normalizados):**
    
    El exponente está vacío, pero hay al menos un bit prendido en la mantisa. Este es el "salvavidas" del procesador para poder medir números microscópicos antes de caer en el cero absoluto. Para lograrlo, la máquina hace dos excepciones: desactiva el truco del "1 implícito" (fijate que en la fórmula ahora le suma la mantisa a un **`0.`**) y clava el multiplicador fijo en el límite inferior: $(0. + \text{Mantisa}) \times 2^{-126}$.
    
      
    
3. **Exponente = 1 a 254 (Números normalizados):**
    
    Este es el escenario estándar donde ocurre el 99% de la matemática diaria de tu computadora. Se aplica la regla general: el procesador asume automáticamente que hay un "1" entero antes de la coma, y calcula el exponente real restándole el exceso 127 al código binario que encontró guardado: $(1. + \text{Mantisa}) \times 2^{\text{exp}-127}$.
    
      
    
4. **Exponente = 255 y Mantisa = 0 (Infinito):**
    
    Todos los bits del exponente están prendidos en `1`, pero la mantisa está completamente limpia. Es el código de alerta para reportar **Infinito**. Salta automáticamente si un número sufre un _overflow_ masivo (superando el límite de la zona segura) o si tu programa intenta dividir un número por cero. Dependiendo de cómo haya quedado el bit de signo, indicará $+\infty$ o $-\infty$.
    
      
    
5. **Exponente = 255 y Mantisa = <>0 (Not a Number / NaN):**
    
    El exponente está al máximo, pero la mantisa tiene datos adentro (algún bit en `1`). Es el código de error absoluto del procesador para reportar una aberración matemática que no tiene solución. Salta si le pedís a la computadora calcular cosas imposibles, como hacer $0 \div 0$, infinito menos infinito, o la raíz cuadrada de un número negativo.







¡Pausa acá! Se te mezclaron los conceptos, pero es súper normal porque la norma hace un juego de ida y vuelta. Vamos a desenredarlo en dos partes para que quede impecable.

  

**Primero: El `1.` de la fórmula no tiene NADA que ver con el bit de signo.**

Tu bit de signo (el que te dice si el número final es positivo o negativo) vive en su propio casillero individual al principio de todo y no participa de esta fórmula.

  

Ese `1.` aparece por cómo funciona la notación científica en binario. En decimal, la notación científica siempre deja un número del 1 al 9 antes de la coma (ej: $3,52 \times 10^5$). En binario, como solo existen el 0 y el 1, un número normalizado **siempre pero siempre** va a empezar con un `1` antes de la coma (ej: $1,0110 \times 2^5$). Como ese "1" es una fija universal, los ingenieros decidieron no guardarlo en la memoria para ahorrar espacio. La fórmula se lo inyecta de prepo (`1. + Mantisa`) para reconstruir el número.

  

**Segundo: La confusión de sumar o restar 127**

El secreto para entender esto es separar el momento de **GUARDAR** un número del momento de **LEERLO**.

  

1. **Cuando querés GUARDAR (Pasar del papel a la memoria):** Acá aplicás tu regla de **sumar**.
    
    Si tu exponente matemático real en el papel es **5**, la computadora no puede guardar un 5 así nomás. Hace $5 + 127 = \mathbf{132}$. Ese `132` (en binario `10000100`) es lo que se guarda físicamente en los 8 casilleros de la memoria.
    
      
    
2. **Cuando querés LEER (La fórmula de la diapositiva):** La fórmula que pasaste es el manual de instrucciones que usa la computadora para **desempaquetar** lo que está en la memoria.
    
    La variable `exp` en esa fórmula representa el número físico que la máquina encontró en los 8 casilleros. En nuestro ejemplo, la compu lee un `132`. Para saber cuál era tu exponente original, tiene que deshacer el truco, por eso **resta**. Hace $132 - 127 = \mathbf{5}$. ¡Y ahí recuperó tu exponente real!
    
      
    

Entonces, respondiendo a tu pregunta: si tuvieras un exponente matemático de `-127` en papel, caés en la zona de números hiper microscópicos (Underflow, la fila de arriba de la tabla) y se activan otras reglas. Pero para los números normales (del -126 al 127), el proceso es simple: **le sumás 127 para meterlo en la memoria, y la fórmula le resta 127 para sacarlo.**





![[Pasted image 20260826210224.png]]


Esta diapositiva te presenta al hermano mayor de lo que veníamos viendo: el formato de **Doble Precisión** (los famosos 64 bits). Es exactamente la misma lógica de "Punto Flotante" que ya entendiste a la perfección, pero con una caja de memoria mucho más grande. Es el tipo de dato `double` que usás cuando programás.

Conceptualmente no cambia absolutamente nada, solo se escalan los números. Acá tenés los tres cambios clave:

- **El nuevo reparto de los casilleros:** Pasás de tener 32 bits a 64 bits totales. El bit de signo sigue siendo 1 solo, pero ahora tenés **11 bits** para el exponente (lo que te permite guardar números ridículamente más gigantes o microscópicos) y **52 bits** para la mantisa (lo que te da una precisión milimétrica, ideal para que no haya errores de redondeo en cálculos largos).
    
- **El nuevo Exceso (1023 en lugar de 127):** Como ahora tu exponente tiene 11 bits, la cantidad de combinaciones salta a $2^{11} = 2048$. Los casilleros físicos van del `0` al `2047`. Si aplicás la misma fórmula que antes para buscar la mitad, hacés $(2047 - 1) / 2$ y te da **1023**. Ese es tu nuevo "Exceso".
    
- **La nueva regla de guardado y lectura:** La fórmula del recuadro negro es idéntica a la anterior, pero actualizada. Cuando hacés un cálculo en papel y lo querés guardar en la memoria, le **sumás 1023** a tu exponente real. Cuando la computadora quiere leer lo que está en la memoria (la fórmula del cuadro), agarra el exponente físico `E` y le **resta 1023** para recuperar tu número original. Sigue usando el `1,` implícito de siempre.
    

**¡Ojo con un pifie en la diapositiva!**

Si leés el texto con atención, vas a ver que en el medio del párrafo el profesor escribió: _"El formato de simple precisión tiene un exponente de 11 bits en formato exceso 1023"_. Claramente se copió y pegó el texto de la diapositiva anterior y se olvidó de cambiar la palabra "simple" por "doble". No te confundas con eso; todo lo que dice ahí aplica exclusivamente a la Doble Precisión de 64 bits.

Los extremos de este formato funcionan igual que en la tabla que vimos antes: el exponente físico de puros ceros (`0`) se guarda para el cero absoluto y los números no normalizados, y el exponente físico de puros unos (`2047`) se guarda para el Infinito y el NaN. Tus exponentes reales para cuentas normales ahora viajan desde el **-1022 hasta el +1023**.



![[Pasted image 20260826210234.png]]


Esta es exactamente la misma tabla de excepciones (el "diccionario" del procesador) que desglosamos hace un rato, pero escalada a las grandes ligas de la **Doble Precisión (64 bits)**. La lógica conceptual no cambia ni un milímetro, solo se agrandan los límites físicos.

  

Vamos a marcar las tres cosas más importantes (y un error de la diapositiva):

  

**1. El nuevo techo (Rango de representación)**

Mirá el número bestial que quedó arriba: $1,79... \times 10^{308}$.

En Simple Precisión el límite máximo llegaba hasta $10^{38}$. Al sumarle casilleros al exponente, la computadora ahora puede manejar cálculos a escala astronómica sin chocar contra la pared del Overflow.

  

**2. ¡Ojo con el pifie del profesor! (La Precisión)**

A la izquierda dice **Precisión = $2^{-32}$**. **Esto está mal**.

¿Te acordás que en la diapositiva de Simple Precisión la precisión era $2^{-23}$ porque tenías exactamente 23 casilleros para la mantisa? Bueno, en Doble Precisión tenés **52 casilleros** para la mantisa. Por lo tanto, la precisión real (el escalón más ínfimo que la máquina puede medir) es **$2^{-52}$**. Al profesor le debe haber quedado pegado un número de otra filmina o se le cruzaron los cables con los 32 bits totales de la Simple Precisión. Anotátelo por las dudas.

  

**3. La tabla actualizada con los nuevos límites**

El funcionamiento es calcado al que ya entendiste, pero usando el Exceso 1023:

  

- **La cuenta diaria (Exponente físico de 1 a 2046):** Es la zona segura. Acá la fórmula hace su magia de siempre: asume el `1.` implícito que no guardaste y le resta el Exceso 1023 al código de la memoria para devolverte tu exponente real.
    
      
    
- **Los códigos de Error (Exponente físico 2047):** Como ahora tu tope de combinaciones es 2047 (puros unos en los 11 bits), ese es el número que prende las alarmas. Si la mantisa está en `0`, es **Infinito**. Si la mantisa tiene algún `1`, es un error **NaN** (Not a Number).
    
      
    
- **El código Microscópico (Exponente físico 0):** Sigue funcionando igual. Si la mantisa está vacía, es el **Cero absoluto**. Si hay algo en la mantisa, entra en modo emergencia (números no normalizados): desactiva el `1.` implícito y fija el multiplicador en $2^{-1022}$ para evitar redondear a cero de golpe.


![[Pasted image 20260826210243.png]]

El estándar IEEE 754 es el sistema universal que utiliza el procesador para representar números fraccionarios (con coma flotante) en la memoria. Se basa en la notación científica binaria y divide el espacio físico en tres bloques fundamentales.

  

**1. Los Componentes del Número**

  

- **Bit de Signo (1 bit):** Funciona de manera independiente. Un `0` indica que el número es positivo y un `1` indica que es negativo.
    
      
    
- **La Mantisa y el Bit Implícito:** Es el bloque donde se guardan los números reales. Como en binario normalizado la notación científica siempre obliga a que el número empiece con un `1` a la izquierda de la coma (ej: $1,\text{algo} \times 2^{\text{exponente}}$), ese `1,` entero **nunca se guarda en la memoria**. La mantisa almacena únicamente los decimales que van después de la coma. Al recuperar el número, el procesador inyecta ese `1,` de forma automática, permitiendo ganar un bit extra de precisión sin ocupar espacio físico.
    
      
    
- **El Exponente y el Exceso:** Para evitar lidiar con números negativos dentro del exponente, se utiliza un sistema de desplazamiento llamado Exceso. Al exponente real matemático se le **suma** un número base fijo antes de guardarlo en la memoria. Cuando la computadora necesita hacer cálculos, lee ese código físico y le **resta** el Exceso para recuperar el exponente original (la fórmula $E - \text{Exceso}$).
    
      
    

**2. Las Dos Escalas del Formato**

  

- **Simple Precisión (32 bits totales):**
    
      
    - **Exponente:** 8 bits. Su Exceso es **127**. (Los exponentes matemáticos van del -126 al +127).
        
          
        
    - **Mantisa:** 23 bits (más el bit implícito).
        
          
        
- **Doble Precisión (64 bits totales):**
    
      
    - **Exponente:** 11 bits. Su Exceso es **1023**. Permite manejar cálculos a escala astronómica.
        
          
        
    - **Mantisa:** 52 bits (más el bit implícito). Otorga una precisión milimétrica para evitar errores de redondeo.
        
          
        

**3. Casos Especiales (Los límites físicos del Exponente)**

La norma reserva los valores extremos del exponente físico (todos los bits en `0` o todos los bits en `1`) para identificar situaciones anómalas:

  

- **Exponente físico en 0 (Puros ceros):**
    
      
    - Si la mantisa está vacía (0): Representa el **Cero absoluto**.
        
          
        
    - Si la mantisa tiene datos: Son **Números No Normalizados**. El procesador desactiva el `1,` implícito para poder representar valores microscópicos extremadamente cercanos al cero sin colapsar.
        
          
        
- **Exponente físico al máximo (Puros unos: 255 o 2047):**
    
      
    - Si la mantisa está vacía (0): Representa **Infinito** (suele darse por divisiones por cero o desbordamientos masivos).
        
          
        
    - Si la mantisa tiene datos: Representa **NaN (Not a Number)**, un código de error matemático para cálculos imposibles o indeterminados.







**Proceso para Guardar (Codificar un número al hardware)**

  

El objetivo es transformar un número decimal normal en los 32 bits físicos de la norma de Simple Precisión. Vamos a guardar el número **$-5,5$**.

  

1. **Pasar a binario puro:**
    
    El $5$ entero es `101`. El $0,5$ decimal es `0,1` en binario (porque representa $2^{-1}$).
    
    Tu número base es: `101,1`
    
      
    
2. **Normalizar (Mover la coma):**
    
    Tenés que correr la coma hacia la izquierda hasta que quede un único `1` entero.
    
    `101,1` se transforma en $1,011 \times 2^2$ (porque corriste la coma 2 lugares).
    
      
    
3. **Armar los 3 bloques físicos:**
    
      
    - **Signo:** Como es negativo ($-5,5$), el bit de signo es **`1`**.
        
          
        
    - **Exponente (Aplicar Exceso):** Tu exponente matemático es $2$. Para guardarlo, le sumás el exceso 127 ($2 + 127 = 129$). Pasás el 129 a binario: **`10000001`**.
        
          
        
    - **Mantisa (Eliminar el 1 implícito):** De tu número normalizado ($1,011$), tachás el `1,` inicial y te quedás solo con los decimales: `011`. Rellenás con ceros a la derecha hasta completar los 23 casilleros: **`01100000000000000000000`**.
        
          
        

El número físico guardado en la memoria de la computadora queda:

`1 10000001 01100000000000000000000`

  

**Proceso para Leer (Decodificar desde el hardware)**

  

El objetivo es hacer el camino inverso: el procesador lee una cadena de 32 bits y debe reconstruir el valor matemático para usarlo en una cuenta. Vamos a leer esta cadena:

`0 10000010 01000000000000000000000`

  

1. **Desarmar los 3 bloques:**
    
      
    - **Signo:** Es `0`, por lo tanto el número es **positivo (+)**.
        
          
        
    - **Exponente físico:** Es `10000010`, que en decimal equivale a $130$.
        
          
        
    - **Mantisa física:** Es `010000...` (ignoramos los ceros de relleno).
        
          
        
2. **Recuperar el exponente real (Restar el Exceso):**
    
    Al exponente físico guardado le restás la base de 127 para deshacer el truco.
    
    $130 - 127 = 3$. Tu exponente matemático real es **$3$**.
    
      
    
3. **Reconstruir con la fórmula:**
    
    El procesador inyecta el "1," fantasma adelante de tu mantisa y arma la notación científica:
    
    $+ 1,01 \times 2^3$
    
      
    
4. **Desnormalizar (Volver a correr la coma):**
    
    Como el exponente es $3$, movés la coma 3 lugares hacia la derecha para desarmar la notación científica:
    
    `1,01` $\rightarrow$ `1010,0`
    
      
    
5. **Pasar a decimal:**
    
    El binario `1010` equivale exactamente al número **$10$** decimal. Ese es el valor que el procesador entrega a la pantalla.