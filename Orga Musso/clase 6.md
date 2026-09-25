
![[Pasted image 20260922071205.png]]

Karnaugh se hace complicado con mas de 4 variables, para esto esta este nuevo método


![[Pasted image 20260922072111.png]]

tengo que identificar los que tienen igual cantidad de unos

![[Pasted image 20260922072524.png]]

los tengo que sumar, con el guion lo que hago es eliminar la variable que cambia

![[Pasted image 20260922072734.png]]

![[Pasted image 20260922072942.png]]

una vez que reduje , ahora tengo que seguir reduciendo


![[Pasted image 20260922073338.png]]


como el 4 no esta en ninguno de los anteriores lo tengo que agregar con su pareja

![[Pasted image 20260922073417.png]]

lo mismo para el 10

![[Pasted image 20260922073449.png]]

![[Pasted image 20260922073621.png]]

De aca saco los implicante primo esenciales


![[Pasted image 20260922073816.png]]










Circuitos combinacionales

![[Pasted image 20260922073927.png]]

![[Pasted image 20260922073948.png]]

![[Pasted image 20260922074022.png]]

![[Pasted image 20260922074146.png]]

Acá las palabras son a0 y a1,  y b0 y b1. Palabra a y palabra b

![[Pasted image 20260922075257.png]]


![[Pasted image 20260922075719.png]]




![[Pasted image 20260922075958.png]]


El concepto de "reducir" y "devolver al original" está bien orientado en cuanto a la cantidad de cables o líneas físicas del circuito, pero la diferencia principal radica en qué formato tiene la información en cada extremo.

- **El Codificador:** Recibe múltiples señales de entrada individuales y le asigna un código binario de salida a la señal que esté aplicada al dispositivo. Es decir, pasa de una "posición física" (muchas líneas de entrada, donde generalmente se enciende de a una) a un formato comprimido en "código binario" (pocas líneas de salida).
    
 
- **El Decodificador:** Realiza exactamente el trabajo inverso. Detecta la presencia de una combinación específica de valores lógicos (un código binario) en sus entradas y, en base a eso, activa una sola de sus múltiples líneas de salida. Pasa del "código binario" de vuelta a una "posición física" específica.


Para visualizarlo en la práctica, imaginá un teclado de computadora conectado a un monitor:

Cuando presionás la tecla del número '9', estás activando mecánicamente una sola línea física. Un **codificador** integrado en el teclado toma esa única señal física y la transforma ("comprime") en un código binario corto para que el procesador de la computadora lo pueda leer e interpretar.

Por otro lado, cuando la computadora decide que tiene que prender una luz indicadora específica en un panel, le envía un código binario a un **decodificador**. Este componente lee el código y activa exclusivamente la única línea eléctrica de salida que enciende esa luz en particular.

habilitación lee la entrada, si mi A0 =1 la salida 1 va a estar activa y la de 0 no, ósea mis respectivos c


Exactamente, tu razonamiento es muy acertado. Las salidas **C** ($C_0, C_1, C_2, C_3$) representan esos "cables" individuales o líneas físicas de destino.

Lo que "devuelve" el decodificador no es un código nuevo, sino la **activación de uno solo de esos cables** dependiendo exclusivamente del número binario que ingresó. Actúa como un distribuidor que lee una dirección en formato binario y enciende únicamente la salida correspondiente a esa dirección.

Si mirás la tabla del **Decodificador de dos entradas** en la imagen, podés ver exactamente a qué cable le da la señal (el valor '1') según el código que recibe en las entradas $A_1$ y $A_0$:


- Si entra el código binario **00** (cero en decimal), enciende solo el cable **$C_0$**.

- Si entra el código binario **01** (uno en decimal), enciende solo el cable **$C_1$**.

- Si entra el código binario **10** (dos en decimal), enciende solo el cable **$C_2$**.

- Si entra el código binario **11** (tres en decimal), enciende solo el cable **$C_3$**.

Por lo tanto, si conectaras un codificador y un decodificador juntos, el decodificador efectivamente estaría volviendo a encender "el cable original" que inició todo el proceso del otro lado, traduciendo ese binario intermedio de vuelta a una posición física.

![[Pasted image 20260922080408.png]]



- El **codificador** toma la activación de una señal física en una de sus múltiples entradas y la traduce entregando un código binario en sus salidas.
    
- El **decodificador** hace el camino inverso: recibe un código binario en sus entradas y lo traduce activando una única señal física de salida correspondiente a ese valor.

Son procesos completamente complementarios. ¡Muy buena deducción!

![[Pasted image 20260922080442.png]]

![[Pasted image 20260922080644.png]]

Esta imagen muestra una aplicación muy práctica del decodificador: usarlo como un **Generador de Funciones Lógicas**. Básicamente, te enseña cómo aprovechar ese comportamiento de "encender un solo cable" que vimos antes para implementar cualquier tabla de verdad de manera muy sencilla.

El proceso funciona así:

- **El objetivo:** Mirá la tabla de verdad de la izquierda. Se busca crear un circuito cuya salida $F$ sea '1' únicamente cuando las entradas (A, B, C) representan los números decimales 1, 3, 5 o 7. Esto se resume en la ecuación matemática $F(A,B,C) = \sum(1,3,5,7)$.
    
- **El decodificador:** Se utiliza un decodificador estándar donde las entradas del circuito (A, B, C) se conectan a los pines receptores ($A_0, A_1, A_2$). El pin de habilitación ($E$) se conecta directamente a $VCC$ (+5 voltios) para que el circuito esté encendido y funcionando permanentemente.
    
- **La magia de la compuerta OR:** Como ya sabemos, si ingresa por ejemplo el número 3 en binario (011), el decodificador va a encender exclusivamente el "cable" de salida $D_3$. Para lograr que la salida final $F$ se active con los valores deseados (1, 3, 5 o 7), simplemente se toman los cables de salida $D_1, D_3, D_5$ y $D_7$ y se conectan todos juntos a una **compuerta OR**.


De esta forma, si el decodificador recibe cualquiera de esos cuatro códigos binarios, encenderá su cable respectivo, la compuerta OR detectará esa señal y devolverá un '1' en la salida $F$, cumpliendo perfectamente con la tabla de verdad requerida.

![[Pasted image 20260922081910.png]]

Un **multiplexor** es básicamente un selector electrónico. Es un circuito combinacional que recibe información digital desde varias líneas de entrada diferentes y dirige solo una de ellas hacia una única línea de salida compartida.

Para entenderlo visualmente, podés mirar el esquema de la derecha en la imagen: el circuito funciona como una llave o un interruptor de múltiples posiciones. Para que el dispositivo sepa exactamente cuál de todas las entradas de datos debe conectar físicamente con la salida, utiliza un segundo grupo de conexiones llamadas **entradas de control** o selector.

La regla matemática que lo define indica que para un multiplexor de $2^n$ líneas de entrada, siempre se van a necesitar $n$ entradas de control. Estas entradas de control reciben un número binario que le indica al interruptor qué canal debe abrir.  

El esquema inferior izquierdo muestra el **Multiplexor de Una Entrada de Control**, que es la versión más básica para entender el concepto:


- Tiene dos líneas de entrada de datos (D0 y D1) y una única salida final (Y).
    
- Utiliza una sola línea de control (S) que actúa como selector.
    
- Dependiendo del valor binario que ingrese por ese cable selector S (que puede ser '0' o '1'), el circuito hace un "puente" interno y deja pasar la información de D0 o la de D1 hacia la salida Y.

![[Pasted image 20260922082017.png]]

Tus dos canales de entrada de datos son efectivamente $D_1$ y $D_0$. La letra **$S$** significa **Selector** y funciona como tu entrada de control.

Siguiendo la analogía anterior, $S$ es el "botón" que decide cuál de los dos canales se conecta a la pantalla (la salida $Y$). La tabla de verdad en el centro de la imagen muestra exactamente cómo toma la decisión:

- Si la señal en **$S$ es 0**, el multiplexor elige el canal **$D_0$** y deja pasar su información a la salida $Y$.
    
- Si la señal en **$S$ es 1**, el multiplexor cambia de posición y conecta el canal **$D_1$** a la salida $Y$.

El diagrama gris a la derecha muestra cómo se construye esa "llave" físicamente en el hardware: el valor de $S$ se usa para encender (habilitar) una sola compuerta lógica AND a la vez, bloqueando el paso de un canal y permitiendo el paso del otro hacia la salida final.

![[Pasted image 20260922082130.png]]

![[Pasted image 20260922082448.png]]

![[Pasted image 20260922082640.png]]

![[Pasted image 20260922082745.png]]


El **demultiplexor** hace exactamente la operación inversa al multiplexor. Es un circuito combinacional que recibe información de **una sola línea de entrada** y la transmite o distribuye a **una de varias líneas de salida posibles**.

  
Siguiendo con el ejemplo de la tele, imaginate el caso contrario: tenés un solo decodificador de cable o una sola consola (tu única entrada de datos) pero tenés cables yendo a 4 pantallas distintas en diferentes habitaciones (tus múltiples salidas).

¿Cómo decidís a qué pantalla mandar la imagen? Usando nuevamente las **entradas de control (o selector $S$)**. El valor binario que le pases a ese selector actúa como la "llave" que direcciona la señal de entrada hacia una pantalla específica, bloqueando el paso hacia el resto.

  
**Un dato clave de diseño lógico:**

Estructuralmente, un demultiplexor es idéntico al **decodificador** que vimos un par de imágenes atrás. Para usar un decodificador como demultiplexor, se hace lo siguiente:


- Conectás tu señal de entrada (el dato que querés transmitir) directamente al pin general de **Habilitación ($E$)**.

- Usás las entradas normales del decodificador ($A_1, A_0$) como tus pines **selectores ($S$)**.

Dependiendo del código binario que pongas en esos selectores, la señal de datos va a salir por una y solo una de las líneas de salida ($C_0, C_1, C_2$ o $C_3$).

