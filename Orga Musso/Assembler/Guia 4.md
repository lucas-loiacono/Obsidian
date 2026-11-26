


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