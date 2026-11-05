
![[Pasted image 20261021140857.png]]

![[Pasted image 20261021142245.png]]

![[Pasted image 20261021142514.png]]

![[Pasted image 20261021162448.png]]

Los componentes de la arquitectura de Von Neumann ilustrados en la imagen cumplen las siguientes funciones fundamentales:

- **Memory Unit**: Almacena tanto los datos a procesar como las instrucciones de los programas en ejecución, manteniéndolos disponibles para la computadora.
    
- **Arithmetic and Logic Unit (ALU)**: Ejecuta todas las operaciones matemáticas (sumas, restas) y evaluaciones lógicas (comparaciones, AND, OR) necesarias para procesar la información.
    
- **Control Unit**: Coordina el funcionamiento del sistema leyendo las instrucciones de la memoria, interpretándolas y enviando señales de mando al resto de las unidades para su ejecución.
    
- **Input Unit**: Recibe la información y los comandos ingresados desde el exterior hacia el sistema central (por ejemplo, a través de un teclado o un sensor).
    
- **Output Unit**: Entrega o muestra los resultados del procesamiento de datos hacia el exterior (por ejemplo, a través de una pantalla o impresora).

Lo característica de Von Neumann es que los programas se almacenan en la memoria juntos con los datos a procesar


Bus de sistema es compartir el medio físico donde se van a compartir los datos de información y las direcciones de memoria

El **Bus de Sistemas** funciona como un canal único de comunicación que centraliza la conexión entre los componentes principales de la computadora (la CPU, la Memoria y las unidades de Entrada/Salida). Su función principal es reducir la cantidad de rutas individuales necesarias para que estos elementos se comuniquen entre sí, permitiendo la transferencia de datos de forma más eficiente.


Para gestionar esta transferencia y mapear físicamente las posiciones de memoria, el bus de sistema se divide en tres líneas o sub-buses especializados:

- **Bus de Direcciones (Address Bus):** Transporta el número o «dirección» que identifica de manera única la posición específica en el mapa de memoria (o el dispositivo de E/S) a la que la CPU quiere acceder para leer o escribir.
    
- **Bus de Datos (Data Bus):** Es el canal por el que viaja la información o los datos reales (el contenido) una vez que se ha localizado la dirección correcta.
    
- **Bus de Control (Control Bus):** Transmite las señales de mando que indican qué acción se debe realizar (por ejemplo, si la CPU quiere "leer" de la memoria o "escribir" en ella) y coordina el tráfico para que la información no colisione.

![[Pasted image 20261021162852.png]]

Imagina el interior de tu computadora como una gran ciudad logística. El **bus del sistema** es la autopista principal que conecta los edificios más importantes: la oficina de gerencia (CPU), el enorme depósito de archivos (Memoria) y las puertas de carga y descarga hacia el exterior (Entrada/Salida). En lugar de construir cientos de calles privadas entre cada par de edificios, todos comparten esta gran autopista central para comunicarse.

  

Esta autopista está dividida en tres carriles altamente especializados que trabajan en equipo para cada tarea:

  

- **Bus de Direcciones (El sistema GPS):** Transmite las coordenadas exactas. Si la CPU necesita buscar un documento en el depósito, utiliza este carril para enviar la dirección exacta (por ejemplo, pasillo 4, estante 12) del lugar preciso al que necesita acceder.
    
      
    
- **Bus de Datos (Los camiones de carga):** Transporta la mercancía real. Una vez que el bus de direcciones ubica el destino, los camiones viajan por este carril llevando la información, ya sea transportando un dato crudo hacia la CPU para procesarlo, o llevando un resultado terminado hacia la memoria para guardarlo.
    
      
    
- **Bus de Control (Los semáforos y órdenes de trabajo):** Gestiona el tráfico y las reglas. Coordina los tiempos (la señal de reloj) para que los camiones no colisionen y lleva el formulario con la orden exacta de lo que hay que hacer al llegar: "Vengo a retirar un archivo (Lectura)" o "Vengo a depositar una caja (Escritura)".




