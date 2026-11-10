![[Pasted image 20261110014120.png]]


![[Pasted image 20261107160459.png]]

````Ejercicio 1.1: Complejidad y Recursividad

### Enunciado
Dada la siguiente función recursiva en Java:

```java
void funcionMisteriosa(int n) {
    if (n > 0) {
        System.out.print(n + "-");
        funcionMisteriosa(n - 1);
        System.out.print(n + "-");
    }
}
````

¿Qué se imprime por pantalla al invocar `funcionMisteriosa(3);`?

- (a) `3-2-1-1-2-3-`
    
- (b) `3-2-1-`
    
- (c) `3-3-2-2-1-1-`
    
- (d) `1-2-3-3-2-1-`
    
- (e) Se lanza una excepción de tipo `StackOverflowError`
    

### Solución y Explicación

La respuesta correcta es la **(a): `3-2-1-1-2-3-`**.

#### Trazabilidad de la Pila de Llamadas

Esta función ejecuta instrucciones tanto en la **ida** (antes del llamado recursivo) como en la **vuelta** (cuando se resuelve la recursión y se desapila).

Ejecución paso a paso para `n = 3`:

1. **`funcionMisteriosa(3)`**:
    
    - $3 > 0 \rightarrow$ Verdadero.
        
    - Imprime: `3-`
        
    - Llama a `funcionMisteriosa(2)` y queda en estado de espera.
        
2. **`funcionMisteriosa(2)`**:
    
    - $2 > 0 \rightarrow$ Verdadero.
        
    - Imprime: `2-`
        
    - Llama a `funcionMisteriosa(1)` y queda en estado de espera.
        
3. **`funcionMisteriosa(1)`**:
    
    - $1 > 0 \rightarrow$ Verdadero.
        
    - Imprime: `1-`
        
    - Llama a `funcionMisteriosa(0)` y queda en estado de espera.
        
4. **`funcionMisteriosa(0)`**:
    
    - $0 > 0 \rightarrow$ Falso. (Caso base).
        
    - Finaliza sin hacer nada y retorna el control a `funcionMisteriosa(1)`.
        
5. **Retomamos `funcionMisteriosa(1)`**:
    
    - Ejecuta la instrucción posterior a la recursión con su contexto actual ($n=1$).
        
    - Imprime: `1-`
        
    - Retorna el control a `funcionMisteriosa(2)`.
        
6. **Retomamos `funcionMisteriosa(2)`**:
    
    - Ejecuta la instrucción posterior a la recursión con su contexto actual ($n=2$).
        
    - Imprime: `2-`
        
    - Retorna el control a `funcionMisteriosa(3)`.
        
7. **Retomamos `funcionMisteriosa(3)`**:
    
    - Ejecuta la instrucción posterior a la recursión con su contexto actual ($n=3$).
        
    - Imprime: `3-`
        
    - Finaliza la ejecución del programa.
        

#### Resultado final

Al concatenar las impresiones cronológicamente obtenemos el string:**`3-2-1-1-2-3-`**

![[Pasted image 20261107160445.png]]

# Ejercicio 1.2: Complejidad Asintótica

### Enunciado
Sea la función de tiempo de un algoritmo[cite: 2]:

$$T(n) = 3n \ln(n) + 4n - 5$$[cite: 2]

Donde $n$ es el tamaño de la entrada[cite: 2]. Marcar **TODAS** las opciones válidas[cite: 2]:

- (a) $\Theta(3n^2)$[cite: 2]
- (b) $O(2n^2)$[cite: 2]
- (c) $\Omega(300)$[cite: 2]
- (d) $\Omega(300n \ln(n))$[cite: 2]
- (e) $O(n + n\sqrt{n})$[cite: 2]
- (f) $\Theta(300n + n \ln(n))$[cite: 2]
- (g) $O(n!)$[cite: 2]
- (h) $\Omega(30!)$[cite: 2]

---

### Solución y Explicación

Las opciones correctas son: **(b), (c), (d), (e), (f), (g), (h)**.

#### Análisis del término dominante
Para encontrar la complejidad del algoritmo $T(n)$, debemos identificar el término que crece más rápido cuando $n \to \infty$. 
- Los términos son: $3n \ln(n)$, $4n$ y $-5$.
- El término de mayor orden de crecimiento es $3n \ln(n)$.
- En notación asintótica, las constantes multiplicativas (el $3$) y los términos de menor orden se descartan. 
- Por lo tanto, el orden de crecimiento exacto (la cota ajustada) del algoritmo es **$\Theta(n \ln n)$**.

#### Evaluación de cada opción
Recordemos qué significan las notaciones:
- **$O(g(n))$**: Cota superior (crece igual o más rápido).
- **$\Omega(g(n))$**: Cota inferior (crece igual o más lento).
- **$\Theta(g(n))$**: Cota ajustada (crece exactamente al mismo ritmo).

1. **(a) $\Theta(3n^2)$ $\rightarrow$ FALSO**. Equivale a $\Theta(n^2)$. Nuestra función crece a un ritmo de $n \ln n$, que es estrictamente menor que $n^2$. No es una cota ajustada.
2. **(b) $O(2n^2)$ $\rightarrow$ VERDADERO**. Equivale a $O(n^2)$. Como $n \ln n$ crece más lento que $n^2$, $n^2$ funciona perfectamente como un límite superior (cota superior).
3. **(c) $\Omega(300)$ $\rightarrow$ VERDADERO**. $300$ es una constante, por lo que equivale a $\Omega(1)$. Como $T(n)$ crece hacia el infinito al aumentar $n$, siempre será mayor que una constante para un $n$ grande. Es una cota inferior válida.
4. **(d) $\Omega(300n \ln(n))$ $\rightarrow$ VERDADERO**. Descartando la constante, equivale a $\Omega(n \ln n)$. Como $T(n)$ es exactamente $\Theta(n \ln n)$, por definición también cumple con ser su propia cota inferior $\Omega(n \ln n)$.
5. **(e) $O(n + n\sqrt{n})$ $\rightarrow$ VERDADERO**. El término dominante aquí es $n\sqrt{n}$, que es lo mismo que $n^{1.5}$. El logaritmo $\ln(n)$ crece asintóticamente más lento que cualquier potencia fraccionaria como $n^{0.5}$. Por ende, $n \ln n$ está acotado superiormente por $n^{1.5}$.
6. **(f) $\Theta(300n + n \ln(n))$ $\rightarrow$ VERDADERO**. Dentro del paréntesis, el término que domina es $n \ln(n)$ (le gana a $300n$). Al descartar las constantes, esta expresión es equivalente a $\Theta(n \ln n)$, que es exactamente la cota ajustada de nuestra $T(n)$.
7. **(g) $O(n!)$ $\rightarrow$ VERDADERO**. La función factorial $n!$ tiene un crecimiento colosalmente más rápido que $n \ln n$. Sirve como cota superior (aunque sea muy holgada).
8. **(h) $\Omega(30!)$ $\rightarrow$ VERDADERO**. Aunque $30!$ es un número inmensamente grande, no deja de ser un número fijo (una constante). Por lo tanto, asintóticamente equivale a $\Omega(1)$, exactamente igual que la opción (c). Es una cota inferior válida.


# Comportamiento de $\ln(n)$ y potencias polinómicas

### 1. ¿Cómo es la función $\ln(n)$?

La función $\ln(n)$ es el **logaritmo natural** (logaritmo en base $e$, donde $e \approx 2.718$). En el contexto de análisis de algoritmos, lo más importante que tenés que saber sobre los logaritmos (sin importar su base) es que **crecen de manera extremadamente lenta**.

Para darte una idea visual de lo lento que crece a medida que $n$ se hace grande:
- Si $n = 10$, $\ln(10) \approx 2.3$
- Si $n = 100$, $\ln(100) \approx 4.6$
- Si $n = 1000$, $\ln(1000) \approx 6.9$
- Si $n = 1.000.000$, $\ln(1.000.000) \approx 13.8$

Mientras $n$ explota hacia números gigantes, el logaritmo sube a paso de tortuga. 

---

### 2. ¿Por qué $n \ln(n)$ está acotado por $O(n^{1.5})$?

La opción (e) del ejercicio proponía $O(n + n\sqrt{n})$.
Por propiedades de exponentes, sabemos que $\sqrt{n}$ es lo mismo que $n^{0.5}$. Entonces:
$n \cdot \sqrt{n} = n^1 \cdot n^{0.5} = n^{1.5}$

Para saber si $n \ln(n) \in O(n^{1.5})$, tenemos que ver quién crece más rápido. Si dividimos ambas funciones por $n$ para simplificar la comparación, nos queda:
- Del lado izquierdo: **$\ln(n)$**
- Del lado derecho: **$n^{0.5}$** (que es $\sqrt{n}$)

Aquí entra una **regla de oro de la complejidad asintótica**:
> **Cualquier función logarítmica siempre crece más lento que cualquier función polinómica/potencial con exponente mayor a cero.**

No importa qué tan chico sea el exponente. Un $\ln(n)$ siempre va a perder a la larga contra $n^{0.5}$, contra $n^{0.1}$ e incluso contra $n^{0.0001}$. Al principio el logaritmo puede parecer más grande, pero cuando $n$ tiende a infinito, la potencia fraccionaria lo pasa por encima.

**Conclusión:**
Como $\sqrt{n}$ crece estrictamente más rápido que $\ln(n)$, si multiplicamos ambas por $n$, resulta que **$n^{1.5}$ crece estrictamente más rápido que $n \ln(n)$**. 

Al crecer más rápido, $n^{1.5}$ funciona perfectamente como un "techo" (cota superior) para tu algoritmo, haciendo que la afirmación $T(n) \in O(n^{1.5})$ sea matemáticamente correcta.


# Comportamiento de $\ln(n)$ y potencias polinómicas

### 1. ¿Cómo es la función $\ln(n)$?

La función $\ln(n)$ es el **logaritmo natural** (logaritmo en base $e$, donde $e \approx 2.718$). En el contexto de análisis de algoritmos, lo más importante que tenés que saber sobre los logaritmos (sin importar su base) es que **crecen de manera extremadamente lenta**.

Para darte una idea visual de lo lento que crece a medida que $n$ se hace grande:
- Si $n = 10$, $\ln(10) \approx 2.3$
- Si $n = 100$, $\ln(100) \approx 4.6$
- Si $n = 1000$, $\ln(1000) \approx 6.9$
- Si $n = 1.000.000$, $\ln(1.000.000) \approx 13.8$

Mientras $n$ explota hacia números gigantes, el logaritmo sube a paso de tortuga. 

---

### 2. ¿Por qué $n \ln(n)$ está acotado por $O(n^{1.5})$?

La opción (e) del ejercicio proponía $O(n + n\sqrt{n})$.
Por propiedades de exponentes, sabemos que $\sqrt{n}$ es lo mismo que $n^{0.5}$. Entonces:
$n \cdot \sqrt{n} = n^1 \cdot n^{0.5} = n^{1.5}$

Para saber si $n \ln(n) \in O(n^{1.5})$, tenemos que ver quién crece más rápido. Si dividimos ambas funciones por $n$ para simplificar la comparación, nos queda:
- Del lado izquierdo: **$\ln(n)$**
- Del lado derecho: **$n^{0.5}$** (que es $\sqrt{n}$)

Aquí entra una **regla de oro de la complejidad asintótica**:
> **Cualquier función logarítmica siempre crece más lento que cualquier función polinómica/potencial con exponente mayor a cero.**

No importa qué tan chico sea el exponente. Un $\ln(n)$ siempre va a perder a la larga contra $n^{0.5}$, contra $n^{0.1}$ e incluso contra $n^{0.0001}$. Al principio el logaritmo puede parecer más grande, pero cuando $n$ tiende a infinito, la potencia fraccionaria lo pasa por encima.

**Conclusión:**
Como $\sqrt{n}$ crece estrictamente más rápido que $\ln(n)$, si multiplicamos ambas por $n$, resulta que **$n^{1.5}$ crece estrictamente más rápido que $n \ln(n)$**. 

Al crecer más rápido, $n^{1.5}$ funciona perfectamente como un "techo" (cota superior) para tu algoritmo, haciendo que la afirmación $T(n) \in O(n^{1.5})$ sea matemáticamente correcta.

![[Pasted image 20261107165445.png]]

![[Pasted image 20261107170332.png]]

# Ejercicio 1.3: Complejidad Asintótica

### Enunciado
Sea la función de tiempo de un algoritmo[cite: 4]:

$$T(n) = 3n \ln(n) + 2n^2$$[cite: 4]

Donde $n$ es el tamaño de la entrada[cite: 4]. Entonces, el orden del algoritmo es (marcar **TODAS** las opciones válidas)[cite: 4]:

- (a) $\Omega(30n^2)$[cite: 4]
- (b) $O(n^2 + n)$[cite: 4]
- (c) $\Theta(2n^2 + 3n)$[cite: 4]
- (d) $\Omega(n \ln(n))$[cite: 4]
- (e) $O(n^2 + n\sqrt{n})$[cite: 4]
- (f) $\Theta(n^2 \ln(n))$[cite: 4]
- (g) $O(n!)$[cite: 4]
- (h) $\Omega(30!)$[cite: 4]

---

### Solución y Explicación

Las opciones correctas son: **(a), (b), (c), (d), (e), (g), (h)**. La única incorrecta es la (f).

#### 1. Análisis del término dominante
Para determinar la complejidad de $T(n)$, debemos identificar el término que crece más rápido a medida que $n$ tiende a infinito:
- Tenemos dos términos: $3n \ln(n)$ y $2n^2$.
- Podemos pensar en $n^2$ como $n \cdot n$. Si lo comparamos con el primer término $n \cdot \ln(n)$, la competencia se reduce a comparar $n$ contra $\ln(n)$.
- Como vimos en el ejercicio anterior, cualquier polinomio (en este caso $n^1$) crece asintóticamente más rápido que un logaritmo ($\ln(n)$).
- Por lo tanto, el término $2n^2$ domina sobre $3n \ln(n)$.
- Descartando constantes y términos de menor orden, la cota ajustada exacta de nuestro algoritmo es **$\Theta(n^2)$**.

#### 2. Evaluación de cada opción
Sabiendo que $T(n) \in \Theta(n^2)$, analizamos las afirmaciones:

- **(a) $\Omega(30n^2)$ $\rightarrow$ VERDADERO**. Al descartar la constante $30$, la expresión equivale a $\Omega(n^2)$. Como $T(n)$ es exactamente $\Theta(n^2)$, por definición también cumple con ser su propia cota inferior $\Omega(n^2)$.
- **(b) $O(n^2 + n)$ $\rightarrow$ VERDADERO**. Dentro del paréntesis, el término que domina es $n^2$. La expresión equivale a $O(n^2)$. Dado que $T(n) \in \Theta(n^2)$, $n^2$ funciona perfectamente como su cota superior.
- **(c) $\Theta(2n^2 + 3n)$ $\rightarrow$ VERDADERO**. El término dominante del polinomio propuesto es $n^2$, por lo que equivale a $\Theta(n^2)$. Es exactamente la misma cota ajustada que la de nuestro $T(n)$.
- **(d) $\Omega(n \ln(n))$ $\rightarrow$ VERDADERO**. Aquí se nos pregunta si $T(n)$ crece *igual o más rápido* que $n \ln(n)$. Como el ritmo de crecimiento de nuestro algoritmo es $n^2$ y este crece estrictamente más rápido que $n \ln(n)$, la afirmación es correcta. Funciona como una cota inferior válida.
- **(e) $O(n^2 + n\sqrt{n})$ $\rightarrow$ VERDADERO**. El término dominante del paréntesis es $n^2$ (porque $n^2 > n^{1.5}$). Por lo tanto, equivale a $O(n^2)$, que sabemos que es una cota superior correcta para nuestro $T(n)$.
- **(f) $\Theta(n^2 \ln(n))$ $\rightarrow$ FALSO**. Se afirma que el crecimiento de $T(n)$ es exactamente proporcional a $n^2 \ln(n)$. Esto es incorrecto, ya que $n^2 \ln(n)$ crece más rápido que nuestro verdadero límite, que es $n^2$.
- **(g) $O(n!)$ $\rightarrow$ VERDADERO**. La función factorial $n!$ crece infinitamente más rápido que $n^2$. Por lo tanto, sirve como una cota superior (muy holgada, pero matemáticamente válida).
- **(h) $\Omega(30!)$ $\rightarrow$ VERDADERO**. $30!$ es un número colosal, pero constante. En términos asintóticos, equivale a $\Omega(1)$. Como $T(n)$ crece hacia el infinito, siempre será mayor que cualquier constante para un $n$ suficientemente grande. Es una cota inferior válida.

![[Pasted image 20261107170803.png]]


  


### Código y conteo de OE por línea

Al analizar el código de la función `buscar`, sumamos el costo de recibir los parámetros y el costo individual de cada línea.

**Criterio utilizado:** 1 OE por asignación, operación lógica/aritmética, comparación, retorno, acceso a propiedades (`.length`) y acceso a posiciones de arreglos (`[i]`). Se asume cortocircuito lógico en el `&&`.

```java
boolean buscar(int[] vec, int dato) {          // 2 OE (asignación de parámetros al iniciar)
    int i = 0;                                 // 1 OE (asignación)
    boolean encontrado = false;                // 1 OE (asignación)
    while (i < vec.length && !encontrado) {    // 4 OE (acceso a length, comparación <, negación !, AND &&)
        if (vec[i] == dato) {                  // 2 OE (acceso a arreglo, comparación ==)
            encontrado = true;                 // 1 OE (asignación)
        } else {
            i++;                               // 2 OE (suma y asignación, equivalente a i = i + 1)
        }
    }
    return encontrado;                         // 1 OE (retorno)
}
````

