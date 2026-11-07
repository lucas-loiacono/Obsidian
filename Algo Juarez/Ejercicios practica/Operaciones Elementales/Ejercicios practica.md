
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