El cambio en las flechas del **bus de direcciones** (Address Bus) indica que el flujo de información en este canal es **unidireccional** (viaja en un solo sentido), a diferencia del bus de datos que es bidireccional.

Esto ocurre por la forma en que se comunican los componentes:

- **La CPU es quien dirige:** Como indica la diapositiva, la señal del bus de direcciones deriva de la unidad solicitante, que generalmente es el procesador (CPU). La CPU es la única encargada de generar y enviar el número de dirección para especificar exactamente a qué elemento quiere acceder.
    
- **La Memoria y el I/O solo reciben:** La Memoria y las unidades de Entrada/Salida actúan como receptores en este paso. Solo reciben la dirección enviada por la CPU para saber dónde ubicarse. Nunca le envían una dirección de memoria a la CPU.
    

Por el contrario, el **bus de datos** tiene flechas hacia arriba y hacia abajo porque se utiliza para transferir información en ambas direcciones entre la unidad que solicita y la unidad con la que se completa la transferencia (dependiendo de si la CPU está pidiendo leer un archivo o enviando uno para guardarlo).

# Bus de interrupción

Las **líneas de interrupción** (a menudo agrupadas conceptualmente dentro del Bus de Control) son parte de las funciones y señales obligatorias que requiere el sistema de bus de hardware para funcionar correctamente.

Siguiendo la analogía de la ciudad logística, la línea de interrupción funciona como un **teléfono rojo de emergencias** directo a la oficina de gerencia (CPU). Su funcionamiento es el siguiente:

  
- **Aviso inmediato:** Sirven para que los dispositivos periféricos (como el teclado, el mouse o una placa de red) le avisen a la CPU que necesitan atención inmediata, sin tener que esperar su turno.
    
- **Eficiencia:** Evitan que la CPU tenga que gastar tiempo preguntando constantemente a cada dispositivo "¿necesitas algo?" (un proceso ineficiente conocido como _polling_).
    
- **Pausa y retoma:** Cuando un dispositivo envía una señal por esta línea, la CPU pausa temporalmente el programa que está ejecutando, guarda su estado actual, atiende la petición urgente (por ejemplo, registrar qué tecla presionaste) y, una vez resuelto, retoma su trabajo original exactamente donde lo dejó.

![[Pasted image 20261022011723.png]]

La imagen "image_f7141f.png" define la función fundamental de la CPU, la cual se resume en una tarea principal: ejecutar programas.

Para llevar a cabo esta ejecución, el procesador realiza una secuencia continua de cuatro pasos:

1. **Buscar (Fetch):** Accede a la memoria para buscar la próxima instrucción que debe ser ejecutada.
    
2. **Decodificar (Decode):** Analiza e interpreta el código de operación de esa instrucción específica para entender qué acción matemática o lógica se requiere.
    
3. **Ejecutar (Execute):** Lleva a cabo la instrucción.
    
4. **Repetir:** Vuelve al primer paso para continuar con la siguiente instrucción de forma indefinida.

Este proceso estructurado se denomina formalmente **«ciclo de búsqueda-ejecución»** o **ciclo de «fetch»**.

En la parte inferior, la diapositiva recupera el diagrama de la Arquitectura de Bus de Sistemas (CPU, Memoria y dispositivos de Entrada/Salida conectados a través de los buses de Datos, Direcciones y Control). Este esquema ilustra la infraestructura de hardware sobre la cual ocurre este ciclo constantemente, mostrando por dónde viajan las direcciones para buscar las instrucciones y por dónde regresan los datos para ser decodificados y ejecutados.


![[Pasted image 20261022012450.png]]

La imagen "image_f775d9.png" ilustra un ejemplo de un **mapa de memoria** a nivel de microarquitectura, detallando cómo se estructura lógicamente el almacenamiento y cómo interactúa con los buses del sistema.

  

El diagrama se organiza en tres secciones principales:


- **Mapa de Memoria (Izquierda):** Representa la disposición interna de la memoria, donde cada posición almacena datos de 32 bits (divididos en bytes) y se ubica mediante una dirección (Address) que va desde 0 hasta $2^{32}-1$. Este gran bloque se subdivide en áreas con propósitos específicos:
    
      
    - **Reservado para el sistema operativo:** Ocupa el bloque inicial desde la dirección 0 hasta la 2047.
        
          
        
    - **Espacio de usuario (User Space):** Comienza a partir de la dirección 2048, destinado a los programas y aplicaciones del usuario.
        
          
        
    - **Pila del sistema (System Stack):** Un área delimitada por el fondo de la pila (Bottom of stack) en la dirección $2^{31}-4$ y cuyo tope es indicado dinámicamente por un puntero de pila (Stack pointer).
        
          
        
    - **Espacio de Entrada/Salida (I/O space):** Ubicado en las direcciones finales (hasta $2^{32}-4$), donde las posiciones de memoria se mapean directamente a periféricos de hardware como el disco, la terminal y la impresora.
        
          
        
- **Interfaz de Memoria (Centro):** Muestra el bloque conceptual de la memoria recibiendo las señales que provienen de los buses: direcciones (Address), control y datos de entrada (Data In). A su vez, emite la información solicitada a través de la línea de salida de datos (Data Out).
    
      
    
- **Contexto del Sistema (Derecha):** Recupera el esquema de la Arquitectura de Bus de Sistemas, mostrando cómo este bloque de memoria central se interconecta con la CPU y las unidades de I/O mediante los buses de datos, direcciones y control.





Tiene mucho sentido. El diagrama ilustra exactamente cómo un **procesador de 32 bits** (en este caso, de la arquitectura ARC) "ve" y organiza la memoria.

El mapa de memoria siempre está definido por la arquitectura del procesador que lo utiliza. Como se trata de un procesador de 32 bits, el diagrama refleja directamente sus reglas de diseño y limitaciones en el hardware:

  

- **Capacidad de direccionamiento:** Un procesador de 32 bits utiliza un bus de direcciones de ese mismo tamaño, lo que le permite apuntar a un máximo de $2^{32}$ ubicaciones únicas. Por eso, el mapa a la izquierda comienza en la dirección 0 y su límite exacto en la parte inferior es $2^{32}-1$.
    
      
    
- **Ancho de palabra:** La arquitectura procesa y transfiere la información en bloques de 32 bits, lo cual se indica explícitamente en la parte superior de la columna de datos del mapa.
    
      
    

Por lo tanto, aunque el bloque central representa el hardware de almacenamiento (la memoria RAM), la estructura lógica del mapa y la división de los espacios (espacio de usuario, sistema operativo, pila, entrada/salida) son la plantilla impuesta por el procesador ARC de 32 bits para poder trabajar con ella.






El procesador necesita su propia memoria interna porque la memoria RAM principal es demasiado lenta y está físicamente muy lejos para seguirle el ritmo de trabajo. Si un procesador moderno, como un Ryzen de la serie 5000, tuviera que viajar por la placa madre a través del bus del sistema hacia la RAM para cada simple instrucción, pasaría la mayor parte de su tiempo inactivo, simplemente esperando a que lleguen los datos.

  

Para resolver este cuello de botella y no frenar el procesamiento, la arquitectura de las computadoras utiliza una jerarquía de memoria basada en la velocidad y la cercanía:

  

- **Registros:** Son la memoria más rápida y pequeña que existe, construida directamente con flip-flops y circuitos secuenciales dentro de la propia CPU. Son las "manos" del procesador: guardan los datos exactos que la ALU está calculando o comparando en ese microsegundo preciso.
    
      
    
- **Memoria Caché (L1, L2, L3):** Es un almacenamiento intermedio súper rápido integrado en el chip del procesador. Como ir a la RAM "cuesta" mucho tiempo, la CPU adivina qué datos vas a necesitar a continuación y trae bloques enteros desde la RAM hacia la caché.
    
      
    
