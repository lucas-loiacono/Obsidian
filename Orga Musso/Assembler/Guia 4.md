


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

## **Pasos de ejecución del programa**

Como `x = 15` e `y = 9`, el programa sigue el siguiente camino:

1. `ld [x], %r1`**:** carga el número 15 en el registro `%r1`.

2. `ld [y], %r2`**:** carga el número 9 en el registro `%r2`.

3. `addcc %r14,-4,%r14`**:** decrementa el puntero de la pila en 4 bytes. Ahora `%r14 = SP - 4`.

4. `st %r1,%r14`**:** almacena el contenido de `%r1` (15) en la posición de memoria apuntada por `%r14`.

5. `addcc %r14,-4,%r14`**:** decrementa nuevamente el puntero de la pila en 4 bytes. Ahora `%r14 = SP - 8`.

6. `st %r2,%r14`**:** almacena el contenido de `%r2` (9) en la posición de memoria apuntada por `%r14`.

7. `call sbr_add`**:** guarda la dirección de la instrucción actual en `%r15` y salta a la subrutina `sbr_add`.

8. `ld %r14,%r8`**:** carga el valor ubicado en el tope de la pila (9) en el registro `%r8`.

9. `addcc %r14,4,%r14`**:** incrementa el puntero de la pila en 4 bytes. Ahora `%r14 = SP - 4`.

10. `ld %r14,%r9`**:** carga el valor ubicado en el tope de la pila (15) en el registro `%r9`.

11. `addcc %r8,%r9,%r10`**:** suma 9 y 15, almacena el resultado 24 en `%r10` y actualiza los códigos de condición.

12. `st %r10,%r14`**:** almacena el resultado de la suma (24) en la posición de memoria apuntada por `%r14`, sobrescribiendo el valor 15.

13. `jmpl %r15+4,%r0`**:** retorna de la subrutina, saltando a la instrucción inmediatamente posterior al `call sbr_add`.

14. `ld %r14,%r3`**:** carga el resultado de la suma (24), ubicado en el tope de la pila, en el registro `%r3`.

15. `addcc %r14,4,%r14`**:** incrementa el puntero de la pila en 4 bytes, recuperando su posición inicial. Ahora `%r14 = SP`.

16. `st %r3,[z]`**:** almacena el contenido de `%r3` (24) en la variable `z`.

17. `ba final`**:** realiza un salto incondicional a la etiqueta `final`.

18. `final: ba final`**:** salta hacia su propia dirección de memoria, generando un bucle infinito.



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



El registro `%r15` se utiliza como **registro de enlace (Link Register)**. Su función es guardar la dirección de memoria de la instrucción `call`, para que posteriormente podamos regresar de una subrutina.

A diferencia de `%r14`, no se utiliza para manejar la pila.

## **Ejemplo con el ejercicio 4.16**

Tenemos las siguientes instrucciones y direcciones de memoria:

```
2072: call sbr_add
2076: ld %r14,%r3
...
2092: sbr_add: ld %r14,%r8
...
2112: jmpl %r15+4,%r0
```

Cuando se ejecuta `call sbr_add`:

- Se guarda 2072 en `%r15`.
    
- Se salta a la dirección 2092, donde comienza la subrutina.
    

Cuando se ejecuta `jmpl %r15+4,%r0`:

- Se calcula `2072 + 4 = 2076`.
    
- Se salta a la dirección 2076, continuando con el programa principal.
    

**%r15 = 2072**

Se conserva la dirección del call durante la subrutina.

## **Diferencia entre los registros especiales**

|Registro|Función|
|---|---|
|`%r0`|Siempre contiene 0.|
|`%r14`|Stack Pointer: apunta al tope de la pila.|
|`%r15`|Link Register: guarda la dirección de la instrucción `call`.|
|`PC`|Program Counter: contiene la dirección de la instrucción que se está ejecutando.|

**Importante:** cada vez que ejecutás un `call`, se sobrescribe `%r15`. Por eso, si una subrutina llama a otra subrutina, normalmente se guarda previamente `%r15` en la pila para no perder la dirección de retorno original.


![[Pasted image 20261126012237.png]]


## **Conceptos nuevos**

`.macro` **y** `.endmacro`

Indican el comienzo y el final de una macro. Una macro es un conjunto de instrucciones que el ensamblador reemplaza directamente en el lugar donde se la invoca.

A diferencia de una subrutina, no necesita utilizar `call`, `jmpl` ni `%r15`.

`.dwb 5`

Reserva cinco palabras adicionales de memoria, es decir, 20 bytes.

`length: 20`

