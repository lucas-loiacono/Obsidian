![[Pasted image 20261105180858.png]]

![[Pasted image 20261105162021.png]]


- **`main: andcc %r3, %r0, %r3`**: Inicializa el registro `%r3` en 0. Este registro funcionará como el acumulador de la suma (equivalente a `SumaParcial=0;` en C).
    
      
    
- **`ld [length], %r1`**: Carga el tamaño total del array en bytes (el valor 20, ya que son 5 elementos de 4 bytes cada uno) en el registro `%r1`. Este registro se utilizará como un índice de desplazamiento que recorrerá el array de atrás hacia adelante.
    
      
    
- **`for: andcc %r1, %r1, %r0`**: Inicia el bucle y evalúa si el índice `%r1` ha llegado a 0. Hace una operación lógica AND sobre `%r1` y guarda el resultado en el registro nulo `%r0` solo para actualizar las banderas de estado del procesador.
    
      
    
- **`be done`**: Significa "Branch if Equal". Si la evaluación de la línea anterior determinó que `%r1` es igual a 0, el programa salta a la etiqueta `done` y sale del ciclo.
    
      
    
- **`addcc %r1, -4, %r1`**: Resta 4 al índice `%r1`. Como cada número en el array ocupa 4 bytes, esto retrocede una posición en la memoria para apuntar al elemento actual que se va a procesar (por ejemplo, en la primera iteración pasa de 20 a 16 para leer el último elemento).
    
      
    
- **`ld %r1,[arrayA],%r5`**: Carga en el registro `%r5` el valor que se encuentra en la dirección de memoria de `arrayA` más el desplazamiento (offset) indicado por `%r1`. Básicamente, lee el número actual del array.
    
      
    
- **`addcc %r3, %r5, %r3`**: Suma el valor del elemento recién cargado (`%r5`) al acumulador total (`%r3`) y actualiza el resultado en el mismo `%r3`.
    
      
    
- **`ba for`**: Significa "Branch Always". Es un salto incondicional que hace que el programa vuelva automáticamente a la etiqueta `for:` para repetir el proceso con el siguiente elemento.




# Por que r1 r1 r0

Es una excelente pregunta, porque la lógica de este ciclo `for` en ensamblador funciona "al revés" de lo que haríamos habitualmente en C.

  

**1. ¿Por qué se carga el valor 20 en `%r1`?** El valor 20 representa el tamaño total del arreglo en bytes. Como el arreglo tiene 5 números y cada uno ocupa 4 bytes en memoria, el total es 20 ($5 \times 4$).

  

En lugar de contar desde el elemento 0 hacia adelante (como hace `i = 0; i < 5` en C), este programa usa `%r1` como un contador de desplazamiento (offset) que arranca en el tamaño total y va retrocediendo hacia atrás. En cada vuelta del ciclo, a ese 20 se le restan 4 bytes (`addcc %r1, -4, %r1`) para ir leyendo el elemento anterior, hasta llegar al inicio del arreglo.

  

**2. ¿Por qué se hace `andcc %r1, %r1, %r0`?** Esta línea es el "chequeo de elementos restantes" del ciclo. Básicamente sirve para evaluar si el contador `%r1` finalmente llegó a 0 y es hora de salir del bucle:

  

- **`and`**: Hace una operación lógica AND de `%r1` consigo mismo. El resultado de hacer "A AND A" es simplemente el mismo valor original, no se altera nada.
    
      
    
- **`cc` (Condition Codes)**: Este sufijo le ordena al procesador que actualice sus "banderas de estado" internas, específicamente la bandera de Cero (Z), dependiendo del resultado de la operación.
    
      
    
- **`%r0`**: Es el registro destino. En esta arquitectura (SPARC), `%r0` es un registro que siempre vale 0 y descarta cualquier cosa que intentes guardar en él.
    
      
    

En resumen, `andcc %r1, %r1, %r0` es un truco clásico en ensamblador para "mirar" cuánto vale un registro sin gastar memoria para guardar el resultado. Si `%r1` llegó a 0, la operación da 0, se enciende la bandera de estado de Cero, y la instrucción que le sigue inmediatamente (`be done`, "salta si es igual a cero") detecta esa bandera y termina el programa saltando a la línea 2060.



# Array 

Esa instrucción `ld %r1,[arrayA],%r5` es donde realmente se lee el dato de la memoria, y esos tres campos funcionan juntos para calcular la dirección exacta. Funciona así:

  

