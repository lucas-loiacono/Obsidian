


![[Pasted image 20261126001735.png]]


El código arranca en `main` con `%r1 = 0` y `array` ubicado en la dirección `12` (`0x0C`, justo después de las tres instrucciones de 4 bytes cada una), y recorre los pasos siguientes:

1. **`nop` (dir. `0`)**: No hace nada; solo avanza el `%pc` a `4`.
    
2. **`addcc %r1, 4, %r1` (dir. `4`)**: Suma `0 + 4` y guarda `4` en `%r1` (actualizando las flags en `0`). El `%pc` pasa a `8`.
    
3. **`ld %r1, [array+8], %r7` (dir. `8`)**: Calcula la dirección efectiva sumando `%r1 + array + 8` (`4 + 12 + 8 = 24`, que corresponde a `array + 12`, el cuarto elemento del arreglo) y carga su valor, **`5`**, en `%r7`. El `%pc` pasa a `12`.
    

En resumen: prepara un desplazamiento de `4` bytes en `%r1` y lee `array[3]` (`5`) hacia `%r7`.

|**Instrucción**|**Dirección (Decimal)**|**Dirección (Hexadecimal)**|**Posición relativa a main**|
|---|---|---|---|
|`nop`|`0`|`0x00000000`|`main + 0`|
|`addcc %r1, 4, %r1`|`4`|`0x00000004`|`main + 4`|
|`ld %r1, [array+8], %r7`|`8`|`0x00000008`|`main + 8`|
como no tengo el org empieza en la direccion 0


### ) Código de máquina real vs. Directivas al ensamblador

- **Líneas que generan código de máquina real (instrucciones ejecutables por la CPU):** Son traducidas por el ensamblador a palabras binarias de 32 bits con su respectivo _opcode_ y operandos:
    
    1. `nop` _(en ARC se ensambla como `sethi 0, %g0`, palabra `0x01000000`)_
        
    2. `addcc %r1, 4, %r1`
        
    3. `ld %r1, [array+8], %r7`
        
- **Líneas que NO generan instrucciones de máquina (directivas, etiquetas y definición de datos):**
    
    - **Directivas al ensamblador propiamente dichas:**
        
        - `.begin` (marca el inicio del ensamblado).
            
        - `.end` (marca el final del ensamblado).
            
    - **Etiquetas simbólicas (referencias de dirección para el ensamblador):**
        
        - `main:`
            
        - `array:`


![[Pasted image 20261126002741.png]]

Como la variable `valor` contiene el número 25, el programa sigue el siguiente camino:

1. `ld [valor], %r1`**:** carga el número 25 en el registro `%r1`.

2. `andcc %r1,1,%r1`**:** realiza un AND bit a bit entre 25 y 1. El resultado es 1, que se almacena en `%r1`. Como el resultado es distinto de cero, el flag Z queda en 0.

3. `be espar`**:** verifica si el flag Z vale 1. Como Z vale 0, no realiza el salto y continúa con la siguiente instrucción.

4. `ba esimpar`**:** realiza un salto incondicional a la etiqueta `esimpar`, omitiendo las instrucciones del bloque `espar`.

5. `or %r0,0,%r2`**:** realiza un OR entre 0 y 0, almacenando el resultado 0 en `%r2`.

6. `or %r0,1,%r3`**:** realiza un OR entre 0 y 1, almacenando el resultado 1 en `%r3`.

7. `ba fin`**:** realiza un salto incondicional a la etiqueta `fin`.

8. `fin: ba fin`**:** salta hacia su propia dirección de memoria, generando un bucle infinito.

**Conclusión:** el programa determina que 25 es impar, dejando el registro `%r2` en 0 y el registro `%r3` en 1.


### **Inicio del programa**

- `.begin`**:** directiva que indica al ensamblador el comienzo del programa.
    
- `main:` etiqueta que identifica el comienzo del código principal.
    