Representa la cantidad de bytes que ocupan los cinco elementos que se van a sumar. Como cada elemento ocupa 4 bytes:

\[ 5\cdot4=20\text{ bytes} \]

## **Pasos de ejecución del programa**

1. `mcr_suma_array array, length, resultado`**:** invoca la macro, reemplazando sus parámetros `pos_array`, `pos_length` y `varResult` por `array`, `length` y `resultado`, respectivamente.

2. `ld [pos_length],%r1`**:** carga el valor 20 en el registro `%r1`.

3. `and %r0,%r0,%r3`**:** realiza un AND entre 0 y 0, inicializando el acumulador `%r3` en 0.

### **Primera iteración**

4. `add %r1,-4,%r1`**:** resta 4 al contenido de `%r1`, quedando `%r1 = 16`.

5. `ld %r1,[pos_array],%r2`**:** carga en `%r2` el elemento ubicado en la dirección base del arreglo más el desplazamiento 16. En este caso, `%r2 = 21`.

6. `add %r2,%r3,%r3`**:** suma 21 y 0, almacenando el resultado 21 en `%r3`.

7. `andcc %r1,%r1,%r0`**:** realiza un AND entre 16 y 16. Como el resultado es distinto de cero, el flag Z queda en 0. El resultado del AND se descarta porque el destino es `%r0`.

8. `be fin`**:** como Z vale 0, no realiza el salto.

9. `ba sumar`**:** salta incondicionalmente a la etiqueta `sumar`, comenzando una nueva iteración.

### **Segunda iteración**

- Se resta 4 a `%r1`, quedando `%r1 = 12`.
    
- Se carga el elemento -5 en `%r2`.
    
- Se suma -5 al acumulador, quedando `%r3 = 16`.
    
- Como `%r1` es distinto de 0, Z vale 0 y se vuelve a `sumar`.
    

### **Tercera iteración**

- Se resta 4 a `%r1`, quedando `%r1 = 8`.
    
- Se carga el elemento 3 en `%r2`.
    
- Se suma 3 al acumulador, quedando `%r3 = 19`.
    
- Como `%r1` es distinto de 0, Z vale 0 y se vuelve a `sumar`.
    

### **Cuarta iteración**

- Se resta 4 a `%r1`, quedando `%r1 = 4`.
    
- Se carga el elemento -32 en `%r2`.
    
- Se suma -32 al acumulador, quedando `%r3 = -13`.
    
- Como `%r1` es distinto de 0, Z vale 0 y se vuelve a `sumar`.
    

### **Quinta iteración**

- Se resta 4 a `%r1`, quedando `%r1 = 0`.
    
- Se carga el elemento 25 en `%r2`.
    
- Se suma 25 al acumulador, quedando `%r3 = 12`.
    
- Se realiza el AND entre 0 y 0, dejando el flag Z en 1.
    
- `be fin` realiza el salto a la etiqueta `fin`.
    
- `st %r3,[varResult]` almacena el valor 12 en la variable `resultado`.




Los parámetros de una macro funcionan de manera similar a los parámetros de una función en C, pero con una diferencia importante: **el ensamblador reemplaza los parámetros por los argumentos que le pasamos antes de ejecutar el programa.**

## **1. Definición de la macro**

La estructura general de una macro en ARC es:

```
.macro nombre_macro parametro1, parametro2, parametro3

    ! Instrucciones

.endmacro
```

En tu ejercicio tenemos:

```
.macro mcr_suma_array pos_array, pos_length, varResult
```

La macro recibe tres parámetros:

- `pos_array`: dirección de memoria donde comienza el arreglo.
    
- `pos_length`: dirección de memoria donde está almacenada la longitud del arreglo en bytes.
    
- `varResult`: dirección de memoria donde se almacenará el resultado.
    

## **2. Invocación de la macro**

En el programa principal tenemos:

```
main: mcr_suma_array array, length, resultado
```

Los argumentos se pasan **por orden de posición**, separados por comas.

En este caso, le estamos pasando las etiquetas que representan las direcciones de memoria, no directamente los valores almacenados en ellas.

## **3. ¿Qué hace el ensamblador?**

Cuando encuentra la invocación de la macro, copia todas sus instrucciones y reemplaza los parámetros por los argumentos correspondientes.

Por ejemplo, esta instrucción de la macro:

```
ld [pos_length],%r1
```

Se transforma en:

```
ld [length],%r1
```

Y esta instrucción:

```
st %r3,[varResult]
```

Se transforma en:

```
st %r3,[resultado]
```

## **4. ¿Cómo queda el código después del reemplazo?**

El ensamblador transforma la invocación de la macro en el siguiente código:

```
main:
    ld [length],%r1
    and %r0,%r0,%r3

sumar:
    add %r1,-4,%r1
    ld %r1,[array],%r2
    add %r2,%r3,%r3
    andcc %r1,%r1,%r0
    be fin
    ba sumar

fin:
    st %r3,[resultado]
```

Es como si hubieras escrito directamente todas esas instrucciones en `main`.

## **5. Diferencia entre una macro y una subrutina**

|Característica|Macro|Subrutina|
|---|---|---|
|Invocación|Nombre de la macro|`call etiqueta`|
|Parámetros|Reemplazados por el ensamblador|Mediante registros, memoria o pila|
|Utiliza `%r15`|No es necesario|Sí, para retornar|
|Necesita `jmpl` para retornar|No|Normalmente sí|
|Código|Se copia en cada invocación|Se reutiliza el mismo bloque|
|Momento del reemplazo o llamada|Ensamblado|Ejecución|

**Lo importante:** una macro no realiza un salto a otro bloque de código. Simplemente reemplaza su invocación por las instrucciones que contiene, sustituyendo sus parámetros por los argumentos que le pasaste.



![[Pasted image 20261126012535.png]]


## **a) ¿Por qué el código no funciona?**

```
.begin
.org 8192

valor .equ 5

var:    valor
        ld [var], %r1
.end
```

Primero, tenemos que entender las siguientes directivas:

- `.org 8192`**:** indica que el código y los datos comienzan en la dirección de memoria 8192.
    
- `valor .equ 5`**:** define una constante llamada `valor` que equivale a 5. No reserva espacio en memoria.
    
- `var: valor`**:** almacena el número 5 en la dirección de memoria 8192.
    

El problema aparece en la instrucción:

```
ld [var], %r1
```

Esta instrucción intenta cargar el contenido de la dirección 8192 en `%r1`.

Sin embargo, el campo inmediato de la instrucción `ld` dispone de solamente **13 bits con signo**, por lo que puede representar valores comprendidos entre:

\[ -2^{12}\leq x\leq 2^{12}-1 \]

\[ -4096\leq x\leq4095 \]

Como la dirección 8192 supera el máximo valor representable (4095), no puede codificarse directamente en el campo inmediato de la instrucción.

Formato de la instrucción ld (32 bits)

**Conclusión del inciso A:** el código no funciona porque la dirección de memoria de `var` es demasiado grande para representarse en el campo inmediato de 13 bits de la instrucción `ld`.

## **b) ¿Por qué el siguiente código resuelve el problema?**

```
.begin
.org 8192

valor .equ 5

var:    valor
        and %r1,%r0,%r1
        sethi %hi(var),%r1
        or %r1,%lo(var),%r1
        ld %r1,%r7
.end
```

La solución consiste en construir la dirección de memoria de 8192 dentro de un registro de 32 bits y luego utilizar ese registro para acceder a memoria.

### **Conceptos nuevos:** `sethi`**,** `%hi` **y** `%lo`

Una dirección de 32 bits se puede dividir en dos partes:

Representación de la dirección 8192 en 32 bits.

- `%hi(var)`**:** obtiene los 22 bits más significativos de la dirección.
    
- `%lo(var)`**:** obtiene los 10 bits menos significativos de la dirección.
    
- `sethi`**:** coloca un valor en los 22 bits superiores del registro destino y pone en 0 los 10 bits inferiores.
    

## **Pasos de ejecución del programa**

**1.** `and %r1,%r0,%r1`

Realiza un AND bit a bit entre `%r1` y 0, inicializando `%r1` en 0.

```
%r1 = 0
```

Esta instrucción es redundante, ya que `sethi` sobrescribe todo el registro.

**2.** `sethi %hi(var),%r1`

Obtiene los 22 bits superiores de la dirección de `var` (8192) y los coloca en los 22 bits superiores de `%r1`.

En este caso:

\[ \%hi(8192)=8 \]

La instrucción `sethi` desplaza ese valor 10 posiciones hacia la izquierda:

\[ 8\cdot 2^{10}=8192 \]

```
%r1 = 8192
```

**3.** `or %r1,%lo(var),%r1`

Realiza un OR bit a bit entre el contenido de `%r1` y los 10 bits inferiores de la dirección de `var`.

Como los 10 bits inferiores de 8192 son todos cero:

```
    00000000 00000000 00100000 00000000
OR  00000000 00000000 00000000 00000000
    -----------------------------------
    00000000 00000000 00100000 00000000
```

El registro `%r1` contiene ahora la dirección completa de `var`.

```
%r1 = 8192
```

