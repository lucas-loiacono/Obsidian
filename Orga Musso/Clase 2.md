![[Pasted image 20260825070057.png]]

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


![[Pasted image 20260825070344.png]]

![[Pasted image 20260825070355.png]]


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

![[Pasted image 20260825070542.png]]

![[Pasted image 20260825070718.png]]

![[Pasted image 20260825070729.png]]

![[Pasted image 20260825070742.png]]

![[Pasted image 20260825070757.png]]

![[Pasted image 20260825070812.png]]

![[Pasted image 20260825070823.png]]