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

![[Pasted image 20260825070325.png]]

![[Pasted image 20260825070344.png]]

![[Pasted image 20260825070355.png]]

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