**4.** `ld %r1,%r7`

Accede a la posición de memoria apuntada por `%r1` (8192) y carga su contenido (5) en `%r7`.

```
%r7 = 5
```

## **Resultado final**

```
%r1 = 8192
%r7 = 5
```

**Conclusión del inciso B:** el código resuelve el problema utilizando `sethi` y `or` para construir la dirección completa de 32 bits dentro del registro `%r1`. De esta manera, la instrucción `ld` puede acceder a la dirección 8192 sin estar limitada por el campo inmediato de 13 bits.

## **Diferencia entre ambos códigos**

El primero intenta acceder directamente a la dirección:

```
ld [var],%r1       ! No funciona: 8192 no entra en 13 bits
```

El segundo guarda previamente la dirección en un registro:

```
sethi %hi(var),%r1
or %r1,%lo(var),%r1
ld %r1,%r7         ! Funciona: %r1 tiene 32 bits
```

Podés pensarlo como un puntero en C: `%r1` almacena la dirección de memoria y `ld` permite acceder al contenido de esa dirección.











# Sethi

Exactamente. En lugar de pasarle la dirección directamente a la instrucción, primero la cargás en un registro y después trabajás con ese registro.

**Si la dirección entra en los 13 bits**, podés hacer directamente:

```
ld [var], %r1
```

**Si la dirección no entra en los 13 bits**, primero la construís en un registro:

```
sethi %hi(var), %r2
or %r2, %lo(var), %r2
ld %r2, %r1
```

En este último caso:

- `%r2` contiene la dirección de memoria de `var`.
    
- `%r1` recibe el contenido almacenado en esa dirección.
    

El procesador solamente necesita codificar el identificador de `%r2` (5 bits) dentro de la instrucción y luego puede acceder a sus 32 bits de contenido.

Es prácticamente el mismo concepto que un puntero en C: **guardás una dirección en un registro y después accedés a la memoria mediante ese registro.**


# SETHI - Arquitectura ARC

## ¿Para qué sirve?

La instrucción `sethi` permite construir números o direcciones de memoria de 32 bits dentro de un registro cuando estos no pueden representarse directamente en el campo inmediato de una instrucción.

Instrucciones como `ld`, `st`, `add`, `addcc`, `and` y `or` utilizan un campo inmediato de 13 bits con signo.

El rango de valores que pueden representar es:

$$
-2^{12} \leq x \leq 2^{12}-1
$$

$$
-4096 \leq x \leq 4095
$$

Si necesitamos utilizar un valor fuera de este rango, podemos construirlo previamente en un registro mediante `sethi` y `or`.

> [!important]
> La limitación está en el espacio disponible dentro de la instrucción, no en la capacidad de los registros, ya que estos poseen 32 bits.

---

## Funcionamiento de SETHI

### Sintaxis

```asm
sethi inmediato, registro_destino
```

La instrucción `sethi` recibe un inmediato de 22 bits y lo coloca en los 22 bits más significativos del registro destino, completando los 10 bits menos significativos con ceros.

```text
| 22 bits superiores   | 10 bits inferiores |
|      Inmediato       |     0000000000     |
31                    10 9                  0
```

Es equivalente a desplazar el inmediato 10 posiciones hacia la izquierda:

$$
R_d = inmediato \cdot 2^{10}
$$

### Características

- Recibe un inmediato de 22 bits.
- Lo coloca en los 22 bits más significativos.
- Completa los 10 bits menos significativos con ceros.
- Sobrescribe completamente el registro destino.
- No modifica los códigos de condición.
- No accede a la memoria.

---

## Operadores %hi y %lo

Son operadores del ensamblador que permiten dividir un valor de 32 bits en dos partes.

- `%hi(valor)`: obtiene los 22 bits más significativos.
- `%lo(valor)`: obtiene los 10 bits menos significativos.

Matemáticamente, para un valor sin signo:

$$
hi(x) = \left\lfloor \frac{x}{1024} \right\rfloor
$$

$$
lo(x) = x \bmod 1024
$$

Para construir un valor completo de 32 bits:

```asm
sethi %hi(valor), %r1
or %r1, %lo(valor), %r1
```

### Paso 1: SETHI

Coloca los 22 bits superiores y completa con ceros.

```text
|      %hi(valor)      |     0000000000     |
```

### Paso 2: OR

Completa los 10 bits inferiores sin modificar los superiores.

```text
|      %hi(valor)      |     0000000000     |
                      OR
| 0000000000000000000000 |   %lo(valor)     |
------------------------------------------------
|      %hi(valor)      |     %lo(valor)     |
```