### a. Paso a paso en el MEJOR caso

El mejor caso ocurre cuando el elemento `dato` se encuentra en la **primera posición** del arreglo (`vec[0]`).

  

1. **Paso de parámetros e Inicialización:**
    
      
    - `vec` y `dato` $\rightarrow$ 2 OE
        
          
        
    - `i = 0` $\rightarrow$ 1 OE
        
          
        
    - `encontrado = false` $\rightarrow$ 1 OE
        
          
        
2. **Primera evaluación del `while` (Entra al ciclo):**
    
      
    - `(0 < vec.length && !false)` $\rightarrow$ 4 OE
        
          
        
3. **Evaluación del `if` (Verdadero):**
    
      
    - `vec[0] == dato` $\rightarrow$ 2 OE
        
4. **Cuerpo del `if`:**
    
      
    - `encontrado = true` $\rightarrow$ 1 OE
        
          
        
5. **Segunda evaluación del `while` (Sale del ciclo):**
    
      
    - `(0 < vec.length && !true)` $\rightarrow$ 4 OE (La primera parte es V, evalúa la segunda y el AND da Falso).
        
          
        
6. **Retorno:**
    
      
    - `return encontrado` $\rightarrow$ 1 OE
        
          
        

**Total Mejor Caso:** $2 + 1 + 1 + 4 + 2 + 1 + 4 + 1 =$ **16 OE**

  

