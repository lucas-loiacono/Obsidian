
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


habilitación lee la entrada, si mi A0 =1 la salida 1 va a estar activa y la de 0 no, ósea mis respectivos c

![[Pasted image 20260922080408.png]]

![[Pasted image 20260922080442.png]]

![[Pasted image 20260922080644.png]]

![[Pasted image 20260922081910.png]]

![[Pasted image 20260922082017.png]]

![[Pasted image 20260922082130.png]]

![[Pasted image 20260922082448.png]]

![[Pasted image 20260922082640.png]]

![[Pasted image 20260922082745.png]]

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


![[Pasted image 20260924162839.png]]

![[Pasted image 20260924162956.png]]

![[Pasted image 20260924163121.png]]