- **Memoria RAM (La Principal):** Es el bloque grande central que veíamos en los diagramas. Tiene muchísima capacidad para mantener abiertos el sistema operativo y todos tus programas, pero la latencia para buscar un dato hasta ahí es de decenas o cientos de ciclos de reloj.
    
      
    

Retomando la analogía de la ciudad logística: si la RAM es el inmenso depósito de archivos al otro lado de la autopista, los registros y la caché son los bolsillos y el escritorio personal del gerente. Tienen muy poco espacio de almacenamiento, pero el acceso a la información que está ahí mismo es instantáneo.


![[Pasted image 20261022013609.png]]

![[Pasted image 20261022013742.png]]

Si empiezas en la dirección 0, la siguiente celda completa (la fila de abajo) es la **4**.

  

Esto ocurre porque la memoria se direcciona **por bytes** (cada número de dirección guarda 8 bits), pero cada fila del mapa tiene un ancho de **32 bits** (4 bytes). Por lo tanto, la primera fila contiene internamente los bytes 0, 1, 2 y 3; la fila de abajo contiene el 4, 5, 6 y 7, y así sucesivamente (los saltos para leer una palabra completa de 32 bits van de 4 en 4).

  

Las distintas secciones que dividen este mapa de memoria son:

  

- **Reserved for operating system (0 a 2047):** Espacio bloqueado y dedicado exclusivamente para las rutinas e instrucciones del sistema operativo.
    
      
    
- **User Space (2048 en adelante):** Área libre donde se cargan en la memoria los programas ensambladores y aplicaciones que tú escribes y ejecutas.
    
      
    
- **System Stack (Pila del Sistema):** Su base o fondo (Bottom of stack) se ubica en la dirección $2^{31}-4$. A medida que el programa apila datos (por ejemplo, al llamar funciones), la pila crece hacia direcciones con números menores, siendo rastreada dinámicamente por el puntero de pila (Stack pointer).
    
      
    
- **I/O Space (Entrada/Salida mapeada):** Ocupa el extremo final de las direcciones (hasta $2^{32}-4$). Escribir o leer en estas posiciones de memoria no guarda un dato tradicional, sino que envía o recibe información directamente del hardware físico de los periféricos, como el disco (Disk), la consola (Terminal) o la impresora (Printer).

![[Pasted image 20261022013817.png]]

La microarquitectura de la CPU mostrada en la imagen se compone de las siguientes partes fundamentales:

  
- **Unidad de Control (Control Unit):** Ubicada en la sección de control (Control Section), es el componente coordinador responsable de dirigir y controlar la ejecución de las instrucciones implementando el ciclo de fetch.
    
      
    
- **ALU (Unidad Aritmético Lógica):** Se encuentra dentro de la sección de datos y es el componente de cálculo encargado de realizar todas las operaciones aritméticas y lógicas.
    
      
    
- **Registros (Registers):** Son pequeñas memorias internas de alta velocidad conectadas directamente a la ALU, que abarcan tanto los registros visibles para el programador como los registros internos que requiere la unidad de control para funcionar.
    
      
    
- **Datapath (Sección de Datos):** Es el bloque estructural que agrupa a la ALU y los registros, conformando el área dedicada exclusivamente a la manipulación y procesamiento de los datos.
    
      
    
- **System Bus (Bus del Sistema):** Es la autopista de comunicación externa a la que se conecta la CPU para poder interactuar y transferir información con el resto de la computadora (como la Memoria RAM y los periféricos).



Los componentes internos de la CPU se comunican a través de rutas de datos y líneas de señales de control, representadas en el diagrama por las flechas bidireccionales:

  

- **Registros y ALU (Dentro del Datapath):** Se comunican de forma directa e inmediata. Los registros envían los números o datos crudos hacia la ALU, y una vez que la ALU realiza la operación matemática o lógica, envía el resultado de vuelta por la misma ruta interna para guardarlo nuevamente en un registro.
    
      
    
