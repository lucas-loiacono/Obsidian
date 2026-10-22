
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