### b. Paso a paso en el PEOR caso

Sea **$n$ el tamaño del arreglo** ($n = \text{vec.length}$). El peor caso ocurre cuando hay que recorrer todo el vector porque el `dato` **no se encuentra** (o porque está recién en la última posición, obligando a recorrerlo por completo).

  

1. **Paso de parámetros e Inicialización:**
    
      
    - `vec` y `dato` $\rightarrow$ 2 OE
        
          
        
    - `i = 0` $\rightarrow$ 1 OE
        
          
        
    - `encontrado = false` $\rightarrow$ 1 OE
        
          
        
2. **Ejecución del ciclo `while` ($n$ iteraciones):** Como se recorre todo el vector, el ciclo se ejecuta $n$ veces completas. Por cada iteración:
    
      
    - Condición del `while`: 4 OE
        
          
        
    - Condición del `if` (da falso): 2 OE
        
          
        
    - Cuerpo del `else` (`i++`): 2 OE
        
          
        
    - _Total por iteración:_ $8$ OE $\rightarrow$ _Costo de recorrer el vector:_ **$8n$ OE**
        
          
        
3. **Última evaluación del `while` (Sale del ciclo):**
    
      
    - Cuando $i = n$, la condición `i < vec.length` da falso. Por el cortocircuito lógico de Java, la ejecución se frena ahí y no evalúa la segunda parte (`&& !encontrado`).
        
          
        
    - Costo de salida: 2 OE (acceso a `length` y comparación `<`).
        
          
        