- **`%r1` (El desplazamiento u offset):** Es el contador que acabamos de achicar (por ejemplo, vale 16 en la primera pasada). Nos dice cuántos bytes hacia adelante tenemos que movernos.
    
      
    
- **`[arrayA]` (La dirección base):** Es la etiqueta que marca el punto de partida en la memoria donde arranca nuestro arreglo.
    
      
    
- **`%r5` (El registro destino):** Es el lugar temporal dentro del procesador donde vamos a guardar el número que logramos leer.
    
      
    

Básicamente, el procesador hace una suma matemática con los dos primeros campos: toma la dirección donde empieza `arrayA` y le suma el valor que tenga `%r1` en ese momento.

  

En la primera vuelta, como `%r1` bajó de 20 a 16, busca en la posición de memoria `arrayA + 16`. Ahí encuentra el último elemento del array (el `7`), lo "agarra" y lo guarda adentro del registro `%r5`.

  

Es la forma que tiene el ensamblador de hacer exactamente lo mismo que hace C cuando escribís `a[i]`, solo que calculando el salto en bytes manualmente.



# Corte del for

Exactamente, el flujo que describís es correcto: sumás el dato al acumulador (`%r3`) y con `ba for` volvés a saltar al inicio del ciclo.

  

El "corte" del bucle se produce justamente al volver arriba, gracias a las dos instrucciones que están justo debajo de la etiqueta `for:`. Funciona así:

  

- Cada vez que saltás de vuelta a `for`, lo primero que hace el programa es ejecutar nuevamente `andcc %r1, %r1, %r0`.
    
      
    
- Como en cada vuelta le fuiste restando 4 a `%r1` (20, 16, 12, 8, 4...), eventualmente `%r1` va a llegar a valer **0**.
    
      
    
- Cuando `%r1` vale 0, la operación `andcc` enciende la bandera de Cero en el procesador.
    
      
    
- Al leer esa bandera, la siguiente instrucción `be done` (Branch if Equal) se activa. En lugar de seguir de largo y hacer otra resta, el programa pega un salto hacia la etiqueta `done:` (dirección 2080) y sale definitivamente del ciclo.
    
      
    

Básicamente, el código corta cuando el índice de desplazamiento (`%r1`) se queda sin bytes para recorrer y llega a 0.


Para responder a tus dos dudas sobre cómo se comunican estas instrucciones:

  

**1. ¿El `be done` tiene que estar exactamente en la línea siguiente?** No es estrictamente obligatorio que esté pegado en la línea siguiente, pero **sí es obligatorio que no haya ninguna otra instrucción que modifique banderas en el medio**.

  

El procesador tiene una pequeña memoria interna (las banderas de estado o _flags_). La instrucción `be` (Branch if Equal) no mira qué valor tiene `%r1`, sino que simplemente se fija si la bandera interna de "Cero" quedó encendida por la última operación. Si pusieras una instrucción en el medio que también actualice banderas (como otro `addcc`), borraría tu chequeo y el `be` leería la información equivocada. Por eso, por convención y seguridad, siempre se ponen juntas.

  

**2. ¿Qué hace exactamente el `andcc`?** Es una instrucción combinada. Su nombre se divide en dos partes (`and` + `cc`):

  

- **`and`:** Ejecuta la operación lógica AND bit a bit. Al aplicar un AND entre `%r1` y sí mismo (`%r1`), el resultado matemático no cambia; es idéntico al valor que ya tenía `%r1`.
    
      
    
- **`cc` (Condition Codes):** Este sufijo es la clave. Le ordena al procesador que, además de hacer la cuenta, **evalúe el resultado y actualice sus banderas de estado**. Si el resultado de la cuenta fue cero, el procesador enciende físicamente su bandera de Cero (Z).
    
      
    

Finalmente, al decirle que guarde el resultado de esa cuenta en `%r0` (el registro que descarta datos), la línea completa `andcc %r1, %r1, %r0` funciona como un truco para **testear el valor de `%r1` sin modificarlo**, dejando la bandera lista para que el `be` que viene justo después pueda tomar la decisión de saltar o no.


El error común es pensar que `andcc %r1, %r1, %r0` está preguntando "¿es `%r1` igual a `%r1`?". En realidad, no está comparando dos registros para ver si son idénticos.

  