De esta manera obtenemos el valor completo de 32 bits.

> [!note]
> Si los 10 bits inferiores del valor son cero, la instrucción `or` puede omitirse.

---

## ¿Por qué funciona utilizando un registro?

Todas las instrucciones de ARC ocupan 32 bits. Dentro de esos 32 bits deben codificarse diferentes campos, como la operación, los registros y el inmediato.

Cuando utilizamos un inmediato, el número debe almacenarse directamente dentro de la instrucción.

Por ejemplo:

```asm
add %r1, 8192, %r3
```

Esta instrucción no puede codificarse porque 8192 no entra en los 13 bits con signo disponibles.

En cambio, podemos hacer:

```asm
sethi %hi(8192), %r2
or %r2, %lo(8192), %r2
add %r1, %r2, %r3
```

Ahora la instrucción `add` no necesita almacenar el número 8192 directamente, sino solamente el identificador del registro `%r2`.

Como ARC posee 32 registros, solamente se necesitan 5 bits para identificar un registro.

$$
2^5 = 32
$$

El identificador de `%r2` es:

```text
00010
```

El procesador identifica el registro y luego obtiene sus 32 bits de contenido para realizar la operación.

> [!important]
> Cuando pasamos un registro a una instrucción, no estamos codificando su contenido dentro de la instrucción, sino solamente su identificador.

---

## Ejemplo 1: Cargar una dirección de memoria

```asm
.begin
.org 8192

valor .equ 5
var: valor

main:
    sethi %hi(var), %r1
    or %r1, %lo(var), %r1
    ld %r1, %r7

.end
```

La variable `var` se encuentra en la dirección de memoria 8192 y contiene el número 5.

### ¿Por qué no podemos utilizar LD directamente?

```asm
ld [var], %r7
```

La dirección 8192 no entra en los 13 bits del campo inmediato de `ld`.

El problema no es el valor 5 almacenado en memoria, sino la dirección 8192 donde se encuentra.

### Pasos de ejecución

1. `sethi %hi(var), %r1`

   Carga los 22 bits superiores de la dirección 8192 en `%r1`.

   Como `%hi(8192) = 8`:

   $$
   r1 = 8 \cdot 1024 = 8192
   $$

2. `or %r1, %lo(var), %r1`

   Completa los 10 bits inferiores de la dirección.

   Como `%lo(8192) = 0`:

   $$
   r1 = 8192
   $$

3. `ld %r1, %r7`

   Accede a la dirección de memoria almacenada en `%r1` y carga su contenido en `%r7`.

### Resultado final

```text
%r1 = 8192  (dirección de memoria)
%r7 = 5     (contenido de esa dirección)
```

Es un concepto similar al de los punteros en C: almacenamos una dirección y luego accedemos al contenido de esa dirección.

---

## Ejemplo 2: Construir el número 8200

```asm
sethi %hi(8200), %r1
or %r1, %lo(8200), %r1
```

Calculamos ambas partes:

$$
hi(8200) = 8
$$

$$
lo(8200) = 8
$$

### Primera instrucción

```asm
sethi %hi(8200), %r1
```

$$
r1 = 8 \cdot 1024 = 8192
$$

### Segunda instrucción

```asm
or %r1, %lo(8200), %r1
```

$$
r1 = 8192 \text{ OR } 8 = 8200
$$

En binario:

```text
8192 = 00000000 00000000 00100000 00000000
   8 = 00000000 00000000 00000000 00001000
                     OR
-----------------------------------------
8200 = 00000000 00000000 00100000 00001000
```

Resultado final: `%r1 = 8200`.

---

## Diferencia entre inmediato y registro

| Característica | Inmediato | Registro |
|---|---|---|
| Tamaño del valor | 13 bits con signo | 32 bits |
| Qué se codifica | El valor directamente | El identificador del registro |
| Bits del identificador | No corresponde | 5 bits |
| Permite utilizar 8192 | No | Sí |

---

## Resumen

> [!summary] SETHI
> - Permite construir valores y direcciones de 32 bits.
> - Se utiliza cuando un valor no entra en el campo inmediato de 13 bits.
> - `sethi` carga los 22 bits superiores.
> - `%hi` obtiene los 22 bits superiores.
> - `%lo` obtiene los 10 bits inferiores.
> - `or` completa los 10 bits inferiores.
> - El valor completo queda almacenado en un registro.
> - Luego podemos utilizar ese registro en instrucciones como `ld`, `st`, `add`, `and`, etc.

La idea principal es no pasarle un número o una dirección demasiado grande directamente a una instrucción, sino construirlo previamente en un registro y trabajar con dicho registro.