- **Unidad de Control y Datapath:** Se comunican mediante un intercambio de órdenes y estados a través de la flecha horizontal que los une. La Unidad de Control envía las señales que dictan exactamente qué operación debe hacer la ALU y qué registros debe habilitar, mientras que el Datapath (como respuesta) le informa sobre el estado de ese cálculo.
    
      
    
- **CPU y el exterior (System Bus):** La interfaz inferior conecta estructuralmente tanto a la Unidad de Control como al Datapath con el Bus del Sistema. Esta conexión permite que la CPU interactúe con el exterior, enviando direcciones y recibiendo instrucciones o datos desde la Memoria RAM a través de los canales de la placa madre.



La Unidad de Control funciona como el director de la CPU, interpretando cada instrucción y enviando las señales de mando que dictan qué operación realizar y qué registros específicos habilitar. Por su parte, el Datapath (que agrupa a los registros y la ALU) actúa estrictamente como el ejecutor físico. Estos componentes se limitan a recibir la información, obedecer las señales de control para ejecutar el cálculo matemático o lógico correspondiente, y devolver el resultado procesado.

![[Pasted image 20261022014527.png]]


La imagen "image_c6a9ca.png" hace un acercamiento al interior de la CPU para mostrar en detalle cómo está diseñado físicamente el **Trayecto de Datos** (Datapath). Es decir, ilustra el circuito interno por donde viaja la información entre los registros y la ALU durante la ejecución de una instrucción.

  

El diagrama muestra el siguiente circuito de funcionamiento:

  

- **Entrada de Datos:** La información proveniente de la memoria o el exterior ingresa por la izquierda ("From Data Bus") y se almacena en el **Register File** (el banco donde están agrupados todos los registros de la CPU).
    
      
    
- **Envío a la ALU (Fuentes):** Cuando se necesita hacer una operación, el archivo de registros envía los operandos hacia la ALU a través de dos canales principales: **Register Source 1 (rs1)** y **Register Source 2 (rs2)**.
    
      
    
- **El Rol del Control:** Las líneas finas negras ilustran cómo la Unidad de Control gobierna este sector. Es la encargada de enviar las señales para seleccionar qué registros específicos se van a usar ("Control Unit selects registers") y decirle a la ALU qué cálculo exacto debe realizar ("and ALU function").
    
      
    
- **Guardado del Resultado (Destino):** Una vez que la ALU procesa la información, el resultado sale por la parte inferior y vuelve a subir por el camino grueso llamado **Register Destination (rd)** para guardarse de nuevo en el archivo de registros.
    
      
    
- **Señales de Estado:** Al terminar el cálculo, la ALU también emite una señal hacia la derecha ("Status to Control Unit") para informarle a la Unidad de Control detalles sobre el resultado, como si la operación dio cero o si hubo un desbordamiento (overflow).
    
      
    
- **Conexiones de Salida:** El diagrama detalla que este trayecto interno se conecta de vuelta con el bus del sistema hacia el exterior: la línea _rs1_ se bifurca para enviar direcciones hacia la memoria ("To Address Bus"), y la línea _rs2_ se bifurca para enviar datos a guardar en la memoria ("To Data Bus").



![[Pasted image 20261022014823.png]]

La imagen "image_728fb5.png" ilustra el flujo completo de traducción que atraviesa un programa informático, desde su creación por un desarrollador hasta su ejecución física en el procesador. Este proceso de transformación desciende a través de tres niveles de abstracción:

**Lenguaje de Alto Nivel** Es el punto de partida del flujo, diseñado con una sintaxis cercana a la lógica humana matemática y estructurada. El diagrama lo ejemplifica con un fragmento clásico de código en lenguaje C, donde se declaran variables (`char operando = 26;`), se realizan sumas y se imprime un resultado por pantalla. La ventaja principal de este nivel es que es **independiente del hardware**. Permite programar sin necesidad de conocer la arquitectura interna del procesador que ejecutará el programa.


