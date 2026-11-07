
![[Pasted image 20261107160459.png]]

````markdown
# Ejercicio 1.1: Complejidad y Recursividad

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