- `ld [valor], %r1`**:** carga el contenido de la posición de memoria `valor` (25) en el registro `%r1`.
    
- `andcc %r1,1,%r1`**:** realiza una operación AND bit a bit entre `%r1` y 1, almacena el resultado en `%r1` y actualiza los códigos de condición. Si el resultado es 0, el flag Z se activa; de lo contrario, queda en 0.
    
- `be espar`**:** realiza un salto a la etiqueta `espar` si el flag Z vale 1.
    
- `ba esimpar`**:** realiza un salto incondicional a la etiqueta `esimpar`.
    

### **Bloque espar**

- `espar:` etiqueta que identifica el bloque que se ejecuta si el número es par.
    
- `or %r0,1,%r2`**:** realiza un OR bit a bit entre 0 y 1, almacenando 1 en `%r2`.
    
- `or %r0,0,%r3`**:** realiza un OR bit a bit entre 0 y 0, almacenando 0 en `%r3`.
    
- `ba fin`**:** realiza un salto incondicional a la etiqueta `fin`.
    

### **Bloque esimpar**

- `esimpar:` etiqueta que identifica el bloque que se ejecuta si el número es impar.
    
- `or %r0,0,%r2`**:** realiza un OR bit a bit entre 0 y 0, almacenando 0 en `%r2`.
    
- `or %r0,1,%r3`**:** realiza un OR bit a bit entre 0 y 1, almacenando 1 en `%r3`.
    
- `ba fin`**:** realiza un salto incondicional a la etiqueta `fin`.
    

### **Datos y finalización**

- `valor: 25`**:** etiqueta que identifica una posición de memoria donde se almacena el número 25.
    
- `fin: ba fin`**:** realiza un salto incondicional hacia su propia dirección de memoria, generando un bucle infinito.
    
- `.end`**:** directiva que indica al ensamblador el final del programa.

![[Pasted image 20261126004752.png]]

## **Pasos de ejecución del programa**

Como `sumando1 = 10` y `sumando2 = 15`, el programa sigue el siguiente camino:

1. `call sumar`**:** guarda la dirección de la instrucción actual en `%r15` y salta a la subrutina `sumar`.
    
2. `ld [sumando1], %r1`**:** carga el número 10 en el registro `%r1`.
    
3. `ld [sumando2], %r2`**:** carga el número 15 en el registro `%r2`.
    
4. `addcc %r1,%r2,%r3`**:** suma el contenido de `%r1` y `%r2`, almacena el resultado 25 en `%r3` y actualiza los códigos de condición.
    
5. `jmpl %r15+4, %r0`**:** retorna de la subrutina `sumar`, saltando a la instrucción siguiente al `call sumar`.
    
6. `or %r3,%r0,%r1`**:** realiza un OR bit a bit entre 25 y 0, almacenando el resultado 25 en `%r1`.
    
7. `call esimpar`**:** guarda la dirección de la instrucción actual en `%r15` y salta a la subrutina `esimpar`.
    
8. `andcc %r1,1,%r4`**:** realiza un AND bit a bit entre 25 y 1. Almacena el resultado 1 en `%r4` y actualiza los códigos de condición, dejando el flag Z en 0.
    
9. `jmpl %r15+4, %r0`**:** retorna de la subrutina `esimpar`, saltando a la instrucción siguiente al `call esimpar`.
    
10. `st %r3,[resultado]`**:** almacena el contenido de `%r3` (25) en la posición de memoria `resultado`.
    
11. `st %r4,[paridad]`**:** almacena el contenido de `%r4` (1) en la posición de memoria `paridad`.
    
12. `ba fin`**:** realiza un salto incondicional a la etiqueta `fin`.
    
13. `fin: ba fin`**:** salta hacia su propia dirección de memoria, generando un bucle infinito.


La instrucción `jmpl %r15+4, %r0` sirve, en este ejercicio, para **volver de una subrutina al lugar desde donde fue llamada**.