4. **Retorno:**
    
      
    - `return encontrado` $\rightarrow$ 1 OE
        
          
        

**Total Peor Caso:** $2 + 1 + 1 + 8n + 2 + 1 =$ **$8n + 7$ OE**


![[Pasted image 20261107171507.png]]


# Ejercicio 1.5: Cálculo de $T(n)$ en el Peor Caso

### Enunciado
Dado el siguiente método, completar la función que indica cuántas OE (operaciones elementales) tiene en el peor caso:

```java
public int f(int[] vec, int n, int valor) {
    int i = 0;
    int idx = -1;
    boolean fin = false;
    while (i < n && !fin) {
        if (vec[i] == valor) {
            idx = i;
            fin = true;
        } else {
            i++;
        }
    }
    return idx;
}
````

### Análisis de Operaciones Elementales (OE) línea por línea

Consideramos 1 OE para: asignaciones, operaciones aritméticas/lógicas, comparaciones, accesos a arreglos y retornos. Se contabiliza el paso de parámetros a la función como asignaciones iniciales.



```Java
public int f(int[] vec, int n, int valor) {    // 3 OE (paso de los 3 parámetros)
    int i = 0;                                 // 1 OE (asignación)
    int idx = -1;                              // 1 OE (asignación)
    boolean fin = false;                       // 1 OE (asignación)
    
    // Ciclo while:
    while (i < n && !fin) {                    // 3 OE (comparación <, negación !, y AND lógico &&)
        if (vec[i] == valor) {                 // 2 OE (acceso al arreglo [i], comparación ==)
            idx = i;                           // 1 OE (asignación)
            fin = true;                        // 1 OE (asignación)
        } else {
            i++;                               // 2 OE (suma y asignación: i = i + 1)
        }
    }
    return idx;                                // 1 OE (retorno)
}
```

### Evaluación del Peor Caso

El **peor caso** ocurre cuando el elemento `valor` **no se encuentra** en el arreglo de tamaño $n$. Esto obliga al algoritmo a recorrer todos los $n$ elementos, ejecutando siempre el bloque `else` y evaluando la condición de salida una vez al final.

1. **Bloque inicial (se ejecuta 1 sola vez al arrancar):**
    
    - Parámetros: 3 OE
        
    - Asignaciones de variables (`i`, `idx`, `fin`): 3 OE
        
    - _Total inicial =_ **6 OE**
        
2. **Iteraciones del ciclo `while` (se repite $n$ veces):** Por cada elemento del arreglo que no coincide con `valor`, se ejecuta:
    
    - Evaluación de la condición del `while`: 3 OE
        
    - Evaluación de la condición del `if` (da falsa): 2 OE
        
    - Ejecución del cuerpo del `else` (`i++`): 2 OE
        
    - _Costo por iteración =_ $7$ OE
        
    - _Costo total de las $n$ iteraciones =_ **$7n$ OE**
        
3. **Condición de corte (salida del ciclo):**
    
    - Cuando `i == n`, la evaluación `i < n` da `false`.
        
    - Por la regla de evaluación de cortocircuito en Java (operador `&&`), la segunda parte de la condición (`!fin`) no se evalúa.
        
    - _Costo de salida =_ **1 OE** (solo la comparación de `i < n`).
        
4. **Retorno final:**
    
    - `return idx;` = **1 OE**
        

### Suma Total y Resultado Final

Para armar el polinomio final, sumamos todas las partes:

$$T(n) = \text{Inicialización} + \text{Iteraciones} + \text{Corte} + \text{Retorno}$$

$$T(n) = 6 + 7n + 1 + 1$$

$$T(n) = 7n + 8$$

**Respuesta final para completar el enunciado:**$T(n) = 7n + 8$


![[Pasted image 20261107172201.png]]

# Ejercicio 1.6: Teorema Maestro

### Enunciado
Sea la función de tiempo de un algoritmo recursivo[cite: 8]:
$$T(n) = 5T(n/2) + 4n^2$$
Donde $n$ es el tamaño de la entrada. Entonces, el orden del algoritmo, según el Teorema Maestro, es[cite: 8]:
- (a) $\Theta(5n \ln(n))$
- (b) $\Theta(n^2 \log(n))$
- (c) $\Theta(n^2)$
- (d) $\Theta(n^{\log_2(5)})$

### Solución y Explicación
Para aplicar el Teorema Maestro, primero identificamos los valores de las constantes en la ecuación de recurrencia de la forma $T(n) = a \cdot T(n/b) + c \cdot n^d$[cite: 8]:
- **$a = 5$** (cantidad de llamadas recursivas)[cite: 8].
- **$b = 2$** (factor de división del problema)[cite: 8].
- **$d = 2$** (exponente del término independiente $4n^2$)[cite: 8].

Ahora evaluamos la relación entre $a$ y $b^d$[cite: 8]:
- $b^d = 2^2 = 4$
- Comparamos: **$5 > 4 \implies a > b^d$**

Según el recordatorio del teorema, cuando $a > b^d$, el costo de las hojas (llamadas recursivas) domina sobre el costo de combinar, y el orden es $\Theta(n^{\log_b a})$[cite: 8].
Reemplazando nuestros valores, obtenemos: **$\Theta(n^{\log_2 5})$**

**Opción correcta: (d)**[cite: 8]

---

# Ejercicio 1.7: Teorema Maestro

### Enunciado
Sea la función de tiempo de un algoritmo recursivo[cite: 8]:
$$T(n) = 5T(n/4) + 4n^3$$
Donde $n$ es el tamaño de la entrada. Entonces, el orden del algoritmo, según el Teorema Maestro, es[cite: 8]:
- (a) $\Theta(5n \ln(n))$
- (b) $\Theta(n^3 \log(n))$
- (c) $\Theta(n^3)$
- (d) $\Theta(n^{\log_4(5)})$

### Solución y Explicación
Volvemos a identificar los parámetros de la ecuación $T(n) = a \cdot T(n/b) + c \cdot n^d$[cite: 8]:
- **$a = 5$**[cite: 8]
- **$b = 4$**[cite: 8]
- **$d = 3$** (exponente del término independiente $4n^3$)[cite: 8]

Evaluamos la relación entre $a$ y $b^d$:
- $b^d = 4^3 = 64$
- Comparamos: **$5 < 64 \implies a < b^d$**

Según el Teorema Maestro, cuando $a < b^d$, el costo de particionar y combinar domina sobre el costo de las llamadas recursivas. En este caso, el orden está dictado directamente por el término polinómico de mayor grado, es decir, $\Theta(n^d)$[cite: 8].
Reemplazando nuestro valor de $d$, obtenemos: **$\Theta(n^3)$**

**Opción correcta: (c)**[cite: 8]

# ¿Para qué sirve $T(n) = c \cdot n^d$ cuando $1 \le n < b$?

Esa primera línea en la llave del Teorema Maestro representa el **caso base** del algoritmo recursivo.

### Explicación detallada

1. **Freno de la recursión:** Un algoritmo recursivo no puede dividirse infinitamente. Cuando el tamaño del problema de entrada ($n$) se vuelve lo suficientemente pequeño (estrictamente menor que $b$, que es el número por el cual dividís el problema), el algoritmo deja de llamarse a sí mismo.
2. **Resolución directa:** En ese punto (cuando $1 \le n < b$), el problema es tan chico que se resuelve de manera directa, sin recursividad. El costo de tiempo de resolver ese problema diminuto se define genéricamente como $c \cdot n^d$ (aunque en la práctica de programación, esto casi siempre representa un costo constante $\Theta(1)$).
3. **Impacto en la Complejidad Asintótica:** Matemáticamente es obligatorio definir esta condición de parada para que la función esté completa. Sin embargo, **el caso base no afecta el orden de complejidad final**. 

En resumen: sirve para que la definición matemática de la recurrencia sea correcta y tenga un punto final. Pero a la hora de calcular el orden $\Theta$ usando el Teorema Maestro, esta parte se ignora por completo, ya que lo que determina el crecimiento del tiempo para un $n$ gigante (tendiendo a infinito) es únicamente la parte recursiva de abajo (cuando $n \ge b$).


![[Pasted image 20261107172538.png]]

# Ejercicio 1.8: Teorema Maestro a partir de código

### Enunciado
Indicar el orden de la siguiente función aplicando el **Teorema Maestro**. Justificar[cite: 9].

### Análisis del código y deducción de la ecuación de recurrencia
Para aplicar el Teorema Maestro, primero debemos traducir el comportamiento del código a una ecuación matemática de la forma $T(n) = a \cdot T(n/b) + c \cdot n^d$[cite: 9].
Sea $n$ el tamaño del problema, representado por la variable `largo` ($n = \text{fin} - \text{ini}$)[cite: 9].

1. **Valor de $a$ (cantidad de llamadas recursivas):** Dentro de la función, hay exactamente 3 invocaciones a sí misma (`funcion(...)`)[cite: 9]. Por lo tanto, **$a = 3$**.
2. **Valor de $b$ (factor de división):** El tamaño original `largo` se divide en 3 (`int parte = largo / 3;`), y cada llamada recursiva procesa una porción de ese tamaño[cite: 9]. Por lo tanto, **$b = 3$**.
3. **Valor de $d$ (costo de combinar/dividir):** Al final del bloque, se ejecuta `realizarTrabajoLineal(vec);`, cuyo comentario indica que tiene una complejidad de $O(\text{largo})$[cite: 9]. Esto equivale a un trabajo extra proporcional a $n^1$. Por lo tanto, el exponente del término polinómico es **$d = 1$**.

Con estos datos, la ecuación de recurrencia que modela la función es:
$$T(n) = 3T(n/3) + O(n^1)$$

### Aplicación del Teorema Maestro
Evaluamos la relación entre $a$ y $b^d$[cite: 9]:
- $a = 3$
- $b^d = 3^1 = 3$
- Comparamos: **$a = b^d \implies 3 = 3$**

Según el recordatorio del Teorema Maestro, cuando $a = b^d$, el costo está balanceado de manera uniforme a través del árbol de recursión[cite: 9]. El orden del algoritmo corresponde al caso del medio, cuya complejidad es $\Theta(n^d \cdot \log n)$[cite: 9].

Reemplazando nuestro valor de $d=1$, obtenemos: **$\Theta(n \log n)$**

---
**Respuesta final:**
El orden de la función es **$\Theta(n \log n)$**. 
*Justificación:* La ecuación de recurrencia asociada es $T(n) = 3T(n/3) + O(n)$, la cual satisface la condición $a = b^d$ ($3 = 3^1$) del Teorema Maestro, resultando en una complejidad de $\Theta(n^1 \log n)$.




La ecuación de recurrencia general $T(n) = a \cdot T(n/b) + f(n)$ se divide exactamente en las dos partes que mencionás:

- **La parte recursiva ($a \cdot T(n/b)$):** Es el costo exclusivo de las llamadas a la función en sí misma. Lo que acompaña a la $T$ indica **cuántas veces** llamás a la recursión ($a$), y lo de adentro indica **de qué tamaño** le pasás el problema ($n/b$).
    

- **La parte NO recursiva ($+ f(n)$ o $+ c \cdot n^d$):** Es el costo de todo el trabajo extra que hace la función _afuera_ de esas llamadas recursivas (como dividir el problema antes, o juntar los resultados después). Como bien decís, puede ser un **número constante** (si hace operaciones elementales simples, le sumás algo como $+ O(1)$ o $+ c$) o una **función** (si tiene un ciclo `for` o llama a otra función lineal, le sumás $+ O(n)$ o $+ n^2$).

Esa es la clave fundamental para leer el código de cualquier algoritmo recursivo y armar su ecuación al instante.






# Que es B?
Sí, $b$ siempre representa el factor por el cual se divide (o reduce) el tamaño del problema original en cada nueva llamada recursiva, sin importar si ese "tamaño" es la longitud de un vector, las dimensiones de una matriz o un número entero $n$.

# Resumen: Parámetros del Teorema Maestro

El Teorema Maestro sirve para hallar la complejidad asintótica (orden $\Theta$) de algoritmos recursivos cuya ecuación de tiempo se puede expresar con la siguiente forma general:

$$T(n) = a \cdot T\left(\frac{n}{b}\right) + c \cdot n^d$$

### Desglose de cada variable

*   **$T(n)$:** Es el tiempo total de ejecución del algoritmo para un problema de tamaño $n$.
*   **$a$ (Llamadas recursivas):** Representa la **cantidad de veces** que la función se llama a sí misma dentro del código.
    *   *Ejemplo:* Si en el código ves que la función recursiva se invoca 3 veces por cada ejecución, entonces $a = 3$. Siempre es un número entero $a \ge 1$.
*   **$b$ (Factor de división):** Representa la proporción en la que se **divide el tamaño del problema** original para pasárselo a la siguiente llamada recursiva.
    *   *Ejemplo:* Si el problema original tiene tamaño $n$ (como un vector) y a la recursión le pasás la mitad de ese vector, el problema se achicó por 2, entonces $b = 2$. Siempre debe ser $b > 1$.
*   **$c \cdot n^d$ o $O(n^d)$ (Trabajo extra / NO recursivo):** Es el tiempo que gasta la función haciendo tareas *fuera* de las llamadas recursivas (operaciones matemáticas, un ciclo `for` para combinar resultados, dividir el arreglo, etc.).
    *   **$d$ (Exponente del trabajo extra):** Define el ritmo de crecimiento de ese trabajo no recursivo.
        *   Si el trabajo extra es apenas un par de variables o un `if`, el tiempo es constante $O(1)$. Como $1 = n^0$, entonces **$d = 0$**.
        *   Si el trabajo extra requiere recorrer el vector con un ciclo simple, el tiempo es lineal $O(n)$. Como $n = n^1$, entonces **$d = 1$**.
        *   Si el trabajo extra requiere ciclos anidados, el tiempo es cuadrático $O(n^2)$, entonces **$d = 2$**.
    *   **$c$ (Constante):** Es un número que acompaña al trabajo extra (ej. el $4$ en $4n^2$). A fines prácticos para el teorema, **se ignora**, ya que el exponente $d$ es el único que define la complejidad asintótica.

---

### Resumen de los 3 casos (Evaluando $a$ vs $b^d$)

Para saber el resultado, siempre tenés que calcular $b^d$ y compararlo con $a$.

1.  **Si $a < b^d$ (Domina el trabajo no recursivo):**
    El peso del algoritmo está en lo que hace afuera de la recursión (particionar o combinar).
    $\implies \mathbf{\Theta(n^d)}$
2.  **Si $a = b^d$ (Trabajo equilibrado):**
    El costo de las llamadas recursivas y el trabajo extra están perfectamente balanceados en todo el árbol de ejecución.
    $\implies \mathbf{\Theta(n^d \log n)}$
3.  **Si $a > b^d$ (Dominan las llamadas recursivas):**
    El costo de dividirse en tantas sub-ramas es lo que más tiempo consume en el algoritmo.
    $\implies \mathbf{\Theta(n^{\log_b a})}$