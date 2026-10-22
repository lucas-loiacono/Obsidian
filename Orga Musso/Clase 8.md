
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