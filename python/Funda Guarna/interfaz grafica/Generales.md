# Sticky vs Anchor

Sticky
sticky pega el widget completo a la direccion que le marque
``` python
# El texto está centrado en el cartel por defecto
cartel = Label(miframe, text="Hola", width=50, bg="red")

# Empujamos TODO EL CARTEL ROJO contra la pared derecha de la celda
cartel.grid(row=0, column=0, sticky="e") 
```

_Resultado:_ Ves un bloque rojo entero pegado a la derecha, y la palabra "Hola" en el medio de ese bloque rojo.

**Caso 2: Usando solo `anchor`**

``` python
# El cartel está fijo, pero empujamos el texto hacia la derecha DEL CARTEL
cartel = Label(miframe, text="Hola", width=50, bg="blue", anchor="e")

# El cartel se queda en el centro de la celda por defecto
cartel.grid(row=0, column=0) 
```


# yo siempre que quiero interactuar con la variable de un entry tengo que llamar a un boton para que tome "una fotografía" del momento y saque los datos de ahi

¡Qué buena analogía! Me encantó lo de "tomar una fotografía". Sí, para el 90% de los casos funciona exactamente así.

En la programación orientada a eventos (como Tkinter), el programa se queda esperando en pausa gracias a ese `mainloop()` del final. El recuadro del `Entry` es como una persona posando frente a la cámara, y el `Button` es el disparador del fotógrafo. Hasta que el usuario no hace "clic" (que llama a la función) y ejecutás el `.get()`, a tu programa por detrás no le importa qué está pasando adentro de esa caja de texto.

**¿Es la única forma de sacar la foto?** No, no siempre _necesitás_ un botón visible, pero sí necesitás un **evento** que le avise a tu código que es hora de recolectar los datos. Por ejemplo:

1. **El fotógrafo (El Botón):** Hacés clic en "Enviar", llama a la función, hace el `.get()` y valida. Es la que usaste vos y es perfecta para formularios.
    
2. **El temporizador (Tecla Enter):** En vez de hacer clic en un botón, podés programar la ventana para que tome la foto justo cuando el usuario aprieta la tecla `Enter` estando parado en el recuadro de texto (en Tkinter se hace "bindeando" la tecla `<Return>`).
    
3. **La cámara de seguridad (Tiempo real):** Hay una forma más avanzada donde no sacás fotos, sino que estás "filmando". Se le puede conectar un "espía" (un método llamado `trace`) directamente a tu `StringVar()`. De esta forma, _cada vez que el usuario teclea o borra una sola letra_, tu programa se entera al instante. Esto se usa un montón para esas barras de búsqueda de Google o de tiendas que te van filtrando resultados en vivo mientras vas escribiendo.
    

Pero para lo que es ingresos de datos estructurados, validaciones y altas en bases de datos (como tu formulario), **la lógica de la fotografía con el botón es la ideal y la que se usa siempre**. El usuario llena todo a su ritmo, y cuando está 100% seguro, te manda la señal para que vos captures la foto final.



# siempre que quiero trabajar con el valor de una variable del entry tengo que hacer un get

Siempre que quieras extraer el texto para usarlo en tu lógica de Python (para un `if`, para guardarlo en una base de datos, o para imprimirlo), **tenés que usar el `.get()`**.

¿Por qué es obligatorio? Porque las variables de Tkinter (como el `StringVar()`) o los recuadros de `Entry` **no son textos normales** de Python, son objetos especiales que se comunican con la interfaz gráfica.

Fijate la diferencia:

- **Si hacés `print(nombre)`:** Python te va a devolver el código interno del objeto en la memoria (algo rarísimo como `PY_VAR1` o `<tkinter.StringVar object>`). ¡No te da el texto!
    
- **Si hacés `print(nombre.get())`:** Ahí sí actúa el fotógrafo. Va al recuadro, extrae lo que dice adentro, y te devuelve un `string` de texto normal (por ejemplo, `"Lucas"`) que tu código sí entiende y puede manipular.
    

**El dato extra (la operación inversa):** Así como usás `.get()` para "sacar" la foto y leer el dato, si alguna vez querés que el código escriba algo automáticamente adentro de ese recuadro, usás su hermano gemelo: **`.set()`**. Por ejemplo: `nombre.set("Escriba aquí")` llenaría el recuadro con ese texto.