**Assembler (Lenguaje Ensamblador)** Mediante el proceso de **compilación**, el código de alto nivel se traduce a Assembler. Este lenguaje representa el conjunto de instrucciones nativas de la CPU, pero utilizando "símbolos significativos para humanos" (mnemotécnicos) en lugar de números puros, tales como `Add` (sumar), `mul` (multiplicar) y operaciones lógicas como `and`. Como advierte la nota inferior del diagrama, para programar directamente en esta etapa se **necesita conocer cómo está organizada la memoria** y la arquitectura de la CPU, ya que las instrucciones operan de manera directa sobre los registros físicos del hardware.

**Código de Máquina** En el paso final, un proceso llamado **ensamblado** traduce las instrucciones de Assembler al Código de Máquina. Este es el único lenguaje que la CPU puede procesar y ejecutar, compuesto exclusivamente por una **secuencia de 0s y 1s**. La diapositiva proporciona un ejemplo directo de esta conversión lógica: la instrucción simbólica de Assembler `Add r0, r1, r2` se ensambla transformándose literalmente en la cadena binaria `0110101110101101`. Esta secuencia final es la que la Unidad de Control leerá, decodificará y enviará a la ALU para realizar el cálculo.

![[Pasted image 20261022014858.png]]

La imagen "image_c55103.png" define conceptualmente qué es el **Mapa de Memoria de un Sistema** y establece la diferencia clave entre los límites físicos que impone el hardware y las decisiones de diseño del sistema.

  

Según la diapositiva, el mapa de memoria representa la asignación específica que se le da al espacio de direcciones. Para entender cómo se diseña este mapa, el texto y el recuadro de la derecha destacan dos reglas fundamentales:

  

- **El procesador define el tamaño (El rango máximo):** El tamaño total del espacio direccionable es específico del procesador. Es la CPU la que impone el límite de cuántas direcciones pueden existir (por ejemplo, de 0 a $2^{32}-1$ en un procesador de 32 bits).
    
      
    
- **El sistema define la organización (La función asignada):** El tipo específico de computadora (el sistema) es quien decide cómo se divide y para qué se utiliza cada segmento de ese espacio disponible. Por esta razón, el mapa de memoria es específico de un sistema. Como conclusión importante, la diapositiva señala que dos sistemas distintos basados exactamente en el mismo procesador no tienen necesariamente el mismo mapa de memoria.
    
      
    

Finalmente, la diapositiva aborda los **Dispositivos de entrada/salida (I/O)**. Aclara que a estos periféricos también se accede mediante direcciones, pero su ubicación depende del diseño elegido por el sistema: pueden estar ubicados dentro del mismo espacio de direcciones que la memoria (como se ilustra en la zona inferior del gráfico, conocida como E/S mapeada en memoria) o pueden no estarlo.


![[Pasted image 20261022014916.png]]

La imagen "image_c54d87.png" es idéntica a la diapositiva que analizamos anteriormente sobre la **Arquitectura ARC (A RISC Computer)**, la cual resume las reglas fundamentales de cómo este procesador de 32 bits interactúa con la memoria.

Aquí tienes el desglose de sus características principales:

- **RISC:** Significa "Reduced Instruction Set Computer" (Computadora con Conjunto de Instrucciones Reducido).
    
- **Capacidad y Almacenamiento:** Es una máquina de 32 bits que puede manejar datos de ese tamaño, pero su memoria está organizada y es direccionable por bytes (bloques de 8 bits).
    
- **Sistema Operativo:** Las primeras 2048 posiciones de memoria están reservadas estrictamente para el sistema operativo.
    
- **Espacio de Usuario (User Space):** Es la zona donde se cargan los programas ensambladores que crea el usuario.
    
- **Pila del Sistema (System Stack):** Su base está en la dirección $2^{31}-4$ y crece hacia direcciones inferiores de memoria a medida que se apilan los datos.
    