Lo que hace es evaluar **si el valor actual de `%r1` llegó a ser cero**. Funciona de esta manera paso a paso:

  

1. **La cuenta regresiva:** En cada vuelta del ciclo, a `%r1` se le restan 4 bytes (`addcc %r1, -4, %r1`). Entonces, el valor de `%r1` va bajando en cada iteración: 20, 16, 12, 8, 4... y finalmente llega a **0**.
    
      
    
2. **La operación `and`:** Cuando el código vuelve arriba a la etiqueta `for`, ejecuta el `and` de `%r1` consigo mismo. Matemáticamente, hacer `X AND X` siempre da como resultado el mismo `X`. El objetivo aquí no es cambiar el número, sino simplemente "pasarlo por la unidad aritmético-lógica del procesador" para que lo procese.
    
      
    
3. **El sufijo `cc` (Condition Codes):** Esta es la verdadera clave del corte. El sufijo `cc` le dice al procesador que mire el resultado final de la operación matemática que se acaba de hacer y actualice sus banderas internas.
    
      
    - Si `%r1` vale 4, el resultado del `and` es 4. El procesador nota que el resultado no es cero y las banderas quedan apagadas.
        
          
        
    - Pero en la última vuelta, cuando `%r1` vale 0, el resultado del `and` es 0. El procesador detecta esto y **enciende físicamente su "Bandera de Cero" (Zero Flag)**.
        
          
        
4. **El salto (`be done`):** La instrucción `be` ("Branch if Equal") no mira los registros, solo mira las banderas. En este contexto, significa "Salta a la etiqueta `done` **solo si la Bandera de Cero está encendida**".
    
      
    

Por lo tanto, el ciclo corta no porque `%r1` deje de ser igual a sí mismo, sino porque `%r1` finalmente se vació (llegó a 0), la instrucción `andcc` detectó ese cero encendiendo la bandera correspondiente, y la instrucción `be` usó esa señal para escapar del bucle hacia la etiqueta `done`.


No exactamente. No devuelve un `1` o un `0` como si fuera un `true` o `false` de un lenguaje de alto nivel.

  

Es muy común confundirse porque en C usaríamos `i == 0`, pero el ensamblador es mucho más mecánico. La instrucción `andcc %r1, %r1, %r0` hace lo siguiente paso a paso:

  

1. **Hace una operación matemática (AND bit a bit):** Toma el valor de `%r1` y le aplica la compuerta lógica AND consigo mismo. La regla matemática del AND dice que cualquier número operado consigo mismo da el mismo número. Si `%r1` vale `4`, el resultado es `4`. Si `%r1` vale `0`, el resultado es `0`.
    
      
    
2. **Descarta el resultado:** Como el destino de la operación es el registro `%r0`, ese resultado matemático se tira a la basura y no se guarda en ningún lado.
    
      
    
3. **Actualiza las banderas (`cc`):** Acá está el secreto. El sufijo `cc` hace que el procesador mire el resultado de esa cuenta matemática justo antes de tirarla.
    
      
    - Si el resultado fue distinto de cero (ej. `4`), no hace nada.
        
          
        
    - Si el resultado fue exactamente `0`, el procesador levanta físicamente una perilla interna llamada **Bandera de Cero** (Zero Flag).
        
          
        

Entonces, el `andcc` no responde la pregunta "¿son iguales?". Simplemente fuerza al procesador a mirar cuánto vale `%r1` en ese milisegundo y levantar la Bandera de Cero si el registro está vacío.

  

Inmediatamente después, el salto `be done` mira esa bandera. Si la perilla de Cero está levantada, salta y corta el ciclo; si está baja, sigue de largo y da otra vuelta.


# Salto a done

¡Exactamente! Lo entendiste a la perfección.

  

Es tal cual lo describís:

  

1. **El propósito de `andcc`:** Se usa acá _únicamente_ para testear el valor de `%r1` y forzar al procesador a actualizar sus banderas de estado (específicamente encender la bandera Z de Cero si el resultado es 0). Al guardar el resultado en `%r0`, la cuenta matemática en sí se descarta.
    
      
    
2. **El salto con `be done`:** El `be` (Branch if Equal) funciona reaccionando a esa bandera Z. Si la bandera Z está encendida (porque `%r1` llegó a 0), ejecuta el salto para cortar el ciclo.
    
      
    