![[Pasted image 20260922083656.png]]

![[Pasted image 20260922084117.png]]

![[Pasted image 20260922084328.png]]

![[Pasted image 20260922084750.png]]

**Lo que es 100% correcto:** Sí, **vos elegís los valores de $R$ y $S$** para forzar los cambios. Esos son tus pines de control externos. Si querés guardar un '1', activás $S$ (Set); si querés borrarlo y guardar un '0', activás $R$ (Reset). Y si los dejás quietos ($S='0'$ y $R='0'$), el circuito usa su memoria y retiene el último estado que elegiste

El circuito siempre tiene un estado lógico inicial girando en ese bucle. Ese cableado cruzado o "ciclo" es el mecanismo que **mantiene** el valor atrapado y guardado indefinidamente, actuando como la memoria del dispositivo.

Tus pines externos $R$ y $S$ entran en juego justamente para esos "ciertos casos" en los que necesitás intervenir. La dinámica se divide en dos partes:

  
- **El ciclo de retroalimentación:** Se encarga de la retención. Mientras no envíes ninguna orden ($R='0'$ y $S='0'$), el ciclo asegura que la salida siga siendo exactamente la misma, alimentándose a sí misma.
    
- **Las entradas ($R$ y $S$):** Son tus comandos de escritura. Cuando activás uno de ellos con un '1', rompés temporalmente la inercia del ciclo y forzás a las compuertas a cambiar el estado de la salida.
    

Una vez que dejás de enviar esa señal por $R$ o $S$ (volviéndolos a '0'), el ciclo vuelve a tomar el control y deja "atrapado" al nuevo valor que acabás de establecer. Esta lógica exacta es la piedra angular de cómo se construye un bit de memoria estática en la arquitectura de cualquier computadora. ¿Queda más claro cómo interactúan ambas partes ahora?