- **Entrada/Salida (I/O Space):** La arquitectura utiliza "entrada mapeada en memoria", lo que significa que reserva una zona al final de las direcciones de memoria para almacenar los datos de los dispositivos externos (como el disco, la terminal y la impresora).
    
- **Big Endian:** Para guardar una palabra de 32 bits, la arquitectura almacena el byte más significativo en la dirección de memoria más baja.

![[Pasted image 20261022014953.png]]

La imagen "image_c545c5.png" resume las especificaciones técnicas de la Arquitectura ARC, dividiéndolas en dos categorías principales: el manejo de la memoria y su set de instrucciones.

  

**Memoria**

  

- **Espacio de direcciones:** Posee un límite de $2^{32}$ posiciones direccionables.
    
      
    
- **Mapa de memoria:** Su estructura interna (con las zonas reservadas para el sistema operativo, espacio de usuario, pila y E/S) está dictada por el diagrama ubicado a la derecha de la diapositiva.
    
      
    
- **Ordenamiento:** Utiliza el formato **Big-endian** para almacenar información que ocupa más de un byte.
    
      
    

**Set de Instrucciones**

  

- **Base:** Este set es un subconjunto derivado de la arquitectura SPARC.
    
      
    
- **Tamaño fijo:** Absolutamente todas las instrucciones del procesador ocupan exactamente 32 bits.
    
      
    
- **Registros:** La CPU cuenta en su interior con un total de 32 registros, cada uno de ellos con una capacidad de 32 bits.
    
      
    
- **Program Status Register (PSR):** Es un registro especial dedicado exclusivamente a guardar los flags (banderas de estado) generados por la ALU tras realizar una operación.
    
      
    
- **Acceso a memoria (Modelo Load/Store):** Característico de las arquitecturas RISC, el procesamiento de datos se hace solo en los registros; por lo tanto, **solo dos instrucciones** pueden interactuar directamente con la memoria principal: una para leer de la memoria a un registro, y otra para escribir desde un registro hacia la memoria.







# Assemebler

![[Pasted image 20261022015009.png]]

![[Pasted image 20261022015027.png]]

La imagen "image_c3f3ad.png" detalla el banco de **Registros Accesibles al Programador** dentro de la CPU para la arquitectura ARC.

El diagrama muestra un conjunto principal de 32 registros, numerados del 00 al 31 y nombrados en el código con el prefijo `%` (desde `%r0` hasta `%r31`). Aunque la mayoría son de propósito general, la arquitectura tiene registros de uso predefinido:

- **`%r0`:** Es un registro que vale siempre cero (`[= 0]`).
    
- **`%r14`:** Funciona como el puntero de pila o _stack pointer_ (`[%sp]`).
    
- **`%r15`:** Actúa como el registro de enlace (`[link]`), encargado de almacenar la dirección de retorno de un procedimiento o función.

Adicionalmente, en la parte inferior se listan dos registros especiales separados, ambos con una longitud de 32 bits:

- **PC (`%pc`):** El contador de programa.
    
- **PSR (`%psr`):** El registro de estado del programa. El esquema en la base detalla los 32 bits de este registro (numerados del 31 al 00) y resalta una sección específica que contiene las letras **n, z, v, c**, las cuales representan las banderas (flags) generadas por la ALU.

![[Pasted image 20261022015043.png]]

![[Pasted image 20261022015059.png]]

![[Pasted image 20261022015313.png]]

![[Pasted image 20261022180325.png]]

![[Pasted image 20261022180346.png]]

![[Pasted image 20261022180359.png]]

![[Pasted image 20261022180429.png]]

![[Pasted image 20261022180505.png]]

![[Pasted image 20261022180701.png]]

![[Pasted image 20261022180721.png]]

![[Pasted image 20261022180806.png]]

![[Pasted image 20261022180826.png]]

![[Pasted image 20261022180940.png]]

![[Pasted image 20261022181002.png]]

![[Pasted image 20261022181838.png]]








# Practica