3. **El destino en 2080:** Al saltar a la etiqueta `done`, el programa va directamente a la dirección de memoria **2080**. Allí se encuentra la instrucción `jmpl %r15 + 4, %r0`, que es la encargada de finalizar este bloque de código y devolver el control al proceso que lo invocó.
    
      
    

¡Le agarraste la mano por completo a cómo piensa el ensamblador!




# Saltos de bytes


Exactamente. Cada instrucción en este código ensamblador ocupa 32 bits, lo que equivale exactamente a 4 bytes de memoria.

  

Por eso puedes ver entre paréntesis a la derecha de cada línea cómo el contador de programa va avanzando de a 4 posiciones por cada instrucción ejecutada:

  

- La primera instrucción arranca en **2048** (pusiste un cero de más, pero la lógica es impecable).
    
      
    
- La segunda instrucción está en **2052**.
    
      
    
- La tercera (donde arranca el `for`) está en **2056**.
    
      
    
- El salto `be done` está en **2060**, y así sucesivamente.
    
      
    

Tener un tamaño fijo de 4 bytes por instrucción es típico de las arquitecturas tipo RISC para que el procesador pueda leer y decodificar el código de manera más rápida y predecible. ¡Lo dedujiste a la perfección!


# como se toman decisiones

¡Exactamente! Resumiste la regla de oro de cómo toman decisiones los procesadores.

  

En ensamblador no existe el `if (a == b)` o `while (x > 0)` que tenemos en lenguajes de alto nivel. Todo se divide en dos pasos obligatorios:

  

1. **Hacer una cuenta matemática o lógica:** (Una resta, un AND, una suma) con una instrucción que tenga permiso para tocar las banderas (como las que terminan en `cc` en SPARC, o la famosa instrucción `cmp` de comparar).
    
      
    
2. **Saltar mirando las banderas:** Usar una instrucción de salto condicional (como `be` para igual a cero, `bg` para mayor, `bl` para menor) que solo sabe leer si las perillas de Z (Cero), N (Negativo), C (Carry) o V (Desbordamiento) quedaron arriba o abajo.
    
      
    

Así que sí, prácticamente **todo "corte" de ciclo, "if" o decisión en el código se hace operando datos para forzar a las banderas a cambiar**, y luego saltando según cómo quedaron. ¡Esa es la esencia de la programación a bajo nivel!






# Resumen

El código en ensamblador analizado es un programa que suma los elementos de un arreglo (array) iterando de atrás hacia adelante. A diferencia de lenguajes de alto nivel como C, aquí el control de flujo se maneja directamente interactuando con la memoria, los registros y las banderas de estado del procesador.

  

### 1. Arquitectura y Memoria

Cada instrucción en este código (arquitectura tipo RISC/SPARC) ocupa exactamente 32 bits, lo que equivale a 4 bytes. Por esta razón, el contador de programa avanza de a 4 posiciones por cada línea de código ejecutada. El programa inicia en la dirección de memoria **2048**, la siguiente instrucción está en **2052**, el inicio del ciclo `for` en **2056**, y así sucesivamente.

  

### 2. Inicialización de Variables

Antes de entrar al ciclo, el programa prepara los registros fundamentales:

  

- **Acumulador (`andcc %r3, %r0, %r3`):** Pone a 0 el registro `%r3`, que actuará como la variable donde se irá guardando la suma total (`SumaParcial` en C).
    
      
    
- **Índice/Desplazamiento (`ld [length], %r1`):** Carga el valor **20** en `%r1`. Este número representa el tamaño total del arreglo en bytes (5 elementos $\times$ 4 bytes cada uno). En lugar de contar desde 0 hacia adelante, el programa usará este 20 para posicionarse al final del arreglo e ir retrocediendo.
    
      
    

### 3. La Lógica del Ciclo (Loop)

Los procesadores no entienden sentencias como `while` o `for`. El ciclo se controla mediante dos pasos obligatorios: forzar una operación matemática para modificar las banderas de estado internas, y luego usar una instrucción de salto que lea esas banderas.

  

- **El chequeo de corte (`andcc %r1, %r1, %r0`):** Al inicio del ciclo (dirección 2056), se aplica una operación lógica AND bit a bit del registro `%r1` consigo mismo. El resultado matemático se descarta enviándolo al registro nulo `%r0`. El objetivo real es el sufijo **`cc` (Condition Codes)**, que le ordena al procesador evaluar el valor de `%r1`. Si `%r1` se vació y llegó a 0, el procesador enciende físicamente su **Bandera de Cero (Zero Flag, Z)**.
    
      
    