![[Pasted image 20260922084950.png]]
`
q y q' son salidas y entradas a la vez, ya que la primera vez que entran, entran con el valor de la memoria, entran al circuito y salen por el mismo lugar solo que con el valor cambiado en ciertos casos

MI Q Y Q' estaban al principio en un valor logico 0 y 1, pero una vez que retroalimento cambian, dependiendo de mi r y s, y se quedan estables, ya que si realimento sigue dando el mismo valor

![[Pasted image 20260922090058.png]]

como después de la retroalimentación me dio q y notq el mismo valor, ósea 0, es incoherente, por lo cual no tiene sentido

![[Pasted image 20260924015658.png]]

aca tenggo mis valores de r y s, y el resultado es que devuelve despues de la retroalimentacion

![[Pasted image 20260924015828.png]]

esto me da mi estado inicial y el resultado al que quiero llegar, y cuales serian los valores que tienen que tomar mi r y s para ese caso


![[Pasted image 20260924020119.png]]

¡Ah, excelente observación! Estás mirando los cuadros de abajo (los mapas de Karnaugh) exactamente en la fila donde **RS = 00**.


Efectivamente, si leés esa fila de izquierda a derecha, ves un **0** y luego un **1**. Lo que tenés que mirar son los encabezados de las columnas para entender por qué están esos números ahí:

Los números que están _adentro_ de las casillas representan el resultado final, es decir, el valor de **$Q_{n+1}$** (el estado siguiente). Las dos columnas separan los dos escenarios posibles de tu memoria actual (**$Qn$**):

- **Primera columna ($Qn = 0$):** Si mirás la intersección con la fila RS=00, el resultado adentro es **0**. Esto se lee así: si el circuito ya tenía guardado un 0 ($Qn=0$) y vos no le enviás ninguna señal de cambio ($R=0, S=0$), el estado siguiente se queda en 0 ($Q_{n+1}=0$).
    
- **Segunda columna ($Qn = 1$):** Si mirás la intersección con la fila RS=00, el resultado adentro es **1** (que está encerrado en el círculo rojo). Esto se lee así: si el circuito ya tenía guardado un 1 ($Qn=1$) y vos no le enviás ninguna señal de cambio ($R=0, S=0$), el estado siguiente se queda en 1 ($Q_{n+1}=1$).
    

Por eso ves un "0" y un "1" en esa fila. El cuadro simplemente te está mostrando en formato visual que, cuando $R$ y $S$ valen cero (estado de retención), el resultado $Q_{n+1}$ copia exactamente el mismo valor que tenía la columna $Qn$ correspondiente.



También puedo conseguir sus funciones

![[Pasted image 20260924020442.png]]

![[Pasted image 20260924020630.png]]

El biestable J-K (Jack Kilby) es una mejora directa del biestable RS, diseñada para solucionar su principal limitación: el estado prohibido.

- **Estructura interna:** Como se ve en el primer esquema, el núcleo del circuito J-K es literalmente un biestable RS convencional. La diferencia física radica en que se agregan compuertas AND a las nuevas entradas J y K, y se conectan cables de retroalimentación adicionales que viajan desde las salidas (Q y Not Q) de vuelta hacia estas compuertas de entrada.
    
- **Comportamiento similar:** Analizando la "Tabla Reducida", el J-K actúa de forma casi idéntica al RS en tres de sus cuatro combinaciones. Si ingresás J=0 y K=0, el circuito mantiene su memoria (Qn). Si J=1 y K=0, actúa como el comando Set y guarda un 1. Si J=0 y K=1, actúa como el comando Reset y guarda un 0.
    
- **La diferencia clave:** La ventaja del J-K se evidencia cuando activás ambas entradas a la vez (J=1 y K=1). En el circuito RS, ingresar dos unos simultáneos generaba un error lógico o estado "Prohibido". En el J-K, gracias a esa retroalimentación cruzada extra, esta combinación ahora es funcional y hace que el biestable invierta su valor actual (Not Qn). Esto significa que si tenía guardado un 0, pasará a 1; y si tenía un 1, pasará a 0.

El circuito interno funciona conectando una sola salida a cada compuerta AND de entrada:

- **Para llegar a S:** La compuerta AND de arriba toma tu entrada **$J$** y la conecta exclusivamente con la salida de abajo, es decir, **Not Q** (o $Q'$).
    
- **Para llegar a R:** La compuerta AND de abajo toma tu entrada **$K$** y la conecta exclusivamente con la salida de arriba, que es **$Q$**.
    

Por lo tanto, al núcleo interno le llegan exactamente estas operaciones lógicas: $S = J \cdot Q'$ y $R = K \cdot Q$.

Ese cableado cruzado es justamente el truco maestro de este diseño. Como $Q$ y $Q'$ siempre tienen valores opuestos (si uno es '1', el otro obligatoriamente es '0'), las compuertas AND actúan como un filtro de seguridad.

Si vos intentás forzar el error mandando $J=1$ y $K=1$ al mismo tiempo, la retroalimentación cruzada se asegura de que solo una de las compuertas AND se active (la que esté conectada a la salida que actualmente valga '1'). Así, al núcleo RS interno siempre le llega la orden correcta para invertir su estado (Not Qn) en lugar de bloquearse en un estado prohibido


¡Exactamente! Lo entendiste a la perfección. Ese "volver a entrar al circuito" es el corazón de todo este tema.


En diseño digital, a ese cableado se lo llama **retroalimentación cruzada**.

Las compuertas lógicas básicas por sí solas no tienen memoria; si les cortás la señal de entrada, su salida desaparece al instante. Pero al agarrar los cables de salida (Q y Q') y obligarlos a volver hacia atrás para entrar en las compuertas del lado opuesto, creás un **bucle infinito de validación**.

Funciona como un mecanismo donde las dos salidas se sostienen mutuamente:

1. Si **Q** logró ponerse en '1', ese '1' viaja por el cable de retroalimentación hacia la compuerta de abajo.
    
2. Al recibir ese '1', la compuerta de abajo es forzada a apagar su salida, garantizando que **Not Q** sea '0'.
    
3. Ese '0' viaja por el otro cable de retroalimentación hacia la compuerta de arriba, lo que le confirma a la de arriba que debe mantener a **Q** en '1'.
    
Es un sistema que se auto-mantiene. Gracias a que las salidas vuelven a entrar, cuando vos dejás de mandar órdenes externas (por ejemplo, dejás las entradas R y S en 0), el circuito no se "apaga". Se queda trabado en ese bucle, reteniendo el último estado para siempre (mientras la computadora siga encendida).



![[Pasted image 20260924020913.png]]

Estos dos circuitos son simplificaciones muy prácticas que se construyen utilizando como base el biestable J-K que acabamos de ver. Al agrupar las entradas J y K de distintas maneras, logran comportamientos específicos:

  
- **Biestable "D" (Data):** Está diseñado específicamente para almacenar un bit de información.
    
      
    - Como muestra el esquema, tiene una sola entrada $D$. Esta entrada se conecta directamente a la terminal J del bloque J-K interno, y pasa por una compuerta NOT (inversora) antes de llegar a la terminal K. Esto asegura que J y K siempre reciban valores opuestos.
        
    
    - Su comportamiento es el más simple de todos: la "Tabla Reducida" y su Ecuación Característica ($Q_{n+1} = D$) indican que la salida siempre va a copiar exactamente el valor que le pongas en la entrada. Si ingresás un 0, guarda un 0; si ingresás un 1, guarda un 1.
        
          
        
- **Biestable "T" (Toggle):** Su función principal es alternar o "bascular" el estado de la salida, como si fuera el botón de encendido/apagado de un control remoto.
    
      
    - En este diseño físico, la única entrada $T$ se ramifica y se conecta directamente tanto a J como a K al mismo tiempo.
        
    
    - Según su "Tabla Reducida", si la entrada $T$ es 0, el circuito simplemente retiene su memoria actual ($Q_{n+1} = Q$).
        
    - Pero si la entrada $T$ es 1, el circuito invierte o cambia de estado ($Q_{n+1} = Q'$). Su Ecuación Característica formaliza esto como $Q_{n+1} = T \cdot (\text{Not } Q_n) + (\text{Not } T) \cdot Q_n$.



Como los esquemas muestran un bloque J-K en su interior, si "abrimos" esa cajita, vamos a encontrar exactamente la misma estructura que vimos en la imagen del biestable Jack Kilby: un núcleo SR que tiene esas compuertas AND en sus entradas (recibiendo J y K) junto con los cables de retroalimentación cruzada desde las salidas.

  

Lo que hacen estos diseños D y T es tomar ese circuito J-K completo (con sus compuertas AND ya incluidas adentro) y simplemente cambiar cómo se conectan los cables _por fuera_ para forzarlo a hacer tareas específicas:

  

- En el **Biestable D**, le ponen una compuerta NOT externa en la pata K para asegurarse de que las compuertas AND internas siempre reciban valores opuestos.
    
- En el **Biestable T**, simplemente empalman el mismo cable a las patas J y K para que ambas compuertas AND internas reciban la misma señal simultáneamente.

Así que sí, toda la "magia" de evitar los estados prohibidos gracias a esas compuertas AND sigue estando presente adentro de estos dos nuevos circuitos.








# Resumen

Las diferencias principales radican en la cantidad de entradas y en la función específica para la que fue optimizada su memoria:


- **Biestable R-S (Reset-Set):** Es la estructura base original. Tiene dos entradas independientes donde S (Set) graba un 1 y R (Reset) borra a 0. Su mayor desventaja es su vulnerabilidad lógica: si recibe un 1 en ambas entradas simultáneamente, entra en un estado lógico prohibido o inestable.
    
    
- **Biestable J-K:** Es la versión perfeccionada del R-S. Mantiene las dos entradas, pero incorpora la retroalimentación cruzada para solucionar el estado prohibido. Si recibe la orden simultánea (1,1), en lugar de colapsar, ejecuta una orden segura de alternancia (invierte el valor actual de su memoria).
    
      
- **Biestable D (Data):** Es una especialización orientada a la integridad de los datos. Tiene una sola entrada de información (D) y utiliza una compuerta NOT interna para garantizar que al núcleo nunca le lleguen señales iguales. Simplemente "copia y retiene" el valor de la entrada en la salida. Es la pieza ideal para almacenar bits de forma pura.
    
    
- **Biestable T (Toggle):** Es otra especialización de una sola entrada, lograda al unir físicamente los pines J y K. Funciona como el botón de encendido de un control remoto: si T recibe un 0, retiene su estado; si recibe un 1, bascula hacia el estado opuesto. Es el componente central para diseñar circuitos contadores.


![[Pasted image 20260924162839.png]]

A diferencia de los circuitos anteriores (que reaccionaban de forma inmediata a cualquier cambio en sus entradas), estos introducen el concepto clave de **Sincronización** mediante una **Señal de reloj** o `clk` (clock).


En los modelos que veníamos viendo, si vos cambiabas el valor de una entrada, la salida cambiaba al instante (circuitos asincrónicos). En estos sistemas secuenciales sincronizados, el circuito funciona con un "director de orquesta" (el reloj) que emite una onda cuadrada periódica que alterna entre 0 y 1 a lo largo del tiempo. El biestable solo tiene permitido "leer" sus entradas y cambiar su memoria en los momentos precisos que le dicta este reloj.

La segunda imagen detalla los tipos de sincronización posibles:

- **Por Nivel:** El circuito se habilita y "escucha" a sus entradas durante todo el lapso de tiempo en el que el reloj se mantiene en un estado estable, que puede ser **Nivel 1** (alto) o **Nivel 0** (bajo). Si mirás la última imagen, el **Biestable R-S Sincronizado por Nivel Alto** se construye agregándole simplemente dos compuertas AND controladas por el pin `clk`. Si el `clk` envía un '1', la compuerta se abre y deja pasar tus órdenes R y S hacia el núcleo del circuito. Si envía un '0', se bloquea e ignora lo que hagas.
    
  
- **Por Flanco:** Es un control de tiempo mucho más estricto y veloz. El circuito solo se habilita para leer las entradas en el instante milimétrico en el que la señal de reloj está transicionando de un nivel a otro: ya sea cuando sube de 0 a 1 (**Flanco Ascendente**) o cuando cae de 1 a 0 (**Flanco Descendente**). Fuera de ese instante exacto de transición, el circuito queda ciego a cualquier cambio en las entradas.

Exactamente. El pin `clk` (clock) es por donde ingresa físicamente esa señal que está constantemente alternando entre 1 y 0.

Sin embargo, hay que hacer una pequeña distinción para no mezclar los conceptos, ya que al final mencionaste "cuando hay un flanco":

- En la imagen que muestra el circuito armado (**Biestable "R-S" Sincronizado por Nivel Alto**), la activación **no es por flanco**, sino por **nivel**. Esto significa que las compuertas de entrada se "abren" y el circuito se activa durante _todo el tiempo_ que la señal `clk` se mantenga en el valor 1 (toda la línea plana superior de la onda). En el momento que `clk` baja a 0, las compuertas se bloquean y el circuito se desactiva.
    
- Si el circuito estuviera diseñado para funcionar verdaderamente **por flanco** (como mostraba el esquema con las flechas verticales de la imagen anterior), su comportamiento sería distinto: no se mantendría activado durante todo el tiempo que dura el "1", sino que solo se activaría en el instante exacto y milimétrico en el que la señal pega el salto de 0 a 1 (flanco ascendente).

En resumen: sí, el `clk` es tu cable que trae los 1 y 0. Pero es el diseño del circuito el que decide si va a "prestar atención" durante todo el rato que dura ese 1 (nivel), o si solo va a reaccionar en el instante del cambio (flanco).

  

¿Se logra visualizar esa sutil pero importante diferencia en los tiempos de activación?

![[Pasted image 20260924162956.png]]

![[Pasted image 20260924163121.png]]


Como el pin `clk` está conectado directamente a las dos compuertas AND de la entrada, si el reloj marca **'0'**, la multiplicación lógica (AND) obliga a que el resultado de ambas compuertas sea '0', sin importar qué valores estés intentando mandar por tus cables R o S.


¿Y qué pasaba cuando al núcleo de un biestable R-S le llegaban dos ceros? Como vimos en las tablas anteriores, entraba automáticamente en su **estado de memoria o retención**.

  

Así es como funciona el "bloqueo" físico: al mandar un '0', el reloj anula tus señales R y S y obliga al circuito interno a recibir (0,0), asegurándose de que no haga otra cosa más que retener el dato que ya tenía guardado de antes. Recién cuando el `clk` vuelve a subir a '1', las compuertas AND se "abren" y dejan pasar el verdadero valor de tus señales R y S hacia el núcleo.

  

Si mirás con detalle el esquema del **Biestable "D" Sincronizado por Nivel Alto** en la imagen, vas a notar que en el centro hay un bloque rectangular interno que ya tiene sus pines J, K, Q, Q' y **su propia entrada etiquetada como `clk`**.

  
Lo que sucede en la práctica es lo siguiente:

- Las compuertas AND que controlan el paso de la señal no desaparecieron, sino que **ya están integradas adentro** de ese bloque central J-K.
    
- El diseño del biestable D simplemente agarra un circuito J-K (que ya viene sincronizado de fábrica) y le agrega la entrada D con su compuerta NOT por fuera.
    
- El cable `clk` que ves entrar viaja directo hacia el interior de ese bloque central para cumplir la misma función de barrera.
    
El mecanismo es idéntico: cuando el `clk` manda un '0', las compuertas internas de ese bloque J-K se cierran, ignorando por completo cualquier cambio que hagas en la entrada D. Recién cuando el reloj manda un '1', el bloque interno se "despierta", lee si en D pusiste un 0 o un 1, y actualiza su memoria.

![[Pasted image 20260925010920.png]]

Esta es la solución ingeniosa para lograr que un circuito funcione verdaderamente **"Por Flanco"** (reaccionando solo en el instante del salto) utilizando los componentes que funcionaban por nivel. Se conoce como **Sincronización Maestro-Esclavo**.

Para lograrlo, el circuito encadena dos biestables R-S internamente:

1. El primero es el **Maestro**, que recibe tus señales externas S y R.
    
2. El segundo es el **Esclavo**, que está conectado a las salidas del Maestro y es el que entrega el resultado final del circuito.

El "truco" está en cómo se conecta la señal de reloj (`clk`): Si observás el esquema de la izquierda, el cable de `clk` se divide. Va directo hacia el Esclavo, pero para entrar al Maestro pasa primero por un pequeño círculo (un inversor o compuerta NOT). Esto significa que trabajan en turnos opuestos, como muestra el **Diagrama Temporal**:

- **Cuando el reloj está en '0':** El Maestro está activo y se encarga de leer y procesar los cambios que hagas en S y R ("Q del Maestro conmuta"). Mientras tanto, el Esclavo está bloqueado e ignora al Maestro, manteniendo intacta la salida final ("Q del Esclavo no conmuta").
    
- **En el instante que el reloj salta a '1' (Flanco Ascendente):** Los roles se invierten. El Maestro se bloquea automáticamente y congela el dato que acababa de leer ("Q del Maestro no cambia"). En ese mismísimo instante, el Esclavo se activa, lee el dato congelado por el Maestro y lo copia en la salida final ("Q del Esclavo cambia").

El resultado de esta carrera de relevos es que **la salida final del sistema solo se actualiza en el microsegundo exacto en que la señal de reloj pasa de 0 a 1**, logrando la sincronización por flanco. En la "Simbología" a la derecha, esto se representa dibujando un pequeño **triángulo** en la entrada del reloj, indicando que este componente es sensible a los flancos y no a los niveles fijos.

![[Pasted image 20260925010822.png]]

Este circuito es una alternativa ingeniosa para lograr la sincronización por flanco (Edge Triggered), pero usando un truco físico con los tiempos de retardo de las compuertas en lugar de acoplar dos biestables enteros como en el sistema Maestro-Esclavo.


Si analizás el esquema de la izquierda, la señal de reloj principal (la línea **`a`**) se divide en dos caminos antes de entrar a la compuerta AND verde:

- El camino de abajo (**`c`**) va directo, sin alteraciones.
    
- El camino de arriba pasa por una compuerta NOT (inversor), convirtiéndose en la señal **`b`**.
    

La "magia" ocurre por un detalle físico del mundo real: las compuertas lógicas no son instantáneas. La compuerta NOT tarda una mínima fracción de segundo en procesar la electricidad y cambiar su salida.

Si mirás el diagrama temporal de abajo, podés ver cómo se aprovecha ese retraso:

1. Cuando la señal `a` pega el salto de 0 a 1 (un flanco ascendente), la señal de abajo `c` copia ese salto a '1' inmediatamente.
    
2. Sin embargo, la señal de arriba `b` (que estaba en '1' porque invierte el '0' inicial) tarda un microsegundo en darse cuenta de que tiene que bajar a '0'.
    
3. Durante ese brevísimo instante de retraso (el hueco marcado con el símbolo $\Delta$), se da una condición especial: **tanto `b` como `c` valen '1' al mismo tiempo**.
    
4. Como la compuerta verde es una AND, al recibir esos dos '1' simultáneos en sus entradas, dispara un pulso en su salida (**`d`**) extremadamente corto (el pico vertical que ves arriba con el punto rojo).

Ese pulso microscópico `d` es el que se conecta finalmente al pin `clk` del biestable R-S.

Básicamente, este diseño "engaña" a un biestable normal. Agarra una señal de reloj que sube y se queda en nivel alto durante mucho tiempo, y la exprime hasta convertirla en un "pinchazo" de energía que dura solo una fracción de segundo. Así, obliga al biestable a activarse y leer las entradas S y R de forma ultra-rápida, logrando que reaccione únicamente en el instante exacto del flanco.

![[Pasted image 20260925010322.png]]


¡Exactamente! Hiciste un resumen perfecto de las dos filosofías de diseño. Ambas estrategias logran el mismo objetivo (que el circuito reaccione solo en el salto), pero lo hacen con mecánicas físicas completamente distintas:

- **El sistema Maestro-Esclavo (Sincronización lógica):** Utiliza dos circuitos que funcionan "por nivel", pero desfasados. El maestro lee la información durante el nivel bajo ('0') y el esclavo la bloquea. En el instante exacto del **flanco** (el salto a '1'), ocurre el "cambio de guardia": el maestro se bloquea reteniendo la información, y el esclavo se abre para dejarla salir. Juegan en equipo para asegurar que el dato final solo cambie en ese punto de transición.
    
- **El sistema de retardo "Edge Triggered" (Sincronización física):** Es una estrategia más directa. Toma un circuito normal y usa el retardo físico de la compuerta NOT para exprimir la señal de reloj, convirtiéndola en un pulso microscópico. Como bien dijiste, esto obliga al biestable a despertarse **una sola vez y por un instante tan fugaz** que físicamente solo tiene tiempo de leer las entradas durante el flanco positivo, volviendo a cerrarse casi de inmediato.

Ambos son trucos brillantes de la ingeniería digital para domar el tiempo y asegurar que millones de componentes dentro de una computadora se actualicen en el mismo microsegundo exacto sin pisarse entre sí.


Esa es exactamente la principal diferencia práctica entre ambas arquitecturas, y tiene un impacto enorme en la ventana de tiempo que tienen disponible para "escuchar" la información.

En el **sistema Maestro-Esclavo**, la ventana de lectura es amplia. El circuito Maestro está activo y reaccionando a las entradas $S$ y $R$ durante **todo el tiempo que dura el nivel bajo ('0')**. Si mientras el reloj está en '0' cambiás los valores de entrada varias veces, el Maestro va a registrar todos esos cambios internamente. Recién en el instante del salto a '1', el Maestro cierra sus puertas y "congela" el último valor que llegó a leer para pasárselo al Esclavo.

En el **sistema "Edge Triggered" por retardo**, la ventana de lectura es drásticamente menor. El circuito ignora tus entradas durante todo el nivel '0' y todo el nivel '1'. Únicamente se despierta y permite el ingreso de datos durante ese **instante microscópico ($\Delta$)** que dura el pulso generado por la compuerta NOT.

Esta diferencia hace que el diseño por retardo sea mucho más robusto frente a errores transitorios (conocidos como _glitches_). En un Maestro-Esclavo, si hay un pico de ruido eléctrico en los cables de entrada mientras el reloj está en '0', el Maestro podría asimilarlo accidentalmente. En el diseño por retardo, como la puerta lógica solo se abre por una fracción de nanosegundo, es estadísticamente mucho más difícil que una interferencia indeseada logre colarse justo en ese milisegundo exacto.

![[Pasted image 20260925010446.png]]

Esta imagen muestra cómo se le agregan **entradas de anulación o emergencia** a un biestable sincronizado, conocidas como Entradas Asincrónicas.

Estas nuevas terminales se llaman **Pr (Preset)** para forzar un 1 en la memoria, y **Cl (Clear)** para forzar un 0. Se denominan "asincrónicas" porque **no necesitan esperar al reloj (`clk`)** para actuar. Mientras que las entradas normales R y S tienen que esperar a que el reloj les dé permiso a través de las compuertas AND de la izquierda, las señales Pr y Cl ingresan mediante compuertas OR que están ubicadas _después_ de la barrera del reloj, inyectando la orden directo en el núcleo del circuito.

La tabla de verdad inferior demuestra esta prioridad absoluta utilizando la letra **X**, que en lógica digital significa "no importa qué valor tenga" (Don't Care):

- Si activás el Preset (`Pr = 1` y `Cl = 0`), la salida $Q_{n+1}$ será 1 de manera instantánea, sin importar (X) en qué nivel esté el reloj o qué valores tengan R y S en ese momento.
    
 
- Si activás el Clear (`Pr = 0` y `Cl = 1`), la salida se borra a 0 al instante, ignorando por completo al reloj y a las entradas normales.
    
- Si ambas entradas de emergencia están apagadas (`Pr = 0` y `Cl = 0`), el biestable retoma su funcionamiento normal y vuelve a obedecer a las señales R, S y al reloj.
    
- Si intentás mandar la orden de forzar un 1 y forzar un 0 al mismo tiempo (`Pr = 1` y `Cl = 1`), el circuito entra en el clásico estado "Prohibida", generando un error lógico.

En la práctica, la entrada `Cl` (Clear) es el equivalente funcional al botón físico de "Reset" en el gabinete de una computadora: suprime y puentea cualquier cálculo normal que se esté ejecutando en ese milisegundo y fuerza a todos los componentes a volver a un estado inicial en cero para arrancar en limpio.



¡Exactamente! Esa es la forma perfecta de verlo. Tienen **prioridad absoluta** sobre todo el resto del circuito.

Al estar conectadas a través de esas compuertas OR que están ubicadas después de la barrera del reloj, las señales asincrónicas `Pr` y `Cl` actúan como una orden de "fuerza mayor".

Por eso en la tabla de verdad aparecen tantas **X** cuando `Pr` o `Cl` valen 1. Esa X (Don't Care) demuestra esa prioridad: al circuito literalmente no le importa si el reloj está subiendo, bajando, o si en las entradas normales R y S hay un 0 o un 1. Si vos activás el Preset o el Clear, el circuito interrumpe inmediatamente cualquier proceso sincronizado que estuviera haciendo y obedece esa orden directa para forzar el 1 o el 0 en la memoria.

Es el mismo concepto que un botón de "parada de emergencia" en una máquina: no importa qué instrucciones normales esté recibiendo el motor en ese momento, si tocás la emergencia, la máquina ignora todo lo demás y acata esa única orden al instante.







Pensá en la mecánica de una partida de un juego táctico como Counter-Strike o Valorant para entender la diferencia en cómo reaccionan a las entradas.

**Sistema Maestro-Esclavo (Ventana de tiempo amplia)**

Funciona como la "Fase de Compra" antes de que caigan las barreras. Durante esos segundos previos (mientras el reloj se mantiene en un nivel estable), el sistema Maestro está completamente abierto y escuchando. En esa ventana de tiempo podés alterar tus entradas todas las veces que quieras: comprar un arma, arrepentirte, venderla y comprar otra. El Maestro absorbe y registra todas esas fluctuaciones. Recién en el instante en que el tiempo se acaba y cae la barrera (el flanco de bajada), tu decisión final se congela y el sistema Esclavo se abre para publicar ese inventario definitivo en la ronda activa.

  

**Sistema Edge-Triggered (Instante microscópico)**

Funciona como sacar una captura de pantalla pulsando la tecla F12. No existe una "fase" previa en la que el circuito esté asimilando información. El sistema simplemente dispara un flash ultrarrápido y captura el estado exacto de tus entradas en ese milisegundo puntual. Cualquier cambio que hayas hecho un nanosegundo antes o un nanosegundo después de apretar el botón, el circuito lo ignora por completo.

  
Respecto a tu segunda duda: **sí, por supuesto que podés tener varias entradas.**

Acá es fundamental separar dos conceptos que en los esquemas a veces se mezclan:


- **Qué función lógica cumple:** Esto determina tu cantidad de entradas de datos. Un biestable R-S o J-K va a tener dos entradas principales. Un D o T va a tener solo una.
    
- **Cómo se sincroniza con el reloj:** Esto es el Maestro-Esclavo o el Edge-Triggered. Es la arquitectura de seguridad que gestiona el tiempo.
    

Podés construir perfectamente un biestable J-K (que procesa dos variables a la vez) utilizando una arquitectura Maestro-Esclavo. En ese caso, el circuito Maestro interno tendría conectados los cables J y K. El sistema Maestro-Esclavo solo dicta las reglas de _cuándo_ y _cómo_ se habilita el paso del tiempo, pero no impone ninguna restricción sobre _cuántas_ entradas de datos lógicos podés conectar.