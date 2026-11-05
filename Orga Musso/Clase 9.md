![[Pasted image 20261105020209.png]]

![[Pasted image 20261105020253.png]]

![[Pasted image 20261105020449.png]]

La imagen "image_a99e02.jpg" detalla la estructura a nivel de bits de los **Cinco formatos de instrucción** en código de máquina para la arquitectura ARC. Muestra cómo los 32 bits de cada instrucción se dividen en "campos" específicos que la Unidad de Control decodifica para saber qué hacer.

  

Los bloques y campos fundamentales que estructuran estos formatos son:

  

- **Campo `op` (Bits 31-30):** Son los dos bits más significativos y determinan la categoría principal de la instrucción. Según la tabla inferior izquierda, si los bits son `00` el formato es SETHI/Branch, si son `01` es CALL, si son `10` es Aritmética, y si son `11` es de Memoria.
    
      
    
- **Campos de Registros (`rd`, `rs1`, `rs2`):** Son bloques de 5 bits que le indican a la CPU qué registros específicos utilizar para el destino (`rd`) o las fuentes (`rs1`, `rs2`). Al tener 5 bits, permiten apuntar exactamente a cualquiera de los 32 registros del procesador ($2^5 = 32$).
    
      
    
- **Códigos de Operación Secundarios (`op2`, `op3`):** Se utilizan para especificar la instrucción exacta dentro de una categoría general. Por ejemplo, dentro del formato aritmético (`op=10`), la tabla inferior muestra que el campo `op3` distingue si la operación será una suma (`010000` para `addcc`), una operación lógica (`010001` para `andcc`), o el fin de una subrutina (`111000` para `jmpl`).
    
      
    
- **El Bit `i` (Bit 13):** En los formatos Aritméticos y de Memoria, este bit actúa como un interruptor. Si vale `0`, la instrucción utilizará el contenido de un segundo registro apuntado en `rs2`. Si vale `1`, la instrucción tomará los últimos 13 bits (`simm13`) directamente como un número entero (constante inmediata) para realizar la operación.
    
      
    

Desglose de los formatos presentados:

  

- **CALL format:** Es el diseño más directo. Utiliza sus 2 bits iniciales (`op=01`) para identificarse y destina los 30 bits restantes (`disp30`) exclusivamente para almacenar la dirección a la que debe saltar para invocar la subrutina.
    
      
    
- **SETHI / Branch Format:** Ambos comparten el código principal `op=00` y utilizan el campo `op2` para diferenciarse entre sí (`100` para sethi, `010` para branch). El formato Branch incluye además un campo `cond` de 4 bits que define bajo qué condición matemática se realizará el salto (ej. `0001` para `be`, que salta si los valores son iguales).
    
      
    
- **Arithmetic y Memory Formats:** Comparten una distribución interna casi idéntica, organizando los bits para designar el registro destino, la operación específica (`op3`) y los operandos fuente. Se diferencian por su código principal (`10` para cálculos en la ALU y `11` para operaciones de carga y guardado en RAM).


![[Pasted image 20261105021115.png]]

![[Pasted image 20261105021335.png]]