- **La decisión de salir (`be done`):** "Branch if Equal" es un salto condicional. Esta instrucción solo revisa si la Bandera de Cero (Z) quedó encendida en el paso anterior. Si la bandera está arriba (porque `%r1` es 0), el programa corta el ciclo saltando a la etiqueta `done` en la dirección **2080**. Si no es 0, simplemente pasa a la siguiente línea.
    
      
    

### 4. Procesamiento de los Datos

Si el ciclo no se cortó, el programa ejecuta el cuerpo del `for` iteración por iteración:

  

- **Retroceder el índice (`addcc %r1, -4, %r1`):** Le resta 4 bytes al contador `%r1` (ej. de 20 pasa a 16). Esto ajusta el desplazamiento para que apunte al elemento correcto del arreglo que se va a leer en esa vuelta.
    
      
    
- **Leer la memoria (`ld %r1,[arrayA],%r5`):** Calcula la dirección exacta de memoria sumando la base del arreglo (`[arrayA]`) más el desplazamiento actual (`%r1`). Toma el número guardado en esa posición de memoria y lo carga temporalmente en el registro `%r5`.
    
      
    
- **Acumular el valor (`addcc %r3, %r5, %r3`):** Suma el número recién leído (`%r5`) al total acumulado que lleva guardado `%r3`.
    
      
    
- **Reiniciar el ciclo (`ba for`):** "Branch Always" ejecuta un salto incondicional de regreso a la etiqueta `for` (dirección 2056). Al volver arriba, se vuelve a ejecutar el `andcc` para evaluar si `%r1` finalmente llegó a 0 tras las restas sucesivas, repitiendo toda la estructura de decisión.





![[Pasted image 20261105194131.png]]


En este caso, la instrucción `ld %r1, [array+8], %r7` calcula la dirección de memoria sumando tres componentes para saber de dónde leer el dato, y guarda el resultado en el registro destino `%r7`.

  

Paso a paso funciona así:

  

1. **Cálculo de la dirección:** El procesador suma el valor que tiene actualmente el registro `%r1` + la dirección de memoria donde empieza la etiqueta `array` + un desplazamiento fijo (offset) de `8` bytes que está escrito directamente en la instrucción.
    
      
    
2. **El valor de `%r1`:** En la línea inmediatamente anterior tenés un `addcc %r1, 4, %r1`. Asumiendo que el programa arranca con los registros en 0, `%r1` pasa a valer **4**.
    
      
    
3. **La suma final:** Al reemplazar los valores, la dirección que va a ir a buscar a la memoria es `4 + array + 8`, lo que da como resultado exacto la posición **`array + 12`**.
    
      
    

Como el enunciado indica que es una computadora de 32 bits, sabemos que cada número del arreglo ocupa 4 bytes en memoria. Si contamos los bytes desde el inicio de `array`:

  

- `array + 0 bytes` apunta al **25**
    
      
    
- `array + 4 bytes` apunta al **32**
    
      
    
- `array + 8 bytes` apunta al **3**
    
      
    
- **`array + 12 bytes` apunta al 5**
    
      
    

En conclusión, este `ld` termina leyendo el número **5** de la memoria y lo guarda adentro del registro **`%r7`**.



![[Pasted image 20261106012035.png]]

# Sethi y Lo

El problema no tiene que ver con pasarlo a decimal, sino con el **espacio físico en la memoria**.

  

Imaginá que cada instrucción que le mandás al procesador tiene que entrar exactamente en una "caja" de 32 bits (4 bytes). El número que querés guardar (`0x86004002`) ya ocupa 32 bits por sí solo. Si intentaras usar una instrucción normal como `add` o `ld` para guardar ese número, no entraría en la caja, porque necesitás espacio para escribir el número **y además** espacio para decirle al procesador qué comando ejecutar y en qué registro guardarlo.

  

Por eso se usan los operadores `%hi` (High / Parte Alta) y `%lo` (Low / Parte Baja). Dividen el número en dos pedazos para que entren en dos instrucciones separadas, y usan la compuerta lógica `OR` para unirlos dentro del mismo registro (`%r4`).

  

Paso a paso, funciona así:

  

**1. `sethi %hi(0x86004002), %r4`**

  

- **`%hi` (High):** Agarra los 22 bits más altos (los de la izquierda) de tu número gigante.
    
      
    