Para entenderla, primero tenés que entender cómo funciona `call`.

## **1. ¿Qué hace** `call sumar`**?**

Supongamos que las instrucciones están en las siguientes direcciones de memoria (comenzando desde la dirección 0):

|Dirección|Instrucción|
|---|---|
|16|`call sumar`|
|20|`or %r3,%r0,%r1`|
|24|`call esimpar`|
|...|...|
|40|`sumar: ld [sumando1],%r1`|

Cuando se ejecuta `call sumar`, ocurren dos cosas:

- Se guarda la dirección de la instrucción `call` en `%r15`, es decir, `%r15 = 16`.
    
- Se salta a la dirección de la etiqueta `sumar`, es decir, 40.
    

## **2. ¿Qué hace** `jmpl %r15+4, %r0`**?**

Cuando termina la subrutina, necesitamos volver a la instrucción que está inmediatamente después del `call`.

Como cada instrucción ocupa 4 bytes:

\[ \%r15+4=16+4=20 \]

Por lo tanto, se salta a la dirección 20.

● Llamada● Retorno

## **3. ¿Por qué se utiliza** `%r0`**?**

La instrucción `jmpl` realiza dos operaciones:

- Guarda la dirección de la propia instrucción `jmpl` en el registro destino.
    
- Salta a la dirección calculada por el primer operando.
    

Como no nos interesa guardar la dirección del `jmpl`, utilizamos `%r0` como destino. Este registro siempre vale 0 y no permite modificar su contenido, por lo que se descarta ese valor.

## **4. ¿Qué pasaría si no sumamos 4?**

Si escribiéramos:

```
jmpl %r15, %r0
```

Volveríamos a la dirección 16, donde está el `call sumar`, y llamaríamos nuevamente a la subrutina, repitiendo el proceso indefinidamente.

Por eso se suma 4.

**En resumen:**

```
call sumar          ! Llama a la subrutina
jmpl %r15+4, %r0    ! Retorna de la subrutina
```

Podés pensar en `jmpl %r15+4, %r0` como el equivalente a un `return` de una función en C, pero a nivel de instrucciones del procesador.


![[Pasted image 20261126010724.png]]

Casi, pero es al revés. En este ejercicio, **la pila crece hacia las direcciones de memoria más bajas**.

El registro `%r14` efectivamente apunta al tope de la pila (Stack Pointer).

- `%r14 - 4`**:** reserva espacio para un nuevo elemento en la pila.
    
- `%r14 + 4`**:** libera el espacio del elemento que está en el tope de la pila.
    

Ninguna de estas operaciones escribe ni elimina físicamente datos de la memoria. Solamente modifica el puntero.

## **Ejemplo práctico**

Supongamos que inicialmente `%r14 = 1000`.

1. Estado inicial

2. Restamos 4 y almacenamos el número 15

```
addcc %r14,-4,%r14
st %r1,%r14
```

Ahora %r14 = 996. Tenemos un elemento en la pila.

3. Sumamos 4 al puntero

```
addcc %r14,4,%r14
```

Ahora %r14 = 1000. El número 15 sigue en memoria, pero ya no pertenece a la pila activa.

## **PUSH y POP**

Para agregar un elemento a la pila (**PUSH**):

```
addcc %r14,-4,%r14
st %r1,%r14
```

Primero reservás espacio y después almacenás el dato.

Para retirar un elemento de la pila (**POP**):

```
ld %r14,%r1
addcc %r14,4,%r14
```

Primero recuperás el dato y después liberás el espacio.

**Lo importante es que liberar espacio no significa borrar el dato.** El dato sigue estando en memoria hasta que otra operación lo sobrescriba.

Podés pensarlo de manera similar a manejar un puntero en C: modificar el puntero no modifica el contenido de la memoria a la que apuntaba anteriormente.