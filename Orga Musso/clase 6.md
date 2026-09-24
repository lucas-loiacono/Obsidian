
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

![[Pasted image 20260924020913.png]]

![[Pasted image 20260924021113.png]]