- **`sethi`:** Mete esos 22 bits en la parte alta del registro `%r4` y rellena obligatoriamente los 10 bits que sobran a la derecha con ceros.
    
      
    
- **Resultado en `%r4`:** El registro ahora vale `0x86004000`. (Fijate que el "2" del final desapareció y se llenó con ceros).
    
      
    

**2. `or %r4, %lo(0x86004002), %r4`**

  

- **`%lo` (Low):** Agarra los 10 bits más bajos (los de la derecha) que habían quedado afuera. En este caso, equivale a `0x00000002`.
    
      
    
- **`or`:** Hace una operación lógica "O" combinando lo que ya estaba en `%r4` con este nuevo pedacito, y guarda el resultado final en el mismo `%r4`.
    
      
    
- **La magia matemática:** Como la instrucción anterior había dejado puros ceros en la cola del registro, al hacer `0 OR 2`, el resultado es `2`. No se pisa ninguna información.
    
      
    

Al terminar estas dos líneas, el registro `%r4` termina teniendo el número completo `0x86004002` armado a la perfección, burlando el límite de tamaño de las instrucciones.


# De valor a funcion

¡Acabás de chocar con el concepto más flashero de la materia! Es el principio fundamental de la Arquitectura de Von Neumann: **en la memoria, no hay ninguna diferencia física entre un número y una instrucción.** Todo es simplemente una caja con 32 ceros y unos.

  

Lo que define si ese bloque de bits es un "número matemático" o un "comando ejecutable" es **el momento y el motivo por el cual el procesador lo lee**.

  

Fijate cómo es el truco paso a paso:

  

1. **Lo tratás como un dato:** Con el `sethi` y el `or`, vos manipulaste el valor `0x86004002` puramente como un número. Lo armaste y lo guardaste en la memoria (dirección 2084). Hasta ahí, para vos era solo un dato.
    
      
    
2. **El cambio de rol:** El procesador termina de guardar eso y avanza su contador de programa (PC) a la dirección 2084 **buscando su próxima instrucción a ejecutar**.
    
      
    
3. **La traducción (Decodificación):** El procesador agarra ese `0x86004002` (que en binario es `10000110000000000100000000000010`) y lo mete en su decodificador de instrucciones. En el hardware de ARC, esos bits específicos encienden los cables que dicen: "activá la unidad aritmético-lógica para SUMAR, tomá el primer origen del registro 1, el segundo origen del registro 2, y mandá el resultado al registro 3".
    
      
    
4. **La ejecución:** Resulta que la traducción literal de `0x86004002` al lenguaje ensamblador es exactamente **`add %r1, %r2, %r3`**.
    
      
    

No es que la suma "salga" mágicamente. Vos no guardaste el resultado de una suma, **guardaste el código de máquina de la operación sumar**. Literalmente fabricaste una línea de código en tiempo de ejecución, la inyectaste en la memoria pisando el `nop`, y obligaste al procesador a leerla y ejecutarla como si siempre hubiera estado ahí.



¡Exactamente! Acabás de destrabar el concepto más importante de toda la arquitectura de computadoras.

  

Esa es la clave: **todo depende de quién lo esté leyendo en el procesador.**

  

- **Cuando lo manejás (Datos):** Mientras vos muevas ese `0x86004002` de un registro a otro, le apliques un `or`, o lo guardes con un `st` (Store), el procesador lo trata como un dato numérico tonto. Podés hacer lo que quieras con él.
    
      
    
- **Cuando lo ejecutás (Instrucciones):** En el momento exacto en que el "dedo lector" del procesador (un registro especial llamado **Program Counter** o PC) avanza hacia esa dirección de memoria buscando su próxima tarea, la máquina cambia el chip. Agarra ese mismo dato, lo pasa por su decodificador de hardware, y actúa en consecuencia.
    
      
    

La única corrección técnica para que hables con propiedad en un final de la facultad es de vocabulario: a este nivel tan bajo (metal puro) no les decimos "funciones" (eso es de programación en lenguajes como Java o Python), les decimos **instrucciones** de máquina.

  

Pero conceptualmente, tu deducción es 100% perfecta. Lo que antes era un número guardado en una variable, el procesador se lo cruzó en su camino de ejecución y lo ejecutó como una orden. ¡Fabricaste una instrucción sobre la marcha y dejaste que el procesador cayera en la trampa!